---
keywords: Experience Platform；首頁；熱門主題；API；API；XDM；XDM系統；體驗資料模型；資料模型；ui；工作區；欄位群組；欄位群組；
solution: Experience Platform
title: 在UI中建立和編輯結構描述欄位群組
description: 瞭解如何在Experience Platform使用者介面中建立和編輯結構欄位群組。
exl-id: 928d70a6-0468-4fb7-a53a-6686ac77f2a3
source-git-commit: fded2f25f76e396cd49702431fa40e8e4521ebf8
workflow-type: tm+mt
source-wordcount: '1001'
ht-degree: 8%

---

# 在 UI 中建立和編輯結構描述欄位 {#ui-create-and-edit}

>[!CONTEXTUALHELP]
>id="platform_schemas_fieldgroup_filter"
>title="標準或自訂欄位群組篩選器"
>abstract="可用欄位群組清單已根據其建立方式預先進行篩選。選取選項按鈕，在「標準」和「自訂」選項之間進行選擇。標準選項顯示由 Adobe 建立的實體，而自訂選項顯示在您的組織內建立的實體。請參閱文件以了解更多有關建立和編輯欄位群組的資訊。"

在Experience Data Model (XDM)中，結構描述欄位群組是可重複使用的元件，可定義一或多個實作特定功能的欄位，例如個人詳細資料、飯店偏好設定或地址。 欄位群組是要包含在實作相容類別的結構描述中。

欄位群組會根據欄位群組代表的資料行為（記錄或時間序列），定義其相容的類別。 這表示並非所有欄位群組都可用於所有類別。

Adobe Experience Platform提供許多標準欄位群組，涵蓋廣泛的行銷使用案例。 不過，您也可以建立和編輯自己的自訂欄位群組，以在XDM結構描述中定義與您的業務相關的其他概念。 本指南概述如何在Experience Platform UI中建立、編輯及管理組織的自訂欄位群組。

## 先決條件 {#prerequisites}

本指南需要實際瞭解XDM系統。 請參閱[XDM總覽](../../home.md)，瞭解XDM在Experience Platform生態系統中的角色簡介，以及[結構描述組合基本概念](../../schema/composition.md)，瞭解欄位群組對XDM結構描述的貢獻。

雖然本指南並非必要專案，但建議您也按照有關[在UI](../../tutorials/create-schema-ui.md)中構成結構描述的教學課程，熟悉[!DNL Schema Editor]的各種功能。

## 建立新的欄位群組 {#create}

