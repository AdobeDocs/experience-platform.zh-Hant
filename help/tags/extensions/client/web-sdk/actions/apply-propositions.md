---
title: 套用主張
description: 可在單頁應用程式中轉譯主張，而不增加量度。
source-git-commit: 217282135bcd750740f4d3f8c6e17a0b8f9578bd
workflow-type: tm+mt
source-wordcount: '352'
ht-degree: 0%

---

# 套用主張

**[!UICONTROL Apply propositions]**&#x200B;動作型別可讓您在不增加量度的情況下，在單頁應用程式中轉譯主張。 在使用單頁應用程式時，如果頁面的部分重新呈現，可能會覆寫已套用至頁面的任何個人化，此動作型別會很有用。

1. 使用您的Adobe ID憑證登入[experience.adobe.com](https://experience.adobe.com)。
1. 導覽至&#x200B;**[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**。
1. 選取所需的標籤屬性。
1. 導覽至&#x200B;**[!UICONTROL Rules]**，然後選取所需的規則。
1. 在[!UICONTROL Actions]下，選取現有動作或建立動作。
1. 將[!UICONTROL Extension]下拉式欄位設為&#x200B;**[!UICONTROL Adobe Experience Platform Web SDK]**，然後將[!UICONTROL Action type]設為&#x200B;**[!UICONTROL Apply propositions]**。

![顯示「套用主張」動作型別的Experience Platform Tags UI。](../assets/apply-propositions.png)

## 使用案例

您可以針對各種使用案例使用此動作型別，例如：

1. **呈現mbox HTML選件**。 透過&#x200B;**[!UICONTROL Send event]**&#x200B;動作之範圍或介面明確要求的主張不會自動轉譯。 您可以使用&#x200B;**[!UICONTROL Apply propositions]**&#x200B;動作型別，指定主張中繼資料，告訴Web SDK在何處轉譯它們。
2. **在單頁應用程式上呈現檢視的選件**。 呈現檢視變更事件時，如果分析資料尚未準備就緒，您可以使用&#x200B;**[!UICONTROL Apply propositions]**&#x200B;動作來呈現頁面頂端的檢視主張。 如需詳細資訊，請參閱[頁面事件的頂端和底部（第二個頁面檢視 — 選項2）](/help/collection/use-cases/personalization/top-bottom-page-events.md)。 若要使用它，請在表單中輸入&#x200B;**[!UICONTROL View name]**。
3. **重新呈現建議**。 當您的網站使用React等架構重新呈現內容時，您可能需要重新套用個人化。 在這種情況下，您可以使用&#x200B;**[!UICONTROL Apply propositions]**&#x200B;動作型別來執行此操作。

此動作型別不會針對演算後的主張傳送顯示事件。 它會追蹤已轉譯的主張，以便將其納入後續&#x200B;**[!UICONTROL Send event]**&#x200B;呼叫中。

## 可用欄位

此動作型別支援下列欄位：

* **[!UICONTROL Instance]**：動作套用的SDK執行個體。 如果您的實作使用單一SDK例項，此下拉式功能表會停用。
* **[!UICONTROL Propositions]**：您要重新呈現的主張物件陣列。
* **[!UICONTROL View name]**：要呈現的檢視名稱。
* **[!UICONTROL Proposition metadata]**：決定如何套用HTML選件的物件。 您可以透過表單或資料元素提供此資訊。 它包含下列屬性：
   * **[!UICONTROL Scope]**
   * **[!UICONTROL Selector]**
   * **[!UICONTROL Action type]**
