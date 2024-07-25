---
keywords: Experience Platform；首頁；熱門主題；API；API；XDM；XDM系統；體驗資料模型；資料模型；ui；工作區；類別；類別；
solution: Experience Platform
title: 在UI中建立和編輯類別
description: 瞭解如何在Experience Platform使用者介面中建立和編輯類別。
exl-id: 1b4c3996-2319-45dd-9edd-a5bcad46578b
source-git-commit: c2832821ea6f9f630e480c6412ca07af788efd66
workflow-type: tm+mt
source-wordcount: '1458'
ht-degree: 5%

---

# 在 UI 中建立和編輯類別 {#ui-create-and-edit}

>[!CONTEXTUALHELP]
>id="platform_schemas_class_filter"
>title="標準或自訂類別篩選器"
>abstract="可用類別清單已根據其建立方式預先進行篩選。選取選項按鈕，在「標準」和「自訂」選項之間進行選擇。標準選項顯示由 Adobe 建立的實體，並包括 XDM 個人設定檔和 XDM 體驗事件類別。自訂選項顯示在您的組織內建立的實體。請參閱文件以了解更多有關建立和編輯類別的資訊。"

在Adobe Experience Platform中，結構描述的類別會定義結構描述將包含的資料的行為方面（記錄或時間序列）。 除此之外，類別會說明基於該類別的所有結構描述所需包含的最小通用屬性數量，並提供合併多個相容資料集的方法。

Adobe提供幾個標準（「核心」）Experience Data Model (XDM)類別，包括XDM Individual Profile和XDM ExperienceEvent。 除了這些核心類別之外，您也可以建立自己的自訂類別，以說明貴組織更具體的使用案例。

本檔案概述如何在Experience PlatformUI中建立、編輯及管理自訂類別。

## 先決條件 {#prerequisites}

本指南需要實際瞭解XDM系統。 請參閱[XDM總覽](../../home.md)，瞭解XDM在Experience Platform生態系統中的角色簡介，以及結構描述組合的[基本概念](../../schema/composition.md)，以瞭解類別對XDM結構描述的貢獻。

雖然本指南並非必要，但建議您也按照有關[在UI](../../tutorials/create-schema-ui.md)中構成結構描述的教學課程，熟悉結構描述編輯器的各種功能。

## 快速入門 {#getting-started}

在Platform UI中，選取左側導覽中的&#x200B;**[!UICONTROL 結構描述]**&#x200B;以開啟[!UICONTROL 結構描述]工作區，然後選取&#x200B;**[!UICONTROL 類別]**&#x200B;索引標籤。 會顯示可用類別的清單。

## 篩選類別 {#filter}

系統會根據類別的建立方式自動篩選類別清單。 預設設定會顯示由Adobe定義的類別。 您還可以篩選清單以顯示您的組織建立的清單。 選取選項按鈕以在[!UICONTROL 標準]與[!UICONTROL 自訂]選項之間選擇。 [!UICONTROL Standard]選項會顯示Adobe建立的實體，而[!UICONTROL Custom]選項則會顯示在您的組織內建立的實體。

![ [!UICONTROL 結構描述]工作區的[!UICONTROL 類別]索引標籤中反白顯示[!UICONTROL 標準]和[!UICONTROL 自訂]。](../../images/ui/resources/classes/standard-and-custom-classes.png)

>[!TIP]
>
>使用搜尋功能，根據類別名稱篩選或尋找類別。 如需詳細資訊，請參閱[探索XDM資源](../explore.md)的指南。

## 建立新類別 {#create}

在Platform UI中建立類別有兩個方法。 從[!UICONTROL 結構描述]工作區中的任何索引標籤中，選取&#x200B;**[!UICONTROL 建立結構描述]**，或從[!UICONTROL 類別]索引標籤中，選取&#x200B;**[!UICONTROL 建立類別]**。

