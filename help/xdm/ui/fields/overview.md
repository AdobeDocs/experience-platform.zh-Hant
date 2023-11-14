---
keywords: Experience Platform；首頁；熱門主題；API；API；XDM；XDM系統；體驗資料模型；資料模型；ui；工作區；欄位；
solution: Experience Platform
title: 在使用者介面中定義XDM欄位
description: 瞭解如何在Experience Platform使用者介面中定義XDM欄位。
exl-id: 2adb03d4-581b-420e-81f8-e251cf3d9fb9
source-git-commit: 765079f084dce316d321fbac5aee9e387373ba00
workflow-type: tm+mt
source-wordcount: '1505'
ht-degree: 4%

---

# 在UI中定義XDM欄位

此 [!DNL Schema Editor] 在Adobe Experience Platform使用者介面中，您可以在自訂體驗資料模型(XDM)類別和結構描述欄位群組中定義自己的欄位。 本指南涵蓋在UI中定義XDM欄位的步驟，包括每個欄位型別的可用設定選項。

## 先決條件

本指南需要實際瞭解XDM系統。 請參閱 [XDM概覽](../../home.md) 介紹XDM在Experience Platform生態系統內的角色，以及 [結構描述組合的基本面](../../schema/composition.md) 以瞭解類別和欄位群組如何為XDM結構描述貢獻欄位。

雖然本指南並非必要，但建議您也參閱相關的教學課程： [在UI中構成結構描述](../../tutorials/create-schema-ui.md) 熟悉 [!DNL Schema Editor].

## 選取要新增欄位的資源 {#select-resource}

