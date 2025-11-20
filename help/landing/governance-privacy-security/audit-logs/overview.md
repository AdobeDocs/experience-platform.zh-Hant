---
title: 稽核記錄概觀
description: 了解稽核紀錄如何讓您查看誰在 Adobe Experience Platform 中執行了哪些操作。
role: Admin,Developer
feature: Audits
exl-id: 00baf615-5b71-4e0a-b82a-ca0ce8566e7f
source-git-commit: d6575e44339ea41740fa18af07ce5b893f331488
workflow-type: tm+mt
source-wordcount: '1579'
ht-degree: 29%

---

# 稽核記錄 {#audit-logs}

>[!CONTEXTUALHELP]
>id="platform_audits_privacyconsole_actions"
>title="熱門動作"
>abstract="此小工具會顯示在所選時間範圍內在 Experience Platform 最常執行的動作類型。若要查看 Experience Platform 中記錄的動作的完整清單，請在左側導覽中選取「**稽核**」。"

>[!CONTEXTUALHELP]
>id="platform_audits_privacyconsole_users"
>title="熱門使用者"
>abstract="此小工具會顯示在所選時間範圍於 Experience Platform 執行最多動作的使用者。若要查看 Experience Platform 中記錄的動作的完整清單，請在左側導覽中選取「**稽核**」。"

>[!CONTEXTUALHELP]
>id="platform_privacyConsole_audits_description"
>title="監控 Experience Platform 中的使用者活動"
>abstract="<h2>說明</h2><p>您可以採用稽核記錄的形式監控各種 Experience Platform 服務和功能的使用者活動。這些記錄會形成稽核軌跡，其中記錄<b>什麼人</b>在<b>什麼時間</b>執行了<b>什麼動作</b>。稽核記錄可以幫助解決 Experience Platform 上的問題，並幫助您的企業有效地遵守公司資料管理原則和監管需求。</p>"

為了提高系統中所執行活動的透明度和可見度，Adobe Experience Platform可讓您以「稽核記錄」的形式，稽核各種服務和功能的使用者活動。 這些記錄形成了稽核軌跡，可以幫助對Experience Platform問題進行疑難排解，並幫助您的企業有效遵守公司資料管理政策和監管要求。

基本上，稽核記錄會告知&#x200B;**誰**&#x200B;執行了&#x200B;**什麼**&#x200B;動作，以及&#x200B;**何時**。 記錄中記錄的每個動作都包含中繼資料，其指出動作型別、日期和時間、執行動作之使用者的電子郵件ID，以及與動作型別相關的其他屬性。

當使用者執行動作時，會記錄兩種型別的稽核事件。 核心事件擷取動作[!UICONTROL allow]或[!UICONTROL deny]的授權結果，而增強型事件則擷取執行結果[!UICONTROL success]或[!UICONTROL failure]。 多個增強型事件可連結至相同的核心事件。 例如，啟用目的地時，核心事件會記錄[!UICONTROL Destination Update]動作的授權，而增強型事件會記錄多個[!UICONTROL Segment Activate]動作。

>[!NOTE]
>
> 在&#x200B;**角色**&#x200B;資源中，動作&#x200B;**新增使用者**&#x200B;和&#x200B;**移除使用者**&#x200B;的中繼資料不會包含執行動作之使用者的電子郵件識別碼。 記錄檔而是會顯示系統產生的電子郵件ID (system@adobe.com)。

本文件涵蓋了 Experience Platform 中的稽核日誌，包括如何在 UI 或 API 中查看和管理日誌。

## 由稽核記錄擷取的事件類型 {#category}

下表說明審計日誌記錄哪些資源的行動：

