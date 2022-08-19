---
title: 即時CDP B2B中的預測線索和帳戶評分
type: Documentation
description: 有關Experience PlatformCDP B2B中預測銷售線索和帳戶記分功能的概述和詳細資訊。
source-git-commit: 5ac8e099a6de563371f9a53a8b4816e6cf4d1953
workflow-type: tm+mt
source-wordcount: '858'
ht-degree: 2%

---

# 即時CDP B2B中的預測線索和帳戶評分

B2B營銷人員在營銷渠道的頂端面臨著多重挑戰。 為了有效，B2B營銷人員需要一種自動化的方法來鑑定大量人員，以便他們能夠專注於高價值目標。 資格應與最終銷售結果一致，而不僅是營銷轉換。

客戶是購買B2B產品和服務的最終實體。 為了有效地營銷和銷售，B2B營銷人員不僅要瞭解個人的購買可能性，還要瞭解客戶的購買可能性。

特別是基於客戶的市場營銷，將客戶作為市場營銷目標進行戰略規劃。 客戶購買傾向評分大大有助於B2B營銷人員在客戶中排定優先順序，以最大化其投資回報。

預測性線索和帳戶評分服務通過學習機會階段轉換事件並對其進行預測，以及將人員活動聚合到帳戶級別以生成帳戶分數，從而解決上述挑戰。 這些分數可以作為個人配置檔案和帳戶配置檔案上的自定義欄位隨時可用，並且可以輕鬆地作為段標準包括在內，以優化您的受眾。 在總量和單位層面，也有最大的影響因素，幫助B2B營銷人員更好地理解是什麼因素驅動了分數。

## 瞭解預測線索和帳戶評分 {#how-it-works}

>[!NOTE]
>
>[!DNL Marketo] 資料源當前是必需的，因為它是唯一可以在人員配置檔案層提供轉換事件的資料源。

預測線索和帳戶評分使用基於樹（隨機林/梯度提升）的機器學習方法來構建預測線索評分模型。

管理員可以配置多個配置檔案計分目標（也稱為模型），每個配置轉換事件都配置一個目標，允許為每個配置目標生成單獨的分數。

預測銷售線索和帳戶記分支援以下轉換目標類型和欄位：

| 目標類型 | 欄位 |
| --- | --- |
| `leadOperation.convertLead` | <ul><li>`leadOperation.convertLead.convertedStatus`</li><li>`leadOperation.convertLead.assignTo`</li></ul> |
| `opportunityEvent.opportunityUpdated` | <ul><li>`opportunityEvent.dataValueChanges.attributeName`</li><li>`opportunityEvent.dataValueChanges.newValue`</li><li>`opportunityEvent.dataValueChanges.oldValue`</li>示例： `opportunityEvent.dataValueChanges.attributeName` 等於 `Stage` 和 `opportunityEvent.dataValueChanges.newValue` 等於 `Contract`</ul> |

算法考慮了以下屬性和輸入資料：

* 人員配置檔案

| XDM欄位 | 必填/選填 |
| --- | --- |
| `personComponents.sourceAccountKey.sourceKey` | 必填 |
| `workAddress.country` | 選填 |
| `extSourceSystemAudit.createdDate` | 必填 |
| `extendedWorkDetails.jobTitle` | 選填 |

>[!NOTE]
> 
>該算法僅檢查 `sourceAccountKey.sourceKey` 「人員：人員」欄位組中的欄位。

* 帳戶配置檔案

| XDM欄位 | 必填/選填 |
| --- | --- |
| `accountKey.sourceKey` | 必填 |
| `extSourceSystemAudit.createdDate` | 必填 |
| `accountOrganization.industry` | 選填 |
| `accountOrganization.numberOfEmployees` | 選填 |
| `accountOrganization.annualRevenue.amount` | 選填 |

* 體驗事件

| XDM欄位 | 必填/選填 |
| --- | --- |
| `_id` | 必填 |
| `personKey.sourceKey` | 必填 |
| `timestamp` | 必填 |
| `eventType` | 必填 |

支援多個型號，並設定了以下硬限制：

* 每個生產沙箱都有5種型號。
* 每個開發沙箱都有權使用一種模型。

資料質量要求如下：

* 理想情況下，有兩年的最新資料用於培訓目的。
* 所需資料的最小長度為6個月加預測窗口。
* 對於每個預測目標，至少需要10個合格轉換事件。

記分作業每天運行，結果將保存為配置檔案屬性和帳戶屬性，然後可在段定義和個性化中使用。 在客戶概述儀表板上也提供了現成分析見解。

有關如何執行以下操作的詳細資訊，請參閱文檔 [管理預測性銷售線索和帳戶記分](/help/rtcdp/b2b-ai-ml-services/manage-predictive-lead-and-account-scoring.md) 服務。

## 查看預測潛在顧客和帳戶評分結果 {#how-to-view}

作業運行後，結果將保存在名稱下每個模型的新系統資料集中 `LeadsAI.Scores` - ***分數名稱***。 每個得分欄位組可位於 `{CUSTOM_FIELD_GROUP}.LeadsAI.the_score_name`。

| 屬性 | 說明 |
| --- | --- |
| 分數 | 在所定義的時間範圍內，輪廓實現預測目標的相對似然。 此值不應被視為概率百分比，而應被視為與總體人口相比的概率。 此分數範圍為0到100。 |
| 百分點 | 此值提供有關配置檔案相對於其他類似得分的配置檔案的效能的資訊。 百分位數範圍從1到100。 |
| 模型類型 | 選定的模型類型，指明這是人員還是帳戶分數。 |
| 分數日期 | 發生計分的日期。 |
| 影響因素 | 關於配置檔案可能轉換的原因的預測原因。 因素包括以下屬性：<ul><li>代碼：對配置檔案的預測得分產生積極影響的配置檔案或行為屬性。</li><li>值：配置檔案或行為屬性的值。</li><li>重要性：指示配置檔案或行為屬性對預測得分（低、中、高）的權重。</li></ul> |

### 查看客戶配置檔案分數

要查看人員配置檔案的預測分數，請選擇 **[!UICONTROL 配置檔案]** 在左側面板的customer部分下，然後輸入標識名稱空間和標識值。 完成後，選擇 **[!UICONTROL 視圖]**。

接下來，從清單中選擇配置檔案。

![客戶配置檔案](/help/rtcdp/accounts/images/b2b-view-customer-profile.png)

的 **[!UICONTROL 詳細資訊]** 頁面現在包括預測分數。 按一下預測分數旁邊的圖表表徵圖。

![客戶配置檔案預測得分](/help/rtcdp/accounts/images/b2b-view-customer-profile-predictive-score.png)

彈出對話框顯示得分、總得分分佈、此得分的最大影響因素以及得分目標定義。

![客戶配置檔案預測分數詳細資訊](/help/rtcdp/accounts/images/b2b-view-customer-profile-predictive-score-details.png)

## 監視預測性線索和帳戶記分作業 {#monitoring-jobs}

您可以通過儀表板監視基本度量和日常作業運行狀態。 指標包括：

* 個人/帳戶配置檔案總計
* 下一計分作業（日期）
* 下一個培訓作業（日期）

有關詳細資訊，請參閱 [預測線索和帳戶記分的監視作業](/help/dataflows/ui/b2b/monitor-profile-enrichment.md)。
