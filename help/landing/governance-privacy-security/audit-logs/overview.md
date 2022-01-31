---
title: 審核日誌概述
description: 瞭解審核日誌如何讓您查看誰在Adobe Experience Platform執行了哪些操作。
exl-id: 00baf615-5b71-4e0a-b82a-ca0ce8566e7f
source-git-commit: 7e4853cee8a0fa937c82eb842cd73b675eb337a3
workflow-type: tm+mt
source-wordcount: '657'
ht-degree: 5%

---

# 審核日誌(Beta)

>[!IMPORTANT]
>
>Adobe Experience Platform的審計日誌功能當前處於測試版中，您的組織可能尚未訪問它。 本文檔中描述的功能可能會發生更改。

為了提高系統中所執行活動的透明度和可見性，Adobe Experience Platform允許您以「審計日誌」的形式對用戶活動進行各種服務和功能的審計。 這些日誌形成了審核跟蹤，可幫助解決平台上的問題，並幫助您的企業有效地遵守公司資料管理策略和法規要求。

從基本意義上講，審計日誌會告訴 **誰** 執行 **什麼** 操作和 **何時**。 記錄在日誌中的每個操作都包含元資料，這些元資料指示操作類型、日期和時間、執行該操作的用戶的電子郵件ID以及與操作類型相關的其他屬性。

本文檔介紹平台中的審核日誌，包括如何在UI或API中查看和管理這些日誌。

## 由審核日誌捕獲的事件類型 {#category}

下表概述了審計日誌記錄資源的操作：

| 資源 | 動作 |
| --- | --- |
| [資料集](../../../catalog/datasets/overview.md) | <ul><li>建立</li><li>更新</li><li>刪除</li><li>啟用 [即時客戶概要資訊](../../../profile/home.md)</li></ul> |
| [方案](../../../xdm/schema/composition.md) | <ul><li>建立</li><li>更新</li><li>刪除</li></ul> |
| [類](../../../xdm/schema/composition.md#class) | <ul><li>建立</li><li>更新</li><li>刪除</li></ul> |
| [欄位組](../../../xdm/schema/composition.md#field-group) | <ul><li>建立</li><li>更新</li><li>刪除</li></ul> |
| [資料類型](../../../xdm/schema/composition.md#data-type) | <ul><li>建立</li><li>更新</li><li>刪除</li></ul> |
| [沙箱](../../../sandboxes/home.md) | <ul><li>建立</li><li>更新</li><li>重設</li><li>刪除</li></ul> |
| [目標](../../../destinations/home.md) | <ul><li>啟動</li></ul> |

## 訪問審核日誌

為您的組織啟用該功能後，會在發生活動時自動收集審核日誌。 您不需要手動啟用日誌收集。

要查看和導出審核日誌，您必須 **[!UICONTROL 查看用戶活動日誌]** 授予的訪問控制權限(在 [!UICONTROL 資料治理] )。 要瞭解如何管理平台功能的各個權限，請參閱 [訪問控制文檔](../../../access-control/home.md)。

## 管理UI中的審核日誌

您可以在以下位置查看Experience Platform功能的審核日誌： **[!UICONTROL 審計]** 工作區。 工作區顯示記錄日誌的清單，預設情況下從最近到最近排序。

![審核日誌儀表板](../../images/audit-logs/audits.png)

系統只顯示去年的審核日誌。 超過此限制的日誌將自動從系統中刪除。

從清單中選擇一個事件，以在右欄中查看其詳細資訊。

![事件詳細資訊](../../images/audit-logs/select-event.png)

### 篩選審核日誌

選擇漏斗表徵圖(![「篩選器」表徵圖](../../images/audit-logs/icon.png))以顯示篩選器控制項清單，以幫助縮小結果範圍。

![篩選條件](../../images/audit-logs/filters.png)

以下篩選器可用於UI中的審核事件：

| 篩選 | 說明 |
| --- | --- |
| [!UICONTROL 類別] | 使用下拉菜單按 [類別](#category)。 |
| [!UICONTROL 動作] | 按操作篩選。 僅當前 [!UICONTROL 建立] 和 [!UICONTROL 刪除] 可以篩選操作。 |
| [!UICONTROL 狀態] | 按操作是否允許（完成）或由於缺少而被拒絕進行篩選 [訪問控制](../../../access-control/home.md) 權限。 |
| [!UICONTROL 日期] | 選擇起始日期和/或終止日期以定義日期範圍以篩選結果。 |

要刪除濾鏡，請為有關的濾鏡選擇「X」，或選擇 **[!UICONTROL 全部清除]** 按鈕，將選定控制項在Tab鍵次序中下移一個位置。

![清除篩選器](../../images/audit-logs/clear-filters.png)

### 導出審核日誌

要導出當前審核日誌清單，請選擇 **[!UICONTROL 下載日誌]**。

![下載日誌](../../images/audit-logs/download.png)

在顯示的對話框中，選擇首選格式( **[!UICONTROL CSV]** 或 **[!UICONTROL JSON]**)，然後選擇 **[!UICONTROL 下載]**。 瀏覽器下載生成的檔案並將其保存到您的電腦。

![選擇下載格式](../../images/audit-logs/select-download-format.png)

## 管理API中的審核日誌

您可以在UI中執行的所有操作也可以使用API調用完成。 查看 [API參考文檔](https://www.adobe.io/experience-platform-apis/references/audit-query/) 的子菜單。

## 管理Adobe Admin Console的審計日誌

要瞭解如何管理Adobe Admin Console活動的審核日誌，請參閱以下內容 [文檔](https://helpx.adobe.com/enterprise/using/audit-logs.html)。

## 後續步驟

本指南介紹了如何管理Experience Platform中的審核日誌。 有關如何監視平台活動的詳細資訊，請參閱 [可觀性洞察](../../../observability/home.md) 和 [監控資料接收](../../../ingestion/quality/monitor-data-ingestion.md)。
