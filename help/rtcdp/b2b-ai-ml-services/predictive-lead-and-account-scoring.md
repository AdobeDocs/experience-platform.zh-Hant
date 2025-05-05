---
title: Real-Time CDP B2B中的預測性銷售線索和帳戶評分
type: Documentation
description: 有關Experience PlatformCDP B2B中預測性銷售線索和帳戶評分功能的概述和詳細資訊。
feature: Profiles, B2B
badgeB2B: label="B2B版本" type="Informative" url="https://helpx.adobe.com/tw/legal/product-descriptions/real-time-customer-data-platform-b2b-edition-prime-and-ultimate-packages.html newtab=true"
exl-id: d3afbabb-005d-4537-831a-857c88043759
source-git-commit: db57fa753a3980dca671d476521f9849147880f1
workflow-type: tm+mt
source-wordcount: '859'
ht-degree: 2%

---

# Real-Time CDP B2B中的預測性銷售線索和帳戶評分

B2B行銷人員在行銷漏斗頂端面臨多種挑戰。 為了有效率，B2B行銷人員需要自動化方式來限定大量人員，以便聚焦於高價值目標。 資格應該與最終銷售結果保持一致，而不僅僅是行銷轉換。

帳戶是購買B2B產品和服務的最終實體。 為了有效行銷和銷售，B2B行銷人員不僅要瞭解個人的情況，還要瞭解帳戶購買的可能性。

尤其是以帳戶為基礎的行銷，會將帳戶策略化為行銷目標。 帳戶購買傾向分數可大幅協助B2B行銷人員安排帳戶優先順序，以實現投資報酬的最大化。

預測性銷售線索和帳戶評分服務透過學習和預測機會階段轉換事件，並將個人活動彙總到帳戶層級以產生帳戶分數，來解決上述挑戰。 這些分數可做為個人設定檔和帳戶設定檔的自訂欄位取得，並可輕鬆作為區段條件納入，以縮小您的對象範圍。 彙總和單位層級也提供主要影響因素，以協助B2B行銷人員更瞭解哪些元素驅動分數。

## 瞭解預測性銷售線索和帳戶評分 {#how-it-works}

>[!NOTE]
>
>目前需要[!DNL Marketo]資料來源，因為它是唯一可在個人設定檔層級提供轉換事件的資料來源。

預測性銷售線索和帳戶評分使用樹狀結構（隨機森林/漸層提升）機器學習方法，以建立預測性銷售線索評分模型。

管理員可以設定多個設定檔評分目標（也稱為模型），每個已設定的轉換事件各一個，以便為每個已設定的目標產生個別的分數。

預測性銷售線索和帳戶評分支援下列轉換目標型別和欄位：

| 目標型別 | 欄位 |
| --- | --- |
| `leadOperation.convertLead` | <ul><li>`leadOperation.convertLead.convertedStatus`</li><li>`leadOperation.convertLead.assignTo`</li></ul> |
| `opportunityEvent.opportunityUpdated` | <ul><li>`opportunityEvent.dataValueChanges.attributeName`</li><li>`opportunityEvent.dataValueChanges.newValue`</li><li>`opportunityEvent.dataValueChanges.oldValue`</li>範例： `opportunityEvent.dataValueChanges.attributeName`等於`Stage`而`opportunityEvent.dataValueChanges.newValue`等於`Contract`</ul> |

演演算法會考量下列屬性和輸入資料：

* 個人設定檔

| XDM欄位 | 必要/選用 |
| --- | --- |
| `personComponents.sourceAccountKey.sourceKey` | 必要 |
| `workAddress.country` | 選填 |
| `extSourceSystemAudit.createdDate` | 必要 |
| `extendedWorkDetails.jobTitle` | 選填 |

>[!NOTE]
> 
>演演算法只會檢查Person：personComponents欄位群組中的`sourceAccountKey.sourceKey`欄位。

* 帳戶輪廓

