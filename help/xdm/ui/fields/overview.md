---
keywords: Experience Platform;home;popular topics;api;API;XDM;XDM system;experience data model;data model;ui;workspace;field;
solution: Experience Platform
title: 在UI中定義XDM欄位
description: 瞭解如何在Experience Platform使用者介面中定義XDM欄位。
topic: user guide
translation-type: tm+mt
source-git-commit: 2e20403122e65d28f04114af9b7e8d41874f76e2
workflow-type: tm+mt
source-wordcount: '1241'
ht-degree: 4%

---


# 在UI中定義XDM欄位

Adobe Experience Platform使用者介面中的[!DNL Schema Editor]可讓您在自訂的Experience Data Model(XDM)類別和混音中定義您自己的欄位。 本指南涵蓋在UI中定義XDM欄位的步驟，包括每個欄位類型的可用設定選項。

## 先決條件

本指南需要對XDM System有充分的瞭解。 請參閱[XDM概述](../../home.md)以瞭解XDM在Experience Platform生態系統中的角色，以及[架構構成基礎](../../schema/composition.md)，瞭解類別和混合如何將欄位貢獻至XDM架構。

雖然本指南不是必要的，但建議您也要遵循在UI](../../tutorials/create-schema-ui.md)中構成架構的[教學課程，以熟悉[!DNL Schema Editor]的各種功能。

## 選擇資源以將欄位添加到{#select-resource}

要在UI中定義新的XDM欄位，必須首先在[!DNL Schema Editor]中開啟一個模式。 根據[!DNL Schema Library]中當前可用的方案，您可以選擇[建立新方案](../resources/schemas.md#create)或[選擇現有方案以編輯](../resources/schemas.md#edit)。

開啟[!DNL Schema Editor]後，請使用左側導軌來選取您要定義欄位的類別或混音。 如果資源是由您的組織定義的自訂資源，則在畫布中會顯示新增或編輯欄位的控制項。 這些控制項會出現在方案名稱旁邊，以及已在所選類別或混合項下定義的任何物件類型欄位。

![](../../images/ui/fields/overview/select-resource.png)

>[!NOTE]
>
>如果您選取的類別或混音是Adobe提供的核心資源，則無法編輯它，因此不會顯示上述控制項。 如果要向中添加欄位的方案基於核心XDM類，並且不包含任何自定義混音，則可以[建立新混音](../resources/mixins.md#create)以改為添加到方案。

要向資源添加新欄位，請在畫布中方案名稱旁選擇&#x200B;**加號(+)**&#x200B;表徵圖，或在要定義欄位的對象類型欄位旁選擇。

![](../../images/ui/fields/overview/plus-icon.png)

## 定義資源{#define}的欄位

在選擇&#x200B;**plus(+)**&#x200B;圖示後，畫布中會顯示&#x200B;**[!UICONTROL 新欄位]**，位於與您唯一租用戶ID同名的根層級物件中（如下例中顯示為`_tenantId`）。 透過自訂類別和混音新增至架構的所有欄位都會自動置於此命名空間中，以避免與Adobe提供之類別和混音的其他欄位產生衝突。

![](../../images/ui/fields/overview/new-field.png)

在&#x200B;**[!UICONTROL 欄位屬性]**&#x200B;下方的右側欄位中，您可以設定新欄位的詳細資訊。 每個欄位都需要下列資訊：

| 欄位屬性 | 說明 |
| --- | --- |
| [!UICONTROL 欄位名稱] | 欄位的唯一描述性名稱。 請注意，儲存結構後，欄位的名稱便無法變更。<br><br>最理想的情況是，名稱應以camelCase寫入。它可能包含英數字元、破折號或底線字元，但&#x200B;**不能**&#x200B;以底線開頭。<ul><li>**正確**:  `fieldName`</li><li>**可接受：** `field_name2`、 `Field-Name`、  `field-name_3`</li><li>**錯誤**:  `_fieldName`</li></ul> |
| [!UICONTROL 顯示名稱] | 這個田地的人性化名稱。 |
| [!UICONTROL 類型] | 欄位將包含的資料類型。 從此下拉菜單中，可以選擇XDM支援的[標準標量類型](../../schema/field-constraints.md)中的一種，或者選擇以前在[!DNL Schema Registry]中定義的多欄位[資料類型](../resources/data-types.md)中的一種。<br><br>您也可以選取「進 **[!UICONTROL 階類型搜]** 尋」，以搜尋和篩選現有的資料類型，並更輕鬆地尋找所需類型。 |

您也可以為欄位提供可選的人讀&#x200B;**[!UICONTROL Description]**，以提供欄位預定使用案例的更多內容。

>[!NOTE]
>
>視您為欄位選取的&#x200B;**[!UICONTROL Type]**&#x200B;而定，其他組態控制項可能會出現在右側導軌中。 有關這些控制項的詳細資訊，請參閱[類型特定欄位屬性](#type-specific-properties)一節。
>
>右邊欄還提供用於指定特殊欄位類型的複選框。 如需詳細資訊，請參閱[特殊欄位類型](#special)一節。

完成欄位配置後，選擇&#x200B;**[!UICONTROL Apply]**。

![](../../images/ui/fields/overview/field-details.png)

畫布會更新以顯示欄位的名稱和類型，而右側欄現在除了列出欄位的其他屬性外，還會列出欄位的路徑。

![](../../images/ui/fields/overview/field-added.png)

您可以繼續遵循上述步驟，將更多欄位新增至架構。 儲存架構後，如果對其進行任何變更，也會儲存其基本類別和混合。

>[!NOTE]
>
>您對某個架構的mixin或類所做的任何更改都將反映在所有採用它們的其他架構中。

## 類型特定欄位屬性{#type-specific-properties}

定義新欄位時，根據您為欄位選擇的&#x200B;**[!UICONTROL Type]**，其他配置選項可能出現在右側邊欄中。 下表概述了這些附加欄位屬性及其相容類型：

| 欄位屬性 | 相容類型 | 說明 |
| --- | --- | --- |
| [!UICONTROL 預設值] | [!UICONTROL String] Double [!UICONTROL , Long], Short [!UICONTROL , ShortByte, Short], Boolean, ShortByte    [!UICONTROL , Boolean] | 如果擷取期間未提供其他值，則會指派給此欄位的預設值。 此值必須符合欄位的選定類型。 |
| [!UICONTROL 圖樣] | [!UICONTROL 字串] | [規則運算式](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Regular_Expressions)，此欄位的值必須符合，才能在擷取期間被接受。 |
| [!UICONTROL Format] | [!UICONTROL 字串] | 從預先定義的字串格式清單中選取值必須符合的格式。 可用格式包括： <ul><li>[[!UICONTROL 日期——時間]](https://tools.ietf.org/html/rfc3339)</li><li>[[!UICONTROL 電子郵件]](https://tools.ietf.org/html/rfc2822)</li><li>[[!UICONTROL 主機名]](https://tools.ietf.org/html/rfc1123#page-13)</li><li>[[!UICONTROL ipv4]](https://tools.ietf.org/html/rfc791)</li><li>[[!UICONTROL ipv6]](https://tools.ietf.org/html/rfc2460)</li><li>[[!UICONTROL uri]](https://tools.ietf.org/html/rfc3986)</li><li>[[!UICONTROL uri-reference]](https://tools.ietf.org/html/rfc3986#section-4.1)</li><li>[[!UICONTROL url-template]](https://tools.ietf.org/html/rfc6570)</li><li>[[!UICONTROL json-pointer]](https://tools.ietf.org/html/rfc6901)</li></ul> |
| [!UICONTROL 最小長度] | [!UICONTROL 字串] | 字串必須包含的字元數目下限，才能在擷取期間接受值。 |
| [!UICONTROL 長度上限] | [!UICONTROL 字串] | 字串必須包含的字元數上限，才能在擷取期間接受值。 |
| [!UICONTROL 最小值] | [!UICONTROL 雙倍] | 擷取期間接受Double的最小值。 如果收錄的值與此處輸入的值完全相符，則會接受該值。 |
| [!UICONTROL 最大值] | [!UICONTROL 雙倍] | 擷取期間接受Double的最大值。 如果收錄的值與此處輸入的值完全相符，則會接受該值。 |
| [!UICONTROL 獨佔最小值] | [!UICONTROL 雙倍] | 擷取期間接受Double的最大值。 如果收錄的值與此處輸入的值完全相符，則會拒絕該值。 |
| [!UICONTROL 獨佔最大值] | [!UICONTROL 雙倍] | 擷取期間接受Double的最大值。 如果收錄的值與此處輸入的值完全相符，則會拒絕該值。 |

## 特殊欄位類型{#special}

右邊欄提供幾個複選框，用於為選定欄位指定特殊角色。 其中一些選項的使用案例涉及有關您的資料模型策略以及您打算如何使用下游平台服務的重要考量。

若要進一步瞭解這些特殊類型，請參閱下列檔案：

* [[!UICONTROL 必填]](./required.md)
* [[!UICONTROL 陣列]](./array.md)
* [[!UICONTROL Enum]](./enum.md)
* [[!UICONTROL Identity]](./identity.md) （僅適用於字串欄位）
* [[!UICONTROL 關係]](./relationship.md) （僅適用於字串欄位）

雖然技術上不是特殊欄位類型，但建議您造訪[定義物件類型欄位](./object.md)的指南，以進一步瞭解如果架構結構，定義巢狀子欄位。

## 後續步驟

本指南提供如何在UI中定義XDM欄位的概觀。 請記住，欄位只能透過使用類別和混合來新增至結構。 若要進一步瞭解如何在UI中管理這些資源，請參閱有關建立和編輯[類別](../resources/classes.md)和[mixins](../resources/mixins.md)的指南。

有關[!UICONTROL 方案]工作區功能的詳細資訊，請參閱[[!UICONTROL 方案]工作區概述](../overview.md)。