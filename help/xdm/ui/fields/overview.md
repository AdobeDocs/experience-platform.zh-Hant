---
keywords: Experience Platform；首頁；熱門主題；API; API; XDM; XDM系統；體驗資料模型；資料模型；ui；工作區；欄位；
solution: Experience Platform
title: 在UI中定義XDM欄位
description: 了解如何在Experience Platform使用者介面中定義XDM欄位。
exl-id: 2adb03d4-581b-420e-81f8-e251cf3d9fb9
source-git-commit: bed627b945c5392858bcc2dce18e9bbabe8bcdb6
workflow-type: tm+mt
source-wordcount: '1414'
ht-degree: 4%

---

# 在UI中定義XDM欄位

此 [!DNL Schema Editor] 在Adobe Experience Platform使用者介面中，您可在自訂Experience Data Model(XDM)類別和結構欄位群組中定義自己的欄位。 本指南涵蓋在UI中定義XDM欄位的步驟，包括每個欄位類型可用的設定選項。

## 先決條件

本指南需要妥善了解XDM系統。 請參閱 [XDM概觀](../../home.md) 了解XDM在Experience Platform生態系統中的角色，以及 [綱要構成基本知識](../../schema/composition.md) 若要了解類別和欄位群組如何將欄位貢獻至XDM結構。

雖然本指南並非必要項目，但建議您也參照 [在UI中合成架構](../../tutorials/create-schema-ui.md) 熟悉 [!DNL Schema Editor].

## 選取要新增欄位的資源 {#select-resource}

