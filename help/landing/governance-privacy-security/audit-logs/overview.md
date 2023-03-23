---
title: 稽核記錄概述
description: 了解稽核紀錄如何讓您查看誰在 Adobe Experience Platform 中執行了哪些操作。
exl-id: 00baf615-5b71-4e0a-b82a-ca0ce8566e7f
source-git-commit: cf6ff8bcd3dfebe551ac3d7289fa8d5fb2a78079
workflow-type: tm+mt
source-wordcount: '946'
ht-degree: 33%

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
>title="說明"
>abstract=""

為了提高系統中執行活動的透明度和可見度，Adobe Experience Platform可讓您以「稽核記錄」的形式，稽核各種服務和功能的使用者活動。 這些日誌形成了審核跟蹤，可以幫助Platform上的問題進行故障排除，並幫助您的企業有效遵守公司資料管理策略和法規要求。

就基本概念而言，稽核記錄說明了&#x200B;**誰**&#x200B;執行了&#x200B;**什麼**&#x200B;動作，以及&#x200B;**何時**&#x200B;執行。稽核記錄中所記錄的每個動作都包含中繼資料，其指出動作類型、日期和時間、執行動作之使用者的電子郵件 ID，以及與動作類型相關的其他屬性。

本檔案涵蓋Platform中的稽核記錄，包括如何在UI或API中檢視及管理這些記錄。

## 由稽核記錄擷取的事件類型 {#category}

下表概述稽核記錄要記錄哪些資源的動作：

