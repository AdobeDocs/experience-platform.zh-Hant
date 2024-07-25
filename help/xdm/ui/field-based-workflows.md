---
title: 結構描述編輯器中的欄位式工作流程
description: 瞭解如何將現有欄位群組中的欄位個別新增至您的Experience Data Model (XDM)結構描述。
exl-id: 0499ff30-a602-419b-b9d3-2defdd4354a7
source-git-commit: c2832821ea6f9f630e480c6412ca07af788efd66
workflow-type: tm+mt
source-wordcount: '1301'
ht-degree: 0%

---

# 結構描述編輯器中的欄位式工作流程

Adobe Experience Platform提供一組強大的標準化[欄位群組](../schema/composition.md#field-group)，以用於體驗資料模型(XDM)結構描述。 這些欄位群組背後的結構和語意經過精心設計，以符合各種細分使用案例和Platform中其他下游應用程式。 您也可以定義自己的自訂欄位群組，以滿足獨特的業務需求。

將欄位群組新增到結構描述時，該結構描述會繼承該群組包含的所有欄位。 不過，您現在可以將個別欄位新增到結構描述中，而無需包含關聯的欄位群組中，您可能不一定要使用的其他欄位。

本指南說明在Platform UI中新增個別欄位至結構描述的不同方法。

## 先決條件

本教學課程假設您熟悉XDM結構描述的[構成](../schema/composition.md)，以及如何在Platform UI中使用結構描述編輯器。 若要繼續，您應該開始進行[建立新結構描述](./resources/schemas.md)並將其指派給標準類別的程式，然後再繼續本指南。

## 移除從標準欄位群組新增的欄位 {#remove-field-group}

將標準欄位群組新增到結構描述後，您可以移除任何您不需要的標準欄位。

>[!NOTE]
>
>從標準欄位群組中移除欄位只會影響正在處理的結構描述，不會影響欄位群組本身。 如果您移除一個結構描述中的標準欄位，這些欄位仍然可在採用相同欄位群組的所有其他結構描述中使用。

在下列範例中，已將標準欄位群組&#x200B;**[!UICONTROL 人口統計詳細資料]**&#x200B;新增到結構描述。 若要移除單一欄位（例如`maritalStatus`），請選取畫布中的欄位，然後在右側邊欄中選取&#x200B;**[!UICONTROL 移除]**。

![包含欄位群組、[婚姻狀況]欄位和[移除]的結構描述編輯器，反白顯示。](../images/ui/field-based-workflows/remove-single-field.png)

如果您想要移除多個欄位，可以整體管理欄位群組。 在畫布中選取屬於群組的欄位，然後在右側邊欄中選取&#x200B;**[!UICONTROL 管理相關欄位]**。

![結構描述編輯器，包含反白顯示的欄位和「管理」相關欄位。](../images/ui/field-based-workflows/manage-related-fields.png)

會出現一個對話方塊，顯示相關欄位群組的結構。 在此，您可以使用提供的核取方塊來選取或取消選取所需的欄位。 在您滿意後，請選取&#x200B;**[!UICONTROL 確認]**。

![[管理相關欄位]對話方塊中反白顯示欄位群組圖表和[確認]。](../images/ui/field-based-workflows/select-fields.png)

畫布會重新出現，架構結構中只會顯示選取的欄位。

![結構描述編輯器，新編輯的欄位群組已反白顯示。](../images/ui/field-based-workflows/fields-added.png)

## 直接將標準欄位新增到結構描述

您可以將標準欄位群組中的欄位直接新增到結構描述，而無需預先知道其對應的欄位群組。 若要將標準欄位新增到結構描述，請在畫布中選取結構描述名稱旁的加號(**+**)圖示。 結構描述結構中出現&#x200B;**[!UICONTROL 未命名的欄位]**&#x200B;預留位置，且右側邊欄更新以顯示設定欄位的控制項。

![根欄位預留位置反白的結構描述編輯器。](../images/ui/field-based-workflows/root-custom-field.png)

在&#x200B;**[!UICONTROL 欄位名稱]**&#x200B;下，開始輸入您要新增的欄位名稱。 系統會自動搜尋符合查詢的標準欄位，並在&#x200B;**[!UICONTROL 建議的標準欄位]**&#x200B;下列出它們，包括它們所屬的欄位群組。

![反白顯示的欄位名稱，以及結構描述編輯器的欄位屬性中顯示的建議標準欄位清單。](../images/ui/field-based-workflows/standard-field-search.png)

雖然有些標準欄位會共用相同的名稱，但其結構可能會依其來源欄位群組而有所不同。 如果標準欄位巢狀內嵌在欄位群組結構的父物件中，則新增子欄位時，父欄位也會包含在結構描述中。

選取標準欄位旁的預覽圖示（![預覽圖示](/help/images/icons/preview.png)）以檢視其欄位群組的結構，並更瞭解其巢狀化方式。 若要將標準欄位新增至結構描述，請選取加號圖示（![加號圖示](/help/images/icons/add-circle.png)）。

![新增圖示在建議標準欄位的專案上反白顯示。](../images/ui/field-based-workflows/add-standard-field.png)

畫布更新以顯示新增到結構描述的標準欄位，包括它巢狀內嵌在欄位群組結構下的任何父欄位。 欄位群組的名稱也會列在左側邊欄的&#x200B;**[!UICONTROL 欄位群組]**&#x200B;下。 如果您想要從相同的欄位群組新增更多欄位，請在右側邊欄中選取&#x200B;**[!UICONTROL 管理相關欄位]**。

![結構描述編輯器，其欄位群組、標準欄位和管理相關欄位已反白顯示。](../images/ui/field-based-workflows/standard-field-added.png)

## 直接將自訂欄位新增到結構描述

與標準欄位的工作流程類似，您也可以將自己的自訂欄位直接新增到結構描述。

若要將欄位新增至結構描述的根層級，請在畫布中選取結構描述名稱旁的加號(**+**)圖示。 結構描述結構中出現&#x200B;**[!UICONTROL 未命名的欄位]**&#x200B;預留位置，且右側邊欄更新以顯示設定欄位的控制項。

![結構描述編輯器，包含新增圖示和醒目提示的無標題根層級欄位。](../images/ui/field-based-workflows/root-custom-field.png)

開始輸入您要新增的欄位名稱，系統就會自動開始搜尋相符的標準欄位。 若要建立新的自訂欄位，請選取附加&#x200B;**（[!UICONTROL 新欄位]）**&#x200B;的頂端選項。

![結構描述編輯器的欄位屬性中反白顯示的欄位名稱和新欄位建議。](../images/ui/field-based-workflows/custom-field-search.png)

從這裡，提供欄位的顯示名稱和資料型別。 在&#x200B;**[!UICONTROL 指派欄位群組]**&#x200B;下，您必須選取要與新欄位相關聯的欄位群組。 開始輸入欄位群組的名稱，如果您之前已[建立自訂欄位群組](./resources/field-groups.md#create)，它們將會顯示在下拉式清單中。 或者，您可以在欄位中輸入唯一名稱，以建立新的欄位群組。

![結構描述編輯器中反白顯示的顯示名稱、型別和指派給欄位屬性設定。](../images/ui/field-based-workflows/select-field-group.png)

>[!WARNING]
>
>如果您選取現有的自訂欄位群組，則採用該欄位群組的任何其他結構描述在您儲存變更後，也將繼承新新增的欄位。 因此，如果您想要此型別的傳輸，請僅選取現有的欄位群組。 否則，您應該選擇建立新的自訂欄位群組。

完成後，選取&#x200B;**[!UICONTROL 套用]**。

結構描述編輯器的欄位屬性中反白顯示![套用。](../images/ui/field-based-workflows/apply-field.png)

新欄位已新增到畫布中，並且已在您的[租使用者識別碼](../api/getting-started.md#know-your-tenant_id)下命名，以避免與標準XDM欄位衝突。 與新欄位相關聯的欄位群組也出現在左側邊欄的&#x200B;**[!UICONTROL 欄位群組]**&#x200B;下。

![結構描述編輯器，新欄位已新增到畫布中，並位於您的租使用者ID下。 欄位群組和欄位會反白顯示。](../images/ui/field-based-workflows/tenantId.png)

>[!NOTE]
>
>依預設，所選自訂欄位群組提供的其餘欄位會從結構描述中移除。 如果要將其中一些欄位新增到結構描述中，請選取屬於該群組的欄位，然後在右側邊欄中選取&#x200B;**[!UICONTROL 管理相關欄位]**。

### 將自訂欄位新增至標準欄位群組的結構

如果您使用的結構描述具有由標準欄位群組提供的物件型別欄位，您可以將自己的自訂欄位新增到該標準物件。 選取物件根目錄旁邊的加號(**+**)圖示。

>[!IMPORTANT]
>
>在一個結構描述中新增到欄位群組的任何欄位也會出現在採用相同欄位群組的所有其他結構描述中。

![結構描述編輯器，在標示的標準物件旁有加號圖示。](../images/ui/field-based-workflows/add-field-to-standard-object.png)

如需新增自訂欄位的詳細資訊，請參閱UI指南](./resources/schemas.md#custom-fields-for-standard-groups)中的[建立和編輯結構描述。

## 後續步驟

本指南涵蓋Platform UI中結構描述編輯器的全新欄位式工作流程。 如需在UI中管理結構描述的詳細資訊，請參閱[UI總覽](./overview.md)。
