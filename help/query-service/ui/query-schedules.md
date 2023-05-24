---
title: 查詢計畫
description: 瞭解如何自動執行計畫查詢運行、刪除或禁用查詢計畫，以及通過Adobe Experience PlatformUI利用可用的計畫選項。
exl-id: 984d5ddd-16e8-4a86-80e4-40f51f37a975
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '748'
ht-degree: 0%

---

# 查詢計畫

您可以通過建立查詢計畫來自動運行查詢。 計畫的查詢在自定節奏上運行，以根據頻率、日期和時間管理資料。 如果需要，還可以為結果選擇輸出資料集。 已保存為模板的查詢可以從查詢編輯器計畫。

>[!IMPORTANT]
>
>以下是使用查詢編輯器時計畫查詢的限制清單。 它們不適用於 [!DNL Query Service] API:<br/>您只能向已建立、保存和運行的查詢添加計畫。<br/>你 **不能** 向參數化查詢添加計畫。<br/>計畫查詢 **不能** 包含匿名塊。

所有計畫查詢都將添加到 [!UICONTROL 計畫查詢] 頁籤。 在該工作區中，您可以通過UI監視所有計畫查詢作業的狀態。 在 [!UICONTROL 計畫查詢] 頁籤，您可以查找有關查詢運行和訂閱警報的重要資訊。 可用資訊包括運行失敗時的狀態、計畫詳細資訊和錯誤消息/代碼。 查看 [監視計畫查詢文檔](./monitor-queries.md) 的子菜單。

## 建立查詢計畫 {#create-schedule}

要向查詢添加計畫，請從 [!UICONTROL 模板] 頁籤 [!UICONTROL 計畫查詢] 頁籤。

要瞭解如何使用API添加計畫，請閱讀 [計畫查詢終結點指南](../api/scheduled-queries.md)。

從查詢編輯器訪問已保存的查詢時， [!UICONTROL 計畫] 的子菜單。 選擇 **[!UICONTROL 計畫]**。

![突出顯示了「計畫」頁籤的查詢編輯器。](../images/ui/query-schedules/schedules-tab.png)

此時將顯示計畫工作區。 選擇 **[!UICONTROL 添加計畫]** 的子菜單。

![「查詢編輯器計畫」工作區，「添加」計畫突出顯示。](../images/ui/query-schedules/add-schedule.png)

此時將顯示「計畫詳細資訊」頁。 在此頁上，您可以選擇計畫查詢的頻率、開始和結束日期、計畫查詢將運行的星期幾，以及要將查詢導出到的資料集。

![「計畫詳細資訊」面板突出顯示。](../images/ui/query-schedules/schedule-details.png)

您可以為 **[!UICONTROL 頻率]**:

- **[!UICONTROL 每小時]**:計畫查詢將在您選擇的日期期間每小時運行一次。
- **[!UICONTROL 每日]**:計畫查詢將在您選擇的時間和日期期間每X天運行一次。 請注意，所選時間在 **UTC**，而不是您的本地時區。
- **[!UICONTROL 每週]**:所選查詢將在您選擇的周、時間和日期期間的天運行。 請注意，所選時間在 **UTC**，而不是您的本地時區。
- **[!UICONTROL 每月]**:所選查詢將在您選擇的日期、時間和日期期間每月運行。 請注意，所選時間在 **UTC**，而不是您的本地時區。
- **[!UICONTROL 每年]**:所選查詢將每年在您選擇的日期、月、時間和日期期間運行。 請注意，所選時間在 **UTC**，而不是您的本地時區。

對於輸出資料集，您可以選擇使用現有資料集或建立新資料集。

>[!IMPORTANT]
>
> 由於您正在使用現有資料集或建立新資料集，因此您需要 **不** 需要包括 `INSERT INTO` 或 `CREATE TABLE AS SELECT` 作為查詢的一部分，因為資料集已設定。 包括 `INSERT INTO` 或 `CREATE TABLE AS SELECT` 作為計畫查詢的一部分將導致錯誤。

確認所有這些詳細資訊後，選擇 **[!UICONTROL 保存]** 的子菜單。 您將返回到計畫工作區，該工作區顯示新建立的計畫的詳細資訊，包括計畫ID、計畫本身和計畫的輸出資料集。 您可以使用計畫ID查找有關計畫查詢本身運行的詳細資訊。 要瞭解更多資訊，請閱讀 [計畫查詢運行終結點指南](../api/runs-scheduled-queries.md)。

![突出顯示新建立的計畫的計畫工作區。](../images/ui/query-schedules/schedules-workspace.png)

## 刪除或禁用計畫 {#delete-schedule}

可以從計畫工作區中刪除或禁用計畫。 您必須從 [!UICONTROL 模板] 頁籤 [!UICONTROL 計畫查詢] 頁籤，導航到查詢編輯器並選擇 **[!UICONTROL 計畫]** 中設定網格顏色。

從可用計畫行中選擇計畫。 可以使用切換來禁用或啟用計畫查詢。

>[!IMPORTANT]
>
>必須先禁用計畫，然後才能刪除查詢的計畫。

選擇 **[!UICONTROL 刪除計畫]** 刪除禁用的計畫。

![突出顯示了「禁用計畫」和「刪除計畫」的計畫工作區。](../images/ui/query-schedules/delete-schedule.png)
