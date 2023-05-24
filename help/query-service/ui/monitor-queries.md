---
title: 監視計畫查詢
description: 瞭解如何通過查詢服務用戶介面監視查詢。
exl-id: 4640afdd-b012-4768-8586-32f1b8232879
source-git-commit: 1b4554e204663d40c3a18da792614305abb7d296
workflow-type: tm+mt
source-wordcount: '1252'
ht-degree: 0%

---

# 監視計畫查詢

Adobe Experience Platform通過UI為所有查詢作業的狀態提供了改進的可見性。 從 [!UICONTROL 計畫查詢] 頁籤，您現在可以找到有關查詢運行的重要資訊，其中包括狀態、計畫詳細資訊以及錯誤消息/代碼（如果它們失敗）。 您還可以通過UI訂閱查詢的警報，這些警報基於查詢的狀態通過 [!UICONTROL 計畫查詢] 頁籤。

## [!UICONTROL 計畫查詢]

的 [!UICONTROL 計畫查詢] 頁籤提供所有計畫的CTAS和ITAS查詢的概述。 可以找到所有計畫查詢的運行詳細資訊以及任何失敗查詢的錯誤代碼和消息。

導航到 [!UICONTROL 計畫查詢] 頁籤 **[!UICONTROL 查詢]** 從左導航欄開始，然後 **[!UICONTROL 計畫查詢]**

![「查詢」(Queries)工作區中的「計畫查詢」(Scheduled Queries)頁籤。](../images/ui/monitor-queries/scheduled-queries.png)

下表介紹了每個可用列。

