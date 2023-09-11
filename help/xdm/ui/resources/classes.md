---
keywords: Experience Platform；首頁；熱門主題；API；API；XDM；XDM系統；體驗資料模型；資料模型；ui；工作區；類別；類別；
solution: Experience Platform
title: 在UI中建立和編輯類別
description: 瞭解如何在Experience Platform使用者介面中建立和編輯類別。
exl-id: 1b4c3996-2319-45dd-9edd-a5bcad46578b
source-git-commit: 51ef116ad125b0d699bf4808e3d26d3b00b743e2
workflow-type: tm+mt
source-wordcount: '971'
ht-degree: 0%

---

# 在UI中建立和編輯類別 {#ui-create-and-edit}

>[!CONTEXTUALHELP]
>id="platform_schemas_class_filter"
>title="標準或自訂類別篩選器"
>abstract="系統會根據可用類別的建立方式，預先篩選這些類別。 選取選項按鈕以在「標準」和「自訂」選項之間選擇。 「標準」選項會顯示Adobe建立的實體，並包含XDM個人設定檔和XDM體驗事件類別。 自訂選項會顯示您的組織內建立的實體。 請參閱檔案以深入瞭解如何建立和編輯類別。"

在Adobe Experience Platform中，結構描述的類別會定義結構描述將包含的資料的行為方面（記錄或時間序列）。 除此之外，類別會說明基於該類別的所有結構描述所需包含的最小通用屬性數量，並提供合併多個相容資料集的方法。

Adobe提供幾個標準（「核心」）體驗資料模型(XDM)類別，包括 [!DNL XDM Individual Profile] 和 [!DNL XDM ExperienceEvent]. 除了這些核心類別之外，您也可以建立自己的自訂類別，以說明貴組織更具體的使用案例。

本檔案概述如何在Experience PlatformUI中建立、編輯及管理自訂類別。

## 先決條件

本指南需要實際瞭解XDM系統。 請參閱 [XDM概覽](../../home.md) 介紹XDM在Experience Platform生態系統內的角色，以及 [結構描述組合的基本面](../../schema/composition.md) 以瞭解類別對XDM結構描述的貢獻。

雖然本指南並非必要，但建議您也參閱相關的教學課程： [在UI中構成結構描述](../../tutorials/create-schema-ui.md) 熟悉 [!DNL Schema Editor].

## 建立新類別 {#create}

在 **[!UICONTROL 方案]** 工作區，選取 **[!UICONTROL 建立結構描述]**，然後選取 **[!UICONTROL 瀏覽]** 下拉式清單中的。

![](../../images/ui/resources/classes/browse-classes.png)

會出現一個對話方塊，讓您從可用類別清單中進行選取。 在對話方塊頂端，選取 **[!UICONTROL 建立新類別]**. 然後，您可以為新類別提供顯示名稱（類別的短名稱、描述性名稱、唯一名稱及好記名稱）、說明，以及結構描述將定義的資料行為(**[!UICONTROL 記錄]** 或 **[!UICONTROL 時間序列]**)。

完成後，選取 **[!UICONTROL 指派類別]**.

![](../../images/ui/resources/classes/class-details.png)

此 [!DNL Schema Editor] 就會顯示，在畫布中顯示以您剛建立的自訂類別為基礎的新結構描述。 由於類別尚未新增任何欄位，因此結構描述僅包含 `_id` 欄位，代表系統產生的唯一識別碼，會自動套用至 [!DNL Schema Registry].

![](../../images/ui/resources/classes/schema.png)

>[!IMPORTANT]
>
>當建置實作由您的組織定義之類別的結構描述時，請記住，結構描述欄位群組只能與相容的類別搭配使用。 由於您定義的類別是新的，因此清單中沒有相容的欄位群組。 **[!UICONTROL 新增欄位群組]** 對話方塊。 反之，您將需要 [建立新欄位群組](./field-groups.md#create) 以便與該類別搭配使用。 下次當您撰寫實作新類別的結構描述時，將會列出您定義的欄位群組並可供使用。

您現在可以開始 [將欄位新增至類別](#add-fields)，所有採用類別的結構描述都會共用。

## 編輯現有類別 {#edit}

>[!NOTE]
>
>只有貴組織定義的自訂類別才能完全編輯和自訂。 對於由Adobe定義的核心類別，只能在個別結構描述的內容中編輯其欄位的顯示名稱。 請參閱以下小節： [編輯結構欄位的顯示名稱](./schemas.md#display-names) 以取得詳細資訊。
>
>儲存自訂類別並用於資料擷取後，之後只能對其執行附加變更。 請參閱 [結構描述演化的規則](../../schema/composition.md#evolution) 以取得詳細資訊。

若要編輯現有類別，請選取 **[!UICONTROL 瀏覽]** 標籤，然後選取使用您要編輯之類別的結構描述名稱。

![](../../images/ui/resources/classes/select-for-edit.png)

>[!TIP]
>
>您可以使用工作區的搜尋和篩選功能來協助您更輕鬆地尋找結構。 請參閱以下指南： [探索XDM資源](../explore.md) 以取得詳細資訊。

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