| XDM欄位 | 必要/選用 |
| --- | --- |
| `accountKey.sourceKey` | 必要 |
| `extSourceSystemAudit.createdDate` | 必要 |
| `accountOrganization.industry` | 選填 |
| `accountOrganization.numberOfEmployees` | 選填 |
| `accountOrganization.annualRevenue.amount` | 選填 |

* 體驗事件

| XDM欄位 | 必要/選用 |
| --- | --- |
| `_id` | 必要 |
| `personKey.sourceKey` | 必要 |
| `timestamp` | 必要 |
| `eventType` | 必要 |

支援多種機型，並設定下列硬性限制：

* 每個生產沙箱有權使用五個模型。
* 每個開發沙箱都有權使用一種模型。

資料品質要求如下：

* 理想情況下，應提供兩年的最新資料以供訓練之用。
* 所需的最小資料長度為六個月加上預測期間。
* 對於每個預測目標，至少需要10個合格的轉換事件。

評分工作每天都會執行，且結果會儲存為設定檔屬性和帳戶屬性，然後可用於區段定義和個人化。 現成的Analytics深入分析也可在帳戶概述控制面板上取得。

請參閱檔案，以取得關於如何[管理預測性銷售線索和帳戶評分](/help/rtcdp/b2b-ai-ml-services/manage-predictive-lead-and-account-scoring.md)服務的詳細資訊。

## 檢視預測性銷售線索與帳戶評分結果 {#how-to-view}

工作執行後，結果會儲存在名稱為`LeadsAI.Scores` - ***分數名稱***&#x200B;的每個模型的新系統資料集中。 每個分數欄位群組都可以位於`{CUSTOM_FIELD_GROUP}.LeadsAI.the_score_name`。

| 屬性 | 說明 |
| --- | --- |
| 分數 | 設定檔在定義的時間範圍內達到預測目標的相對可能性。 此值不被視為機率百分比，而是個人資料相較於整體母體的可能性。 此分數介於0到100之間。 |
| 百分位數 | 此值提供設定檔相對於其他類似評分的設定檔的效能相關資訊。 百分位數的範圍介於1到100。 |
| 模型類型 | 選取的模型型別會指示這是人員或帳戶分數。 |
| 評分日期 | 評分發生的日期。 |
| 影響因素 | 個人資料可能發生轉換的預測原因。 因子由下列屬性組成：<ul><li>程式碼：對設定檔的預測分數產生正面影響的設定檔或行為屬性。</li><li>值：設定檔或行為屬性的值。</li><li>重要性：表示設定檔或行為屬性對預測分數（低、中、高）的權重。</li></ul> |

### 檢視客戶設定檔分數

若要檢視人員設定檔的預測性分數，請選取左側面板中客戶區段下的&#x200B;**[!UICONTROL 設定檔]**，然後輸入身分名稱空間和身分值。 完成後，請選取&#x200B;**[!UICONTROL 檢視]**。

接著，從清單中選取設定檔。

![客戶設定檔](/help/rtcdp/accounts/images/b2b-view-customer-profile.png)

**[!UICONTROL 詳細資料]**&#x200B;頁面現在包含預測性分數。 按一下預測性分數旁的圖表圖示。

![客戶設定檔預測性分數](/help/rtcdp/accounts/images/b2b-view-customer-profile-predictive-score.png)

快顯對話方塊會顯示分數、整體分數分佈、此分數的主要影響因素，以及分數目標定義。

![客戶設定檔預測性分數詳細資料](/help/rtcdp/accounts/images/b2b-view-customer-profile-predictive-score-details.png)

## 監控預測性銷售線索和帳戶評分工作 {#monitoring-jobs}

您可以透過儀表板監視基本度量和每日工作執行狀態。 這些量度包括：

* 已評分的人員/帳戶個人檔案總數
* 下一個評分工作（日期）
* 下一個訓練工作（日期）

如需詳細資訊，請參閱有關[針對預測性銷售線索和帳戶評分](/help/dataflows/ui/b2b/monitor-profile-enrichment.md)監視工作的檔案。
