---
keywords: Experience Platform；首頁；熱門主題；API；API；XDM；XDM系統；體驗資料模型；資料模型；ui；工作區；類別；類別；
solution: Experience Platform
title: 在UI中建立和編輯類別
description: 瞭解如何在Experience Platform使用者介面中建立和編輯類別。
exl-id: 1b4c3996-2319-45dd-9edd-a5bcad46578b
source-git-commit: 4214339c4a661c6bca2cd571919ae205dcb47da1
workflow-type: tm+mt
source-wordcount: '1374'
ht-degree: 5%

---

# 在UI中建立和編輯類別 {#ui-create-and-edit}

>[!CONTEXTUALHELP]
>id="platform_schemas_class_filter"
>title="標準或自訂類別篩選器"
>abstract="可用類別清單已根據其建立方式預先進行篩選。選取選項按鈕，在「標準」和「自訂」選項之間進行選擇。標準選項顯示由 Adobe 建立的實體，並包括 XDM 個人設定檔和 XDM 體驗事件類別。自訂選項顯示在您的組織內建立的實體。請參閱文件以了解更多有關建立和編輯類別的資訊。"

在Adobe Experience Platform中，結構描述的類別會定義結構描述將包含的資料的行為方面（記錄或時間序列）。 除此之外，類別會說明基於該類別的所有結構描述所需包含的最小通用屬性數量，並提供合併多個相容資料集的方法。

Adobe提供幾個標準（「核心」）體驗資料模型(XDM)類別，包括 [!DNL XDM Individual Profile] 和 [!DNL XDM ExperienceEvent]. 除了這些核心類別之外，您也可以建立自己的自訂類別，以說明貴組織更具體的使用案例。

本檔案概述如何在Experience PlatformUI中建立、編輯及管理自訂類別。

## 先決條件

本指南需要實際瞭解XDM系統。 請參閱 [XDM概覽](../../home.md) 介紹XDM在Experience Platform生態系統內的角色，以及 [結構描述組合的基本面](../../schema/composition.md) 以瞭解類別對XDM結構描述的貢獻。

雖然本指南並非必要，但建議您也參閱相關的教學課程： [在UI中構成結構描述](../../tutorials/create-schema-ui.md) 熟悉 [!DNL Schema Editor].

## 快速入門

在Platform UI中選取 **[!UICONTROL 方案]** 在左側導覽以開啟 [!UICONTROL 方案] 工作區，然後選取 **[!UICONTROL 類別]** 標籤。 會顯示可用類別的清單。

## 篩選類別 {#filter}

系統會根據類別的建立方式自動篩選類別清單。 預設設定會顯示由Adobe定義的類別。 您還可以篩選清單以顯示您的組織建立的清單。 選取選項按鈕以選擇 [!UICONTROL 標準] 和 [!UICONTROL 自訂] 選項。 此 [!UICONTROL 標準] 選項會顯示由Adobe建立的實體，以及 [!UICONTROL 自訂] 選項會顯示在您組織內建立的實體。

![此 [!UICONTROL 類別] 的標籤 [!UICONTROL 方案] 工作區，使用 [!UICONTROL 標準] 和 [!UICONTROL 自訂] 反白顯示。](../../images/ui/resources/classes/standard-and-custom-classes.png)

>[!TIP]
>
>您可以使用工作區的搜尋功能來協助您更輕鬆地尋找結構。 請參閱以下指南： [探索XDM資源](../explore.md) 以取得詳細資訊。

## 建立新類別 {#create}

在Platform UI中建立類別有兩個方法。 從「 」中的任何標籤 **[!UICONTROL 方案]** 工作區，選取 **[!UICONTROL 建立結構描述]**，或從 [!UICONTROL 類別] 索引標籤選取 **[!UICONTROL 建立類別]**.

![此 [!UICONTROL 類別] 的標籤 [!UICONTROL 方案] 工作區，使用 [!UICONTROL 建立結構描述] 和 [!UICONTROL 建立類別] 反白顯示](../../images/ui/resources/classes/create-class-methods.png)

如果您選取 **[!UICONTROL 建立類別]**，則 [!UICONTROL 建立類別] 對話方塊隨即顯示。 輸入 [!UICONTROL 名稱] 和 [!UICONTROL 說明] ，並使用選項按鈕選擇您類別的預期行為。 類別可以是記錄序列或時間序列。 選取 **[!UICONTROL 建立]** 以確認您的選擇。

![此 [!UICONTROL 建立類別] 對話方塊 [!UICONTROL 建立] 反白顯示。](../../images/ui/resources/classes/create-class-dialog.png)

此 [!DNL Schema Editor] 就會顯示，在畫布中顯示以您剛建立的自訂類別為基礎的新結構描述。 由於類別尚未新增任何欄位，因此結構描述僅包含 `_id` 欄位，代表系統產生的唯一識別碼，會自動套用至 [!DNL Schema Registry].

![](../../images/ui/resources/classes/schema.png)

