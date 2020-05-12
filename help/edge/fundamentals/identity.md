---
title: 擷取Experience Cloud ID
seo-title: Adobe Experience Platform Web SDK擷取Experience Cloud ID
description: 瞭解如何取得Adobe Experience Cloud Id。
seo-description: 瞭解如何取得Adobe Experience Cloud Id。
translation-type: tm+mt
source-git-commit: 9bd6feb767e39911097bbe15eb2c370d61d9842a
workflow-type: tm+mt
source-wordcount: '424'
ht-degree: 7%

---


# （測試版）擷取Experience Cloud ID

>[!IMPORTANT]
>
>Adobe Experience Platform Web SDK目前為測試版，並非所有使用者都能使用。 文件和功能可能會有所變更。

Adobe Experience Platform Web SDK運用 [Adobe Identity Service](../../identity-service/ecid.md)。 這可確保每個裝置都有一個唯一識別碼，該識別碼會保存在裝置上，以便將頁面之間的活動系結在一起。

## 第一方身分

ID服務將識別儲存在第一方網域的Cookie中。 如果ID服務失敗，則ID服務會嘗試在網域上使用HTTP標題來設定Cookie，而會回到透過Javascript設定Cookie。 Adobe建議您設定CNAME，以確保您的Cookie不受用戶端ITP限制。

## 第三方身份

ID服務可將ID與第三方網域(demdex.net)同步，以啟用跨網站的追蹤。 啟用此功能後，會對demdex.net提出對訪客的第一個要求（例如，沒有ECID的訪客）。 這只會在允許其執行的瀏覽器（例如Chrome）上執行，並由設定中的 `thirdPartyCookiesEnabled` 參數控制。 如果您想要停用此功能，請全部設 `thirdPartyCookiesEnabled` 為false。

## 擷取訪客ID

如果要使用此唯一ID，請使用命 `getIdentity` 令。 `getIdentity` 傳回目前訪客的現有ECID。 對於尚未擁有ECID的首次訪客，此命令會產生新的ECID。

>[!NOTE]
>
>此方法通常用於需要讀取Experience Cloud ID的自訂解決方案。 標準實作不會使用它。

```javascript
alloy("getIdentity")
  .then(function(result.identity.ECID) {
    // This function will get called with Adobe Experience Cloud Id when the command promise is resolved
  })
  .catch(function(error) {
    // The command failed.
    // "error" will be an error object with additional information
  })
```

## 同步身分識別

此外，Identity Service可讓您使用命令將您自己的識別碼與ECID同 `syncIdentity` 步。

```javascript
alloy("syncIdentity",{
    identity:{
      "AppNexus":{
        "id":"123456,
        "authenticationState":"ambiguous",
        "primary":false,
        "hashEnabled": true,
      }
    }
})
```

### 同步身分選項

#### Identity Namespace符號

| **類型** | **必填** | **預設值** |
| -------- | ------------ | ----------------- |
| 字串 | 是 | nown |

物件的索引鍵是 [Identity Namespace](../../identity-service/namespaces.md) Symbol。 您可在「身分識別」下的Adobe Experience Platform UI中找到此項。

#### `id`

| **類型** | **必填** | **預設值** |
| -------- | ------------ | ----------------- |
| 字串 | 是 | nown |

這是您要針對指定命名空間同步的ID。

#### `primary`

| **類型** | **必填** | **預設值** |
| -------- | ------------ | ----------------- |
| 布林值 | 可選 | false |

此身分是否應當用作統一描述檔中的主要片段。 依預設，ECID會設為使用者的主要識別碼。

#### `hashEnabled`

| **類型** | **必填** | **預設值** |
| -------- | ------------ | ----------------- |
| 布林值 | 可選 | false |

如果啟用，則會使用SHA256雜湊來雜湊識別。