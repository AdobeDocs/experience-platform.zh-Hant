---
keywords: Experience Platform; home；熱門主題；api;API;XDM;XDM系統；體驗資料模型；資料模型；ui;workspace;field;
solution: Experience Platform
title: 在UI中定義XDM欄位
description: 瞭解如何在Experience Platform使用者介面中定義XDM欄位。
topic-legacy: user guide
exl-id: 2adb03d4-581b-420e-81f8-e251cf3d9fb9
translation-type: tm+mt
source-git-commit: d425dcd9caf8fccd0cb35e1bac73950a6042a0f8
workflow-type: tm+mt
source-wordcount: '1250'
ht-degree: 3%

---

# 在UI中定義XDM欄位

Adobe Experience Platform用戶介面中的[!DNL Schema Editor]允許您在自定義Experience Data Model(XDM)類和模式欄位組中定義自己的欄位。 本指南涵蓋在UI中定義XDM欄位的步驟，包括每個欄位類型的可用設定選項。

## 先決條件

本指南需要對XDM System有充分的瞭解。 有關XDM在Experience Platform生態系統中的角色介紹，請參閱[XDM概述](../../home.md)和[架構構成基礎](../../schema/composition.md)，以瞭解類和欄位組如何將欄位貢獻給XDM架構。

