---
keywords: Experience Platform;home；熱門主題；api;API;XDM;XDM系統；體驗資料模型；ui;workspace;schema;schema;
solution: Experience Platform
title: 在UI中建立和編輯結構描述
description: 瞭解如何在Experience Platform使用者介面中建立和編輯結構描述的基本知識。
topic-legacy: user guide
exl-id: be83ce96-65b5-4a4a-8834-16f7ef9ec7d1
translation-type: tm+mt
source-git-commit: d425dcd9caf8fccd0cb35e1bac73950a6042a0f8
workflow-type: tm+mt
source-wordcount: '1370'
ht-degree: 0%

---

# 在UI中建立和編輯結構

本指南概述如何在Adobe Experience PlatformUI中為您的組織建立、編輯和管理體驗資料模型(XDM)結構。

>[!IMPORTANT]
>
>XDM架構具有極強的可自訂性，因此，建立架構時涉及的步驟可能會因您希望架構捕獲的資料類型而異。 因此，本文檔僅涵蓋您可在UI中與結構描述進行的基本互動，並排除自訂類別、結構描述欄位群組、資料類型和欄位等相關步驟。
>
>有關模式建立過程的完整指南，請遵循[模式建立教程](../../tutorials/create-schema-ui.md)來建立完整的示例模式並熟悉[!DNL Schema Editor]的許多功能。

## 先決條件

本指南需要對XDM System有充分的瞭解。 有關XDM在Experience Platform生態系統中的角色介紹，請參閱[XDM概述](../../home.md)，有關架構構成的概述，請參閱[基本架構構成](../../schema/composition.md)。

## 建立新模式{#create}

在[!UICONTROL Schemas]工作區中，選擇右上角的&#x200B;**[!UICONTROL Create schema]**。 在出現的下拉式清單中，您可以選擇&#x200B;**[!UICONTROL XDM Individual Profile]**&#x200B;和&#x200B;**[!UICONTROL XDM ExperienceEvent]**&#x200B;作為架構的基本類別。 或者，您可以選擇&#x200B;**[!UICONTROL Browse]**&#x200B;以從可用類的完整清單中進行選擇，或者選擇[建立新的自定義類](./classes.md#create)。

![](../../images/ui/resources/schemas/create-schema.png)

選擇類後，將顯示[!DNL Schema Editor] ，並在畫布中顯示方案的基本結構（由類提供）。 在此處，可以使用右邊欄為架構添加&#x200B;**[!UICONTROL Display name]**&#x200B;和&#x200B;**[!UICONTROL Description]**。

![](../../images/ui/resources/schemas/schema-details.png)

