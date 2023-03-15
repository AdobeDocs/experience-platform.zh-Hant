---
title: Adobe Experience Platform發行說明2022年9月
description: 2022年9月Adobe Experience Platform發行說明。
exl-id: a7a4dcf8-2cf3-4e39-879d-bdfcbacb737a
source-git-commit: 668b2624b7a23b570a3869f87245009379e8257c
workflow-type: tm+mt
source-wordcount: '2916'
ht-degree: 5%

---

# Adobe Experience Platform 發行說明

**發行日期：2022 年 9 月 28 日**

Adobe Experience Platform的新功能：

- [以屬性為基礎的存取控制](#abac)

Adobe Experience Platform 現有功能更新：

- [[!DNL Artificial Intelligence and Machine Learning Services]](#ai-and-ml-services)
- [稽核記錄](#audit-logs)
- [[!DNL Dashboards]](#dashboards)
- [資料收集](#data-collection)
- [目的地](#destinations)
- [Experience Data Model(XDM)](#xdm)
- [身份識別服務](#identity-service)
- [查詢服務](#query-service)
- [來源](#sources)

## 以屬性為基礎的存取控制 {#abac}

>[!IMPORTANT]
>
>從2022年10月起，將啟用基於屬性的存取控制。 若您想成為早期收養者，請聯絡您的Adobe代表。

基於屬性的存取控制是Adobe Experience Platform的一項功能，可讓具備隱私權意識的品牌在管理使用者存取方面擁有更大的彈性。 可將個別物件（例如結構欄位和區段）指派給使用者角色。 此功能可讓您授予或撤銷組織中特定Platform使用者對個別物件的存取權。

透過基於屬性的存取控制，貴組織的管理員可控制使用者對所有平台工作流程和資源的存取、敏感個人資料(SPD)、個人識別資訊(PII)和其他自訂資料類型。 管理員可以定義只有特定欄位和與這些欄位對應的資料存取權的使用者角色。

| 功能 | 說明 |
| --- | --- |
| 以屬性為基礎的存取控制 | 以屬性為基礎的存取控制可讓您為Experience Data Model(XDM)結構欄位和區段加上標籤，以定義組織或資料使用範圍。 同時，管理員可使用使用者和角色管理介面來定義涵蓋XDM架構欄位和區段的存取原則，以更妥善地管理提供給使用者或使用者群組（內部、外部或第三方使用者）的存取權。 如需詳細資訊，請參閱 [基於屬性的訪問控制概述](../../access-control/abac/overview.md). |
| 權限 | 權限是管理員可在其中定義用戶角色和訪問策略，以管理產品應用程式中功能和對象的訪問權限的Experience Cloud區域。 透過權限，您可以建立和管理角色、指派這些角色所需的資源權限，以及建立原則以運用標籤，並定義哪些使用者角色可存取特定平台資源。 權限也可讓您管理與特定角色相關聯的標籤、沙箱和使用者。如需詳細資訊，請參閱 [權限UI指南](../../access-control/abac/ui/browse.md). |

有關基於屬性的訪問控制的詳細資訊，請參見 [基於屬性的訪問控制概述](../../access-control/abac/overview.md). 有關基於屬性的訪問控制工作流的完整指南，請閱讀 [基於屬性的訪問控制端到端指南](../../access-control/abac/end-to-end-guide.md).

## [!DNL Artificial Intelligence/Machine Learning services] {#ai-and-ml-services}

AI/ML服務讓行銷分析師和從業人員能夠在客戶體驗使用案例中運用人工智慧和機器學習的強大功能。 這可讓行銷分析人員使用業務層級設定，針對公司的需求設定特定的模型，而不需要資料科學的專業知識。

### Attribution AI

Attribution AI 可將點數歸因到促成轉換事件的接觸點。 行銷人員可善用此工具，協助量化客戶歷程中各個獨立行銷接觸點對行銷的影響。

| 功能 | 說明 |
| --- | --- |
| 儲存草稿例項 | 這項新功能可讓行銷分析人員將模型設定儲存為草稿例項，並繼續編輯，直到完成為止，再進行訓練和計分。 此功能有幫助的案例包括：使用者在工作流程中有多個要定義的欄位，但由於時間限制而無法完成。 另一個案例是正在處理一或多個資料集統計資料，但尚未提供。 閱讀 [Attribution AI使用指南](../../intelligent-services/attribution-ai/user-guide.md#governance-policies) 了解更多。 |
| 治理政策 | 在使用者透過設定工作流程提交以建立執行個體後，新的原則實施服務會檢查是否有任何違反資料使用原則的情況，並在彈出式視窗中顯示詳細資訊。 它可確保資料操作和行銷動作符合Adobe Experience Platform上設定的資料使用原則。 |

如需Attribution AI的詳細資訊，請 [Attribution AI概述](../../intelligent-services/attribution-ai/overview.md). 如需資料控管原則的資訊，請參閱 [原則概述](../../data-governance/policies/overview.md).

### Customer AI

Real-time Customer Data Platform提供的Customer AI可產生自訂傾向分數，例如大規模個別設定檔的流失和轉換。

| 功能 | 說明 |
| --- | --- |
| 儲存草稿例項 | 這項新功能可讓行銷分析人員將模型設定儲存為草稿例項，並繼續編輯，直到完成為止，再進行訓練和計分。 此功能有幫助的案例包括：使用者在工作流程中有多個要定義的欄位，但由於時間限制而無法完成。 另一個案例是正在處理一或多個資料集統計資料，但尚未提供。 閱讀 [Customer AI使用手冊](../../intelligent-services/customer-ai/user-guide/configure.md#governance-policies) 了解更多。 |
| 治理政策 | 在使用者透過設定工作流程提交以建立執行個體後，新的原則實施服務會檢查是否有任何違反資料使用的原則，並在彈出式視窗中顯示詳細資訊。 它可確保資料操作和行銷動作符合Adobe Experience Platform上設定的資料使用原則。 |

如需Customer AI的詳細資訊，請參閱 [Customer AI概觀](../../intelligent-services/customer-ai/overview.md). 如需資料控管原則的資訊，請參閱 [原則概述](../../data-governance/policies/overview.md).

## 稽核記錄 {#audit-logs}

Experience Platform可讓您稽核各種服務和功能的使用者活動。 稽核記錄會提供關於執行動作的人員以及執行時間的資訊。

**更新功能**

| 功能 | 名稱 | 說明 |
| --- | --- | --- |
| 新增資源 | <ul><li>Attribution AI例項</li><li>Customer AI例項</li><li>資料流</li></ul> | 稽核記錄資源會在活動發生時自動記錄。 如果已啟用功能，則無需手動啟用日誌收集。 |

{style="table-layout:auto"}

如需Platform中稽核記錄所追蹤之不同資源專屬事件類型的詳細資訊，請參閱 [稽核記錄概述](../../landing/governance-privacy-security/audit-logs/overview.md).

## [!DNL Dashboards] {#dashboards}

Adobe Experience Platform提供多個控制面板，讓您透過這些控制面板檢視組織資料的重要深入分析（在每日快照中擷取）。

| 功能 | 說明 |
| --- | --- |
| 使用中標籤 | 在介面工具集資料庫中檢視時，使用中標籤可輕鬆識別控制面板中是否存在現有介面工具集。 這可讓您輕鬆避免重複，不過您仍可以多次新增相同的Widget。 |
| 使用者定義的控制面板 | 使用者定義的控制面板可讓您建立和管理自訂控制面板，協助您加速深入分析和自訂視覺效果。 透過使用者定義的控制面板，您可以建立、新增及編輯定制小工具，以視覺化與貴組織相關的關鍵量度。 閱讀 [功能指南](../../dashboards/user-defined-dashboards.md) 了解更多。 |
| Customer Data Platform Insights資料模型 | Customer Data Platform(CDP)Insights Data Model功能可公開資料模型和SQL，為各種設定檔、目的地和細分小工具提供深入分析。 您可以自訂這些SQL查詢範本，為您的行銷和關鍵績效指標使用案例建立CDP報表。 然後，這些前瞻分析便可作為使用者定義控制面板的自訂小工具。 閱讀 [CDP Insights Data Model功能指南](../../dashboards/cdp-insights-data-model.md) 了解更多。 |
| 對象重疊報表介面工具集 | 此介面工具集適用於兩者 [!UICONTROL 設定檔] 和 [!UICONTROL 區段] 控制面板。 報表提供依所選區段最高或最低重疊百分比排名的受眾順序清單。 從 [!UICONTROL 設定檔] 您可以透過合併政策，從所有可用區段中篩選及檢視對象重疊。 此 [!UICONTROL 區段] 控制面板可讓您依據特定區段來篩選對象重疊。<br>使用此分析來建立新的高效能區段，並避免將相同的對象傳送至不同的目的地。 此報表也有助於識別隱藏的深入分析，以改善細分或找出要追蹤的不重複設定檔。 閱讀 [設定檔](../../dashboards/guides/profiles.md#audience-overlap-report) 和 [區段](../../dashboards/guides/segments.md#audience-overlap-report) 介面工具集指南以深入了解。 |

如需 [!DNL Dashboards]，請參閱 [[!DNL Dashboards] 概述](../../dashboards/home.md).

## 資料收集 {#data-collection}

Adobe Experience Platform提供一套技術，可讓您收集用戶端客戶體驗資料，並傳送至Adobe Experience Platform Edge Network，以便在中加以擴充、轉換及分發至Adobe或非Adobe目的地。

**新功能或更新功能**

| 功能 | 說明 |
| --- | --- |
| Platform UI中的左側導覽整合 | 先前專屬於資料收集UI的所有功能（包括標籤、事件轉送和資料流），現在也可透過Experience Platform類別下的左側導覽取得 **[!UICONTROL 資料收集]**. 如此一來，使用Platform中的資料收集功能時，就不需要在UI之間切換。 |
| 標籤和事件轉送中的使用者歸因 | 清單可用時 [!UICONTROL 屬性] 在「標籤」和「事件轉送」中，每個列出的屬性現在都會顯示其上次更新的時間，以及哪個使用者進行了更新。 |
| [[!DNL Snap Conversions API] 擴充功能](https://exchange.adobe.com/apps/ec/108550) 用於事件轉送 | 您現在可以將資料傳送至 [!DNL Snapchat Conversions API] 使用 [事件轉送](../../tags/ui/event-forwarding/overview.md) 擴充功能。 如需如何驗證和使用API的詳細資訊，請參閱 [[!DNL Snapchat Marketing API] 檔案](https://marketingapi.snapchat.com/docs/conversion.html). |
| [[!DNL User-Agent Client Hints] 在Web SDK中](../../edge/fundamentals/user-agent-client-hints.md) | Web SDK現在支援 [[!DNL User-Agent Client Hints]](https://developer.chrome.com/docs/privacy-sandbox/user-agent/). 客戶端提示允許網站所有者訪問 [!DNL User-Agent] 串，但更能保護隱私。 |
| [網頁SDK逐頁移轉](../../edge/home.md#migrating-to-web-sdk) | 您現在可以從其他Experience Cloud程式庫(例如 [!DNL at.js]，至Web SDK，一次一頁。 這可以分階段移轉Web SDK，而不需一次移轉所有頁面。 |

{style="table-layout:auto"}

<!-- | [[!DNL Adobe Journey Optimizer] support for datastreams](../../edge/datastreams/overview.md#aep)| The Adobe Experience Platform service for datastreams now supports [!DNL Adobe Journey Optimizer]. This option allows you to use web and app-based inbound channels in [!DNL Adobe Journey Optimizer].|
-->

如需Platform中資料收集的詳細資訊，請參閱 [資料匯集概述](../../collection/home.md).

## [!DNL Destinations] {#destinations}

[!DNL Destinations] 預先建置與目的地平台的整合，可順暢地從Adobe Experience Platform啟動資料。 您可以使用目的地來針對跨通路行銷活動、電子郵件行銷活動、目標廣告和其他許多使用案例，啟用已知和未知的資料。

**新功能或更新功能**

| 功能 | 說明 |
| ----------- | ----------- |
| 目標 SDK | Destination SDK現在可為合作夥伴和客戶提供完整支援，協助他們建立批次（或檔案型）產品化或私人目的地。 如需詳細資訊，請參閱下列檔案頁面： <ul><li>[Destination SDK概述](/help/destinations/destination-sdk/overview.md)</li><li>[配置基於檔案的目標](/help/destinations/destination-sdk/configure-file-based-destination-instructions.md)</li><li>[為檔案型目的地配置檔案格式選項](/help/destinations/destination-sdk/configure-file-based-destination-instructions.md)</li><li>[測試您的檔案型目的地](/help/destinations/destination-sdk/file-based-destination-testing-overview.md)</li></ul> |

{style="table-layout:auto"}

**新目的地或更新目的地**

| 目的地 | 說明 |
| ----------- | ----------- |
| [[!DNL Adobe Campaign Managed Cloud Services]](../../destinations/catalog/email-marketing/adobe-campaign-managed-services.md) | Adobe Campaign Managed Cloud Services提供設計跨管道客戶體驗的平台，以及視覺化行銷活動策劃、即時互動管理和跨管道執行的環境。 [開始使用Campaign](https://experienceleague.adobe.com/docs/campaign/campaign-v8/start/get-started.html). 請注意，此整合適用於 [Adobe Campaign 8.4版或更高版本](https://experienceleague.adobe.com/docs/campaign/campaign-v8/new/release-notes.html?lang=en#release-8-4-1). |
| [[!DNL Salesforce CRM]](../../destinations/catalog/crm/salesforce.md) | 此 [!DNL Salesforce CRM] 目標已更新，以支援聯絡人和潛在客戶更新，並改善效能以加快更新。 |

{style="table-layout:auto"}

**新檔案或更新檔案**

| 文件 | 說明 |
| ----------- | ----------- |
| 目的地流量服務API檔案 | 此 [目的地API參考檔案](https://developer.adobe.com/experience-platform-apis/references/destinations/) 已更新，包含如何對檔案式目的地執行作業的指引。 稍後將新增串流目的地的作業。 |

如需目的地的詳細一般資訊，請參閱 [目的地概述](../../destinations/home.md).

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

{style="table-layout:auto"}

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

{style="table-layout:auto"}

如需Platform中XDM的詳細資訊，請參閱 [XDM系統概觀](../../xdm/home.md).

## 身份識別服務 {#identity-service}

要提供相關的數位體驗，必須全面了解客戶。 當您的客戶資料分散到不同的系統中，導致每個客戶看起來都有多個「身分」時，就會更難做到這一點。

Adobe Experience Platform Identity Service可跨裝置和系統橋接身分，協助您即時提供具影響力的個人數位體驗，進而協助您更清楚掌握客戶及其行為。

**更新功能**

| 功能 | 說明 |
| --- | --- |
| 支援刪除資料集 | Identity Service現在支援透過 [目錄服務API](https://developer.adobe.com/experience-platform-apis/references/catalog/)、UI或資料衛生。 閱讀指南 [在UI中刪除資料集](../../catalog/datasets/user-guide.md#delete-a-dataset) 以取得更多資訊。 |

若要進一步了解Identity Service，請閱讀 [Identity服務概述](../../identity-service/home.md).

## 查詢服務 {#query-service}

查詢服務可讓您使用標準SQL在Adobe Experience Platform中查詢資料 [!DNL Data Lake]. 您可以從 [!DNL Data Lake] 並將查詢結果擷取為新資料集，以用於報表、Data Science Workspace或擷取至「即時客戶個人檔案」。

**更新功能**

| 功能 | 說明 |
| --- | --- |
| 警報訂閱API | Adobe Experience Platform Query Service可讓您訂閱臨機和排程查詢的警報。 您可以在Platform UI內透過電子郵件、或兩者，接收警報。 目前，查詢警報只能使用 [查詢服務API](https://developer.adobe.com/experience-platform-apis/references/query-service/). |
| 資料集範例 | 查詢服務資料集範例可讓您對大資料執行探索式查詢，大幅縮短處理時間，並降低查詢準確度。 請參閱 [資料集範例指南](../../query-service/essential-concepts/dataset-samples.md) 了解更多。 |

如需 [!DNL Query Service]，請參閱 [[!DNL Query Service] 概述](../../query-service/home.md).

請參閱 [查詢警報檔案](../../query-service/api/alert-subscriptions.md) 了解更多。

## 來源 {#sources}

Adobe Experience Platform可內嵌來自外部來源的資料，同時允許您使用Platform服務來建構、加標籤及增強該資料。 您可以內嵌來自各種來源的資料，例如Adobe應用程式、雲端儲存、協力廠商軟體和您的CRM系統。

Experience Platform提供RESTful API和互動式UI，讓您輕鬆為各種資料提供者設定來源連線。 這些源連接允許您驗證並連接到外部儲存系統和CRM服務、設定獲取運行時間以及管理資料獲取吞吐量。

**更新功能**

| 功能 | 說明 |
| --- | --- |
| Audience Manager區段母體對即時客戶設定檔的影響 | 首次使用Audience Manager來源將Audience Manager區段傳送至Platform時，擷取大量Audience Manager區段母體會直接影響您的設定檔總數。 這表示選取所有區段可能會導致設定檔計數超過您的授權使用權限。 如需詳細資訊，請閱讀 [Audience Manager來源概觀](../../sources/connectors/adobe-applications/audience-manager.md). 如需您使用授權的詳細資訊，請參閱 [使用授權使用控制面板](../../dashboards/guides/license-usage.md). |
| 支援Adobe Campaign管理Cloud Service | 使用Adobe Campaign受管Cloud Service來源將Adobe Campaign v8.4的傳送和追蹤記錄檔資料Experience Platform。 閱讀指南 [在UI中建立Adobe Campaign托管Cloud Service來源連線](../../sources/tutorials/ui/create/adobe-applications/campaign.md) 以取得更多資訊。 |
| 批次來源的隨需內嵌API支援 | 使用按需獲取功能為具有的指定資料流建立臨時流運行 [!DNL Flow Service] API。 已建立的流量執行必須設為一次性擷取。 如需詳細資訊，請參閱 [使用API建立流程以執行隨選擷取](../../sources/tutorials/api/on-demand-ingestion.md) 以取得更多資訊。 |
| 為批源重試失敗的資料流運行提供API支援 | 使用 `re-trigger` 操作，通過API重試失敗的資料流。 閱讀指南 [使用API重試失敗的資料流運行](../../sources/tutorials/api/retry-flows.md) 以取得更多資訊。 |
| API支援篩選 [!DNL Google BigQuery] 和 [!DNL Snowflake] 來源 | 使用邏輯和比較運算子來篩選 [!DNL Google BigQuery] 和 [!DNL Snowflake] 來源。 閱讀指南 [使用API篩選來源的資料](../../sources/tutorials/api/filter.md) 以取得更多資訊。 |

若要進一步了解來源，請閱讀 [來源概觀](../../sources/home.md).
