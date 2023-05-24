---
title: 架構編輯器中基於欄位的工作流（測試版）
description: 瞭解如何將現有欄位組中的欄位單獨添加到您的體驗資料模型(XDM)架構中。
hide: true
hidefromtoc: true
exl-id: 0499ff30-a602-419b-b9d3-2defdd4354a7
source-git-commit: 07faf4dd749219a955df720a8c740427113a5de2
workflow-type: tm+mt
source-wordcount: '1208'
ht-degree: 0%

---

# 架構編輯器中基於欄位的工作流（測試版）

>[!IMPORTANT]
>
>此測試版文檔中描述的工作流現在在Adobe Experience Platform普遍提供。 有關架構編輯器中基於欄位的工作流的最新指導，請參閱 [架構UI指南](./resources/schemas.md) 的雙曲餘切值。 此指南將很快刪除。

Adobe Experience Platform提供了一套健全的標準化 [欄位組](../schema/composition.md#field-group) 用於體驗資料模型(XDM)架構。 這些欄位組的結構和語義都經過精心的定製，以滿足平台中各種分割使用案例和其他下游應用。 您還可以定義自己的自定義欄位組，以滿足獨特的業務需要。

將欄位組添加到架構時，該架構將繼承該組中包含的所有欄位。 但是，您現在可以將單個欄位添加到您的架構中，而無需包括關聯欄位組中不一定使用的其他欄位。

本指南介紹了將各個欄位添加到平台UI中架構的不同方法。

## 先決條件

本教程假定您熟悉 [XDM模式的組合](../schema/composition.md) 以及如何在平台UI中使用架構編輯器。 要跟進，應啟動 [建立新架構](./resources/schemas.md) 在繼續使用本指南之前，將其分配給標準類。

## 刪除從標準欄位組添加的欄位 {#remove-field-group}

將標準欄位組添加到架構後，可以刪除不需要的任何標準欄位。

>[!NOTE]
>
>從標準欄位組中刪除欄位只影響正在處理的架構，而不影響欄位組本身。 如果刪除一個方案中的標準欄位，則這些欄位在使用相同欄位組的所有其他方案中仍然可用。

在以下示例中，標準欄位組 **[!UICONTROL 人口結構詳細資訊]** 已添加到架構。 刪除單個欄位，如 `taxId`，選擇畫布中的欄位，然後選擇 **[!UICONTROL 刪除]** 右欄。

![刪除單個欄位](../images/ui/field-based-workflows/remove-single-field.png)

如果要刪除多個欄位，則可以將欄位組作為一個整體進行管理。 選擇畫布中屬於組的欄位，然後選擇 **[!UICONTROL 管理相關欄位]** 右欄。

![管理相關欄位](../images/ui/field-based-workflows/manage-related-fields.png)

將出現一個對話框，顯示有關欄位組的結構。 在此處，您可以使用提供的複選框來選擇或取消選擇所需欄位。 滿足後，選擇 **[!UICONTROL 確認]**。

![從欄位組中選擇欄位](../images/ui/field-based-workflows/select-fields.png)

畫布將重新顯示，只顯示架構結構中的選定欄位。

![已添加欄位](../images/ui/field-based-workflows/fields-added.png)

## 將標準欄位直接添加到架構

您可以直接將標準欄位組中的欄位添加到架構中，而無需事先知道相應的欄位組。 要向架構添加標準欄位，請選擇加號(**+**)表徵圖。 安 **[!UICONTROL 無標題欄位]** 佔位符顯示在架構結構中，右滑軌更新顯示用於配置欄位的控制項。

![欄位佔位符](../images/ui/field-based-workflows/root-custom-field.png)

下 **[!UICONTROL 欄位名]**，開始鍵入要添加的欄位的名稱。 系統會自動搜索與查詢匹配的標準欄位，並將它們列在 **[!UICONTROL 建議的標準欄位]**，包括它們所屬的欄位組。

![建議的標準欄位](../images/ui/field-based-workflows/standard-field-search.png)

雖然某些標準欄位具有相同的名稱，但其結構可能會因其來源的欄位組而異。 如果標準欄位嵌套在欄位組結構中的父對象中，則如果添加子欄位，則父欄位也將包括在方案中。

選擇預覽表徵圖(![預覽表徵圖](../images/ui/field-based-workflows/preview-icon.png))旁邊，查看其欄位組的結構，並更好地瞭解該欄位可能嵌套的方式。 要將標準欄位添加到方案，請選擇加號表徵圖(![加號表徵圖](../images/ui/field-based-workflows/add-icon.png))。

![添加標準欄位](../images/ui/field-based-workflows/add-standard-field.png)

畫布將更新，以顯示添加到架構的標準欄位，包括它嵌套在欄位組結構中的任何父欄位。 欄位組的名稱也列在 **[!UICONTROL 欄位組]** 左欄。 如果要從同一欄位組中添加更多欄位，請選擇 **[!UICONTROL 管理相關欄位]** 右欄。

![已添加標準欄位](../images/ui/field-based-workflows/standard-field-added.png)

## 將自定義欄位直接添加到架構

與標準欄位的工作流類似，您也可以將您自己的自定義欄位直接添加到架構中。

要將欄位添加到架構的根級別，請選擇加號(**+**)表徵圖。 安 **[!UICONTROL 無標題欄位]** 佔位符顯示在架構結構中，右滑軌更新顯示用於配置欄位的控制項。

![根自定義欄位](../images/ui/field-based-workflows/root-custom-field.png)

開始鍵入要添加的欄位的名稱，系統將自動開始搜索匹配的標準欄位。 要改為建立新的自定義欄位，請選擇附加了 **([!UICONTROL 新建欄位])**。

![新建欄位](../images/ui/field-based-workflows/custom-field-search.png)

在此處，提供欄位的顯示名稱和資料類型。 下 **[!UICONTROL 分配欄位組]**，必須為要關聯的新欄位選擇一個欄位組。 開始鍵入欄位組的名稱，如果您以前 [建立自定義域組](./resources/field-groups.md#create) 它們將顯示在下拉清單中。 或者，可以在欄位中鍵入唯一名稱，以改為建立新欄位組。

![選擇欄位組](../images/ui/field-based-workflows/select-field-group.png)

>[!WARNING]
>
>如果選擇現有的自定義欄位組，則使用該欄位組的任何其它方案也將在保存更改後繼承新添加的欄位。 因此，僅當要選擇此類型的傳播時，才選擇現有欄位組。 否則，應選擇建立新的自定義欄位組。

完成後，選擇 **[!UICONTROL 應用]**。

![應用欄位](../images/ui/field-based-workflows/apply-field.png)

新欄位將添加到畫布中，並在您的 [租戶ID](../api/getting-started.md#know-your-tenant_id) 以避免與標準XDM欄位衝突。 與新欄位關聯的欄位組也顯示在 **[!UICONTROL 欄位組]** 左欄。

![租戶ID](../images/ui/field-based-workflows/tenantId.png)

>[!NOTE]
>
>預設情況下，所選自定義欄位組提供的其餘欄位將從架構中刪除。 如果要將其中的一些欄位添加到方案，請選擇屬於該組的欄位，然後選擇 **[!UICONTROL 管理相關欄位]** 右欄。

### 將自定義欄位添加到標準欄位組的結構

如果正在處理的方案具有由標準欄位組提供的對象類型欄位，則可以將您自己的自定義欄位添加到該標準對象。 選擇加號(**+**)表徵圖，並提供右欄中自定義欄位的詳細資訊。

![將欄位添加到標準對象](../images/ui/field-based-workflows/add-field-to-standard-object.png)

應用更改後，新欄位將顯示在標準對象中的租戶ID命名空間下。 此嵌套命名空間可防止欄位組本身內的欄位名稱衝突，以避免中斷使用相同欄位組的其他架構中的更改。

![添加到標準對象的欄位](../images/ui/field-based-workflows/added-to-standard-object.png)

## 後續步驟

本指南涵蓋了平台UI中架構編輯器的新的基於欄位的工作流。 有關在UI中管理架構的詳細資訊，請參見 [UI概述](./overview.md)。
