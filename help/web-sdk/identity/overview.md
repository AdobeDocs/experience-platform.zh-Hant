---
title: Web SDK中的身分資料
description: 瞭解如何使用Adobe Experience Platform Web SDK擷取和管理Adobe Experience Cloud ID (ECID)。
exl-id: 03060cdb-becc-430a-b527-60c055c2a906
source-git-commit: 3724c43090e37d21384e9dfe45e60ee2eec68a81
workflow-type: tm+mt
source-wordcount: '1554'
ht-degree: 0%

---


# Web SDK中的身分資料

Adobe Experience Platform Web SDK使用[Adobe Experience Cloud ID (ECID)](../../identity-service/features/ecid.md)來追蹤訪客行為。 使用[!DNL ECIDs]時，您可以確保每個裝置都有唯一識別碼，此識別碼可以跨多個工作階段持續存在，將發生在網頁工作階段期間或跨網頁工作階段的所有點選繫結至特定裝置。

本檔案概述如何使用網頁SDK管理[!DNL ECIDs]和[!DNL CORE IDs]。

## 使用網頁SDK追蹤ECID {#tracking-ecids-web-sdk}

Web SDK會使用Cookie指派及追蹤[!DNL ECIDs]，並有多種可用方法來設定這些Cookie的產生方式。

當新使用者進入您的網站時，[Adobe Experience Cloud Identity Service](../../identity-service/home.md)會嘗試為該使用者設定裝置識別Cookie。

* 初次造訪的訪客會在來自Experience PlatformEdge Network的第一個回應中產生並傳回[!DNL ECID]。
* 若為再度訪問的訪客，系統會從`kndctr_{YOUR-ORG-ID}_AdobeOrg_identity` Cookie擷取[!DNL ECID]，並由Edge Network將其新增至請求承載。

設定包含[!DNL ECID]的Cookie後，網頁SDK產生的每個後續請求都會在`kndctr_{YOUR-ORG-ID}_AdobeOrg_identity` Cookie中包含編碼的[!DNL ECID]。

使用Cookie來識別裝置時，您有兩種方式可與Edge Network互動：

