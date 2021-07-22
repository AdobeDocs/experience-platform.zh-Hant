---
keywords: Experience Platform；首頁；熱門主題；API;API;XDM;XDM系統；體驗資料模型；資料模型；ui；工作區；結構；結構；結構；
solution: Experience Platform
title: 在UI中建立和編輯結構
description: 了解如何在Experience Platform使用者介面中建立和編輯結構的基本知識。
topic-legacy: user guide
exl-id: be83ce96-65b5-4a4a-8834-16f7ef9ec7d1
source-git-commit: 6402499535b71f43c158fcec7e2b0065437bed51
workflow-type: tm+mt
source-wordcount: '1434'
ht-degree: 0%

---

# 在UI中建立和編輯結構

本指南概述如何在Adobe Experience Platform UI中為貴組織建立、編輯及管理Experience Data Model(XDM)結構。

>[!IMPORTANT]
>
>XDM結構具有極強的可自訂性，因此建立結構時的步驟可能會因您要結構擷取的資料類型而異。 因此，本檔案僅涵蓋您可以在UI中與結構進行的基本互動，並排除了自訂類別、結構欄位群組、資料類型和欄位等相關步驟。
>
>有關架構建立過程的完整教程，請按照[架構建立教程](../../tutorials/create-schema-ui.md)建立完整的示例架構，並熟悉[!DNL Schema Editor]的許多功能。

## 先決條件

本指南需要妥善了解XDM系統。 請參閱[XDM概述](../../home.md) ，了解XDM在Experience Platform生態系統中的角色，以及架構組合的[基本概念](../../schema/composition.md) ，以了解如何建構架構的概觀。

## 建立新結構 {#create}

在[!UICONTROL 結構]工作區中，選擇右上角的&#x200B;**[!UICONTROL 建立結構]**。 在顯示的下拉式清單中，您可以選擇&#x200B;**[!UICONTROL XDM個別設定檔]**&#x200B;和&#x200B;**[!UICONTROL XDM ExperienceEvent]**&#x200B;作為架構的基本類別。 或者，您可以選擇&#x200B;**[!UICONTROL Browse]**&#x200B;以從可用類的完整清單中進行選擇，或者選擇[建立新的自定義類](./classes.md#create)。

![](../../images/ui/resources/schemas/create-schema.png)

選取類別後，會顯示[!DNL Schema Editor]，而畫布中會顯示架構的基礎結構（由類別提供）。 從這裡，您可以使用右側邊欄，為架構新增&#x200B;**[!UICONTROL 顯示名稱]**&#x200B;和&#x200B;**[!UICONTROL 說明]**。

![](../../images/ui/resources/schemas/schema-details.png)