| 資源 | 動作 |
| --- | --- |
| [存取控制原則（以屬性為基礎的存取控制）](../../../access-control/home.md) | <ul><li>建立</li><li>更新</li><li>刪除</li></ul> |
| [帳號（Adobe）](../../../sources/connectors/tutorials/ui/../../../tutorials/ui/update.md) | <ul><li>建立</li><li>更新</li><li>刪除</li></ul> |
| [Attribution AI執行個體](../../../intelligent-services/attribution-ai/overview.md) | <ul><li>建立</li><li>更新</li><li>刪除</li><li>啟用</li><li>停用</li></ul> |
| [稽核記錄](../../../landing/governance-privacy-security/audit-logs/overview.md) | <ul><li>匯出</li></ul> |
| [類別](../../../xdm/schema/composition.md#class) | <ul><li>建立</li><li>更新</li><li>刪除</li></ul> |
| 計算屬性 | <ul><li>建立</li><li>更新</li><li>刪除</li></ul> |
| [Customer AI執行個體](../../../intelligent-services/customer-ai/overview.md) | <ul><li>建立</li><li>更新</li><li>刪除</li><li>啟用</li><li>停用</li></ul> |
| [資料集](../../../catalog/datasets/overview.md) | <ul><li>建立</li><li>更新</li><li>刪除</li><li>為[即時客戶設定檔](../../../profile/home.md)啟用</li><li>為輪廓停用</li><li>新增資料</li><li>刪除批次</li></ul> |
| [資料流](../../../datastreams/overview.md) | <ul><li>建立</li><li>更新</li><li>刪除</li><li>啟用</li><li>停用</li><li>[編輯對應](../../../datastreams/data-prep.md)</li></ul> |
| [資料類型](../../../xdm/schema/composition.md#data-type) | <ul><li>建立</li><li>更新</li><li>刪除</li></ul> |
| [目標](../../../destinations/home.md) | <ul><li>建立</li><li>更新</li><li>刪除</li><li>啟用</li><li>停用</li><li>資料集啟用</li><li>資料集移除</li><li>輪廓啟用</li><li>輪廓移除</li></ul> |
| [欄位群組](../../../xdm/schema/composition.md#field-group) | <ul><li>建立</li><li>更新</li><li>刪除</li></ul> |
| [恆等圖](../../../identity-service/features/identity-graph-viewer.md) | <ul><li>檢視</li></ul> |
| [身份命名空間](../../../identity-service/features/namespaces.md) | <ul><li>建立</li><li>更新</li></ul> |
| [合併原則](../../../profile/merge-policies/overview.md) | <ul><li>建立</li><li>更新</li><li>刪除</li></ul> |
| [產品設定檔](../../../access-control/home.md) | <ul><li>建立</li><li>更新</li><li>刪除</li></ul> |
| [查詢](../../../query-service/ui/overview.md) | <ul><li>執行</li></ul> |
| [查詢範本](../../../query-service/ui/overview.md) | <ul><li>建立</li><li>更新</li><li>刪除</li></ul> |
| [角色（基於屬性的存取控制）](../../../access-control/home.md) | <ul><li>建立</li><li>更新</li><li>刪除</li><li>新增使用者</li><li>移除使用者</li></ul> |
| [沙箱](../../../sandboxes/home.md) | <ul><li>建立</li><li>更新</li><li>重設</li><li>刪除</li></ul> |
| [排定的查詢](../../../query-service/ui/overview.md) | <ul><li>建立</li><li>更新</li><li>刪除</li></ul> |
| [結構描述](../../../xdm/schema/composition.md) | <ul><li>建立</li><li>更新</li><li>刪除</li><li>為輪廓啟用</li></ul> |
| [區段](../../../segmentation/home.md) | <ul><li>建立</li><li>刪除</li><li>區段啟用</li><li>區段移除</li></ul> |
| [Source資料流程](../../../sources/connectors/tutorials/ui/../../../tutorials/ui/update.md) | <ul><li>建立</li><li>更新</li><li>刪除</li><li>啟用</li><li>停用</li><li>資料集啟用</li><li>資料集移除</li><li>設定檔啟用</li><li>輪廓移除</li></ul> |
| [工作訂單](../../../hygiene/home.md) | <ul><li>建立</li></ul> |

## 存取稽核日誌

當您的組織啟用此功能時，審計日誌會隨著活動發生自動被收集。 您不需要手動啟用記錄收集。

要查看和匯出稽核日誌，您必須取得 **[!UICONTROL View User Activity Log]** 存取控制權限（可在分類中 [!UICONTROL Data Governance] 取得）。 欲了解如何管理 Experience Platform 功能的個別權限，請參閱 [存取控制文件](../../../access-control/home.md)。

## 在 UI 中管理稽核記錄 {#managing-audit-logs-in-the-ui}

>[!CONTEXTUALHELP]
>id="platform_privacyConsole_audits_instructions"
>title="說明"
>abstract="<ul><li>在左側導覽中選取<b>稽核</b>。「稽核」工作區會顯示已記錄的記錄清單，依預設會從時間最近的開始排序。</li>   <li> 注意：稽核記錄會保留 365 天，超過此天數將從系統中刪除。因此，您最多只能往回查看 365 天。如果您需要查看超過 365 天的資料，您應該定期匯出記錄以符合您的內部原則需求。 </li><li>從清單中選取一個事件以在右邊欄中查看其詳細資料。 </li><li>選取漏斗圖示以顯示篩選控制項清單，可協助縮小結果範圍。僅顯示最後 1,000 條記錄，無論選取的篩選器為何。 </li><li>若要匯出目前的稽核記錄清單，請選取&#x200B;**下載記錄**。</li><li>如需有關此功能的更多說明，請參閱 Experience League 上的<a href="https://experienceleague.adobe.com/docs/experience-platform/landing/governance-privacy-security/audit-logs/overview.html?lang=zh-Hant">稽核記錄概觀</a>。</li></ul>"

你可以在 Experience Platform UI 中查看 Experience Platform 功能中不同功能的 **[!UICONTROL Audits]** 稽核日誌。 工作區會顯示一份記錄日誌清單，預設依最新到最近排序。

![左側選單中「稽核」儀表板，重點顯示稽核。](../../images/audit-logs/audits.png)

稽核日誌會保留365天，之後會從系統中刪除。 若您需要超過 365 天的資料，應以定期匯出日誌以符合內部政策要求。

你申請稽核日誌的方式會改變允許的時間範圍和你可存取的紀錄數量。 [匯出日誌](#export-audit-logs) 可以讓你回溯 365 天（以 90 天為單位）回溯到最多 10,000 筆審計日誌（核心或增強版），而 [Experience Platform 的活動日誌介面](#filter-audit-logs) 則顯示過去 90 天最多 1,000 個核心事件，每個事件都有相應的強化事件。

從清單中選取一個事件以在右邊欄中查看其詳細資料。

![審計儀表板活動日誌標籤，並標示事件詳情面板。](../../images/audit-logs/select-event.png)

### 過濾器稽核日誌

選取funnel圖示（![篩選圖示](/help/images/icons/filter.png)）以顯示篩選控制項清單，協助縮小結果範圍。

>[!NOTE]
>
>Experience Platform UI只會顯示過去90天最多1000個核心事件，每個事件都有對應的增強事件，無論套用的篩選器為何。 如果您需要超過該天的記錄（最多365天），您需要[匯出稽核記錄](#export-audit-logs)。

![已反白篩選活動記錄檔的[稽核]儀表板。](../../images/audit-logs/filters.png)

下列篩選器可用於UI中的稽核事件：

| 篩選器 | 說明 |
| --- | --- |
| [!UICONTROL Category] | 使用下拉式功能表，依[類別](#category)篩選顯示的結果。 |
| [!UICONTROL Action] | 依動作篩選。 每項服務的可用動作會顯示在資源表格中。 |
| [!UICONTROL User] | 輸入完整的使用者識別碼（例如，`johndoe@acme.com`）以依使用者篩選。 |
| [!UICONTROL Status] | 依結果篩選稽核事件：成功、失敗、允許或拒絕，因為缺少[存取控制](../../../access-control/home.md)許可權。 對於已執行的動作，核心事件顯示[!UICONTROL Allow]或[!UICONTROL Deny]。 當核心事件為[!UICONTROL Allow]時，它可能已附加一或多個顯示&#x200B;**[!UICONTROL Success]**&#x200B;或&#x200B;**[!UICONTROL Failure]**&#x200B;的增強型事件。 例如，成功的動作在核心事件上顯示[!UICONTROL Allow]，在附加的增強事件上顯示[!UICONTROL Success]。 |
| [!UICONTROL Date] | 選取開始日期和/或結束日期，以定義篩選結果的日期範圍。 可匯出回顧期間為90天的資料（例如，2021-12-15至2022-03-15）。 這可能因事件型別而異。 |

若要移除濾鏡，請針對有問題的濾鏡選取藥丸圖示上的「X」，或選取&#x200B;**[!UICONTROL Clear all]**&#x200B;以移除所有濾鏡。

![反白顯示具有清除篩選器的稽核儀表板。](../../images/audit-logs/clear-filters.png)

傳回的稽核記錄檔資料包含符合所選篩選條件之所有查詢的下列資訊。

| 欄名稱 | 說明 |
|---|---|
| [!UICONTROL Timestamp] | 以`month/day/year hour:minute AM/PM`格式執行之動作的確切日期和時間。 |
| [!UICONTROL Asset Name] | [!UICONTROL Asset Name]欄位的值取決於選擇作為篩選的類別。 |
| [!UICONTROL Category] | 此欄位符合在篩選下拉式清單中選取的類別。 |
| [!UICONTROL Action] | 可用的動作取決於選擇作為篩選器的類別。 |
| [!UICONTROL User] | 此欄位提供執行查詢的使用者ID。 |

![已反白篩選活動記錄檔的[稽核]儀表板。](../../images/audit-logs/filtered.png)

### 匯出稽核記錄 {#export-audit-logs}

若要匯出目前的稽核記錄清單，請選取&#x200B;**[!UICONTROL Download log]**。

>[!NOTE]
>
>可在90天間隔內要求記錄檔，最多可達365天過去。 然而，單一匯出期間可傳回的最大記錄數量為10,000個稽核事件（核心或增強功能）。

![反白顯示[!UICONTROL Download log]的稽核儀表板。](../../images/audit-logs/download.png)

在出現的對話方塊中，選取您偏好的格式（**[!UICONTROL CSV]**&#x200B;或&#x200B;**[!UICONTROL JSON]**），然後選取&#x200B;**[!UICONTROL Download]**。 瀏覽器會下載產生的檔案，並將其儲存到您的電腦。

![反白顯示[!UICONTROL Download]的檔案格式選取對話方塊。](../../images/audit-logs/select-download-format.png)

## 啟用警示 {#enable-alerts}

您可以啟用稽核警示來接收下列規則的通知：

* 客群建立
* 客群更新
* 客群刪除
* 資料集建立
* 資料集更新
* 資料集刪除
* 結構描述建立
* 結構描述更新
* 結構描述刪除

從清單中選取所需的警報，以訂閱接收通知。 如需警示的詳細資訊，請參閱[使用UI訂閱警示](../../../observability/alerts/ui.md)的指南。

## 管理API中的稽核記錄

所有可以在UI中執行的動作，也可以使用API呼叫來完成。 如需詳細資訊，請參閱[API參考檔案](https://www.adobe.io/experience-platform-apis/references/audit-query/)。

## 管理Adobe Admin Console的稽核記錄

若要瞭解如何管理Adobe Admin Console中活動的稽核記錄，請參閱下列[檔案](https://helpx.adobe.com/tw/enterprise/using/audit-logs.html)。

## 下一步與額外資源

本指南涵蓋了如何在 Experience Platform 管理稽核日誌。 欲了解更多如何監控 Experience Platform 活動的資訊，請參閱有關 [可觀察性洞察](../../../observability/home.md) 與 [監控資料擷取](../../../ingestion/quality/monitor-data-ingestion.md)的文件。

為了加強你對 Experience Platform 審計日誌的理解，請觀看以下影片：

>[!VIDEO](https://video.tv.adobe.com/v/341450?quality=12&learn=on)
