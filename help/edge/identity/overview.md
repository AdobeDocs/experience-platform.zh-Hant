---
title: Platform Web SDK中的身分資料
description: 瞭解如何使用Adobe Experience Platform Web SDK擷取和管理Adobe Experience Cloud ID (ECID)。
keywords: 身分；第一方身分；身分服務；第三方身分；ID移轉；訪客ID；第三方身分；thirdPartyCookiesEnabled；idMigrationEnabled；getIdentity；同步身分；syncIdentity；sendEvent；identityMap；主要；ecid；身分名稱空間；名稱空間id；authenticationState；hashEnabled；
exl-id: 03060cdb-becc-430a-b527-60c055c2a906
source-git-commit: e300e57df998836a8c388511b446e90499185705
workflow-type: tm+mt
source-wordcount: '1414'
ht-degree: 1%

---

# Platform Web SDK中的身分資料

Adobe Experience Platform Web SDK可運用 [Adobe Experience Cloud ID (ECID)](../../identity-service/ecid.md) 以追蹤訪客行為。 使用ECID，您可以確保每個裝置都有唯一識別碼，此識別碼可以跨多個工作階段持續存在，繫結特定裝置在Web工作階段期間和之間發生的所有點選。

本檔案概述如何使用Platform Web SDK管理ECID。

## 使用SDK追蹤ECID

Platform Web SDK可透過使用Cookie指派及追蹤ECID，並提供多種設定這些Cookie產生方式的可用方法。

當新使用者進入您的網站時，Adobe Experience Cloud Identity Service會嘗試為該使用者設定裝置識別Cookie。 首次造訪的訪客會在首次從Adobe Experience Platform Edge Network回應時產生並傳回ECID。 若為重複訪客，ECID會擷取自 `kndctr_{YOUR-ORG-ID}_AdobeOrg_identity` Cookie並由Edge Network新增至裝載。

包含ECID的Cookie設定完成後，Web SDK產生的每個後續請求都會在 `kndctr_{YOUR-ORG-ID}_AdobeOrg_identity` Cookie。

使用Cookie來識別裝置時，您有兩個選項可以與Edge Network互動：