您現在可以透過[新增架構欄位群組](#add-field-groups)開始建立架構結構。

## 編輯現有架構 {#edit}

>[!NOTE]
>
>儲存結構並用於資料擷取後，就只能對其進行加入式變更。 如需詳細資訊，請參閱架構演化的[規則](../../schema/composition.md#evolution)。

要編輯現有架構，請選擇&#x200B;**[!UICONTROL Browse]**&#x200B;頁簽，然後選擇要編輯的架構的名稱。

![](../../images/ui/resources/schemas/edit-schema.png)

>[!TIP]
>
>您可以使用工作區的搜尋和篩選功能來協助您更輕鬆找到結構。 如需詳細資訊，請參閱[探索XDM資源](../explore.md)的指南。

選取架構後，畫布中會顯示[!DNL Schema Editor]架構的結構。 您現在可以將[欄位組](#add-field-groups)添加到架構中，或者將欄位顯示名稱](#display-names)編輯，或者，如果架構採用任何模式，則可以編輯現有的自定義欄位組](./field-groups.md#edit)。[[

## 將欄位群組新增至結構 {#add-field-groups}

>[!NOTE]
>
>本節說明如何將現有欄位群組新增至結構。 如果要建立新的自定義欄位組，請改為參閱[建立和編輯欄位組](./field-groups.md#create)上的指南。

在[!DNL Schema Editor]中開啟架構後，可以使用欄位組將欄位添加到架構中。 若要開始，請在左側邊欄中選取&#x200B;**[!UICONTROL 欄位群組]**&#x200B;旁的&#x200B;**[!UICONTROL 新增]**。

![](../../images/ui/resources/schemas/add-field-group-button.png)

隨即出現對話框，其中顯示可為架構選擇的欄位組清單。 由於欄位組僅與一個類相容，因此將只列出與架構的所選類相關聯的那些欄位組。 依預設，列出的欄位群組會根據其在您組織中的使用人氣排序。

![](../../images/ui/resources/schemas/field-group-popularity.png)

如果您知道要新增欄位的一般活動或業務區域，請在左側欄中選取一或多個垂直產業類別，以篩選顯示的欄位群組清單。

![](../../images/ui/resources/schemas/industry-filter.png)

>[!NOTE]
>
>如需XDM中特定產業資料模型最佳實務的詳細資訊，請參閱[產業資料模型](../../schema/industries/overview.md)的相關檔案。

您也可以使用搜尋列來協助找出您想要的欄位群組。 名稱與查詢相符的欄位群組會顯示在清單頂端。 在&#x200B;**[!UICONTROL 標準欄位]**&#x200B;下，將顯示包含描述所需資料屬性的欄位的欄位組。

![](../../images/ui/resources/schemas/field-group-search.png)

選取您要新增至架構之欄位群組名稱旁的核取方塊。 您可以從清單中選取多個欄位群組，每個選取的欄位群組會顯示在右側邊欄中。

![](../../images/ui/resources/schemas/add-field-group.png)

>[!TIP]
>
>對於任何列出的欄位組，您可以暫留或聚焦在資訊表徵圖(![](../../images/ui/resources/schemas/info-icon.png))，以查看欄位組捕獲的資料類型的簡短說明。 您也可以選取預覽圖示(![](../../images/ui/resources/schemas/preview-icon.png))，以在您決定將欄位新增至架構之前，檢視欄位群組提供之欄位的結構。

選擇欄位組後，選擇&#x200B;**[!UICONTROL 添加欄位組]**&#x200B;將它們添加到架構。

![](../../images/ui/resources/schemas/add-field-group-finish.png)

[!DNL Schema Editor]會以畫布中顯示的欄位群組提供的欄位重新顯示。

![](../../images/ui/resources/schemas/field-groups-added.png)

## 啟用即時客戶個人檔案的結構 {#profile}

[即時客戶設定檔](../../../profile/home.md) 從不同的來源呈現資料，以建構每個客戶的完整檢視。如果希望架構捕獲的資料參與此過程，必須啟用該架構以用於[!DNL Profile]。

>[!IMPORTANT]
>
>為[!DNL Profile]啟用架構，必須定義主標識欄位。 如需詳細資訊，請參閱[定義身分欄位](../fields/identity.md)的指南。

若要啟用架構，請從左側邊欄中選取架構的名稱開始，然後選取右側邊欄中的&#x200B;**[!UICONTROL Profile]**&#x200B;切換按鈕。

![](../../images/ui/resources/schemas/profile-toggle.png)

畫面會顯示彈出視窗，警告一旦啟用並儲存架構後，就無法停用。 選擇&#x200B;**[!UICONTROL 啟用]**&#x200B;以繼續。

![](../../images/ui/resources/schemas/profile-confirm.png)

畫布會重新顯示，並啟用[!UICONTROL 設定檔]切換。

>[!IMPORTANT]
>
>由於尚未儲存結構，如果您改變心意讓結構參與即時客戶設定檔，則此為無法傳回的點：儲存已啟用的架構後，就無法再停用該架構。 再次選擇&#x200B;**[!UICONTROL Profile]**&#x200B;切換以禁用架構。

要完成該過程，請選擇&#x200B;**[!UICONTROL Save]**&#x200B;以保存架構。

![](../../images/ui/resources/schemas/profile-enabled.png)

此結構現已啟用，可在即時客戶設定檔中使用。 Platform根據此結構將資料內嵌至資料集時，該資料將會併入您合併的設定檔資料中。

## 編輯架構欄位的顯示名稱 {#display-names}

在您指派類別並新增欄位群組至架構後，無論標準或自訂XDM資源是否已提供這些欄位，您都可以編輯任何架構欄位的顯示名稱。

>[!NOTE]
>
>請記住，屬於標準類或欄位組的欄位的顯示名稱只能在特定架構的上下文中編輯。 換言之，更改一個方案中標準欄位的顯示名稱不會影響採用相同關聯類別或欄位群組的其他方案。
>
>變更結構欄位的顯示名稱后，這些變更會立即反映在根據該結構的任何現有資料集中。

若要編輯架構欄位的顯示名稱，請在畫布中選取欄位。 在右側邊欄中，在&#x200B;**[!UICONTROL 顯示名稱]**&#x200B;下提供新名稱。

![](../../images/ui/resources/schemas/display-name.png)

在右側邊欄中選取「**[!UICONTROL 套用]**」，畫布會更新以顯示欄位的新顯示名稱。 選擇&#x200B;**[!UICONTROL Save]**&#x200B;以將更改應用到架構。

![](../../images/ui/resources/schemas/display-name-changed.png)

## 更改架構的類 {#change-class}

您可以在儲存架構之前的初始合成程式期間的任何時間點變更架構的類別。

>[!WARNING]
>
>為架構重新指派類別時應格外小心。 欄位組僅與某些類相容，因此更改類將重置畫布和您添加的任何欄位。

要重新分配類，請在畫布的左側選擇&#x200B;**[!UICONTROL Assign]**。

![](../../images/ui/resources/schemas/assign-class-button.png)

此時將顯示一個對話框，其中顯示所有可用類的清單，包括您的組織定義的任何類（所有者為&quot;[!UICONTROL Customer]&quot;）以及由Adobe定義的標準類。

從清單中選擇一個類，以在對話框的右側顯示其說明。 您也可以選擇&#x200B;**[!UICONTROL 預覽類結構]**&#x200B;以查看與類關聯的欄位和元資料。 選擇&#x200B;**[!UICONTROL 分配類]**&#x200B;以繼續。

![](../../images/ui/resources/schemas/assign-class.png)

將開啟一個新對話框，要求您確認要指派新類。 選擇&#x200B;**[!UICONTROL Assign]**&#x200B;以確認。

![](../../images/ui/resources/schemas/assign-confirm.png)

確認類別變更後，畫布會重設，所有合成進度都會遺失。

## 後續步驟

本檔案說明在Platform UI中建立和編輯結構描述的基本知識。 強烈建議您檢閱[架構建立教學課程](../../tutorials/create-schema-ui.md)，以了解在UI中建立完整架構的完整工作流程，包括針對不重複使用案例建立自訂欄位群組和資料類型。

如需[!UICONTROL 結構]工作區功能的詳細資訊，請參閱[[!UICONTROL 結構]工作區概述](../overview.md)。

若要了解如何在[!DNL Schema Registry] API中管理結構，請參閱[結構端點指南](../../api/schemas.md)。
