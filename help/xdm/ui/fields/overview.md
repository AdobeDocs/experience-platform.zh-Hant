---
keywords: Experience Platform；首頁；熱門主題；API; API; XDM; XDM系統；體驗資料模型；資料模型；ui；工作區；欄位；
solution: Experience Platform
title: 在UI中定義XDM欄位
description: 了解如何在Experience Platform使用者介面中定義XDM欄位。
topic-legacy: user guide
exl-id: 2adb03d4-581b-420e-81f8-e251cf3d9fb9
source-git-commit: 39d04cf482e862569277211d465bb2060a49224a
workflow-type: tm+mt
source-wordcount: '1331'
ht-degree: 4%

---

# 在UI中定義XDM欄位

Adobe Experience Platform使用者介面中的[!DNL Schema Editor]可讓您在自訂Experience Data Model(XDM)類別和結構欄位群組中定義自己的欄位。 本指南涵蓋在UI中定義XDM欄位的步驟，包括每個欄位類型可用的設定選項。

## 先決條件

本指南需要妥善了解XDM系統。 請參閱[XDM概述](../../home.md) ，了解XDM在Experience Platform生態系統中的角色，以及架構組成[基本概念](../../schema/composition.md)，以了解類別和欄位群組如何將欄位貢獻至XDM結構。

