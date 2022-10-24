---
description: 使用 [!UICONTROL 設定檔擴充] 控制面板，了解設定檔擴充作業是否成功執行及完成，以及檢視基本量度以評估擴充的成效。
solution: Experience Platform
title: 監控設定檔擴充作業
type: Tutorial
exl-id: 096a2212-ed7f-4419-8ead-fa1ca01c2804
source-git-commit: 14e3eff3ea2469023823a35ee1112568f5b5f4f7
workflow-type: tm+mt
source-wordcount: '768'
ht-degree: 2%

---

# 在UI中監視設定檔擴充作業 {#monitor-profile-enrichment}

使用 [!UICONTROL 設定檔擴充] 控制面板，了解設定檔擴充作業是否成功執行及完成，以及檢視基本量度以評估擴充的成效。

在 [平台UI](https://platform.adobe.com)，選取 **[!UICONTROL 監控]** 從左側導覽器存取 [!UICONTROL 監控] 控制面板。 在檢視選取器中，選取 **B2B流量** 若要查看 [Real-Time CDP B2B](/help/rtcdp/b2b-overview.md).  此 [!UICONTROL 監控] 控制面板包含最新成功執行的基本量度，以及最多90天的每日工作狀態。

## 相關帳戶設定檔擴充 {#related-accounts}

此 [!UICONTROL 相關帳戶] 控制面板顯示基本量度，以及 [相關帳戶](/help/rtcdp/b2b-ai-ml-services/related-accounts.md) 設定檔擴充。

![以視覺化方式指示如何前往Experience PlatformUI中的設定檔擴充作業監控畫面。](/help/dataflows/assets/ui/b2b/monitoring-profile-enrichment-jobs.png)

中的資料 **[!UICONTROL 量度]** 卡片包含最新成功執行「相關帳戶」工作的基本量度。

下列量度適用於相關帳戶設定檔擴充作業：

| 量度 | 說明 |
| --------- | ---------- |
| **[!UICONTROL 帳戶設定檔總計]** | 指出貴組織有權存取的帳戶設定檔總數。 |
| **[!UICONTROL 帳戶群組]** | 指示相關帳戶機器學習作業聚簇的帳戶組數。 |
| **[!UICONTROL 單一帳戶群組]** | 指示未與其他帳戶一起分組的帳戶數。 |
| **[!UICONTROL 最大組大小]** | 指示最大相關帳戶組的大小。 允許的最大組大小為30。 |
| **[!UICONTROL 中位組大小]** | 指示組織中相關帳戶組的中位數大小。 |
| **[!UICONTROL 上次成功運行]** | 指示上次成功運行相關帳戶作業的日期和時間。 |
| **[!UICONTROL 狀態]** | 指示相關帳戶作業的狀態（成功、失敗或處理）。 |
| **[!UICONTROL 訊息]** | 指示特定作業運行的錯誤或警告消息。 |

## 導致帳戶匹配設定檔擴充 {#lead-to-account-matching}

此 [!UICONTROL 導致帳戶匹配] 控制面板顯示基本量度，以及 [導致帳戶匹配](/help/rtcdp/b2b-ai-ml-services/lead-to-account-matching.md) 設定檔擴充。

![導致帳戶匹配設定檔擴充](/help/dataflows/assets/ui/b2b/mpc-lead-to-account-matching.png)

下列量度可用於導致帳戶符合設定檔擴充作業：

| 量度 | 說明 |
| --------- | ---------- |
| **[!UICONTROL 有賬戶的總人數]** | 指出與帳戶相關聯的總人數。 |
| **[!UICONTROL 帳戶總數]** | 指示帳戶總數。 |
| **[!UICONTROL 有賬戶的現有人]** | 指出已與資料來源之帳戶相關聯的人數。 |
| **[!UICONTROL 匹配人員]** | 指出符合帳戶的人數。 |
| **[!UICONTROL 無與倫比的人]** | 指出與帳戶不相符的人數。 |
| **[!UICONTROL 上次成功運行]** | 指示上次成功銷售線索的日期和時間，以執行帳戶匹配作業。 |
| **[!UICONTROL 狀態]** | 指示銷售機會到帳戶匹配作業的狀態（成功、失敗或處理）。 |

## 預測性銷售機會和帳戶計分設定檔擴充 {#predictive-lead-to-account-scoring}

此 [!UICONTROL 預測性銷售機會和帳戶計分] 控制面板顯示基本量度，以及 [預測性銷售機會和帳戶計分](/help/rtcdp/b2b-ai-ml-services/predictive-lead-and-account-scoring.md) 設定檔擴充。

![預測性銷售機會和帳戶計分設定檔擴充](/help/dataflows/assets/ui/b2b/predictive-lead-and-account-scoring.png)

下列量度可用於預測性銷售機會和帳戶分數設定檔擴充作業：

| 量度 | 說明 |
| --------- | ---------- |
| **[!UICONTROL 工作開始]** | 指示預測潛在客戶和帳戶計分作業運行的開始日期和時間。 |
| **[!UICONTROL 處理時間]** | 完成該作業所花費的總時間。 |
| **[!UICONTROL 分數名稱]** | 工作的分數名稱。 |
| **[!UICONTROL 設定檔類型]** | 分數的類型： <ul><li>「人」</li><li>帳戶</li></ul>。 |
| **[!UICONTROL 作業類型]** | 作業的類型：<ul><li>分數</li><li>訓練</li>。 |
| **[!UICONTROL 狀態]** | 指示預測性潛在客戶和帳戶計分作業的狀態（成功、失敗或處理）。 |

## UI控制項 {#ui-controls}

本節說明監控介面中的各種使用者介面(UI)選項，可讓您篩選顯示在頁面上的量度。

使用箭頭圖示(![箭頭表徵圖](/help/dataflows/assets/ui/monitor-destinations/chevron-up.png))，以展開或關閉畫面頂端的資訊卡，此資訊卡會簡單顯示設定檔擴充工作的相關資訊。

![顯示箭頭表徵圖UI控制項的螢幕錄制。](/help/dataflows/assets/ui/b2b/use-arrow-control.gif)

使用 **[!UICONTROL 度量和圖表]** 切換為關閉顯示最新量度的檢視。

![顯示量度和圖形的螢幕記錄會切換。](/help/dataflows/assets/ui/b2b/metrics-and-graphs-toggle.gif)

使用 **[!UICONTROL 僅顯示故障]** 切換為僅顯示失敗的設定檔擴充作業。

![僅顯示「顯示失敗」的螢幕錄制切換。](/help/dataflows/assets/ui/b2b/show-failures-only.gif)

## 後續步驟 {#next-steps}

依照本教學課程，您現在可以成功監視和了解設定檔擴充作業的量度。 如需詳細資訊，請參閱下列檔案：

* [Real-Time CDP B2B的相關帳戶](/help/rtcdp/b2b-ai-ml-services/related-accounts.md)
* [帳戶設定檔UI指南中的相關帳戶標籤](/help/rtcdp/accounts/account-profile-ui-guide.md)
* [在Real-Time CDP B2B中導致帳戶比對](/help/rtcdp/b2b-ai-ml-services/lead-to-account-matching.md)
* [Real-Time CDP B2B中的預測性銷售機會和帳戶分數](/help/rtcdp/b2b-ai-ml-services/predictive-lead-and-account-scoring.md)
