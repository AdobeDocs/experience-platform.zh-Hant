---
title: 使用者定義的控制面板
description: 了解如何建立和管理自訂控制面板，以便建立、新增和編輯自訂小工具，以視覺化關鍵量度。
exl-id: a9ab83f7-b68d-4dbf-9dc6-ef253df5c82c
source-git-commit: a0be2f8625ca60f9c8f355c1230a889002436d6d
workflow-type: tm+mt
source-wordcount: '1307'
ht-degree: 4%

---

# 使用者定義的控制面板

Adobe Experience Platform控制面板可協助您透過使用者定義的控制面板功能，加速深入分析和自訂視覺效果。 此功能可讓您建立和管理自訂控制面板，在其中建立、新增及編輯定制小工具，以視覺化與貴組織相關的關鍵量度。

<!-- Getting started / permissions section commented out for Beta. This will be necessary after GA only

## Getting started

To view dashboards in Adobe Experience Platform you must have the appropriate permissions enabled. Please read the [dashboards permissions documentation](./permissions.md#available-permissions) to learn how to grant users the ability to view, edit, and update Experience Platform dashboards using Adobe Admin Console. If you do not have administrator privileges for your organization, contact your product administrator to obtain the required permissions. -->

## 建立自訂控制面板

若要建立自訂控制面板，請先導覽至控制面板詳細目錄。 選擇 **[!UICONTROL 控制面板]** 從Platform UI的左側導覽，接著 **[!UICONTROL 建立控制面板]**.

![左側導覽中顯示控制面板的控制面板清單，並反白顯示「建立控制面板」。](./images/user-defined-dashboards/create-dashboard.png)

新增自訂控制面板前，控制面板清單為空，並顯示「找不到控制面板」。 訊息。 建立後，所有使用者定義的控制面板都會列在控制面板清單中。

>[!NOTE]
>
>若要編輯現有的控制面板，請從清單中選取控制面板名稱，後接鉛筆圖示(![鉛筆圖示。](./images/user-defined-dashboards/edit-icon.png))

此 [!UICONTROL 建立控制面板] 對話框。 為要建立的小部件集合輸入易記的描述性名稱，然後選擇 **[!UICONTROL 儲存]**.

![建立控制面板對話方塊。](./images/user-defined-dashboards/create-dashboard-dialog.png)

新建立的空白控制面板會以您選擇的名稱顯示在檢視的左上角。

## 建立介面工具集 {#create-widget}

>[!CONTEXTUALHELP]
>id="platform_dashboards_udd_maxwidgets"
>title="Widget 的最大數量"
>abstract="使用者定義的儀表板最多支援十個 Widget。將十個 Widget 新增到儀表板後，[!UICONTROL 新增 Widget] 選項會停用並顯示為灰色。"

在新控制面板檢視中，選取 **[!UICONTROL 新增介面工具集]** 以開始介面工具集建立程式。

>[!IMPORTANT]
>
>使用者定義的儀表板最多支援十個 Widget。將十個 Widget 新增到儀表板後，[!UICONTROL 新增 Widget] 選項會停用並顯示為灰色。

![反白顯示「新增介面工具集」的新空白控制面板。](./images/user-defined-dashboards/add-new-widget.png)

### 介面工具集撰寫器

介面工具集撰寫器工作區隨即出現。 下一步，選擇 **[!UICONTROL 選擇資料]** 選擇要從中向Widget添加屬性的資料模型。

![介面工具集撰寫器工作區。](./images/user-defined-dashboards/widget-composer.png)

#### 選取資料模型 {#select-data-model}

此 [!UICONTROL 選取資料模型] 對話框。 從左欄選取資料模型，以顯示所有可用表格的預覽清單。 預先設定的Real-time Customer Data Platform資料模型名為 [!UICONTROL CDPInsights].

>[!TIP]
>
>選取資訊圖示(![資訊圖示。](./images/user-defined-dashboards/info-icon.png))，查看完整資料模型名稱（如果太長無法顯示在資料欄中）。

![選擇資料對話框。](./images/user-defined-dashboards/select-data-model-dialog.png)

預覽清單提供資料模型中所含表格的詳細資訊。 下表提供欄欄位及其潛在值的說明。

| 欄欄位 | 說明 |
|---|---|
| [!UICONTROL 標題] | 表的名稱。 |
| [!UICONTROL 表格類型] | 表的類型。 可能的類型包括： `fact`, `dimension`，和 `none`. |
| [!UICONTROL 記錄] | 與所選表關聯的記錄數。 |
| [!UICONTROL 查閱] | 連接到所選表的表數。 |
| [!UICONTROL 屬性] | 所選表的屬性數。 |

選擇 **[!UICONTROL 下一個]** 確認您選擇資料模型。 下一個檢視會在左側邊欄中顯示可用表格的清單。 選取表格，即可查看所選表格中所包含資料的完整劃分。

### 填入介面工具集 {#populate-widget}

此 [!UICONTROL 預覽] 面板包含標籤 [!UICONTROL 記錄範例] 和 [!UICONTROL 屬性]. 此 [!UICONTROL 記錄範例] 頁簽提供清單視圖中選定表中記錄的子集。 此 [!UICONTROL 屬性] 頁簽為與選定表關聯的每個屬性提供屬性名稱、資料類型和源表。

從左側邊欄的可用清單中選取表格，以提供介面工具集的資料，然後選取 **[!UICONTROL 選擇]** 返回介面工具集撰寫器。

![選取資料對話方塊，並反白顯示選取項目。](./images/user-defined-dashboards/select-a-table.png)

介面工具集撰寫器現在會填入您所選表格的資料。

資料模型和目前選取的表格會顯示在左側邊欄的上方，而可用於建立介面工具集的屬性會列在 [!UICONTROL 屬性] 欄。 您可以使用搜尋列來尋找屬性，而非捲動清單，或選取鉛筆圖示來變更選取的資料模型(![鉛筆圖示。](./images/user-defined-dashboards/edit-icon.png))。

![在介面工具集撰寫器中填入資料的介面工具集。](./images/user-defined-dashboards/populated-widget-composer.png)

#### 新增及篩選屬性 {#add-and-filter-attributes}

選取新增圖示(![新增圖示。](./images/user-defined-dashboards/add-icon.png))，以新增屬性至您的介面工具集。 顯示的下拉式選單可讓您將屬性新增為X軸、Y軸、顏色或Widget的篩選器。 此 [!UICONTROL 顏色] 屬性可讓您根據顏色來區分X和Y軸標籤的結果。 它會根據結果在第三個屬性中的構成，將結果分割為不同的顏色來達成此目的。

>[!TIP]
>
>如果要反轉X和Y軸的排列，請選取向上和向下箭頭表徵圖(![向上和向下箭頭表徵圖。](./images/user-defined-dashboards/switch-axis-icon.png))來切換其排列。

![介面工具集撰寫器，其中加亮顯示「新增圖示」下拉式清單。](./images/user-defined-dashboards/attributes-dropdown.png)

若要變更介面工具集的圖形或圖表類型，請選取 [!UICONTROL 標籤] 下拉式清單，然後從可用選項中選擇。 選項包括長條、點、刻度、線或區域。 選取後，會產生介面工具集目前設定的預覽視覺效果。

![以「標籤」下拉式清單反白顯示介面工具集撰寫器。](./images/user-defined-dashboards/marks-dropdown.png)

借由新增屬性作為篩選器，您可以選取要在介面工具集中包含或排除的值。 從屬性清單新增篩選器後， [!UICONTROL 篩選] 對話方塊隨即出現，您可以在其中使用其核取方塊選取或取消選取值。

![篩選對話方塊，用於從介面工具集篩選值。](./images/user-defined-dashboards/filter-dialog.png)

### 介面工具集屬性

選取屬性圖示(![屬性圖示。](./images/user-defined-dashboards/properties-icon.png))以開啟「屬性」面板。 在 [!UICONTROL 屬性] 面板中，在 [!UICONTROL 介面工具集標題] 文字欄位。

![屬性面板中顯示屬性圖示，並反白顯示Widget標題欄位。](./images/user-defined-dashboards/properties-panel.png)

從介面工具集屬性面板，您可以編輯介面工具集的多個方面。 您可以完全控制編輯介面工具集圖例的位置。 若要移動圖例，請選取 [!UICONTROL 圖例放置] 下拉式清單中，從可用選項清單中選擇您想要的位置。 您也可以在 [!UICONTROL 圖例標題] 文字欄位，或 [!UICONTROL 軸標籤] 文字欄位。

#### 儲存介面工具集 {#save-widget}

在介面工具集撰寫器中儲存時，會將介面工具集儲存在本機至您的控制面板。 如果您希望保存工作並稍後繼續，請選擇 **[!UICONTROL 儲存]**. 介面工具集名稱下方的勾選圖示表示該介面工具集已儲存。 或者，當您對介面工具集滿意時，請選取 **[!UICONTROL 儲存並關閉]** 讓具有控制面板存取權限的所有其他使用者都能使用該介面工具集。 選擇 **[!UICONTROL 取消]** 放棄工作並返回自訂控制面板。

![新介面工具集儲存確認。](./images/user-defined-dashboards/save-confirmation.png)

>[!TIP]
>
>選取屬性圖示(![屬性圖示。](./images/user-defined-dashboards/properties-icon.png))，以查看其建立的詳細資訊。 您可以在顯示的對話方塊中變更控制面板的名稱。

在此工作區中，可以重新排列小部件並調整其大小。 選擇 **[!UICONTROL 儲存]** 以保留控制面板名稱和設定的配置。

![使用自訂介面工具集的使用者定義控制面板，並反白顯示「儲存」按鈕。](./images/user-defined-dashboards/user-defined-dashboard.png)

為確保Adobe Real-time Customer Data Platform深入分析控制面板的每個查詢都有足夠的資源來有效執行，API會為每個查詢指派並行槽來追蹤資源使用情形。 該系統最多可處理四個併發查詢，因此，在任何給定時間都有四個併發查詢槽可用。 根據併發槽將查詢放入隊列，然後在隊列中等待，直到有足夠的併發槽可用。

## 後續步驟和其他資源

閱讀本檔案後，您就更能了解如何建立自訂控制面板，以及如何為該控制面板建立、編輯和更新自訂小工具。

若要探索 [設定檔](./guides/profiles.md#standard-widgets), [區段](./guides/segments.md#standard-widgets)，和 [目的地](./guides/destinations.md#standard-widgets) 控制面板，請參閱其個別檔案中的標準Widget清單。

若要加深您對Experience Platform中使用者定義控制面板的了解，請觀看下列影片：

>[!VIDEO](https://video.tv.adobe.com/v/3409637?quality=12&learn=on)
