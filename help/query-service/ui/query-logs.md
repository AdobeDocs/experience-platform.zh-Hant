---
title: 查詢記錄檔
description: 每次執行查詢時都會自動產生查詢記錄，並可透過UI使用，以協助進行疑難排解。 本檔案概述如何使用和導覽UI的「查詢服務記錄檔」區段。
source-git-commit: 95d3604a9589a4d0db7e426dd000ddec9cd4f2ce
workflow-type: tm+mt
source-wordcount: '585'
ht-degree: 0%

---

# 查詢記錄檔

>[!IMPORTANT]
>
>某些查詢記錄功能目前處於有限版本中，並非所有客戶都能使用。 若沒有編輯圖示，您的UI可能會呈現稍微不同的外觀。 此外，選取查詢名稱的程式可導覽至「查詢編輯器」，而非 [!UICONTROL 查詢日誌詳細資訊] 檢視。

Adobe Experience Platform會維護透過API和UI發生的所有查詢事件記錄。 此資訊可在查詢服務UI中，從 [!UICONTROL 記錄檔] 標籤。

日誌檔案由任何查詢事件自動生成，並包含包括所使用的SQL、查詢的狀態、所用時間和上次運行時間等資訊。 您可以使用查詢日誌資料作為功能強大的工具，用於排除低效或有問題的查詢。 更全面的記錄資訊會保留為稽核記錄功能的一部分，可在 [稽核記錄檔案](../../landing/governance-privacy-security/audit-logs/overview.md).

## 檢查查詢日誌

要檢查查詢日誌，請選擇 [!UICONTROL 查詢] 導覽至「查詢服務」工作區，然後選取 [!UICONTROL 記錄檔] 中。

![反白顯示查詢和記錄的Platform UI。](../images/ui/query-log/logs.png)

## 自訂和搜尋 {#customize-and-search}

查詢服務日誌以可自定義的表格格式顯示。 若要自訂表格欄，請選取設定圖示(![設定圖示。](../images/ui/query-log/settings-icon.png))即可取得Advertising Cloud的說明。 A [!UICONTROL 自訂表格] 對話框出現，可取消選擇每列。

您也可以在搜尋欄位中輸入範本名稱，以搜尋與特定查詢範本相關的記錄檔。

![反白顯示「查詢記錄工作區」(Querys Log workspace with the search bar and manage column table)下拉式清單。](../images/ui/query-log/customize-logs.png)

A [記錄表各列的說明](./overview.md#log) 可在「查詢服務」概覽的「記錄」區段中找到。

## 發現日誌資料

每一列代表與查詢範本相關聯的查詢執行的記錄資料。 從表格中選取任何一列，將該執行的記錄資料填入右側側欄。

![選中一行的「查詢日誌」工作區，右側邊欄中突出顯示日誌資料。](../images/ui/query-log/log-details.png)

在日誌詳細資訊面板中，您可以選擇新的輸出資料集，並查看或複製運行中使用的完整SQL查詢。

![選中一行的「查詢日誌」工作區，並突出顯示輸出資料集和SQL查詢。](../images/ui/query-log/edit-output-dataset.png)

>[!IMPORTANT]
>
>某些查詢記錄功能目前處於有限版本中，並非所有客戶都能使用。

您也可以從 [!UICONTROL 名稱] 欄以直接導覽至 [!UICONTROL 查詢日誌詳細資訊] 檢視。

>[!NOTE]
>
>如果查詢是使用API建立的，在初始化期間未提供任何模板名稱，則會改為顯示SQL查詢的前幾個字元。

![查詢日誌詳細資訊視圖。](../images/ui/query-log/query-log-details.png)

每一列的範本名稱或SQL程式碼片段旁都是鉛筆圖示(![鉛筆圖示。](../images/ui/query-log/edit-icon.png))，以導覽至查詢編輯器。 然後，查詢會預先填入編輯器中以進行編輯。

![以鉛筆圖示反白顯示「查詢記錄」工作區。](../images/ui/query-log/edit-query.png)

## 後續步驟

閱讀本檔案後，您現在更清楚了解查詢服務UI中如何存取及使用查詢記錄檔。

請參閱 [UI概述](./overview.md)，或 [查詢服務API指南](../api/getting-started.md) 以進一步了解Query Service功能。

請參閱 [監視查詢文檔](./monitor-queries.md) 了解查詢服務如何改善已排程查詢執行的可見性。
