---
title: 客戶端狀態管理
description: 了解Adobe Experience Platform Edge Network如何管理用戶端狀態
seo-description: Learn how the Adobe Experience Platform Edge Network  manages client state
keywords: 用戶端；狀態；管理；邊緣；網路；閘道；API
exl-id: 798ecc52-1af1-4480-a2a3-3198a83538f8
source-git-commit: 85b428b3997d53cbf48e4f112e5c09c0f40f7ee1
workflow-type: tm+mt
source-wordcount: '850'
ht-degree: 2%

---

# 客戶端狀態管理

邊緣網路本身無狀態（不會維護自己的工作階段）。 不過，某些使用案例需要用戶端狀態持續性，例如：

* 一致的設備標識(請參閱 [訪客身分識別](visitor-identification.md))
* 收集並強制使用者同意
* 保留個人化工作階段ID

邊緣網路使用狀態管理通訊協定，將儲存方面委派給其用戶端/SDK，並在其回應中包含狀態項目。 若為瀏覽器，項目會儲存為Cookie。

用戶端的責任是儲存這些請求，並將其納入後續的所有請求中。 客戶端還必須按照網關的指示處理條目的正確過期。 當登入項目儲存為Cookie時，瀏覽器會自動執行這一切。

儘管州級入口總是很清楚 `String` 值（可見於呼叫者/SDK），您不應以任何方式使用或篡改值。 值結構/格式甚至名稱本身可能隨時都會變更，這可能導致內部使用狀態之用戶端發生非預期行為。 狀態旨在始終由網關本身或其他邊緣服務使用。

## 以中繼資料的形式保留用戶端狀態

由 [!DNL Edge Network] 在回應內文中為 `Handle` 具有類型的對象 `state:store`.

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
| `key` | 字串 | **必填**. 項目名稱。 |
| `value` | 字串 | *可選*. 輸入值。 |
| `maxAge` | 整數 | *可選* 項目過期的時間（以秒為單位）。 遺失時，應僅儲存目前工作階段的項目。 |
| `attrs` | `Map<String, String>` | *可選*. 登入屬性的選用清單。 對於具有安全引用者HTTP標頭的所有安全連接， `SameSite` 屬性設為 `None`. |


為了支援多標籤（亦即在相同屬性中有多個SDK例項，可能會參照不同的組織），所有狀態項目都會自動加上前置詞 `kndctr_` 和URL安全的組織ID。

用戶端SDK收到 `state:store` 在回應中處理，它必須執行下列動作：

* 在客戶端儲存條目，並遵守網關提供的到期時間。
* 從用戶端存放區載入，並在後續請求中納入所有未過期的項目。

以下是在用戶端儲存狀態中傳遞的請求範例：

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

## 瀏覽器Cookie中持續存在用戶端狀態

使用瀏覽器用戶端時，邊緣網路會自動將項目保留為瀏覽器Cookie。 這可支援透明狀態儲存，因為瀏覽器預設會遵守狀態管理通訊協定。

幾乎所有的項目在啟用和支援時都會實化為第一方Cookie（請參閱下方注意事項），但當第三方時，閘道也可以儲存某些第三方Cookie `adobedc.demdex.net` 已使用網域。

由於條目的定義始終綁定到特定範圍（設備/應用程式），因此只有與當前請求上下文相容的子集才由邊緣網路寫入。 未寫入的項在 `state:store` 手柄。

一般來說，應用程式範圍的項目一律會寫入為第一方Cookie，而裝置範圍的項目則會寫入為第三方Cookie。 該決定對呼叫者完全透明，網關根據呼叫上下文決定可以寫入哪些條目。

呼叫者必須透過 `meta.state.cookiesEnabled` 標幟：

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
| `cookiesEnabled` | 布林值 | 設定後，即可啟用對Cookie的支援。 預設值為 `false`。 |
| `domain` | 字串 | 必要時機 `cookiesEnabled: true`. 應寫入Cookie的頂層網域。 邊緣網路會使用此值來決定狀態是否可持續保存為Cookie。 |

即使透過 `cookiesEnabled` 標幟時，Adobe Experience Platform邊緣網路只會在請求頂層網域符合 `domain` 由調用方指定。 當出現不相符時，會在 `state:store` 手柄。

在下列情況下，無法寫入第一方Cookie（即使已啟用支援亦然）:

* 請求來自第三方 `adobedc.demdex.net` 網域。
* 要求是第一方 `CNAME` 域，不同於 `meta.state.domain`.

## Cookie安全性

所有Cookie皆具有 [安全標幟](https://developer.mozilla.org/en-US/docs/Web/HTTP/Cookies#restrict_access_to_cookies) 盡可能啟用。

所有安全Cookie皆具有 [SameSite屬性](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Set-Cookie/SameSite) 設為 `None`，表示會在所有內容（第一方和跨原始）中傳送cookie。

* 針對第一方Cookie(`kndcrt_*`), `Secure` 只有在要求內容安全(HTTPS)且反向連結([參考HTTP標題](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Referer))也是HTTPS。 如果反向連結不安全(HTTP)，則 `Secure` 標幟皆會省略，以允許Web SDK讀取這些標幟。 無法從不安全的內容讀取安全Cookie。
* 若為第三方Cookie(demdex)，則 `Secure` 標幟一律會設定，因為所有要求都是HTTPS，因此要求內容安全，且絕不會從JavaScript讀取此Cookie。

此 `Secure` 標幟不存在於 [cookie的中繼資料表示](#state-as-metadata). 僅 `SameSite` 屬性。 在此情況下，客戶有責任正確設定 `Secure` 標幟，只要 `SameSite` 屬性存在。 Cookie與 `SameSite=None` 也必須指定 `Secure` 屬性，因為它們需要安全內容(HTTPS)。
