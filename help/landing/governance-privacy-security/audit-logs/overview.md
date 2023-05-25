---
title: 稽核記錄概觀
description: 了解稽核紀錄如何讓您查看誰在 Adobe Experience Platform 中執行了哪些操作。
exl-id: 00baf615-5b71-4e0a-b82a-ca0ce8566e7f
source-git-commit: 8f61840ad60b7d24c980b218b6f742485f5ebfdd
workflow-type: tm+mt
source-wordcount: '1156'
ht-degree: 48%

---

# 稽核記錄 {#audit-logs}

>[!CONTEXTUALHELP]
>id="platform_audits_privacyconsole_actions"
>title="熱門動作"
>abstract="此 Widget 會顯示在所選時間範圍內在 Experience Platform 最常執行的動作類型。若要查看 Platform 中記錄的動作的完整清單，請在左側導覽中選取&#x200B;**稽核**。"

>[!CONTEXTUALHELP]
>id="platform_audits_privacyconsole_users"
>title="熱門使用者"
>abstract="此 Widget 會顯示在所選時間範圍於 Experience Platform 執行最多動作的使用者。若要查看 Platform 中記錄的動作的完整清單，請在左側導覽中選取&#x200B;**稽核**。"

>[!CONTEXTUALHELP]
>id="platform_privacyConsole_audits_description"
>title="監控 Platform 中的使用者活動"
>abstract="<h2>說明</h2><p>您可以採用「稽核記錄」的方式監控各種 Platform 服務和功能的使用者活動。這些記錄會形成稽核軌跡，其中會記錄<b>什麼人</b>在<b>什麼時間</b>執行了<b>什麼動作</b>。稽核記錄可以幫助解決 Platform 上的問題，並幫助您的企業有效地遵守公司資料管理原則和監管要求。</p>"

為了提高系統中所執行活動的透明度和可見度，Adobe Experience Platform可讓您以「稽核記錄」的形式，稽核各種服務和功能的使用者活動。 這些記錄形成稽核軌跡，可協助疑難排解Platform上的問題，並幫助您的企業有效遵守公司資料管理政策和法規要求。

就基本概念而言，稽核記錄說明了&#x200B;**誰**&#x200B;執行了&#x200B;**什麼**&#x200B;動作，以及&#x200B;**何時**&#x200B;執行。稽核記錄中所記錄的每個動作都包含中繼資料，其指出動作類型、日期和時間、執行動作之使用者的電子郵件 ID，以及與動作類型相關的其他屬性。

