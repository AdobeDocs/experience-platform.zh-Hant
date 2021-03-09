---
title: 使用Adobe Experience Platform網頁SDK擷取Experience CloudID
description: 瞭解如何使用Adobe Experience Platform網頁SDK擷取Adobe Experience CloudID(ECID)。
seo-description: 瞭解如何取得Adobe Experience CloudID。
keywords: Identity；第一方身分；Identity Service；第三方身份；ID移轉；訪客ID；第三方身份；第三方身份；第三方CookieEnabled;idMigrationEnabled;getIdentity；同步身份；syncIdentity;sendEvent;identityMap;primary;ecid;ItyNamespace idenamespace id;authenticationState;authenticationhashEnabled;
translation-type: tm+mt
source-git-commit: 882bcd2f9aa7a104270865783eed82089862dea3
workflow-type: tm+mt
source-wordcount: '963'
ht-degree: 3%

---


# 擷取Adobe Experience CloudID

Adobe Experience Platform網頁SDK運用[Adobe身分服務](../../identity-service/ecid.md)。 這可確保每個裝置都有一個唯一識別碼，該識別碼會保存在裝置上，以便將頁面之間的活動系結在一起。

## 第一方身分

[!DNL Identity Service]會將身分儲存在第一方網域的Cookie中。 [!DNL Identity Service]會嘗試使用網域上的HTTP標題來設定Cookie。 如果失敗，[!DNL Identity Service]將會回到透過Javascript設定Cookie。 Adobe建議您設定CNAME，以確保您的Cookie不受用戶端ITP限制。

## 第三方身份

[!DNL Identity Service]可將ID與第三方網域(demdex.net)同步，以便跨網站追蹤。 啟用此功能後，將會對demdex.net提出訪客的第一個要求（例如，沒有ECID的訪客）。 這只會在允許其執行的瀏覽器（例如Chrome）上執行，並由組態中的`thirdPartyCookiesEnabled`參數控制。 如果您想要同時停用此功能，請將`thirdPartyCookiesEnabled`設為false。

## ID移轉

從使用訪客API進行移轉時，您也可以移轉現有的AMCV Cookie。 要啟用ECID遷移，請在配置中設定`idMigrationEnabled`參數。 ID移轉可啟用下列使用案例：

* 當網域的某些頁面使用訪客API，而其他頁面使用此SDK時。 為支援此案例，SDK會讀取現有的AMCV Cookie，並使用現有的ECID寫入新Cookie。 此外，SDK會編寫AMCV Cookie，如此，如果ECID是先在SDK所創作的頁面上取得，則使用訪客API所創作的後續頁面具有相同的ECID。
* 當Adobe Experience Platform網頁SDK設定在具有訪客API的頁面上時。 為支援此案例，如果未設定AMCV Cookie,SDK會在頁面上尋找訪客API並呼叫它以取得ECID。
* 當整個網站使用Adobe Experience Platform網頁SDK且沒有訪客API時，移轉ECID以保留回訪訪客資訊會很有用。 在SDK與`idMigrationEnabled`一起部署一段時間後，如此大部分的訪客Cookie都會移轉，就可關閉設定。

## 更新移轉特徵

當XDM格式化的資料發送到Audience Manager時，遷移時需要將這些資料轉換為信號。 您的特徵需要更新，以反映XDM提供的新密鑰。 使用該Audience Manager已建立的[BAAM工具](https://docs.adobe.com/content/help/en/audience-manager/user-guide/reference/bulk-management-tools/bulk-management-intro.html#getting-started-with-bulk-management)，使此過程更加容易。

## 伺服器端轉送

如果您目前已啟用伺服器端轉送，且使用`appmeasurement.js`。 和`visitor.js`，您可以保持啟用伺服器端轉送功能，而不會造成任何問題。 在後端，Adobe會擷取AAM任何區段，並將它們新增至對Analytics的呼叫。 如果對Analytics的呼叫包含這些區段，Analytics不會呼叫Audience Manager來轉送任何資料，因此沒有雙重資料收集。 使用Web SDK時也不需要位置提示，因為後端會呼叫相同的分段端點。

## 擷取訪客ID和地區ID

如果您想要使用唯一訪客ID，請使用`getIdentity`命令。 `getIdentity` 傳回目前訪客的現有ECID。對於尚未擁有ECID的首次訪客，此命令會產生新的ECID。 `getIdentity` 也會傳回訪客的地區ID。如需詳細資訊，請參閱[Adobe Audience Manager使用指南](https://experienceleague.adobe.com/docs/audience-manager/user-guide/api-and-sdk-code/dcs/dcs-api-reference/dcs-regions.html)。

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
>除了雜湊功能外，2.1.0版中還移除了`syncIdentity`方法。 如果您使用2.1.0+版並想要同步身分，可以直接在`sendEvent`命令的`xdm`選項（位於`identityMap`欄位下）中傳送身分。

此外，[!DNL Identity Service]還允許您使用`syncIdentity`命令將自己的標識符與ECID同步。

>[!NOTE]
>
>強烈建議在每個`sendEvent`命令上傳遞所有可用身份。 這可解鎖一系列使用案例，包括個人化。 現在，您可以在`sendEvent`命令中傳遞這些身分，就可以直接放在DataLayer中。

同步身分可讓您使用多個身分識別裝置／使用者、設定其驗證狀態，並決定哪個識別碼被視為主要識別碼。 如果未將標識符設定為`primary`，則主標識符預設為`ECID`。

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

`identityMap`中的每個屬性代表屬於特定[identity namespace](../../identity-service/namespaces.md)的身分。 屬性名稱應為身份名稱空間符號，您可在「[!UICONTROL Identities]」下的Adobe Experience Platform用戶介面中找到該符號。 屬性值應為與該標識名稱空間相關的標識陣列。

身份陣列中的每個身份對象的結構如下：

### `id`

| **類型** | **必填** | **預設值** |
| -------- | ------------ | ----------------- |
| 字串 | 是 | 無 |

這是您要針對指定命名空間同步的ID。

### `authenticationState`

| **類型** | **必填** | **預設值** | **可能的值** |
| -------- | ------------ | ----------------- | ------------------------------------ |
| 字串 | 是 | 模糊 | 不明確、已驗證和已登錄已註銷 |

ID的驗證狀態。

### `primary`

| **類型** | **必填** | **預設值** |
| -------- | ------------ | ----------------- |
| 布林值 | 可選 | false |

確定是否應將此身份用作統一配置檔案中的主片段。 依預設，ECID會設為使用者的主要識別碼。
