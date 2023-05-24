---
title: 客戶端狀態管理
description: 瞭解Adobe Experience Platform邊緣網路如何管理客戶端狀態
seo-description: Learn how the Adobe Experience Platform Edge Network  manages client state
keywords: 客戶端；狀態；管理；邊緣；網路；網關；api;client;state;management;edge;network;gateway;api
exl-id: 798ecc52-1af1-4480-a2a3-3198a83538f8
source-git-commit: 85b428b3997d53cbf48e4f112e5c09c0f40f7ee1
workflow-type: tm+mt
source-wordcount: '850'
ht-degree: 2%

---

# 客戶端狀態管理

邊緣網路本身是無狀態的（它不維護自己的會話）。 但是，有些使用情形需要客戶端狀態持久性，例如：

* 一致的設備標識(請參見 [訪客身份](visitor-identification.md))
* 收集並強制用戶同意
* 保留個性化會話ID

邊緣網路使用狀態管理協定，將儲存方面委託給其客戶端/SDK，並在其響應中包括狀態條目。 對於瀏覽器，這些條目以Cookie的形式儲存。

客戶的責任是將它們儲存並包含在所有後續請求中。 客戶端還必須按照網關的指示，對條目進行適當的過期處理。 當這些條目以Cookie儲存時，瀏覽器會自動執行所有這些操作。

雖然州條目總是有一個 `String` 值（對調用方/SDK可見），您不應以任何方式使用或篡改這些值。 值結構/格式甚至名稱本身可能隨時更改，這可能導致內部使用狀態的客戶端出現意外行為。 該狀態旨在始終由網關本身或其他邊緣服務使用。

## 將客戶端狀態作為元資料保留

由 [!DNL Edge Network] 在響應體中 `Handle` 類型對象 `state:store`。

```json
{
   "requestId":"421036b3-a7ff-480b-a9ab-30adba6eb4f0",
   "handle":[
      {
         "payload":[
            {
               "key":"kndctr_53A16ACB5CC1D3760A495C99_AdobeOrg_consent_check",
               "value":"1",
               "maxAge":7200,
               "attrs":{
                  "SameSite":"None"
               }
            },
            {
               "key":"kndctr_53A16ACB5CC1D3760A495C99_AdobeOrg_identity",
               "value":"CiY1NDc1ODIxNzIzODk5MDY5MzQzMTIzNjQ1NTczNzExNjE4OTA1MFINCLGOvszNLhABGAEgBKABsY6-zM0uqAGHz-z2y82cul3wAbGOvszNLg==",
               "maxAge":34128000,
               "attrs":{
                  "SameSite":"None"
               }
            },
            {
               "key":"kndctr_53A16ACB5CC1D3760A495C99_AdobeOrg_consent",
               "value":"general=in",
               "maxAge":15552000,
               "attrs":{
                  "SameSite":"None"
               }
            }
         ],
         "type":"state:store"
      }
   ]
}
```

| 屬性 | 類型 | 說明 |
| --- | --- | --- |
| `key` | 字串 | **必填**. 條目名稱。 |
| `value` | 字串 | *可選*. 輸入值。 |
| `maxAge` | 整數 | *可選* 條目過期的時間（秒）。 缺少時，應僅儲存當前會話的條目。 |
| `attrs` | `Map<String, String>` | *可選*. 條目屬性的可選清單。 對於具有安全引用器HTTP標頭的所有安全連接， `SameSite` 屬性設定為 `None`。 |


為支援多標籤（即同一屬性中的多個SDK實例，這些實例可能引用不同的組織），所有狀態項都會自動以前置詞 `kndctr_` 和URL安全組織ID。

當客戶端SDK收到 `state:store` 在響應中，它必須執行以下操作：

* 在客戶端儲存條目，並遵守網關提供的過期時間。
* 從客戶端儲存載入它們，並在後續請求中包括所有未過期的項。

以下是以客戶端儲存狀態傳遞的請求示例：

```json
{
   "meta":{
      "state":{
         "entries":[
            {
               "key":"kndctr_53A16ACB5CC1D3760A495C99_AdobeOrg_consent_check",
               "value":"1"
            },
            {
               "key":"kndctr_53A16ACB5CC1D3760A495C99_AdobeOrg_personalization_sessionId",
               "value":"0a88f43e-044b-41a6-a4f3-6c2848bbc672"
            }
         ]
      }
   }
}
```

## 在瀏覽器Cookie中保留客戶端狀態

使用瀏覽器客戶端時，邊緣網路可以自動將條目保留為瀏覽器cookie。 這允許透明狀態儲存支援，因為瀏覽器預設遵守狀態管理協定。

幾乎所有條目在啟用和支援時都作為第一方Cookie進行實例化（請參閱下面的注釋），但當第三方 `adobedc.demdex.net` 已使用域。

由於條目始終按其定義綁定到特定範圍（設備/應用程式），因此邊緣網路將只寫入與當前請求上下文相容的子集。 不寫入的條目在 `state:store` 框。

通常，應用程式範圍的條目總是作為第一方Cookie寫入，而設備範圍的條目作為第三方Cookie寫入。 該決定對呼叫者完全透明，網關根據呼叫上下文決定哪些條目可以被寫入。

調用方必須通過 `meta.state.cookiesEnabled` 標誌：

```json
{
   "meta":{
      "state":{
         "cookiesEnabled":true,
         "domain":"foo.com"
      }
   }
}
```

| 屬性 | 類型 | 說明 |
| --- | --- | --- |
| `cookiesEnabled` | 布林值 | 設定後，啟用對Cookie的支援。 預設值為 `false`。 |
| `domain` | 字串 | 在 `cookiesEnabled: true`。 應在其上寫入Cookie的頂級域。 邊緣網路將使用此值來確定是否可以將狀態保留為cookie。 |

即使通過 `cookiesEnabled` 標誌，只有當請求頂級域與 `domain` 由調用方指定。 當不匹配時，在 `state:store` 框。

在以下情況下，無法寫入第一方Cookie（即使已啟用支援）:

* 請求是在第三方 `adobedc.demdex.net` 。
* 這個請求是第一方 `CNAME` 域，與調用方在 `meta.state.domain`。

## Cookie安全

所有Cookie都 [安全標誌](https://developer.mozilla.org/en-US/docs/Web/HTTP/Cookies#restrict_access_to_cookies) 在可能時啟用。

所有安全Cookie都 [SameSite屬性](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Set-Cookie/SameSite) 設定為 `None`，表示在所有上下文（第1方和跨原點）中發送cookie。

* 對於第一方cookie(`kndcrt_*`) `Secure` 僅當請求上下文安全(HTTPS)和引用者([引用HTTP標頭](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Referer))也是HTTPS。 如果引用者不安全(HTTP), `Secure` 將省略標誌以允許Web SDK讀取它們。 無法從不安全上下文讀取安全cookie。
* 對於第三方cookie(demdex), `Secure` 始終設定標誌，因為所有請求都是HTTPS，因此請求上下文是安全的，並且此cookie永遠不會從JavaScript讀取。

的 `Secure` 標誌不在 [Cookie的元資料表示](#state-as-metadata)。 僅 `SameSite` 屬性。 在這種情況下，客戶有責任正確設定 `Secure` 在 `SameSite` 屬性存在。 Cookie `SameSite=None` 還必須指定 `Secure` 屬性，因為它們需要安全上下文(HTTPS)。
