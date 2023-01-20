---
title: 查詢排程
description: 了解如何透過Adobe Experience Platform UI自動執行已排程的查詢執行、刪除或停用查詢排程，以及運用可用的排程選項。
source-git-commit: cde7c99291ec34be811ecf3c85d12fad09bcc373
workflow-type: tm+mt
source-wordcount: '748'
ht-degree: 0%

---

# 查詢排程

您可以透過建立查詢排程來自動執行查詢。 排程的查詢會在自訂順序上執行，以根據頻率、日期和時間管理您的資料。 您也可以視需要為結果選擇輸出資料集。 已另存為範本的查詢可從查詢編輯器排程。

>[!IMPORTANT]
>
>以下是使用查詢編輯器時排程查詢的限制清單。 它們不適用於 [!DNL Query Service] API:<br/>您只能將排程新增至已建立、儲存及執行的查詢。<br/>您 **不能** 將計畫添加到參數化查詢。<br/>排程查詢 **不能** 包含匿名塊。

任何已排程的查詢都會新增至 [!UICONTROL 排程查詢] 標籤。 從該工作區，您可以透過UI監控所有已排程查詢作業的狀態。 在 [!UICONTROL 排程查詢] 索引標籤，您可以找到有關查詢執行和訂閱警報的重要資訊。 可用資訊包括狀態、排程詳細資訊，以及執行失敗時的錯誤訊息/代碼。 請參閱 [監視計畫查詢文檔](./monitor-queries.md) 以取得更多資訊。

## 建立查詢排程 {#create-schedule}

若要將排程新增至查詢，請從 [!UICONTROL 範本] 標籤或 [!UICONTROL 排程查詢] 頁簽，導覽至查詢編輯器。

若要了解如何使用API新增排程，請參閱 [排程查詢端點指南](../api/scheduled-queries.md).

從查詢編輯器存取儲存的查詢時， [!UICONTROL 排程] 索引標籤會顯示在查詢名稱下方。 選擇 **[!UICONTROL 排程]**.

![突出顯示「調度」頁簽的查詢編輯器。](../images/ui/query-schedules/schedules-tab.png)

排程工作區隨即出現。 選擇 **[!UICONTROL 新增排程]** 來建立排程。

![查詢編輯器排程工作區中，已反白顯示新增排程。](../images/ui/query-schedules/add-schedule.png)

此時將顯示「計畫詳細資訊」頁。 在此頁面上，您可以選擇已排程查詢的頻率、開始和結束日期、已排程查詢將執行的一週中的某天，以及要匯出查詢的資料集。

![「計畫詳細資訊」面板突出顯示。](../images/ui/query-schedules/schedule-details.png)

您可以選擇下列選項 **[!UICONTROL 頻率]**:

- **[!UICONTROL 每小時]**:在您選取的日期期間，排程查詢將每小時執行一次。
- **[!UICONTROL 每日]**:排程查詢會在您選取的時間和日期期間，每X天執行一次。 請注意，所選時間在 **UTC**，而非您的當地時區。
- **[!UICONTROL 每週]**:選定的查詢將在您選擇的一週天數、時間和日期期間運行。 請注意，所選時間在 **UTC**，而非您的當地時區。
- **[!UICONTROL 每月]**:選定的查詢將在您選擇的日、時和日期期間每月運行。 請注意，所選時間在 **UTC**，而非您的當地時區。
- **[!UICONTROL 每年]**:選定的查詢將每年在您選擇的日、月、時間和日期期間運行。 請注意，所選時間在 **UTC**，而非您的當地時區。

針對輸出資料集，您可以選擇使用現有資料集或建立新資料集。

>[!IMPORTANT]
>
> 由於您使用現有資料集或建立新資料集， **not** 需要包括 `INSERT INTO` 或 `CREATE TABLE AS SELECT` 做為查詢的一部分，因為資料集已設定。 包括 `INSERT INTO` 或 `CREATE TABLE AS SELECT` 作為排程查詢的一部分，將會導致錯誤。

確認所有這些詳細資訊後，請選取 **[!UICONTROL 儲存]** 來建立排程。 系統會將您返回到計畫工作區，該工作區顯示新建立的計畫的詳細資訊，包括計畫ID、計畫本身和計畫的輸出資料集。 您可以使用排程ID來查詢有關排程查詢本身執行的詳細資訊。 若要進一步了解，請閱讀 [排程查詢執行端點指南](../api/runs-scheduled-queries.md).

![重新建立的排程會反白顯示排程工作區。](../images/ui/query-schedules/schedules-workspace.png)

## 刪除或禁用計畫 {#delete-schedule}

您可以從排程工作區中刪除或停用排程。 您必須從 [!UICONTROL 範本] 標籤或 [!UICONTROL 排程查詢] 頁簽，導航到查詢編輯器並選擇 **[!UICONTROL 排程]** 來存取排程工作區。

從可用排程的列中選取排程。 您可以使用切換來停用或啟用排程查詢。

>[!IMPORTANT]
>
>您必須先停用排程，才能刪除查詢的排程。

選擇 **[!UICONTROL 刪除排程]** 刪除禁用的計畫。

![會反白顯示「停用排程」和「刪除排程」的排程工作區。](../images/ui/query-schedules/delete-schedule.png)


