---
title: 擷取Experience Cloud ID
seo-title: Adobe Experience Platform Web SDK擷取Experience Cloud ID
description: 瞭解如何取得Adobe Experience Cloud Id。
seo-description: 瞭解如何取得Adobe Experience Cloud Id。
keywords: Identity;First Party Identity;Identity Service;3rd Party Identity;ID Migration;Visitor ID;third party identity;thirdPartyCookiesEnabled;idMigrationEnabled;getIdentity;Syncing Identities;syncIdentity;sendEvent;identityMap;primary;ecid;Identity Namespace;namespace id;authenticationState;hashEnabled;
translation-type: tm+mt
source-git-commit: 1b5ee9b1f9bdc7835fa8de59020b3eebb4f59505
workflow-type: tm+mt
source-wordcount: '731'
ht-degree: 3%

---


# 身分——擷取Experience Cloud ID

Adobe Experience Platform Web SDK運用 [Adobe Identity Service](../../identity-service/ecid.md)。 這可確保每個裝置都有一個唯一識別碼，該識別碼會保存在裝置上，以便將頁面之間的活動系結在一起。

## 第一方身分

該 [!DNL Identity Service] 識別碼儲存在第一方網域的Cookie中。 嘗 [!DNL Identity Service] 試使用網域上的HTTP標題來設定Cookie。 如果失敗，則 [!DNL Identity Service] 會回到透過Javascript設定Cookie。 Adobe建議您設定CNAME，以確保您的Cookie不受用戶端ITP限制。

## 第三方身份

可 [!DNL Identity Service] 以將ID與第三方網域(demdex.net)同步，以便跨網站追蹤。 啟用此功能後，會對demdex.net提出對訪客的第一個要求（例如，沒有ECID的訪客）。 這只會在允許其執行的瀏覽器（例如Chrome）上執行，並由設定中的 `thirdPartyCookiesEnabled` 參數控制。 如果您想要一起停用此功能，請設 `thirdPartyCookiesEnabled` 為false。

## ID移轉

從使用訪客API進行移轉時，您也可以移轉現有的AMCV Cookie。 若要啟用ECID移轉，請在 `idMigrationEnabled` 設定中設定參數。 ID移轉可啟用下列使用案例：

* 當網域的某些頁面使用訪客API，而其他頁面使用此SDK時。 為支援此案例，SDK會讀取現有的AMCV Cookie，並使用現有的ECID寫入新Cookie。 此外，SDK會編寫AMCV Cookie，如此，如果ECID是先在SDK所創作的頁面上取得，則使用訪客API所創作的後續頁面具有相同的ECID。
* 當Adobe Experience Platform Web SDK設定在同時具有訪客API的頁面上時。 為支援此案例，如果未設定AMCV Cookie,SDK會在頁面上尋找訪客API並呼叫它以取得ECID。
* 當整個網站使用Adobe Experience Platform Web SDK且沒有訪客API時，移轉ECID以保留回訪訪客資訊會很有用。 在SDK與部署一段 `idMigrationEnabled` 時間後，如此大部分的訪客Cookie都會移轉，就可關閉設定。

## 擷取訪客ID

如果要使用此唯一ID，請使用命 `getIdentity` 令。 `getIdentity` 傳回目前訪客的現有ECID。 對於尚未擁有ECID的首次訪客，此命令會產生新的ECID。

>[!NOTE]
>
>此方法通常用於需要讀取 [!DNL Experience Cloud] ID的自訂解決方案。 標準實作不會使用此函數。

```javascript
alloy("getIdentity")
  .then(function(result) {
    // The command succeeded.
    console.log(result.identity.ECID);
  })
  .catch(function(error) {
    // The command failed.
    // "error" will be an error object with additional information.
  });
```

## 同步身分

>[!NOTE]
>
>除了 `syncIdentity` 雜湊功能外，2.1.0版中也移除了該方法。 如果您使用2.1.0+版，並想要同步身分識別，可以直接在命令的選項( `xdm` 位於 `sendEvent` 欄位下)中 `identityMap` 傳送。

此外， [!DNL Identity Service] 還允許您使用命令將自己的標識符與ECID `syncIdentity` 同步。

>[!NOTE]
>
>強烈建議在每個命令上傳遞所有可用的 `sendEvent` 身份。 這可解鎖一系列使用案例，包括個人化。 現在，您可以在命令中傳遞這些身 `sendEvent` 分識別，因此可將它們直接放在DataLayer中。

同步身分可讓您使用多個身分識別裝置／使用者、設定其驗證狀態，並決定哪個識別碼被視為主要識別碼。 如果未將標識符設定為 `primary`，則主要預設值為 `ECID`。

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

內的每個屬 `identityMap` 性代表屬於特定身分命名空 [間的身分](../../identity-service/namespaces.md)。 屬性名稱應為身分名稱空間符號，您可在Adobe Experience Platform使用者介面的「身分識別」下方找[!UICONTROL 到]。 屬性值應為與該標識名稱空間相關的標識陣列。

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
