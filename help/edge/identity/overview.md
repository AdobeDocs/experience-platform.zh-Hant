---
title: 平台Web SDK中的身份資料
description: 瞭解如何使用Adobe Experience CloudWeb SDK檢索和管理Adobe Experience PlatformID(ECID)。
keywords: 身份；第一方身份；身份服務；第三方身份；ID遷移；訪問者ID；第三方身份；第三方CookieEnabled;idMigrationEnabled;getIdentity；同步身份；同步身份；sendIdentity;identityMap;primary;ecid;Identity Namespace;authenticationState;hashEnabled;
exl-id: 03060cdb-becc-430a-b527-60c055c2a906
source-git-commit: 0edd9422d6ea1b8e3aeaba1b24bc38b42ca809d8
workflow-type: tm+mt
source-wordcount: '1404'
ht-degree: 0%

---

# 平台Web SDK中的標識資料

Adobe Experience PlatformWeb SDK利用 [Adobe Experience CloudID(ECID)](../../identity-service/ecid.md) 追蹤訪客行為。 使用ECID，您可以確保每台設備具有唯一標識符，該標識符可以跨多個會話持續存在，從而將在Web會話期間和跨Web會話發生的所有命中與特定設備綁定。

本文檔概述了如何使用平台Web SDK管理ECID。

## 使用SDK跟蹤ECID

平台Web SDK通過使用cookie來分配和跟蹤ECID，並使用多種可用方法來配置這些cookie的生成方式。

當新用戶到達您的網站時，Adobe Experience Cloud身份服務會嘗試為該用戶設定設備標識cookie。 對於首次訪問者，在來自Adobe Experience Platform邊緣網路的第一響應中生成並返回ECID。 對於重複訪問者，從 `kndctr_{YOUR-ORG-ID}_AdobeOrg_identity` Cookie和邊緣網路添加到負載。

一旦設定了包含ECID的Cookie,Web SDK生成的每個後續請求將在 `kndctr_{YOUR-ORG-ID}_AdobeOrg_identity` 餅乾。

使用cookie進行設備標識時，您有兩個選項可與邊緣網路交互：

