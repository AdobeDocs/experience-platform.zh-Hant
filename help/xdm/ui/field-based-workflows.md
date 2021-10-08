---
title: 結構編輯器（測試版）中的欄位型工作流程
description: 了解如何將現有欄位群組的欄位個別新增至Experience Data Model(XDM)結構。
hide: true
hidefromtoc: true
exl-id: 0499ff30-a602-419b-b9d3-2defdd4354a7
source-git-commit: 0bac76ce754468bd7e5396b6f68fbcfc3d6e4aed
workflow-type: tm+mt
source-wordcount: '1199'
ht-degree: 0%

---

# 結構編輯器（測試版）中的欄位型工作流程

>[!IMPORTANT]
>
>本檔案所述的工作流程目前為測試版，而您的組織可能尚未取得這些工作流程的存取權。 本檔案所述的功能可能會有所變更。

Adobe Experience Platform提供一組完善的標準化[欄位群組](../schema/composition.md#field-group)，以用於Experience Data Model(XDM)結構。 這些欄位群組背後的結構和語義都經過精心定制，以滿足Platform中各種不同的細分使用案例和其他下游應用程式。 您也可以定義自己的自訂欄位群組，以滿足獨特的業務需求。

將欄位組添加到架構時，該架構將繼承該組中包含的所有欄位。 不過，您現在可以將個別欄位新增至您的結構，而不需要從相關聯的欄位群組加入其他欄位，您不一定會使用這些欄位。

本指南涵蓋將個別欄位新增至Platform UI結構的不同方法。

## 先決條件

本教學課程假設您熟悉XDM結構](../schema/composition.md)的[組成，以及如何在Platform UI中使用結構編輯器。 接下來，您應開始[建立新架構](./resources/schemas.md)並將其指派給標準類的過程，然後再繼續閱讀本指南。

## 移除從標準欄位群組新增的欄位

將標準欄位群組新增至結構後，您就可以移除任何您不需要的標準欄位。

>[!NOTE]
>
>從標準欄位組中刪除欄位只會影響正在處理的架構，而不會影響欄位組本身。 如果刪除一個架構中的標準欄位，則這些欄位仍可用於採用相同欄位群組的所有其他架構中。

在以下範例中，標準欄位群組&#x200B;**[!UICONTROL 人口統計詳細資料]**&#x200B;已新增至架構。 若要移除單一欄位，例如`taxId`，請選取畫布中的欄位，然後在右側邊欄中選取&#x200B;**[!UICONTROL Remove]**。

![移除單一欄位](../images/ui/field-based-workflows/remove-single-field.png)

如果要移除多個欄位，您可以整體管理欄位群組。 在畫布中選取屬於群組的欄位，然後選取右側邊欄中的「管理相關欄位&#x200B;]**」 。**[!UICONTROL 

![管理相關欄位](../images/ui/field-based-workflows/manage-related-fields.png)

將出現一個對話框，顯示有關欄位組的結構。 從這裡，您可以使用提供的核取方塊來選取或取消選取您需要的欄位。 滿足後，選擇&#x200B;**[!UICONTROL 確認]**。

![從欄位組中選擇欄位](../images/ui/field-based-workflows/select-fields.png)

畫布會重新顯示，只有選取的欄位會顯示在架構結構中。

![新增欄位](../images/ui/field-based-workflows/fields-added.png)

## 直接將標準欄位新增至結構

您可以直接將標準欄位群組中的欄位新增至結構，而不需要預先知道其對應的欄位群組。 若要將標準欄位新增至架構，請在畫布中選取架構名稱旁的加號(**+**)圖示。 架構結構中會顯示&#x200B;**[!UICONTROL 未命名欄位]**&#x200B;預留位置，而右側邊欄會更新，顯示用以設定欄位的控制項。

![欄位預留位置](../images/ui/field-based-workflows/root-custom-field.png)

在&#x200B;**[!UICONTROL 欄位名稱]**&#x200B;下，開始鍵入要添加的欄位的名稱。 系統會自動搜尋符合查詢的標準欄位，並在&#x200B;**[!UICONTROL 建議標準欄位]**&#x200B;下列出，包括其所屬的欄位群組。

![建議的標準欄位](../images/ui/field-based-workflows/standard-field-search.png)

雖然某些標準欄位具有相同名稱，但其結構可能會因其來源欄位群組而異。 如果在欄位組結構中的父對象內嵌套了標準欄位，則如果添加了子欄位，則父欄位也將包含在架構中。

選取標準欄位旁的預覽圖示（![預覽圖示](../images/ui/field-based-workflows/preview-icon.png)），以檢視其欄位群組的結構，並更清楚了解其可能巢狀內嵌的方式。 若要將標準欄位新增至架構，請選取加號圖示（![加號圖示](../images/ui/field-based-workflows/add-icon.png)）。

![新增標準欄位](../images/ui/field-based-workflows/add-standard-field.png)

畫布會更新，顯示新增至架構的標準欄位，包括欄位群組結構內巢狀的任何父欄位。 欄位群組的名稱也會列在左側邊欄的&#x200B;**[!UICONTROL 欄位群組]**&#x200B;底下。 如果您想從相同欄位群組新增更多欄位，請選取右側欄位中的「管理相關欄位&#x200B;]**」 。**[!UICONTROL 

![新增標準欄位](../images/ui/field-based-workflows/standard-field-added.png)

## 直接將自訂欄位新增至結構

與標準欄位的工作流程類似，您也可以將自己的自訂欄位直接新增至結構。

若要將欄位新增至架構的根層級，請在畫布中選取架構名稱旁的加號(**+**)圖示。 架構結構中會顯示&#x200B;**[!UICONTROL 未命名欄位]**&#x200B;預留位置，而右側邊欄會更新，顯示用以設定欄位的控制項。

![根自訂欄位](../images/ui/field-based-workflows/root-custom-field.png)

開始在要添加的欄位名稱中鍵入，系統會自動開始搜索匹配的標準欄位。 若要改為建立新自訂欄位，請選取附加&#x200B;**（[!UICONTROL 新欄位]）**&#x200B;的上層選項。

![新欄位](../images/ui/field-based-workflows/custom-field-search.png)

從此處，提供欄位的顯示名稱和資料類型。 在&#x200B;**[!UICONTROL 分配欄位組]**&#x200B;下，必須為要關聯的新欄位選擇一個欄位組。 開始鍵入欄位組的名稱，如果先前已建立了自定義欄位組](./resources/field-groups.md#create)，則它們將出現在下拉清單中。 [或者，您也可以在欄位中輸入唯一名稱，以改為建立新欄位群組。

![選擇欄位組](../images/ui/field-based-workflows/select-field-group.png)

>[!WARNING]
>
>如果您選取現有的自訂欄位群組，則使用該欄位群組的任何其他結構也會在您儲存變更後繼承新新增的欄位。 因此，如果要此傳播類型，則僅選擇現有欄位組。 否則，您應該選擇建立新的自訂欄位群組。

完成後，選擇&#x200B;**[!UICONTROL Apply]**。

![應用欄位](../images/ui/field-based-workflows/apply-field.png)

新欄位會新增至畫布，並且會以您的[租用戶ID](../api/getting-started.md#know-your-tenant_id)命名，以避免與標準XDM欄位產生衝突。 您與新欄位相關聯的欄位群組也會顯示在左側欄的&#x200B;**[!UICONTROL 欄位群組]**&#x200B;下方。

![租用戶ID](../images/ui/field-based-workflows/tenantId.png)

>[!NOTE]
>
>依預設，所選自訂欄位群組提供的其餘欄位會從架構中移除。 如果要將其中一些欄位添加到架構中，請選擇屬於該組的欄位，然後在右側欄位中選擇&#x200B;**[!UICONTROL 管理相關欄位]**。

### 將自訂欄位新增至標準欄位群組的結構

如果您正在處理的結構具有標準欄位組提供的對象類型欄位，則您可以將自己的自定義欄位添加到該標準對象。 選取物件根目錄旁的加號(**+**)圖示，並在右側邊欄中提供自訂欄位的詳細資訊。

![將欄位新增至標準物件](../images/ui/field-based-workflows/add-field-to-standard-object.png)

套用變更後，新欄位會顯示在標準物件的租用戶ID命名空間底下。 此巢狀命名空間可防止欄位群組本身內的欄位名稱衝突，以避免在使用相同欄位群組的其他結構中中斷變更。

![新增至標準物件的欄位](../images/ui/field-based-workflows/added-to-standard-object.png)

## 後續步驟

本指南說明Platform UI中結構編輯器的新欄位式工作流程。 如需有關在UI中管理結構的詳細資訊，請參閱[UI概述](./overview.md)。
