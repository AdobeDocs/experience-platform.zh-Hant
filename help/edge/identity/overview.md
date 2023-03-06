---
title: Platform Web SDK中的身分資料
description: 了解如何使用Adobe Experience Cloud Web SDK擷取和管理Adobe Experience Platform ID(ECID)。
keywords: 身分；第一方身分；身分識別服務；第三方身分；ID移轉；訪客ID；第三方身分；第三方CookieEnabled;idMigrationEnabled;getIdentity；同步身分；syncIdentity;sendEvent;identityMap；主要；ecid；身分命名空間；命名空間ID;authenticationState;hashEnabled;
exl-id: 03060cdb-becc-430a-b527-60c055c2a906
source-git-commit: 0edd9422d6ea1b8e3aeaba1b24bc38b42ca809d8
workflow-type: tm+mt
source-wordcount: '1404'
ht-degree: 0%

---

# Platform Web SDK中的身分資料

Adobe Experience Platform Web SDK採用 [Adobe Experience Cloud ID(ECID)](../../identity-service/ecid.md) 來追蹤訪客行為。 使用ECID，您可確保每個裝置都有可跨多個工作階段持續使用的唯一識別碼，將工作階段期間和跨Web工作階段發生的所有點擊連結至特定裝置。

本檔案概述如何使用Platform Web SDK管理ECID。

## 使用SDK追蹤ECID

Platform Web SDK會透過使用Cookie來指派和追蹤ECID，並提供多種可用方法來設定這些Cookie的產生方式。

當新使用者到達您的網站時，Adobe Experience Cloud Identity Service會嘗試為該使用者設定裝置識別Cookie。 若為首次訪客，系統會產生ECID，並在第一次回應中從Adobe Experience Platform邊緣網路傳回。 若為重複訪客，系統會從 `kndctr_{YOUR-ORG-ID}_AdobeOrg_identity` Cookie並新增至邊緣網路的裝載。

包含ECID的Cookie設定完成後，Web SDK產生的每個後續請求都會在 `kndctr_{YOUR-ORG-ID}_AdobeOrg_identity` cookie。

使用Cookie進行裝置識別時，您有兩個選項可與邊緣網路互動：

