---
title: 取得Media Analytics追蹤器
description: 將舊版Media API匯出至視窗物件。
source-git-commit: c55e425f146e4afdb2314b432c9dc48391e02e63
workflow-type: tm+mt
source-wordcount: '150'
ht-degree: 0%

---

# 取得Media Analytics追蹤器

**[!UICONTROL Get Media Analytics tracker]**&#x200B;動作用於取得舊版Media Analytics API。 設定動作並提供物件名稱時，系統會匯出舊版Media Analytics API至該視窗物件。 從舊版Media Analytics移至串流媒體Analytics時，此動作相當實用。

1. 使用您的Adobe ID憑證登入[experience.adobe.com](https://experience.adobe.com)。
1. 導覽至&#x200B;**[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**。
1. 選取所需的標籤屬性。
1. 導覽至&#x200B;**[!UICONTROL Rules]**，然後選取所需的規則。
1. 在[!UICONTROL Actions]下，選取現有動作或建立動作。
1. 將[!UICONTROL Extension]下拉式欄位設為&#x200B;**[!UICONTROL Adobe Experience Platform Web SDK]**，然後將[!UICONTROL Action type]設為&#x200B;**[!UICONTROL Get Media Analytics tracker]**。

![Experience Platform UI影像顯示「取得Media Analytics追蹤器」動作型別。](../assets/get-media-analytics-tracker.png)

此動作包含可設定的單一欄位：

* **[!UICONTROL Export the Media Legacy API to this window object]**：選取要將Media Legacy API匯出到的物件。 如果未提供任何專案，動作會將API匯出至`window.Media`。
