---
keywords: Experience Platform；首頁；熱門主題；api;API;XDM;XDM系統；經驗資料模型；資料模型；ui;workspace;field;
solution: Experience Platform
title: 在UI中定義XDM欄位
description: 瞭解如何在Experience Platform用戶介面中定義XDM欄位。
exl-id: 2adb03d4-581b-420e-81f8-e251cf3d9fb9
source-git-commit: bed627b945c5392858bcc2dce18e9bbabe8bcdb6
workflow-type: tm+mt
source-wordcount: '1414'
ht-degree: 4%

---

# 在UI中定義XDM欄位

的 [!DNL Schema Editor] 在Adobe Experience Platform用戶介面中，可以在自定義體驗資料模型(XDM)類和架構欄位組中定義自己的欄位。 本指南介紹在UI中定義XDM欄位的步驟，包括每種欄位類型的可用配置選項。

## 先決條件

本指南要求對XDM系統有正確的瞭解。 請參閱 [XDM概述](../../home.md) 介紹XDM在Experience Platform生態系統中的作用， [架構組合基礎](../../schema/composition.md) 瞭解類和欄位組如何將欄位貢獻到XDM架構。

雖然本指南不是必需的，但建議您也學習上的教程 [在UI中合成架構](../../tutorials/create-schema-ui.md) 熟悉 [!DNL Schema Editor]。

## 選擇要將欄位添加到的資源 {#select-resource}

