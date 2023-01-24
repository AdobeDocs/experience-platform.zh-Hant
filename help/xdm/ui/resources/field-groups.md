---
keywords: Experience Platform；首頁；熱門主題；API;API;XDM;XDM系統；體驗資料模型；資料模型；ui；工作區；欄位群組；欄位群組；
solution: Experience Platform
title: 在UI中建立和編輯結構欄位群組
description: 了解如何在Experience Platform使用者介面中建立和編輯結構欄位群組。
exl-id: 928d70a6-0468-4fb7-a53a-6686ac77f2a3
source-git-commit: 542ad49f475ac9586da506a8afa5408e83262121
workflow-type: tm+mt
source-wordcount: '839'
ht-degree: 0%

---

# 在UI中建立和編輯結構欄位群組

在Experience Data Model(XDM)中，結構欄位群組是可重複使用的元件，可定義一或多個欄位，以實作特定功能，例如個人詳細資訊、飯店偏好設定或位址。 欄位組將作為實現相容類的架構的一部分而包含。

欄位組根據欄位組所代表的資料行為（記錄或時間序列）定義其相容的類別。 這表示並非所有欄位組都可用於所有類別。

Adobe Experience Platform提供許多標準欄位群組，涵蓋廣泛的行銷使用案例。 不過，您也可以建立和編輯自己的自訂欄位群組，以定義XDM結構中與您的業務相關的其他概念。 本指南概述如何在Platform UI中建立、編輯及管理貴組織的自訂欄位群組。

## 先決條件

本指南需要妥善了解XDM系統。 請參閱 [XDM概觀](../../home.md) 了解XDM在Experience Platform生態系統中的角色，以及 [綱要構成基本知識](../../schema/composition.md) 了解欄位群組對XDM結構的貢獻方式。

雖然本指南並非必要項目，但建議您也參照 [在UI中合成架構](../../tutorials/create-schema-ui.md) 熟悉 [!DNL Schema Editor].

## 建立新欄位群組 {#create}

要建立新欄位組，必須首先選擇要添加該欄位組的架構。 您可以選擇 [建立新架構](./schemas.md#create) 或 [選擇要編輯的現有架構](./schemas.md#edit).

在中開啟結構後 [!DNL Schema Editor]，選取 **[!UICONTROL 新增]** 旁邊 [!UICONTROL 欄位群組] 區段。

![](../../images/ui/resources/field-groups/add-field-group.png)

在顯示的對話方塊中，選取 **[!UICONTROL 建立新欄位組]**. 您可以在此提供 **[!UICONTROL 顯示名稱]** 和 **[!UICONTROL 說明]** 欄位群組。 完成後，請選取 **[!UICONTROL 新增欄位群組]**.

![](../../images/ui/resources/field-groups/create-field-group.png)

此 [!DNL Schema Editor] 重新顯示，新欄位群組列在左側邊欄中。 由於這是全新欄位群組，因此目前不提供任何欄位給結構，因此畫布維持不變。 您現在可以開始 [新增欄位至欄位群組](#add-fields).

![](../../images/ui/resources/field-groups/field-group-added.png)

## 編輯現有欄位組 {#edit}

>[!NOTE]
>
>只有貴組織定義的自訂欄位群組才能完全編輯和自訂。 對於由Adobe定義的核心欄位群組，在個別結構的內容中只能編輯其欄位的顯示名稱。 請參閱 [編輯架構欄位的顯示名稱](./schemas.md#display-names) 以取得詳細資訊。
>
>儲存自訂欄位群組並用於資料擷取的結構後，之後只能對欄位群組進行加法變更。 請參閱 [模式演化規則](../../schema/composition.md#evolution) 以取得更多資訊。

若要編輯現有欄位群組，您必須先開啟在 [!DNL Schema Editor]. 您可以 [選擇要編輯的現有架構](./schemas.md#edit)或 [建立新架構](./schemas.md#create) 並添加有關的欄位組。

在編輯器中開啟結構後，您就可以開始 [新增欄位至欄位群組](#add-fields).

## 新增欄位至欄位群組 {#add-fields}

>[!NOTE]
>
>本節著重於新增欄位至自訂欄位群組。 有關如何將自訂欄位新增至標準欄位群組的資訊，請參閱 [結構UI指南](./schemas.md#custom-fields-for-standard-groups).

若要將欄位新增至自訂欄位群組，請從選取 **加號(+)** 圖示。

![](../../images/ui/resources/field-groups/add-field.png)

安 **[!UICONTROL 無標題欄位]** 預留位置會顯示在畫布中，而右側邊欄會更新，顯示設定欄位屬性的控制項。 請參閱 [定義UI中的欄位](../fields/overview.md#define) ，以了解如何設定不同欄位類型的特定步驟。

在 **[!UICONTROL 指派給]**，請選取 **[!UICONTROL 欄位組]** 選項，然後使用下拉式清單從清單中選取所需的欄位群組。 您可以開始在欄位群組的名稱中輸入以縮小結果。

![](../../images/ui/resources/field-groups/select-field-group.png)

在 **[!UICONTROL 指派給]**，請選取 **[!UICONTROL 欄位組]** 選項，然後使用下拉式清單從清單中選取所需的欄位群組。 您可以開始在欄位群組的名稱中輸入以縮小結果。

![](../../images/ui/resources/field-groups/select-field-group.png)

欄位新增至架構後，即會指派給選取的欄位群組。 繼續將所需的欄位新增至欄位群組。 完成後，請選取 **[!UICONTROL 儲存]** 以儲存結構和欄位群組。

![](../../images/ui/resources/field-groups/complete-field-group.png)

如果其他結構中已採用相同的欄位群組，則新新增的欄位會自動顯示在這些結構中。

## 後續步驟

本指南說明如何使用Platform UI建立和編輯欄位群組。 如需功能的詳細資訊，請參閱 [!UICONTROL 結構] 工作區，請參閱 [[!UICONTROL 結構] 工作區概述](../overview.md).

若要了解如何使用 [!DNL Schema Registry] API，請參閱 [欄位群組端點指南](../../api/field-groups.md).
