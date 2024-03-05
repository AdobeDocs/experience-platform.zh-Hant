---
title: edgbasePath
description: 用來與Adobe服務互動的端點基本路徑。
source-git-commit: b6e084d2beed58339191b53d0f97b93943154f7c
workflow-type: tm+mt
source-wordcount: '156'
ht-degree: 0%

---

# `edgeBasePath`

此 `edgeBasePath` 屬性會在您與Adobe服務互動時改變目的地路徑。 大多陣列織不需要設定或變更此屬性。

## 使用Web SDK標籤擴充功能的邊緣基本路徑

在「 」中輸入所需的文字 **[!UICONTROL 邊緣基底路徑]** 文字欄位，當 [設定標籤擴充功能](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md).

1. 登入 [experience.adobe.com](https://experience.adobe.com) 使用您的Adobe ID憑證。
1. 瀏覽至 **[!UICONTROL 資料彙集]** > **[!UICONTROL 標籤]**.
1. 選取所需的標籤屬性。
1. 瀏覽至 **[!UICONTROL 擴充功能]**，然後按一下 **[!UICONTROL 設定]** 於 [!UICONTROL Adobe Experience Platform Web SDK] 卡片。
1. 向下捲動至 [!UICONTROL 進階設定] 區段，然後在 **[!UICONTROL 邊緣基底路徑]** 文字欄位。
1. 按一下 **[!UICONTROL 儲存]**，然後發佈您的變更。

## 使用Web SDK JavaScript程式庫的邊緣基本路徑

設定 `edgeBasePath` 文字欄位 `configure` 命令。 如果您忽略此屬性，其預設值為 `ee`. Adobe建議在大部分的設定中省略此屬性。

```js
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "edgeBasePath": "ee"
});
```
