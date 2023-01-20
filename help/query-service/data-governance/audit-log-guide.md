---
title: 查詢服務審核日誌整合
description: 查詢服務審核日誌維護各種用戶操作的記錄，以形成用於故障排除問題或遵守公司資料管理策略和法規要求的審核跟蹤。 本教學課程概述Query Service專用的稽核記錄功能。
exl-id: 5fdc649f-3aa1-4337-965f-3f733beafe9d
source-git-commit: cde7c99291ec34be811ecf3c85d12fad09bcc373
workflow-type: tm+mt
source-wordcount: '935'
ht-degree: 2%

---

# [!DNL Query Service] 稽核記錄整合

Adobe Experience Platform [!DNL Query Service] 稽核記錄整合提供查詢相關使用者動作的記錄。 稽核記錄是疑難排解和遵循公司資料管理政策和法規要求的重要工具。 此功能可讓您傳回許多事件類型的動作記錄，並篩選及匯出記錄。 可透過Platform UI或 [稽核查詢API](https://www.adobe.io/experience-platform-apis/references/audit-query/) 和下載為CSV或JSON檔案格式。

若要進一步了解稽核記錄使用者介面，請參閱 [審核日誌概述文檔](../../landing/governance-privacy-security/audit-logs/overview.md). 若要進一步了解如何呼叫Platform API，請參閱 [稽核記錄API指南](../../landing/api-guide.md).

## 先決條件

您必須擁有 [!DNL Data Governance] [!UICONTROL 查看用戶活動日誌] 已啟用在Platform UI中檢視稽核記錄控制面板的權限。 權限會透過Adobe啟用 [Admin Console](https://adminconsole.adobe.com/). 如果您沒有啟用此權限的管理員權限，請與貴組織的管理員聯繫。 請參閱存取控制檔案，以取得 [透過Admin Console新增權限的完整指示](../../access-control/home.md).

## [!DNL Query Service] 審計日誌類別 {#audit-log-categories}

提供的審核日誌類別 [!DNL Query Service] 如下所示。

| 類別 | 說明 |
|---|---|
| [!UICONTROL 查詢] | 此類別允許您審核查詢執行。 |
| [!UICONTROL 查詢範本] | 此類別可讓您稽核對查詢範本採取的各種動作（建立、更新和刪除）。 |
| [!UICONTROL 排程查詢] | 此類別可讓您稽核已在中建立、更新或刪除的排程 [!DNL Query Service]. |

## 執行 [!DNL Query Service] 稽核記錄 {#perform-an-audit-log}

要執行審核，請執行以下操作 [!DNL Query Service] 活動，選取 **[!UICONTROL 稽核]** 從左側導覽，後面接著漏斗圖示(![篩選圖示。](../images/audit-log/filter.png))以顯示篩選控制項清單，以縮小結果範圍。

![Platform UI稽核記錄控制面板左側導覽中顯示「稽核」，並反白顯示篩選控制項。](../images/audit-log/filter-controls.png)

從 [!UICONTROL 稽核] 儀表板 [!UICONTROL 活動記錄] 標籤中，您可以依 [!DNL Query Service] 類別。 可以根據執行的時段、採取的動作/函式或頒布查詢的使用者，進一步篩選記錄結果。 請參閱稽核記錄檔案，以取得 [如何根據類別、動作、使用者和狀態篩選記錄的完整指示](../../landing/governance-privacy-security/audit-logs/overview.md#managing-audit-logs-in-the-ui).

傳回的稽核記錄資料包含符合您所選篩選條件之所有查詢的下列資訊。

| 資料行名稱 | 說明 |
|---|---|
| [!UICONTROL 時間戳記] | 在 `month/day/year hour:minute AM/PM` 格式。 |
| [!UICONTROL 資產名稱] | 的值 [!UICONTROL 資產名稱] 欄位取決於選擇作為篩選的類別。 使用 [!UICONTROL 排程查詢] 類別，這是 **排程名稱**. 使用 [!UICONTROL 查詢範本] 類別，這是 **範本名稱**. 使用 [!UICONTROL 查詢] 類別，這是 **工作階段ID** |
| [!UICONTROL 類別] | 此欄位符合您在篩選下拉式清單中選取的類別。 |
| [!UICONTROL 動作] | 這可以是建立、刪除、更新或執行。 可用的動作取決於選擇作為篩選的類別。 |
| [!UICONTROL 使用者] | 此欄位提供執行查詢的使用者ID。 |

![「稽核」控制面板中會反白顯示篩選的活動記錄。](../images/audit-log/filtered-activity.png)

>[!NOTE]
>
>比起預設顯示在稽核記錄控制面板中，以CSV或JSON檔案格式下載記錄結果，可提供更多查詢詳細資料。

## 詳細資訊面板

選取稽核記錄結果的任何一列，以開啟畫面右側的「詳細資訊」面板。

![稽核控制面板活動記錄索引標籤，並反白顯示詳細資訊面板。](../images/audit-log/details-panel.png)

「詳細資訊」面板可用來尋找 [!UICONTROL 資產ID] 和 [!UICONTROL 事件狀態].

的值 [!UICONTROL 資產ID] 會根據稽核中使用的類別而變更。

* 使用 [!UICONTROL 查詢] 類別， [!UICONTROL 資產ID] 是  **工作階段ID**.
* 使用 [!UICONTROL 查詢範本] 類別， [!UICONTROL 資產ID] 是 **範本ID** 加上前置詞 `[!UICONTROL templateID:]`.
* 使用 [!UICONTROL 排程查詢] 類別， [!UICONTROL 資產ID] 是  **排程ID** 加上前置詞 `[!UICONTROL scheduleID:]`.

的值 [!UICONTROL 事件狀態] 會根據稽核中使用的類別而變更。

* 使用 [!UICONTROL 查詢] 類別， [!UICONTROL 事件狀態] 欄位提供所有 **查詢ID** 由該工作階段內的使用者執行。
* 使用 [!UICONTROL 查詢範本] 類別， [!UICONTROL 事件狀態] 欄位提供 **範本名稱** 作為事件狀態的前置詞。
* 使用 [!UICONTROL 查詢排程] 類別， [!UICONTROL 事件狀態] 欄位提供 **排程名稱** 作為事件狀態的前置詞。

## 適用於 [!DNL Query Service] 審計日誌類別 {#available-filters}

可用的篩選器會依下拉式清單中選取的類別而有所不同。 下表詳細說明了可用的篩選器 [[!DNL Query Service] 審計日誌類別](#audit-log-categories).

| 篩選 | 說明 |
|---|---|
| 類別 | 請參閱 [[!DNL Query Service] 審計日誌類別](#audit-log-categories) 區段，以取得可用類別的完整清單。 |
| 動作 | 當參考 [!DNL Query Service] 審核類別，更新是 **修改為現有表單**，刪除即為 **移除排程或範本**，建立為 **建立新計畫或模板**，則執行 **運行查詢**. |
| 使用者 | 輸入要依使用者篩選的完整使用者ID(例如，johndoe@acme.com)。 |
| 狀態 | 此 [!UICONTROL 允許], [!UICONTROL 成功]，和 [!UICONTROL 失敗] 選項會根據「狀態」或「事件狀態」來篩選記錄，而 [!UICONTROL 拒絕] 選項將篩選 **all** 記錄檔。 |
| 日期 | 選取開始日期和/或結束日期，以定義要依據篩選結果的日期範圍。 |

## 後續步驟

閱讀本檔案，您便能更清楚了解 [!DNL Query Service] 稽核記錄功能，以及如何用來篩選您的 [!DNL Query Service] 使用者動作。

如果您使用 [!DNL Query Service] 用於疑難排解目的的稽核記錄功能，建議您閱讀 [疑難排解指南](../troubleshooting-guide.md).
