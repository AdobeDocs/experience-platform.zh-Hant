---
description: 使用 [!UICONTROL 配置檔案富集] 控制板，瞭解配置檔案富集作業是否成功運行和完成，並查看基本度量以評估環境的有效性。
solution: Experience Platform
title: 監視配置檔案富集作業
type: Tutorial
source-git-commit: f3389ef2c2bd9ff52ecde2a4f5fd55e5b86783fc
workflow-type: tm+mt
source-wordcount: '466'
ht-degree: 1%

---

# 監視UI中的配置檔案富集作業

使用 [!UICONTROL 配置檔案富集] 控制板，瞭解配置檔案富集作業是否成功運行和完成，並查看基本度量以評估環境的有效性。

在 [平台UI](https://platform.adobe.com)選中 **[!UICONTROL 監視]** 從左側導航 [!UICONTROL 監視] 控制項欄。 在視圖選擇器中，選擇 **B2B流** 查看特定於的儀表板元素 [Real-Time CDPB2B](/help/rtcdp/b2b-overview.md)。  的 [!UICONTROL 監視] 儀表板包括來自最新成功運行的基本指標，以及過去最多90天的日作業狀態。 的 [!UICONTROL 相關帳戶] 儀表板顯示特定於 [相關帳戶](/help/rtcdp/b2b-ai-ml-services/related-accounts.md) 輪廓富集。

![如何進入Experience PlatformUI中配置檔案富集作業監視螢幕的直觀指示。](/help/dataflows/assets/ui/b2b/monitoring-profile-enrichment-jobs.png)

中的資料 **[!UICONTROL 度量]** 該卡包括來自最近成功運行「相關帳戶」作業的基本度量。

以下指標可用於相關帳戶配置檔案富集作業：

| 量度 | 說明 |
---------|----------|
| **[!UICONTROL 帳戶配置檔案總數]** | 指示您的組織有權訪問的帳戶配置檔案總數。 |
| **[!UICONTROL 帳戶組]** | 指示由「相關帳戶」機器學習作業聚集的帳戶組數。 |
| **[!UICONTROL 單帳戶組]** | 指示未與其他帳戶一起分組的帳戶數。 |
| **[!UICONTROL 最大組大小]** | 指示最大相關帳戶組的大小。 允許的最大組大小為30。 |
| **[!UICONTROL 中值組大小]** | 指示組織中相關帳戶組的中值大小。 |
| **[!UICONTROL 上次成功運行]** | 指示上次成功運行相關帳戶作業的日期和時間。 |
| **[!UICONTROL 狀態]** | 指示相關帳戶作業的狀態（成功、失敗或處理）。 |
| **[!UICONTROL 訊息]** | 指示特定作業運行的錯誤或警告消息。 |

## UI控制項 {#ui-controls}

本節介紹監視介面中的各種用戶介面(UI)選項，這些選項允許您過濾該頁上顯示的度量。

使用箭頭表徵圖(![箭頭表徵圖](/help/dataflows/assets/ui/monitor-destinations/chevron-up.png))展開或關閉螢幕頂部的卡，該卡會顯示有關配置檔案豐富作業的一覽式資訊。

![顯示箭頭表徵圖UI控制項的螢幕錄制。](/help/dataflows/assets/ui/b2b/use-arrow-control.gif)

使用 **[!UICONTROL 度量和圖形]** 切換以關閉顯示最新度量的視圖。

![顯示度量和圖形的螢幕錄制切換。](/help/dataflows/assets/ui/b2b/metrics-and-graphs-toggle.gif)

使用 **[!UICONTROL 僅顯示失敗]** 切換以僅顯示失敗的配置檔案富集作業。

![僅顯示「顯示失敗」的螢幕錄制可切換。](/help/dataflows/assets/ui/b2b/show-failures-only.gif)

## 後續步驟 {#next-steps}

通過學習本教程，您現在可以成功監視和瞭解相關帳戶配置檔案富集作業的度量。 有關詳細資訊，請參閱以下文檔：

* [即時CDP B2B中的相關客戶](/help/rtcdp/b2b-ai-ml-services/related-accounts.md)
* [「帳戶配置檔案UI」指南中的「相關帳戶」頁籤](/help/rtcdp/accounts/account-profile-ui-guide.md)