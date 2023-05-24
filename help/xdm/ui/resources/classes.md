---
keywords: Experience Platform；首頁；熱門主題；api;API;XDM;XDM系統；經驗資料模型；資料模型；ui;workspace;class;class;
solution: Experience Platform
title: 在UI中建立和編輯類
description: 瞭解如何在Experience Platform用戶介面中建立和編輯類。
exl-id: 1b4c3996-2319-45dd-9edd-a5bcad46578b
source-git-commit: 3a9b97b25980d88e0fff3d71e43407b641e6454d
workflow-type: tm+mt
source-wordcount: '902'
ht-degree: 0%

---

# 在UI中建立和編輯類

在Adobe Experience Platform，架構的類定義架構將包含的資料的行為方面（記錄或時間序列）。 此外，類還描述了基於該類的所有方案需要包括的最小數量的公共屬性，並為合併多個相容資料集提供了一種方法。

Adobe提供多個標準（「核心」）體驗資料模型(XDM)類，包括 [!DNL XDM Individual Profile] 和 [!DNL XDM ExperienceEvent]。 除了這些核心類之外，您還可以建立自己的自定義類，以說明組織的更具體的使用案例。

本文檔概述了如何在Experience PlatformUI中建立、編輯和管理自定義類。

## 先決條件

本指南要求對XDM系統有正確的瞭解。 請參閱 [XDM概述](../../home.md) 介紹XDM在Experience Platform生態系統中的作用， [架構組合基礎](../../schema/composition.md) 瞭解類如何對XDM架構作出貢獻。

雖然本指南不是必需的，但建議您也學習上的教程 [在UI中合成架構](../../tutorials/create-schema-ui.md) 熟悉 [!DNL Schema Editor]。

## 建立新類 {#create}

在 **[!UICONTROL 架構]** 工作區，選擇 **[!UICONTROL 建立架構]**，然後選擇 **[!UICONTROL 瀏覽]** 的下界。

![](../../images/ui/resources/classes/browse-classes.png)

將顯示一個對話框，允許您從可用類清單中進行選擇。 在對話框頂部，選擇 **[!UICONTROL 建立新類]**。 然後，您可以為新類提供顯示名稱（類的簡短、描述性、唯一性和用戶友好名稱）、說明以及方案將定義的資料的行為(**[!UICONTROL 記錄]** 或 **[!UICONTROL 時間序列]**)。

完成後，選擇 **[!UICONTROL 分配類]**。

![](../../images/ui/resources/classes/class-details.png)

的 [!DNL Schema Editor] 顯示，在畫布中顯示基於剛建立的自定義類的新架構。 由於尚未將欄位添加到類，因此架構僅包含 `_id` 欄位，表示系統生成的唯一標識符，該標識符自動應用於 [!DNL Schema Registry]。

![](../../images/ui/resources/classes/schema.png)

>[!IMPORTANT]
>
>構建實現由您的組織定義的類的架構時，請記住，架構欄位組僅可用於相容類。 由於您定義的類是新的，因此在 **[!UICONTROL 添加欄位組]** 對話框。 相反，你需要 [新建欄位組](./field-groups.md#create) 用在那門課上。 下次構建實現新類的方案時，將列出您定義的欄位組並可供使用。

現在可以開始 [將欄位添加到類](#add-fields)，將由使用類的所有架構共用。

## 編輯現有類 {#edit}

>[!NOTE]
>
>只有組織定義的自定義類才能完全編輯和自定義。 對於由Adobe定義的核心類，只能在單個方案的上下文中編輯其欄位的顯示名稱。 請參閱 [編輯架構欄位的顯示名稱](./schemas.md#display-names) 的雙曲餘切值。
>
>自定義類一旦保存並用於資料接收，以後只能對其進行附加更改。 查看 [模式演化規則](../../schema/composition.md#evolution) 的子菜單。

要編輯現有類，請選擇 **[!UICONTROL 瀏覽]** 頁籤，然後選擇使用要編輯的類的架構的名稱。

![](../../images/ui/resources/classes/select-for-edit.png)

>[!TIP]
>
>可以使用工作區的搜索和篩選功能幫助更輕鬆地查找架構。 請參閱上的指南 [探索XDM資源](../explore.md) 的子菜單。

的 [!DNL Schema Editor] 顯示，其中在畫布中顯示架構的結構。 現在可以開始 [將欄位添加到類](#add-fields)。

![](../../images/ui/resources/classes/edit.png)

## 將欄位添加到類 {#add-fields}

一旦您的架構使用在 [!UICONTROL 架構編輯器]，可開始向類添加欄位。 要添加新欄位，請選擇 **加(+)** 表徵圖。

![](../../images/ui/resources/classes/add-field.png)

>[!IMPORTANT]
>
>請記住，添加到類的任何欄位都將用於使用該類的所有架構。 因此，您應仔細考慮哪些欄位在所有架構使用情形中都有用。 如果您正考慮添加一個欄位，該欄位可能只能看到此類下的某些架構中的使用，則您可能希望考慮通過以下方式將其添加到這些架構中 [建立欄位組](./field-groups.md#create) 的雙曲餘切值。

安 **[!UICONTROL 無標題欄位]** 佔位符顯示在畫布中，右滑軌將更新以顯示用於配置欄位屬性的控制項。 下 **[!UICONTROL 分配給]**&#x200B;選中 **[!UICONTROL 類]**。

![](../../images/ui/resources/classes/assign-to-class.png)

![](../../images/ui/resources/classes/assign-to-class.png)

請參閱上的指南 [定義UI中的欄位](../fields/overview.md#define) 有關如何配置欄位並將其添加到類的特定步驟。 繼續向類添加所需的任意多個欄位。 完成後，選擇 **[!UICONTROL 保存]** 來保存架構和類。

![](../../images/ui/resources/classes/save.png)

如果您以前建立過使用此類的方案，則新添加的欄位將自動顯示在這些方案中。

## 更改架構的類 {#schema}

在初始建立過程中，在保存架構之前，可以在任何時間點更改該架構的類。 請參閱上的指南 [建立和編輯架構](./schemas.md#change-class) 的子菜單。

## 後續步驟

本文檔介紹了如何使用平台UI建立和編輯類。 有關功能的詳細資訊 [!UICONTROL 架構] 工作區，請參閱 [[!UICONTROL 架構] 工作區概述](../overview.md)。

瞭解如何使用 [!DNL Schema Registry] API，請參見 [類終結點指南](../../api/classes.md)。
