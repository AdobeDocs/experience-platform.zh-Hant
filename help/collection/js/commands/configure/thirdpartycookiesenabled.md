---
title: thirdpartyCookiesEnabled
description: 允許使用第三方Cookie來識別訪客。
exl-id: f241a9ae-a892-46a5-b0dd-5ac72a44d4ac
source-git-commit: c6a2b9700f0a688f65fec9febf5622c6c7b6aafa
workflow-type: tm+mt
source-wordcount: '193'
ht-degree: 0%

---

# `thirdPartyCookiesEnabled`

`thirdPartyCookiesEnabled`屬性是布林值，可決定Web SDK是否會在第三方內容中設定Cookie。 如果您想要識別您組織擁有的子網域或網域之間的訪客，啟用此選項會很有用。 不過，許多現代瀏覽器會限制第三方Cookie的設定和到期日。 如果訪客的瀏覽器不支援第三方Cookie，則此屬性不會產生任何效用。

`thirdPartyCookiesEnabled`屬性也會控制是否可以在[`CORE ID`](/help/collection/use-cases/identity/id-overview.md#tracking-coreid-web-sdk)呼叫上要求[`getIdentity`](../getidentity.md)。

啟用此選項後，網頁SDK會使用Adobe Audience Manager來協助識別訪客。 停用此選項時，會停用對Audience Manager的呼叫。 如需詳細資訊，請參閱Audience Manager使用手冊中的[瞭解向Demdex網域進行的呼叫](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/demdex-calls.html?lang=zh-Hant)。

執行`thirdPartyCookiesEnabled`命令時設定`configure`布林值。 如果您在設定Web SDK時省略此屬性，其預設值為`true`。 如果您不希望網頁SDK使用Audience Manager來協助識別訪客，請將此值設為`false`。

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  thirdPartyCookiesEnabled: false
});
```

## 使用網頁SDK標籤擴充功能啟用第三方Cookie

您可以使用[身分組態設定](/help/tags/extensions/client/web-sdk/configure/identity.md#use-third-party-cookies)，在Web SDK標籤擴充功能中設定此設定。
