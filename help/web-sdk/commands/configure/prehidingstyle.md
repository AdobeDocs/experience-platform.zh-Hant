---
title: 預先隱藏樣式
description: 建立CSS定義，允許個人化內容載入而不發生閃爍。
source-git-commit: b6e084d2beed58339191b53d0f97b93943154f7c
workflow-type: tm+mt
source-wordcount: '271'
ht-degree: 0%

---

# `prehidingStyle`

此 `prehidingStyle` 屬性可讓您定義CSS選取器，以隱藏個人化內容直到載入為止。 此屬性在同步Web SDK實施中非常有用，可避免忽隱忽現的情形。 Adobe建議使用 [預先隱藏程式碼片段](../../personalization/manage-flicker.md) 用於非同步Web SDK實作。

您在此屬性中定義的CSS選取器會在您第一次執行時開始隱藏內容 [`sendEvent`](../sendevent/overview.md) 指令。 收到Adobe的回應時（通常包括個人化內容），內容會取消隱藏。 如果符合下列條件，內容也會取消隱藏 `sendEvent` 命令失敗或逾時。

如果您同時包含兩者 `prehidingStyle` 以及實作中的預先隱藏程式碼片段，預先隱藏程式碼片段的優先順序高於此設定屬性。

## 使用Web SDK標籤擴充功能預先隱藏樣式

選取 **[!UICONTROL 提供預先隱藏樣式]** 按鈕時間 [設定標籤擴充功能](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md).

1. 登入 [experience.adobe.com](https://experience.adobe.com) 使用您的Adobe ID憑證。
1. 瀏覽至 **[!UICONTROL 資料彙集]** > **[!UICONTROL 標籤]**.
1. 選取所需的標籤屬性。
1. 瀏覽至 **[!UICONTROL 擴充功能]**，然後按一下 **[!UICONTROL 設定]** 於 [!UICONTROL Adobe Experience Platform Web SDK] 卡片。
1. 向下捲動至 [!UICONTROL 個人化] 區段，然後選取按鈕 **[!UICONTROL 提供預先隱藏樣式]**.
1. 此按鈕會開啟含有CSS編輯器的模型視窗。 插入所需的CSS選取器和宣告區塊，然後按一下 **[!UICONTROL 儲存]** 以關閉強制回應視窗。
1. 按一下 **[!UICONTROL 儲存]** 在擴充功能設定底下，然後發佈變更。

## 使用Web SDK JavaScript程式庫預先隱藏樣式

設定 `prehidingStyle` 字串 `configure` 命令。 如果您在設定Web SDK時省略此屬性，則執行第一個 `sendEvent` 指令。 針對同步載入的程式庫，將此值設為所需的CSS選取器和宣告區塊。

```js
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "prehidingStyle": "#container { opacity: 0 !important }"
});
```
