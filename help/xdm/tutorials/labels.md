---
title: 管理結構描述的資料使用標籤
description: 瞭解如何在Adobe Experience Platform UI中新增資料使用標籤到Experience Data Model (XDM)結構描述欄位。
exl-id: 92284bf7-f034-46cc-b905-bdfb9fcd608a
source-git-commit: ac6af3e90c417d1c97860394ce8afb07a0a7917d
workflow-type: tm+mt
source-wordcount: '766'
ht-degree: 8%

---

# 管理結構描述的資料使用標籤

所有帶入Adobe Experience Platform的資料都受到Experience Data Model (XDM)結構描述的限制。 此資料可能受貴組織或法律法規所定義的使用限制所約束。 為了說明這個問題，Platform可讓您透過使用[資料使用標籤](../../data-governance/labels/overview.md)來限制特定資料集和欄位的使用。

套用至結構描述欄位的標籤會指出套用至該特定欄位中所包含資料的使用原則。

標籤可套用至個別結構描述，以及這些結構描述內的欄位。 標籤直接套用至結構描述時，這些標籤會傳播至以該結構描述為基礎的所有現有和未來資料集。

此外，您新增至一個結構描述的任何欄位標籤，都會傳播至採用共用類別或欄位群組中相同欄位的所有其他結構描述。 這可協助確保類似欄位的使用規則在整個資料模型中保持一致。

本教學課程涵蓋在Platform UI中使用結構描述編輯器將標籤新增到結構描述的步驟。

## 快速入門

本指南需要您深入了解下列 Adobe Experience Platform 元件：

* [[!DNL Experience Data Model (XDM) System]](../home.md)： [!DNL Experience Platform]用來組織客戶體驗資料的標準化架構。
   * [結構描述編輯器](../ui/overview.md)：瞭解如何在Platform UI中建立和管理結構描述和其他資源。
* [[!DNL Adobe Experience Platform Data Governance]](../../data-governance/home.md)：提供基礎結構，以強制對Platform作業執行資料使用限制，使用定義哪些行銷動作可以（或無法）對標籤資料執行的原則。

## 選取要新增標籤的結構描述或欄位 {#select-schema-field}

>[!CONTEXTUALHELP]
>id="platform_schemas_editgovernancelabels"
>title="編輯控管標籤"
>abstract="將標籤套用在結構描述欄位以顯示適用於該特定欄位中包含的資料的使用原則。"

若要開始新增標籤，您必須先[選取要編輯的現有結構描述](../ui/resources/schemas.md#edit)，或[建立新的結構描述](../ui/resources/schemas.md#create)以在結構描述編輯器中檢視其結構。

若要編輯個別欄位的標籤，您可以在畫布中選取欄位，然後在右側邊欄中選取&#x200B;**[!UICONTROL 管理存取權]**。

>[!IMPORTANT]
>
>標籤上限為300個可套用至任何結構描述。

![從結構描述編輯器畫布選取欄位](../images/tutorials/labels/manage-access.png)

您也可以選取&#x200B;**[!UICONTROL 標籤]**&#x200B;標籤，從清單中選擇所需的欄位，然後在右側邊欄中選取&#x200B;**[!UICONTROL 套用存取權和資料治理標籤]**。

![從[!UICONTROL 標籤]索引標籤](../images/tutorials/labels/select-field-on-labels-tab.png)中選取欄位

若要編輯整個結構描述的標籤，請在&#x200B;**[!UICONTROL 標籤]**&#x200B;標籤中，選取篩選圖示下的核取方塊。 這會選取結構描述中的每個可用欄位。 接著，在右側邊欄中選取&#x200B;**[!UICONTROL 套用存取權和資料治理標籤]**。

![從[!UICONTROL 標籤]索引標籤](../images/tutorials/labels/select-schema-on-labels-tab.png)選取結構描述名稱

>[!NOTE]
>
>當您首次嘗試編輯結構描述或欄位的標籤時，會顯示免責宣告訊息，說明標籤使用方式如何根據您組織的原則影響下游作業。 選取&#x200B;**[!UICONTROL 繼續]**&#x200B;以繼續編輯。
>
>![標籤使用免責宣告](../images/tutorials/labels/disclaimer.png)

## 編輯結構描述或欄位的標籤 {#edit-labels}

會出現一個對話方塊，讓您編輯所選欄位的標籤。 如果您選取個別物件型別欄位，右側邊欄會列出套用標籤將傳播到的子欄位。

![套用存取權和資料控管標籤對話方塊中反白顯示的選取欄位。](../images/tutorials/labels/edit-labels.png)

>[!NOTE]
>
>如果您正在編輯整個結構描述的欄位，右側邊欄不會列出適用的欄位，而是顯示結構描述名稱。

使用顯示的清單來選取您要新增到結構描述或欄位的標籤。 選擇標籤後，**[!UICONTROL 套用的標籤]**&#x200B;區段會更新，以顯示目前為止已選取的標籤。

![套用存取權和資料控管標籤對話方塊中反白顯示套用的標籤。](../images/tutorials/labels/applied-labels.png)

若要依型別篩選顯示的標籤，請在左側邊欄中選取所需的類別。 若要建立新的自訂標籤，請選取&#x200B;**[!UICONTROL 建立標籤]**。

![套用存取權和資料控管標籤對話方塊，已套用標籤型別篩選器，並反白顯示建立標籤。](../images/tutorials/labels/filter-and-create-custom.png)

在您滿意所選取的標籤之後，請選取&#x200B;**[!UICONTROL 儲存]**&#x200B;以將其套用至欄位或結構描述。

![反白顯示[套用存取權和資料控管標籤]對話方塊的[儲存]。](../images/tutorials/labels/save-labels.png)

**[!UICONTROL 標籤]**&#x200B;標籤會重新出現，顯示結構描述套用的標籤。

![已套用欄位標籤醒目提示的結構描述工作區的[標籤]索引標籤。](../images/tutorials/labels/field-labels-added.png)

## 後續步驟

本指南說明如何管理結構描述和欄位的資料使用標籤。 如需有關管理資料使用標籤的資訊，包括如何將其新增到特定資料集而不是結構描述層級，請參閱[資料使用標籤UI指南](../../data-governance/labels/user-guide.md)。
