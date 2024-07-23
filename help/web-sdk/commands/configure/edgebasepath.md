---
title: edgbasePath
description: 用來與Adobe服務互動的端點基本路徑。
exl-id: 3542575d-ad02-415c-8e47-97c877dfdd9d
source-git-commit: 8fc0fd96f13f0642f7671d0e0f4ecfae8ab6761f
workflow-type: tm+mt
source-wordcount: '156'
ht-degree: 0%

---

# `edgeBasePath`

當您與Adobe服務互動時，`edgeBasePath`屬性會變更目的地路徑。 大多陣列織不需要設定或變更此屬性。

## 使用Web SDK標籤擴充功能的Edge基本路徑

當[設定標籤延伸模組](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md)時，請在&#x200B;**[!UICONTROL Edge基本路徑]**&#x200B;文字欄位中輸入所要的文字。

1. 使用您的Adobe ID憑證登入[experience.adobe.com](https://experience.adobe.com)。
1. 導覽至&#x200B;**[!UICONTROL 資料彙集]** > **[!UICONTROL 標籤]**。
1. 選取所需的標籤屬性。
1. 導覽至&#x200B;**[!UICONTROL 擴充功能]**，然後按一下[!UICONTROL Adobe Experience Platform Web SDK]卡片上的&#x200B;**[!UICONTROL 設定]**。
1. 向下捲動至[!UICONTROL 進階設定]區段，然後在&#x200B;**[!UICONTROL Edge基本路徑]**&#x200B;文字欄位中輸入所需的值。
1. 按一下&#x200B;**[!UICONTROL 儲存]**，然後發佈您的變更。

## 使用Web SDK JavaScript程式庫的Edge基本路徑

執行`configure`命令時設定`edgeBasePath`文字欄位。 如果您省略此屬性，其預設值為`ee`。 Adobe建議在大部分的設定中省略此屬性。

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  edgeBasePath: "ee"
});
```
