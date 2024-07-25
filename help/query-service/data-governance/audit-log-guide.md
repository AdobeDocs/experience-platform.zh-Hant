---
title: 查詢服務稽核記錄整合
description: 查詢服務稽核記錄會維護各種使用者動作的記錄，以形成稽核軌跡，用於疑難排解問題或遵循公司資料管理政策和法規要求。 本教學課程提供查詢服務專屬稽核記錄功能的概觀。
exl-id: 5fdc649f-3aa1-4337-965f-3f733beafe9d
source-git-commit: c2832821ea6f9f630e480c6412ca07af788efd66
workflow-type: tm+mt
source-wordcount: '930'
ht-degree: 1%

---

# [!DNL Query Service]稽核記錄整合

Adobe Experience Platform [!DNL Query Service]稽核記錄整合提供查詢相關使用者動作的記錄。 稽核記錄是進行疑難排解，並遵守公司資料管理政策和法規要求的重要工具。 此功能可讓您傳回許多事件型別的動作記錄，並篩選及匯出記錄。 可透過Platform UI或[稽核查詢API](https://www.adobe.io/experience-platform-apis/references/audit-query/)存取記錄檔，並以CSV或JSON檔案格式下載。

若要瞭解有關稽核記錄使用者介面的詳細資訊，請參閱[稽核記錄概觀檔案](../../landing/governance-privacy-security/audit-logs/overview.md)。 若要進一步瞭解如何呼叫Platform API，請參閱[稽核記錄API指南](../../landing/api-guide.md)。

## 先決條件

您必須啟用[!DNL Data Governance] [!UICONTROL 檢視使用者活動記錄]許可權，才能在Platform UI中檢視稽核記錄儀表板。 已透過Adobe[Admin Console](https://adminconsole.adobe.com/)啟用許可權。 如果您沒有啟用此許可權的管理員許可權，請聯絡貴組織的管理員。 請參閱存取控制檔案以取得[透過Admin Console](../../access-control/home.md)新增許可權的完整指示。

## [!DNL Query Service]稽核記錄類別 {#audit-log-categories}

[!DNL Query Service]提供的稽核記錄類別如下。

| 類別 | 說明 |
|---|---|
| [!UICONTROL 查詢] | 此類別可讓您稽核查詢執行。 |
| [!UICONTROL 查詢範本] | 此類別可讓您稽核對查詢範本採取的各種動作（建立、更新和刪除）。 |
| [!UICONTROL 排定的查詢] | 此類別可讓您稽核在[!DNL Query Service]內建立、更新或刪除的排程。 |

## 執行[!DNL Query Service]稽核記錄 {#perform-an-audit-log}

若要執行[!DNL Query Service]活動的稽核，請從左側導覽選取&#x200B;**[!UICONTROL 稽核]**，然後選取漏斗圖示(![篩選圖示。](/help/images/icons/filter.png))以顯示篩選控制項清單，協助縮小結果範圍。

![Platform UI稽核記錄儀表板，在左側導覽中顯示「稽核」，且篩選器控制項反白顯示。](../images/audit-log/filter-controls.png)

您可以從[!UICONTROL 稽核]儀表板[!UICONTROL 活動記錄]索引標籤中，依[!DNL Query Service]類別的任何一個篩選所有記錄的平台動作。 可根據記錄結果執行的時段、執行的動作/功能或執行查詢的使用者來進一步篩選記錄結果。 請參閱稽核記錄檔案以取得[有關如何根據類別、動作、使用者和狀態來篩選記錄的完整指示](../../landing/governance-privacy-security/audit-logs/overview.md#managing-audit-logs-in-the-ui)。

傳回的稽核記錄檔資料包含符合所選篩選條件之所有查詢的下列資訊。

| 欄名稱 | 說明 |
|---|---|
| [!UICONTROL 時間戳記] | 以`month/day/year hour:minute AM/PM`格式執行之動作的確切日期和時間。 |
| [!UICONTROL 資產名稱] | [!UICONTROL 資產名稱]欄位的值取決於選擇作為篩選的類別。 使用[!UICONTROL 排程查詢]類別時，這是&#x200B;**排程名稱**。 使用[!UICONTROL 查詢範本]類別時，這是&#x200B;**範本名稱**。 使用[!UICONTROL 查詢]類別時，這是&#x200B;**工作階段識別碼** |
| [!UICONTROL 類別] | 此欄位符合您在篩選下拉式清單中選取的類別。 |
| [!UICONTROL 動作] | 這可以是建立、刪除、更新或執行。 可用的動作取決於選擇作為篩選器的類別。 |
| [!UICONTROL 使用者] | 此欄位提供執行查詢的使用者ID。 |

![已反白篩選活動記錄檔的[稽核]儀表板。](../images/audit-log/filtered-activity.png)

>[!NOTE]
>
>透過下載CSV或JSON檔案格式的記錄結果，提供的查詢詳細資訊多於稽核記錄儀表板中預設顯示的內容。

## 詳細資訊面板

選取稽核記錄結果的任一列，即可開啟畫面右側的詳細資訊面板。

![稽核儀表板活動記錄索引標籤，並反白顯示詳細資訊面板。](../images/audit-log/details-panel.png)

詳細資料面板可用來尋找[!UICONTROL 資產識別碼]和[!UICONTROL 事件狀態]。

[!UICONTROL 資產ID]的值會隨著稽核所使用的類別而變更。

* 使用[!UICONTROL 查詢]類別時，[!UICONTROL 資產識別碼]是&#x200B;**工作階段識別碼**。
* 使用[!UICONTROL 查詢範本]類別時，[!UICONTROL 資產識別碼]是&#x200B;**範本識別碼**，並加上前置詞`[!UICONTROL templateID:]`。
* 使用[!UICONTROL 排程查詢]類別時，[!UICONTROL 資產識別碼]為&#x200B;**排程識別碼**，並加上前置詞`[!UICONTROL scheduleID:]`。

[!UICONTROL 事件狀態]的值會根據稽核中使用的類別而變更。

* 使用[!UICONTROL 查詢]類別時，[!UICONTROL 事件狀態]欄位會提供使用者在該工作階段內執行的所有&#x200B;**查詢ID**&#x200B;清單。
* 使用[!UICONTROL 查詢範本]類別時，[!UICONTROL 事件狀態]欄位會提供&#x200B;**範本名稱**&#x200B;做為事件狀態的前置詞。
* 使用[!UICONTROL 查詢排程]類別時，[!UICONTROL 事件狀態]欄位會提供&#x200B;**排程名稱**&#x200B;做為事件狀態的前置詞。

## [!DNL Query Service]稽核記錄類別的可用篩選器 {#available-filters}

可用的篩選器會依下拉式清單中所選的類別而有所不同。 下表詳細說明可用於[[!DNL Query Service] 稽核記錄類別](#audit-log-categories)的篩選器。

| 篩選器 | 說明 |
|---|---|
| 類別 | 如需可用類別的完整清單，請參閱[[!DNL Query Service] 稽核記錄類別](#audit-log-categories)區段。 |
| 動作 | 參考[!DNL Query Service]稽核類別時，更新是對現有表單的&#x200B;**修改**，刪除是移除排程或範本&#x200B;**，建立是**&#x200B;建立新排程或範本&#x200B;**，執行是**&#x200B;執行查詢&#x200B;**。** |
| 使用者 | 輸入完整的使用者ID (例如johndoe@acme.com)以依使用者篩選。 |
| 狀態 | [!UICONTROL 允許]、[!UICONTROL 成功]和[!UICONTROL 失敗]選項會根據「狀態」或「事件狀態」來篩選記錄檔，而[!UICONTROL 拒絕]選項則會篩選掉&#x200B;**所有**&#x200B;記錄檔。 |
| 日期 | 選取開始日期和/或結束日期，以定義篩選結果的日期範圍。 |

## 後續步驟

閱讀本檔案可讓您更瞭解[!DNL Query Service]稽核記錄功能，以及如何使用它來篩選您的[!DNL Query Service]使用者動作。

如果您使用[!DNL Query Service]稽核記錄功能進行疑難排解，建議您閱讀[疑難排解指南](../troubleshooting-guide.md)。
