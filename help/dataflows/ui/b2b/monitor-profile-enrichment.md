---
description: 使用 [!UICONTROL 配置檔案富集] 控制板，瞭解配置檔案富集作業是否成功運行和完成，並查看基本度量以評估環境的有效性。
solution: Experience Platform
title: 監視配置檔案富集作業
type: Tutorial
exl-id: 096a2212-ed7f-4419-8ead-fa1ca01c2804
source-git-commit: 14e3eff3ea2469023823a35ee1112568f5b5f4f7
workflow-type: tm+mt
source-wordcount: '768'
ht-degree: 2%

---

# 監視UI中的配置檔案富集作業 {#monitor-profile-enrichment}

使用 [!UICONTROL 配置檔案富集] 控制板，瞭解配置檔案富集作業是否成功運行和完成，並查看基本度量以評估環境的有效性。

在 [平台UI](https://platform.adobe.com)選中 **[!UICONTROL 監視]** 從左側導航 [!UICONTROL 監視] 控制項欄。 在視圖選擇器中，選擇 **B2B流** 查看特定於的儀表板元素 [Real-Time CDPB2B](/help/rtcdp/b2b-overview.md)。  的 [!UICONTROL 監視] 儀表板包括來自最新成功運行的基本指標，以及過去最多90天的日作業狀態。

## 相關帳戶配置檔案豐富 {#related-accounts}

的 [!UICONTROL 相關帳戶] 儀表板顯示特定於 [相關帳戶](/help/rtcdp/b2b-ai-ml-services/related-accounts.md) 輪廓富集。

![如何進入Experience PlatformUI中配置檔案富集作業監視螢幕的直觀指示。](/help/dataflows/assets/ui/b2b/monitoring-profile-enrichment-jobs.png)

中的資料 **[!UICONTROL 度量]** 該卡包括來自最近成功運行「相關帳戶」作業的基本度量。

以下指標可用於相關帳戶配置檔案富集作業：

| 量度 | 說明 |
| --------- | ---------- |
| **[!UICONTROL 帳戶配置檔案總數]** | 指示您的組織有權訪問的帳戶配置檔案總數。 |
| **[!UICONTROL 帳戶組]** | 指示由相關帳戶機器學習作業聚集的帳戶組數。 |
| **[!UICONTROL 單帳戶組]** | 指示未與其他帳戶一起分組的帳戶數。 |
| **[!UICONTROL 最大組大小]** | 指示最大相關帳戶組的大小。 允許的最大組大小為30。 |
| **[!UICONTROL 中值組大小]** | 指示組織中相關帳戶組的中值大小。 |
| **[!UICONTROL 上次成功運行]** | 指示上次成功運行相關帳戶作業的日期和時間。 |
| **[!UICONTROL 狀態]** | 指示相關帳戶作業的狀態（成功、失敗或處理）。 |
| **[!UICONTROL 訊息]** | 指示特定作業運行的錯誤或警告消息。 |

## 導出至帳戶匹配配置檔案的豐富 {#lead-to-account-matching}

的 [!UICONTROL 銷售線索到帳戶匹配] 控制板顯示特定於 [銷售線索到帳戶匹配](/help/rtcdp/b2b-ai-ml-services/lead-to-account-matching.md) 輪廓富集。

![導出至帳戶匹配配置檔案的豐富](/help/dataflows/assets/ui/b2b/mpc-lead-to-account-matching.png)

以下度量可用於線索到帳戶匹配配置檔案富集作業：

| 量度 | 說明 |
| --------- | ---------- |
| **[!UICONTROL 有帳戶的人員總數]** | 指示與帳戶關聯的人員總數。 |
| **[!UICONTROL 帳戶總數]** | 指示帳戶總數。 |
| **[!UICONTROL 具有帳戶的現有人員]** | 指示已與來自資料源的帳戶關聯的人員數。 |
| **[!UICONTROL 匹配的人]** | 指示與帳戶匹配的人員數。 |
| **[!UICONTROL 無匹配人]** | 指示與帳戶不匹配的人員數。 |
| **[!UICONTROL 上次成功運行]** | 指示上次成功引導至帳戶匹配作業運行的日期和時間。 |
| **[!UICONTROL 狀態]** | 指示潛在客戶到帳戶匹配作業的狀態（成功、失敗或處理）。 |

## 預測性線索和帳戶記分配置檔案的豐富 {#predictive-lead-to-account-scoring}

的 [!UICONTROL 預測線索和帳戶記分] 控制板顯示特定於 [預測線索和帳戶記分](/help/rtcdp/b2b-ai-ml-services/predictive-lead-and-account-scoring.md) 輪廓富集。

![預測性線索和帳戶記分配置檔案的豐富](/help/dataflows/assets/ui/b2b/predictive-lead-and-account-scoring.png)

以下指標可用於預測潛在客戶和帳戶評分配置檔案富集作業：

| 量度 | 說明 |
| --------- | ---------- |
| **[!UICONTROL 作業開始]** | 指示預測性線索和帳戶記分作業運行的起始日期和時間。 |
| **[!UICONTROL 處理時間]** | 作業完成所用的總時間。 |
| **[!UICONTROL 分數名稱]** | 作業的分數名稱。 |
| **[!UICONTROL 配置檔案類型]** | 分數的類型： <ul><li>「人」</li><li>帳戶</li></ul>。 |
| **[!UICONTROL 作業類型]** | 作業的類型：<ul><li>評分</li><li>訓練</li>。 |
| **[!UICONTROL 狀態]** | 指示預測線索和帳戶記分作業的狀態（成功、失敗或處理）。 |

## UI控制項 {#ui-controls}

本節介紹監視介面中的各種用戶介面(UI)選項，這些選項允許您過濾該頁上顯示的度量。

使用箭頭表徵圖(![箭頭表徵圖](/help/dataflows/assets/ui/monitor-destinations/chevron-up.png))展開或關閉螢幕頂部的卡，該卡會顯示有關配置檔案豐富作業的一覽式資訊。

![顯示箭頭表徵圖UI控制項的螢幕錄制。](/help/dataflows/assets/ui/b2b/use-arrow-control.gif)

使用 **[!UICONTROL 度量和圖形]** 切換以關閉顯示最新度量的視圖。

![顯示度量和圖形的螢幕錄制切換。](/help/dataflows/assets/ui/b2b/metrics-and-graphs-toggle.gif)

使用 **[!UICONTROL 僅顯示失敗]** 切換以僅顯示失敗的配置檔案富集作業。

![僅顯示「顯示失敗」的螢幕錄制可切換。](/help/dataflows/assets/ui/b2b/show-failures-only.gif)

## 後續步驟 {#next-steps}

通過學習本教程，您現在可以成功監視和瞭解配置檔案富集作業的度量。 有關詳細資訊，請參閱以下文檔：

* [Real-Time CDPB2B相關賬戶](/help/rtcdp/b2b-ai-ml-services/related-accounts.md)
* [「帳戶配置檔案UI」指南中的「相關帳戶」頁籤](/help/rtcdp/accounts/account-profile-ui-guide.md)
* [在Real-Time CDPB2B中實現帳戶匹配](/help/rtcdp/b2b-ai-ml-services/lead-to-account-matching.md)
* [Real-Time CDPB2B中的預測線索和帳戶評分](/help/rtcdp/b2b-ai-ml-services/predictive-lead-and-account-scoring.md)