要在UI中定義新的XDM欄位，必須先在 [!DNL Schema Editor]。 根據您當前可以使用的架構 [!DNL Schema Library]，您可以選擇 [建立新架構](../resources/schemas.md#create) 或 [選擇要編輯的現有架構](../resources/schemas.md#edit)。

一旦你擁有 [!DNL Schema Editor] 開啟時，要添加的控制項將出現在畫布中。 這些控制項出現在方案名稱旁邊，以及在所選類或欄位組下定義的任何對象類型欄位。

![](../../images/ui/fields/overview/select-resource.png)

>[!WARNING]
>
>如果嘗試將欄位添加到由標準欄位組提供的對象，則該欄位組將轉換為自定義欄位組，並且原始欄位組將不再可用。 請參閱 [將欄位添加到標準欄位組](../resources/schemas.md#custom-fields-for-standard-groups) 中。

要向資源添加新欄位，請選擇 **加(+)** 表徵圖，位於畫布中方案名稱旁邊，或要在下定義欄位的對象類型欄位旁邊。

![](../../images/ui/fields/overview/plus-icon.png)

根據您是直接將欄位添加到方案還是其組成類和欄位組，添加該欄位所需的步驟會有所不同。 本文檔的其餘部分將重點介紹如何配置欄位的屬性，而不管該欄位在架構中的顯示位置如何。 有關欄位可以添加到架構的不同方式的詳細資訊，請參閱架構UI指南中的以下各節：

* [將欄位添加到欄位組](../resources/schemas.md#add-fields)
* [將欄位直接添加到架構](../resources/schemas.md#add-individual-fields)

## 定義欄位的屬性 {#define}

選擇 **加(+)** 表徵圖 **[!UICONTROL 無標題欄位]** 佔位符顯示在畫布中。

![](../../images/ui/fields/overview/new-field.png)

在右欄下 **[!UICONTROL 欄位屬性]**，可以配置新欄位的詳細資訊。 每個欄位都需要以下資訊：

| 欄位屬性 | 說明 |
| --- | --- |
| [!UICONTROL 欄位名稱] | 欄位的唯一描述性名稱。 請注意，一旦保存了架構，就無法更改欄位的名稱。 此值用於標識和引用代碼和其他下游應用程式中的欄位<br><br>最好用camelCase寫名。 它可能包含字母數字、短划線或下划線字元，但 **不能** 以下划線開頭。<ul><li>**正確**: `fieldName`</li><li>**可接受：** `field_name2`。 `Field-Name`。 `field-name_3`</li><li>**錯誤**: `_fieldName`</li></ul> |
| [!UICONTROL 顯示名稱] | 欄位的顯示名稱。 這是將用於表示架構編輯器畫布中欄位的名稱。 欄位名可以使用 [顯示名稱切換](../resources/schemas.md#display-name-toggle)。 |
| [!UICONTROL 類型] | 欄位將包含的資料類型。 從此下拉菜單中，可以選擇 [標準標量類型](../../schema/field-constraints.md) 由XDM或多欄位之一支援 [資料類型](../resources/data-types.md) 以前在 [!DNL Schema Registry]。<br><br>也可以選擇 **[!UICONTROL 高級類型搜索]** 搜索和篩選現有資料類型，並更輕鬆地查找所需類型。 |

{style="table-layout:auto"}

您還可以提供可選的人可讀 **[!UICONTROL 說明]** 到該欄位以提供有關該欄位的預期使用案例的更多上下文。

>[!NOTE]
>
>取決於 **[!UICONTROL 類型]** 為該欄位選擇的，其它配置控制項可能出現在右滑軌中。 請參閱 [類型特定的欄位屬性](#type-specific-properties) 的雙曲餘切值。
>
>右滑軌還提供用於指定特殊欄位類型的複選框。 請參閱 [特殊欄位類型](#special) 的子菜單。

配置完欄位後，選擇 **[!UICONTROL 應用]**。

![](../../images/ui/fields/overview/field-details.png)

畫布將更新以顯示新添加的欄位，該欄位位於與您的唯一租戶ID同名的對象中(顯示為 `_tenantId` )。 添加到架構的所有自定義欄位將自動放置在此命名空間中，以防止與Adobe提供的類和欄位組中的其他欄位發生衝突。 現在，右滑軌除了列出欄位的其他屬性外，還列出了欄位的路徑。

![](../../images/ui/fields/overview/field-added.png)

您可以繼續執行上述步驟，向架構添加更多欄位。 保存架構後，如果對其進行了任何更改，則還會保存其基類和欄位組。

>[!NOTE]
>
>對一個架構的欄位組或類所做的任何更改都將反映在使用它們的所有其它架構中。

## 類型特定的欄位屬性 {#type-specific-properties}

定義新欄位時，其他配置選項可能會根據 **[!UICONTROL 類型]** 選擇該欄位。 下表概述了這些附加欄位屬性及其相容類型：

| 欄位屬性 | 相容類型 | 說明 |
| --- | --- | --- |
| [!UICONTROL 預設值] | [!UICONTROL 字串]。 [!UICONTROL 雙]。 [!UICONTROL 龍]。 [!UICONTROL 整數]。 [!UICONTROL 短]。 [!UICONTROL 位元組]。 [!UICONTROL 布爾型] | 如果接收期間未提供其他值，則將分配給此欄位的預設值。 此值必須符合欄位的選定類型。 |
| [!UICONTROL 模式] | [!UICONTROL 字串] | A [規則運算式](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Regular_Expressions) 該欄位的值必須符合，才能在接收期間接受。 |
| [!UICONTROL 格式] | [!UICONTROL 字串] | 從預先定義的字串格式清單中選擇值必須符合的格式。 可用格式包括： <ul><li>[[!UICONTROL 日期時間]](https://tools.ietf.org/html/rfc3339)</li><li>[[!UICONTROL 電子郵件]](https://tools.ietf.org/html/rfc2822)</li><li>[[!UICONTROL 主機名]](https://tools.ietf.org/html/rfc1123#page-13)</li><li>[[!UICONTROL ipv4]](https://tools.ietf.org/html/rfc791)</li><li>[[!UICONTROL ipv6]](https://tools.ietf.org/html/rfc2460)</li><li>[[!UICONTROL uri]](https://tools.ietf.org/html/rfc3986)</li><li>[[!UICONTROL uri引用]](https://tools.ietf.org/html/rfc3986#section-4.1)</li><li>[[!UICONTROL url-template]](https://tools.ietf.org/html/rfc6570)</li><li>[[!UICONTROL json指針]](https://tools.ietf.org/html/rfc6901)</li></ul> |
| [!UICONTROL 最小長度] | [!UICONTROL 字串] | 要在接收期間接受該值，字串必須包含的最小字元數。 |
| [!UICONTROL 長度上限] | [!UICONTROL 字串] | 要在接收期間接受該值，字串必須包含的最大字元數。 |
| [!UICONTROL 最小值] | [!UICONTROL 雙倍] | 接收期間要接受的Double的最小值。 如果攝入的值與此處輸入的值完全匹配，則接受該值。 使用此約束時，「」[!UICONTROL 獨佔最小值]&quot;約束必須留空。 |
| [!UICONTROL 最大值] | [!UICONTROL 雙倍] | 接收期間要接受的Double的最大值。 如果攝入的值與此處輸入的值完全匹配，則接受該值。 使用此約束時，「」[!UICONTROL 獨佔最大值]&quot;約束必須留空。 |
| [!UICONTROL 獨佔最小值] | [!UICONTROL 雙倍] | 接收期間要接受的Double的最大值。 如果攝入的值與此處輸入的值完全匹配，則拒絕該值。 使用此約束時，「」[!UICONTROL 最小值]&quot;（非獨佔）約束必須留空。 |
| [!UICONTROL 獨佔最大值] | [!UICONTROL 雙倍] | 接收期間要接受的Double的最大值。 如果攝入的值與此處輸入的值完全匹配，則拒絕該值。 使用此約束時，「」[!UICONTROL 最大值]&quot;（非獨佔）約束必須留空。 |

{style="table-layout:auto"}

## 特殊欄位類型 {#special}

右滑軌提供多個複選框，用於為選定欄位指定特殊角色。 其中一些選項的使用案例涉及有關資料建模策略以及您打算如何使用下游平台服務的重要考慮事項。

要瞭解有關這些特殊類型的詳細資訊，請參閱以下文檔：

* [[!UICONTROL 必填]](./required.md)
* [[!UICONTROL 陣列]](./array.md)
* [[!UICONTROL 枚舉]](./enum.md)
* [[!UICONTROL 身份]](./identity.md) （僅適用於字串欄位）
* [[!UICONTROL 關係]](./relationship.md) （僅適用於字串欄位）

雖然技術上不是特殊的欄位類型，但建議您訪問指南 [定義對象類型欄位](./object.md) 以瞭解有關定義嵌套子欄位（如架構結構）的詳細資訊。

## 後續步驟

本指南概述了如何在UI中定義XDM欄位。 請記住，只能通過使用類和欄位組將欄位添加到架構中。 要瞭解有關如何在UI中管理這些資源的詳細資訊，請參閱有關建立和編輯的指南 [類](../resources/classes.md) 和 [欄位組](../resources/field-groups.md)。

有關功能的詳細資訊 [!UICONTROL 架構] 工作區，請參閱 [[!UICONTROL 架構] 工作區概述](../overview.md)。
