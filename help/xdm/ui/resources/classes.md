---
keywords: Experience Platform；首頁；熱門主題；API;API;XDM;XDM系統；體驗資料模型；資料模型；ui；工作區；類別；類別；
solution: Experience Platform
title: 在UI中建立和編輯類
description: 了解如何在Experience Platform用戶介面中建立和編輯類。
topic-legacy: user guide
exl-id: 1b4c3996-2319-45dd-9edd-a5bcad46578b
source-git-commit: a854a40034666159fabca550227efe9f3a47fb53
workflow-type: tm+mt
source-wordcount: '901'
ht-degree: 0%

---

# 在UI中建立和編輯類

在Adobe Experience Platform中，結構的類別會定義結構將包含之資料的行為層面（記錄或時間序列）。 除此之外，類還描述了基於該類的所有結構都需要包含的最小公共屬性數，並為合併多個相容資料集提供了一種方法。

Adobe提供數種標準（「核心」）Experience Data Model(XDM)類別，包括 [!DNL XDM Individual Profile] 和 [!DNL XDM ExperienceEvent]. 除了這些核心類別之外，您還可以建立自己的自訂類別，以說明貴組織的更具體使用案例。

本檔案概述如何在Experience PlatformUI中建立、編輯和管理自訂類別。

## 先決條件

本指南需要妥善了解XDM系統。 請參閱 [XDM概觀](../../home.md) 了解XDM在Experience Platform生態系統中的角色，以及 [綱要構成基本知識](../../schema/composition.md) 了解類別對XDM結構的貢獻。

雖然本指南並非必要項目，但建議您也參照 [在UI中合成架構](../../tutorials/create-schema-ui.md) 熟悉 [!DNL Schema Editor].

## 建立新類 {#create}

在 **[!UICONTROL 結構]** 工作區，選取 **[!UICONTROL 建立結構]**，然後選取 **[!UICONTROL 瀏覽]** 中。

![](../../images/ui/resources/classes/browse-classes.png)

將顯示一個對話框，允許您從可用類清單中進行選擇。 在對話方塊頂端，選取 **[!UICONTROL 建立新類]**. 然後，您可以為新類指定顯示名稱（該類的簡短、描述性、唯一且用戶友好的名稱）、說明以及架構將定義的資料的行為(**[!UICONTROL 記錄]** 或 **[!UICONTROL 時間序列]**)。

完成後，請選取 **[!UICONTROL 分配類]**.

![](../../images/ui/resources/classes/class-details.png)

此 [!DNL Schema Editor] 畫布中，根據您剛建立的自訂類別顯示新結構。 由於尚未將任何欄位新增至類別，架構僅包含 `_id` 欄位，代表系統產生的唯一識別碼，會自動套用至 [!DNL Schema Registry].

![](../../images/ui/resources/classes/schema.png)

>[!IMPORTANT]
>
>建立實施貴組織定義的類的架構時，請記住，架構欄位組僅可與相容的類一起使用。 由於您定義的類別是新的，因此中沒有列出相容的欄位群組 **[!UICONTROL 新增欄位群組]** 對話框。 相反地，您需要 [建立新欄位組](./field-groups.md#create) 用於該類。 下次您構成實施新類的架構時，將列出您定義的欄位組，並且可供使用。

您現在可以開始 [向類添加欄位](#add-fields)，此資訊將由採用類別的所有結構共用。

## 編輯現有類 {#edit}

>[!NOTE]
>
>只有貴組織定義的自訂類別才能完全編輯和自訂。 對於由Adobe定義的核心類，在個別結構的上下文中只能編輯其欄位的顯示名稱。 請參閱 [編輯架構欄位的顯示名稱](./schemas.md#display-names) 以取得詳細資訊。
>
>儲存自訂類別並用於資料擷取後，之後只能對其進行加法變更。 請參閱 [模式演化規則](../../schema/composition.md#evolution) 以取得更多資訊。

要編輯現有類，請選擇 **[!UICONTROL 瀏覽]** 頁簽，然後選擇採用要編輯的類的架構的名稱。

![](../../images/ui/resources/classes/select-for-edit.png)

>[!TIP]
>
>您可以使用工作區的搜尋和篩選功能來協助您更輕鬆找到結構。 請參閱 [探索XDM資源](../explore.md) 以取得更多資訊。

此 [!DNL Schema Editor] 畫布中顯示結構。 您現在可以開始 [向類添加欄位](#add-fields).

![](../../images/ui/resources/classes/edit.png)

## 向類添加欄位 {#add-fields}

一旦您有採用自訂類別的結構開啟於 [!UICONTROL 結構編輯器]，您可以開始將欄位新增至類別。 若要新增欄位，請選取 **加號(+)** 表徵圖。

![](../../images/ui/resources/classes/add-field.png)

>[!IMPORTANT]
>
>請記住，您添加到類的任何欄位將用於採用該類的所有架構。 因此，您應謹慎考慮哪些欄位在所有架構使用案例中會很實用。 如果您想要新增欄位，而此欄位可能只會看到此類別下某些結構中的使用，建議您考慮將它新增至這些結構 [建立欄位群組](./field-groups.md#create) 。

A **[!UICONTROL 新欄位]** 會顯示在畫布中，而右側邊欄會更新，顯示設定欄位屬性的控制項。 在 **[!UICONTROL 指派給]**，選取 **[!UICONTROL 類別]**.

![](../../images/ui/resources/classes/assign-to-class.png)

請參閱 [定義UI中的欄位](../fields/overview.md#define) 以了解如何設定欄位並將欄位新增至類別的特定步驟。 繼續將所需的欄位新增至類別。 完成後，請選取 **[!UICONTROL 儲存]** 以儲存架構和類別。

![](../../images/ui/resources/classes/save.png)

如果您先前已建立採用此類別的結構，則新新增的欄位會自動顯示在這些結構中。

## 更改架構的類 {#schema}

您可以在初始建立過程中儲存架構之前的任意時間點更改架構的類。 請參閱 [建立和編輯結構](./schemas.md#change-class) 以取得更多資訊。

## 後續步驟

本檔案說明如何使用Platform UI建立和編輯類別。 如需功能的詳細資訊，請參閱 [!UICONTROL 結構] 工作區，請參閱 [[!UICONTROL 結構] 工作區概述](../overview.md).

了解如何使用 [!DNL Schema Registry] API，請參閱 [classes endpoint guide](../../api/classes.md).