現在，您可以通過[添加模式欄位組](#add-field-groups)開始構建模式結構。

## 編輯現有模式{#edit}

>[!NOTE]
>
>在儲存架構並用於資料擷取後，就只能對其進行加法變更。 如需詳細資訊，請參閱[模式演化規則](../../schema/composition.md#evolution)。

要編輯現有方案，請選擇&#x200B;**[!UICONTROL Browse]**&#x200B;頁籤，然後選擇要編輯的方案名稱。

![](../../images/ui/resources/schemas/edit-schema.png)

>[!TIP]
>
>您可以使用工作區的搜尋和篩選功能，協助您更輕鬆地尋找結構。 如需詳細資訊，請參閱[探索XDM資源](../explore.md)指南。

選擇架構後，[!DNL Schema Editor]將顯示，其結構顯示在畫布中。 現在，如果方案採用任何方案，您可以[將欄位組](#add-field-groups)添加到方案中， [編輯欄位顯示名稱](#display-names)，或[編輯現有的自定義欄位組](./field-groups.md#edit)。

## 將欄位組添加到方案{#add-field-groups}

>[!NOTE]
>
>本節介紹如何將現有欄位組添加到架構中。 如果要建立新的自定義欄位組，請參閱[建立和編輯欄位組](./field-groups.md#create)上的指南。

在[!DNL Schema Editor]中開啟架構後，可以通過使用欄位組將欄位添加到架構中。 若要開始，請選取左側導軌中&#x200B;**[!UICONTROL Field groups]**&#x200B;旁的&#x200B;**[!UICONTROL Add]**。

![](../../images/ui/resources/schemas/add-field-group-button.png)

此時將顯示一個對話框，其中顯示可為架構選擇的欄位組清單。 由於欄位組只與一個類相容，因此將只列出與方案選定類關聯的那些欄位組。 依預設，列出的欄位群組會根據其在您組織中的使用人氣來排序。

![](../../images/ui/resources/schemas/field-group-popularity.png)

如果您知道要添加的欄位的一般活動或業務區，請在左側導軌中選擇一個或多個行業垂直類別，以過濾顯示的欄位組清單。

![](../../images/ui/resources/schemas/industry-filter.png)

>[!NOTE]
>
>有關XDM中特定行業資料建模的最佳實踐的詳細資訊，請參閱[行業資料模型](../../schema/industries/overview.md)上的文檔。

您也可以使用搜尋列來協助找出您所要的欄位群組。 名稱與查詢相符的欄位群組會出現在清單頂端。 在&#x200B;**[!UICONTROL Standard Fields]**&#x200B;下，會顯示包含描述所需資料屬性之欄位的欄位群組。

![](../../images/ui/resources/schemas/field-group-search.png)

選擇要添加到方案的欄位組名稱旁的複選框。 您可以從清單中選取多個欄位群組，每個選取的欄位群組都會顯示在右側欄位中。

![](../../images/ui/resources/schemas/add-field-group.png)

>[!TIP]
>
>對於任何列出的欄位組，您可以將滑鼠暫留在資訊表徵圖(![](../../images/ui/resources/schemas/info-icon.png))上查看欄位組捕獲的資料類型的簡要說明。 您也可以選擇預覽表徵圖(![](../../images/ui/resources/schemas/preview-icon.png))，在決定將欄位組添加到方案之前查看欄位組提供的欄位結構。

選擇欄位組後，選擇&#x200B;**[!UICONTROL Add field groups]**&#x200B;將其添加到模式。

![](../../images/ui/resources/schemas/add-field-group-finish.png)

[!DNL Schema Editor]會重新顯示，畫布中會顯示欄位群組提供的欄位。

![](../../images/ui/resources/schemas/field-groups-added.png)

## 啟用即時客戶配置檔案{#profile}的方案

[即時客戶分析](../../../profile/home.md) 從不同來源獲得資料，以建構每個客戶的完整視圖。如果希望架構捕獲的資料參與此進程，則必須啟用該架構以用於[!DNL Profile]。

>[!IMPORTANT]
>
>要為[!DNL Profile]啟用模式，它必須定義主標識欄位。 如需詳細資訊，請參閱[定義身分欄位](../fields/identity.md)上的指南。

要啟用方案，請從在左側導軌中選擇方案的名稱開始，然後選擇右側導軌中的&#x200B;**[!UICONTROL Profile]**&#x200B;切換。

![](../../images/ui/resources/schemas/profile-toggle.png)

此時會顯示快顯視窗，警告您一旦啟用並儲存結構，便無法停用它。 選擇&#x200B;**[!UICONTROL Enable]**&#x200B;繼續。

![](../../images/ui/resources/schemas/profile-confirm.png)

畫布會重新顯示，並啟用[!UICONTROL Profile]切換。

>[!IMPORTANT]
>
>由於尚未保存結構，因此，如果您改變讓結構參與即時客戶概要檔案的想法，則此點是不返回的：保存啟用的模式後，它將不能再禁用。 再次選擇&#x200B;**[!UICONTROL Profile]**&#x200B;切換以禁用模式。

要完成該過程，請選擇&#x200B;**[!UICONTROL Save]**&#x200B;以保存模式。

![](../../images/ui/resources/schemas/profile-enabled.png)

此結構現在已啟用，可用於即時客戶個人檔案。 當平台根據此模式將資料收錄到資料集時，該資料將被併入到合併的配置檔案資料中。

## 編輯架構欄位{#display-names}的顯示名稱

在為架構分配了類並添加了欄位組後，您可以編輯該架構的任何欄位的顯示名稱，而不管這些欄位是由標準還是自定義XDM資源提供。

>[!NOTE]
>
>請記住，屬於標準類或欄位組的欄位的顯示名稱只能在特定方案的上下文中編輯。 換句話說，更改一個方案中標準欄位的顯示名稱不會影響使用相同關聯類或欄位組的其他方案。

若要編輯結構欄位的顯示名稱，請選取畫布中的欄位。 在右邊欄中，在&#x200B;**[!UICONTROL Display name]**&#x200B;下提供新名稱。

![](../../images/ui/resources/schemas/display-name.png)

在右邊欄中選取&#x200B;**[!UICONTROL Apply]**，畫布就會更新以顯示欄位的新顯示名稱。 選擇&#x200B;**[!UICONTROL Save]**&#x200B;將更改應用到模式。

![](../../images/ui/resources/schemas/display-name-changed.png)

## 更改方案的類{#change-class}

可以在保存模式之前，在初始合成過程中的任意點更改模式的類。

>[!WARNING]
>
>重新指派架構的類別時應格外小心。 欄位群組僅與特定類別相容，因此變更類別將重設畫布和您新增的任何欄位。

要重新指派類，請在畫布左側選擇&#x200B;**[!UICONTROL Assign]**。

![](../../images/ui/resources/schemas/assign-class-button.png)

此時將顯示一個對話框，其中顯示所有可用類的清單，包括您的組織定義的任何類（所有者為&quot;[!UICONTROL Customer]&quot;）以及Adobe定義的標準類。

從清單中選擇一個類，在對話框的右側顯示其說明。 您也可以選取&#x200B;**[!UICONTROL Preview class structure]**&#x200B;來查看與類別相關的欄位和中繼資料。 選擇&#x200B;**[!UICONTROL Assign class]**&#x200B;繼續。

![](../../images/ui/resources/schemas/assign-class.png)

隨即開啟新對話方塊，要求您確認您要指派新類別。 選擇&#x200B;**[!UICONTROL Assign]**&#x200B;進行確認。

![](../../images/ui/resources/schemas/assign-confirm.png)

在確認類別變更後，畫布將重設，而所有的構圖進度都將遺失。

## 後續步驟

本檔案涵蓋在平台UI中建立和編輯結構描述的基本知識。 強烈建議您檢閱[架構建立教學課程](../../tutorials/create-schema-ui.md)，以取得在UI中建立完整架構的完整工作流程，包括建立自訂欄位群組和資料類型，以利獨特使用案例。

有關[!UICONTROL Schemas]工作區功能的詳細資訊，請參閱[[!UICONTROL Schemas]工作區概述](../overview.md)。

要瞭解如何在[!DNL Schema Registry] API中管理方案，請參閱[方案端點指南](../../api/schemas.md)。