本檔案涵蓋Platform中的稽核記錄，包括如何在UI或API中檢視和管理它們。

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
| [資料集](../../../catalog/datasets/overview.md) | <ul><li>建立</li><li>更新</li><li>刪除</li><li>啟用對象 [即時客戶個人檔案](../../../profile/home.md)</li><li>為設定檔停用</li><li>新增資料</li><li>刪除批次</li></ul> |
| [資料流](../../../edge/datastreams/overview.md) | <ul><li>建立</li><li>更新</li><li>刪除</li><li>啟用</li><li>停用</li><li>[編輯對應](../../../edge/datastreams/data-prep.md)</li></ul> |
| [資料類型](../../../xdm/schema/composition.md#data-type) | <ul><li>建立</li><li>更新</li><li>刪除</li></ul> |
| [目標](../../../destinations/home.md) | <ul><li>建立</li><li>更新</li><li>刪除</li><li>啟用</li><li>停用</li><li>資料集啟動</li><li>資料集移除</li><li>設定檔啟動</li><li>設定檔移除</li></ul> |
| [欄位群組](../../../xdm/schema/composition.md#field-group) | <ul><li>建立</li><li>更新</li><li>刪除</li></ul> |
| [識別圖](../../../identity-service/ui/identity-graph-viewer.md) | <ul><li>檢視</li></ul> |
| [身分名稱空間](../../../identity-service/ui/identity-graph-viewer.md) | <ul><li>建立</li><li>更新</li></ul> |
| [合併原則](../../../profile/merge-policies/overview.md) | <ul><li>建立</li><li>更新</li><li>刪除</li></ul> |
| [產品描述檔](../../../access-control/home.md) | <ul><li>建立</li><li>更新</li><li>刪除</li></ul> |
| [查詢](../../../query-service/ui/overview.md) | <ul><li>執行</li></ul> |
| [查詢範本](../../../query-service/ui/overview.md) | <ul><li>建立</li><li>更新</li><li>刪除</li></ul> |
| [角色（以屬性為基礎的存取控制）](../../../access-control/home.md) | <ul><li>建立</li><li>更新</li><li>刪除</li><li>新增使用者</li><li>移除使用者</li></ul> |
| [沙箱](../../../sandboxes/home.md) | <ul><li>建立</li><li>更新</li><li>重設</li><li>刪除</li></ul> |
| [排定的查詢](../../../query-service/ui/overview.md) | <ul><li>建立</li><li>更新</li><li>刪除</li></ul> |
| [方案](../../../xdm/schema/composition.md) | <ul><li>建立</li><li>更新</li><li>刪除</li><li>為設定檔啟用</li></ul> |
| [區段](../../../segmentation/home.md) | <ul><li>建立</li><li>刪除</li><li>區段啟用</li><li>區段移除</li></ul> |
| [來源資料流程](../../../sources/connectors/tutorials/ui/../../../tutorials/ui/update.md) | <ul><li>建立</li><li>更新</li><li>刪除</li><li>啟用</li><li>停用</li><li>資料集啟用</li><li>資料集移除</li><li>設定檔啟用</li><li>設定檔移除</li></ul> |
| [工單](../../../hygiene/home.md) | <ul><li>建立</li></ul> |

## 存取稽核記錄

為您的組織啟用此功能後，活動發生時系統自動收集稽核記錄。您無需手動啟用記錄收集。

若要檢視和匯出稽核記錄，您必須擁有 **[!UICONTROL 檢視使用者活動記錄]** 已授予存取控制許可權(可在 [!UICONTROL 資料控管] 類別)。 若要瞭解如何管理Platform功能的個別許可權，請參閱 [存取控制檔案](../../../access-control/home.md).

## 在UI中管理稽核記錄 {#managing-audit-logs-in-the-ui}

>[!CONTEXTUALHELP]
>id="platform_privacyConsole_audits_instructions"
>title="說明"
>abstract="<ul><li>在左側導覽中選取<b>稽核</b>。「稽核」工作區會顯示已記錄的記錄清單，依預設會從時間最近的開始排序。</li>   <li> 注意：稽核記錄會保留 365 天，超過此天數將從系統中刪除。因此，您最多只能往回查看 365 天。如果您需要查看超過 365 天的資料，您應該定期匯出記錄以符合您的內部政策要求。 </li><li>從清單中選取一個事件以在右邊欄中查看其詳細資料。 </li><li>選取漏斗圖示以顯示篩選控制項清單，可協助縮小結果範圍。僅顯示最後 1,000 條記錄，無論選取的篩選器為何。 </li><li>若要匯出目前的稽核記錄清單，請選取&#x200B;**下載記錄**。</li><li>如需有關此功能的更多說明，請參閱 Experience League 上的<a href="https://experienceleague.adobe.com/docs/experience-platform/landing/governance-privacy-security/audit-logs/overview.html?lang=zh-Hant">稽核記錄概觀</a>。</li></ul>"

您可以在中檢視不同Experience Platform功能的稽核記錄 **[!UICONTROL 稽核]** Platform UI中的工作區。 工作區會顯示記錄日誌的清單，預設情況下會從最近到最近排序。

![稽核記錄儀表板](../../images/audit-logs/audits.png)

稽核記錄會保留365天，之後會從系統中刪除它們。 因此，您最多只能往回查看 365 天。如果您需要超過365天的資料，您應定期匯出記錄檔，以符合內部原則需求。

從清單中選取一個事件以在右邊欄中查看其詳細資料。

![事件詳細資料](../../images/audit-logs/select-event.png)

### 篩選稽核記錄

>[!NOTE]
由於這是一項新功能，顯示的資料僅追溯至2022年3月。 根據選取的資源，從2022年1月起，可能會提供舊版資料。


選取漏斗圖示(![篩選圖示](../../images/audit-logs/icon.png))來顯示篩選控制項清單，以協助縮小結果範圍。 僅顯示最後1000筆記錄，無論選擇的各種篩選器為何。

![篩選器](../../images/audit-logs/filters.png)

以下篩選器可用於 UI 中的稽核事件：

| 篩選 | 說明 |
| --- | --- |
| [!UICONTROL 類別] | 使用下拉式選單，依以下條件篩選顯示的結果 [類別](#category). |
| [!UICONTROL 動作] | 依動作篩選。 目前僅適用 [!UICONTROL 建立] 和 [!UICONTROL 刪除] 可以篩選動作。 |
| [!UICONTROL 使用者] | 輸入完整的使用者ID (例如， `johndoe@acme.com`)，依使用者篩選。 |
| [!UICONTROL 狀態] | 篩選條件為允許（完成）動作或因缺少動作而拒絕動作 [存取控制](../../../access-control/home.md) 許可權。 |
| [!UICONTROL 日期] | 選取開始日期和/或結束日期，以定義篩選結果的日期範圍。 可匯出90天回顧期間的資料（例如，2021-12-15到2022-03-15）。 這可能因事件型別而異。 |

若要移除篩選條件，請針對有問題的篩選條件，選取藥丸圖示上的「X」，或選取 **[!UICONTROL 全部清除]** 以移除所有篩選器。

![清除篩選器](../../images/audit-logs/clear-filters.png)

### 匯出稽核記錄

若要匯出目前的稽核記錄清單，請選取&#x200B;**[!UICONTROL 下載記錄]**。

![下載記錄](../../images/audit-logs/download.png)

在出現的對話方塊中，選取您偏好的格式 **[!UICONTROL CSV]** 或 **[!UICONTROL JSON]**)，然後選取 **[!UICONTROL 下載]**. 瀏覽器會下載產生的檔案，並將其儲存到您的電腦。

![選取下載格式](../../images/audit-logs/select-download-format.png)

## 管理API中的稽核記錄

所有可以在 UI 中執行的動作，也可以使用 API 呼叫來完成。如需詳細資訊，請參閱 [ API 參考文件](https://www.adobe.io/experience-platform-apis/references/audit-query/)。

## 管理Adobe Admin Console的稽核記錄

若要瞭解如何管理Adobe Admin Console活動的稽核記錄，請參閱下列內容 [檔案](https://helpx.adobe.com/enterprise/using/audit-logs.html).

## 後續步驟和其他資源

本指南說明如何管理Experience Platform稽核記錄。 如需如何監視Platform活動的詳細資訊，請參閱以下檔案： [可觀察性深入分析](../../../observability/home.md) 和 [監控資料擷取](../../../ingestion/quality/monitor-data-ingestion.md).

若要加深您對Experience Platform稽核記錄的瞭解，請觀看以下影片：

>[!VIDEO](https://video.tv.adobe.com/v/341450?quality=12&learn=on)
