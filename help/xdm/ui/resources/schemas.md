---
keywords: Experience Platform;home;popular topics;api;API;XDM;XDM system;experience data model;data model;ui;workspace;schema;schemas;
solution: Experience Platform
title: 在UI中建立和編輯結構
description: 瞭解如何在Experience Platform使用者介面中建立和編輯結構描述的基本知識。
topic: user guide
translation-type: tm+mt
source-git-commit: efa1d8efb26f4196f6724702784ccd13a9337a8a
workflow-type: tm+mt
source-wordcount: '1032'
ht-degree: 0%

---


# 在UI中建立和編輯結構

本指南概述如何在Adobe Experience Platform UI中為您的組織建立、編輯和管理Experience Data Model(XDM)結構。

>[!IMPORTANT]
>
>XDM架構具有極強的可自訂性，因此，建立架構時涉及的步驟可能會因您希望架構捕獲的資料類型而異。 因此，本文檔僅涵蓋您可在UI中與結構描述進行的基本互動，並排除自訂類別、混合、資料類型和欄位等相關步驟。
>
>有關模式建立過程的完整指南，請遵循[模式建立教程](../../tutorials/create-schema-ui.md)來建立完整的示例模式並熟悉[!DNL Schema Editor]的許多功能。

## 先決條件

本指南需要對XDM System有充分的瞭解。 請參閱[XDM概述](../../home.md)以瞭解Experience Platform生態系統中XDM的角色介紹，以及[架構構成基礎](../../schema/composition.md)，以瞭解如何構建架構。

## 建立新模式{#create}

在[!UICONTROL 方案]工作區中，選擇右上角的&#x200B;**[!UICONTROL 建立方案]**。 在出現的下拉式清單中，您可以選擇&#x200B;**[!UICONTROL XDM Individual Profile]**&#x200B;和&#x200B;**[!UICONTROL XDM ExperienceEvent]**&#x200B;作為架構的基本類別。 或者，您可以選擇&#x200B;**[!UICONTROL Browse]**&#x200B;以從可用類的完整清單中進行選擇，或者選擇[建立新的自定義類](./classes.md#create)。

![](../../images/ui/resources/schemas/create-schema.png)

選擇類後，將顯示[!DNL Schema Editor] ，並在畫布中顯示方案的基本結構（由類提供）。 從這裡，您可以使用右邊欄為架構添加&#x200B;**[!UICONTROL 顯示名稱]**&#x200B;和&#x200B;**[!UICONTROL 說明]**。

![](../../images/ui/resources/schemas/schema-details.png)

