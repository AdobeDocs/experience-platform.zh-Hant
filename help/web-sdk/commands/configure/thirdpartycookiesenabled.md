---
title: thirdpartyCookiesEnabled
description: 允許使用第三方Cookie來識別訪客。
exl-id: f241a9ae-a892-46a5-b0dd-5ac72a44d4ac
source-git-commit: a884790aa48fb97eebe2421124fc5d5f76c8a79d
workflow-type: tm+mt
source-wordcount: '237'
ht-degree: 0%

---


# `thirdPartyCookiesEnabled`

`thirdPartyCookiesEnabled`屬性是布林值，可決定Web SDK是否會在第三方內容中設定Cookie。 如果您想要識別您組織擁有的子網域或網域之間的訪客，啟用此選項會很有用。 不過，許多現代瀏覽器會限制第三方Cookie的設定和到期日。

`thirdPartyCookiesEnabled`屬性也會控制是否可以在[`getIdentity`](../getidentity.md)呼叫上要求[`CORE ID`](../../identity/overview.md#tracking-coreid-web-sdk)。

啟用此選項後，Web SDK會使用Adobe Audience Manager來協助識別訪客。 停用此選項時，會停用Audience Manager呼叫。 如需詳細資訊，請參閱Audience Manager使用手冊中的[瞭解向Demdex網域進行的呼叫](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/demdex-calls.html?lang=zh-Hant)。

## 使用Web SDK標籤擴充功能啟用第三方Cookie

選取[設定標籤擴充功能](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md)時的&#x200B;**[!UICONTROL 使用第三方Cookie]**&#x200B;核取方塊。

1. 使用您的Adobe ID憑證登入[experience.adobe.com](https://experience.adobe.com)。
1. 導覽至&#x200B;**[!UICONTROL 資料彙集]** > **[!UICONTROL 標籤]**。
1. 選取所需的標籤屬性。
1. 導覽至&#x200B;**[!UICONTROL 擴充功能]**，然後按一下[!UICONTROL Adobe Experience Platform Web SDK]卡片上的&#x200B;**[!UICONTROL 設定]**。
1. 向下捲動至[!UICONTROL 身分識別]區段，然後選取核取方塊&#x200B;**[!UICONTROL 使用第三方Cookie]**。
1. 按一下&#x200B;**[!UICONTROL 儲存]**，然後發佈您的變更。

## 使用Web SDK JavaScript資料庫啟用第三方Cookie

執行`configure`命令時設定`thirdPartyCookiesEnabled`布林值。 如果您在設定Web SDK時省略此屬性，其預設值為`true`。 如果您不希望Web SDK使用Audience Manager來協助識別訪客，請將此值設為`false`。

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  thirdPartyCookiesEnabled: false
});
```