1. 直接將資料發送到邊緣網路域 `adobedc.net`。 此方法稱為 [第三方資料收集](#third-party)。
1. 在您自己的域上建立指向 `adobedc.net`。 此方法稱為 [第一方資料收集](#first-party)。

如下面各節所述，您選擇使用的資料收集方法會直接影響瀏覽器的cookie生存期。

### 第三方資料收集 {#third-party}

第三方資料收集涉及將資料直接發送到邊緣網路域 `adobedc.net`。

近年來，網路瀏覽器在處理第三方設定的Cookie時的限制越來越大。 預設情況下，某些瀏覽器會阻止第三方Cookie。 如果您使用第三方Cookie來標識站點訪問者，則這些Cookie的生命週期幾乎總是比使用第一方Cookie提供的時間短。 在某些情況下，第三方Cookie在七天內就會過期。

此外，當使用第三方資料收集時，某些廣告攔截器將流量限制為完全Adobe資料收集端點。

### 第一方資料收集 {#first-party}

第一方資料收集涉及通過您自己的域上的CNAME設定Cookie，該CNAME指向 `adobedc.net`。

雖然瀏覽器長期以類似於站點所有端點設定的方式處理由CNAME端點設定的Cookie，但瀏覽器最近實施的更改在處理CNAME Cookie的方式上造成了區別。 雖然預設情況下沒有當前阻止第一方CNAME Cookie的瀏覽器，但某些瀏覽器將使用CNAME設定的Cookie的生存期限限制為七天。

### 餅乾壽命對Adobe Experience Cloud應用的影響 {#lifespans}

無論您是選擇第一方還是第三方資料收集，Cookie可以持續的時間長短將直接影響Adobe Analytics和Customer Journey Analytics的訪問者人數。 此外，當站點上使用Adobe Target或Offer decisioning時，最終用戶可能會體驗到不一致的個性化體驗。

例如，考慮您建立個性化體驗的情況，如果用戶在過去七天中已三次查看任何項目，則此體驗會將其提升到首頁。

如果最終用戶一週內訪問三次，然後連續七天不返回站點，則當他們返回站點時，可能會將該使用視為新用戶，因為瀏覽器策略可能已刪除了他們的cookie（具體取決於他們訪問站點時使用的瀏覽器）。 如果出現這種情況，則您的分析工具將視訪問者為新用戶，即使訪問者在七天多一點之前訪問了該站點。 此外，將再次開始為用戶個性化體驗。

### 第一方設備ID

要考慮上述Cookie壽命計畫的影響，可以選擇設定和管理自己的設備標識符。 請參閱上的指南 [第一方設備ID](./first-party-device-ids.md) 的子菜單。

## 正在檢索當前用戶的ECID和區域

要檢索當前訪問者的唯一ECID，請使用 `getIdentity` 的子菜單。 對於尚未具有ECID的首次訪問者，此命令將生成新ECID。 `getIdentity` 也返回訪問者的區域ID。

>[!NOTE]
>
>此方法通常用於需要讀取 [!DNL Experience Cloud] ID或需要Adobe Audience Manager的位置提示。 標準實作不會使用此函數。

```javascript
alloy("getIdentity")
  .then(function(result) {
    // The command succeeded.
    console.log("ECID:", result.identity.ECID);
    console.log("RegionId:", result.edge.regionId);
  })
  .catch(function(error) {
    // The command failed.
    // "error" will be an error object with additional information.
  });
```

## 使用 `identityMap`

使用XDM [`identityMap` 場](../../xdm/schema/composition.md#identityMap)，您可以使用多個標識來標識設備/用戶，設定其身份驗證狀態，並確定將哪個標識符視為主標識符。 如果未將標識符設定為 `primary`，主預設值為 `ECID`。

`identityMap` 將使用 `sentEvent` 的子菜單。

```javascript
alloy("sendEvent", {
  xdm: {
    "identityMap": {
      "ID_NAMESPACE": [ // Notice how each namespace can contain multiple identifiers.
        {
          "id": "1234",
          "authenticatedState": "ambiguous",
          "primary": true
        }
      ]
    }
  }
});
```

內的每個屬性 `identityMap` 表示屬於特定 [標識命名空間](../../identity-service/namespaces.md)。 屬性名稱應為標識命名空間符號，您可以在Adobe Experience Platform用戶介面的「 」下找到[!UICONTROL 身份]。 屬性值應為與該標識命名空間相關的標識陣列。

>[!IMPORTANT]
>
>傳入的命名空間ID `identityMap` 區分大小寫。 確保使用正確的命名空間ID以避免不完整的資料收集。

標識陣列中的每個標識對象都包含以下屬性：

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `id` | 字串 | **（必需）** 要為給定命名空間設定的ID。 |
| `authenticationState` | 字串 | **（必需）** ID的驗證狀態。 可能的值為 `ambiguous`。 `authenticated`, `loggedOut`。 |
| `primary` | 布林值 | 確定是否應將此標識用作配置檔案中的主要片段。 預設情況下，ECID設定為用戶的主標識符。 如果省略，此值預設為 `false`。 |

使用 `identityMap` 欄位以識別設備或用戶導致的結果與使用 [`setCustomerIDs`](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/setcustomerids.html?lang=en) 的 [!DNL ID Service API]。 查看 [ID服務API文檔](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/get-set.html?lang=en) 的子菜單。

## 從訪問者API遷移到ECID

從使用訪問者API遷移時，您還可以遷移現有AMCV Cookie。 要啟用ECID遷移，請設定 `idMigrationEnabled` 的子菜單。 ID遷移可啟用以下使用情形：

* 當域的某些頁使用訪問者API而其他頁使用此SDK時。 為支援此情況，SDK會讀取現有AMCV Cookie，並使用現有ECID寫入新Cookie。 另外，SDK寫入AMCV Cookie，以便如果ECID是首先在SDK所檢測的頁面上獲得的，則隨訪API所檢測的後續頁面具有相同的ECID。
* 當Adobe Experience PlatformWeb SDK設定在同時具有訪問者API的頁面上時。 為支援此情況，如果未設定AMCVcookie,SDK將在頁面上查找訪問者API並調用它以獲取ECID。
* 當整個站點使用Adobe Experience PlatformWeb SDK且沒有訪問者API時，遷移ECID以保留返回訪問者資訊是非常有用的。 部署SDK後 `idMigrationEnabled` 在一段時間內，可以關閉設定，以便大多數訪問者cookie被遷移。

### 正在更新遷移特徵

當XDM格式化資料被發送到Audience Manager時，遷移時需要將該資料轉換為信號。 需要更新您的特徵，以反映XDM提供的新密鑰。 通過使用 [BAAAM工具](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/bulk-management-tools/bulk-management-intro.html#getting-started-with-bulk-management) Audience Manager創造的。

## 在事件轉發中使用

如果您當前 [事件轉發](../../tags/ui/event-forwarding/overview.md) 已啟用並正在使用 `appmeasurement.js` 和 `visitor.js`，您可以保持啟用事件轉發功能，這不會導致任何問題。 在後端，Adobe提取任AAM何段，並將它們添加到對Analytics的調用中。 如果對Analytics的調用包含這些段，Analytics將不調用Audience Manager轉發任何資料，因此不存在任何雙重資料收集。 使用Web SDK時也不需要位置提示，因為後端調用了相同的分段終結點。
