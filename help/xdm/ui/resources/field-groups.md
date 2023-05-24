---
keywords: Experience Platform；首頁；熱門主題；api;API;XDM;XDM系統；經驗資料模型；資料模型；ui;workspace;field group；欄位組；
solution: Experience Platform
title: 在UI中建立和編輯架構欄位組
description: 瞭解如何在Experience Platform用戶介面中建立和編輯架構欄位組。
exl-id: 928d70a6-0468-4fb7-a53a-6686ac77f2a3
source-git-commit: 542ad49f475ac9586da506a8afa5408e83262121
workflow-type: tm+mt
source-wordcount: '839'
ht-degree: 0%

---

# 在UI中建立和編輯架構欄位組

在經驗資料模型(XDM)中，架構欄位組是可重用的元件，它們定義了一個或多個欄位，這些欄位實現了某些功能，如個人詳細資訊、酒店首選項或地址。 欄位組將作為實現相容類的架構的一部分被包括。

欄位組基於欄位組所表示的資料的行為（記錄或時間序列）來定義與哪些類相容。 這意味著並非所有欄位組都可用於所有類。

Adobe Experience Platform提供許多標準的現場小組，涵蓋各種營銷使用案例。 但是，您也可以建立和編輯自己的自定義欄位組，以定義與XDM架構中的業務相關的附加概念。 本指南概述了如何在平台UI中建立、編輯和管理組織的自定義欄位組。

## 先決條件

本指南要求對XDM系統有正確的瞭解。 請參閱 [XDM概述](../../home.md) 介紹XDM在Experience Platform生態系統中的作用， [架構組合基礎](../../schema/composition.md) 欄位組如何貢獻XDM架構。

雖然本指南不是必需的，但建議您也學習上的教程 [在UI中合成架構](../../tutorials/create-schema-ui.md) 熟悉 [!DNL Schema Editor]。

## 建立新欄位組 {#create}

要建立新欄位組，必須首先選擇將添加該欄位組的架構。 您可以選擇 [建立新架構](./schemas.md#create) 或 [選擇要編輯的現有架構](./schemas.md#edit)。

在中開啟架構後 [!DNL Schema Editor]選中 **[!UICONTROL 添加]** 的 [!UICONTROL 欄位組] 在左欄上。

![](../../images/ui/resources/field-groups/add-field-group.png)

在顯示的對話框中，選擇 **[!UICONTROL 建立新欄位組]**。 在這裡，您可以提供 **[!UICONTROL 顯示名稱]** 和 **[!UICONTROL 說明]** 欄位組。 完成後，選擇 **[!UICONTROL 添加欄位組]**。

![](../../images/ui/resources/field-groups/create-field-group.png)

的 [!DNL Schema Editor] 重新顯示，新欄位組列在左滑軌中。 由於這是全新的欄位組，因此它當前不向架構提供任何欄位，因此畫布保持不變。 現在可以開始 [將欄位添加到欄位組](#add-fields)。

![](../../images/ui/resources/field-groups/field-group-added.png)

## 編輯現有欄位組 {#edit}

>[!NOTE]
>
>只有組織定義的自定義欄位組才能完全編輯和自定義。 對於由Adobe定義的核心欄位組，只能在單個方案的上下文中編輯其欄位的顯示名稱。 請參閱 [編輯架構欄位的顯示名稱](./schemas.md#display-names) 的雙曲餘切值。
>
>一旦在模式中保存並使用了自定義欄位組以進行資料接收，此後只能對欄位組進行附加更改。 查看 [模式演化規則](../../schema/composition.md#evolution) 的子菜單。

要編輯現有欄位組，必須先開啟一個在 [!DNL Schema Editor]。 你可以 [選擇要編輯的現有架構](./schemas.md#edit)或 [建立新架構](./schemas.md#create) 並添加該欄位組。

在編輯器中開啟架構後，可以啟動 [將欄位添加到欄位組](#add-fields)。

## 將欄位添加到欄位組 {#add-fields}

>[!NOTE]
>
>本節重點介紹將欄位添加到自定義欄位組。 有關如何將自定義欄位添加到標準欄位組的資訊，請參閱 [架構UI指南](./schemas.md#custom-fields-for-standard-groups)。

要向自定義欄位組添加欄位，請首先選擇 **加(+)** 表徵圖，位於畫布中架構名稱旁邊。

![](../../images/ui/resources/field-groups/add-field.png)

安 **[!UICONTROL 無標題欄位]** 佔位符顯示在畫布中，右滑軌將更新以顯示用於配置欄位屬性的控制項。 請參閱上的指南 [定義UI中的欄位](../fields/overview.md#define) 有關如何配置不同欄位類型的特定步驟。

下 **[!UICONTROL 分配給]**，選擇 **[!UICONTROL 欄位組]** 選項，然後使用下拉清單從清單中選擇所需的欄位組。 可以開始鍵入欄位組的名稱以縮小結果範圍。

![](../../images/ui/resources/field-groups/select-field-group.png)

下 **[!UICONTROL 分配給]**，選擇 **[!UICONTROL 欄位組]** 選項，然後使用下拉清單從清單中選擇所需的欄位組。 可以開始鍵入欄位組的名稱以縮小結果範圍。

![](../../images/ui/resources/field-groups/select-field-group.png)

將欄位添加到架構後，將其分配給選定的欄位組。 繼續向欄位組添加所需的任意多個欄位。 完成後，選擇 **[!UICONTROL 保存]** 保存架構和欄位組。

![](../../images/ui/resources/field-groups/complete-field-group.png)

如果其他方案中已使用同一欄位組，則新添加的欄位將自動顯示在這些方案中。

## 後續步驟

本指南介紹了如何使用平台UI建立和編輯欄位組。 有關功能的詳細資訊 [!UICONTROL 架構] 工作區，請參閱 [[!UICONTROL 架構] 工作區概述](../overview.md)。

瞭解如何使用 [!DNL Schema Registry] API，請參見 [欄位組終結點指南](../../api/field-groups.md)。
