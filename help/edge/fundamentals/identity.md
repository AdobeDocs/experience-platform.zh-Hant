---
title: 擷取Experience Cloud ID
seo-title: Adobe Experience Platform Web SDK擷取Experience Cloud ID
description: 瞭解如何取得Adobe Experience Cloud Id。
seo-description: 瞭解如何取得Adobe Experience Cloud Id。
translation-type: tm+mt
source-git-commit: 5f263a2593cdb493b5cd48bc0478379faa3e155d
workflow-type: tm+mt
source-wordcount: '412'
ht-degree: 9%

---


# 身分——擷取Experience Cloud ID

Adobe Experience Platform Web SDK運用 [Adobe Identity Service](../../identity-service/ecid.md)。 這可確保每個裝置都有一個唯一識別碼，該識別碼會保存在裝置上，以便將頁面之間的活動系結在一起。

## 第一方身分

該 [!DNL Identity Service] 識別碼儲存在第一方網域的Cookie中。 嘗 [!DNL Identity Service] 試使用網域上的HTTP標題來設定Cookie。 如果失敗，則 [!DNL Identity Service] 會回到透過Javascript設定Cookie。 Adobe建議您設定CNAME，以確保您的Cookie不受用戶端ITP限制。

## 第三方身份

可 [!DNL Identity Service] 以將ID與第三方網域(demdex.net)同步，以便跨網站追蹤。 啟用此功能後，會對demdex.net提出對訪客的第一個要求（例如，沒有ECID的訪客）。 這只會在允許其執行的瀏覽器（例如Chrome）上執行，並由設定中的 `thirdPartyCookiesEnabled` 參數控制。 如果您想要一起停用此功能，請設 `thirdPartyCookiesEnabled` 為false。

## 擷取訪客ID

如果要使用此唯一ID，請使用命 `getIdentity` 令。 `getIdentity` 傳回目前訪客的現有ECID。 對於尚未擁有ECID的首次訪客，此命令會產生新的ECID。

>[!NOTE]
>
>此方法通常用於需要讀取Experience Cloud ID的自訂解決方案。 標準實作不會使用此函數。

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

此外， [!DNL Identity Service] 還允許您使用命令將自己的標識符與ECID `syncIdentity` 同步。

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

物件的索引鍵是 [Identity Namespace](../../identity-service/namespaces.md) Symbol。 您可在「身分識別」下方的Adobe Experience Platform使用者介面中找到此 [!UICONTROL 項目]。

#### `id`

| **類型** | **必填** | **預設值** |
| -------- | ------------ | ----------------- |
| 字串 | 是 | nown |

這是您要針對指定命名空間同步的ID。

#### `authenticationState`

| **類型** | **必填** | **預設值** | **可能的值** |
| -------- | ------------ | ----------------- | ------------------------------------ |
| 字串 | 是 | 模糊 | 不明確、已驗證和已登錄已註銷 |

ID的驗證狀態。

#### `primary`

| **類型** | **必填** | **預設值** |
| -------- | ------------ | ----------------- |
| 布林值 | 可選 | false |

確定是否應將此身份用作統一配置檔案中的主片段。 依預設，ECID會設為使用者的主要識別碼。

#### `hashEnabled`

| **類型** | **必填** | **預設值** |
| -------- | ------------ | ----------------- |
| 布林值 | 可選 | false |

如果啟用，則會使用SHA256雜湊來雜湊識別。