| 資源 | 動作 |
| --- | --- |
| [訪問控制策略（基於屬性的訪問控制）](../../../access-control/home.md) | <ul><li>建立</li><li>更新</li><li>刪除</li></ul> |
| [帳戶(Adobe)](../../../sources/connectors/tutorials/ui/../../../tutorials/ui/update.md) | <ul><li>建立</li><li>更新</li><li>刪除</li></ul> |
| [Attribution AI例項](../../../intelligent-services/attribution-ai/overview.md) | <ul><li>建立</li><li>更新</li><li>刪除</li><li>啟用</li><li>停用</li></ul> |
| [稽核記錄](../../../landing/governance-privacy-security/audit-logs/overview.md) | <ul><li>轉存</li></ul> |
| [類別](../../../xdm/schema/composition.md#class) | <ul><li>建立</li><li>更新</li><li>刪除</li></ul> |
| [計算屬性](../../../profile/computed-attributes/overview.md) | <ul><li>建立</li><li>更新</li><li>刪除</li></ul> |
| [Customer AI例項](../../../intelligent-services/customer-ai/overview.md) | <ul><li>建立</li><li>更新</li><li>刪除</li><li>啟用</li><li>停用</li></ul> |
| [資料集](../../../catalog/datasets/overview.md) | <ul><li>建立</li><li>更新</li><li>刪除</li><li>啟用 [即時客戶個人檔案](../../../profile/home.md)</li><li>對配置檔案禁用</li><li>新增資料</li><li>刪除批</li></ul> |
| [資料流](../../../edge/datastreams/overview.md) | <ul><li>建立</li><li>更新</li><li>刪除</li><li>啟用</li><li>停用</li><li>[編輯對應](../../../edge/datastreams/data-prep.md)</li></ul> |
| [資料類型](../../../xdm/schema/composition.md#data-type) | <ul><li>建立</li><li>更新</li><li>刪除</li></ul> |
| [目標](../../../destinations/home.md) | <ul><li>建立</li><li>更新</li><li>刪除</li><li>啟用</li><li>停用</li><li>資料集啟動</li><li>資料集移除</li><li>設定檔啟用</li><li>設定檔移除</li></ul> |
| [欄位群組](../../../xdm/schema/composition.md#field-group) | <ul><li>建立</li><li>更新</li><li>刪除</li></ul> |
| [身分圖](../../../identity-service/ui/identity-graph-viewer.md) | <ul><li>檢視</li></ul> |
| [身分命名空間](../../../identity-service/ui/identity-graph-viewer.md) | <ul><li>建立</li><li>更新</li></ul> |
| [合併策略](../../../profile/merge-policies/overview.md) | <ul><li>建立</li><li>更新</li><li>刪除</li></ul> |
| [產品描述檔](../../../access-control/home.md) | <ul><li>建立</li><li>更新</li><li>刪除</li></ul> |
| [查詢](../../../query-service/ui/overview.md) | <ul><li>執行</li></ul> |
| [查詢範本](../../../query-service/ui/overview.md) | <ul><li>建立</li><li>更新</li><li>刪除</li></ul> |
| [角色（基於屬性的訪問控制）](../../../access-control/home.md) | <ul><li>建立</li><li>更新</li><li>刪除</li><li>新增使用者</li><li>移除使用者</li></ul> |
| [沙箱](../../../sandboxes/home.md) | <ul><li>建立</li><li>更新</li><li>重設</li><li>刪除</li></ul> |
| [排程查詢](../../../query-service/ui/overview.md) | <ul><li>建立</li><li>更新</li><li>刪除</li></ul> |
| [方案](../../../xdm/schema/composition.md) | <ul><li>建立</li><li>更新</li><li>刪除</li><li>啟用設定檔</li></ul> |
| [區段](../../../segmentation/home.md) | <ul><li>建立</li><li>刪除</li><li>區段啟用</li><li>區段移除</li></ul> |
| [源資料流](../../../sources/connectors/tutorials/ui/../../../tutorials/ui/update.md) | <ul><li>建立</li><li>更新</li><li>刪除</li><li>啟用</li><li>停用</li><li>資料集啟用</li><li>資料集移除</li><li>設定檔啟用</li><li>設定檔移除</li></ul> |
| [工作順序](../../../hygiene/home.md) | <ul><li>建立</li></ul> |

## 存取稽核記錄

為您的組織啟用此功能後，活動發生時系統自動收集稽核記錄。您無需手動啟用記錄收集。

若要檢視及匯出稽核記錄檔，您必須具備 **[!UICONTROL 查看用戶活動日誌]** 授予的存取控制權限(可在 [!UICONTROL 資料控管] 類別)。 若要了解如何管理Platform功能的個別權限，請參閱 [存取控制檔案](../../../access-control/home.md).

## 在UI中管理稽核記錄 {#managing-audit-logs-in-the-ui}

>[!CONTEXTUALHELP]
>id="platform_privacyConsole_audits_instructions"
>title="說明"
>abstract=""

您可以在 **[!UICONTROL 稽核]** 工作區。 工作區會顯示記錄的記錄清單，依預設會從最近到最近排序。

![稽核記錄控制面板](../../images/audit-logs/audits.png)

稽核記錄會保留365天，之後將從系統中刪除。 因此，您最多只能返回365天的期間。 如果您需要超過365天的資料，則應定期匯出日誌，以符合內部政策要求。

從清單中選取事件，以在右側邊欄中檢視其詳細資訊。

![事件詳細資料](../../images/audit-logs/select-event.png)

### 篩選稽核記錄

>[!NOTE]
>
>由於這是一項新功能，所顯示的資料只會回溯至2022年3月。 根據所選資源，2022年1月起可能會提供先前的資料。


選取漏斗圖示(![篩選圖示](../../images/audit-logs/icon.png))以顯示篩選控制項清單，以縮小結果範圍。 無論選取的各種篩選器為何，都只會顯示最後1000筆記錄。

![篩選器](../../images/audit-logs/filters.png)

以下篩選器可用於 UI 中的稽核事件：

| 篩選 | 說明 |
| --- | --- |
| [!UICONTROL 類別] | 使用下拉式功能表，依據篩選顯示的結果 [類別](#category). |
| [!UICONTROL 動作] | 依動作篩選。 目前僅 [!UICONTROL 建立] 和 [!UICONTROL 刪除] 可篩選動作。 |
| [!UICONTROL 使用者] | 輸入完整的使用者ID(例如 `johndoe@acme.com`)來依使用者篩選。 |
| [!UICONTROL 狀態] | 依照是否允許（完成）或因缺少而拒絕動作進行篩選 [存取控制](../../../access-control/home.md) 權限。 |
| [!UICONTROL 日期] | 選取開始日期和/或結束日期，以定義要依據篩選結果的日期範圍。 資料可匯出為90天回顧期間(例如2021-12-15至2022-03-15)。 這可能因事件類型而異。 |

若要移除篩選器，請針對相關篩選器在藥丸圖示上選取「X」，或選取 **[!UICONTROL 全部清除]** 移除所有篩選器。

![清除篩選器](../../images/audit-logs/clear-filters.png)

### 導出審核日誌

要導出審核日誌的當前清單，請選擇 **[!UICONTROL 下載記錄檔]**.

![下載記錄檔](../../images/audit-logs/download.png)

在顯示的對話方塊中，選取您偏好的格式( **[!UICONTROL CSV]** 或 **[!UICONTROL JSON]**)，然後選取 **[!UICONTROL 下載]**. 瀏覽器會下載產生的檔案，並將其儲存至電腦。

![選擇下載格式](../../images/audit-logs/select-download-format.png)

## 管理API中的稽核記錄

所有可以在 UI 中執行的動作，也可以使用 API 呼叫來完成。如需詳細資訊，請參閱 [ API 參考文件](https://www.adobe.io/experience-platform-apis/references/audit-query/)。

## 管理Adobe Admin Console的稽核記錄

若要了解如何管理Adobe Admin Console中活動的稽核記錄，請參閱下列內容 [檔案](https://helpx.adobe.com/enterprise/using/audit-logs.html).

## 後續步驟和其他資源

本指南說明如何在Experience Platform中管理稽核記錄。 如需如何監控Platform活動的詳細資訊，請參閱 [可觀察性深入分析](../../../observability/home.md) 和 [監控資料擷取](../../../ingestion/quality/monitor-data-ingestion.md).

若要加深您對Experience Platform稽核記錄的了解，請觀看下列影片：

>[!VIDEO](https://video.tv.adobe.com/v/341450?quality=12&learn=on)
