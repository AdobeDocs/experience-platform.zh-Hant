---
title: 用戶定義的儀表板
description: 瞭解如何構建和管理自定義儀表板，在此可以建立、添加和編輯定制小部件以可視化關鍵度量。
exl-id: a9ab83f7-b68d-4dbf-9dc6-ef253df5c82c
source-git-commit: 8507ecceca47fac3d321b89e4fed018ee9784777
workflow-type: tm+mt
source-wordcount: '1608'
ht-degree: 3%

---

# 用戶定義的儀表板

Adobe Experience Platform儀表板通過用戶定義的儀表板功能幫助您加快洞察和自定義可視化。 此功能使您能夠構建和管理自定義儀表板，您可以在其中建立、添加和編輯定制小部件，以可視化與您的組織相關的關鍵度量。

<!-- Getting started / permissions section commented out for Beta. This will be necessary after GA only

## Getting started

To view dashboards in Adobe Experience Platform you must have the appropriate permissions enabled. Please read the [dashboards permissions documentation](./permissions.md#available-permissions) to learn how to grant users the ability to view, edit, and update Experience Platform dashboards using Adobe Admin Console. If you do not have administrator privileges for your organization, contact your product administrator to obtain the required permissions. -->

## 建立自定義儀表板

要建立自定義儀表板，請首先導航至儀表板清單。 選擇 **[!UICONTROL 儀表板]** 從平台UI的左側導航，然後 **[!UICONTROL 建立儀表板]**。

![左側導航中帶有儀表板的儀表板清單和突出顯示的「建立儀表板」。](./images/user-defined-dashboards/create-dashboard.png)

在添加自定義儀表板之前，儀表板清單為空並顯示「未找到儀表板」。 。 建立後，所有用戶定義的儀表板都會列在儀表板清單中。

>[!NOTE]
>
>要編輯現有儀表板，請從清單清單中選擇儀表板名稱，然後選擇鉛筆表徵圖(![鉛筆表徵圖。](./images/user-defined-dashboards/edit-icon.png))

的 [!UICONTROL 建立儀表板] 對話框。 輸入要建立的小部件集合的人性化的描述性名稱，然後選擇 **[!UICONTROL 保存]**。

![「建立儀表板」對話框。](./images/user-defined-dashboards/create-dashboard-dialog.png)

新建立的空白儀表板將以您所選的名稱出現在視圖的左上角。

## 建立小部件 {#create-widget}

>[!CONTEXTUALHELP]
>id="platform_dashboards_udd_maxwidgets"
>title="Widget 的最大數量"
>abstract="使用者定義的儀表板最多支援十個 Widget。將十個 Widget 新增到儀表板後，[!UICONTROL 新增 Widget] 選項會停用並顯示為灰色。"

從新儀表板視圖中，選擇 **[!UICONTROL 添加新小部件]** 開始構件建立過程。

>[!IMPORTANT]
>
>使用者定義的儀表板最多支援十個 Widget。將十個 Widget 新增到儀表板後，[!UICONTROL 新增 Widget] 選項會停用並顯示為灰色。

![突出顯示了「添加新小部件」的新空儀表板。](./images/user-defined-dashboards/add-new-widget.png)

### 小部件編寫器

將顯示小部件編寫器工作區。 下一步，選擇 **[!UICONTROL 選擇資料]** 選擇向小部件添加屬性的資料模型。

![小部件編寫器工作區。](./images/user-defined-dashboards/widget-composer.png)

#### 選擇資料模型 {#select-data-model}

的 [!UICONTROL 選擇資料模型] 對話框。 從左列中選擇一個資料模型以顯示所有可用表的預覽清單。 預配置的Real-time Customer Data Platform資料模型名為 [!UICONTROL CDPInsights]。

>[!TIP]
>
>選擇資訊表徵圖(![資訊表徵圖。](./images/user-defined-dashboards/info-icon.png))查看完整的資料模型名稱（如果在資料欄中顯示太長）。

![選擇資料對話框。](./images/user-defined-dashboards/select-data-model-dialog.png)

預覽清單提供有關資料模型中包含的表的詳細資訊。 下表提供了列欄位及其潛在值的說明。

| 列欄位 | 說明 |
|---|---|
| [!UICONTROL 標題] | 表的名稱。 |
| [!UICONTROL 表格類型] | 表的類型。 潛在類型包括： `fact`。 `dimension`, `none`。 |
| [!UICONTROL 記錄] | 與所選表關聯的記錄數。 |
| [!UICONTROL 查找] | 聯接到所選表的表數。 |
| [!UICONTROL 屬性] | 所選表的屬性數。 |

選擇 **[!UICONTROL 下一個]** 確認您選擇的資料模型。 下一個視圖顯示左滑軌中可用表的清單。 選擇一個表，查看所選表中包含的資料的全面細分。

### 填充小部件 {#populate-widget}

的 [!UICONTROL 預覽] 面板包含頁籤 [!UICONTROL 示例記錄] 和 [!UICONTROL 屬性]。 的 [!UICONTROL 示例記錄] 頁籤提供清單視圖中選定表中記錄的子集。 的 [!UICONTROL 屬性] 頁籤為與所選表關聯的每個屬性提供屬性名稱、資料類型和源表。

從左側滑軌中可用的清單中選擇一個表，以提供小部件的資料，然後選擇 **[!UICONTROL 選擇]** 返回到小部件作曲家。

![「選擇資料」對話框，其中「選擇」突出顯示。](./images/user-defined-dashboards/select-a-table.png)

現在，小部件編寫器將填充所選表中的資料。

資料模型和當前選定的表顯示在左滑軌的頂部，可用於建立小部件的屬性列在 [!UICONTROL 屬性] 的雙曲餘切值。 您可以使用搜索欄來查找屬性，而不是滾動清單，或通過選擇鉛筆表徵圖(![鉛筆表徵圖。](./images/user-defined-dashboards/edit-icon.png))。

![在小部件編寫器中填充資料的小部件。](./images/user-defined-dashboards/populated-widget-composer.png)

#### 添加和篩選屬性 {#add-and-filter-attributes}

選擇添加表徵圖(![添加表徵圖。](./images/user-defined-dashboards/add-icon.png))，以將屬性添加到小部件。 顯示的下拉菜單允許您將屬性添加為小部件的X軸、Y軸、顏色或濾鏡。 的 [!UICONTROL 顏色] 屬性允許您根據顏色來區分X和Y軸標籤的結果。 它通過根據結果對第三個屬性的合成將結果拆分為不同的顏色來實現這一點。

>[!TIP]
>
>如果要反向X和Y軸的排列，請選取上箭頭和下箭頭表徵圖(![上箭頭和下箭頭表徵圖。](./images/user-defined-dashboards/switch-axis-icon.png))來改變他們的安排。

![突出顯示了添加表徵圖下拉清單的小部件編寫器。](./images/user-defined-dashboards/attributes-dropdown.png)

要更改小部件的圖形或圖表類型，請選擇 [!UICONTROL 標籤] 下拉清單，然後從可用選項中選擇。 選項包括條、點、刻度、線條或區域。 選定後，將生成小部件當前設定的預覽可視化。

![突出顯示標籤下拉的構件編寫器。](./images/user-defined-dashboards/marks-dropdown.png)

通過將屬性添加為篩選器，您可以選擇要包括或從構件中排除的值。 在從屬性清單中添加篩選器後， [!UICONTROL 篩選] 對話框，您可以在其中使用值複選框選擇或取消選擇值。

![用於篩選小部件中值的篩選器對話框。](./images/user-defined-dashboards/filter-dialog.png)

#### 篩選歷史資料 {#filter-historical-data}

要從小部件生成的透視中篩選歷史資料，請添加 `date_key` 屬性作為篩選器並選擇 **[!UICONTROL 最近日期]** 後跟 **[!UICONTROL 應用]**。 此篩選器確保用於獲取洞察力的資料是從最近的系統快照獲取的。

![的 [!UICONTROL 篩選器：日期鍵] 對話 [!UICONTROL 最近日期] 和 [!UICONTROL 應用] 。](./images/user-defined-dashboards/recent-date.png)

或者，您可以建立自定義期間以按篩選資料。 選擇 **[!UICONTROL 選擇日期]** 將對話框擴展為可用日期清單。 使用 **[!UICONTROL 全選]** 複選框以啟用或禁用所有可用選項，或單獨選中每天的複選框。 最後，選擇 **[!UICONTROL 應用]** 確認你的選擇。

>[!NOTE]
>
>如果 `date_key` 屬性已添加為篩選器，請選擇省略號後跟 **[!UICONTROL 編輯]** 的子菜單。

![的 [!UICONTROL 篩選器：日期鍵] 對話框，其中選中和取消選中各個日複選框。](./images/user-defined-dashboards/select-dates.png)

### 小部件屬性

選擇屬性表徵圖(![屬性表徵圖。](./images/user-defined-dashboards/properties-icon.png))開啟屬性面板。 在 [!UICONTROL 屬性] 面板，在 [!UICONTROL 小部件標題] 的子菜單。

![帶有屬性表徵圖的屬性面板和突出顯示的小部件標題欄位。](./images/user-defined-dashboards/properties-panel.png)

在小部件屬性面板中，可以編輯小部件的幾個方面。 您可以完全控制編輯小部件圖例的位置。 要移動圖例，請選擇 [!UICONTROL 圖例放置] 下拉清單，然後從可用選項清單中選擇所需的位置。 也可以通過在圖例中輸入新名稱來更名與圖例、X或Y軸關聯的標籤 [!UICONTROL 圖例標題] 文本欄位，或 [!UICONTROL 軸標籤] 文本欄位。

#### 保存小部件 {#save-widget}

在小部件編寫器中保存小部件時，會將該小部件本地保存到儀表板。 如果希望保存您的工作並稍後繼續，請選擇 **[!UICONTROL 保存]**。 小部件名稱下面的勾選表徵圖表示該小部件已保存。 或者，當您對小部件感到滿意時，選擇 **[!UICONTROL 保存並關閉]** 使該小部件可供有權訪問儀表板的所有其他用戶使用。 選擇 **[!UICONTROL 取消]** 放棄您的工作並返回到自定義儀表板。

![新小部件保存確認。](./images/user-defined-dashboards/save-confirmation.png)

>[!TIP]
>
>選擇屬性表徵圖(![屬性表徵圖。](./images/user-defined-dashboards/properties-icon.png))，查看有關其建立的詳細資訊。 可在顯示的對話框中更改儀表板的名稱。

在此工作區中可以重新排列小部件並調整小部件大小。 選擇 **[!UICONTROL 保存]** 以保留儀表板名稱和配置的佈局。

![帶有自定義小部件的用戶定義的儀表板和突出顯示的保存按鈕。](./images/user-defined-dashboards/user-defined-dashboard.png)

為確保Adobe Real-time Customer Data Platform透視儀表板的每個查詢都有足夠的資源來高效執行，API通過為每個查詢分配併發槽來跟蹤資源使用情況。 系統最多可處理四個併發查詢，因此在任何給定時間都可使用四個併發查詢槽。 查詢將基於併發時隙被放入隊列中，然後在隊列中等待直到有足夠的併發時隙可用。

### 複製小部件

建立小部件後，您可以複製整個小部件並自定義其屬性以建立唯一的小部件，而無需從頭開始。 要複製小部件，請首先導航到儀表板清單。 然後從清單清單中選擇儀表板名稱。 將顯示您的自定義儀表板。

![帶儀表板的平台UI和自定義儀表板名稱突出顯示。](./images/user-defined-dashboards/dashbaord-inventory.png)

選擇鉛筆表徵圖(![鉛筆表徵圖。](./images/user-defined-dashboards/edit-icon.png))，進入編輯模式。

![突出顯示鉛筆表徵圖的自定義儀表板。](./images/user-defined-dashboards/edit-mode.png)

接下來，選擇要複製的小部件右上角的橢圓，然後 **[!UICONTROL 重複]** 的子菜單。

![在突出顯示橢圓和重複小部件的用戶定義的儀表板中的小部件。](./images/user-defined-dashboards/duplicate.png)

在用戶定義的儀表板中顯示重複的小部件。 選擇新小部件的省略號，然後 **[!UICONTROL 編輯]**，以自定義新小部件。

## 後續步驟和其他資源

通過閱讀此文檔，您可以更好地瞭解如何建立自定義儀表板以及如何為該儀表板建立、編輯和更新自定義小部件。

查找可用的預配置度量和可視化 [配置檔案](./guides/profiles.md#standard-widgets)。 [段](./guides/segments.md#standard-widgets), [目的地](./guides/destinations.md#standard-widgets) 控制板，請參閱各自文檔中的標準小部件清單。

要增強您對Experience Platform中用戶定義的儀表板的瞭解，請觀看以下視頻：

>[!VIDEO](https://video.tv.adobe.com/v/3409637?quality=12&learn=on)