雖然本指南不是必要的，但建議您也要遵循在UI](../../tutorials/create-schema-ui.md)中構成架構的[教學課程，以熟悉[!DNL Schema Editor]的各種功能。

## 選擇資源以將欄位添加到{#select-resource}

要在UI中定義新的XDM欄位，必須首先在[!DNL Schema Editor]中開啟一個模式。 根據[!DNL Schema Library]中當前可用的方案，您可以選擇[建立新方案](../resources/schemas.md#create)或[選擇現有方案以編輯](../resources/schemas.md#edit)。

開啟[!DNL Schema Editor]後，使用左側導軌選擇要為其定義欄位的類或欄位組。 如果資源是由您的組織定義的自訂資源，則在畫布中會顯示新增或編輯欄位的控制項。 這些控制項會顯示在方案名稱旁邊，以及已在選定類或欄位組下定義的任何對象類型欄位。

![](../../images/ui/fields/overview/select-resource.png)

>[!NOTE]
>
>如果您選擇的類或欄位組是Adobe提供的核心資源，則無法編輯它，因此將不顯示上述控制項。 如果要向中添加欄位的方案基於核心XDM類，且不包含任何自定義欄位組，則可以[建立一個新欄位組](../resources/field-groups.md#create)以添加到方案。

要向資源添加新欄位，請在畫布中方案名稱旁選擇&#x200B;**加號(+)**&#x200B;表徵圖，或在要定義欄位的對象類型欄位旁選擇。

![](../../images/ui/fields/overview/plus-icon.png)

## 定義資源{#define}的欄位

在選取&#x200B;**plus(+)**&#x200B;圖示後，畫布中會出現&#x200B;**[!UICONTROL New field]**，位於與您唯一租用戶ID同名的根層級物件內（如下例中顯示為`_tenantId`）。 透過自訂類別和欄位群組新增至架構的所有欄位都會自動置於此命名空間中，以避免與Adobe提供類別和欄位群組中的其他欄位產生衝突。

![](../../images/ui/fields/overview/new-field.png)

在&#x200B;**[!UICONTROL Field properties]**&#x200B;下方的右邊欄中，您可以設定新欄位的詳細資料。 每個欄位都需要下列資訊：

| 欄位屬性 | 說明 |
| --- | --- |
| [!UICONTROL Field name] | 欄位的唯一描述性名稱。 請注意，儲存結構後，欄位的名稱便無法變更。<br><br>最理想的情況是，名稱應以camelCase寫入。它可能包含英數字元、破折號或底線字元，但&#x200B;**不能**&#x200B;以底線開頭。<ul><li>**正確**:  `fieldName`</li><li>**可接受：** `field_name2`、 `Field-Name`、  `field-name_3`</li><li>**錯誤**:  `_fieldName`</li></ul> |
| [!UICONTROL Display name] | 這個田地的人性化名稱。 |
| [!UICONTROL Type] | 欄位將包含的資料類型。 從此下拉菜單中，可以選擇XDM支援的[標準標量類型](../../schema/field-constraints.md)中的一種，或者選擇以前在[!DNL Schema Registry]中定義的多欄位[資料類型](../resources/data-types.md)中的一種。<br><br>您也可以選取以 **[!UICONTROL Advanced type search]** 搜尋和篩選現有的資料類型，並更輕鬆地找出所要的類型。 |

您也可以為欄位提供可選的人讀&#x200B;**[!UICONTROL Description]**，以提供欄位預定使用案例的更多內容。

>[!NOTE]
>
>視您為欄位選取的&#x200B;**[!UICONTROL Type]**&#x200B;而定，其他組態控制項可能會出現在右側導軌中。 有關這些控制項的詳細資訊，請參閱[類型特定欄位屬性](#type-specific-properties)一節。
>
>右邊欄還提供用於指定特殊欄位類型的複選框。 如需詳細資訊，請參閱[特殊欄位類型](#special)一節。

完成欄位配置後，請選擇&#x200B;**[!UICONTROL Apply]**。

![](../../images/ui/fields/overview/field-details.png)

畫布會更新以顯示欄位的名稱和類型，而右側欄現在除了列出欄位的其他屬性外，還會列出欄位的路徑。

![](../../images/ui/fields/overview/field-added.png)

您可以繼續遵循上述步驟，將更多欄位新增至架構。 保存結構後，如果對結構進行了任何更改，則也會保存其基本類和欄位組。

>[!NOTE]
>
>對某個方案的欄位組或類所做的任何更改都將反映在所有採用它們的其他方案中。

## 類型特定欄位屬性{#type-specific-properties}

定義新欄位時，可能會在右邊欄中顯示其他配置選項，具體取決於您為該欄位選擇的&#x200B;**[!UICONTROL Type]**。 下表概述了這些附加欄位屬性及其相容類型：

| 欄位屬性 | 相容類型 | 說明 |
| --- | --- | --- |
| [!UICONTROL Default value] | [!UICONTROL String], [!UICONTROL Double], [!UICONTROL Long], [!UICONTROL Integer], [!UICONTROL Short], [!UICONTROL Byte], [!UICONTROL Boolean] | 如果擷取期間未提供其他值，則會指派給此欄位的預設值。 此值必須符合欄位的選定類型。 |
| [!UICONTROL Pattern] | [!UICONTROL String] | [規則運算式](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Regular_Expressions)，此欄位的值必須符合，才能在擷取期間被接受。 |
| [!UICONTROL Format] | [!UICONTROL String] | 從預先定義的字串格式清單中選取值必須符合的格式。 可用格式包括： <ul><li>[[!UICONTROL date-time]](https://tools.ietf.org/html/rfc3339)</li><li>[[!UICONTROL email]](https://tools.ietf.org/html/rfc2822)</li><li>[[!UICONTROL hostname]](https://tools.ietf.org/html/rfc1123#page-13)</li><li>[[!UICONTROL ipv4]](https://tools.ietf.org/html/rfc791)</li><li>[[!UICONTROL ipv6]](https://tools.ietf.org/html/rfc2460)</li><li>[[!UICONTROL uri]](https://tools.ietf.org/html/rfc3986)</li><li>[[!UICONTROL uri-reference]](https://tools.ietf.org/html/rfc3986#section-4.1)</li><li>[[!UICONTROL url-template]](https://tools.ietf.org/html/rfc6570)</li><li>[[!UICONTROL json-pointer]](https://tools.ietf.org/html/rfc6901)</li></ul> |
| [!UICONTROL Minimum length] | [!UICONTROL String] | 字串必須包含的字元數目下限，才能在擷取期間接受值。 |
| [!UICONTROL Maximum length] | [!UICONTROL String] | 字串必須包含的字元數上限，才能在擷取期間接受值。 |
| [!UICONTROL Minimum value] | [!UICONTROL Double] | 擷取期間接受Double的最小值。 如果收錄的值與此處輸入的值完全相符，則會接受該值。 使用此約束時，&quot;[!UICONTROL Exclusive minimum value]&quot;約束必須留空。 |
| [!UICONTROL Maximum value] | [!UICONTROL Double] | 擷取期間接受Double的最大值。 如果收錄的值與此處輸入的值完全相符，則會接受該值。 使用此約束時，&quot;[!UICONTROL Exclusive maximum value]&quot;約束必須留空。 |
| [!UICONTROL Exclusive minimum value] | [!UICONTROL Double] | 擷取期間接受Double的最大值。 如果收錄的值與此處輸入的值完全相符，則會拒絕該值。 使用此約束時，&quot;[!UICONTROL Minimum value]&quot;（非獨佔）約束必須留空。 |
| [!UICONTROL Exclusive maximum value] | [!UICONTROL Double] | 擷取期間接受Double的最大值。 如果收錄的值與此處輸入的值完全相符，則會拒絕該值。 使用此約束時，&quot;[!UICONTROL Maximum value]&quot;（非獨佔）約束必須留空。 |

## 特殊欄位類型{#special}

右邊欄提供幾個複選框，用於為選定欄位指定特殊角色。 其中一些選項的使用案例涉及有關您的資料模型策略以及您打算如何使用下游平台服務的重要考量。

若要進一步瞭解這些特殊類型，請參閱下列檔案：

* [[!UICONTROL Required]](./required.md)
* [[!UICONTROL Array]](./array.md)
* [[!UICONTROL Enum]](./enum.md)
* [[!UICONTROL Identity]](./identity.md) （僅適用於字串欄位）
* [[!UICONTROL Relationship]](./relationship.md) （僅適用於字串欄位）

雖然技術上不是特殊欄位類型，但建議您造訪[定義物件類型欄位](./object.md)的指南，以進一步瞭解如果架構結構，定義巢狀子欄位。

## 後續步驟

本指南提供如何在UI中定義XDM欄位的概觀。 請記住，欄位只能透過使用類別和欄位群組新增至結構。 若要進一步瞭解如何在UI中管理這些資源，請參閱有關建立和編輯[類](../resources/classes.md)和[欄位組](../resources/field-groups.md)的指南。

有關[!UICONTROL Schemas]工作區功能的詳細資訊，請參閱[[!UICONTROL Schemas]工作區概述](../overview.md)。
