---
title: 查詢記錄
description: 每次執行查詢時都會自動產生查詢記錄，並可透過UI取得查詢記錄以協助疑難排解。 本檔案概述如何使用及導覽UI的「查詢服務記錄檔」區段。
exl-id: 929e9fba-a9ba-4bf9-a363-ca8657a84f75
source-git-commit: 88498a1382202bed057b8dc52d09359ba02748ea
workflow-type: tm+mt
source-wordcount: '899'
ht-degree: 0%

---

# 查詢記錄

>[!IMPORTANT]
>
>某些查詢記錄功能目前還在有限版本中，無法供所有客戶使用。 如果沒有編輯圖示，您的UI可能會以稍微不同的方式顯示。 此外，選擇查詢名稱的過程可能會導航到查詢編輯器，而不是 [!UICONTROL 查詢記錄檔詳細資料] 檢視。

Adobe Experience Platform會維護透過API和UI發生的所有查詢事件的記錄。 此資訊可在以下網址的查詢服務UI中使用： [!UICONTROL 記錄檔] 標籤。

記錄檔是由任何查詢事件自動產生，並包含所使用SQL、查詢狀態、所需時間以及上次執行時間等資訊。 您可以使用查詢記錄檔資料當作強大的工具，來疑難排解低效或問題查詢。 稽核記錄功能會保留更完整的記錄資訊，可在以下連結中找到： [稽核記錄檔案](../../landing/governance-privacy-security/audit-logs/overview.md).

## 檢查查詢記錄

若要檢查查詢記錄，請選取 [!UICONTROL 查詢] 導覽至查詢服務工作區，然後選取 [!UICONTROL 記錄] 可用選項中的。

![顯示查詢和記錄的Platform UI。](../images/ui/query-log/logs.png)

## 自訂和搜尋 {#customize-and-search}

查詢服務記錄以可自訂的表格格式顯示。 若要自訂表格欄，請選取設定圖示(![設定圖示。](../images/ui/query-log/settings-icon.png))。 A [!UICONTROL 自訂表格] 對話方塊隨即出現，可在其中取消選取每一欄。

您也可以在搜尋欄位中輸入範本名稱，以搜尋與特定查詢範本相關的記錄。

![使用搜尋列和管理欄表格下拉式清單強調顯示的查詢記錄工作區。](../images/ui/query-log/customize-logs.png)

A [每個日誌表格資料欄的說明](./overview.md#log) 您可以在查詢服務概觀的記錄區段找到。

## 探索記錄檔資料

每一列代表與查詢範本相關之查詢回合的記錄資料。 從表格中選取任何列，以該回合的記錄資料填入右側邊欄。

![查詢記錄工作區中選取了一列，並且右側邊欄中的記錄資料反白顯示。](../images/ui/query-log/log-details.png)

在記錄詳細資料面板中，您可以選取新的輸出資料集，並檢視或複製執行中使用的完整SQL查詢。

![查詢記錄工作區中選取了一列，並反白顯示輸出資料集和SQL查詢。](../images/ui/query-log/edit-output-dataset.png)

>[!IMPORTANT]
>
>某些查詢記錄功能目前還在有限版本中，無法供所有客戶使用。

您也可以從以下位置選取查詢範本名稱： [!UICONTROL 名稱] 欄，直接導覽至 [!UICONTROL 查詢記錄檔詳細資料] 檢視。

>[!NOTE]
>
>如果查詢是使用API建立的，且在初始化期間未提供範本名稱，則會改為顯示SQL查詢的前幾十個字元。

![「查詢記錄詳細資料」檢視。](../images/ui/query-log/query-log-details.png)

## 編輯記錄 {#edit-logs}

每一列的範本名稱或SQL程式碼片段旁邊是一個鉛筆圖示(![鉛筆圖示。](../images/ui/query-log/edit-icon.png))以導覽至查詢編輯器。 然後會在編輯器中預先填入查詢以進行編輯。

![以鉛筆圖示反白顯示的查詢記錄工作區。](../images/ui/query-log/edit-query.png)

## 篩選記錄 {#filter-logs}

您可以根據各種設定來篩選查詢記錄清單。 選取篩選器圖示(![篩選圖示。](../images/ui/query-log/filter-icon.png))，以在左側欄中開啟一組篩選選項。

![查詢記錄工作區中反白了篩選圖示。](../images/ui/query-log/log-filter.png)

將顯示可用篩選器清單。

![查詢記錄工作區，其中顯示並反白了篩選選項。](../images/ui/query-log/log-filter-settings.png)

下表證明了每個篩選的說明。

| 篩選 | 說明 |
| ------ | ----------- |
| [!UICONTROL 排除儀表板查詢] | 此核取方塊預設為啟用，並排除用於產生深入分析的查詢所產生的記錄。 這些查詢是系統產生的，模糊了使用者產生的記錄，這些記錄是監視、管理和疑難排解所必需的。 若要檢視系統產生的記錄，請取消選取核取方塊。 |
| [!UICONTROL 開始日期] | 若要篩選在特定期間內建立之查詢的記錄，請設定 [!UICONTROL 開始] 和 [!UICONTROL 結束] 中的日期 [!UICONTROL 開始日期] 區段。 |
| [!UICONTROL 完成日期] | 若要篩選在特定期間內完成的查詢記錄，請設定 [!UICONTROL 開始] 和 [!UICONTROL 結束] 中的日期 [!UICONTROL 完成日期] 區段。 |
| [!UICONTROL 狀態] | 若要根據以下專案篩選記錄檔： [!UICONTROL 狀態] 在查詢中，選取適當的選項按鈕。 可用的選項包括 [!UICONTROL 已提交]， [!UICONTROL 進行中]， [!UICONTROL 成功]、和 [!UICONTROL 已失敗]. 您一次只能根據一個狀態條件篩選記錄。 |
| [!UICONTROL 用戶端] | 若要根據使用的查詢使用者端篩選記錄，請在任意文字欄位中輸入下列其中一個接受的值： `API`， `Adobe Query Service UI`，或 `QsAccel`. |
| [!UICONTROL 我的查詢] | 使用 [!UICONTROL 我的查詢] 切換以篩選由您執行的查詢記錄。 |
| [!UICONTROL 查詢記錄ID] | 若要根據查詢的唯一記錄ID進行篩選，請在任意文字欄位中輸入記錄ID。 此資訊可在以下網址找到： [!UICONTROL 記錄詳細資料]. |

任何套用的篩選器都會顯示在篩選的記錄結果上方。

![「查詢」工作區的「記錄」索引標籤，並將套用的篩選器清單反白顯示。](../images/ui/query-log/applied-log-filters.png)

## 後續步驟

閱讀本檔案後，您現在能更清楚瞭解在查詢服務UI中如何存取及使用查詢記錄。

請參閱 [UI總覽](./overview.md)，或 [查詢服務API指南](../api/getting-started.md) 以進一步瞭解查詢服務功能。

請參閱 [監視查詢檔案](./monitor-queries.md) 以瞭解查詢服務如何改善已排程查詢執行的可見度。
