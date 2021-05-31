---
title: 使用Adobe Experience Platform Web SDK擷取Experience CloudID
description: 了解如何使用Adobe Experience Cloud Web SDK擷取Adobe Experience Platform ID(ECID)。
seo-description: 了解如何取得Adobe Experience Cloud Id。
keywords: 身分；第一方身分；身分識別服務；第三方身分；ID移轉；訪客ID；第三方身分；第三方CookieEnabled;idMigrationEnabled;getIdentity；同步身分；syncIdentity;sendEvent;identityMap；主要；ecid；身分命名空間；命名空間ID;authenticationState;hashEnabled;
exl-id: 03060cdb-becc-430a-b527-60c055c2a906
source-git-commit: c3d66e50f647c2203fcdd5ad36ad86ed223733e3
workflow-type: tm+mt
source-wordcount: '961'
ht-degree: 3%

---

# 擷取Adobe Experience Cloud ID

Adobe Experience Platform Web SDK採用[Adobe身分服務](../../identity-service/ecid.md)。 這可確保每個裝置都有唯一識別碼，且會保存在裝置上，以便將頁面之間的活動系結在一起。

## 第一方身分

[!DNL Identity Service]會將身分儲存在第一方網域的Cookie中。 [!DNL Identity Service]會嘗試在網域上使用HTTP標題來設定Cookie。 若失敗，[!DNL Identity Service]將會回復為透過Javascript設定Cookie。 Adobe建議您設定CNAME，以確保用戶端ITP限制不會限制您的Cookie。

## 第三方身分識別

[!DNL Identity Service]能將ID與第三方網域(demdex.net)同步，以啟用跨網站的追蹤。 啟用此功能後，系統會向demdex.net提出訪客的第一個要求（例如，沒有ECID的訪客）。 這只會在允許的瀏覽器（例如Chrome）上執行，並由設定中的`thirdPartyCookiesEnabled`參數控制。 如果您想要一起停用此功能，請將`thirdPartyCookiesEnabled`設為false。

## ID移轉

從使用訪客API進行移轉時，您也可以移轉現有的AMCV Cookie。 若要啟用ECID移轉，請在設定中設定`idMigrationEnabled`參數。 ID移轉可啟用下列使用案例：

* 當網域的某些頁面使用訪客API，而其他頁面使用此SDK時。 為支援此情況，SDK會讀取現有的AMCV Cookie，並使用現有ECID寫入新Cookie。 此外，SDK會寫入AMCV Cookie，如果先在以SDK創作的頁面上取得ECID，則以訪客API創作的後續頁面會有相同的ECID。
* 當Adobe Experience Platform Web SDK設定於同時具有訪客API的頁面上時。 為支援此情況，如果未設定AMCV Cookie,SDK會在頁面上尋找訪客API，並呼叫它以取得ECID。
* 當整個網站使用Adobe Experience Platform Web SDK且沒有訪客API時，移轉ECID以保留傳回的訪客資訊會很實用。 在SDK與`idMigrationEnabled`一起部署一段時間以便移轉大部分的訪客Cookie後，即可關閉設定。

## 更新特徵以進行移轉

將XDM格式化資料傳送至Audience Manager時，此資料在移轉時需轉換為訊號。 您的特徵需要更新，以反映XDM提供的新索引鍵。 使用Audience Manager已建立的[BAAAM工具](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/bulk-management-tools/bulk-management-intro.html#getting-started-with-bulk-management)，讓此程式更輕鬆。

## 伺服器端轉送

如果您目前已啟用伺服器端轉送，且正在使用`appmeasurement.js`。 和`visitor.js`您可以保持啟用伺服器端轉送功能，這不會造成任何問題。 在後端，Adobe會擷取任何AAM區段，並將它們新增至對Analytics的呼叫。 如果對Analytics的呼叫包含這些區段，Analytics不會呼叫Audience Manager來轉送任何資料，因此不會有任何雙重資料收集。 使用Web SDK時也不需要位置提示，因為後端會呼叫相同的分段端點。

## 擷取訪客ID和地區ID

如果您想使用唯一訪客ID，請使用`getIdentity`命令。 `getIdentity` 傳回目前訪客的現有ECID。對於尚未具備ECID的首次訪客，此命令會產生新ECID。 `getIdentity` 也會傳回訪客的地區ID。如需詳細資訊，請參閱[Adobe Audience Manager使用手冊](https://experienceleague.adobe.com/docs/audience-manager/user-guide/api-and-sdk-code/dcs/dcs-api-reference/dcs-regions.html) 。

>[!NOTE]
>
>此方法通常用於需要讀取[!DNL Experience Cloud] ID或需要Adobe Audience Manager位置提示的自訂解決方案。 標準實作不會使用此函數。

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

## 同步身分

>[!NOTE]
>
>除了雜湊功能外，2.1.0版中已移除`syncIdentity`方法。 如果您使用2.1.0+版，並且想要同步身分，則可以在`sendEvent`命令的`xdm`選項（`identityMap`欄位下）中直接發送身份。

此外， [!DNL Identity Service]還允許您使用`syncIdentity`命令，將自己的識別碼與ECID同步。

>[!NOTE]
>
>強烈建議在每個`sendEvent`命令上傳遞所有可用身份。 這可解除鎖定一系列使用案例，包括個人化。 現在，您可以在`sendEvent`命令中傳遞這些身份，可以直接將它們放置在DataLayer中。

同步身分可讓您使用多個身分識別裝置/使用者、設定其驗證狀態，並決定將哪個識別碼視為主要識別碼。 如果未將標識符設定為`primary`，則主預設值為`ECID`。

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

`identityMap`內的每個屬性代表屬於特定[身分命名空間](../../identity-service/namespaces.md)的身分。 屬性名稱應為身分命名空間符號，您可在Adobe Experience Platform使用者介面的「[!UICONTROL Identities]」下方找到。 屬性值應該是與該身分識別命名空間相關的身分識別陣列。

身分陣列中的每個身分物件結構如下：

### `id`

| **類型** | **必填** | **預設值** |
| -------- | ------------ | ----------------- |
| 字串 | 是 | 無 |

這是您要針對指定命名空間同步的ID。

### `authenticationState`

| **類型** | **必填** | **預設值** | **可能的值** |
| -------- | ------------ | ----------------- | ------------------------------------ |
| 字串 | 是 | 模糊 | 不明確、已驗證和已登出 |

ID的驗證狀態。

### `primary`

| **類型** | **必填** | **預設值** |
| -------- | ------------ | ----------------- |
| 布林值 | 可選 | false |

判斷是否應將此身分用作統一設定檔中的主要片段。 依預設，ECID會設為使用者的主要識別碼。
