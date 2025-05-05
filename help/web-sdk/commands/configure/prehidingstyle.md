---
title: 預先隱藏樣式
description: 建立CSS定義，允許個人化內容載入而不發生閃爍。
exl-id: 3693542a-69d3-4ad8-bea4-4cabf7d80563
source-git-commit: 8fc0fd96f13f0642f7671d0e0f4ecfae8ab6761f
workflow-type: tm+mt
source-wordcount: '271'
ht-degree: 0%

---

# `prehidingStyle`

`prehidingStyle`屬性可讓您定義CSS選取器以隱藏個人化內容，直到其載入為止。 此屬性在同步Web SDK實施中非常有用，可避免忽隱忽現的情形。 Adobe建議針對非同步Web SDK實作使用[預先隱藏程式碼片段](../../personalization/manage-flicker.md)。

您在頁面上執行第一個[`sendEvent`](../sendevent/overview.md)命令時，在此屬性中定義的CSS選取器會開始隱藏內容。 收到Adobe的回應時（通常包括個人化內容），內容會取消隱藏。 如果`sendEvent`命令失敗或逾時，也會取消隱藏內容。

如果您在實施中同時包含`prehidingStyle`和預先隱藏程式碼片段，則預先隱藏程式碼片段會優先於此設定屬性。

## 使用Web SDK標籤擴充功能預先隱藏樣式

選取[設定標籤延伸時](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md)的&#x200B;**[!UICONTROL 提供預先隱藏樣式]**&#x200B;按鈕。

1. 使用您的Adobe ID憑證登入[experience.adobe.com](https://experience.adobe.com)。
1. 導覽至&#x200B;**[!UICONTROL 資料彙集]** > **[!UICONTROL 標籤]**。
1. 選取所需的標籤屬性。
1. 導覽至&#x200B;**[!UICONTROL 擴充功能]**，然後按一下[!UICONTROL Adobe Experience Platform Web SDK]卡片上的&#x200B;**[!UICONTROL 設定]**。
1. 向下捲動至[!UICONTROL Personalization]區段，然後選取按鈕&#x200B;**[!UICONTROL 提供預先隱藏樣式]**。
1. 此按鈕會開啟含有CSS編輯器的模型視窗。 插入所需的CSS選取器和宣告區塊，然後按一下[儲存]以關閉模型視窗。**&#x200B;**
1. 按一下擴充功能設定下的&#x200B;**[!UICONTROL [儲存]**]，然後發佈您的變更。

## 使用Web SDK JavaScript程式庫預先隱藏樣式

執行`configure`命令時設定`prehidingStyle`字串。 如果您在設定Web SDK時省略此屬性，則在頁面上執行第一個`sendEvent`命令時不會隱藏任何內容。 針對同步載入的程式庫，將此值設為所需的CSS選取器和宣告區塊。

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  prehidingStyle: "#container { opacity: 0 !important }"
});
```
