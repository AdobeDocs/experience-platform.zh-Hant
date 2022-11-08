---
title: 監視查詢
description: 了解如何透過Query Service UI監控查詢。
exl-id: 4640afdd-b012-4768-8586-32f1b8232879
source-git-commit: a9887535b12b8c4aeb39bb5a6646da88db4f0308
workflow-type: tm+mt
source-wordcount: '1033'
ht-degree: 1%

---

# 監視查詢

Adobe Experience Platform透過UI改善所有查詢作業的狀態可見性。 從 [!UICONTROL 排程查詢] 索引標籤您現在可以找到有關查詢執行的重要資訊，包括狀態、排程詳細資訊，以及失敗時的錯誤訊息/程式碼。 您也可以透過UI，針對任何這些查詢，根據查詢的狀態來訂閱警報 [!UICONTROL 排程查詢] 標籤。

## [!UICONTROL 排程查詢]

此 [!UICONTROL 排程查詢] 索引標籤提供已執行和已排程查詢的概觀。 工作區包含所有排程執行或至少執行一次的CTAS和ITAS查詢。 可以找到所有計畫查詢的運行詳細資訊，以及失敗查詢的錯誤代碼和消息。

導覽至 [!UICONTROL 排程查詢] 索引標籤，選取 **[!UICONTROL 查詢]** 從左側導覽列，隨後 **[!UICONTROL 排程查詢]**

![查詢工作區中的「排程查詢」索引標籤。](./images/monitor-queries/scheduled-queries.png)

下表說明了每個可用列。

