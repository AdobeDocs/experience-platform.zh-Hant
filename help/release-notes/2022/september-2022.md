---
title: Adobe Experience Platform發行說明2022年9月
description: 2022年9月Adobe Experience Platform發行說明。
source-git-commit: a3f12b9524d393441923cd11e09ed3e406814691
workflow-type: tm+mt
source-wordcount: '1377'
ht-degree: 7%

---

# Adobe Experience Platform 發行說明

**發行日期：2022 年 9 月 28 日**

Adobe Experience Platform 現有功能更新：

- [Experience Data Model(XDM)](#xdm)
- [身份識別服務](#identity-service)
- [[!DNL Artificial Intelligence and Machine Learning Services]](#ai-and-ml-services)
- [來源](#sources)

## Experience Data Model(XDM) {#xdm}

XDM是開放原始碼規格，可針對匯入Adobe Experience Platform的資料提供通用結構和定義（結構）。 遵循XDM標準，所有客戶體驗資料皆可整合至通用表示法，以更快速、更整合的方式提供深入分析。 您可以從客戶動作中獲得寶貴的深入分析、透過區段定義客戶受眾，以及將客戶屬性用於個人化目的。

**新功能**

| 功能 | 說明 |
| --- | --- |
| 列舉和建議值的UI支援 | 除了啟用資料驗證的列舉外，您現在還可以 [新增或移除建議值](../../xdm/ui/fields/enum.md) 標準或自訂字串欄位，讓Platform使用者在建立區段時，有好記的值清單可供選取。 |

**新XDM元件**

| 元件類型 | 名稱 | 說明 |
| --- | --- | --- |
| 欄位群組 | [[!UICONTROL AJO分類欄位]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/decisioning/proposition-action.schema.json) | 與之互動的特定元素的屬性，會觸發主張事件。 |
| 欄位群組 | [[!UICONTROL MediaAnalytics互動詳細資訊]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-media-analytics.schema.json) | 追蹤一段時間內的媒體互動。 |
| 欄位群組 | [[!UICONTROL 媒體詳細資訊]](https://github.com/adobe/xdm/blob/master/components/datatypes/mediadetails.schema.json) | 跟蹤介質詳細資訊。 |
| 欄位群組 | [[!UICONTROL AdobeCJM ExperienceEvent — 曲面]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/customerJourneyManagement/surfaces.schema.json) | 說明Adobe Journey Optimizer中體驗事件的曲面。 |

{style=&quot;table-layout:auto&quot;}

**更新XDM元件**

| 元件類型 | 名稱 | 說明 |
| --- | --- | --- |
| 行為 | [[!UICONTROL 時間序列]](https://github.com/adobe/xdm/blob/master/components/behaviors/time-series.schema.json) | <ul><li>新增 `eventType`:<ul><li>`decisioning.propositionSend`</li><li>`decisioning.propositionDismiss`</li><li>`decisioning.propositionTrigger`</li><li>`media.downloaded`</li><li>`location.entry`</li><li>`location.exit`</li></ul></li><li>移除 `eventType`:<ul><li>`decisioning.propositionDeliver`</li><li>`media.stateStart`</li><li>`media.stateEnd`</li></ul></li></ul> |
| 欄位群組 | （多個） | [更新數個欄位說明](https://github.com/adobe/xdm/pull/1628/files) 跨Journey Orchestration元件。 |
| 欄位群組 | （多個） | [更新數個Adobe Workfront元件的標題](https://github.com/adobe/xdm/pull/1634/files) 一致性。 |
| 欄位群組 | [[!UICONTROL AJO分類欄位]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/decisioning/proposition-event-type.schema.json) | 將數個欄位的命名空間更新為 `xdm`. |
| 欄位群組 | [[!UICONTROL Journey Orchestration步驟事件常見欄位]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/journeyOrchestration/stepEvents/journeyStepEventCommonFieldsMixin.schema.json) | 新增欄位， `isReadSegmentTriggerStartEvent`. |
| 欄位群組 | [[!UICONTROL 預測天氣]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/shared/forecasted-weather.schema.json) | 變更 `xdm:uvIndex` 欄位新增為整數類型， `xdm` 命名空間至缺少的多個欄位。 |
| 欄位群組 | [[!UICONTROL 媒體詳細資訊]](https://github.com/adobe/xdm/blob/master/components/datatypes/mediadetails.schema.json) | `xdm:endUserIDs` 和 `xdm:implementationDetails` 已從欄位組中刪除。 |
| 資料類型 | （多個） | [已更新多個媒體屬性名稱](https://github.com/adobe/xdm/pull/1626/files) 以保持一致性。 |
| 資料類型 | [[!UICONTROL 實作詳細資料]](https://github.com/adobe/xdm/blob/master/components/datatypes/industry-verticals/implementationdetails.schema.json) | 已新增已知的顫動名稱。 |
| 資料類型 | [[!UICONTROL 興趣點詳細資訊]](https://github.com/adobe/xdm/blob/master/components/datatypes/poi-detail.schema.json) | 資料類型現在可以接受與地標相關聯的中繼資料索引鍵/值組清單。 |
| 資料類型 | [[!UICONTROL 主張行動]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/decisioning/proposition-action.schema.json) | [!DNL AJO Classification Fields] 已重新命名為 [!UICONTROL 主張行動]. |
| 資料類型 | [[!UICONTROL 主張事件類型]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/decisioning/proposition-event-type.schema.json) | [!DNL AJO Classification Fields] 已重新命名為 [!UICONTROL 主張行動]. |
| （多個） | （多個） | 實驗性質 [穩定於所有B2B元件](https://github.com/adobe/xdm/pull/1617/files). |
| （多個） | （多個） | Adobe Journey Optimizer實體 [穩定](https://github.com/adobe/xdm/pull/1625/files). |
| （多個） | （多個） | 幾個實驗元件中特定欄位的命名空間已 [已更新一致性](https://github.com/adobe/xdm/pull/1626/files). |

{style=&quot;table-layout:auto&quot;}

如需Platform中XDM的詳細資訊，請參閱 [XDM系統概觀](../../xdm/home.md).

## 身份識別服務 {#identity-service}

要提供相關的數位體驗，必須全面了解客戶。 當您的客戶資料分散到不同的系統中，導致每個客戶看起來都有多個「身分」時，就會更難做到這一點。

Adobe Experience Platform Identity Service可跨裝置和系統橋接身分，協助您即時提供具影響力的個人數位體驗，進而協助您更清楚掌握客戶及其行為。

**更新功能**

| 功能 | 說明 |
| --- | --- |
| 支援刪除資料集 | Identity Service現在支援透過 [目錄服務API](https://developer.adobe.com/experience-platform-apis/references/catalog/)、UI或資料衛生。 閱讀指南 [在UI中刪除資料集](../../catalog/datasets/user-guide.md#delete-a-dataset) 以取得更多資訊。 |

若要進一步了解Identity Service，請閱讀 [Identity服務概述](../../identity-service/home.md).

## [!DNL Artificial Intelligence/Machine Learning services] {#ai-and-ml-services}

AI/ML服務讓行銷分析師和從業人員能夠在客戶體驗使用案例中運用人工智慧和機器學習的強大功能。 這可讓行銷分析人員使用業務層級設定，針對公司的需求設定特定的模型，而不需要資料科學的專業知識。

### Attribution AI

Attribution AI 可將點數歸因到促成轉換事件的接觸點。 行銷人員可善用此工具，協助量化客戶歷程中各個獨立行銷接觸點對行銷的影響。

| 功能 | 說明 |
| --- | --- |
| 儲存草稿例項 | 這項新功能可讓行銷分析人員在設定期間將模型設定儲存為草稿例項，並繼續編輯草稿，直到訓練及計分完成為止。 當使用者在設定工作流程中有多個要定義的欄位，且一次無法完成，或一或多個資料集統計資料（例如欄完整性）使用時，此功能有所幫助的案例包括但不限於需要處理時間才能使用。 閱讀 [Attribution AI使用指南](../../intelligent-services/attribution-ai/user-guide.md) 了解更多。 |
| 治理政策 | 在使用者透過設定工作流程提交以建立執行個體後，新的原則實施服務會檢查是否有任何違反資料使用原則的情況，並在彈出式視窗中顯示詳細資訊。 它可確保資料操作和行銷動作符合Adobe Experience Platform上設定的資料使用原則。 |

如需Attribution AI的詳細資訊，請 [Attribution AI概述](../../intelligent-services/attribution-ai/overview.md). 如需資料控管原則的資訊，請參閱 [原則概述](../../data-governance/policies/overview.md).

### Customer AI

Real-time Customer Data Platform提供的Customer AI可產生自訂傾向分數，例如大規模個別設定檔的流失和轉換。

| 功能 | 說明 |
| --- | --- |
| 儲存草稿例項 | 這項新功能可讓行銷分析人員在設定期間將模型設定儲存為草稿例項，並繼續編輯草稿，直到訓練及計分完成為止。 當使用者在設定工作流程中有多個要定義的欄位，且一次無法完成，或一或多個資料集統計資料（例如欄完整性）使用時，此功能有所幫助的案例包括但不限於需要處理時間才能使用。 閱讀 [Customer AI使用手冊](../../intelligent-services/customer-ai/user-guide/configure.md) 了解更多。 |
| 治理政策 | 在使用者透過設定工作流程提交以建立執行個體後，新的原則實施服務會檢查是否有任何違反資料使用原則的情況，並在彈出式視窗中顯示詳細資訊。 它可確保資料操作和行銷動作符合Adobe Experience Platform上設定的資料使用原則。 |

如需Customer AI的詳細資訊，請參閱 [Customer AI概觀](../../intelligent-services/customer-ai/overview.md). 如需資料控管原則的資訊，請參閱 [原則概述](../../data-governance/policies/overview.md).

## 來源 {#sources}

Adobe Experience Platform可內嵌來自外部來源的資料，同時允許您使用Platform服務來建構、加標籤及增強該資料。 您可以內嵌來自各種來源的資料，例如Adobe應用程式、雲端儲存、協力廠商軟體和您的CRM系統。

Experience Platform提供RESTful API和互動式UI，讓您輕鬆為各種資料提供者設定來源連線。 這些源連接允許您驗證並連接到外部儲存系統和CRM服務、設定獲取運行時間以及管理資料獲取吞吐量。

**更新功能**

| 功能 | 說明 |
| --- | --- |
| Audience Manager區段母體對即時客戶設定檔的影響 | 首次使用Audience Manager來源將Audience Manager區段傳送至Platform時，擷取大量Audience Manager區段母體會直接影響您的設定檔總數。 這表示選取所有區段可能會導致設定檔計數超過您的授權使用權限。 如需詳細資訊，請閱讀 [Audience Manager來源概觀](../../sources/connectors/adobe-applications/audience-manager.md). 如需您使用授權的詳細資訊，請參閱 [使用授權使用控制面板](../../dashboards/guides/license-usage.md). |

若要進一步了解來源，請閱讀 [來源概觀](../../sources/home.md).