>[!IMPORTANT]
>
>當建置實作由您的組織定義之類別的結構描述時，請記住，結構描述欄位群組只能與相容的類別搭配使用。 由於您定義的類別是新的，因此清單中沒有相容的欄位群組。 **[!UICONTROL 新增欄位群組]** 對話方塊。 反之，您將需要 [建立新欄位群組](./field-groups.md#create) 以便與該類別搭配使用。 下次當您撰寫實作新類別的結構描述時，將會列出您定義的欄位群組並可供使用。

### 建立或編輯類別 {#create-or-edit}

如果您選取 **[!UICONTROL 建立結構描述]**，則 [!UICONTROL 建立結構描述] 工作流程隨即顯示。 在 [!UICONTROL 結構描述詳細資料] 區段，選取 **[!UICONTROL 其他]**. 可用的類別清單隨即顯示。 從這裡，您可以瀏覽並篩選作為新類別基礎的現有類別。

>[!NOTE]
>
>只有貴組織定義的自訂類別才能完全編輯和自訂。 對於由Adobe定義的核心類別，只能在個別結構描述的內容中編輯其欄位的顯示名稱。 請參閱以下小節： [編輯結構欄位的顯示名稱](./schemas.md#display-names) 以取得詳細資訊。
>
>儲存自訂類別並用於資料擷取後，之後只能對其執行附加變更。 請參閱 [結構描述演化的規則](../../schema/composition.md#evolution) 以取得詳細資訊。

![此 [!UICONTROL 建立結構描述] 工作流程與 [!UICONTROL 其他] 反白顯示 [!UICONTROL 結構描述詳細資料] 區段。](../../images/ui/resources/classes/other-schema-details.png)

選取選項按鈕，根據類別是自訂或標準類別來篩選類別。 您也可以根據產業來篩選可用的結果，或使用搜尋欄位來搜尋特定類別。

![此 [!UICONTROL 建立結構描述] 具有搜尋列的工作流程， [!UICONTROL 自訂]、和 [!UICONTROL 產業] 反白顯示。](../../images/ui/resources/classes/filter-and-search.png)

為協助您決定適當的類別，我們提供![資訊圖示。](../../images/ui/resources/classes/info.png))和預覽(![預覽圖示。](../../images/ui/resources/classes/preview.png))圖示來代表每個類別。 資訊圖示會開啟對話方塊，提供類別及其關聯產業的說明。 預覽圖示會開啟包含結構描述圖表及其屬性的類別的預覽對話方塊。

![所選類別的預覽，其中結構描述圖表和類別屬性會反白顯示。](../../images/ui/resources/classes/class-preview.png)

選取任何資料列以選擇類別，然後選取 **[!UICONTROL 下一個]** 以確認您的選擇。

![此 [!UICONTROL 建立結構描述] 從可用類別和表格中選取類別的工作流程 [!UICONTROL 下一個] 反白顯示。](../../images/ui/resources/classes/select-class.png)

此 [!UICONTROL 名稱和說明] 區段隨即顯示。 在此區段中，提供名稱和說明來識別您的結構描述。&#x200B;URL結構描述的基本結構（由類別提供）會顯示在畫布中，供您檢閱及驗證選取的類別和結構描述結構。

為中的類別輸入簡短的、描述性的、唯一的和使用者易記的名稱 [!UICONTROL 結構描述顯示名稱] 文字欄位。 接下來，輸入適當的說明以識別結構描述所定義的資料行為。 當您檢閱了結構描述結構並對設定感到滿意時，請選取「 」 **[!UICONTROL 完成]** 以建立架構。

![此 [!UICONTROL 名稱和評論] 的區段 [!UICONTROL 建立結構描述] 使用的工作流程 [!UICONTROL 結構描述顯示名稱]， [!UICONTROL 說明]、和 [!UICONTROL 完成] 反白顯示。](../../images/ui/resources/classes/name-and-review-class.png)

此 [!DNL Schema Editor] 會出現，而結構描述的結構會顯示在畫布中。 您現在可以開始 [將欄位新增至類別](#add-fields).

![](../../images/ui/resources/classes/edit.png)

## 將欄位新增至類別 {#add-fields}

一旦您的結構描述採用中開啟的自訂類別 [!UICONTROL 結構描述編輯器]，您就可以開始將欄位新增至類別。 若要新增欄位，請選取 **加(+)** 圖示加以識別。

![](../../images/ui/resources/classes/add-field.png)

>[!IMPORTANT]
>
>請記住，您新增到類別的任何欄位都將用於使用該類別的所有結構描述。 因此，您應該仔細考慮哪些欄位在所有結構描述使用案例中都將很有用。 如果您考慮新增一個欄位，而該欄位可能只會在此類別底下的某些結構描述中使用，您可能會想要考慮透過將其新增到這些結構描述中 [建立欄位群組](./field-groups.md#create) 而非。

一個 **[!UICONTROL 未命名的欄位]** 預留位置會顯示在畫布中，而右側邊欄會更新為顯示控制項，以設定欄位的屬性。 在 **[!UICONTROL 指派給]**，選取 **[!UICONTROL 類別]**.

![](../../images/ui/resources/classes/assign-to-class.png)

![](../../images/ui/resources/classes/assign-to-class.png)

請參閱以下指南： [在UI中定義欄位](../fields/overview.md#define) 有關如何設定欄位並將其新增到類別的特定步驟。 繼續將所需數量的欄位新增至類別。 完成後，選取 **[!UICONTROL 儲存]** 以儲存架構和類別。

![](../../images/ui/resources/classes/save.png)

如果您先前已建立採用此類別的結構描述，則新新增的欄位會自動出現在這些結構描述中。

## 變更結構描述的類別 {#schema}

您可以在儲存架構之前，於初始建立程式期間隨時變更架構的類別。 請參閱以下指南： [建立和編輯方案](./schemas.md#change-class) 以取得詳細資訊。

## 後續步驟

本檔案說明如何使用Platform UI建立和編輯類別。 如需功能的詳細資訊， [!UICONTROL 方案] 工作區，請參閱 [[!UICONTROL 方案] 工作區概觀](../overview.md).

若要瞭解如何使用 [!DNL Schema Registry] API，請參閱 [類別端點指南](../../api/classes.md).
