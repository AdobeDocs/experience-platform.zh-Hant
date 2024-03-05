---
title: edgeDomain
description: 決定您要傳送資料的目的地根網域。
source-git-commit: f75dcfc945be2f45c1638bdd4d670288aef6e1e6
workflow-type: tm+mt
source-wordcount: '215'
ht-degree: 1%

---

# `edgeDomain`

此 `edgeDomain` 屬性可讓您變更Web SDK傳送資料的網域。 此屬性經常由使用的組織使用 [第一方Cookie](https://experienceleague.adobe.com/docs/core-services/interface/administration/ec-cookies/cookies-first-party.html?lang=zh-Hant). 資料會傳送至組織自己的網域，然後CNAME記錄會將該資料轉送至Adobe。

您的組織在設定時，會為此屬性決定正確的值 [第一方Cookie](https://experienceleague.adobe.com/docs/core-services/interface/administration/ec-cookies/cookies-first-party.html?lang=zh-Hant). 組織通常為此使用專用子網域。 例如，如果您使用網域 `example.com`，您可以在上設定第一方Cookie `data.example.com`.

## 使用Web SDK標籤擴充功能設定邊緣網域

設定 **[!UICONTROL 邊緣網域]** 文字欄位，當 [設定標籤擴充功能](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md).

1. 登入 [experience.adobe.com](https://experience.adobe.com) 使用您的Adobe ID憑證。
1. 瀏覽至 **[!UICONTROL 資料彙集]** > **[!UICONTROL 標籤]**.
1. 選取所需的標籤屬性。
1. 瀏覽至 **[!UICONTROL 擴充功能]**，然後按一下 **[!UICONTROL 設定]** 於 [!UICONTROL Adobe Experience Platform Web SDK] 卡片。
1. 找到文字欄位 **[!UICONTROL 邊緣網域]**，然後輸入所需的值。
1. 按一下 **[!UICONTROL 儲存]**，然後發佈您的變更。

## 使用Web SDK JavaScript程式庫設定邊緣網域

設定 `edgeDomain` 字串 `configure` 命令。 如果您在設定SDK時省略此屬性，其預設值為 `edge.adobedc.net`. 如果您想要覆寫Web SDK傳送資料的目標網域，請設定此值。

```js
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "edgeDomain": "data.example.com"
});
```
