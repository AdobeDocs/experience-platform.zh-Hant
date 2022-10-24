---
title: Real-Time CDP B2B中的預測性銷售機會和帳戶分數
type: Documentation
description: 有關Experience PlatformCDP B2B中預測性潛在客戶和帳戶計分功能的概述和詳細資訊。
exl-id: d3afbabb-005d-4537-831a-857c88043759
source-git-commit: 14e3eff3ea2469023823a35ee1112568f5b5f4f7
workflow-type: tm+mt
source-wordcount: '858'
ht-degree: 2%

---

# Real-Time CDP B2B中的預測性銷售機會和帳戶分數

B2B行銷人員在行銷漏斗頂端面臨多項挑戰。 為了有效運作，B2B行銷人員需要自動化的方式，讓大量人員符合資格，以便專注於高價值目標。 資格應與最終銷售結果保持一致，而不僅是行銷轉換。

帳戶是購買B2B產品和服務的最終實體。 為了有效行銷和銷售，B2B行銷人員不僅需要了解個人的購買機率，還需要了解帳戶的購買可能性。

以帳戶為基礎的行銷，尤其是將帳戶策略化為行銷目標。 帳戶購買傾向分數可協助B2B行銷人員在帳戶之間排定優先順序，以最大化其投資報酬率。

預測性銷售機會和帳戶分數服務通過學習機會階段轉換事件並預測機會階段轉換事件，並將人員活動聚合到帳戶級別以生成帳戶分數，從而解決上述挑戰。 這些分數可隨時以人員設定檔和帳戶設定檔的自訂欄位形式提供，且可輕鬆納入為區段條件，以精簡您的對象。 匯總和單位層級也提供最具影響力的因素，協助B2B行銷人員更清楚了解促成分數的因素。

## 了解預測性銷售機會和帳戶計分 {#how-it-works}

>[!NOTE]
>
>[!DNL Marketo] 資料來源目前為必要項目，因為這是唯一可在人員設定檔層級提供轉換事件的資料來源。

「預測銷售機會」和「帳戶計分」使用樹狀結構（隨機森林/漸層提升）機器學習方法來建立預測銷售機會計分模型。

管理員能設定多個設定檔計分目標（也稱為模型），每個設定的轉換事件各一個，以便為每個設定的目標產生不同的分數。

預測性銷售機會和帳戶分數支援下列轉換目標類型和欄位：

| 目標類型 | 欄位 |
| --- | --- |
| `leadOperation.convertLead` | <ul><li>`leadOperation.convertLead.convertedStatus`</li><li>`leadOperation.convertLead.assignTo`</li></ul> |
| `opportunityEvent.opportunityUpdated` | <ul><li>`opportunityEvent.dataValueChanges.attributeName`</li><li>`opportunityEvent.dataValueChanges.newValue`</li><li>`opportunityEvent.dataValueChanges.oldValue`</li>範例： `opportunityEvent.dataValueChanges.attributeName` 等於 `Stage` 和 `opportunityEvent.dataValueChanges.newValue` 等於 `Contract`</ul> |

演算法考慮了下列屬性和輸入資料：

* 人員設定檔

| XDM欄位 | 必填/選填 |
| --- | --- |
| `personComponents.sourceAccountKey.sourceKey` | 必填 |
| `workAddress.country` | 選填 |
| `extSourceSystemAudit.createdDate` | 必填 |
| `extendedWorkDetails.jobTitle` | 選填 |

>[!NOTE]
> 
>算法只會檢查 `sourceAccountKey.sourceKey` 欄位（在「人員：personComponents」欄位組中）。

* 帳戶設定檔

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

支援多個模型，並設定下列硬限制：

* 每個生產沙箱皆有權使用五種型號。
* 每個開發沙箱都有權使用一個模型。

資料品質要求如下：

* 理想情況下，為培訓目的提供兩年的最新資料。
* 所需資料的最小長度為6個月加上預測窗口。
* 對於每個預測目標，至少需要10個合格的轉換事件。

計分工作會每天執行，結果會儲存為設定檔屬性和帳戶屬性，然後用於區段定義和個人化。 帳戶概述控制面板也提供現成可用的分析分析。

如需如何取得的詳細資訊，請參閱本檔案 [管理預測性銷售機會和帳戶計分](/help/rtcdp/b2b-ai-ml-services/manage-predictive-lead-and-account-scoring.md) 服務。

## 查看預測性潛在客戶和帳戶評分結果 {#how-to-view}

作業執行後，結果會以名稱儲存至每個模型的新系統資料集 `LeadsAI.Scores` - ***分數名稱***. 每個分數欄位群組位於 `{CUSTOM_FIELD_GROUP}.LeadsAI.the_score_name`.

| 屬性 | 說明 |
| --- | --- |
| 分數 | 設定檔在定義的時間範圍內達到預測目標的相對可能性。 此值不會視為機率百分比，而是設定檔與整體母體比較的可能性。 此分數的範圍介於0到100之間。 |
| 百分位數 | 此值提供關於設定檔相對於其他類似計分設定檔之效能的資訊。 百分位數範圍從1到100。 |
| 模型類型 | 選定的模型類型，指明這是人員還是帳戶分數。 |
| 分數日期 | 發生分數的日期。 |
| 影響因素 | 設定檔可能轉換的預測原因。 因素包括下列屬性：<ul><li>代碼：正面影響設定檔預測分數的設定檔或行為屬性。</li><li>值：設定檔或行為屬性的值。</li><li>重要性：指出設定檔或行為屬性對預測分數（低、中、高）的加權。</li></ul> |

### 檢視客戶設定檔分數

若要檢視人員設定檔的預測分數，請選取 **[!UICONTROL 設定檔]** 在左側面板的「客戶」區段下，然後輸入身分命名空間和身分值。 完成後，請選取 **[!UICONTROL 檢視]**.

接下來，從清單中選取設定檔。

![客戶設定檔](/help/rtcdp/accounts/images/b2b-view-customer-profile.png)

此 **[!UICONTROL 詳細資料]** 頁面現在包含預測分數。 按一下預測分數旁的圖表圖示。

![客戶設定檔預測分數](/help/rtcdp/accounts/images/b2b-view-customer-profile-predictive-score.png)

彈出式對話方塊會顯示分數、整體分數分佈、此分數的最大影響因素，以及分數目標定義。

![客戶設定檔預測分數詳細資料](/help/rtcdp/accounts/images/b2b-view-customer-profile-predictive-score-details.png)

## 監控預測性潛在客戶和帳戶計分作業 {#monitoring-jobs}

您可以透過控制面板監控基本量度和每日作業執行狀態。 量度包括：

* 計分的人員/帳戶設定檔總數
* 下次計分作業（日期）
* 下一培訓作業（日期）

如需詳細資訊，請參閱 [監控預測潛在客戶和帳戶計分的作業](/help/dataflows/ui/b2b/monitor-profile-enrichment.md).
