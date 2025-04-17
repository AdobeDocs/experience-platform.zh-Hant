---
title: 稽核記錄概觀
description: 了解稽核紀錄如何讓您查看誰在 Adobe Experience Platform 中執行了哪些操作。
role: Admin,Developer
feature: Audits
exl-id: 00baf615-5b71-4e0a-b82a-ca0ce8566e7f
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1476'
ht-degree: 32%

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

>[!NOTE]
>
> 在&#x200B;**角色**&#x200B;資源中，動作&#x200B;**新增使用者**&#x200B;和&#x200B;**移除使用者**&#x200B;的中繼資料不會包含執行動作之使用者的電子郵件識別碼。 記錄檔而是會顯示系統產生的電子郵件ID (system@adobe.com)。

本檔案涵蓋Experience Platform中的稽核記錄，包括如何在UI或API中檢視和管理它們。

## 由稽核記錄擷取的事件類型 {#category}

下表概述稽核記錄針對哪些資源所記錄的動作：

| 資源 | 動作 |
| --- | --- |
| [存取控制原則（以屬性為基礎的存取控制）](../../../access-control/home.md) | <ul><li>建立</li><li>更新</li><li>刪除</li></ul> |
| [帳戶(Adobe)](../../../sources/connectors/tutorials/ui/../../../tutorials/ui/update.md) | <ul><li>建立</li><li>更新</li><li>刪除</li></ul> |
| [Attribution AI執行個體](../../../intelligent-services/attribution-ai/overview.md) | <ul><li>建立</li><li>更新</li><li>刪除</li><li>啟用</li><li>停用</li></ul> |
| [稽核記錄](../../../landing/governance-privacy-security/audit-logs/overview.md) | <ul><li>轉存</li></ul> |
| [類別](../../../xdm/schema/composition.md#class) | <ul><li>建立</li><li>更新</li><li>刪除</li></ul> |
| 計算屬性 | <ul><li>建立</li><li>更新</li><li>刪除</li></ul> |
| [Customer AI執行個體](../../../intelligent-services/customer-ai/overview.md) | <ul><li>建立</li><li>更新</li><li>刪除</li><li>啟用</li><li>停用</li></ul> |
| [資料集](../../../catalog/datasets/overview.md) | <ul><li>建立</li><li>更新</li><li>刪除</li><li>為[即時客戶設定檔](../../../profile/home.md)啟用</li><li>為輪廓停用</li><li>新增資料</li><li>刪除批次</li></ul> |
| [資料流](../../../datastreams/overview.md) | <ul><li>建立</li><li>更新</li><li>刪除</li><li>啟用</li><li>停用</li><li>[編輯對應](../../../datastreams/data-prep.md)</li></ul> |
| [資料類型](../../../xdm/schema/composition.md#data-type) | <ul><li>建立</li><li>更新</li><li>刪除</li></ul> |
| [目標](../../../destinations/home.md) | <ul><li>建立</li><li>更新</li><li>刪除</li><li>啟用</li><li>停用</li><li>資料集啟用</li><li>資料集移除</li><li>輪廓啟用</li><li>輪廓移除</li></ul> |
| [欄位群組](../../../xdm/schema/composition.md#field-group) | <ul><li>建立</li><li>更新</li><li>刪除</li></ul> |
| [身分圖表](../../../identity-service/features/identity-graph-viewer.md) | <ul><li>檢視</li></ul> |
| [身分名稱空間](../../../identity-service/features/namespaces.md) | <ul><li>建立</li><li>更新</li></ul> |
| [合併原則](../../../profile/merge-policies/overview.md) | <ul><li>建立</li><li>更新</li><li>刪除</li></ul> |
| [產品設定檔](../../../access-control/home.md) | <ul><li>建立</li><li>更新</li><li>刪除</li></ul> |
| [查詢](../../../query-service/ui/overview.md) | <ul><li>執行</li></ul> |
| [查詢範本](../../../query-service/ui/overview.md) | <ul><li>建立</li><li>更新</li><li>刪除</li></ul> |
| [角色（以屬性為基礎的存取控制）](../../../access-control/home.md) | <ul><li>建立</li><li>更新</li><li>刪除</li><li>新增使用者</li><li>移除使用者</li></ul> |
| [沙箱](../../../sandboxes/home.md) | <ul><li>建立</li><li>更新</li><li>重設</li><li>刪除</li></ul> |
| [排定的查詢](../../../query-service/ui/overview.md) | <ul><li>建立</li><li>更新</li><li>刪除</li></ul> |
| [結構描述](../../../xdm/schema/composition.md) | <ul><li>建立</li><li>更新</li><li>刪除</li><li>為輪廓啟用</li></ul> |
| [區段](../../../segmentation/home.md) | <ul><li>建立</li><li>刪除</li><li>區段啟用</li><li>區段移除</li></ul> |
| [Source資料流程](../../../sources/connectors/tutorials/ui/../../../tutorials/ui/update.md) | <ul><li>建立</li><li>更新</li><li>刪除</li><li>啟用</li><li>停用</li><li>資料集啟用</li><li>資料集移除</li><li>設定檔啟用</li><li>輪廓移除</li></ul> |
| [工單](../../../hygiene/home.md) | <ul><li>建立</li></ul> |

## 存取稽核記錄

為您的組織啟用此功能後，活動發生時會自動收集稽核記錄。 您不需要手動啟用記錄收集。

若要檢視和匯出稽核記錄，您必須授予&#x200B;**[!UICONTROL 檢視使用者活動記錄]**&#x200B;存取控制許可權（可在[!UICONTROL 資料控管]類別下找到）。 若要瞭解如何管理Experience Platform功能的個別許可權，請參閱[存取控制檔案](../../../access-control/home.md)。

## 在 UI 中管理稽核記錄 {#managing-audit-logs-in-the-ui}

>[!CONTEXTUALHELP]
>id="platform_privacyConsole_audits_instructions"
>title="說明"
>abstract="<ul><li>在左側導覽中選取<b>稽核</b>。「稽核」工作區會顯示已記錄的記錄清單，依預設會從時間最近的開始排序。</li>   <li> 注意：稽核記錄會保留 365 天，超過此天數將從系統中刪除。因此，您最多只能往回查看 365 天。如果您需要查看超過 365 天的資料，您應該定期匯出記錄以符合您的內部原則需求。 </li><li>從清單中選取一個事件以在右邊欄中查看其詳細資料。 </li><li>選取漏斗圖示以顯示篩選控制項清單，可協助縮小結果範圍。僅顯示最後 1,000 條記錄，無論選取的篩選器為何。 </li><li>若要匯出目前的稽核記錄清單，請選取&#x200B;**下載記錄**。</li><li>如需有關此功能的更多說明，請參閱 Experience League 上的<a href="https://experienceleague.adobe.com/docs/experience-platform/landing/governance-privacy-security/audit-logs/overview.html?lang=zh-Hant">稽核記錄概觀</a>。</li></ul>"

您可以在Experience Platform UI的&#x200B;**[!UICONTROL 稽核]**&#x200B;工作區中，檢視不同Experience Platform功能的稽核記錄。 工作區會顯示記錄日誌的清單，預設情況下會從最近排序為最近排序。

![左側功能表中反白稽核的稽核儀表板。](../../images/audit-logs/audits.png)

稽核記錄會保留365天，之後會從系統中刪除。 如果您需要超過365天的資料，您應定期匯出記錄檔，以符合內部原則需求。

請求稽核記錄的方法會變更允許的時段以及您可存取的記錄數。 [匯出記錄檔](#export-audit-logs)可讓您回到365天（以90天為間隔），最多為10,000筆記錄，其中作為Experience Platform中的[活動記錄檔UI](#filter-audit-logs)，會顯示過去90天，最多為1000筆記錄。

從清單中選取一個事件以在右邊欄中查看其詳細資料。

![以醒目提示的事件詳細資料面板稽核儀表板活動記錄標籤。](../../images/audit-logs/select-event.png)

### 篩選稽核記錄

選取漏斗圖示（![篩選圖示](/help/images/icons/filter.png)）以顯示篩選控制項清單，以協助縮小結果範圍。

>[!NOTE]
>
>Experience Platform UI只會顯示過去90天的記錄（最多1000筆記錄），無論套用的篩選器為何。 如果您需要超過該天的記錄（最多365天），您需要[匯出稽核記錄](#export-audit-logs)。

![已反白篩選活動記錄檔的[稽核]儀表板。](../../images/audit-logs/filters.png)

下列篩選器可用於UI中的稽核事件：

| 篩選器 | 說明 |
| --- | --- |
| [!UICONTROL 類別] | 使用下拉式功能表，依[類別](#category)篩選顯示的結果。 |
| [!UICONTROL 動作] | 依動作篩選。 每項服務的可用動作會顯示在資源表格中。 |
| [!UICONTROL 使用者] | 輸入完整的使用者識別碼（例如，`johndoe@acme.com`）以依使用者篩選。 |
| [!UICONTROL 狀態] | 依由於缺少[存取控制](../../../access-control/home.md)許可權而允許（完成）或拒絕動作進行篩選。 |
| [!UICONTROL 日期] | 選取開始日期和/或結束日期，以定義篩選結果的日期範圍。 可匯出回顧期間為90天的資料（例如，2021-12-15至2022-03-15）。 這可能因事件型別而異。 |

若要移除濾鏡，請針對有問題的濾鏡選取藥丸圖示上的「X」，或選取&#x200B;**[!UICONTROL 全部清除]**&#x200B;以移除所有濾鏡。

![反白顯示具有清除篩選器的稽核儀表板。](../../images/audit-logs/clear-filters.png)

傳回的稽核記錄檔資料包含符合所選篩選條件之所有查詢的下列資訊。

| 欄名稱 | 說明 |
|---|---|
| [!UICONTROL 時間戳記] | 以`month/day/year hour:minute AM/PM`格式執行之動作的確切日期和時間。 |
| [!UICONTROL 資產名稱] | [!UICONTROL 資產名稱]欄位的值取決於選擇作為篩選的類別。 |
| [!UICONTROL 類別] | 此欄位符合在篩選下拉式清單中選取的類別。 |
| [!UICONTROL 動作] | 可用的動作取決於選擇作為篩選器的類別。 |
| [!UICONTROL 使用者] | 此欄位提供執行查詢的使用者ID。 |

![已反白篩選活動記錄檔的[稽核]儀表板。](../../images/audit-logs/filtered.png)

### 匯出稽核記錄 {#export-audit-logs}

若要匯出目前的稽核記錄清單，請選取&#x200B;**[!UICONTROL 下載記錄]**。

>[!NOTE]
>
>可在90天間隔內要求記錄檔，最多可達365天過去。 不過，單一匯出期間可傳回的最大記錄數量為10,000。

![反白顯示[!UICONTROL 下載記錄]的稽核儀表板。](../../images/audit-logs/download.png)

在出現的對話方塊中，選取您偏好的格式（**[!UICONTROL CSV]**&#x200B;或&#x200B;**[!UICONTROL JSON]**），然後選取&#x200B;**[!UICONTROL 下載]**。 瀏覽器會下載產生的檔案，並將其儲存到您的電腦。

![包含[!UICONTROL 下載]的檔案格式選擇對話方塊已反白顯示。](../../images/audit-logs/select-download-format.png)

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

若要瞭解如何管理Adobe Admin Console中活動的稽核記錄，請參閱下列[檔案](https://helpx.adobe.com/enterprise/using/audit-logs.html)。

## 後續步驟和其他資源

本指南說明如何在Experience Platform中管理稽核記錄。 如需如何監視Experience Platform活動的詳細資訊，請參閱有關[可觀察性深入分析](../../../observability/home.md)和[監視資料擷取](../../../ingestion/quality/monitor-data-ingestion.md)的檔案。

若要加深您對Experience Platform稽核記錄的瞭解，請觀看以下影片：

>[!VIDEO](https://video.tv.adobe.com/v/341450?quality=12&learn=on)