雖然本指南並非必要，但建議您也參照在UI](../../tutorials/create-schema-ui.md)中撰寫架構的[教學課程，熟悉[!DNL Schema Editor]的各種功能。

## 選擇要向{#select-resource}添加欄位的資源

若要在UI中定義新的XDM欄位，您必須先在[!DNL Schema Editor]中開啟架構。 根據您目前在[!DNL Schema Library]中可用的架構，您可以選擇[建立新架構](../resources/schemas.md#create)或[選擇要編輯的現有架構](../resources/schemas.md#edit)。

開啟[!DNL Schema Editor]後，使用左側邊欄選取您要定義欄位的類別或欄位群組。 如果資源是貴組織定義的自訂資源，畫布中會顯示新增或編輯欄位的控制項。 這些控制項會出現在架構名稱旁邊，以及已在所選類或欄位組下定義的任何對象類型欄位。

![](../../images/ui/fields/overview/select-resource.png)

>[!NOTE]
>
>如果您選取的類別或欄位群組是Adobe提供的核心資源，則無法編輯，因此將不會顯示上述控制項。 如果您要新增欄位的架構是根據核心XDM類別，且不包含任何自訂欄位群組，您可以[建立新欄位群組](../resources/field-groups.md#create)以改為新增至架構。

若要向資源新增欄位，請選取畫布中架構名稱旁或您要定義欄位之下之物件類型欄位旁的&#x200B;**加號(+)**&#x200B;圖示。

![](../../images/ui/fields/overview/plus-icon.png)

## 定義資源的欄位 {#define}

選取&#x200B;**加號(+)**&#x200B;圖示後，畫布中會出現&#x200B;**[!UICONTROL 新欄位]**，位於與您的唯一租用戶ID命名的根層級物件內（在以下範例中顯示為`_tenantId`）。 通過自定義類和欄位組添加到架構的所有欄位都會自動放置在此命名空間中，以防止與Adobe提供的類和欄位組中的其他欄位發生衝突。

![](../../images/ui/fields/overview/new-field.png)

在右側欄的&#x200B;**[!UICONTROL 欄位屬性]**&#x200B;下，您可以設定新欄位的詳細資訊。 每個欄位都需要下列資訊：

| 欄位屬性 | 說明 |
| --- | --- |
| [!UICONTROL 欄位名稱] | 欄位的不重複、描述性名稱。 請注意，一旦儲存架構，就無法變更欄位的名稱。<br><br>名稱最好用camelCase寫。它可能包含英數字元、破折號或底線字元，但它&#x200B;**不能**&#x200B;以底線開頭。<ul><li>**正確**:  `fieldName`</li><li>**可接受：** `field_name2`、  `Field-Name`、  `field-name_3`</li><li>**錯誤**:  `_fieldName`</li></ul> |
| [!UICONTROL 顯示名稱] | 這個田地的人性化名稱。 |
| [!UICONTROL 類型] | 欄位將包含的資料類型。 在此下拉菜單中，您可以選擇XDM支援的[標準標量類型](../../schema/field-constraints.md)之一，或選擇先前已在[!DNL Schema Registry]中定義的多欄位[資料類型](../resources/data-types.md)之一。<br><br>您也可以選取進 **[!UICONTROL 階類]** 型search，以搜尋和篩選現有資料類型，並更輕鬆找到所需類型。 |

{style=&quot;table-layout:auto&quot;}

您也可以為欄位提供可選的人類看得懂的&#x200B;**[!UICONTROL Description]**，以提供有關欄位預期使用案例的更多內容。

>[!NOTE]
>
>視您為欄位選取的&#x200B;**[!UICONTROL 類型]**&#x200B;而定，右側邊欄中可能會顯示其他設定控制項。 有關這些控制項的詳細資訊，請參閱[類型特定欄位屬性](#type-specific-properties)上的部分。
>
>右側邊欄也提供用於指定特殊欄位類型的核取方塊。 如需詳細資訊，請參閱[特殊欄位類型](#special)的區段。

完成欄位配置後，請選擇&#x200B;**[!UICONTROL Apply]**。

![](../../images/ui/fields/overview/field-details.png)

畫布會更新以顯示欄位的名稱和類型，而右側邊欄現在除了列出其他屬性外，還會列出欄位的路徑。

![](../../images/ui/fields/overview/field-added.png)

您可以繼續依照上述步驟，將更多欄位新增至結構。 儲存架構後，如果對架構進行任何變更，也會儲存其基類和欄位群組。

>[!NOTE]
>
>您對某個架構的欄位群組或類別所做的任何變更，都會反映在採用這些變更的所有其他架構中。

## 類型特定欄位屬性{#type-specific-properties}

定義新欄位時，視您為欄位選擇的&#x200B;**[!UICONTROL Type]**&#x200B;而定，其他設定選項可能會顯示在右側欄中。 下表列出這些附加欄位屬性及其相容類型：

| 欄位屬性 | 相容類型 | 說明 |
| --- | --- | --- |
| [!UICONTROL 預設值] | [!UICONTROL 字串]、 [!UICONTROL 雙]、 [!UICONTROL 長]、 [!UICONTROL 整數]、 [!UICONTROL 短]、 [!UICONTROL 位元組]、 [!UICONTROL 布林值] | 如果擷取期間未提供其他值，則會指派給此欄位的預設值。 此值必須符合欄位的選取類型。 |
| [!UICONTROL 圖樣] | [!UICONTROL 字串] | [規則運算式](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Regular_Expressions)必須符合此欄位的值，才能在擷取期間接受。 |
| [!UICONTROL 格式] | [!UICONTROL 字串] | 從預先定義的字串格式清單中選取值必須符合的格式。 可用格式包括： <ul><li>[[!UICONTROL 日期時間]](https://tools.ietf.org/html/rfc3339)</li><li>[[!UICONTROL 電子郵件]](https://tools.ietf.org/html/rfc2822)</li><li>[[!UICONTROL 主機名]](https://tools.ietf.org/html/rfc1123#page-13)</li><li>[[!UICONTROL ipv4]](https://tools.ietf.org/html/rfc791)</li><li>[[!UICONTROL ipv6]](https://tools.ietf.org/html/rfc2460)</li><li>[[!UICONTROL uri]](https://tools.ietf.org/html/rfc3986)</li><li>[[!UICONTROL uri參考]](https://tools.ietf.org/html/rfc3986#section-4.1)</li><li>[[!UICONTROL url-template]](https://tools.ietf.org/html/rfc6570)</li><li>[[!UICONTROL json-pointer]](https://tools.ietf.org/html/rfc6901)</li></ul> |
| [!UICONTROL 最小長度] | [!UICONTROL 字串] | 字串必須包含的最小字元數，該值在擷取期間才可接受。 |
| [!UICONTROL 長度上限] | [!UICONTROL 字串] | 字串必須包含的字元數上限，該值在擷取期間才可接受。 |
| [!UICONTROL 最小值] | [!UICONTROL 雙倍] | 擷取期間，要接受Double的最小值。 如果擷取的值與此處輸入的值完全相符，則接受該值。 使用此約束時，「[!UICONTROL 排他最小值]」約束必須留空。 |
| [!UICONTROL 最大值] | [!UICONTROL 雙倍] | 擷取期間要接受Double的最大值。 如果擷取的值與此處輸入的值完全相符，則接受該值。 使用此約束時，「[!UICONTROL 獨佔最大值]」約束必須留空。 |
| [!UICONTROL 獨佔最小值] | [!UICONTROL 雙倍] | 擷取期間要接受Double的最大值。 如果擷取的值與此處輸入的值完全相符，則拒絕該值。 使用此約束時，「[!UICONTROL 最小值]」（非獨佔）約束必須留空。 |
| [!UICONTROL 獨佔最大值] | [!UICONTROL 雙倍] | 擷取期間要接受Double的最大值。 如果擷取的值與此處輸入的值完全相符，則拒絕該值。 使用此約束時，「[!UICONTROL 最大值]」（非獨佔）約束必須留空。 |

{style=&quot;table-layout:auto&quot;}

## 特殊欄位類型 {#special}

右側邊欄提供數個核取方塊，用以指定所選欄位的特殊角色。 其中某些選項的使用案例對於您的資料模型策略以及您要使用下游Platform服務的方式，會有重要考量。

若要進一步了解這些特殊類型，請參閱下列檔案：

* [[!UICONTROL 必填]](./required.md)
* [[!UICONTROL 陣列]](./array.md)
* [[!UICONTROL 列舉]](./enum.md)
* [[!UICONTROL 身分]](./identity.md) （僅適用於字串欄位）
* [[!UICONTROL 關係]](./relationship.md) （僅適用於字串欄位）

雖然從技術上來說不是特殊欄位類型，但建議您參閱[defining object-type fields](./object.md)上的指南，以進一步了解如果您的架構結構，如何定義巢狀子欄位。

## 後續步驟

本指南概略說明如何在UI中定義XDM欄位。 請記住，只能使用類和欄位組將欄位添加到架構中。 若要進一步了解如何在UI中管理這些資源，請參閱建立和編輯[classes](../resources/classes.md)和[欄位群組](../resources/field-groups.md)的指南。

如需[!UICONTROL 結構]工作區功能的詳細資訊，請參閱[[!UICONTROL 結構]工作區概述](../overview.md)。
