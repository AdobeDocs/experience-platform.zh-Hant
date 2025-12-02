---
title: Cookie
description: 手動寫入、編輯或刪除標籤屬性的Cookie。
source-git-commit: 434d6913ea391b127b4b52c8494730c496bbcfe2
workflow-type: tm+mt
source-wordcount: '382'
ht-degree: 7%

---

# `cookie`

`_satellite.cookie`物件包含可讓您寫入、編輯或刪除標籤規則可參考之Cookie的方法。 它是[`js-cookie`](https://github.com/js-cookie/js-cookie)的部分復本，包含該資料庫的許多核心功能。

## `cookie.set()`

`set()`方法會寫入您的標籤屬性可參考的Cookie。

```ts
_satellite.cookie.set(name: string, value: string, attributes?: {
  expires?: number | Date;
  path?: string;
  domain?: string;
  secure?: boolean;
  sameSite?: 'Strict' | 'Lax' | 'None';
}): string
```

可以使用下列方法引數：

| 名稱 | 類型 | 必要 | 說明 |
|---|---|---|---|
| **`name`** | `string` | 是 | Cookie的名稱。 |
| **`value`** | `string` | 是 | Cookie的值 |
| **`attributes`** | `object` | 無 | 您希望Cookie具備的其他屬性。 |

`attributes`物件支援下列屬性：

| 屬性名稱 | 類型 | 必要 | 預設 | 說明 |
|---|---|---|---|---|
| **`expires`** | `number`或[`Date`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Date) | 無 | Cookie會在瀏覽器作業階段結束時到期 | 您希望Cookie過期的天數。 |
| **`path`** | `string` | 無 | Cookie在整個網站中可見 | 在您網域中可看到Cookie的位置。 |
| **`domain`** | `string` | 無 | Cookie對建立它的網域可見 | 可看到Cookie的有效網域（具有或不具有子網域）。 如果納入的網域不含子網域，則該網域下的所有子網域都會看見Cookie。 |
| **`secure`** | `boolean` | 無 | 未設定屬性 | 決定Cookie是否需要安全通訊協定(`https://`)。 如果省略，則不需要安全通訊協定。 |
| **`sameSite`** | `'Strict' \| 'Lax' \| 'None'` | 無 | 未設定屬性 | 可讓您設定Cookie的[`sameSite`](https://developer.mozilla.org/en-US/docs/Web/HTTP/Reference/Headers/Set-Cookie#samesitesamesite-value)屬性。 如果您將`sameSite`設為`None`，您也必須將`secure`設為`true`。 |

```js
// Sets a cookie valid across the entire site, expires on session close
_satellite.cookie.set('simple_session_cookie', 'value');

// Sets a cookie that expires 7 days from now, valid across the entire site
_satellite.cookie.set('seven_day_cookie', 'value', { expires: 7 });

// Sets a cookie that expires 14 days from now, valid only on the current page
_satellite.cookie.set('page_specific_cookie', 'value', { expires: 14, path: '/' });

// Cross-site compatible cookie (requires HTTPS)
_satellite.cookie.set('cross_site_cookie', 'value', { secure: true, sameSite: 'None' });
```

叫用此方法會寫入所需的Cookie並傳回所寫入的序列化Cookie字串。 此字串主要用於偵錯或記錄目的。

```text
'written_cookie=value; path=/'
```

>[!TIP]
>
>舊版標籤物件已使用`_satellite.setCookie()`。 `setCookie()`方法已過時，而改用`_satellite.cookie.set()`。

## `cookie.get()`

`get()`方法傳回Cookie值。

```ts
_satellite.cookie.get(name: string): string | undefined;
```

| 名稱 | 類型 | 必要 | 說明 |
|---|---|---|---|
| **`name`** | `string` | 是 | 您要從中擷取值的Cookie名稱（區分大小寫）。 |

如果Cookie名稱存在，則會傳回Cookie值。 如果Cookie名稱不存在，則會傳回`undefined`。

>[!TIP]
>
>舊版標籤物件已使用`_satellite.getCookie()`。 `getCookie()`方法已過時，而改用`_satellite.cookie.get()`。

## `cookie.remove()`

`remove()`方法會刪除您已設定的Cookie。

```ts
_satellite.cookie.remove(name: string, attributes?: {
  path?: string;
  domain?: string;
}): void
```

| 名稱 | 類型 | 必要 | 說明 |
|---|---|---|---|
| **`name`** | `string` | 是 | 您要移除的Cookie名稱。 |
| **`attributes`** | `object` | 無 | 與您要移除之Cookie相關聯的屬性。 如果您使用`path`或`domain`屬性設定Cookie，請在移除Cookie時包含這些相同的屬性。 若未包含這些屬性，並不會移除Cookie。 |

```js
// Creates a session cookie
_satellite.cookie.set('session_cookie', 'Cookie value');

// Removes the above cookie
_satellite.cookie.remove('session_cookie');

// Creates a cookie that is only visible on the current page
_satellite.cookie.set('page_specific_cookie', 'value', { path: '/' });

// This remove method does nothing because it does not match the path and domain attributes of the cookie set
_satellite.cookie.remove('page_specific_cookie');

// This remove method works correctly for the page-specific cookie
_satellite.cookie.remove('page_specific_cookie', { path: '/' });
```

>[!TIP]
>
>舊版標籤物件已使用`_satellite.removeCookie()`。 `removeCookie()`方法已過時，而改用`_satellite.cookie.remove()`。