您現在可以通過[添加mixins](#add-mixins)開始構建架構結構。

## 編輯現有模式{#edit}

>[!NOTE]
>
>在儲存架構並用於資料擷取後，就只能對其進行加法變更。 如需詳細資訊，請參閱[模式演化規則](../../schema/composition.md#evolution)。

要編輯現有方案，請選擇&#x200B;**[!UICONTROL 瀏覽]**&#x200B;頁籤，然後選擇要編輯的方案名稱。

![](../../images/ui/resources/schemas/edit-schema.png)

>[!TIP]
>
>您可以使用工作區的搜尋和篩選功能，協助您更輕鬆地尋找結構。 如需詳細資訊，請參閱[探索XDM資源](../explore.md)指南。

選擇架構後，[!DNL Schema Editor]將顯示，其結構顯示在畫布中。 您現在可以將mixins](#add-mixins)新增至架構，或者，如果架構採用任何，則可以編輯現有的自訂mixins](./mixins.md#edit)。[[

## 將混合添加到架構{#add-mixins}

>[!NOTE]
>
>本節介紹如何將現有混合添加到架構中。 如果您想要建立新的自訂混音，請參閱[建立和編輯混音](./mixins.md#create)的指南。

在[!DNL Schema Editor]中開啟架構後，可以通過使用mixins將欄位添加到架構中。 若要開始，請在左側導軌中選擇&#x200B;**[!UICONTROL Mixins]**&#x200B;旁邊的&#x200B;**[!UICONTROL Add]**。

![](../../images/ui/resources/schemas/add-mixin-button.png)

在出現的對話方塊中，您可以從清單中選取所需的混音。 您可以從清單中選取多個混音，每個選取的混音都會出現在右側邊欄中。

![](../../images/ui/resources/schemas/add-mixin.png)

>[!TIP]
>
>對於任何列出的混音，您可以選擇預覽表徵圖(![](../../images/ui/resources/schemas/preview-icon.png))，以在決定將混音添加到架構之前查看混音提供的欄位結構。

選擇mixin後，選擇&#x200B;**[!UICONTROL 添加mixin]**&#x200B;將其添加到模式。

![](../../images/ui/resources/schemas/add-mixin-finish.png)

[!DNL Schema Editor]會重新顯示，畫布中會顯示混合提供的欄位。

![](../../images/ui/resources/schemas/mixins-added.png)

## 啟用即時客戶配置檔案{#profile}的方案

[即時客戶分析](../../../profile/home.md) 從不同來源獲得資料，以建構每個客戶的完整視圖。如果希望架構捕獲的資料參與此進程，則必須啟用該架構以用於[!DNL Profile]。

>[!IMPORTANT]
>
>要為[!DNL Profile]啟用模式，它必須定義主標識欄位。 如需詳細資訊，請參閱[定義身分欄位](../fields/identity.md)上的指南。

要啟用方案，請從在左側導軌中選擇方案的名稱開始，然後選擇右側導軌中的&#x200B;**[!UICONTROL Profile]**&#x200B;切換。

![](../../images/ui/resources/schemas/profile-toggle.png)

此時會顯示快顯視窗，警告您一旦啟用並儲存結構，便無法停用它。 選擇&#x200B;**[!UICONTROL 啟用]**&#x200B;繼續。

![](../../images/ui/resources/schemas/profile-confirm.png)

畫布會重新顯示，並啟用[!UICONTROL Profile]切換。

>[!IMPORTANT]
>
>由於尚未保存結構，因此，如果您改變讓結構參與即時客戶概要檔案的想法，則此點是不返回的：保存啟用的模式後，它將不能再禁用。 再次選擇&#x200B;**[!UICONTROL Profile]**&#x200B;切換以禁用模式。

要完成該過程，請選擇&#x200B;**[!UICONTROL 保存]**&#x200B;以保存模式。

![](../../images/ui/resources/schemas/profile-enabled.png)

此結構現在已啟用，可用於即時客戶個人檔案。 當平台根據此模式將資料收錄到資料集時，該資料將被併入到合併的配置檔案資料中。

## 更改方案的類{#change-class}

可以在保存模式之前，在初始合成過程中的任意點更改模式的類。

>[!WARNING]
>
>重新指派架構的類別時應格外小心。 Mixins僅與特定類別相容，因此變更類別會重設畫布和您新增的任何欄位。

要重新指派類，請在畫布左側選擇&#x200B;**[!UICONTROL Assign]**。

![](../../images/ui/resources/schemas/assign-class-button.png)

此時會出現一個對話框，其中顯示所有可用類的清單，包括您的組織定義的任何類（所有者是&quot;[!UICONTROL Customer]&quot;）以及Adobe定義的標準類。

從清單中選擇一個類，在對話框的右側顯示其說明。 您也可以選擇&#x200B;**[!UICONTROL 預覽類別結構]**，以查看與類別相關聯的欄位和中繼資料。 選擇&#x200B;**[!UICONTROL Assign class]**&#x200B;以繼續。

![](../../images/ui/resources/schemas/assign-class.png)

隨即開啟新對話方塊，要求您確認您要指派新類別。 選擇&#x200B;**[!UICONTROL Assign]**&#x200B;進行確認。

![](../../images/ui/resources/schemas/assign-confirm.png)

在確認類別變更後，畫布將重設，而所有的構圖進度都將遺失。

## 後續步驟

本檔案涵蓋在平台UI中建立和編輯結構描述的基本知識。 強烈建議您檢閱[架構建立教學課程](../../tutorials/create-schema-ui.md)，以取得在UI中建立完整架構的完整工作流程，包括建立自訂混合和資料類型，以利獨特使用案例。

有關[!UICONTROL 方案]工作區功能的詳細資訊，請參閱[[!UICONTROL 方案]工作區概述](../overview.md)。

要瞭解如何在[!DNL Schema Registry] API中管理方案，請參閱[方案端點指南](../../api/schemas.md)。