若要在UI中定義新的XDM欄位，您必須先在 [!DNL Schema Editor]. 根據您目前在「 」中可用的結構描述 [!DNL Schema Library]，您可以選擇 [建立新結構描述](../resources/schemas.md#create) 或 [選取要編輯的現有結構描述](../resources/schemas.md#edit).

一旦您擁有 [!DNL Schema Editor] 開啟時，畫布中會顯示要新增欄位的控制項。 這些控制項會顯示在結構描述名稱旁，以及已定義在所選類別或欄位群組下的任何物件型別欄位旁。

![](../../images/ui/fields/overview/select-resource.png)

>[!WARNING]
>
>如果您嘗試將欄位新增至標準欄位群組提供的物件，該欄位群組將會轉換為自訂欄位群組，且原始欄位群組將不再可用。 請參閱以下小節： [新增欄位至標準欄位群組](../resources/schemas.md#custom-fields-for-standard-groups) 如需詳細資訊，請參閱結構描述UI指南。

若要新增欄位至資源，請選取 **加(+)** 圖示加以存取（位於畫布中的綱要名稱旁），或位於要定義其下之欄位的物件型別欄位旁。

![](../../images/ui/fields/overview/plus-icon.png)

視您是將欄位直接新增到結構描述或其組成類別和欄位群組而定，新增欄位的必要步驟將會有所不同。 本檔案的其餘部分著重於如何設定欄位的屬性，無論該欄位出現在結構描述中的何處。 如需有關欄位可以新增到結構描述的不同方式的詳細資訊，請參閱結構描述UI指南中的下列區段：

* [新增欄位至欄位群組](../resources/schemas.md#add-fields)
* [將欄位直接新增到結構描述](../resources/schemas.md#add-individual-fields)

## 定義欄位的屬性 {#define}

選取 **加(+)** 圖示，一個 **[!UICONTROL 未命名的欄位]** 預留位置會顯示在畫布中。

![](../../images/ui/fields/overview/new-field.png)

在右側邊欄中，在 **[!UICONTROL 欄位屬性]**，您可以設定新欄位的詳細資訊。 每個欄位都需要下列資訊：

| 欄位屬性 | 說明 |
| --- | --- |
| [!UICONTROL 欄位名稱] | 欄位的不重複、描述性名稱。 請注意，一旦結構描述已儲存，欄位名稱就無法變更。 此值用於識別和參考程式碼和其他下游應用程式中的欄位<br><br>理想情況下，名稱應該以駝峰式大小寫撰寫。 它可包含英數、破折號或底線字元，但它 **可能不會** 以底線開頭。<ul><li>**正確**： `fieldName`</li><li>**可接受：** `field_name2`， `Field-Name`， `field-name_3`</li><li>**不正確**： `_fieldName`</li></ul> |
| [!UICONTROL 顯示名稱] | 欄位的顯示名稱。 這是將用於表示結構描述編輯器畫布中欄位的名稱。 可使用將欄位名稱變更為顯示名稱 [顯示名稱切換](../resources/schemas.md#display-name-toggle). |
| [!UICONTROL 類型] | 欄位將包含的資料型別。 從此下拉式功能表中，您可以選取 [標準純量型別](../../schema/field-constraints.md) 受XDM支援，或其中一個多欄位 [資料型別](../resources/data-types.md) 之前已在下列欄位中定義的 [!DNL Schema Registry].<br><br>您也可以選取 **[!UICONTROL 進階型別搜尋]** 搜尋和篩選現有資料型別，更輕鬆地找到所需型別。 |

{style="table-layout:auto"}

您也可以提供人類看得懂的選項 **[!UICONTROL 說明]** 至欄位，以提供有關欄位擬定使用案例的更多內容。

>[!NOTE]
>
>依據 **[!UICONTROL 型別]** 您為欄位選取了，其他設定控制項可能會顯示在右側邊欄中。 請參閱以下小節： [型別特定欄位屬性](#type-specific-properties) 以取得這些控制項的詳細資訊。
>
>右邊欄也提供用於指定特殊欄位型別的核取方塊。 請參閱以下小節： [特殊欄位型別](#special) 以取得詳細資訊。

完成欄位設定後，選取「 」 **[!UICONTROL 套用]**.

![](../../images/ui/fields/overview/field-details.png)

畫布更新以顯示新增的欄位，該欄位位於為您唯一租使用者ID名稱空間的物件內(顯示為 `_tenantId` 在以下範例中)。 新增到結構描述的所有自訂欄位會自動放置在此名稱空間中，以防止與Adobe提供的類別和欄位群組中的其他欄位衝突。 現在，右側邊欄會列出欄位路徑以及其他屬性。

![](../../images/ui/fields/overview/field-added.png)

您可以繼續依照上述步驟，將更多欄位新增至結構描述。 一旦儲存結構描述後，如果對結構描述進行任何變更，也會儲存其基底類別和欄位群組。

>[!NOTE]
>
>您對一個結構描述的欄位群組或類別所做的任何變更，都會反映在採用它們的所有其他結構描述中。

## 特定型別的欄位屬性 {#type-specific-properties}

定義新欄位時，其他設定選項可能會顯示在右側邊欄中，具體取決於 **[!UICONTROL 型別]** 您為欄位選擇。 下表概述這些額外的欄位屬性及其相容型別：

| 欄位屬性 | 相容型別 | 說明 |
| --- | --- | --- |
| [!UICONTROL 預設值] | [!UICONTROL 字串]， [!UICONTROL 兩次]， [!UICONTROL 長]， [!UICONTROL 整數]， [!UICONTROL 短]， [!UICONTROL 位元組]， [!UICONTROL 布林值] | 如果擷取期間未提供其他值，則為指派給此欄位的預設值。 此值必須符合欄位選取的型別。<br><br>擷取時，預設值不會儲存在資料集中，因為這些值會隨著時間變更。 從資料集讀取資料時，下游平台服務和應用程式會推斷結構描述中設定的預設值。 例如，在使用「查詢服務」查詢資料時，如果屬性具有NULL值，但預設值設定為 `5` 在結構描述層級，查詢服務應該會傳回 `5` 而非NULL。 請注意，目前並非所有AEP服務都有這種行為。 |
| [!UICONTROL 模式] | [!UICONTROL 字串] | A [規則運算式](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Regular_Expressions) 此欄位的值必須符合以便在擷取期間接受。 |
| [!UICONTROL 格式] | [!UICONTROL 字串] | 從值必須符合的字串預先定義格式清單中選取。 可用的格式包括： <ul><li>[[!UICONTROL 日期時間]](https://tools.ietf.org/html/rfc3339)</li><li>[[!UICONTROL 電子郵件]](https://tools.ietf.org/html/rfc2822)</li><li>[[!UICONTROL 主機名稱]](https://tools.ietf.org/html/rfc1123#page-13)</li><li>[[!UICONTROL ipv4]](https://tools.ietf.org/html/rfc791)</li><li>[[!UICONTROL ipv6]](https://tools.ietf.org/html/rfc2460)</li><li>[[!UICONTROL uri]](https://tools.ietf.org/html/rfc3986)</li><li>[[!UICONTROL uri-reference]](https://tools.ietf.org/html/rfc3986#section-4.1)</li><li>[[!UICONTROL url-template]](https://tools.ietf.org/html/rfc6570)</li><li>[[!UICONTROL json指標]](https://tools.ietf.org/html/rfc6901)</li></ul> |
| [!UICONTROL 最小長度] | [!UICONTROL 字串] | 為了能在擷取期間接受的值，字串必須包含的最小字元數。 |
| [!UICONTROL 長度上限] | [!UICONTROL 字串] | 為了能在內嵌期間接受的值，字串必須包含的最大字元數。 |
| [!UICONTROL 最小值] | [!UICONTROL 雙倍] | 內嵌期間接受的Double的最小值。 如果內嵌的值與此處輸入的值完全相符，則會接受該值。 使用此限制時， 「[!UICONTROL 專屬最小值]「條件約束必須保留空白。 |
| [!UICONTROL 最大值] | [!UICONTROL 雙倍] | 內嵌期間接受的Double最大值。 如果內嵌的值與此處輸入的值完全相符，則會接受該值。 使用此限制時， 「[!UICONTROL 專屬最大值]「條件約束必須保留空白。 |
| [!UICONTROL 專屬最小值] | [!UICONTROL 雙倍] | 內嵌期間接受的Double最大值。 如果擷取的值與此處輸入的值完全相符，則會拒絕該值。 使用此限制時， 「[!UICONTROL 最小值]「 （非獨佔）限制必須保留空白。 |
| [!UICONTROL 專屬最大值] | [!UICONTROL 雙倍] | 內嵌期間接受的Double最大值。 如果擷取的值與此處輸入的值完全相符，則會拒絕該值。 使用此限制時， 「[!UICONTROL 最大值]「 （非獨佔）限制必須保留空白。 |

{style="table-layout:auto"}

## 特殊欄位型別 {#special}

右邊欄提供數個核取方塊，可指定所選欄位的特殊角色。 其中部分選項的使用案例涉及有關您的資料模型化策略以及您打算如何使用下游平台服務的重要考量。

若要深入瞭解這些特殊型別，請參閱下列檔案：

* [[!UICONTROL 必要]](./required.md)
* [[!UICONTROL 陣列]](./array.md)
* [[!UICONTROL 列舉]](./enum.md)
* [[!UICONTROL 身分]](./identity.md) （僅適用於字串欄位）
* [[!UICONTROL 關係]](./relationship.md) （僅適用於字串欄位）

雖然從技術上講不是特殊欄位型別，但也建議您造訪本指南 [定義物件型別欄位](./object.md) 以進一步瞭解如何在結構描述結構時定義巢狀子欄位。

## 後續步驟

本指南概述如何在UI中定義XDM欄位。 請記住，欄位只能透過使用類別和欄位群組新增到結構描述中。 若要進一步瞭解如何在UI中管理這些資源，請參閱建立和編輯指南 [類別](../resources/classes.md) 和 [欄位群組](../resources/field-groups.md).

如需功能的詳細資訊， [!UICONTROL 方案] 工作區，請參閱 [[!UICONTROL 方案] 工作區概觀](../overview.md).
