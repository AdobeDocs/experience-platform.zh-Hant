---
keywords: Experience Platform；首頁；熱門主題；API；API；XDM；XDM系統；體驗資料模型；資料模型；ui；工作區；欄位；
solution: Experience Platform
title: 在使用者介面中定義XDM欄位
description: 瞭解如何在Experience Platform使用者介面中定義XDM欄位。
exl-id: 2adb03d4-581b-420e-81f8-e251cf3d9fb9
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1607'
ht-degree: 2%

---

# 在UI中定義XDM欄位

Adobe Experience Platform使用者介面中的[!DNL Schema Editor]可讓您在自訂體驗資料模型(XDM)類別和結構描述欄位群組中定義自己的欄位。 本指南涵蓋在UI中定義XDM欄位的步驟，包括每個欄位型別的可用設定選項。

## 先決條件

本指南需要實際瞭解XDM系統。 請參閱[XDM總覽](../../home.md)，瞭解XDM在Experience Platform生態系統中的角色簡介，以及結構描述組合的[基本概念](../../schema/composition.md)，瞭解類別和欄位群組如何對XDM結構描述貢獻欄位。

雖然本指南並非必要專案，但建議您也按照有關[在UI](../../tutorials/create-schema-ui.md)中構成結構描述的教學課程，熟悉[!DNL Schema Editor]的各種功能。

## 選取要新增欄位的資源 {#select-resource}