1. 在您自己的網域上建立指向`adobedc.net`的CNAME。 此方法稱為[第一方資料收集](#first-party)。
1. 將資料直接傳送到Edge Network網域`adobedc.net`。 此方法稱為[第三方資料收集](#third-party)。

如下節所述，您選擇使用的資料收集方法會直接影響各瀏覽器的Cookie存留期。

## 使用網頁SDK追蹤核心ID {#tracking-coreid-web-sdk}

使用已啟用第三方Cookie的Google Chrome且未設定`kndctr_{YOUR-ORG-ID}_AdobeOrg_identity` Cookie時，第一個Edge Network請求會通過`demdex.net`網域，其會設定Demdex Cookie。 此Cookie包含[!DNL CORE ID]。 這是不重複的使用者ID，與[!DNL ECID]不同。

根據您的實作，您可能要[存取 [!DNL CORE ID]](#retrieve-coreid)。

### 第一方資料收集 {#first-party}

第一方資料收集涉及透過您自己的網域上指向`adobedc.net`的`CNAME`設定Cookie。

雖然瀏覽器長期以來以與網站擁有端點所設定類似的方式處理`CNAME`端點所設定的Cookie，但瀏覽器最近實作的變更已對`CNAME` Cookie的處理方式造成差異。 雖然目前沒有瀏覽器預設會封鎖第一方`CNAME` Cookie，但有些瀏覽器會將使用`CNAME`設定的Cookie存留期限製為僅七天。

### 協力廠商資料收集 {#third-party}

第三方資料收集涉及直接傳送資料至Edge Network網域`adobedc.net`。

近年來，網頁瀏覽器在處理第三方設定的Cookie時，限制日益嚴格。 有些瀏覽器預設會封鎖第三方Cookie。 如果您使用第三方Cookie來識別網站訪客，則這些Cookie的存留期幾乎總是比使用第一方Cookie所能提供的短。 有時第三方Cookie最快會在七天後過期。

此外，使用第三方資料收集時，有些廣告封鎖程式會完全將流量限制在Adobe資料收集端點。

### Cookie有效期限對Adobe Experience Cloud應用程式的影響 {#lifespans}

無論您是選擇第一方還是第三方資料收集，Cookie可儲存的時間長度會直接影響[Adobe Analytics](https://experienceleague.adobe.com/zh-hant/docs/analytics)和[Customer Journey Analytics](https://experienceleague.adobe.com/zh-hant/docs/customer-journey-analytics)中的訪客計數。 此外，在網站上使用[Adobe Target](https://experienceleague.adobe.com/zh-hant/docs/target)或[Offer decisioning](https://experienceleague.adobe.com/zh-hant/docs/target/using/integrate/ajo/offer-decision)時，一般使用者可能會遇到不一致的個人化體驗。

例如，假設您已建立個人化體驗，且使用者在過去七天內檢視過任何專案三次，此體驗會將任何專案提升至首頁。

如果一般使用者一週瀏覽三次，然後七天未返回網站，則該使用者在返回網站時可視為新使用者，因為其Cookie可能已遭到瀏覽器原則刪除（取決於使用者瀏覽網站時所使用的瀏覽器）。 如果發生此情況，您的Analytics工具會將訪客視為新使用者，即使他們剛在七天多一點前造訪網站。 此外，使用者個人化體驗的任何工作都會重新開始。

### 第一方裝置ID (FPID) {#fpid}

如上所述，若要考慮Cookie有效期限的影響，您可以選擇設定並管理您自己的裝置識別碼。 如需詳細資訊，請參閱[第一方裝置識別碼](./first-party-device-ids.md)的指南。

## 擷取目前使用者的ECID和區域 {#retrieve-ecid}

根據您的使用案例，有兩種方法可以存取[!DNL ECID]：

* [透過「資料準備」擷取 [!DNL ECID] 以收集資料](#retrieve-ecid-data-prep)：建議您使用此方法。
* [透過`getIdentity()`命令擷取 [!DNL ECID] ](#retrieve-ecid-getidentity)：只有在您需要使用者端的[!DNL ECID]資訊時，才使用此方法。

### 透過資料收集的資料準備擷取[!DNL ECID] {#retrieve-ecid-data-prep}

使用[資料彙集](../../datastreams/data-prep.md)的「資料準備」將[!DNL ECID]對應到[!DNL XDM]欄位。 這是存取[!DNL ECID]的建議方式。

要執行此操作，請將來源欄位設定為以下路徑：

```js
xdm.identityMap.ECID[0].id
```

然後，將目標欄位設定為欄位型別為`string`的XDM路徑。

![](../../tags/extensions/client/web-sdk/assets/access-ecid-data-prep.png)


### 透過`getIdentity()`命令擷取[!DNL ECID] {#retrieve-ecid-getidentity}

>[!IMPORTANT]
>
>您應該只有在使用者端需要[!DNL ECID]時，才透過`getIdentity()`命令擷取ECID。 如果您只想將ECID對應到XDM欄位，請改用[資料收集的資料準備](#retrieve-ecid-data-prep)。

若要擷取目前訪客的唯一ECID，請使用`getIdentity`命令。 對於尚無[!DNL ECID]的首次訪客，這個命令會產生新的[!DNL ECID]。 `getIdentity`也會傳回訪客的地區ID。

>[!NOTE]
>
>此方法通常用於需要讀取[!DNL Experience Cloud] ID或需要Adobe Audience Manager位置提示的自訂解決方案。 標準實作不會使用此函式。

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

## 擷取目前使用者的核心ID {#retrieve-coreid}

若要擷取使用者的核心ID，您可以使用[`getIdentity()`](../commands/getidentity.md)命令，如下所示。

```js
alloy("getIdentity",{
  "namespaces": ["CORE"]
});
```


## 使用`identityMap` {#using-identitymap}

使用XDM [`identityMap`欄位](../../xdm/schema/composition.md#identityMap)，您可以使用多個識別碼來識別裝置/使用者、設定其驗證狀態，以及決定要將哪個識別碼視為主要識別碼。 如果尚未將任何識別碼設為`primary`，則主要預設值為`ECID`。

`identityMap`欄位已使用`sentEvent`命令更新。

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
>Adobe建議將代表個人的名稱空間（例如`CRMID`）傳送為主要身分。


`identityMap`中的每個屬性都代表屬於特定[身分名稱空間](../../identity-service/features/namespaces.md)的身分。 屬性名稱應為身分名稱空間符號，您可以在Adobe Experience Platform使用者介面的&quot;[!UICONTROL 身分]&quot;下方找到該符號。 屬性值應該是屬於該身分名稱空間的身分陣列。

>[!IMPORTANT]
>
>在`identityMap`中傳遞的名稱空間ID區分大小寫。 請務必使用正確的名稱空間ID，以避免不完整的資料收集。

身分陣列中的每個身分物件包含下列屬性：

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `id` | 字串 | **（必要）**&#x200B;您要為指定的名稱空間設定的ID。 |
| `authenticatedState` | 字串 | **（必要）**&#x200B;識別碼的驗證狀態。 可能的值為`ambiguous`、`authenticated`和`loggedOut`。 |
| `primary` | 布林值 | 決定是否應將此身分用作設定檔中的主要片段。 依預設，ECID會設為使用者的主要識別碼。 如果省略，此值會預設為`false`。 |

使用`identityMap`欄位來識別裝置或使用者，會產生與使用[!DNL ID Service API]中的[`setCustomerIDs`](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/setcustomerids.html?lang=zh-Hant)方法相同的結果。 如需詳細資訊，請參閱[ID服務API檔案](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/get-set.html?lang=zh-Hant)。

## 從訪客API移轉至ECID {#migrating-visitor-api-ecid}

從使用訪客API移轉時，您也可以移轉現有的AMCV Cookie。 若要啟用ECID移轉，請在設定中設定`idMigrationEnabled`引數。 ID移轉可啟用下列使用案例：

* 當網域的某些頁面使用訪客API，而其他頁面使用此SDK時。 為了支援此情況，SDK會讀取現有的AMCV Cookie，並使用現有ECID寫入新的Cookie。 此外，SDK會撰寫AMCV Cookie，如此一來，若是先在使用SDK檢測的頁面上取得ECID，則使用訪客API檢測的後續頁面將具有相同的ECID。
* 在也具有Visitor API的頁面上設定Adobe Experience Platform Web SDK時。 為了支援此情況，如果未設定AMCV Cookie，SDK會在頁面上尋找訪客API，並呼叫它以取得ECID。
* 當整個網站使用Adobe Experience Platform Web SDK且沒有訪客API時，移轉ECID以便保留傳回的訪客資訊會很有用。 在使用`idMigrationEnabled`部署SDK以便移轉大部分訪客Cookie後，即可關閉設定。

### 更新要移轉的特徵

將XDM格式資料傳送到Audience Manager時，移轉時必須將此資料轉換為訊號。 必須更新您的特徵，以反映XDM提供的新索引鍵。 使用Audience Manager已建立的[BAAAM工具](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/bulk-management-tools/bulk-management-intro.html?lang=zh-Hant#getting-started-with-bulk-management)，可讓此程式更容易。

## 用於事件轉送

如果您目前已啟用[事件轉送](../../tags/ui/event-forwarding/overview.md)，並且正在使用`appmeasurement.js`和`visitor.js`，您可以保持事件轉送功能已啟用，這樣就不會造成任何問題。 在後端，Adobe會擷取任何AAM區段，並將其新增至Analytics呼叫。 如果對Analytics的呼叫包含這些區段，Analytics將不會呼叫Audience Manager來轉送任何資料，因此不會有任何雙重資料收集。 使用Web SDK時也不需要位置提示，因為後端會呼叫相同的區段端點。
