---
keywords: Experience Platform；使用者介面；UI；控制面板；設定檔；區段；目的地
title: 控制面板自訂概述
description: 進一步了解您可以如何自訂Adobe Experience Platform控制面板中顯示的資料。
exl-id: efabdb61-4148-4b0e-b7a1-6e788b5e43a8
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '480'
ht-degree: 0%

---

# 控制面板自訂概觀

Adobe Experience Platform中可用的設定檔、區段和目的地控制面板，可透過多種不同方式加以自訂。 本指南提供可用自訂項目的概觀，其中包含逐步指示的連結，引導您逐步了解如何個人化控制面板中顯示的介面工具集，以及這些介面工具集的大小、形狀和位置。

>[!NOTE]
>
>顯示於 [!UICONTROL 授權使用] 無法自訂控制面板。 若要深入了解此不重複控制面板，請閱讀 [授權使用控制面板檔案](../guides/license-usage.md).

## 修改控制面板

選取 **[!UICONTROL 修改控制面板]** 透過「設定檔」、「區段」或「目的地」控制面板，您可以調整控制面板中目前可見的介面工具集的大小、順序和位置。 有關如何修改控制面板中小部件外觀的資訊，請參閱 [修改控制面板指南](modify.md).

## 介面工具集程式庫

Experience Platform中的介面工具集程式庫可讓您檢視 [標準](#standard-widgets) 和 [自訂](#custom-widgets) 可供您的組織使用的小工具集。 在控制面板（例如，設定檔控制面板）中，您可以選取 **[!UICONTROL 修改控制面板]** 來顯示 **[!UICONTROL 介面工具集程式庫]** 按鈕。

![突出顯示帶有「修改」(Modify)控制面板的「配置檔案」(Profiles)控制面板。](../images/customization/modify-dashboard.png)

選擇 **[!UICONTROL 介面工具集程式庫]** 若要開啟介面工具集庫並檢視所有可用的標準量度，或開始建立自訂介面工具集。

![「設定檔」控制面板會反白顯示Widget資料庫。](../images/customization/widget-library-button.png)

### 標準介面工具集 {#standard-widgets}

標準介面工具集是指Adobe提供的介面工具集，以便在控制面板中使用。 這些小工具集是唯讀的，您的組織無法編輯。

在介面工具集程式庫內， **[!UICONTROL 標準]** 索引標籤包含Adobe提供的所有可用標準介面工具集。 您可以使用任何這些標準量度來更新控制面板。 若要進一步了解如何將標準Widget新增至控制面板，請參閱指南 [在控制面板中使用標準介面工具](standard-widgets.md).

### 自訂小工具 {#custom-widgets}

自訂小工具是指由組織成員建立和共用的小工具。 這些小工具會透過 **[!UICONTROL 自訂]** 標籤，並要求您的組織透過使用 [綱要](#edit-schema)

有關建立自己的小部件的完整步驟，請參閱 [控制面板的自訂小工具指南](custom-widgets.md).

![反白顯示「標準」和「自訂」的Widget程式庫工作區。](../images/customization/widget-library.png)

#### 編輯方案 {#edit-schema}

若要建立 [自訂介面工具集](#custom-widgets) 針對您的控制面板，您必須先識別介面工具集所依據的即時客戶設定檔屬性。

如需編輯組織結構以建立自訂控制面板小工具的逐步指示，請參閱指南，以取得 [編輯控制面板架構](edit-schema.md).

## 後續步驟

閱讀本檔案後，您就可以開始自訂Experience Platform控制面板，方法是修改現有小工具的大小、形狀和順序、新增Adobe提供的標準小工具，或建立自訂小工具並與組織共用。
