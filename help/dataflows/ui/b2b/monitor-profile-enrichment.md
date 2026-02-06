---
description: 使用[!UICONTROL Profile Enrichment]儀表板來瞭解設定檔擴充工作是否成功執行並完成，並檢視基本量度以評估擴充的有效性。
solution: Experience Platform
title: 監視設定檔擴充工作
type: Tutorial
badgeB2B: label="B2B edition" type="Informative" url="https://experienceleague.adobe.com/docs/experience-platform/rtcdp/intro/rtcdp-intro/overview.html#rtcdp-editions" newtab=true
exl-id: 096a2212-ed7f-4419-8ead-fa1ca01c2804
source-git-commit: 0e993f7d0791f5f6f9dce63eb3848609d892e788
workflow-type: tm+mt
source-wordcount: '696'
ht-degree: 1%

---

# 監視UI中的設定檔擴充工作 {#monitor-profile-enrichment}

使用[!UICONTROL Profile Enrichment]儀表板來瞭解設定檔擴充工作是否成功執行並完成，並檢視基本量度以評估擴充的有效性。

在[Experience Platform UI](https://platform.adobe.com)中，從左側導覽選取&#x200B;**[!UICONTROL Monitoring]**&#x200B;以存取[!UICONTROL Monitoring]儀表板。 在檢視選擇器中，選取&#x200B;**B2B流量**&#x200B;以檢視特定於[Real-Time CDP B2B](/help/rtcdp/b2b-overview.md)的儀表板元素。  [!UICONTROL Monitoring]儀表板包含最近一次成功執行的基本量度，以及過去90天內的每日工作狀態。

## 相關帳戶設定檔擴充 {#related-accounts}

[!UICONTROL Related accounts]儀表板會顯示基本量度，以及[相關帳戶](/help/rtcdp/b2b-ai-ml-services/related-accounts.md)設定檔擴充專屬的每日工作狀態。

![如何在Experience Platform UI中存取設定檔擴充工作監視畫面的視覺指示。](/help/dataflows/assets/ui/b2b/monitoring-profile-enrichment-jobs.png)

**[!UICONTROL Metrics]**&#x200B;卡片中的資料包含最近一次成功執行「相關帳戶」作業的基本量度。

相關帳戶設定檔擴充工作可使用下列量度：

| 量度 | 說明 |
| --------- | ---------- |
| **[!UICONTROL Total account profiles]** | 表示您的組織可存取的帳戶設定檔總數。 |
| **[!UICONTROL Account groups]** | 表示相關帳戶機器學習工作所叢集的帳戶群組數目。 |
| **[!UICONTROL Single-account groups]** | 表示未與其他帳戶一起分組的帳戶數。 |
| **[!UICONTROL Largest group size]** | 指示最大相關帳戶群組的大小。 允許的群組大小上限為30。 |
| **[!UICONTROL Median group size]** | 表示組織中相關帳戶群組的大小中位數。 |
| **[!UICONTROL Last successful run]** | 指示上次成功執行相關帳戶工作的日期和時間。 |
| **[!UICONTROL Status]** | 表示相關帳戶工作的狀態（成功、失敗或處理）。 |
| **[!UICONTROL Message]** | 表示特定工作執行的錯誤或警告訊息。 |

## 銷售線索與帳戶比對設定檔擴充 {#lead-to-account-matching}

[!UICONTROL Lead to account matching]儀表板會顯示基本量度，以及[潛在客戶與帳戶相符](/help/rtcdp/b2b-ai-ml-services/lead-to-account-matching.md)設定檔擴充的特定每日工作執行狀態。

![潛在客戶帳戶比對設定檔擴充](/help/dataflows/assets/ui/b2b/mpc-lead-to-account-matching.png)

下列量度可用於銷售線索與帳戶比對設定檔擴充工作：

| 量度 | 說明 |
| --------- | ---------- |
| **[!UICONTROL Total persons with accounts]** | 表示與帳戶相關聯的總人數。 |
| **[!UICONTROL Total accounts]** | 表示帳戶總數。 |
| **[!UICONTROL Existing persons with accounts]** | 表示已與來自資料來源的帳戶相關聯的人數。 |
| **[!UICONTROL Persons matched]** | 表示符合帳戶的人員數量。 |
| **[!UICONTROL Persons unmatched]** | 表示不符合帳戶的人員數量。 |
| **[!UICONTROL Last successful run]** | 表示上次成功銷售機會與帳戶相符工作執行的日期和時間。 |
| **[!UICONTROL Status]** | 指出銷售機會與帳戶比對工作的狀態（成功、失敗或處理）。 |

## 預測性銷售線索和帳戶評分設定檔擴充 {#predictive-lead-to-account-scoring}

[!UICONTROL Predictive lead and account scoring]儀表板會顯示[預測性銷售線索和帳戶評分](/help/rtcdp/b2b-ai-ml-services/predictive-lead-and-account-scoring.md)個人檔案擴充的特定基本量度和每日工作執行狀態。

![預測性銷售線索與帳戶評分設定檔擴充](/help/dataflows/assets/ui/b2b/predictive-lead-and-account-scoring.png)

下列量度可用於預測性銷售線索與帳戶評分設定檔擴充工作：

| 量度 | 說明 |
| --------- | ---------- |
| **[!UICONTROL Job start]** | 表示預測性銷售線索與帳戶評分工作執行的開始日期和時間。 |
| **[!UICONTROL Processing time]** | 完成工作所花費的總時間。 |
| **[!UICONTROL Score name]** | 工作的分數名稱。 |
| **[!UICONTROL Profile type]** | 分數的型別： <ul><li>人員</li><li>帳戶</li></ul>。 |
| **[!UICONTROL Job type]** | 工作的型別：<ul><li>評分</li><li>訓練</li>。 |
| **[!UICONTROL Status]** | 表示預測性銷售線索和帳戶評分工作的狀態（成功、失敗或處理）。 |

## UI控制項 {#ui-controls}

本節說明監視介面中的各種使用者介面(UI)選項，這些選項可讓您篩選頁面上顯示的測量結果。

使用箭頭圖示（![箭頭圖示](/help/images/icons/chevron-up.png)）來展開或關閉畫面頂端的卡片，此卡片會顯示設定檔擴充工作的相關快速資訊。

![顯示箭頭圖示UI控制項的熒幕錄製。](/help/dataflows/assets/ui/b2b/use-arrow-control.gif)

使用&#x200B;**[!UICONTROL Metrics and graphs]**&#x200B;切換關閉顯示最新量度的檢視。

![熒幕錄製，顯示量度和圖表切換。](/help/dataflows/assets/ui/b2b/metrics-and-graphs-toggle.gif)

使用&#x200B;**[!UICONTROL Show failures only]**&#x200B;切換以僅顯示失敗的設定檔擴充工作。

![熒幕錄製，顯示[僅顯示失敗]切換。](/help/dataflows/assets/ui/b2b/show-failures-only.gif)

## 後續步驟 {#next-steps}

依照本教學課程，您現在可以成功監控和瞭解設定檔擴充工作的量度。 如需更多詳細資訊，請參閱下列檔案：

* [Real-Time CDP B2B中的相關帳戶](/help/rtcdp/b2b-ai-ml-services/related-accounts.md)
* [帳戶設定檔UI指南中的相關帳戶標籤](/help/rtcdp/accounts/account-profile-ui-guide.md)
* [Real-Time CDP B2B中的銷售線索與帳戶相符](/help/rtcdp/b2b-ai-ml-services/lead-to-account-matching.md)
* [Real-Time CDP B2B中的預測性銷售線索和帳戶評分](/help/rtcdp/b2b-ai-ml-services/predictive-lead-and-account-scoring.md)
