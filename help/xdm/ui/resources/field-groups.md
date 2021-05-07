---
keywords: Experience Platform;home；熱門主題；api;API;XDM;XDM系統；體驗資料模型；ui；工作區；欄位組；欄位組；
solution: Experience Platform
title: 在UI中建立和編輯結構欄位群組
description: 瞭解如何在Experience Platform用戶介面中建立和編輯架構欄位組。
topic: 使用指南
translation-type: tm+mt
source-git-commit: 3985ba8f46a62e8d9ea8b1f084198b245318a24f
workflow-type: tm+mt
source-wordcount: '736'
ht-degree: 0%

---


# 在UI中建立和編輯架構欄位群組

在Experience Data Model(XDM)中，架構欄位群組是可重複使用的元件，可定義一或多個欄位，以實作特定功能，例如個人詳細資料、飯店偏好設定或地址。 欄位組將作為實現相容類的架構的一部分被包括。

欄位組根據欄位組所代表的資料的行為（記錄或時間序列）定義與哪些類相容。 這表示並非所有欄位組都可用於所有類。

Adobe Experience Platform提供許多標準欄位群組，涵蓋廣泛的行銷使用案例。 不過，您也可以建立和編輯您自己的自訂欄位群組，以定義XDM結構中與您的業務相關的其他概念。 本指南提供如何在平台UI中建立、編輯和管理您組織的自訂欄位群組的概觀。

## 先決條件

本指南需要對XDM System有充分的瞭解。 有關XDM在Experience Platform生態系統中的角色介紹，請參閱[XDM概述](../../home.md)，有關模式組合[的基本說明](../../schema/composition.md)，瞭解欄位組對XDM架構的貢獻。

雖然本指南不是必要的，但建議您也要遵循在UI](../../tutorials/create-schema-ui.md)中構成架構的[教學課程，以熟悉[!DNL Schema Editor]的各種功能。

## 建立新欄位組{#create}

要建立新欄位組，必須首先選擇要添加該欄位組的方案。 您可以選擇[建立新方案](./schemas.md#create)或[選擇現有方案以編輯](./schemas.md#edit)。

在[!DNL Schema Editor]中開啟架構後，請選擇左側導軌中[!UICONTROL Field groups]部分旁的&#x200B;**[!UICONTROL Add]**。

![](../../images/ui/resources/field-groups/add-field-group.png)

此時會出現對話方塊，顯示您組織的現有欄位群組清單。 在對話框頂部附近，選擇&#x200B;**[!UICONTROL Create new field group]**。 您可在此處為欄位群組提供&#x200B;**[!UICONTROL Display name]**&#x200B;和&#x200B;**[!UICONTROL Description]**。 完成後，選擇&#x200B;**[!UICONTROL Add field group]**。

![](../../images/ui/resources/field-groups/create-field-group.png)

[!DNL Schema Editor]會重新出現，新欄位群組會列在左側欄位中。 由於這是全新的欄位群組，因此目前不會為架構提供任何欄位，因此畫布會維持不變。 您現在可以開始將欄位添加到欄位組](#add-fields)。[

## 編輯現有欄位組{#edit}

>[!NOTE]
>
>您的組織所定義的自訂欄位群組只能完整編輯和自訂。 對於由Adobe定義的核心欄位組，只能在單個方案的上下文中編輯其欄位的顯示名稱。 有關詳細資訊，請參閱[編輯架構欄位的顯示名稱一節。](./schemas.md#display-names)
>
>在自訂欄位群組儲存並用於資料擷取架構後，之後只能對欄位群組進行加法變更。 如需詳細資訊，請參閱[模式演化規則](../../schema/composition.md#evolution)。

要編輯現有欄位組，必須首先開啟[!DNL Schema Editor]中使用欄位組的方案。 您可以[選擇要編輯的現有模式，或者可以[建立新模式](./schemas.md#create)並添加相關欄位組。](./schemas.md#edit)

在編輯器中開啟模式後，可以啟動[向欄位組](#add-fields)添加欄位。

## 將欄位添加到欄位組{#add-fields}

若要將欄位新增至[!DNL Schema Editor]中的欄位群組，請先選取左側欄位中欄位群組的名稱，然後選取畫布中架構名稱旁的&#x200B;**加號(+)**&#x200B;圖示。

![](../../images/ui/resources/field-groups/add-field.png)

畫布中會出現&#x200B;**[!UICONTROL New field]**，右側邊欄會更新，以顯示設定欄位屬性的控制項。 有關如何配置欄位並將其添加到欄位組的具體步驟，請參閱UI](../fields/overview.md#define)中[定義欄位的指南。

繼續新增欄位群組所需的欄位數。 完成後，選擇&#x200B;**[!UICONTROL Save]**&#x200B;以保存模式和欄位組。

![](../../images/ui/resources/field-groups/complete-field-group.png)

如果其他方案中已使用相同的欄位組，則新添加的欄位將自動顯示在這些方案中。

## 後續步驟

本指南說明如何使用平台UI建立和編輯欄位群組。 有關[!UICONTROL Schemas]工作區功能的詳細資訊，請參閱[[!UICONTROL Schemas]工作區概述](../overview.md)。

要瞭解如何使用[!DNL Schema Registry] API管理欄位組，請參閱[欄位組端點指南](../../api/field-groups.md)。