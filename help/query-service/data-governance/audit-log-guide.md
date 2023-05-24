---
title: 查詢服務審核日誌整合
description: 查詢服務審核日誌維護各種用戶操作的記錄，以形成用於排除問題或遵守公司資料管理策略和法規要求的審核跟蹤。 本教程概述了特定於查詢服務的審計日誌功能。
exl-id: 5fdc649f-3aa1-4337-965f-3f733beafe9d
source-git-commit: cde7c99291ec34be811ecf3c85d12fad09bcc373
workflow-type: tm+mt
source-wordcount: '935'
ht-degree: 2%

---

# [!DNL Query Service] 審計日誌整合

Adobe Experience Platform [!DNL Query Service] 審計日誌整合提供了與查詢相關的用戶操作的記錄。 審核日誌是故障排除和遵守公司資料管理策略和法規要求的重要工具。 該功能允許您返回許多事件類型的操作日誌，並過濾和導出記錄。 可以通過平台UI或 [審核查詢API](https://www.adobe.io/experience-platform-apis/references/audit-query/) 並以CSV或JSON檔案格式下載。

要瞭解有關審核日誌用戶介面的詳細資訊，請參閱 [審核日誌概述文檔](../../landing/governance-privacy-security/audit-logs/overview.md)。 要瞭解有關調用平台API的詳細資訊，請參閱 [審核日誌API指南](../../landing/api-guide.md)。

## 先決條件

您必須 [!DNL Data Governance] [!UICONTROL 查看用戶活動日誌] 已啟用權限，以在平台UI中查看審核日誌儀表板。 權限通過Adobe啟用 [Admin Console](https://adminconsole.adobe.com/)。 如果您沒有啟用此權限的管理員權限，請與組織的管理員聯繫。 請參閱的訪問控制文檔 [有關通過Admin Console添加權限的完整說明](../../access-control/home.md)。

## [!DNL Query Service] 審計日誌類別 {#audit-log-categories}

由提供的審核日誌類別 [!DNL Query Service] 的下界。

| 類別 | 說明 |
|---|---|
| [!UICONTROL 查詢] | 此類別允許您審計查詢執行。 |
| [!UICONTROL 查詢模板] | 此類別允許您審計對查詢模板執行的各種操作（建立、更新和刪除）。 |
| [!UICONTROL 計畫查詢] | 此類別允許您審核在中建立、更新或刪除的計畫 [!DNL Query Service]。 |

## 執行 [!DNL Query Service] 審計日誌 {#perform-an-audit-log}

執行審計 [!DNL Query Service] 活動，選擇 **[!UICONTROL 審計]** 從左導航，然後是漏斗圖表徵圖(![篩選器表徵圖。](../images/audit-log/filter.png))以顯示篩選器控制項清單，以幫助縮小結果範圍。

![左側導航和篩選器控制項中帶有「審核」的Platform UI審核日誌儀表板突出顯示。](../images/audit-log/filter-controls.png)

從 [!UICONTROL 審計] 儀表板 [!UICONTROL 活動日誌] 頁籤中，您可以通過以下任意 [!DNL Query Service] 的下界。 可以根據日誌結果被執行的時間段、所採取的操作/函式或執行查詢的用戶進一步過濾日誌結果。 請參閱的審核日誌文檔 [有關如何根據類別、操作、用戶和狀態篩選日誌的完整說明](../../landing/governance-privacy-security/audit-logs/overview.md#managing-audit-logs-in-the-ui)。

返回的審計日誌資料包含符合所選篩選條件的所有查詢的以下資訊。

| 資料行名稱 | 說明 |
|---|---|
| [!UICONTROL 時間戳記] | 在中執行的操作的確切日期和時間 `month/day/year hour:minute AM/PM` 的子菜單。 |
| [!UICONTROL 資產名稱] | 的值 [!UICONTROL 資產名稱] 欄位取決於選擇作為篩選器的類別。 使用 [!UICONTROL 計畫查詢] 類別 **計畫名稱**。 使用 [!UICONTROL 查詢模板] 類別，這是 **模板名稱**。 使用 [!UICONTROL 查詢] 類別，這是 **會話ID** |
| [!UICONTROL 類別] | 此欄位與您在篩選器下拉清單中選擇的類別匹配。 |
| [!UICONTROL 動作] | 這可以是建立、刪除、更新或執行。 可用操作取決於選擇作為篩選器的類別。 |
| [!UICONTROL 使用者] | 此欄位提供執行查詢的用戶ID。 |

![「審核」儀表板，其中已篩選的活動日誌突出顯示。](../images/audit-log/filtered-activity.png)

>[!NOTE]
>
>通過以CSV或JSON檔案格式下載日誌結果，提供了比審計日誌儀表板中預設顯示的更多查詢詳細資訊。

## 詳細資訊面板

選擇任何行的審核日誌結果以開啟螢幕右側的詳細資訊面板。

![審核儀表板「活動日誌」頁籤，其中突出顯示了「詳細資訊」面板。](../images/audit-log/details-panel.png)

詳細資訊面板可用於查找 [!UICONTROL 資產ID] 和 [!UICONTROL 事件狀態]。

的值 [!UICONTROL 資產ID] 根據審計中使用的類別進行更改。

* 使用 [!UICONTROL 查詢] 的 [!UICONTROL 資產ID] 是  **會話ID**。
* 使用 [!UICONTROL 查詢模板] 的 [!UICONTROL 資產ID] 是 **模板ID** 加上 `[!UICONTROL templateID:]`。
* 使用 [!UICONTROL 計畫查詢] 的 [!UICONTROL 資產ID] 是  **計畫ID** 加上 `[!UICONTROL scheduleID:]`。

的值 [!UICONTROL 事件狀態] 根據審計中使用的類別進行更改。

* 使用 [!UICONTROL 查詢] 的 [!UICONTROL 事件狀態] 欄位提供所有 **查詢ID** 由用戶在該會話中執行。
* 使用 [!UICONTROL 查詢模板] 的 [!UICONTROL 事件狀態] 欄位提供 **模板名稱** 作為事件狀態的前置詞。
* 使用 [!UICONTROL 查詢計畫] 的 [!UICONTROL 事件狀態] 欄位提供 **計畫名稱** 作為事件狀態的前置詞。

## 可用篩選器 [!DNL Query Service] 審計日誌類別 {#available-filters}

可用篩選器因下拉清單中選擇的類別而異。 下表詳細說明了可用於 [[!DNL Query Service] 審計日誌類別](#audit-log-categories)。

| 篩選 | 說明 |
|---|---|
| 類別 | 查看 [[!DNL Query Service] 審計日誌類別](#audit-log-categories) 的子菜單。 |
| 動作 | 當指的是 [!DNL Query Service] 審計類別，更新是 **對現有窗體的修改**，刪除為 **刪除計畫或模板**，建立 **建立新計畫或模板**，並執行 **運行查詢**。 |
| 使用者 | 輸入要按用戶篩選的完整用戶ID(例如johndoe@acme.com)。 |
| 狀態 | 的 [!UICONTROL 允許]。 [!UICONTROL 成功], [!UICONTROL 失敗] 選項根據「狀態」或「事件狀態」篩選日誌，而 [!UICONTROL 拒絕] 選項篩選出 **全部** 日誌。 |
| 日期 | 選擇起始日期和/或終止日期以定義日期範圍以篩選結果。 |

## 後續步驟

通過閱讀此文檔，您可以 [!DNL Query Service] 審計日誌功能以及如何使用它篩選 [!DNL Query Service] 用戶操作。

如果使用 [!DNL Query Service] 為排除故障，建議您閱讀 [故障排除指南](../troubleshooting-guide.md)。
