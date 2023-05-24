---
title: 審核日誌概述
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

為了提高系統中所執行活動的透明度和可見性，Adobe Experience Platform允許您以「審計日誌」的形式對用戶活動進行各種服務和功能的審計。 這些日誌形成了審核跟蹤，可幫助解決平台上的問題，並幫助您的企業有效地遵守公司資料管理策略和法規要求。

就基本概念而言，稽核記錄說明了&#x200B;**誰**&#x200B;執行了&#x200B;**什麼**&#x200B;動作，以及&#x200B;**何時**&#x200B;執行。稽核記錄中所記錄的每個動作都包含中繼資料，其指出動作類型、日期和時間、執行動作之使用者的電子郵件 ID，以及與動作類型相關的其他屬性。

本文檔介紹平台中的審核日誌，包括如何在UI或API中查看和管理這些日誌。

## 由稽核記錄擷取的事件類型 {#category}

下表概述了審計日誌記錄資源的操作：

| 資源 | 動作 |
| --- | --- |
| [訪問控制策略（基於屬性的訪問控制）](../../../access-control/home.md) | <ul><li>建立</li><li>更新</li><li>刪除</li></ul> |
| [帳戶(Adobe)](../../../sources/connectors/tutorials/ui/../../../tutorials/ui/update.md) | <ul><li>建立</li><li>更新</li><li>刪除</li></ul> |
| [Attribution AI實例](../../../intelligent-services/attribution-ai/overview.md) | <ul><li>建立</li><li>更新</li><li>刪除</li><li>啟用</li><li>禁用</li></ul> |
| [稽核記錄](../../../landing/governance-privacy-security/audit-logs/overview.md) | <ul><li>轉存</li></ul> |
| [類別](../../../xdm/schema/composition.md#class) | <ul><li>建立</li><li>更新</li><li>刪除</li></ul> |
| 計算屬性 | <ul><li>建立</li><li>更新</li><li>刪除</li></ul> |
| [客戶AI實例](../../../intelligent-services/customer-ai/overview.md) | <ul><li>建立</li><li>更新</li><li>刪除</li><li>啟用</li><li>禁用</li></ul> |
| [資料集](../../../catalog/datasets/overview.md) | <ul><li>建立</li><li>更新</li><li>刪除</li><li>啟用 [即時客戶配置檔案](../../../profile/home.md)</li><li>禁用配置檔案</li><li>添加資料</li><li>刪除批</li></ul> |
| [資料流](../../../edge/datastreams/overview.md) | <ul><li>建立</li><li>更新</li><li>刪除</li><li>啟用</li><li>禁用</li><li>[編輯對應](../../../edge/datastreams/data-prep.md)</li></ul> |
| [資料類型](../../../xdm/schema/composition.md#data-type) | <ul><li>建立</li><li>更新</li><li>刪除</li></ul> |
| [目標](../../../destinations/home.md) | <ul><li>建立</li><li>更新</li><li>刪除</li><li>啟用</li><li>禁用</li><li>資料集激活</li><li>刪除資料集</li><li>配置檔案激活</li><li>配置檔案刪除</li></ul> |
| [欄位群組](../../../xdm/schema/composition.md#field-group) | <ul><li>建立</li><li>更新</li><li>刪除</li></ul> |
| [識別圖](../../../identity-service/ui/identity-graph-viewer.md) | <ul><li>檢視</li></ul> |
| [標識命名空間](../../../identity-service/ui/identity-graph-viewer.md) | <ul><li>建立</li><li>更新</li></ul> |
| [合併策略](../../../profile/merge-policies/overview.md) | <ul><li>建立</li><li>更新</li><li>刪除</li></ul> |
| [產品描述檔](../../../access-control/home.md) | <ul><li>建立</li><li>更新</li><li>刪除</li></ul> |
| [查詢](../../../query-service/ui/overview.md) | <ul><li>執行</li></ul> |
| [查詢模板](../../../query-service/ui/overview.md) | <ul><li>建立</li><li>更新</li><li>刪除</li></ul> |
| [角色（基於屬性的訪問控制）](../../../access-control/home.md) | <ul><li>建立</li><li>更新</li><li>刪除</li><li>新增使用者</li><li>刪除用戶</li></ul> |
| [沙箱](../../../sandboxes/home.md) | <ul><li>建立</li><li>更新</li><li>重設</li><li>刪除</li></ul> |
| [計畫查詢](../../../query-service/ui/overview.md) | <ul><li>建立</li><li>更新</li><li>刪除</li></ul> |
| [方案](../../../xdm/schema/composition.md) | <ul><li>建立</li><li>更新</li><li>刪除</li><li>啟用配置檔案</li></ul> |
| [區段](../../../segmentation/home.md) | <ul><li>建立</li><li>刪除</li><li>段激活</li><li>段刪除</li></ul> |
| [源資料流](../../../sources/connectors/tutorials/ui/../../../tutorials/ui/update.md) | <ul><li>建立</li><li>更新</li><li>刪除</li><li>啟用</li><li>禁用</li><li>資料集激活</li><li>資料集刪除</li><li>配置檔案激活</li><li>刪除配置檔案</li></ul> |
| [工作單](../../../hygiene/home.md) | <ul><li>建立</li></ul> |

## 存取稽核記錄

為您的組織啟用此功能後，活動發生時系統自動收集稽核記錄。您無需手動啟用記錄收集。

要查看和導出審核日誌，您必須 **[!UICONTROL 查看用戶活動日誌]** 授予的訪問控制權限(在 [!UICONTROL 資料治理] )。 要瞭解如何管理平台功能的各個權限，請參閱 [訪問控制文檔](../../../access-control/home.md)。

## 管理UI中的審核日誌 {#managing-audit-logs-in-the-ui}

>[!CONTEXTUALHELP]
>id="platform_privacyConsole_audits_instructions"
>title="說明"
>abstract="<ul><li>在左側導覽中選取<b>稽核</b>。「稽核」工作區會顯示已記錄的記錄清單，依預設會從時間最近的開始排序。</li>   <li> 注意：稽核記錄會保留 365 天，超過此天數將從系統中刪除。因此，您最多只能往回查看 365 天。如果您需要查看超過 365 天的資料，您應該定期匯出記錄以符合您的內部政策要求。 </li><li>從清單中選取一個事件以在右邊欄中查看其詳細資料。 </li><li>選取漏斗圖示以顯示篩選控制項清單，可協助縮小結果範圍。僅顯示最後 1,000 條記錄，無論選取的篩選器為何。 </li><li>若要匯出目前的稽核記錄清單，請選取&#x200B;**下載記錄**。</li><li>如需有關此功能的更多說明，請參閱 Experience League 上的<a href="https://experienceleague.adobe.com/docs/experience-platform/landing/governance-privacy-security/audit-logs/overview.html?lang=zh-Hant">稽核記錄概觀</a>。</li></ul>"

您可以在以下位置查看Experience Platform功能的審核日誌： **[!UICONTROL 審計]** 工作區。 工作區顯示記錄日誌的清單，預設情況下從最近到最近排序。

![審核日誌儀表板](../../images/audit-logs/audits.png)

審核日誌將保留365天，之後將從系統中刪除。 因此，您最多只能往回查看 365 天。如果需要超過365天的資料，應定期導出日誌以滿足內部策略要求。

從清單中選取一個事件以在右邊欄中查看其詳細資料。

![事件詳細資訊](../../images/audit-logs/select-event.png)

### 篩選稽核記錄

>[!NOTE]
由於這是一項新功能，所顯示的資料只能追溯到2022年3月。 根據所選資源，早期資料可從2022年1月開始提供。


選擇漏斗表徵圖(![「篩選器」表徵圖](../../images/audit-logs/icon.png))以顯示篩選器控制項清單，以幫助縮小結果範圍。 只顯示最後1000條記錄，而與所選的各種篩選器無關。

![篩選器](../../images/audit-logs/filters.png)

以下篩選器可用於 UI 中的稽核事件：

| 篩選 | 說明 |
| --- | --- |
| [!UICONTROL 類別] | 使用下拉菜單按 [類別](#category)。 |
| [!UICONTROL 動作] | 按操作篩選。 僅當前 [!UICONTROL 建立] 和 [!UICONTROL 刪除] 可以篩選操作。 |
| [!UICONTROL 使用者] | 輸入完整的用戶ID(例如， `johndoe@acme.com`)按用戶篩選。 |
| [!UICONTROL 狀態] | 按操作是否允許（完成）或由於缺少而被拒絕進行篩選 [訪問控制](../../../access-control/home.md) 權限。 |
| [!UICONTROL 日期] | 選擇起始日期和/或終止日期以定義日期範圍以篩選結果。 可以使用90天的回望期（例如，2021-12-15到2022-03-15）導出資料。 這可能因事件類型而異。 |

要刪除濾鏡，請為有關的濾鏡選擇「X」，或選擇 **[!UICONTROL 全部清除]** 按鈕，將選定控制項在Tab鍵次序中下移一個位置。

![清除篩選器](../../images/audit-logs/clear-filters.png)

### 導出審核日誌

若要匯出目前的稽核記錄清單，請選取&#x200B;**[!UICONTROL 下載記錄]**。

![下載日誌](../../images/audit-logs/download.png)

在顯示的對話框中，選擇首選格式( **[!UICONTROL CSV]** 或 **[!UICONTROL JSON]**)，然後選擇 **[!UICONTROL 下載]**。 瀏覽器下載生成的檔案並將其保存到您的電腦。

![選擇下載格式](../../images/audit-logs/select-download-format.png)

## 管理API中的審核日誌

所有可以在 UI 中執行的動作，也可以使用 API 呼叫來完成。如需詳細資訊，請參閱 [ API 參考文件](https://www.adobe.io/experience-platform-apis/references/audit-query/)。

## 管理Adobe Admin Console的審計日誌

要瞭解如何管理Adobe Admin Console活動的審核日誌，請參閱以下內容 [文檔](https://helpx.adobe.com/enterprise/using/audit-logs.html)。

## 後續步驟和其他資源

本指南介紹了如何管理Experience Platform中的審核日誌。 有關如何監視平台活動的詳細資訊，請參閱 [可觀性洞察](../../../observability/home.md) 和 [監控資料接收](../../../ingestion/quality/monitor-data-ingestion.md)。

要增強您對Experience Platform中審核日誌的瞭解，請觀看以下視頻：

>[!VIDEO](https://video.tv.adobe.com/v/341450?quality=12&learn=on)
