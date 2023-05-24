---
keywords: Experience Platform；用戶介面；UI；儀表板；儀表板；配置檔案；段；目標
title: 儀表板自定義概述
description: 瞭解有關自定義在Adobe Experience Platform儀表板中顯示的資料的方法的更多資訊。
exl-id: efabdb61-4148-4b0e-b7a1-6e788b5e43a8
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '480'
ht-degree: 0%

---

# 儀表板自定義概述

可以通過多種不同方式自定義Adobe Experience Platform內可用的配置式、段和目標儀表板。 本指南概述了可用的自定義設定，並提供了指向逐步說明的連結，指導您瞭解如何個性化儀表板中顯示哪些小部件以及這些小部件的大小、形狀和位置。

>[!NOTE]
>
>中顯示的小部件 [!UICONTROL 許可證使用] 無法自定義儀表板。 要瞭解有關此唯一儀表板的詳細資訊，請閱讀 [許可證使用儀表板文檔](../guides/license-usage.md)。

## 修改儀表板

選擇 **[!UICONTROL 修改儀表板]** 通過配置檔案、段或目標面板，您可以調整儀表板中當前可見的小部件的大小、順序和位置。 有關如何修改儀表板中小部件外觀的資訊，請參閱 [修改儀表板指南](modify.md)。

## 構件庫

Experience Platform中的小部件庫可在其中查看 [標準](#standard-widgets) 和 [自定義](#custom-widgets) 可用於您組織的小部件。 從儀表板（例如，配置式儀表板）中，可以選擇 **[!UICONTROL 修改儀表板]** 以便顯示 **[!UICONTROL 小部件庫]** 按鈕

![加亮顯示「修改」操控板的「配置檔案」操控板。](../images/customization/modify-dashboard.png)

選擇 **[!UICONTROL 小部件庫]** 開啟小部件庫並查看所有可用的標準度量，或開始建立自定義小部件。

![突出顯示了「配置式」面板，其中顯示了「構件」庫。](../images/customization/widget-library-button.png)

### 標準小部件 {#standard-widgets}

標準小部件指Adobe提供的小部件，可在儀表板中使用。 這些小部件是只讀的，不能由您的組織編輯。

在小部件庫中， **[!UICONTROL 標準]** 頁籤包含Adobe提供的所有可用標準小部件。 您可以使用這些標準度量中的任何一個更新儀表板。 要瞭解有關將標準小部件添加到儀表板的詳細資訊，請參閱指南 [使用儀表板中的標準小部件](standard-widgets.md)。

### 自定義小部件 {#custom-widgets}

自定義小部件是指由您組織的成員建立和共用的小部件。 通過 **[!UICONTROL 自定義]** 頁籤，並要求您的組織通過使用 [架構](#edit-schema)

有關建立自己小部件的完整步驟，請參閱 [《儀表板自定義小部件指南》](custom-widgets.md)。

![突出顯示了「標準」和「自定義」的小部件庫工作區。](../images/customization/widget-library.png)

#### 編輯方案 {#edit-schema}

為了建立 [自定義小部件](#custom-widgets) 對於您的儀表板，您必須首先確定構件所基於的「即時客戶配置檔案」屬性。

有關編輯組織架構以建立自定義儀表板小部件的逐步說明，請訪問指南，以 [編輯儀表板架構](edit-schema.md)。

## 後續步驟

閱讀此文檔後，您就可以開始自定義Experience Platform儀表板，方法是修改現有小部件的大小、形狀和順序、添加Adobe提供的標準小部件，或建立自定義小部件並與您的組織共用。