![ [!UICONTROL 結構描述]工作區的[!UICONTROL 類別]索引標籤有[!UICONTROL 建立結構描述]和[!UICONTROL 建立類別]標示出來](../../images/ui/resources/classes/create-class-methods.png)

如果您選取&#x200B;**[!UICONTROL 建立類別]**，則會顯示[!UICONTROL 建立類別]對話方塊。 輸入類別的[!UICONTROL 顯示名稱]和[!UICONTROL 描述]，然後使用選項按鈕選擇您類別的預期行為。 類別可以是型別、記錄序列或時間序列。 選取&#x200B;**[!UICONTROL 建立]**&#x200B;以確認您的選擇，並返回[!UICONTROL 類別]標籤。

![反白顯示[!UICONTROL 建立]的[!UICONTROL 建立類別]對話方塊。](../../images/ui/resources/classes/create-class-dialog.png)

您建立的類別可以使用，並列在[!UICONTROL 類別]檢視中。

![最近建立之類別反白顯示之[!UICONTROL 結構描述]工作區的[!UICONTROL 類別]標籤。](../../images/ui/resources/classes/new-class-listing.png)

### 建立或編輯類別 {#create-or-edit}

或者，如果您選取&#x200B;**[!UICONTROL 建立結構描述]**，則會顯示[!UICONTROL 建立結構描述]工作流程。 在[!UICONTROL 結構描述詳細資料]區段中，選取&#x200B;**[!UICONTROL 其他]**。 可用的類別清單隨即顯示。 從這裡，您可以瀏覽並篩選作為新類別基礎的現有類別。

