---
keywords: Experience Platform；首頁；熱門主題；API;API;XDM;XDM系統；體驗資料模型；資料模型；ui；工作區；欄位群組；欄位群組；
solution: Experience Platform
title: 在UI中建立和編輯結構欄位群組
description: 了解如何在Experience Platform使用者介面中建立和編輯結構欄位群組。
topic-legacy: user guide
source-git-commit: 97f803f649b2c42b0449a2f8f0cff370ed1aba93
workflow-type: tm+mt
source-wordcount: '752'
ht-degree: 0%

---


# 在UI中建立和編輯結構欄位群組

在Experience Data Model(XDM)中，結構欄位群組是可重複使用的元件，可定義一或多個欄位，以實作特定功能，例如個人詳細資訊、飯店偏好設定或位址。 欄位組將作為實現相容類的架構的一部分而包含。

欄位組根據欄位組所代表的資料行為（記錄或時間序列）定義其相容的類別。 這表示並非所有欄位組都可用於所有類別。

Adobe Experience Platform提供許多標準欄位群組，涵蓋廣泛的行銷使用案例。 不過，您也可以建立和編輯自己的自訂欄位群組，以定義XDM結構中與您的業務相關的其他概念。 本指南概述如何在Platform UI中建立、編輯及管理貴組織的自訂欄位群組。

## 先決條件

本指南需要妥善了解XDM系統。 請參閱[XDM概述](../../home.md) ，了解XDM在Experience Platform生態系統中的角色，以及[架構組合基本概念](../../schema/composition.md) ，以了解欄位群組對XDM架構的貢獻。

雖然本指南並非必要，但建議您也參照在UI](../../tutorials/create-schema-ui.md)中撰寫架構的[教學課程，熟悉[!DNL Schema Editor]的各種功能。

## 建立新欄位群組 {#create}

要建立新欄位組，必須首先選擇要添加該欄位組的架構。 您可以選擇[建立新架構](./schemas.md#create)或[選擇要編輯的現有架構](./schemas.md#edit)。

在[!DNL Schema Editor]中開啟架構後，請在左側邊欄的[!UICONTROL 欄位群組]區段旁選取&#x200B;**[!UICONTROL 新增]**。

![](../../images/ui/resources/field-groups/add-field-group.png)

隨即出現對話方塊，顯示貴組織的現有欄位群組清單。 在對話框頂部附近，選擇「建立新欄位組」]**。**[!UICONTROL &#x200B;您可以在此處為欄位群組提供&#x200B;**[!UICONTROL 顯示名稱]**&#x200B;和&#x200B;**[!UICONTROL 說明]**。 完成後，選擇&#x200B;**[!UICONTROL 添加欄位組]**。

![](../../images/ui/resources/field-groups/create-field-group.png)

會重新顯示[!DNL Schema Editor]，新欄位群組會列在左側邊欄中。 由於這是全新欄位群組，因此目前不提供任何欄位給結構，因此畫布維持不變。 您現在可以開始[將欄位新增至欄位群組](#add-fields)。

## 編輯現有欄位組 {#edit}

>[!NOTE]
>
>只有貴組織定義的自訂欄位群組才能完全編輯和自訂。 對於由Adobe定義的核心欄位群組，在個別結構的內容中只能編輯其欄位的顯示名稱。 有關詳細資訊，請參閱[編輯架構欄位的顯示名稱的部分](./schemas.md#display-names)。
>
>儲存自訂欄位群組並用於資料擷取的結構後，之後只能對欄位群組進行加法變更。 如需詳細資訊，請參閱架構演化的[規則](../../schema/composition.md#evolution)。

要編輯現有欄位組，必須首先開啟在[!DNL Schema Editor]中採用欄位組的架構。 您可以[選擇要編輯的現有架構](./schemas.md#edit)，或者，您可以[建立新架構](./schemas.md#create)並添加相關欄位組。

在編輯器中開啟架構後，您可以啟動[向欄位群組](#add-fields)新增欄位。

## 新增欄位至欄位群組 {#add-fields}

若要將欄位新增至[!DNL Schema Editor]中的欄位群組，請從左側欄中選取欄位群組的名稱開始，然後在畫布中選取架構名稱旁的&#x200B;**加號(+)**&#x200B;圖示。

![](../../images/ui/resources/field-groups/add-field.png)

畫布中會顯示&#x200B;**[!UICONTROL 新欄位]**，而右側邊欄會更新，顯示設定欄位屬性的控制項。 如需如何設定欄位群組並將欄位新增至欄位群組的特定步驟，請參閱UI](../fields/overview.md#define)中[定義欄位的指南。

繼續將所需的欄位新增至欄位群組。 完成後，選擇&#x200B;**[!UICONTROL Save]**&#x200B;以保存架構和欄位組。

![](../../images/ui/resources/field-groups/complete-field-group.png)

如果其他結構中已採用相同的欄位群組，則新新增的欄位會自動顯示在這些結構中。

## 後續步驟

本指南說明如何使用Platform UI建立和編輯欄位群組。 如需[!UICONTROL 結構]工作區功能的詳細資訊，請參閱[[!UICONTROL 結構]工作區概述](../overview.md)。

若要了解如何使用[!DNL Schema Registry] API管理欄位群組，請參閱[欄位群組端點指南](../../api/field-groups.md)。