---
keywords: Experience Platform；使用者介面；UI；控制面板；控制面板；設定檔；區段；目的地；授權使用
title: 控制面板Widget程式庫概述
description: 本指南提供存取Adobe Experience Platform中Widget資料庫的逐步指示。
exl-id: 1d33e3ea-a8a8-4a09-8bd9-2e04ecedebdc
source-git-commit: 09f212741321f17372d52fee507a96d2d2834e85
workflow-type: tm+mt
source-wordcount: '516'
ht-degree: 0%

---

# 介面工具集程式庫概觀

在Adobe Experience Platform使用者介面中，您可以使用多個控制面板來檢視及與組織的資料互動。 您也可以將介面工具集新增至控制面板檢視，以更新特定控制面板。

本指南提供存取 [!UICONTROL 介面工具集程式庫] Experience Platform內，您可以在其中選取標準介面工具集並建立自訂介面工具集，以自訂控制面板中顯示的資訊。

有關如何修改控制面板中已顯示的介面工具集的位置和大小的資訊，請參閱 [修改控制面板指南](modify.md).

>[!NOTE]
>
>顯示於 [!UICONTROL 授權使用] 無法自訂控制面板。 若要深入了解此不重複控制面板，請閱讀 [授權使用控制面板檔案](../guides/license-usage.md).

## 存取介面工具集程式庫 {#access}

從任何控制面板（例如，設定檔控制面板）中，選取 **[!UICONTROL 新增介面工具集]** 若要直接導覽至介面工具集資料庫，您可在此 [新增介面工具集](#add-widgets) 到控制面板。

![「配置檔案」儀表板概述頁簽，其中突出顯示了「添加介面工具集」按鈕。](../images/customization/profiles-overview-add-widget.png)

選擇 **[!UICONTROL 修改控制面板]** 從控制面板移動、調整大小或移除小工具。 您也可以從此顯示中選取 **[!UICONTROL 介面工具集程式庫]** 瀏覽和 [新增介面工具集](#add-widgets). 若要了解如何編輯介面工具集的大小和版面，請參閱 [修改控制面板檔案](./modify.md).

![「設定檔」控制面板概觀，並反白顯示「修改」控制面板。](../images/customization/modify-dashboard.png)

選擇 **[!UICONTROL 介面工具集程式庫]** 若要開啟介面工具集庫並檢視所有可用的標準量度，或開始建立自訂介面工具集。

![修改控制面板檢視，並反白顯示Widget程式庫。](../images/customization/widget-library-button.png)

## 新增介面工具集 {#add-widgets}

從 [!UICONTROL 介面工具集程式庫]，請從可用標準或自訂介面工具集清單中選取任何介面工具集。 介面工具集角落處的勾號表示您的選取項目。

![包含選定介面工具集的介面工具集庫，並突出顯示複選標籤。](../images/customization/confirm-selected-widget-to-add.png)

### 使用中標籤 {#in-use-label}

已添加到控制面板的介面工具集 [!UICONTROL 使用中] 在介面工具集資料庫中檢視時附加的標籤。 此標籤會反白標示已新增至控制面板的Widget，以避免重複。 不過，您仍可以多次新增相同的Widget（視需要而定）。

![醒目提示使用中標籤的介面工具集程式庫。](../images/customization/in-use-label.png)

選取所有必要小工具後，請選取 **[!UICONTROL 新增介面工具集]** 確認您的選擇，並將介面工具集新增至控制面板。

## 標準和自訂Widget {#standard-and-custom}

此 [!UICONTROL 介面工具集程式庫] 包含兩個索引標籤：

* **[!UICONTROL 標準]:** 標準標籤包含由Adobe提供的小工具。 您可以使用任何這些標準量度來更新控制面板。 若要進一步了解如何將標準Widget新增至控制面板，請參閱指南 [在控制面板中使用標準介面工具](standard-widgets.md).
* **[!UICONTROL 自訂]:** 自訂索引標籤可讓您在組織內建立和共用Widget。 有關建立自己的小部件的完整步驟，請參閱 [控制面板的自訂小工具指南](custom-widgets.md).

![強調顯示標準和自訂標籤的介面工具集庫。](../images/customization/widget-library.png)

## 後續步驟

閱讀本檔案後，您現在可以在Experience PlatformUI中存取介面工具集程式庫。 要修改儀表板中顯示的小部件的大小和位置，請參閱 [修改控制面板指南](modify.md).