若要在UI中定義新的XDM欄位，您必須先在[!DNL Schema Editor]中開啟結構描述。 視您在[!DNL Schema Library]中目前可用的結構描述而定，您可以選擇[建立新的結構描述](../resources/schemas.md#create)或[選取要編輯的現有結構描述](../resources/schemas.md#edit)。

開啟[!DNL Schema Editor]後，畫布中就會顯示要新增欄位的控制項。 這些控制項會顯示在結構描述名稱旁，以及已定義在所選類別或欄位群組下的任何物件型別欄位旁。

![反白顯示新增圖示的結構描述編輯器。](../../images/ui/fields/overview/select-resource.png)

>[!WARNING]
>
>如果您嘗試將欄位新增至標準欄位群組提供的物件，該欄位群組將會轉換為自訂欄位群組，且原始欄位群組將不再可用。 如需詳細資訊，請參閱結構描述UI指南中有關[新增欄位至標準欄位群組](../resources/schemas.md#custom-fields-for-standard-groups)的章節。

若要新增欄位至資源，請在畫布中選取結構描述名稱旁的&#x200B;**加號(+)**&#x200B;圖示，或選取您想定義其下欄位的物件型別欄位旁的圖示。

![結構描述編輯器（反白顯示新增圖示）。](../../images/ui/fields/overview/plus-icon.png)

視您是將欄位直接新增到結構描述或其組成類別和欄位群組而定，新增欄位的必要步驟將會有所不同。 本檔案的其餘部分著重於如何設定欄位的屬性，無論該欄位出現在結構描述中的何處。 如需有關欄位可以新增到結構描述的不同方式的詳細資訊，請參閱結構描述UI指南中的下列區段：

* [新增欄位至欄位群組](../resources/schemas.md#add-fields)
* [將欄位直接新增到結構描述](../resources/schemas.md#add-individual-fields)

## 定義欄位的屬性 {#define}

選取&#x200B;**加號(+)**&#x200B;圖示後，**[!UICONTROL 未命名的欄位]**&#x200B;預留位置會顯示在畫布中。

![反白顯示新未命名欄位的結構描述編輯器。](../../images/ui/fields/overview/new-field.png)

在&#x200B;**[!UICONTROL 欄位屬性]**&#x200B;下的右側邊欄中，您可以設定新欄位的詳細資料。 每個欄位都需要下列資訊：

| 欄位屬性 | 說明 |
| --- | --- |
| [!UICONTROL 欄位名稱] | 欄位的不重複、描述性名稱。 請注意，一旦結構描述已儲存，欄位名稱就無法變更。 此值用於識別及參考程式碼和其他下游應用程式中的欄位<br><br>最好以camelCase撰寫此名稱。 它可包含英數字元或底線字元，但&#x200B;**不能**&#x200B;以底線開頭。<ul><li>**正確**： `fieldName`</li><li>**可接受：** `field_name2`，`fieldName_3`</li><li>**不正確**： `_fieldName`</li></ul> |
| [!UICONTROL 顯示名稱] | 欄位的顯示名稱。 這是將用於表示結構描述編輯器畫布中欄位的名稱。 可使用[顯示名稱切換](../resources/schemas.md#display-name-toggle)將欄位名稱變更為顯示名稱。 |
| [!UICONTROL 類型] | 欄位將包含的資料型別。 從這個下拉式功能表，您可以選取XDM支援的[標準純量型別](../../schema/field-constraints.md)之一，或是先前在[!DNL Schema Registry]中定義的多欄位[資料型別](../resources/data-types.md)之一。<br>注意：如果您選取「對應」資料型別，則會顯示[!UICONTROL 對應值型別]屬性。<br><br>您也可以選取&#x200B;**[!UICONTROL 進階型別搜尋]**，以搜尋及篩選現有的資料型別，更輕鬆地找到所要的型別。 |
| [!UICONTROL 對應值型別] | 如果您選取[!UICONTROL 對應]作為欄位的資料型別，則需要此值。 對應的可用值為[!UICONTROL 字串]和[!UICONTROL 整數]。 從可用選項的下拉式清單中選取一個值。<br>若要深入瞭解[特定型別的欄位屬性](#type-specific-properties)，請參閱定義欄位概觀。 |

{style="table-layout:auto"}

您也可以選擇為每個欄位提供說明和附註。 使用&#x200B;**[!UICONTROL Description]**&#x200B;欄位來新增內容並描述對應資料型別的功能。 這有助於實施的可維護性和可讀性。 您也可以新增附註以補充初始說明。 這可提供更細微且具體的資訊，以協助開發人員在程式碼基底的情境下，有效瞭解、維護及使用地圖。 |


>[!NOTE]
>
>根據您為欄位選取的&#x200B;**[!UICONTROL 型別]**，右側邊欄中可能會顯示其他組態控制項。 如需這些控制項的詳細資訊，請參閱[特定型別欄位屬性](#type-specific-properties)的區段。
>
>右邊欄也提供用於指定特殊欄位型別的核取方塊。 如需詳細資訊，請參閱[特殊欄位型別](#special)的相關章節。

完成欄位設定後，請選取&#x200B;**[!UICONTROL 套用]**。

![結構描述編輯器的[!UICONTROL 欄位屬性]區段已反白顯示。](../../images/ui/fields/overview/field-details.png)

畫布更新以顯示新新增的欄位，該欄位位於以您唯一租使用者ID命名的物件中（在以下範例中顯示為`_tenantId`）。 新增到結構描述的所有自訂欄位會自動放置在此名稱空間中，以防止與Adobe提供的類別和欄位群組中的其他欄位衝突。 現在，右側邊欄會列出欄位路徑以及其他屬性。

![結構描述圖表中的新欄位及其在[!UICONTROL 欄位屬性]區段中的對應路徑已反白顯示。](../../images/ui/fields/overview/field-added.png)

您可以繼續依照上述步驟，將更多欄位新增至結構描述。 一旦儲存結構描述後，如果對結構描述進行任何變更，也會儲存其基底類別和欄位群組。

>[!NOTE]
>
>您對一個結構描述的欄位群組或類別所做的任何變更，都會反映在採用它們的所有其他結構描述中。

## 特定型別的欄位屬性 {#type-specific-properties}

定義新欄位時，根據您為欄位選擇的&#x200B;**[!UICONTROL 型別]**，右側邊欄中可能會顯示其他組態選項。 下表概述這些額外的欄位屬性及其相容型別：

| 欄位屬性 | 相容型別 | 說明 |
| --- | --- | --- |
| [!UICONTROL 對應值型別] | [!UICONTROL 地圖] | 只有當您從[!UICONTROL 型別]下拉式選項中選取對應值時，[!UICONTROL 對應值型別]屬性才會出現在UI中。 您可以在String和Integer值型別之間選取Map。<br>![結構描述編輯器，特別標示出「類型」和「對應值類型」欄位。](../../images/ui/fields/overview/map-type.png "結構描述編輯器，特別標示出「類型」和「對應值類型」欄位。"){width="100" zoomable="yes"}<br>注意：任何透過API建立的對應資料型別，若不是String或Integer型別，則會顯示為&#39;[!UICONTROL Complex]&#39;資料型別。 您無法透過UI建立&#39;[!UICONTROL 複雜]&#39;資料型別。 |
| [!UICONTROL 模式] | [!UICONTROL 字串] | 此欄位值必須符合的[規則運算式](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Regular_Expressions)，才能在內嵌期間被接受。 |
| [!UICONTROL 格式] | [!UICONTROL 字串] | 從值必須符合的字串預先定義格式清單中選取。 可用的格式包括： <ul><li>[[!UICONTROL 日期時間]](https://tools.ietf.org/html/rfc3339)</li><li>[[!UICONTROL 電子郵件]](https://tools.ietf.org/html/rfc2822)</li><li>[[!UICONTROL 主機名稱]](https://tools.ietf.org/html/rfc1123#page-13)</li><li>[[!UICONTROL ipv4]](https://tools.ietf.org/html/rfc791)</li><li>[[!UICONTROL ipv6]](https://tools.ietf.org/html/rfc2460)</li><li>[[!UICONTROL uri]](https://tools.ietf.org/html/rfc3986)</li><li>[[!UICONTROL uri-reference]](https://tools.ietf.org/html/rfc3986#section-4.1)</li><li>[[!UICONTROL url範本]](https://tools.ietf.org/html/rfc6570)</li><li>[[!UICONTROL json-pointer]](https://tools.ietf.org/html/rfc6901)</li></ul> |
| [!UICONTROL 最小長度] | [!UICONTROL 字串] | 為了能在擷取期間接受的值，字串必須包含的最小字元數。 |
| [!UICONTROL 最大長度] | [!UICONTROL 字串] | 為了能在內嵌期間接受的值，字串必須包含的最大字元數。 |
| [!UICONTROL 最小值] | [!UICONTROL 雙倍] | 內嵌期間接受的Double的最小值。 如果內嵌的值與此處輸入的值完全相符，則會接受該值。 使用此限制時，「[!UICONTROL 專屬最小值]」限制必須留空。 |
| [!UICONTROL 最大值] | [!UICONTROL 雙倍] | 內嵌期間接受的Double最大值。 如果內嵌的值與此處輸入的值完全相符，則會接受該值。 使用此限制時，「[!UICONTROL 專屬最大值]」限制必須保留空白。 |
| [!UICONTROL 專屬最小值] | [!UICONTROL 雙倍] | 內嵌期間接受的Double最大值。 如果擷取的值與此處輸入的值完全相符，則會拒絕該值。 使用此限制時，「[!UICONTROL 最小值]」（非獨佔）限制必須保留空白。 |
| [!UICONTROL 專屬最大值] | [!UICONTROL 雙倍] | 內嵌期間接受的Double最大值。 如果擷取的值與此處輸入的值完全相符，則會拒絕該值。 使用此限制時，「[!UICONTROL 最大值]」（非獨佔）限制必須保留空白。 |

{style="table-layout:auto"}

## 特殊欄位型別 {#special}

右邊欄提供數個核取方塊，可指定所選欄位的特殊角色。 其中部分選項的使用案例涉及有關您的資料模型化策略以及您打算如何使用下游Experience Platform服務的重要考量。

若要深入瞭解這些特殊型別，請參閱下列檔案：

* [地圖](./map.md)
* [[!UICONTROL 必要]](./required.md)
* [[!UICONTROL 陣列]](./array.md)
* [[!UICONTROL 列舉]](./enum.md)
* [[!UICONTROL 身分]](./identity.md) （僅適用於字串欄位）
* [[!UICONTROL Relationship]](./relationship.md) （僅適用於字串欄位）

雖然從技術上講不是特殊欄位型別，但建議您造訪有關[定義物件型別欄位](./object.md)的指南，以進一步瞭解如何在結構描述結構時定義巢狀子欄位。

## 後續步驟

本指南概述如何在UI中定義XDM欄位。 請記住，欄位只能透過使用類別和欄位群組新增到結構描述中。 若要進一步瞭解如何在UI中管理這些資源，請參閱建立和編輯[類別](../resources/classes.md)和[欄位群組](../resources/field-groups.md)的指南。

如需[!UICONTROL 結構描述]工作區功能的詳細資訊，請參閱[[!UICONTROL 結構描述]工作區概觀](../overview.md)。