1. 直接將資料傳送至邊緣網路網域 `adobedc.net`. 此方法稱為 [協力廠商資料收集](#third-party).
1. 在您自己的網域上建立CNAME，並指向 `adobedc.net`. 此方法稱為 [第一方資料收集](#first-party).

如以下各節所述，您選擇使用的資料收集方法會直接影響瀏覽器的Cookie存留期。

### 協力廠商資料收集 {#third-party}

協力廠商資料收集包括直接傳送資料至邊緣網路網域 `adobedc.net`.

近年來，網頁瀏覽器在處理第三方設定的Cookie時，受到的限制越來越多。 某些瀏覽器預設會封鎖第三方Cookie。 如果您使用第三方Cookie來識別網站訪客，這些Cookie的存留期幾乎永遠比使用第一方Cookie時可用的期限短。 在某些情況下，協力廠商Cookie最少會在七天後過期。

此外，使用協力廠商資料收集時，某些廣告封鎖程式會將流量限制為完全Adobe資料收集端點。

### 第一方資料收集 {#first-party}

第一方資料收集包括透過您所在網域上指向的CNAME設定Cookie `adobedc.net`.

雖然瀏覽器長期以類似網站擁有端點所設定的方式處理CNAME端點所設定的Cookie，但瀏覽器最近實作的變更，在處理CNAME Cookie的方式上有所差異。 雖然目前沒有瀏覽器依預設會封鎖第一方CNAME Cookie，但有些瀏覽器會將使用CNAME設定的Cookie存留期限限制為僅7天。

### Cookie存留期對Adobe Experience Cloud應用程式的影響 {#lifespans}

無論您選擇第一方還是第三方資料收集，Cookie可存留的時間長度，會直接影響Adobe Analytics和Customer Journey Analytics中的訪客計數。 此外，若網站上使用Adobe Target或Offer decisioning，使用者的個人化體驗可能會不一致。

例如，假設您已建立個人化體驗，若使用者在過去七天內檢視過三次，則會將任何項目提升至首頁。

如果一般使用者一週內瀏覽三次，卻連續七天未回訪網站，則當他們回訪網站時，該使用可能會被視為新使用者，因為瀏覽器原則可能已刪除其Cookie（取決於他們造訪網站時使用的瀏覽器）。 如果發生此情況，即使訪客在七天多一點前造訪了該網站，您的Analytics工具仍會將其視為新使用者。 此外，您將再次開始為使用者個人化體驗的任何工作。

### 第一方裝置ID

若要說明上述Cookie存留期的影響，您可以選擇設定並管理自己的裝置識別碼。 請參閱 [第一方裝置ID](./first-party-device-ids.md) 以取得更多資訊。

## 擷取目前使用者的ECID和地區

若要擷取目前訪客的唯一ECID，請使用 `getIdentity` 命令。 對於尚未具備ECID的首次訪客，此命令會產生新ECID。 `getIdentity` 也會傳回訪客的地區ID。

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

使用XDM [`identityMap` 欄位](../../xdm/schema/composition.md#identityMap)，您可以使用多個身分識別裝置/使用者、設定其驗證狀態，並決定將哪個識別碼視為主要識別碼。 如果未將任何識別碼設為 `primary`，主要預設為 `ECID`.

`identityMap` 欄位會使用 `sentEvent` 命令。

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

內的每個屬性 `identityMap` 代表屬於特定 [身分命名空間](../../identity-service/namespaces.md). 屬性名稱應為身分命名空間符號，您可在Adobe Experience Platform使用者介面的「 」下找到[!UICONTROL 身分]」。 屬性值應該是與該身分識別命名空間相關的身分識別陣列。

>[!IMPORTANT]
>
>傳入的命名空間ID `identityMap` 區分大小寫。 請務必使用正確的命名空間ID，以避免資料收集不完整。

身分陣列中的每個身分物件都包含下列屬性：

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `id` | 字串 | **（必要）** 您要為指定命名空間設定的ID。 |
| `authenticationState` | 字串 | **（必要）** ID的驗證狀態。 可能的值包括 `ambiguous`, `authenticated`，和 `loggedOut`. |
| `primary` | 布林值 | 判斷是否應將此身分用作設定檔中的主要片段。 依預設，ECID會設為使用者的主要識別碼。 若省略，此值會預設為 `false`. |

使用 `identityMap` 欄位來識別裝置或使用者，結果與使用 [`setCustomerIDs`](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/setcustomerids.html?lang=en) 方法 [!DNL ID Service API]. 請參閱 [ID服務API檔案](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/get-set.html?lang=en) 以取得更多詳細資訊。

## 從訪客API移轉至ECID

從使用訪客API進行移轉時，您也可以移轉現有的AMCV Cookie。 若要啟用ECID移轉，請設定 `idMigrationEnabled` 參數。 ID移轉可啟用下列使用案例：

* 當網域的某些頁面使用訪客API，而其他頁面使用此SDK時。 為支援此情況，SDK會讀取現有的AMCV Cookie，並使用現有ECID寫入新Cookie。 此外，SDK會寫入AMCV Cookie，如果先在以SDK創作的頁面上取得ECID，則以訪客API創作的後續頁面會有相同的ECID。
* 當Adobe Experience Platform Web SDK設定於同時具有訪客API的頁面上時。 為支援此情況，如果未設定AMCV Cookie,SDK會在頁面上尋找訪客API，並呼叫它以取得ECID。
* 當整個網站使用Adobe Experience Platform Web SDK且沒有訪客API時，移轉ECID以保留傳回的訪客資訊會很實用。 部署SDK後，搭配 `idMigrationEnabled` 一段時間內，即可關閉設定，以便移轉大部分的訪客cookie。

### 更新特徵以進行移轉

將XDM格式化資料傳送至Audience Manager時，此資料在移轉時需轉換為訊號。 您的特徵需要更新，以反映XDM提供的新索引鍵。 使用 [BAAAM工具](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/bulk-management-tools/bulk-management-intro.html#getting-started-with-bulk-management) 該Audience Manager已建立。

## 用於事件轉送

如果您目前有 [事件轉送](../../tags/ui/event-forwarding/overview.md) 已啟用，且正在使用 `appmeasurement.js` 和 `visitor.js`，您可以繼續啟用事件轉送功能，這不會造成任何問題。 在後端，Adobe會擷取任何AAM區段，並將其新增至對Analytics的呼叫。 如果對Analytics的呼叫包含這些區段，Analytics不會呼叫Audience Manager來轉送任何資料，因此不會有任何雙重資料收集。 使用Web SDK時也不需要位置提示，因為後端會呼叫相同的分段端點。