>[!NOTE]
>
>無標題欄中的每一列都包含警報訂閱圖示。 請參閱 [警報訂閱](#alert-subscription) 一節以取得詳細資訊。

| 欄 | 說明 |
|---|---|
| 名稱 | 名稱欄位是模板名稱或SQL查詢的前幾個字元。 任何透過UI使用查詢編輯器建立的查詢，都會在開始時命名。 如果查詢是透過API建立，則查詢的名稱是用於建立查詢的初始SQL的片段。 |
| 範本 | 查詢的模板名稱。 選取範本名稱以導覽至「查詢編輯器」。 為方便起見，查詢模板將顯示在查詢編輯器中。 如果沒有範本名稱，則會以連字型大小標示列，且無法重新導向至查詢編輯器以檢視查詢。 |
| SQL | SQL查詢的一段代碼。 |
| 執行頻率 | 這是設定查詢運行的順序。 可用值包括 `Run once` 和 `Scheduled`. 可以根據查詢的運行頻率來篩選查詢。 |
| 建立者 | 建立查詢的用戶的名稱。 |
| 已建立 | 查詢建立時的時間戳記，以UTC格式表示。 |
| 上次運行時間戳 | 查詢執行時的最新時間戳記。 此欄會強調顯示查詢是否已根據其目前排程執行。 |
| 上次運行狀態 | 最近的查詢執行的狀態。 三個狀態值為： `successful` `failed` 或 `in progress`. |

>[!TIP]
>
>如果您導覽至查詢編輯器，可以選取 **[!UICONTROL 查詢]** 返回 [!UICONTROL 範本] 標籤。

### 自定義計畫查詢的表設定

您可以調整 [!UICONTROL 排程查詢] 標籤。 選取設定圖示(![設定圖示。](./images/monitor-queries/settings-icon.png))以開啟 [!UICONTROL 自訂表格] 「設定」對話框和編輯可用列。

![「自定義表設定」表徵圖。](./images/monitor-queries/customze-table-settings-icon.png)

切換相關核取方塊以移除或新增表格欄。 下一步，選擇 **[!UICONTROL 套用]** 確認您的選擇。

>[!NOTE]
>
>透過UI建立的任何查詢，都會在建立程式中變成指定的範本。 範本名稱會顯示在範本欄中。 如果查詢是透過API建立，則範本欄為空白。

![「自定義表設定」對話框。](./images/monitor-queries/customize-table-dialog.png)

### 訂閱警報 {#alert-subscription}

您可以訂閱 [!UICONTROL 排程查詢] 標籤。 選取警報通知圖示(![警報表徵圖。](./images/monitor-queries/alerts-icon.png))，以開啟 [!UICONTROL 警報] 對話框。 此 [!UICONTROL 警報] 對話方塊會訂閱UI通知和電子郵件警報。 警報是根據查詢的狀態。 有三個可用選項： `start`, `success`，和 `failure`. 選中相應的框或框並選擇 **[!UICONTROL 儲存]** 訂閱。

<!-- This dialog will be updated before release. THe image below will need to be updated inline with these changes. -->

![「警報訂閱」對話框。](./images/monitor-queries/alert-subscription-dialog.png)

<!-- Link to alert subscriptions doc when available -->

### 篩選查詢

您可以根據執行頻率來篩選查詢。 從 [!UICONTROL 排程查詢] 標籤，選取篩選圖示(![篩選器圖示](./images/monitor-queries/filter-icon.png))以開啟篩選器側欄。

![已排程查詢索引標籤並反白顯示篩選圖示。](./images/monitor-queries/filter-queries.png)

選取 **[!UICONTROL 已排程]** 或 **[!UICONTROL 執行一次]** 運行頻率篩選複選框以篩選查詢清單。

>[!NOTE]
>
>任何已執行但未排程為 [!UICONTROL 執行一次].

![反白顯示篩選器側欄的排程查詢標籤。](./images/monitor-queries/filter-sidebar.png)

啟用篩選條件後，請選取 **[!UICONTROL 隱藏篩選器]** 來關閉篩選面板。

## 查詢運行計畫詳細資訊

選擇查詢名稱以定位至「計畫詳細資訊」頁。 此檢視提供該排程查詢中執行之所有執行的清單。 提供的資訊包括使用的開始和結束時間、狀態和資料集。

![排程詳細資料頁面。](./images/monitor-queries/schedule-details.png)

此資訊以五欄表格提供。 每行都表示查詢執行。

| 資料行名稱 | 說明 |
|---|---|
| 查詢運行ID | 每日執行的查詢運行ID。 |
| 查詢運行開始 | 執行查詢時的時間戳記。 此格式為UTC格式。 |
| 查詢運行完成 | 查詢完成時的時間戳記。 此格式為UTC格式。 |
| 狀態 | 最近的查詢執行的狀態。 三個狀態值為： `successful` `failed` 或 `in progress`. |
| 資料集 | 與執行有關的資料集。 |

如需排程查詢的詳細資訊，請參閱 [!UICONTROL 屬性] 中。 此面板包括初始查詢ID、客戶端類型、模板名稱、查詢SQL和調度的順序。

![「計畫詳細資訊」頁，其中突出顯示了「屬性」面板。](./images/monitor-queries/properties-panel.png)

### 執行詳細資訊

選擇查詢運行ID以導航至運行詳細資訊頁並查看查詢資訊。

![「Schedule details（計畫詳細資訊）」螢幕中突出顯示運行ID。](./images/monitor-queries/navigate-to-run-details.png)

此檢視提供有關此排程查詢個別執行的資訊，以及更詳細的執行狀態劃分。 此頁還包含客戶端資訊以及導致查詢失敗的任何錯誤的詳細資訊。

![執行詳細資訊畫面會反白顯示概述區段。](./images/monitor-queries/query-run-details.png)

如果查詢失敗，查詢狀態節將提供錯誤代碼和錯誤消息。

![「運行詳細資訊」螢幕上突出顯示了「錯誤」部分。](./images/monitor-queries/failed-query.png)

您可以從此視圖將查詢SQL複製到剪貼簿。 選擇SQL代碼段右上角的複製表徵圖以複製查詢。 快顯訊息會確認程式碼已複製。

![「運行詳細資訊」螢幕中突出顯示了SQL複製表徵圖。](./images/monitor-queries/copy-sql.png)

選擇 **[!UICONTROL 查詢]** 返回「計畫詳細資訊」螢幕，或 **[!UICONTROL 排程查詢]** 返回 [!UICONTROL 排程查詢] 標籤。

![「Query（查詢）」突出顯示的運行詳細資訊螢幕。](./images/monitor-queries/return-navigation.png)