若要建立新的欄位群組，您必須先選取要新增該欄位群組的結構描述。 您可以選擇[建立新的結構描述](./schemas.md#create)或[選取要編輯的現有結構描述](./schemas.md#edit)。

在[!DNL Schema Editor]中開啟結構描述後，在左側邊欄的[!UICONTROL 欄位群組]區段旁選取&#x200B;**[!UICONTROL 新增]**。

![](../../images/ui/resources/field-groups/add-field-group.png)

在出現的對話方塊中，選取&#x200B;**[!UICONTROL 建立新欄位群組]**。 您可以在這裡提供欄位群組的&#x200B;**[!UICONTROL 顯示名稱]**&#x200B;和&#x200B;**[!UICONTROL 描述]**。 完成後，選取&#x200B;**[!UICONTROL 新增欄位群組]**。

![](../../images/ui/resources/field-groups/create-field-group.png)

[!DNL Schema Editor]會重新出現，新欄位群組會列在左側邊欄中。 由於這是全新的欄位群組，目前未提供任何欄位給結構描述，因此畫布保持不變。 您現在可以開始[新增欄位至欄位群組](#add-fields)。

![](../../images/ui/resources/field-groups/field-group-added.png)

## 篩選欄位群組 {#filter}

可用欄位群組清單已根據其建立方式預先進行篩選。預設設定會顯示Adobe定義的欄位群組。 不過，您也可以篩選清單以顯示貴組織建立的清單。 選取選項按鈕以在[!UICONTROL 標準]與[!UICONTROL 自訂]選項之間選擇。 [!UICONTROL 標準]選項會顯示Adobe建立的實體，而[!UICONTROL 自訂]選項則會顯示貴組織內建立的實體。

![ [!UICONTROL 結構描述]工作區的[!UICONTROL 欄位群組]索引標籤中反白顯示[!UICONTROL 標準]和[!UICONTROL 自訂]。](../../images/ui/resources/field-groups/standard-and-custom-field-groups.png)

## 編輯現有欄位群組 {#edit}

>[!NOTE]
>
>只有貴組織定義的自訂欄位群組才能完全編輯和自訂。 對於Adobe定義的核心欄位群組，只能在個別結構描述的內容中編輯其欄位的顯示名稱。 它們在「結構描述編輯器」中以掛鎖圖示(![掛鎖圖示表示。](/help/images/icons/lock-closed.png))。 如需詳細資訊，請參閱[編輯結構描述欄位](./schemas.md#display-names)的顯示名稱一節。
>
>儲存自訂欄位群組並在結構描述中使用以進行資料擷取後，之後只能對欄位群組進行附加變更。 如需詳細資訊，請參閱結構描述演化[&#128279;](../../schema/composition.md#evolution)的規則。

若要編輯現有的欄位群組，您必須先開啟採用[!DNL Schema Editor]內欄位群組的結構描述。 您可以[選取要編輯的現有結構描述](./schemas.md#edit)，或者您可以[建立新的結構描述](./schemas.md#create)並新增相關欄位群組。

在編輯器中開啟結構描述後，您就可以開始[新增欄位至欄位群組](#add-fields)。

## 新增欄位至欄位群組 {#add-fields}

>[!NOTE]
>
>本節重點介紹如何新增欄位至自訂欄位群組。 有關如何將自訂欄位新增到標準欄位群組的資訊，請參閱[結構描述UI指南](./schemas.md#custom-fields-for-standard-groups)。

若要新增欄位至自訂欄位群組，請在畫布中選取結構描述名稱旁的&#x200B;**加號(+)**&#x200B;圖示。

![](../../images/ui/resources/field-groups/add-field.png)

畫布中會出現&#x200B;**[!UICONTROL 未命名的欄位]**&#x200B;預留位置，而右邊欄會更新以顯示控制項，以設定欄位的屬性。 如需有關如何設定不同欄位型別的具體步驟，請參閱[在UI](../fields/overview.md#define)中定義欄位的指南。

在&#x200B;**[!UICONTROL 指派給]**&#x200B;下，選取&#x200B;**[!UICONTROL 欄位群組]**&#x200B;選項，然後使用下拉式清單從清單中選取所要的欄位群組。 您可以開始輸入欄位群組的名稱來縮小結果範圍。

![](../../images/ui/resources/field-groups/select-field-group.png)

在&#x200B;**[!UICONTROL 指派給]**&#x200B;下，選取&#x200B;**[!UICONTROL 欄位群組]**&#x200B;選項，然後使用下拉式清單從清單中選取所要的欄位群組。 您可以開始輸入欄位群組的名稱來縮小結果範圍。

![](../../images/ui/resources/field-groups/select-field-group.png)

將欄位新增到結構描述後，就會將其指派給所選的欄位群組。 繼續將所需數量的欄位新增至欄位群組。 完成後，選取&#x200B;**[!UICONTROL 儲存]**&#x200B;以儲存結構描述和欄位群組。

![](../../images/ui/resources/field-groups/complete-field-group.png)

如果其他結構描述已採用相同的欄位群組，則新新增的欄位會自動出現在這些結構描述中。

## 後續步驟 {#next-steps}

本指南說明如何使用Experience Platform UI建立和編輯欄位群組。 如需[!UICONTROL 結構描述]工作區功能的詳細資訊，請參閱[[!UICONTROL 結構描述]工作區概觀](../overview.md)。

若要瞭解如何使用[!DNL Schema Registry] API管理欄位群組，請參閱[欄位群組端點指南](../../api/field-groups.md)。