>[!NOTE]
>
>只有貴組織定義的自訂類別才能完全編輯和自訂。 對於由Adobe定義的核心類別，只能在個別結構描述的內容中編輯其欄位的顯示名稱。 如需詳細資訊，請參閱[編輯結構描述欄位](./schemas.md#display-names)的顯示名稱一節。
>
>儲存自訂類別並用於資料擷取後，之後只能對其執行附加變更。 如需詳細資訊，請參閱結構描述演化](../../schema/composition.md#evolution)的[規則。

![在[!UICONTROL 結構描述詳細資料]區段中反白顯示[!UICONTROL Other]的[!UICONTROL 建立結構描述]工作流程。](../../images/ui/resources/classes/other-schema-details.png)

選取選項按鈕，根據類別是自訂或標準類別來篩選類別。 您也可以根據產業來篩選可用的結果，或使用搜尋欄位來搜尋特定類別。

![使用搜尋列[!UICONTROL 自訂]和[!UICONTROL 產業]反白顯示[!UICONTROL 建立結構描述]工作流程。](../../images/ui/resources/classes/filter-and-search.png)

為了協助您決定適當的類別，有資訊(![資訊圖示。](/help/images/icons/info.png))和預覽(![預覽圖示。每個類別的](/help/images/icons/preview.png)個圖示。 資訊圖示會開啟對話方塊，提供類別及其關聯產業的說明。 預覽圖示會開啟包含結構描述圖表及其屬性的類別的預覽對話方塊。

![選取類別的預覽，其中結構描述圖表和類別屬性已反白顯示。](../../images/ui/resources/classes/class-preview.png)

選取任何列以選擇類別，然後選取&#x200B;**[!UICONTROL 下一步]**&#x200B;以確認您的選擇。

![從可用類別資料表中選取類別並反白顯示[!UICONTROL 下一步]的[!UICONTROL 建立結構描述]工作流程。](../../images/ui/resources/classes/select-class.png)

工作流程的[!UICONTROL 名稱與檢閱]區段隨即顯示。 在此區段中，提供名稱和說明來識別您的結構描述。&#x200B;URL結構描述的基本結構（由類別提供）會顯示在畫布中，供您檢閱及驗證選取的類別和結構描述結構。

在[!UICONTROL 結構描述顯示名稱]文字欄位中，為類別輸入簡短的、描述性的、唯一的和使用者易記的名稱。 接下來，輸入適當的說明以識別結構描述所定義的資料行為。 當您檢閱了結構描述結構並對您的設定感到滿意時，請選取&#x200B;**[!UICONTROL 完成]**&#x200B;以建立結構描述。

![使用[!UICONTROL 結構描述顯示名稱]、[!UICONTROL 描述]和[!UICONTROL 完成]反白顯示[!UICONTROL 建立結構描述]工作流程的[!UICONTROL 名稱和檢閱]區段。](../../images/ui/resources/classes/name-and-review-class.png)

隨即顯示「結構描述編輯器」，其結構描述結構顯示在畫布中。 您現在可以開始[新增欄位至類別](#add-fields)。

![畫布中顯示結構描述結構的結構描述編輯器。](../../images/ui/resources/classes/edit.png)

## 將欄位新增至類別 {#add-fields}

一旦您在[!UICONTROL 結構描述編輯器]中開啟了使用自訂類別的結構描述，您就可以開始將欄位新增至類別。 若要新增欄位，請選取結構描述名稱旁的&#x200B;**加號(+)**&#x200B;圖示。

>[!IMPORTANT]
>
>當建置實作由您的組織定義之類別的結構描述時，請記住，結構描述欄位群組只能與相容的類別搭配使用。 由於您定義的類別是新的，因此在&#x200B;**[!UICONTROL 新增欄位群組]**&#x200B;對話方塊中並未列出相容的欄位群組。 反之，您需要[建立新的欄位群組](./field-groups.md#create)以便與該類別搭配使用。 下次當您撰寫實作新類別的結構描述時，將會列出您定義的欄位群組並可供使用。

![結構描述編輯器，其新增按鈕已反白顯示。](../../images/ui/resources/classes/add-field.png)

>[!IMPORTANT]
>
>請記住，您新增到類別的任何欄位都將用於使用該類別的所有結構描述。 因此，您應該仔細考慮哪些欄位在所有結構描述使用案例中都將很有用。 如果您考慮新增一個欄位，而此欄位可能只會在此類別下的某些結構描述中使用，建議您改為建立[欄位群組](./field-groups.md#create)，將其新增至這些結構描述。

畫布中會出現&#x200B;**[!UICONTROL 未命名的欄位]**&#x200B;預留位置，而右邊欄會更新以顯示控制項，以設定欄位的屬性。 在&#x200B;**[!UICONTROL 指派給]**&#x200B;下，選取&#x200B;**[!UICONTROL 類別]**。

![結構描述編輯器的畫布中有未命名的欄位，且已選取並反白指派給類別欄位屬性。](../../images/ui/resources/classes/assign-to-class.png)

請參閱[在UI](../fields/overview.md#define)中定義欄位的指南，以瞭解如何設定欄位並將其新增到類別的特定步驟。 繼續將所需數量的欄位新增至類別。 完成後，選取&#x200B;**[!UICONTROL 儲存]**&#x200B;以儲存結構描述和類別。

![在結構描述編輯器的畫布上新建立的結構描述，並反白顯示[!UICONTROL 儲存]。](../../images/ui/resources/classes/save.png)

如果您先前已建立採用此類別的結構描述，則新新增的欄位會自動出現在這些結構描述中。

## 變更結構描述的類別 {#schema}

您可以在儲存架構之前，於初始建立程式期間隨時變更架構的類別。 但是，應謹慎執行此操作，因為欄位群組僅與特定類別相容。 變更類別會重設畫布和您已新增的任何欄位。
如需詳細資訊，請參閱[建立和編輯結構描述](./schemas.md#change-class)的指南。

## 後續步驟 {#next-steps}

本檔案說明如何使用Platform UI建立和編輯類別。 如需[!UICONTROL 結構描述]工作區功能的詳細資訊，請參閱[[!UICONTROL 結構描述]工作區概觀](../overview.md)。

若要瞭解如何使用Schema Registry API管理類別，請參閱[類別端點指南](../../api/classes.md)。
