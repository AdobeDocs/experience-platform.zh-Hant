---
title: 使用者端狀態管理
description: 瞭解Adobe Experience PlatformEdge Network如何管理使用者端狀態
seo-description: Learn how the Adobe Experience Platform Edge Network  manages client state
keywords: 使用者端；狀態；管理；邊緣；網路；閘道；api
exl-id: 798ecc52-1af1-4480-a2a3-3198a83538f8
source-git-commit: 85b428b3997d53cbf48e4f112e5c09c0f40f7ee1
workflow-type: tm+mt
source-wordcount: '825'
ht-degree: 1%

---

# 使用者端狀態管理

Edge Network本身是無狀態的（不會維護自己的工作階段）。 但是，有些使用案例需要使用者端狀態持續性，例如：

* 一致的裝置識別（請參閱[訪客識別](visitor-identification.md)）
* 收集並強制執行使用者同意
* 保留個人化工作階段ID

Edge Network使用狀態管理通訊協定，將儲存層面委派給其使用者端/SDK，並在其回應中包含狀態專案。 對於瀏覽器，專案會儲存為Cookie。

使用者端的責任是儲存這些變數，並將其納入所有後續的請求。 使用者端也必須按照閘道的指示，注意專案是否到期。 當專案儲存為Cookie時，瀏覽器會自動執行所有這些工作。

雖然狀態專案一律具有純`String`值（呼叫者/SDK可看到），但您不應以任何方式使用或篡改值。 值結構/格式，甚至是名稱本身都可能隨時變更，這可能會導致內部使用狀態的使用者端出現未預期的行為。 此狀態旨在讓閘道本身或其他邊緣服務一律使用。

## 將使用者端狀態作為中繼資料保留

回應主體中[!DNL Edge Network]傳回的狀態是型別為`state:store`的`Handle`物件。

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
| `key` | 字串 | **必要**。 專案名稱。 |
| `value` | 字串 | *選擇性*。 專案值。 |
| `maxAge` | 整數 | *選擇性*&#x200B;專案到期前的時間（秒）。 當遺失時，應該只為目前的工作階段儲存專案。 |
| `attrs` | `Map<String, String>` | *選擇性*。 專案屬性的選擇性清單。 對於具有安全參照HTTP標頭的所有安全連線，`SameSite`屬性皆設為`None`。 |


為了支援多重標籤（亦即相同屬性中的多個SDK執行個體，可能會參考不同的組織），所有狀態專案都會自動加上前置詞`kndctr_`和URL安全的組織ID。

使用者端SDK在回應中收到`state:store`控制代碼時，必須執行下列動作：

* 儲存使用者端專案，遵守閘道所提供的到期時間。
* 從使用者端存放區載入這些專案，並在後續請求中包含所有未過期的專案。

以下是以使用者端儲存狀態傳遞的請求範例：

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

## 在瀏覽器Cookie中儲存使用者端狀態

使用瀏覽器使用者端時，Edge Network會自動將專案保留為瀏覽器Cookie。 這可提供透明狀態儲存支援，因為瀏覽器預設會遵守狀態管理通訊協定。

幾乎所有專案在啟用及支援時都會具體化為第一方Cookie （請參閱下面的附註），但是閘道也可以在使用第三方`adobedc.demdex.net`網域時儲存一些第三方Cookie。

由於專案依其定義一律繫結至特定範圍（裝置/應用程式），因此Edge Network只會寫入與目前要求內容相容的子集。 未寫入的專案為
在`state:store`控制代碼中傳回。

一般而言，應用程式範圍專案一律會寫入為第一方Cookie，而裝置範圍專案則會寫入為第三方Cookie。 此決定對於呼叫者完全透明，閘道會根據呼叫內容決定可以寫入哪些專案。

呼叫者必須透過`meta.state.cookiesEnabled`旗標明確啟用將使用者端狀態儲存為Cookie的支援：

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
| `cookiesEnabled` | 布林值 | 設定後，會啟用對Cookie的支援。 預設值為 `false`。 |
| `domain` | 字串 | `cookiesEnabled: true`時需要。 應在其上寫入Cookie的頂層網域。 Edge Network將使用此值來決定是否可將狀態保留為Cookie。 |

即使透過`cookiesEnabled`旗標啟用Cookie支援，Adobe Experience PlatformEdge Network也只會在要求最上層網域符合呼叫者指定的`domain`時，寫入狀態專案。 當有不相符的專案時，會在`state:store`控制代碼中傳回專案。

在下列情況下，無法寫入第一方Cookie （即使已啟用支援）：

* 要求來自協力廠商`adobedc.demdex.net`網域。
* 要求來自第一方`CNAME`網域，不同於呼叫者在`meta.state.domain`中指定的網域。

## Cookie安全性

所有Cookie都儘可能啟用[安全旗標](https://developer.mozilla.org/en-US/docs/Web/HTTP/Cookies#restrict_access_to_cookies)。

所有安全Cookie的[SameSite屬性](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Set-Cookie/SameSite)都設為`None`，這表示Cookie會在所有內容（第一方和跨來源）中傳送。

* 針對第一方Cookie (`kndcrt_*`)，`Secure`標幟只有在要求內容安全(HTTPS)且反向連結（[Referer HTTP標頭](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Referer)）也是HTTPS時才設定。 如果反向連結不安全(HTTP)，則會省略`Secure`旗標，以允許Web SDK讀取它們。 無法從不安全的內容讀取安全的Cookie。
* 第三方Cookie (demdex)一律會設定`Secure`標幟，因為所有要求都是HTTPS，因此要求內容是安全的，而且絕對不會從JavaScript讀取此Cookie。

`Secure`旗標不存在於Cookie](#state-as-metadata)的[中繼資料表示中。 僅包含`SameSite`屬性。 在此情況下，只要有`SameSite`屬性出現，使用者端有責任正確設定`Secure`標幟。 具有`SameSite=None`的Cookie也必須指定`Secure`屬性，因為它們需要安全內容(HTTPS)。
