---
keywords: Experience Platform；使用者介面；UI；儀表板；儀表板；設定檔；區段；目的地
title: 儀表板自訂概觀
description: 進一步瞭解如何自訂Adobe Experience Platform儀表板中顯示的資料。
exl-id: efabdb61-4148-4b0e-b7a1-6e788b5e43a8
source-git-commit: 32dd90018c990e7013d826b29608a61022ba808b
workflow-type: tm+mt
source-wordcount: '468'
ht-degree: 0%

---

# 儀表板自訂概觀

Adobe Experience Platform中可用的設定檔、區段和目的地儀表板可以透過多種不同方式自訂。 本指南提供可用自訂的概觀，其中連結至逐步指示，引導您瞭解如何個人化控制面板中顯示的介面工具集，以及這些介面工具集的大小、形狀和位置。

>[!NOTE]
>
>控制面板的任何更新都是根據組織和沙箱進行。

## 修改儀表板

選取 **[!UICONTROL 修改儀表板]** 您可從「設定檔」、「區段」或「目的地」儀表板調整目前顯示在儀表板中Widget的大小、順序和位置。 如需如何修改控制面板中Widget外觀的詳細資訊，請參閱 [修改儀表板指南](modify.md).

## Widget資料庫

Experience Platform內的Widget程式庫可讓您檢視所有 [標準](#standard-widgets) 和 [自訂](#custom-widgets) 您的組織可使用Widget。 從您的控制面板（例如設定檔控制面板），您可以選取 **[!UICONTROL 修改儀表板]** 以顯示 **[!UICONTROL Widget資料庫]** 按鈕。

![會反白顯示「修改」儀表板的「設定檔」儀表板。](../images/customization/modify-dashboard.png)

選取 **[!UICONTROL Widget資料庫]** 開啟Widget資料庫並檢視所有可用的標準量度，或開始建立自訂Widget。

![強調顯示Widget資料庫的「設定檔」控制面板。](../images/customization/widget-library-button.png)

### 標準Widget {#standard-widgets}

標準Widget是指Adobe提供用於儀表板的Widget。 這些Widget是唯讀的，您的組織無法編輯。

在Widget程式庫中， **[!UICONTROL 標準]** 索引標籤包含Adobe提供的所有可用標準Widget。 您可以使用任一標準量度來更新您的儀表板。 若要進一步瞭解如何新增標準Widget至您的儀表板，請參閱以下指南： [在儀表板中使用標準Widget](standard-widgets.md).

### 自訂Widget {#custom-widgets}

自訂Widget是指由您組織的成員建立和共用的Widget。 這些Widget是透過 **[!UICONTROL 自訂]** 標籤，並要求您的組織透過使用 [綱要](#edit-schema)

如需建立您自己的Widget的完整步驟，請參閱 [控制面板的自訂Widget指南](custom-widgets.md).

![Widget程式庫工作區中的「標準」和「自訂」會反白顯示。](../images/customization/widget-library.png)

#### 編輯方案 {#edit-schema}

為了建立 [自訂Widget](#custom-widgets) 若要使用儀表板，您必須先識別Widget所根據的「即時客戶設定檔」屬性。

如需編輯您組織結構以建立自訂儀表板Widget的逐步指示，請造訪指南 [編輯您的儀表板結構](edit-schema.md).

## 後續步驟

閱讀本檔案後，您就可以開始自訂Experience Platform儀表板，透過修改現有Widget的大小、形狀和順序、新增Adobe提供的標準Widget，或建立自訂Widget並與您的組織共用。
