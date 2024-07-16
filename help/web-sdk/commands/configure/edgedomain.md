---
title: edgeDomain
description: 決定您要傳送資料的目的地根網域。
exl-id: 6beb5116-cd23-42fd-934c-5cf84d1d7153
source-git-commit: 8be502c9eea67119dc537a5d63a6c71e0bff1697
workflow-type: tm+mt
source-wordcount: '215'
ht-degree: 1%

---

# `edgeDomain`

`edgeDomain`屬性可讓您變更Web SDK傳送資料的網域。 使用[第一方Cookie](https://experienceleague.adobe.com/docs/core-services/interface/administration/ec-cookies/cookies-first-party.html?lang=zh-Hant)的組織經常使用此屬性。 資料會傳送至組織自己的網域，然後CNAME記錄會將該資料轉送至Adobe。

您的組織在設定[第一方Cookie](https://experienceleague.adobe.com/docs/core-services/interface/administration/ec-cookies/cookies-first-party.html?lang=zh-Hant)時，會決定此屬性的正確值。 組織通常為此使用專用子網域。 例如，如果您使用網域`example.com`，您可以在`data.example.com`上設定第一方Cookie。

## 使用Web SDK標籤擴充功能設定邊緣網域

設定[設定標籤延伸模組](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md)時的&#x200B;**[!UICONTROL Edge網域]**&#x200B;文字欄位。

1. 使用您的Adobe ID憑證登入[experience.adobe.com](https://experience.adobe.com)。
1. 導覽至&#x200B;**[!UICONTROL 資料彙集]** > **[!UICONTROL 標籤]**。
1. 選取所需的標籤屬性。
1. 導覽至&#x200B;**[!UICONTROL 擴充功能]**，然後按一下[!UICONTROL Adobe Experience Platform Web SDK]卡片上的&#x200B;**[!UICONTROL 設定]**。
1. 找出文字欄位&#x200B;**[!UICONTROL Edge網域]**，然後輸入所要的值。
1. 按一下&#x200B;**[!UICONTROL 儲存]**，然後發佈您的變更。

## 使用Web SDK JavaScript資料庫設定邊緣網域

執行`configure`命令時設定`edgeDomain`字串。 如果您在設定SDK時省略此屬性，其預設值為`edge.adobedc.net`。 如果您想要覆寫Web SDK傳送資料的目標網域，請設定此值。

```js
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "edgeDomain": "data.example.com"
});
```
