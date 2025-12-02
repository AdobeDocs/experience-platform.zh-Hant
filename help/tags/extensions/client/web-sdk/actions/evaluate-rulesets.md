---
title: 評估規則集
description: 手動觸發規則集評估。
source-git-commit: 46e5d007b27eaa67c9ee49e35a711424de383d68
workflow-type: tm+mt
source-wordcount: '138'
ht-degree: 0%

---

# 評估規則集

**[!UICONTROL Evaluate rulesets]**&#x200B;動作型別可讓您手動觸發規則集評估。 Adobe Journey Optimizer會傳回規則集以支援瀏覽器內訊息等功能。

1. 使用您的Adobe ID憑證登入[experience.adobe.com](https://experience.adobe.com)。
1. 導覽至&#x200B;**[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**。
1. 選取所需的標籤屬性。
1. 導覽至&#x200B;**[!UICONTROL Rules]**，然後選取所需的規則。
1. 在[!UICONTROL Actions]下，選取現有動作或建立動作。
1. 將[!UICONTROL Extension]下拉式欄位設為&#x200B;**[!UICONTROL Adobe Experience Platform Web SDK]**，然後將[!UICONTROL Action type]設為&#x200B;**[!UICONTROL Evaluate rulesets]**。

![顯示[評估規則集]回應動作型別的Experience Platform使用者介面影像。](../assets/evaluate-rulesets.png)

## 可用欄位

此動作型別支援下列選項：

* **[!UICONTROL Render visual personalization decisions]**：核取方塊，在啟用時，會針對符合的規則集專案呈現視覺化個人化決策。
* **[!UICONTROL Decision context]**：在評估裝置上決策的Adobe Journey Optimizer規則集時使用的機碼值對應。 您可以手動或透過資料元素提供決定內容。
