---
title: appendIdentityToUrl
description: 在應用程式、網頁和跨網域之間，更準確地提供個人化體驗。
exl-id: 09dd03bd-66d8-4d53-bda8-84fc4caadea6
source-git-commit: c2564f1b9ff036a49c9fa4b9e9ffbdbc598a07a8
workflow-type: tm+mt
source-wordcount: '226'
ht-degree: 0%

---

# `appendIdentityToUrl`

`appendIdentityToUrl`命令可讓您將使用者識別碼新增至URL做為查詢字串。 此動作可讓您在網域之間攜帶訪客的身分，以防止同時包含網域或管道的資料集出現重複訪客計數。 它適用於Web SDK 2.11.0或更新版本。

產生並附加至URL的查詢字串為`adobe_mc`。 如果網頁SDK找不到ECID，它會呼叫`/acquire`端點以產生一個。

>[!NOTE]
>
>如果尚未提供同意，則傳回此方法的URL不會變更。 此命令會立即執行；不會等待同意更新。

以URL作為引數執行`appendIdentityToUrl`命令。 此方法會傳回URL，並附加識別碼作為查詢字串。

```js
alloy("appendIdentityToUrl",
  {
    url: document.location.href
  }
);
```

您可以為頁面上收到的所有點按新增事件接聽程式，並檢視URL是否符合任何需要的網域。 如果包含，則將身分附加至URL並重新導向使用者。

```js
document.addEventListener("click", event => {
  // Check if the click was a link
  const anchor = event.target.closest("a");
  if (!anchor || !anchor.href) return;

  // Check if the link points to the desired domain
  const url = new URL(anchor.href);
  if (!url.hostname.endsWith(".adobe.com") && !url.hostname.endsWith(".behance.com")) return;

  // Append the identity to the URL, then direct the user to the URL
  event.preventDefault();
  alloy("appendIdentityToUrl", {url: anchor.href}).then(result => { window.open(result.url, anchor.target || "_self"); });
});
```

這個命令支援[`edgeConfigOverrides`](configure/edgeconfigoverrides.md)物件。

## 回應物件

當使用此命令[處理回應](command-responses.md)時，回應物件包含&#x200B;**`url`**，包含身分資訊的新URL已新增為查詢字串引數。

## 使用網路SDK標籤擴充功能將身分附加至URL

與此命令等同的Web SDK標籤擴充功能是[使用身分識別](/help/tags/extensions/client/web-sdk/actions/redirect-with-identity.md)的重新導向。
