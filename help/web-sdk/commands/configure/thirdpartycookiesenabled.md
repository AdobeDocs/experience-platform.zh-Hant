---
title: thirdpartyCookiesEnabled
description: 允許使用第三方Cookie來識別訪客。
source-git-commit: b6e084d2beed58339191b53d0f97b93943154f7c
workflow-type: tm+mt
source-wordcount: '226'
ht-degree: 0%

---

# `thirdPartyCookiesEnabled`

此 `thirdPartyCookiesEnabled` 屬性是布林值，可決定Web SDK是否會在第三方內容中設定Cookie。 如果您想要識別您組織擁有的子網域或網域之間的訪客，啟用此選項會很有用。 不過，許多現代瀏覽器會限制第三方Cookie的設定和到期日。

啟用此選項後，Web SDK會使用Adobe Audience Manager來協助識別訪客。 停用此選項時，會停用Audience Manager呼叫。 另請參閱 [瞭解向Demdex網域進行的呼叫](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/demdex-calls.html?lang=zh-Hant) 詳細資訊，請參閱Audience Manager使用手冊。

## 使用Web SDK標籤擴充功能啟用第三方Cookie

選取 **[!UICONTROL 使用第三方Cookie]** 核取方塊，當 [設定標籤擴充功能](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md).

1. 登入 [experience.adobe.com](https://experience.adobe.com) 使用您的Adobe ID憑證。
1. 瀏覽至 **[!UICONTROL 資料彙集]** > **[!UICONTROL 標籤]**.
1. 選取所需的標籤屬性。
1. 瀏覽至 **[!UICONTROL 擴充功能]**，然後按一下 **[!UICONTROL 設定]** 於 [!UICONTROL Adobe Experience Platform Web SDK] 卡片。
1. 向下捲動至 [!UICONTROL 身分] 區段，然後選取核取方塊 **[!UICONTROL 使用第三方Cookie]**.
1. 按一下 **[!UICONTROL 儲存]**，然後發佈您的變更。

## 使用Web SDK JavaScript程式庫啟用第三方Cookie

設定 `thirdPartyCookiesEnabled` 執行時的布林值 `configure` 命令。 如果您在設定Web SDK時省略此屬性，其預設值為 `true`. 將此值設為 `false` 如果您不希望Web SDK使用Audience Manager來協助識別訪客。

```js
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "thirdPartyCookiesEnabled": false
});
```
