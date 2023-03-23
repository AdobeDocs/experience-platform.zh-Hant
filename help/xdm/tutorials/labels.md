---
title: 管理結構的資料使用量標籤
description: 了解如何將資料使用量標籤新增至Adobe Experience Platform UI中的Experience Data Model(XDM)結構欄位。
exl-id: 92284bf7-f034-46cc-b905-bdfb9fcd608a
source-git-commit: 14e3eff3ea2469023823a35ee1112568f5b5f4f7
workflow-type: tm+mt
source-wordcount: '737'
ht-degree: 3%

---

# 管理結構的資料使用量標籤

>[!IMPORTANT]
>
>以結構為基礎的標籤是 [基於屬性的訪問控制](../../access-control/abac/overview.md)，此功能目前僅適用於美國醫療保健客戶的有限版本。 完整發行後，所有Adobe Real-time Customer Data Platform客戶都能使用此功能。

所有匯入Adobe Experience Platform的資料都受Experience Data Model(XDM)結構的限制。 此資料可能受貴組織或法律法規所定義的使用限制所限制。 為了解決此問題，Platform可讓您透過使用 [資料使用量標籤](../../data-governance/labels/overview.md).

套用至架構欄位的標籤會指出套用至該特定欄位所含資料的使用原則。

雖然標籤可套用至個別資料集（以及這些資料集內的欄位），您也可以在結構層級套用標籤。 將標籤直接套用至結構時，這些標籤會傳播至以該結構為基礎的所有現有和未來資料集。

此外，在一個方案中添加的任何欄位標籤都會傳播到使用共用類或欄位組中相同欄位的所有其他方案。 這有助於確保整個資料模型中類似欄位的使用規則一致。

本教學課程涵蓋使用Platform UI的結構編輯器將標籤新增至結構的步驟。

## 快速入門

本指南需要妥善了解下列Adobe Experience Platform元件：

* [[!DNL Experience Data Model (XDM) System]](../home.md):標準化框架 [!DNL Experience Platform] 組織客戶體驗資料。
   * [結構編輯器](../ui/overview.md):了解如何在Platform UI中建立和管理結構和其他資源。
* [[!DNL Adobe Experience Platform Data Governance]](../../data-governance/home.md):提供對Platform作業強制執行資料使用限制的基礎架構，使用可定義哪些行銷動作可以（或無法）對標示的資料執行的策略。

## 選擇要向添加標籤的架構或欄位 {#select-schema-field}

>[!CONTEXTUALHELP]
>id="platform_schemas_editgovernancelabels"
>title="編輯治理標籤"
>abstract="將標籤套用在方案欄位以顯示適用於該特定欄位中包含的資料的使用原則。"

若要開始新增標籤，您必須先 [選擇要編輯的現有架構](../ui/resources/schemas.md#edit) 或 [建立新架構](../ui/resources/schemas.md#create) 在架構編輯器中查看其結構。

若要編輯個別欄位的標籤，您可以選取畫布中的欄位，然後選取 **[!UICONTROL 管理存取]** 在右側邊欄。

![從架構編輯器畫布中選取欄位](../images/tutorials/labels/manage-access.png)

您也可以選取 **[!UICONTROL 標籤]** 頁簽，從清單中選擇所需欄位，然後選擇 **[!UICONTROL 編輯控管標籤]** 在右側邊欄。

![從 [!UICONTROL 標籤] 標籤](../images/tutorials/labels/select-field-on-labels-tab.png)

若要編輯整個架構的標籤，請選取鉛筆圖示(![](../images/tutorials/labels/pencil-icon.png))，位於 **[!UICONTROL 標籤]** 標籤。

![從 [!UICONTROL 標籤] 標籤](../images/tutorials/labels/select-schema-on-labels-tab.png)

>[!NOTE]
>
>當您首次嘗試編輯結構或欄位的標籤時，會出現免責聲明訊息，說明標籤使用方式如何根據您組織的原則影響下游作業。 選擇 **[!UICONTROL 繼續]** 繼續編輯。
>
>![標籤使用免責聲明](../images/tutorials/labels/disclaimer.png)

## 編輯架構或欄位的標籤

此時將顯示一個對話框，允許您編輯所選欄位的標籤。 如果您選取個別的物件類型欄位，右側邊欄會列出套用標籤將傳播到的子欄位。

![顯示的選定欄位](../images/tutorials/labels/edit-labels.png)

>[!NOTE]
>
>如果您正在編輯整個架構的欄位，右側邊欄不會列出適用的欄位，而會改為顯示架構名稱。

使用顯示的清單選擇要添加到架構或欄位的標籤。 選擇標籤時， **[!UICONTROL 已套用的標籤]** 區段更新，顯示目前已選取的標籤。

![顯示的已套用標籤](../images/tutorials/labels/applied-labels.png)

若要依類型篩選顯示的標籤，請在左側邊欄中選取所需的類別。 若要建立新的自訂標籤，請選取 **[!UICONTROL 建立標籤]**.

![篩選顯示的標籤或建立新標籤](../images/tutorials/labels/filter-and-create-custom.png)

對您選擇的標籤感到滿意後，請選取 **[!UICONTROL 儲存]** 將它們應用到欄位或架構。

![儲存所選標籤](../images/tutorials/labels/save-labels.png)

此 **[!UICONTROL 標籤]** 頁簽，顯示架構的已應用標籤。

![已套用欄位標籤](../images/tutorials/labels/field-labels-added.png)

## 後續步驟

本指南說明如何管理結構和欄位的資料使用標籤。 如需管理資料使用量標籤的相關資訊，包括如何將標籤新增至特定資料集，而非結構層級，請參閱 [資料使用標籤UI指南](../../data-governance/labels/user-guide.md).
