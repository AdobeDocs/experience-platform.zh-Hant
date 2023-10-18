---
title: 使用者定義儀表板
description: 瞭解如何建立及管理自訂儀表板，以便在其中建立、新增和編輯客製化Widget，將關鍵量度視覺化。
exl-id: a9ab83f7-b68d-4dbf-9dc6-ef253df5c82c
source-git-commit: b3bd7a5ba1847518beafd12240c0d3a433a891d0
workflow-type: tm+mt
source-wordcount: '1608'
ht-degree: 3%

---

# 使用者定義的儀表板

Adobe Experience Platform儀表板可協助您透過使用者定義的儀表板功能，快速獲得見解並自訂視覺效果。 此功能可讓您建立和管理自訂儀表板，以便在其中建立、新增和編輯自訂Widget，以視覺化方式呈現與貴組織相關的關鍵量度。

<!-- Getting started / permissions section commented out for Beta. This will be necessary after GA only

## Getting started

To view dashboards in Adobe Experience Platform you must have the appropriate permissions enabled. Please read the [dashboards permissions documentation](./permissions.md#available-permissions) to learn how to grant users the ability to view, edit, and update Experience Platform dashboards using Adobe Admin Console. If you do not have administrator privileges for your organization, contact your product administrator to obtain the required permissions. -->

## 建立自訂儀表板

若要建立自訂儀表板，請先導覽至儀表板詳細目錄。 選取 **[!UICONTROL 儀表板]** 從Platform UI的左側導覽，接著是 **[!UICONTROL 建立儀表板]**.

![在左側導覽中顯示儀表板的儀表板詳細目錄，並反白顯示「建立儀表板」。](./images/user-defined-dashboards/create-dashboard.png)

在新增自訂儀表板之前，儀表板庫存是空的，並顯示「找不到儀表板」。 訊息。 建立後，您的所有使用者定義控制面板都會列在控制面板詳細目錄中。

>[!NOTE]
>
>若要編輯現有儀表板，請從詳細目錄清單中選取儀表板名稱，然後選取鉛筆圖示(![鉛筆圖示。](./images/user-defined-dashboards/edit-icon.png))

此 [!UICONTROL 建立儀表板] 對話方塊隨即顯示。 為您要建立的Widget集合輸入人性化的描述性名稱，然後選取 **[!UICONTROL 儲存]**.

![「建立儀表板」對話方塊。](./images/user-defined-dashboards/create-dashboard-dialog.png)

新建立的空白圖示板會出現，而您選擇的名稱會顯示在檢視的左上角。

## 建立Widget {#create-widget}

>[!CONTEXTUALHELP]
>id="platform_dashboards_udd_maxwidgets"
>title="介面工具的最大數量"
>abstract="使用者定義的儀表板最多支援十個介面工具。將十個介面工具新增到儀表板後，[!UICONTROL 新增介面工具] 選項會停用並顯示為灰色。"

從您的新儀表板檢視中，選取 **[!UICONTROL 新增Widget]** 以開始建立Widget的程式。

>[!IMPORTANT]
>
>使用者定義的儀表板最多支援十個介面工具。將十個介面工具新增到儀表板後，[!UICONTROL 新增介面工具] 選項會停用並顯示為灰色。

![醒目提示新增Widget的新空白儀表板。](./images/user-defined-dashboards/add-new-widget.png)

### Widget composer

Widget Composer工作區隨即顯示。 接下來，選取 **[!UICONTROL 選取資料]** 選擇要將屬性新增至Widget的資料模型。

![Widget Composer工作區。](./images/user-defined-dashboards/widget-composer.png)

#### 選取資料模型 {#select-data-model}

此 [!UICONTROL 選取資料模型] 對話方塊隨即顯示。 從左欄選取資料模型，以顯示所有可用表格的預覽清單。 Real-time Customer Data Platform預先設定的資料模型已命名為 [!UICONTROL CDPInsights].

>[!TIP]
>
>選取資訊圖示(![資訊圖示。](./images/user-defined-dashboards/info-icon.png))，以在資料邊欄中顯示資料模型名稱過長時檢視完整名稱。

![選取資料對話方塊。](./images/user-defined-dashboards/select-data-model-dialog.png)

預覽清單提供資料模型中所含表格的詳細資訊。 下表提供欄欄位及其潛在值的說明。

| 欄欄位 | 說明 |
|---|---|
| [!UICONTROL 標題] | 資料表的名稱。 |
| [!UICONTROL 表格類型] | 表格的型別。 可能的型別包括： `fact`， `dimension`、和 `none`. |
| [!UICONTROL 記錄] | 與所選表格相關聯的記錄數。 |
| [!UICONTROL 查詢] | 連結至所選表格的表格數目。 |
| [!UICONTROL 屬性] | 所選表格的屬性數目。 |

選取 **[!UICONTROL 下一個]** 以確認您選擇的資料模型。 下一個檢視會在左側邊欄中顯示可用表格的清單。 選取表格以檢視所選表格中所包含資料的完整劃分。

### 填入Widget {#populate-widget}

此 [!UICONTROL 預覽] 面板包含索引標籤 [!UICONTROL 範例記錄] 和 [!UICONTROL 屬性]. 此 [!UICONTROL 範例記錄] tab提供表格檢視中選取表格之記錄的子集。 此 [!UICONTROL 屬性] tab為每一個與所選表格關聯的屬性提供屬性名稱、資料型別和來源表格。

從左側邊欄的可用清單中選取表格，以提供Widget的資料，然後選取 **[!UICONTROL 選取]** 以返回widget composer。

![選取資料對話方塊中反白的選取專案。](./images/user-defined-dashboards/select-a-table.png)

Widget撰寫器現在會填入您所選表格的資料。

資料模型和目前選取的表格會顯示在左側邊欄的最上方，而可用於建立Widget的屬性會列在 [!UICONTROL 屬性] 欄。 您可以使用搜尋列來尋找屬性，而不需捲動清單，或選取鉛筆圖示(![鉛筆圖示。](./images/user-defined-dashboards/edit-icon.png))。

![Widget撰寫器中填入資料的Widget。](./images/user-defined-dashboards/populated-widget-composer.png)

#### 新增和篩選屬性 {#add-and-filter-attributes}

選取新增圖示(![新增圖示。](./images/user-defined-dashboards/add-icon.png))來將屬性新增至您的Widget中。 出現的下拉式選單可讓您為Widget將屬性新增為X軸、Y軸、顏色或濾鏡。 此 [!UICONTROL 顏色] attribute可讓您根據顏色來區分X軸與Y軸標籤的結果。 它根據第三個屬性的組成將結果分割成不同的顏色，以達成此目的。

>[!TIP]
>
>如果要反向X軸和Y軸的排列，請選取向上和向下箭頭圖示(![向上和向下箭頭圖示。](./images/user-defined-dashboards/switch-axis-icon.png))以切換其排列方式。

![Widget Composer會醒目顯示新增圖示的下拉式清單。](./images/user-defined-dashboards/attributes-dropdown.png)

若要變更Widget的圖表型別，請選取 [!UICONTROL 標籤] 下拉式清單，然後從可用的選項中選擇。 選項包括長條、點、刻度、直線或區域。 選取後，系統會產生Widget目前設定的預覽視覺效果。

![Widget Composer中的「標籤」下拉式清單會反白顯示。](./images/user-defined-dashboards/marks-dropdown.png)

將屬性新增為篩選器後，您可以選取要包含或排除Widget中的值。 從屬性清單新增篩選器後， [!UICONTROL 篩選] 對話方塊隨即顯示，您可以在其中使用核取方塊選取或取消選取值。

![篩選對話方塊，用於從您的Widget篩選值。](./images/user-defined-dashboards/filter-dialog.png)

#### 篩選掉歷史資料 {#filter-historical-data}

若要從Widget產生的深入分析中篩選掉歷史資料，請新增 `date_key` 屬性作為篩選器並選取 **[!UICONTROL 最近日期]** 後面接著 **[!UICONTROL 套用]**. 此篩選器可確保用於衍生見解的資料是從最近的系統快照中取得。

![此 [!UICONTROL 篩選器：date_key] 對話方塊 [!UICONTROL 最近日期] 和 [!UICONTROL 套用] 反白顯示。](./images/user-defined-dashboards/recent-date.png)

或者，您可以建立自訂時段，依篩選資料。 選取 **[!UICONTROL 選取日期]** 使用可用日期清單來擴充對話方塊。 使用 **[!UICONTROL 全選]** 核取方塊，以啟用或停用所有可用選項，或分別選取每天的核取方塊。 最後，選取 **[!UICONTROL 套用]** 以確認您的選擇。

>[!NOTE]
>
>如果 `date_key` 屬性已新增為篩選器，請選取省略符號，然後選取 **[!UICONTROL 編輯]** 以變更篩選期間。

![此 [!UICONTROL 篩選器：date_key] 對話方塊，其中包含已核取及未核取的個別日期核取方塊。](./images/user-defined-dashboards/select-dates.png)

### Widget屬性

選取屬性圖示(![屬性圖示。](./images/user-defined-dashboards/properties-icon.png))以開啟「屬性」面板。 在 [!UICONTROL 屬性] 面板，在「 」中輸入介面工具集的名稱 [!UICONTROL Widget標題] 文字欄位。

![屬性面板中會顯示屬性圖示，且Widget標題欄位會反白顯示。](./images/user-defined-dashboards/properties-panel.png)

在Widget屬性面板中，您可以編輯Widget的多個層面。 您擁有編輯Widget圖例位置的完整控制權。 若要移動圖例，請選取 [!UICONTROL 圖例位置] 下拉式清單，並從可用選項清單中選擇所需的位置。 您也可以重新命名與圖例關聯的標籤，並在 [!UICONTROL 圖例標題] 文字欄位，或 [!UICONTROL 座標軸標籤] 文字欄位。

#### 儲存您的Widget {#save-widget}

在Widget Composer中儲存時，會將Widget本機儲存至您的儀表板。 如果要儲存工作並在稍後繼續，請選取 **[!UICONTROL 儲存]**. Widget名稱下方的勾號圖示表示已儲存Widget。 或者，當您滿意您的Widget時，請選取 **[!UICONTROL 儲存並關閉]** 讓Widget可供其他可存取您控制面板的使用者使用。 選取 **[!UICONTROL 取消]** 以放棄工作並返回自訂儀表板。

![新Widget儲存確認。](./images/user-defined-dashboards/save-confirmation.png)

>[!TIP]
>
>選取屬性圖示(![屬性圖示。](./images/user-defined-dashboards/properties-icon.png))來檢視關於其建立的詳細資訊。 您可以在出現的對話方塊中變更圖示板的名稱。

在此工作區中，Widget可以重新排列和調整大小。 選取 **[!UICONTROL 儲存]** 以保留您的控制面板名稱和已設定的配置。

![使用者定義儀表板，其中含有自訂Widget及醒目提示的儲存按鈕。](./images/user-defined-dashboards/user-defined-dashboard.png)

為了確保Adobe Real-time Customer Data Platform見解儀表板的每個查詢都有足夠的資源來有效執行，API會透過為每個查詢指派並行位置來追蹤資源使用情況。 系統最多可以處理四個同時查詢，因此在任何給定時間都有四個同時查詢空位可用。 查詢會根據並行位置放入佇列中，然後在佇列中等待，直到有足夠的並行位置可用。

### 複製Widget

建立Widget後，您可以複製整個Widget並自訂其屬性以建立唯一的Widget，而不需從頭開始。 若要複製Widget，請先導覽至控制面板詳細目錄。 然後，從詳細目錄清單中選取控制面板名稱。 您的自訂儀表板隨即出現。

![包含控制面板和自訂控制面板名稱的Platform UI會醒目提示。](./images/user-defined-dashboards/dashbaord-inventory.png)

選取鉛筆圖示(![鉛筆圖示。](./images/user-defined-dashboards/edit-icon.png))，以進入編輯模式。

![反白顯示鉛筆圖示的自訂儀表板。](./images/user-defined-dashboards/edit-mode.png)

接著，選取您要複製之Widget右上方的省略符號，接著再選取 **[!UICONTROL 複製]** 從可用選項清單中選取。

![使用者定義儀表板中的Widget，其中反白顯示橢圓形和重複的Widget。](./images/user-defined-dashboards/duplicate.png)

重複的Widget會顯示在您使用者定義的儀表板中。 選取新Widget的省略符號，然後選取 **[!UICONTROL 編輯]**，以自訂您的新Widget。

## 後續步驟和其他資源

閱讀本檔案後，您將會更加瞭解如何建立自訂儀表板，以及如何為該儀表板建立、編輯和更新自訂Widget。

若要探索適用於的可用預先設定量度和視覺效果 [設定檔](./guides/profiles.md#standard-widgets)， [區段](./guides/audiences.md#standard-widgets)、和 [目的地](./guides/destinations.md#standard-widgets) 儀表板，請參閱其各自檔案中的標準Widget清單。

若要加深您對Experience Platform中使用者定義之控制面板的瞭解，請觀看下列影片：

>[!VIDEO](https://video.tv.adobe.com/v/3409637?quality=12&learn=on)
