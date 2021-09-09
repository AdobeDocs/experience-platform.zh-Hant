---
title: 稽核記錄概述
description: 了解稽核記錄如何讓您查看誰在Adobe Experience Platform中執行了哪些動作。
exl-id: 00baf615-5b71-4e0a-b82a-ca0ce8566e7f
source-git-commit: df269a30251cb17e337ec25787d6a1eed41e9c0b
workflow-type: tm+mt
source-wordcount: '469'
ht-degree: 4%

---

# 稽核記錄（測試版）

>[!IMPORTANT]
>
>Adobe Experience Platform中的稽核記錄功能目前仍在測試中。 本檔案所述的功能可能會有所變更。

為了提高系統中執行活動的透明度和可見度，Adobe Experience Platform可讓您以「稽核記錄」的形式，稽核各種服務和功能的使用者活動。 這些日誌形成了審核跟蹤，可以幫助Platform上的問題進行故障排除，並幫助您的企業有效遵守公司資料管理策略和法規要求。

從基本意義上講，審核日誌告訴&#x200B;**誰**&#x200B;執行了&#x200B;**什麼**&#x200B;操作，以及當&#x200B;**時執行了**&#x200B;操作。 記錄在記錄檔中的每個動作都包含中繼資料，指出動作類型、日期和時間、執行動作之使用者的電子郵件ID，以及與動作類型相關的其他屬性。

本檔案涵蓋Platform中的稽核記錄，包括如何在UI或API中檢視及管理這些記錄。

## 由審核日誌捕獲的事件類型

下表概述稽核記錄要記錄哪些資源的動作：

| 資源 | 動作 |
| --- | --- |
| [沙箱](../../../sandboxes/home.md) | <ul><li>建立</li><li>更新</li><li>重設</li><li>刪除</li></ul> |
| [資料集](../../../catalog/datasets/overview.md) | <ul><li>建立</li><li>更新</li><li>刪除</li><li>啟用[即時客戶設定檔](../../../profile/home.md)</li></ul> |
| [方案](../../../xdm/schema/composition.md) | <ul><li>建立</li><li>更新</li><li>刪除</li></ul> |
| [欄位組](../../../xdm/schema/composition.md#field-group) | <ul><li>建立</li><li>更新</li><li>刪除</li></ul> |
| [目標](../../../destinations/home.md) | <ul><li>啟動</li></ul> |

## 對審核日誌的訪問

為您的組織啟用功能時，稽核記錄會隨著活動發生而自動收集。 您不需要手動啟用記錄檔收集。

若要檢視和匯出稽核記錄檔，您必須已授與「檢視稽核記錄檔」存取控制權限（可在「資料控管」類別下找到）。 若要了解如何管理Platform功能的個別權限，請參閱[存取控制檔案](../../../access-control/home.md)。

## 在UI中管理稽核記錄

您可以在Platform UI的&#x200B;**[!UICONTROL Audits]**&#x200B;工作區中檢視不同Experience Platform功能的稽核記錄。 工作區會顯示記錄的記錄清單，依預設會從最近到最近排序。

![稽核記錄控制面板](../../images/audit-logs/audits.png)

系統只會顯示去年的稽核記錄。 超過此限制的任何日誌都會自動從系統中刪除。

從清單中選取事件，以在右側邊欄中檢視其詳細資訊。

![事件詳細資料](../../images/audit-logs/select-event.png)

<!-- (Planned for post-beta release)
### Export an audit log

Select **[!UICONTROL Download log]** to export an audit log.
-->

## 管理API中的稽核記錄

您在UI中可執行的所有動作也可以透過API呼叫完成。 如需詳細資訊，請參閱[API參考檔案](https://www.adobe.io/experience-platform-apis/references/audit-query/)。

## 管理Adobe Admin Console的稽核記錄

若要了解如何管理Adobe Admin Console中活動的稽核記錄，請參閱下列[document](https://helpx.adobe.com/enterprise/using/audit-logs.html)。

## 後續步驟

本指南說明如何在Experience Platform中管理稽核記錄。 如需如何監控Platform活動的詳細資訊，請參閱[可觀察性前瞻分析](../../../observability/home.md)和[監控資料擷取](../../../ingestion/quality/monitor-data-ingestion.md)的相關檔案。