1. 將資料直接傳送至Edge Network網域 `adobedc.net`. 此方法稱為 [協力廠商資料收集](#third-party).
1. 在您自己的網域上建立指向 `adobedc.net`. 此方法稱為 [第一方資料收集](#first-party).

如下節所述，您選擇使用的資料收集方法會直接影響各瀏覽器的Cookie存留期。

### 協力廠商資料收集 {#third-party}

第三方資料收集涉及將資料直接傳送至Edge Network網域 `adobedc.net`.

近年來，網頁瀏覽器在處理第三方設定的Cookie時，限制日益嚴格。 有些瀏覽器預設會封鎖第三方Cookie。 如果您使用第三方Cookie來識別網站訪客，則這些Cookie的存留期幾乎總是比使用第一方Cookie所能提供的短。 在某些情況下，第三方Cookie最快會在七天後過期。

此外，當使用第三方資料收集時，有些廣告封鎖程式會完全將流量限制在Adobe資料收集端點。

### 第一方資料收集 {#first-party}

第一方資料收集涉及透過您自己的網域上的CNAME將Cookie設定為 `adobedc.net`.

雖然瀏覽器長期以來以與網站擁有端點所設定類似的方式處理CNAME端點所設定的Cookie，但瀏覽器最近實作的變更對CNAME Cookie的處理方式造成差異。 雖然目前沒有瀏覽器預設會封鎖第一方CNAME Cookie，但有些瀏覽器會將使用CNAME設定的Cookie存留期限製為僅七天。

### Cookie有效期限對Adobe Experience Cloud應用程式的影響 {#lifespans}

無論您是選擇第一方還是第三方資料收集，Cookie能持續存在的時間長度會直接影響Adobe Analytics和Customer Journey Analytics中的訪客計數。 此外，在網站上使用Adobe Target或Offer Decisioning時，一般使用者可能會遇到不一致的個人化體驗。

例如，假設您已建立個人化體驗，且如果使用者在過去七天內檢視任何專案三次，此體驗會將任何專案提升至首頁。

如果一般使用者一週瀏覽三次，然後七天未返回網站，則該使用者在返回網站時可視為新使用者，因為其Cookie可能已遭到瀏覽器原則刪除（取決於使用者瀏覽網站時所使用的瀏覽器）。 如果發生這種情形，您的Analytics工具會將訪客視為新使用者，即使他們剛在7天多一點前造訪網站。 此外，為使用者個人化體驗的所有工作都將重新開始。

### 第一方裝置ID

如上所述，若要考慮Cookie有效期限的影響，您可以選擇設定並管理您自己的裝置識別碼。 請參閱以下指南： [第一方裝置ID](./first-party-device-ids.md) 以取得詳細資訊。

## 擷取目前使用者的ECID和區域

若要擷取目前訪客的唯一ECID，請使用 `getIdentity` 命令。 對於尚未擁有ECID的首次訪客，此命令會產生新的ECID。 `getIdentity` 也會傳回訪客的地區ID。

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

使用XDM [`identityMap` 欄位](../../xdm/schema/composition.md#identityMap)，您可使用多個識別碼來識別裝置/使用者、設定其驗證狀態，並決定要將哪個識別碼視為主要識別碼。 如果尚未將任何識別碼設為 `primary`，則主要預設為 `ECID`.

`identityMap` 欄位更新使用 `sentEvent` 命令。

```javascript
alloy("sendEvent", {
  xdm: {
    "identityMap": {
      "ID_NAMESPACE": [ // Notice how each namespace can contain multiple identifiers.
        {
          "id": "1234",
          "authenticatedState": "authenticated",
          "primary": true
        }
      ]
    }
  }
});
```

>[!NOTE]
>
>Adobe建議傳送代表個人的名稱空間，例如 `CRMID`，作為主要身分。


內的每個屬性 `identityMap` 代表屬於特定身分識別 [身分名稱空間](../../identity-service/namespaces.md). 屬性名稱應為身分名稱空間符號，您可以在「 」下方的Adobe Experience Platform使用者介面中找到[!UICONTROL 身分]「。 屬性值應該是屬於該身分名稱空間的身分陣列。

>[!IMPORTANT]
>
>傳入的名稱空間ID `identityMap` 區分大小寫。 請務必使用正確的名稱空間ID，以避免不完整的資料收集。

身分陣列中的每個身分物件包含下列屬性：

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `id` | 字串 | **（必要）** 您要為指定的名稱空間設定的ID。 |
| `authenticationState` | 字串 | **（必要）** ID的驗證狀態。 可能的值包括 `ambiguous`， `authenticated`、和 `loggedOut`. |
| `primary` | 布林值 | 決定是否應將此身分用作設定檔中的主要片段。 依預設，ECID會設為使用者的主要識別碼。 如果省略，此值會預設為 `false`. |

使用 `identityMap` 識別裝置或使用者的欄位會產生與使用相同的結果 [`setCustomerIDs`](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/setcustomerids.html) 來自的方法 [!DNL ID Service API]. 請參閱 [ID服務API檔案](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/get-set.html) 以取得更多詳細資料。

## 從訪客API移轉至ECID

從使用訪客API移轉時，您也可以移轉現有的AMCV Cookie。 若要啟用ECID移轉，請設定 `idMigrationEnabled` 引數來設定。 ID移轉可啟用下列使用案例：

* 當網域的某些頁面使用訪客API，而其他頁面使用此SDK時。 為了支援此情況，SDK會讀取現有的AMCV Cookie，並使用現有的ECID寫入新的Cookie。 此外，SDK會寫入AMCV Cookie，因此如果先在利用SDK進行檢測的頁面上取得ECID，則使用訪客API進行檢測的後續頁面將具有相同的ECID。
* 在也具有Visitor API的頁面上設定Adobe Experience Platform Web SDK時。 為了支援此情況，如果未設定AMCV Cookie，SDK會在頁面上尋找訪客API，並呼叫它以取得ECID。
* 當整個網站使用Adobe Experience Platform Web SDK且沒有訪客API時，移轉ECID以便保留回訪訪客資訊會很有用。 透過部署SDK後 `idMigrationEnabled` 移轉大部分訪客Cookie所需的時間，可關閉此設定。

### 更新要移轉的特徵

將XDM格式資料傳送到Audience Manager時，移轉時需要將此資料轉換為訊號。 您需要更新特徵，以反映XDM提供的新索引鍵。 此程式透過使用 [BAAAM工具](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/bulk-management-tools/bulk-management-intro.html#getting-started-with-bulk-management) 該Audience Manager已建立。

## 用於事件轉送

如果您目前擁有 [事件轉送](../../tags/ui/event-forwarding/overview.md) 已啟用且正在使用 `appmeasurement.js` 和 `visitor.js`，即可讓事件轉送功能保持啟用，這不會造成任何問題。 在後端，Adobe會擷取任何AAM區段，並將其新增至Analytics呼叫。 如果對Analytics的呼叫包含這些區段，Analytics將不會呼叫Audience Manager來轉送任何資料，因此不會有任何雙重資料收集。 使用Web SDK時也不需要位置提示，因為後端會呼叫相同的區段端點。