若要在UI中定義新的XDM欄位，您必須先在 [!DNL Schema Editor]. 視您目前在 [!DNL Schema Library]，您可以選擇 [建立新架構](../resources/schemas.md#create) 或 [選擇要編輯的現有架構](../resources/schemas.md#edit).

一旦您擁有 [!DNL Schema Editor] 開啟，則畫布中會顯示新增欄位的控制項。 這些控制項會出現在架構名稱旁邊，以及已在所選類或欄位組下定義的任何對象類型欄位。

![](../../images/ui/fields/overview/select-resource.png)

>[!WARNING]
>
>如果嘗試將欄位添加到標準欄位組提供的對象中，該欄位組將轉換為自定義欄位組，原始欄位組將不再可用。 請參閱 [將欄位添加到標準欄位組](../resources/schemas.md#custom-fields-for-standard-groups) 如需詳細資訊，請參閱綱要UI指南。

若要將新欄位新增至資源，請選取 **加號(+)** 表徵圖，在畫布中的架構名稱旁邊，或在要定義欄位的對象類型欄位旁邊。

![](../../images/ui/fields/overview/plus-icon.png)

根據您是直接將欄位新增至架構或其組成類別和欄位群組，新增欄位的必要步驟會有所不同。 本檔案的其餘部分著重於如何設定欄位的屬性，而無論該欄位出現在架構中的何處。 如需將欄位新增至結構的不同方式的詳細資訊，請參閱結構UI指南中的下列章節：

* [新增欄位至欄位群組](../resources/schemas.md#add-fields)
* [直接將欄位新增至結構](../resources/schemas.md#add-individual-fields)

## 定義欄位的屬性 {#define}

選取 **加號(+)** 表徵圖， **[!UICONTROL 無標題欄位]** 預留位置會顯示在畫布中。

![](../../images/ui/fields/overview/new-field.png)

在右側邊欄下方 **[!UICONTROL 欄位屬性]**，您可以設定新欄位的詳細資訊。 每個欄位都需要下列資訊：

| 欄位屬性 | 說明 |
| --- | --- |
| [!UICONTROL 欄位名稱] | 欄位的不重複、描述性名稱。 請注意，一旦儲存架構，就無法變更欄位的名稱。 此值可用來識別並參考程式碼和其他下游應用程式中的欄位<br><br>名稱最好用camelCase寫。 它可能包含英數字元、破折號或底線字元，但它 **不能** 從底線開始。<ul><li>**正確**: `fieldName`</li><li>**可接受：** `field_name2`, `Field-Name`, `field-name_3`</li><li>**錯誤**: `_fieldName`</li></ul> |
| [!UICONTROL 顯示名稱] | 欄位的顯示名稱。 這是將用來表示「架構編輯器」畫布中欄位的名稱。 欄位名稱可變更為顯示名稱，使用 [顯示名稱切換](../resources/schemas.md#display-name-toggle). |
| [!UICONTROL 類型] | 欄位將包含的資料類型。 從此下拉式功能表中，您可以選取 [標準標量類型](../../schema/field-constraints.md) 由XDM支援，或多欄位其中一個 [資料類型](../resources/data-types.md) 中 [!DNL Schema Registry].<br><br>您也可以選取 **[!UICONTROL 進階類型搜尋]** 若要搜尋及篩選現有資料類型，並更輕鬆找出所需類型。 |

{style="table-layout:auto"}

您也可以提供人類看得懂的選用 **[!UICONTROL 說明]** 至欄位，提供有關欄位預期使用案例的更多內容。

>[!NOTE]
>
>視 **[!UICONTROL 類型]** 您為欄位選取的其他設定控制項可能會顯示在右側欄中。 請參閱 [類型特定欄位屬性](#type-specific-properties) 以取得這些控制項的詳細資訊。
>
>右側邊欄也提供用於指定特殊欄位類型的核取方塊。 請參閱 [特殊欄位類型](#special) 以取得更多資訊。

完成欄位設定後，請選取 **[!UICONTROL 套用]**.

![](../../images/ui/fields/overview/field-details.png)

畫布會更新，以顯示新新增的欄位，位於與您的不重複租用戶ID命名的物件中（如所示） `_tenantId` 在以下範例中)。 新增至結構的所有自訂欄位都會自動放置在此命名空間中，以防止與Adobe提供的類別和欄位群組中的其他欄位產生衝突。 現在，除了欄位的其他屬性外，右側邊欄還會列出欄位的路徑。

![](../../images/ui/fields/overview/field-added.png)

您可以繼續依照上述步驟，將更多欄位新增至結構。 儲存架構後，如果對架構進行任何變更，也會儲存其基類和欄位群組。

>[!NOTE]
>
>您對某個架構的欄位群組或類別所做的任何變更，都會反映在採用這些變更的所有其他架構中。

## 類型特定欄位屬性 {#type-specific-properties}

定義新欄位時，視 **[!UICONTROL 類型]** 您為欄位選擇。 下表列出這些附加欄位屬性及其相容類型：

| 欄位屬性 | 相容類型 | 說明 |
| --- | --- | --- |
| [!UICONTROL 預設值] | [!UICONTROL 字串], [!UICONTROL 雙倍], [!UICONTROL 長], [!UICONTROL 整數], [!UICONTROL 簡短], [!UICONTROL 位元組], [!UICONTROL 布林值] | 如果擷取期間未提供其他值，則會指派給此欄位的預設值。 此值必須符合欄位的選取類型。 |
| [!UICONTROL 模式] | [!UICONTROL 字串] | A [規則運算式](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Regular_Expressions) 此欄位的值必須符合，才能在擷取期間接受。 |
| [!UICONTROL 格式] | [!UICONTROL 字串] | 從預先定義的字串格式清單中選取值必須符合的格式。 可用格式包括： <ul><li>[[!UICONTROL 日期時間]](https://tools.ietf.org/html/rfc3339)</li><li>[[!UICONTROL 電子郵件]](https://tools.ietf.org/html/rfc2822)</li><li>[[!UICONTROL 主機名]](https://tools.ietf.org/html/rfc1123#page-13)</li><li>[[!UICONTROL ipv4]](https://tools.ietf.org/html/rfc791)</li><li>[[!UICONTROL ipv6]](https://tools.ietf.org/html/rfc2460)</li><li>[[!UICONTROL uri]](https://tools.ietf.org/html/rfc3986)</li><li>[[!UICONTROL uri參考]](https://tools.ietf.org/html/rfc3986#section-4.1)</li><li>[[!UICONTROL url-template]](https://tools.ietf.org/html/rfc6570)</li><li>[[!UICONTROL json-pointer]](https://tools.ietf.org/html/rfc6901)</li></ul> |
| [!UICONTROL 最小長度] | [!UICONTROL 字串] | 字串必須包含的最小字元數，該值在擷取期間才可接受。 |
| [!UICONTROL 長度上限] | [!UICONTROL 字串] | 字串必須包含的字元數上限，該值在擷取期間才可接受。 |
| [!UICONTROL 最小值] | [!UICONTROL 雙倍] | 擷取期間，要接受Double的最小值。 如果擷取的值與此處輸入的值完全相符，則接受該值。 使用此限制時，[!UICONTROL 獨佔最小值]「約束必須留空。 |
| [!UICONTROL 最大值] | [!UICONTROL 雙倍] | 擷取期間要接受Double的最大值。 如果擷取的值與此處輸入的值完全相符，則接受該值。 使用此限制時，[!UICONTROL 獨佔最大值]「約束必須留空。 |
| [!UICONTROL 獨佔最小值] | [!UICONTROL 雙倍] | 擷取期間要接受Double的最大值。 如果擷取的值與此處輸入的值完全相符，則拒絕該值。 使用此限制時，[!UICONTROL 最小值]「（非獨佔）約束必須留空。 |
| [!UICONTROL 獨佔最大值] | [!UICONTROL 雙倍] | 擷取期間要接受Double的最大值。 如果擷取的值與此處輸入的值完全相符，則拒絕該值。 使用此限制時，[!UICONTROL 最大值]「（非獨佔）約束必須留空。 |

{style="table-layout:auto"}

## 特殊欄位類型 {#special}

右側邊欄提供數個核取方塊，用以指定所選欄位的特殊角色。 其中某些選項的使用案例對於您的資料模型策略以及您要使用下游Platform服務的方式，會有重要考量。

若要進一步了解這些特殊類型，請參閱下列檔案：

* [[!UICONTROL 必填]](./required.md)
* [[!UICONTROL 陣列]](./array.md)
* [[!UICONTROL 列舉]](./enum.md)
* [[!UICONTROL 身分]](./identity.md) （僅適用於字串欄位）
* [[!UICONTROL 關係]](./relationship.md) （僅適用於字串欄位）

雖然技術上不是特殊欄位類型，但也建議您參閱 [定義對象類型欄位](./object.md) 若要進一步了解如果您的結構，定義巢狀子欄位。

## 後續步驟

本指南概略說明如何在UI中定義XDM欄位。 請記住，只能使用類和欄位組將欄位添加到架構中。 若要進一步了解如何在UI中管理這些資源，請參閱建立和編輯指南 [類](../resources/classes.md) 和 [欄位群組](../resources/field-groups.md).

如需功能的詳細資訊，請參閱 [!UICONTROL 結構] 工作區，請參閱 [[!UICONTROL 結構] 工作區概述](../overview.md).
