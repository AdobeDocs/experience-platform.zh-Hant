---
keywords: Experience Platform;home；熱門主題；api;API;XDM;XDM系統；體驗資料模型；ui;workspace;mixin;mixins;
solution: Experience Platform
title: 在UI中建立和編輯混音
description: 瞭解如何在Experience Platform使用者介面中建立和編輯混合。
topic: user guide
translation-type: tm+mt
source-git-commit: 2e20403122e65d28f04114af9b7e8d41874f76e2
workflow-type: tm+mt
source-wordcount: '668'
ht-degree: 0%

---


# 在UI中建立和編輯混音

在Experience Data Model(XDM)中，混合是可重複使用的元件，可定義一或多個欄位，以實作特定功能，例如個人詳細資料、飯店偏好設定或地址。 Mixin是作為實現相容類的模式的一部分而包括的。

混音基於混音所代表的資料（記錄或時間序列）的行為，定義它與哪些類相容。 這表示並非所有混音都可用於所有類別。

Adobe Experience Platform提供許多標準混搭，涵蓋廣泛的行銷使用案例。 不過，您也可以建立和編輯您自己的自訂混音，以定義XDM結構中與您的業務相關的其他概念。 本指南提供如何在平台UI中建立、編輯和管理組織自訂混音的概觀。

## 必要條件

本指南需要對XDM System有充分的瞭解。 請參閱[XDM概述](../../home.md)以瞭解XDM在Experience Platform生態系統中的角色，以及[架構構成基礎](../../schema/composition.md)，瞭解mixins對XDM架構的貢獻。

雖然本指南不是必要的，但建議您也要遵循在UI](../../tutorials/create-schema-ui.md)中構成架構的[教學課程，以熟悉[!DNL Schema Editor]的各種功能。

## 建立新的混音{#create}

若要建立新混音，您必須先選取要新增混音的結構。 您可以選擇[建立新方案](./schemas.md#create)或[選擇現有方案以編輯](./schemas.md#edit)。

在[!DNL Schema Editor]中開啟架構後，請在左側導軌的[!UICONTROL Mixins]區段旁選擇「添加」。****

![](../../images/ui/resources/mixins/add-mixin-button.png)

此時會出現對話方塊，顯示您組織的現有混音清單。 在對話框頂部附近，選擇「建立新混音」。 ****&#x200B;在這裡，您可以為混音提供&#x200B;**[!UICONTROL 顯示名稱]**&#x200B;和&#x200B;**[!UICONTROL 說明]**。 完成後，選擇「添加mixin ]**」。**[!UICONTROL 

![](../../images/ui/resources/mixins/create-mixin.png)

[!DNL Schema Editor]會重新出現，新混音列在左側導軌中。 由於這是全新的混音，所以目前不會為架構提供任何欄位，因此畫布會維持不變。 您現在可以開始將欄位添加到mixin](#add-fields)。[

## 編輯{#edit}中的現有混音

>[!NOTE]
>
>只能編輯您組織定義的自訂混音。
>
>此外，一旦混音被保存並用於資料接收模式中，之後只能對混音進行加性改變。 如需詳細資訊，請參閱[模式演化規則](../../schema/composition.md#evolution)。

要編輯現有混音，必須首先開啟在[!DNL Schema Editor]中使用混音的模式。 您可以[選擇要編輯的現有模式，或者可以[建立新模式](./schemas.md#create)並添加相關混合。](./schemas.md#edit)

在編輯器中開啟模式後，可以啟動[向mixin](#add-fields)添加欄位。

## 將欄位新增至mixin {#add-fields}

若要在[!DNL Schema Editor]中將欄位新增至混音，請先在左側導軌中選取混音的名稱，然後在畫布中選取架構名稱旁的&#x200B;**加號(+)**&#x200B;圖示。

![](../../images/ui/resources/mixins/add-field-button.png)

畫布中會顯示&#x200B;**[!UICONTROL 新欄位]**，右側欄位會更新，顯示設定欄位屬性的控制項。 如需如何設定欄位並將欄位新增至混音的特定步驟，請參閱UI](../fields/overview.md#define)中[定義欄位的指南。

繼續新增所需的欄位至混音。 完成後，選擇&#x200B;**[!UICONTROL Save]**&#x200B;以保存模式和混音。

![](../../images/ui/resources/mixins/complete-mixin.png)

如果其他結構中已使用相同的混音，新新增的欄位將自動顯示在這些結構中。

## 後續步驟

本指南說明如何使用平台UI建立和編輯混合。 有關[!UICONTROL 方案]工作區功能的詳細資訊，請參閱[[!UICONTROL 方案]工作區概述](../overview.md)。

要瞭解如何使用[!DNL Schema Registry] API管理混音，請參閱[mixins端點指南](../../api/mixins.md)。