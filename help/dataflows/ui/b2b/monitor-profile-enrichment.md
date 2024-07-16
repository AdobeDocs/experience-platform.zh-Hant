---
description: 使用[!UICONTROL 設定檔擴充]儀表板來瞭解設定檔擴充工作是否成功執行並完成，並檢視基本量度以評估擴充的有效性。
solution: Experience Platform
title: 監視設定檔擴充工作
type: Tutorial
exl-id: 096a2212-ed7f-4419-8ead-fa1ca01c2804
source-git-commit: 14e3eff3ea2469023823a35ee1112568f5b5f4f7
workflow-type: tm+mt
source-wordcount: '764'
ht-degree: 2%

---

# 監視UI中的設定檔擴充工作 {#monitor-profile-enrichment}

使用[!UICONTROL 設定檔擴充]儀表板來瞭解設定檔擴充工作是否成功執行並完成，並檢視基本量度以評估擴充的有效性。

在[平台UI](https://platform.adobe.com)中，從左側導覽選取&#x200B;**[!UICONTROL 監視]**&#x200B;以存取[!UICONTROL 監視]儀表板。 在檢視選擇器中，選取&#x200B;**B2B流量**&#x200B;以檢視特定於[Real-Time CDP B2B](/help/rtcdp/b2b-overview.md)的儀表板元素。  [!UICONTROL 監視]儀表板包含最近一次成功執行的基本量度，以及過去90天內的每日工作狀態。

## 相關帳戶設定檔擴充 {#related-accounts}

[!UICONTROL 相關帳戶]儀表板會顯示基本量度，以及[相關帳戶](/help/rtcdp/b2b-ai-ml-services/related-accounts.md)設定檔擴充特有的每日工作狀態。

![如何在Experience PlatformUI中進入設定檔擴充工作監視畫面的視覺指示。](/help/dataflows/assets/ui/b2b/monitoring-profile-enrichment-jobs.png)

**[!UICONTROL Metrics]**&#x200B;卡片中的資料包含最近成功執行「相關帳戶」工作的基本量度。

相關帳戶設定檔擴充工作可使用下列量度：

| 量度 | 說明 |
| --------- | ---------- |
| **[!UICONTROL 帳戶設定檔總數]** | 表示您的組織可存取的帳戶設定檔總數。 |
| **[!UICONTROL 帳戶群組]** | 表示相關帳戶機器學習工作所叢集的帳戶群組數目。 |
| **[!UICONTROL 單一帳戶群組]** | 表示未與其他帳戶一起分組的帳戶數。 |
| **[!UICONTROL 最大群組大小]** | 指示最大相關帳戶群組的大小。 允許的群組大小上限為30。 |
| **[!UICONTROL 群組大小中位數]** | 表示組織中相關帳戶群組的大小中位數。 |
| **[!UICONTROL 上次成功執行]** | 指示上次成功執行相關帳戶工作的日期和時間。 |
| **[!UICONTROL 狀態]** | 表示相關帳戶工作的狀態（成功、失敗或處理）。 |
| **[!UICONTROL 訊息]** | 表示特定工作執行的錯誤或警告訊息。 |

## 銷售線索與帳戶比對設定檔擴充 {#lead-to-account-matching}

[!UICONTROL 銷售機會與帳戶比對]儀表板顯示[銷售機會與帳戶比對](/help/rtcdp/b2b-ai-ml-services/lead-to-account-matching.md)設定檔擴充的特定基本量度和每日工作執行狀態。

![潛在客戶帳戶比對設定檔擴充](/help/dataflows/assets/ui/b2b/mpc-lead-to-account-matching.png)

下列量度可用於銷售線索與帳戶比對設定檔擴充工作：

| 量度 | 說明 |
| --------- | ---------- |
| **[!UICONTROL 帳戶總人數]** | 表示與帳戶相關聯的總人數。 |
| **[!UICONTROL 帳戶總數]** | 表示帳戶總數。 |
| **[!UICONTROL 具有帳戶的現有人員]** | 表示已與來自資料來源的帳戶相關聯的人數。 |
| **[!UICONTROL 個人符合]** | 表示符合帳戶的人員數量。 |
| **[!UICONTROL 個人不相符]** | 表示不符合帳戶的人員數量。 |
| **[!UICONTROL 上次成功執行]** | 表示上次成功銷售機會與帳戶相符工作執行的日期和時間。 |
| **[!UICONTROL 狀態]** | 指出銷售機會與帳戶比對工作的狀態（成功、失敗或處理）。 |

## 預測性銷售線索和帳戶評分設定檔擴充 {#predictive-lead-to-account-scoring}

[!UICONTROL 預測性銷售線索和帳戶評分]儀表板會顯示[預測性銷售線索和帳戶評分](/help/rtcdp/b2b-ai-ml-services/predictive-lead-and-account-scoring.md)個人檔案擴充的特定基本量度和每日工作執行狀態。

![預測性銷售線索與帳戶評分設定檔擴充](/help/dataflows/assets/ui/b2b/predictive-lead-and-account-scoring.png)

下列量度可用於預測性銷售線索與帳戶評分設定檔擴充工作：

| 量度 | 說明 |
| --------- | ---------- |
| **[!UICONTROL 工作開始]** | 表示預測性銷售線索與帳戶評分工作執行的開始日期和時間。 |
| **[!UICONTROL 處理時間]** | 完成工作所花費的總時間。 |
| **[!UICONTROL 分數名稱]** | 工作的分數名稱。 |
| **[!UICONTROL 設定檔型別]** | 分數的型別： <ul><li>人員</li><li>帳戶</li></ul>。 |
| **[!UICONTROL 工作型別]** | 工作的型別：<ul><li>評分</li><li>訓練</li>。 |
| **[!UICONTROL 狀態]** | 表示預測性銷售線索和帳戶評分工作的狀態（成功、失敗或處理）。 |

## UI控制項 {#ui-controls}

本節說明監視介面中的各種使用者介面(UI)選項，這些選項可讓您篩選頁面上顯示的測量結果。

使用箭頭圖示（![箭頭圖示](/help/dataflows/assets/ui/monitor-destinations/chevron-up.png)）來展開或關閉畫面頂端的卡片，此卡片會顯示設定檔擴充工作的相關快速資訊。

![顯示箭頭圖示UI控制項的熒幕錄製。](/help/dataflows/assets/ui/b2b/use-arrow-control.gif)

使用&#x200B;**[!UICONTROL 度量和圖形]**&#x200B;切換即可關閉顯示最新度量的檢視。

![熒幕錄製，顯示量度和圖表切換。](/help/dataflows/assets/ui/b2b/metrics-and-graphs-toggle.gif)

使用&#x200B;**[!UICONTROL 僅顯示失敗]**&#x200B;切換功能，僅顯示失敗的設定檔擴充工作。

![熒幕錄製，顯示[僅顯示失敗]切換。](/help/dataflows/assets/ui/b2b/show-failures-only.gif)

## 後續步驟 {#next-steps}

依照本教學課程，您現在可以成功監控和瞭解設定檔擴充工作的量度。 如需更多詳細資訊，請參閱下列檔案：

* [Real-Time CDP B2B中的相關帳戶](/help/rtcdp/b2b-ai-ml-services/related-accounts.md)
* [帳戶設定檔UI指南中的相關帳戶標籤](/help/rtcdp/accounts/account-profile-ui-guide.md)
* [Real-Time CDP B2B中的銷售線索與帳戶相符](/help/rtcdp/b2b-ai-ml-services/lead-to-account-matching.md)
* [Real-Time CDP B2B中的預測性銷售線索和帳戶評分](/help/rtcdp/b2b-ai-ml-services/predictive-lead-and-account-scoring.md)