>[!NOTE]
>
>警報預訂表徵圖包含在未命名列的每行中。 查看 [警報訂閱](#alert-subscription) 的子菜單。

| 欄 | 說明 |
|---|---|
| **[!UICONTROL 名稱]** | 名稱欄位是SQL查詢的模板名稱或前幾個字元。 通過UI使用查詢編輯器建立的任何查詢都會在開始時命名。 如果查詢是通過API建立的，則其名稱將成為用於建立查詢的初始SQL的代碼段。 從 [!UICONTROL 名稱] 列，查看與查詢關聯的所有運行的清單。 有關詳細資訊，請參閱 [查詢運行計畫詳細資訊](#query-runs) 的子菜單。 |
| **[!UICONTROL 範本]** | 查詢的模板名稱。 選擇要導航到查詢編輯器的模板名稱。 查詢模板將顯示在查詢編輯器中，以方便您。 如果沒有模板名稱，行將標籤為連字元，並且無法重定向到查詢編輯器來查看查詢。 |
| **[!UICONTROL SQL]** | SQL查詢的片段。 |
| **[!UICONTROL 運行頻率]** | 這是將查詢設定為運行的節奏。 可用值包括 `Run once` 和 `Scheduled`。 可根據查詢的運行頻率過濾查詢。 |
| **[!UICONTROL 建立者]** | 建立查詢的用戶的名稱。 |
| **[!UICONTROL 已建立]** | 以UTC格式建立查詢時的時間戳。 |
| **[!UICONTROL 上次運行時間戳]** | 運行查詢時的最新時間戳。 此列突出顯示查詢是否已根據其當前計畫執行。 |
| **[!UICONTROL 上次運行狀態]** | 最近執行查詢的狀態。 狀態值為： `Success`。 `Failed`。 `In progress`, `No runs`。 |

>[!TIP]
>
>如果導航至查詢編輯器，可以選擇 **[!UICONTROL 查詢]** 返回 [!UICONTROL 模板] 頁籤。

### 自定義計畫查詢的表設定

可以調整 [!UICONTROL 計畫查詢] 頁籤。 選擇設定表徵圖(![設定表徵圖。](../images/ui/monitor-queries/settings-icon.png))開啟 [!UICONTROL 自定義表] 設定對話框並編輯可用列。

![「自定義表設定」表徵圖。](../images/ui/monitor-queries/customze-table-settings-icon.png)

切換相關複選框以刪除或添加表列。 下一步，選擇 **[!UICONTROL 應用]** 確認你的選擇。

>[!NOTE]
>
>通過UI建立的任何查詢都將成為建立過程的指定模板。 模板名稱在模板列中顯示。 如果查詢是通過API建立的，則模板列為空。

![「定制表設定」對話框。](../images/ui/monitor-queries/customize-table-dialog.png)

### 訂閱警報 {#alert-subscription}

您可以訂閱來自 [!UICONTROL 計畫查詢] 頁籤。 選擇警報通知表徵圖(![警報表徵圖。](../images/ui/monitor-queries/alerts-icon.png)) [!UICONTROL 警報] 對話框。 的 [!UICONTROL 警報] 對話框訂閱UI通知和電子郵件警報。 警報基於查詢的狀態。 有三種選擇： `start`。 `success`, `failure`。 選中相應的框並選擇 **[!UICONTROL 保存]** 訂閱。

![警報預訂對話框。](../images/ui/monitor-queries/alert-subscription-dialog.png)

查看 [警報訂閱API文檔](../api/alert-subscriptions.md) 的子菜單。

### 篩選查詢 {#filter}

您可以根據運行頻率篩選查詢。 從 [!UICONTROL 計畫查詢] 頁籤![篩選器表徵圖](../images/ui/monitor-queries/filter-icon.png))開啟篩選器邊欄。

![「已調度的查詢」頁籤，其中「篩選器」表徵圖突出顯示。](../images/ui/monitor-queries/filter-queries.png)

選擇 **[!UICONTROL 計畫]** 或 **[!UICONTROL 運行一次]** 運行頻率篩選器複選框以篩選查詢清單。

>[!NOTE]
>
>已執行但未計畫為的任何查詢 [!UICONTROL 運行一次]。

![已調度的查詢頁籤，並突出顯示過濾器邊欄。](../images/ui/monitor-queries/filter-sidebar.png)

啟用篩選條件後，選擇 **[!UICONTROL 隱藏篩選器]** 按鈕。

## 查詢運行計畫詳細資訊 {#query-runs}

選擇查詢名稱以導航到計畫詳細資訊頁。 此視圖提供作為該計畫查詢的一部分執行的所有運行的清單。 提供的資訊包括使用的開始和結束時間、狀態和資料集。

![調度詳細資訊頁。](../images/ui/monitor-queries/schedule-details.png)

此資訊在五清單中提供。 每行表示查詢執行。

| 資料行名稱 | 說明 |
|---|---|
| **[!UICONTROL 查詢運行ID]** | 每日執行的查詢運行ID。 選擇 **[!UICONTROL 查詢運行ID]** 導航至 [!UICONTROL 查詢運行概述]。 |
| **[!UICONTROL 查詢運行開始]** | 執行查詢時的時間戳。 這是UTC格式。 |
| **[!UICONTROL 查詢運行完成]** | 查詢完成時的時間戳。 這是UTC格式。 |
| **[!UICONTROL 狀態]** | 最近執行查詢的狀態。 三個狀態值是： `successful` `failed` 或 `in progress`。 |
| **[!UICONTROL 資料集]** | 執行中涉及的資料集。 |

有關正在計畫的查詢的詳細資訊，請參見 [!UICONTROL 屬性] 的子菜單。 此面板包括計畫的初始查詢ID、客戶端類型、模板名稱、查詢SQL和順序。

![「計畫詳細資訊」頁面，其中「屬性」面板突出顯示。](../images/ui/monitor-queries/properties-panel.png)

選擇查詢運行ID以導航到運行詳細資訊頁並查看查詢資訊。

![突出顯示運行ID的計畫詳細資訊螢幕。](../images/ui/monitor-queries/navigate-to-run-details.png)

## 查詢運行概述 {#query-run-overview}

的 [!UICONTROL 查詢運行概述] 提供了有關此計畫查詢的單個運行的資訊以及運行狀態的更詳細的細分。 此頁還包括客戶端資訊以及可能導致查詢失敗的任何錯誤的詳細資訊。

![「運行詳細資訊」螢幕，「概述」部分突出顯示。](../images/ui/monitor-queries/query-run-details.png)

如果查詢失敗，查詢狀態部分將提供錯誤代碼和錯誤消息。

![「運行詳細資訊」螢幕，其中「錯誤」部分突出顯示。](../images/ui/monitor-queries/failed-query.png)

您可以從此視圖將查詢SQL複製到剪貼簿。 選擇SQL代碼段右上角的複製表徵圖以複製查詢。 彈出消息確認代碼已複製。

![SQL複製表徵圖突出顯示的運行詳細資訊螢幕。](../images/ui/monitor-queries/copy-sql.png)

### 為具有匿名塊的查詢運行詳細資訊 {#anonymous-block-queries}

使用匿名塊組成其SQL陳述式的查詢被分隔成各自的子查詢。 這允許您單獨檢查每個查詢塊的運行詳細資訊。

>[!NOTE]
>
>使用DROP命令的匿名塊的運行詳細資訊將 **不** 作為單獨的子查詢報告。 CTAS查詢、ITAS查詢和用作匿名塊子查詢的COPY語句可以使用單獨的運行詳細資訊。 當前不支援DROP命令的運行詳細資訊。

匿名塊通過使用 `$$` 查詢前的前置詞。 查看 [匿名塊文檔](../essential-concepts/anonymous-block.md) 查找有關查詢服務中匿名塊的詳細資訊。

匿名塊子查詢在運行狀態左側具有頁籤。 選擇一個頁籤以顯示運行詳細資訊。

![顯示匿名塊查詢的查詢運行概述。 多個查詢頁籤被突出顯示。](../images/ui/monitor-queries/anonymous-block-overview.png)

如果匿名塊查詢失敗，您可以通過此UI找到該特定塊的錯誤代碼。

![「查詢」運行概述顯示匿名塊查詢，其中單個塊的錯誤代碼突出顯示。](../images/ui/monitor-queries/anonymous-block-failed-query.png)

選擇 **[!UICONTROL 查詢]** 返回計畫詳細資訊螢幕，或 **[!UICONTROL 計畫查詢]** 返回 [!UICONTROL 計畫查詢] 頁籤。

![突出顯示「查詢」的「運行詳細資訊」螢幕。](../images/ui/monitor-queries/return-navigation.png)
