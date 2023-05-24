---
title: Adobe Experience Platform發行說明2022年9月
description: 2022年9月為Adobe Experience Platform發佈的說明。
exl-id: a7a4dcf8-2cf3-4e39-879d-bdfcbacb737a
source-git-commit: 8904d44cc8d289d103ec6d65116b8385ed615c4d
workflow-type: tm+mt
source-wordcount: '2940'
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
- [體驗資料模型(XDM)](#xdm)
- [身份識別服務](#identity-service)
- [查詢服務](#query-service)
- [來源](#sources)

## 以屬性為基礎的存取控制 {#abac}

>[!IMPORTANT]
>
>將從2022年10月開始啟用基於屬性的訪問控制。 如果您想成為早期收養者，請聯繫您的Adobe代表。

基於屬性的訪問控制是Adobe Experience Platform公司的一項功能，它為具有隱私意識的品牌提供了管理用戶訪問的更大靈活性。 可以將單個對象（如架構欄位和段）分配給用戶角色。 此功能允許您授予或撤消組織中特定平台用戶對單個對象的訪問權限。

通過基於屬性的訪問控制，您組織的管理員可以控制用戶對所有平台工作流和資源中敏感個人資料(SPD)、個人識別資訊(PII)和其他自定義類型資料的訪問。 管理員可以定義只能訪問特定欄位和與這些欄位對應的資料的用戶角色。

| 功能 | 說明 |
| --- | --- |
| 以屬性為基礎的存取控制 | 基於屬性的訪問控制允許您使用定義組織或資料使用範圍的標籤來標籤體驗資料模型(XDM)架構欄位和段。 同時，管理員可以使用用戶和角色管理介面來定義涵蓋XDM架構欄位和段的訪問策略，以更好地管理授予用戶或用戶組（內部、外部或第三方用戶）的訪問。 有關詳細資訊，請參見 [基於屬性的訪問控制概述](../../access-control/abac/overview.md)。 |
| 權限 | 權限是Experience Cloud區域，管理員可以在該區域定義用戶角色和訪問策略，以管理產品應用程式中功能和對象的訪問權限。 通過權限，您可以建立和管理角色，為這些角色分配所需的資源權限，並構建策略以利用標籤並定義哪些用戶角色有權訪問特定平台資源。 權限也可讓您管理與特定角色相關聯的標籤、沙箱和使用者。有關詳細資訊，請參見 [權限UI指南](../../access-control/abac/ui/browse.md)。 |

有關基於屬性的訪問控制的詳細資訊，請參閱 [基於屬性的訪問控制概述](../../access-control/abac/overview.md)。 有關基於屬性的訪問控制工作流的全面指南，請閱讀 [基於屬性的訪問控制端到端指南](../../access-control/abac/end-to-end-guide.md)。

## [!DNL Artificial Intelligence/Machine Learning services] {#ai-and-ml-services}

AI/ML服務使營銷分析員和從業人員能夠利用人工智慧和機器學習在客戶體驗使用案例中的力量。 這使市場營銷分析員能夠使用業務級配置來設定特定於公司需要的模型，而無需資料科學專業知識。

### Attribution AI

Attribution AI 可將點數歸因到促成轉換事件的接觸點。 行銷人員可善用此工具，協助量化客戶歷程中各個獨立行銷接觸點對行銷的影響。

| 功能 | 說明 |
| --- | --- |
| 保存草稿實例 | 此新功能使市場營銷分析員能夠將模型配置另存為草稿實例，並繼續編輯，直到在培訓和評分之前完成。 此功能有幫助的方案包括：當用戶在工作流中有多個要定義的欄位，但由於時間限制而無法完成該欄位。 另一種情況是正在處理一個或多個資料集統計資訊但尚未提供。 閱讀 [Attribution AI使用手冊](../../intelligent-services/attribution-ai/user-guide.md#governance-policies) 來瞭解更多資訊。 |
| 治理政策 | 在用戶通過配置工作流提交以建立實例後，新策略實施服務將檢查是否存在任何違反資料使用情況的策略，並以跨距顯示詳細資訊。 它確保資料操作和營銷操作符合Adobe Experience Platform上配置的資料使用策略。 |

有關Attribution AI的詳細資訊， [Attribution AI概述](../../intelligent-services/attribution-ai/overview.md)。 有關資料治理策略的資訊，請閱讀 [策略概述](../../data-governance/policies/overview.md)。

### 客戶AI

在Real-time Customer Data Platform提供的客戶AI用於生成定制傾向得分，如按比例對單個配置檔案進行流失和轉換。

| 功能 | 說明 |
| --- | --- |
| 保存草稿實例 | 此新功能使市場營銷分析員能夠將模型配置另存為草稿實例，並繼續編輯，直到在培訓和評分之前完成。 此功能有幫助的方案包括：當用戶在工作流中有多個要定義的欄位，但由於時間限制而無法完成該欄位。 另一種情況是正在處理一個或多個資料集統計資訊但尚未提供。 閱讀 [客戶AI使用手冊](../../intelligent-services/customer-ai/user-guide/configure.md#governance-policies) 來瞭解更多資訊。 |
| 治理政策 | 在用戶通過配置工作流提交以建立實例後，新策略實施服務將檢查是否存在任何違反資料使用情況的策略，並以跨距顯示詳細資訊。 它確保資料操作和營銷操作符合Adobe Experience Platform上配置的資料使用策略。 |

有關客戶AI的詳細資訊，請閱讀 [客戶AI概述](../../intelligent-services/customer-ai/overview.md)。 有關資料治理策略的資訊，請閱讀 [策略概述](../../data-governance/policies/overview.md)。

## 稽核記錄 {#audit-logs}

Experience Platform允許您審計用戶活動中的各種服務和功能。 審計日誌提供了有關誰執行了什麼和何時執行的資訊。

**已更新功能**

| 功能 | 名稱 | 說明 |
| --- | --- | --- |
| 已添加資源 | <ul><li>Attribution AI實例</li><li>客戶AI實例</li><li>資料流</li></ul> | 在活動發生時自動記錄審核日誌資源。 如果啟用了該功能，則無需手動啟用日誌收集。 |

{style="table-layout:auto"}

有關平台中審核日誌跟蹤的不同特定於資源的事件類型的詳細資訊，請參閱 [審核日誌概述](../../landing/governance-privacy-security/audit-logs/overview.md)。

## [!DNL Dashboards] {#dashboards}

Adobe Experience Platform提供了多個儀表板，您可以通過這些儀表板查看有關組織資料的重要見解，如在每日快照中捕獲的。

| 功能 | 說明 |
| --- | --- |
| 使用中標籤 | 在小部件庫中查看時，使用中標籤可輕鬆標識儀表板中現有小部件的存在。 這樣，您就可以輕鬆避免重複，儘管您仍可以多次添加同一小部件（如果需要）。 |
| 用戶定義的儀表板 | 用戶定義的儀表板通過使您能夠構建和管理自定義儀表板來幫助加速洞察和自定義可視化。 使用用戶定義的儀表板，您可以建立、添加和編輯定制小部件，以可視化與您的組織相關的關鍵度量。 閱讀 [特徵指南](../../dashboards/user-defined-dashboards.md) 來瞭解更多資訊。 |
| 客戶資料平台洞察資料模型 | 客戶資料平台(CDP)Insights資料模型功能公開了資料模型和SQL，這些模型和SQL為各種配置檔案、目標和分段小部件提供了見解。 您可以定制這些SQL查詢模板，以便為您的市場營銷和關鍵績效指標使用案例建立CDP報告。 然後，這些見解可以用作用戶定義的儀表板的自定義小部件。 閱讀 [《 CDP Insights資料模型功能指南》](../../dashboards/cdp-insights-data-model.md) 來瞭解更多資訊。 |
| 受眾重疊報表構件 | 此小部件可用於兩者 [!UICONTROL 配置檔案] 和 [!UICONTROL 段] 儀表板。 此報表提供按所選段的最高或最低重疊百分比排序的受眾的有序清單。 從 [!UICONTROL 配置檔案] 儀表板可通過合併策略從所有可用段中篩選和查看受眾重疊。 的 [!UICONTROL 段] 儀表板允許您按特定段過濾受眾重疊。<br>使用此分析可構建新的高效能網段，並避免將相同的受眾發送到不同的目標。 該報告還有助於識別隱藏的洞察力，以改進細分或找到要追蹤的獨特配置檔案。 閱讀相應 [配置檔案](../../dashboards/guides/profiles.md#audience-overlap-report) 和 [段](../../dashboards/guides/segments.md#audience-overlap-report) 小部件參考線以瞭解更多資訊。 |

有關 [!DNL Dashboards]，請參閱 [[!DNL Dashboards] 概述](../../dashboards/home.md)。

## 資料收集 {#data-collection}

Adobe Experience Platform公司提供了一套技術，使您能夠收集客戶端客戶體驗資料並將其發送到Adobe Experience Platform邊緣網路，在該網路中，資料可以得到豐富、轉換並分發到Adobe或非Adobe目的地。

**新增或更新的功能**

| 功能 | 說明 |
| --- | --- |
| 平台UI中的左導航整合 | 以前只有資料收集UI（包括標籤、事件轉發和資料流）的所有功能現在也可通過Experience Platform中的左導航（位於類別下）獲得 **[!UICONTROL 資料收集]**。 這樣，在平台中使用資料收集功能時，無需在UI之間切換。 |
| 標籤和事件轉發中的用戶屬性 | 清單可用時 [!UICONTROL 屬性] 在標籤和事件轉發中，每個列出的屬性現在都顯示上次更新的時間以及更新的用戶。 |
| [[!DNL Snap Conversions API] 擴展](https://exchange.adobe.com/apps/ec/108550) 用於事件轉發 | 您現在可以將資料發送到 [!DNL Snapchat Conversions API] 使用 [事件轉發](../../tags/ui/event-forwarding/overview.md) 擴展。 有關如何驗證和使用API的詳細資訊，請參閱 [[!DNL Snapchat Marketing API] 文檔](https://marketingapi.snapchat.com/docs/conversion.html)。 |
| [[!DNL User-Agent Client Hints] 在Web SDK中](../../edge/fundamentals/user-agent-client-hints.md) | Web SDK現在支援 [[!DNL User-Agent Client Hints]](https://developer.chrome.com/docs/privacy-sandbox/user-agent/)。 客戶端提示允許網站所有者訪問中提供的大部分相同資訊 [!DNL User-Agent] 串，但更能保護隱私。 |
| [Web SDK逐頁遷移](../../edge/home.md#migrating-to-web-sdk) | 現在，您可以從其他Experience Cloud庫遷移現有Web屬性，如 [!DNL at.js]，到Web SDK，一次一頁。 這支援分階段遷移Web SDK的方法，而無需同時遷移所有頁面。 |
| [[!DNL Adobe Journey Optimizer] 支援資料流](../../edge/datastreams/overview.md#aep) | 資料流的Adobe Experience Platform服務現在支援 [!DNL Adobe Journey Optimizer]。 此選項允許您在中使用基於Web和應用的入站通道 [!DNL Adobe Journey Optimizer]。 |

{style="table-layout:auto"}

有關平台中資料收集的詳細資訊，請參閱 [資料收集概述](../../collection/home.md)。

## [!DNL Destinations] {#destinations}

[!DNL Destinations] 是預先構建的與目標平台的整合，允許無縫激活來自Adobe Experience Platform的資料。 您可以使用目標來激活跨渠道市場營銷活動、電子郵件活動、目標廣告和許多其他使用案例的已知和未知資料。

**新增或更新的功能**

| 功能 | 說明 |
| ----------- | ----------- |
| 目標 SDK | Destination SDK現在為合作夥伴和客戶提供全面支援，以建立批（或基於檔案）的產品化或私有目標。 有關詳細資訊，請閱讀以下文檔頁： <ul><li>[Destination SDK概述](../../destinations/destination-sdk/overview.md)</li><li>[配置基於檔案的目標](../../destinations/destination-sdk/guides/configure-file-based-destination-instructions.md)</li><li>[為基於檔案的目標配置檔案格式選項](../../destinations/destination-sdk/guides/batch/configure-file-formatting-options.md)</li><li>[Test基於檔案的目標](../../destinations/destination-sdk/testing-api/batch-destinations/file-based-destination-testing-overview.md)</li></ul> |

{style="table-layout:auto"}

**新建或更新的目標**

| 目的地 | 說明 |
| ----------- | ----------- |
| [[!DNL Adobe Campaign Managed Cloud Services]](../../destinations/catalog/email-marketing/adobe-campaign-managed-services.md) | Adobe Campaign Managed Cloud Services公司為設計跨渠道客戶體驗提供了一個平台，並為視覺營銷協調，即時交互管理和跨渠道執行提供了一個環境。 [市場活動入門](https://experienceleague.adobe.com/docs/campaign/campaign-v8/start/get-started.html)。 請注意，此整合適用於 [Adobe Campaign版本8.4或更高版本](https://experienceleague.adobe.com/docs/campaign/campaign-v8/new/release-notes.html?lang=en#release-8-4-1)。 |
| [[!DNL Salesforce CRM]](../../destinations/catalog/crm/salesforce.md) | 的 [!DNL Salesforce CRM] 目標已更新，以支援聯繫人和線索更新，以及效能改進，以加快更新。 |

{style="table-layout:auto"}

**新建或更新的文檔**

| 文件 | 說明 |
| ----------- | ----------- |
| 目標流服務API文檔 | 的 [目標API參考文檔](https://developer.adobe.com/experience-platform-apis/references/destinations/) 已更新，以包括有關如何在基於檔案的目標上執行操作的指導。 稍後將添加流目標的操作。 |

有關目標的更多一般資訊，請參閱 [目標概述](../../destinations/home.md)。

## 體驗資料模型(XDM) {#xdm}

XDM是一種開源規範，它為傳入Adobe Experience Platform的資料提供通用結構和定義（架構）。 通過遵守XDM標準，所有客戶體驗資料都可以納入到共同的表示形式中，以更快、更整合的方式提供見解。 您可以從客戶操作中獲得有價值的見解，通過細分市場定義客戶受眾，並將客戶屬性用於個性化目的。

**新功能**

| 功能 | 說明 |
| --- | --- |
| 對枚舉和建議值的UI支援 | 除了啟用資料驗證的枚舉外，您現在還可以 [添加或刪除建議值](../../xdm/ui/fields/enum.md) 用於標準或自定義字串欄位，以便平台用戶在建立段時具有要從中選擇的友好值清單。 |

**新的XDM元件**

| 元件類型 | 名稱 | 說明 |
| --- | --- | --- |
| 欄位群組 | [[!UICONTROL AJO分類欄位]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/decisioning/proposition-action.schema.json) | 與之交互的特定元素的屬性導致觸發命題事件。 |
| 欄位群組 | [[!UICONTROL MediaAnalytics交互詳細資訊]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-media-analytics.schema.json) | 跟蹤媒體交互的時間。 |
| 欄位群組 | [[!UICONTROL 介質詳細資訊]](https://github.com/adobe/xdm/blob/master/components/datatypes/mediadetails.schema.json) | 跟蹤介質詳細資訊。 |
| 欄位群組 | [[!UICONTROL AdobeCJM ExperienceEvent — 曲面]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/customerJourneyManagement/surfaces.schema.json) | 描述Adobe Journey Optimizer中「體驗事件」的曲面。 |

{style="table-layout:auto"}

**更新的XDM元件**

| 元件類型 | 名稱 | 說明 |
| --- | --- | --- |
| 行為 | [[!UICONTROL 時間序列]](https://github.com/adobe/xdm/blob/master/components/behaviors/time-series.schema.json) | <ul><li>已為 `eventType`:<ul><li>`decisioning.propositionSend`</li><li>`decisioning.propositionDismiss`</li><li>`decisioning.propositionTrigger`</li><li>`media.downloaded`</li><li>`location.entry`</li><li>`location.exit`</li></ul></li><li>已刪除的值 `eventType`:<ul><li>`decisioning.propositionDeliver`</li><li>`media.stateStart`</li><li>`media.stateEnd`</li></ul></li></ul> |
| 欄位群組 | （多個） | [已更新多個欄位說明](https://github.com/adobe/xdm/pull/1628/files) Journey Orchestration元件。 |
| 欄位群組 | （多個） | [更新了幾個Adobe Workfront部分的標題](https://github.com/adobe/xdm/pull/1634/files) 一致性。 |
| 欄位群組 | [[!UICONTROL AJO分類欄位]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/decisioning/proposition-event-type.schema.json) | 已將多個欄位的命名空間更新為 `xdm`。 |
| 欄位群組 | [[!UICONTROL Journey Orchestration步驟事件公用欄位]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/journeyOrchestration/stepEvents/journeyStepEventCommonFieldsMixin.schema.json) | 添加了一個新欄位， `isReadSegmentTriggerStartEvent`。 |
| 欄位群組 | [[!UICONTROL 預測天氣]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/shared/forecasted-weather.schema.json) | 已更改 `xdm:uvIndex` 將欄位添加到整數類型，並添加 `xdm` 命名空間到缺少的幾個欄位。 |
| 欄位群組 | [[!UICONTROL 介質詳細資訊]](https://github.com/adobe/xdm/blob/master/components/datatypes/mediadetails.schema.json) | `xdm:endUserIDs` 和 `xdm:implementationDetails` 已從欄位組中刪除。 |
| 資料類型 | （多個） | [已更新多個媒體屬性名稱](https://github.com/adobe/xdm/pull/1626/files) 跨多個資料類型以實現一致性。 |
| 資料類型 | [[!UICONTROL 實施詳細資訊]](https://github.com/adobe/xdm/blob/master/components/datatypes/industry-verticals/implementationdetails.schema.json) | 已添加已知的顫振名稱。 |
| 資料類型 | [[!UICONTROL 興趣點詳細資訊]](https://github.com/adobe/xdm/blob/master/components/datatypes/poi-detail.schema.json) | 資料類型現在可以接受與感興趣點相關聯的元資料鍵值對的清單。 |
| 資料類型 | [[!UICONTROL 提案操作]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/decisioning/proposition-action.schema.json) | [!DNL AJO Classification Fields] 已更名為 [!UICONTROL 提案操作]。 |
| 資料類型 | [[!UICONTROL 命題事件類型]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/decisioning/proposition-event-type.schema.json) | [!DNL AJO Classification Fields] 已更名為 [!UICONTROL 提案操作]。 |
| （多個） | （多個） | 實驗性質 [穩定於所有B2B元件](https://github.com/adobe/xdm/pull/1617/files)。 |
| （多個） | （多個） | Adobe Journey Optimizer實體 [穩定](https://github.com/adobe/xdm/pull/1625/files)。 |
| （多個） | （多個） | 幾個實驗元件中某些欄位的命名空間 [已更新一致性](https://github.com/adobe/xdm/pull/1626/files)。 |

{style="table-layout:auto"}

有關平台中XDM的詳細資訊，請參見 [XDM系統概述](../../xdm/home.md)。

## 身份識別服務 {#identity-service}

提供相關數字型驗需要全面瞭解您的客戶。 當您的客戶資料分散在不同的系統中，導致每個客戶都顯得具有多個「身份」時，這就變得更加困難了。

Adobe Experience Platform身份服務通過跨設備和系統橋接身份，幫助您更好地瞭解客戶及其行為，讓您能夠即時提供有影響的個人數字型驗。

**已更新功能**

| 功能 | 說明 |
| --- | --- |
| 支援資料集刪除 | Identity Service現在支援在通過 [目錄服務API](https://developer.adobe.com/experience-platform-apis/references/catalog/)、UI或資料衛生。 閱讀上的指南 [刪除UI中的資料集](../../catalog/datasets/user-guide.md#delete-a-dataset) 的子菜單。 |

要瞭解有關Identity Service的詳細資訊，請閱讀 [Identity Service概述](../../identity-service/home.md)。

## 查詢服務 {#query-service}

查詢服務允許您使用標準SQL查詢Adobe Experience Platform的資料 [!DNL Data Lake]。 您可以加入來自 [!DNL Data Lake] 並將查詢結果捕獲為新資料集，用於報告、Data Science Workspace或用於接收到即時客戶配置檔案。

**已更新功能**

| 功能 | 說明 |
| --- | --- |
| 警報訂閱API | Adobe Experience Platform查詢服務允許您訂閱臨時查詢和計畫查詢的警報。 可以通過電子郵件、平台UI或兩者接收警報。 當前，查詢警報只能訂閱到 [查詢服務API](https://developer.adobe.com/experience-platform-apis/references/query-service/)。 |
| 資料集示例 | Query Service資料集示例使您能夠對大資料執行探索性查詢，同時大大減少了處理時間，並犧牲了查詢準確性。 查看 [資料集示例指南](../../query-service/essential-concepts/dataset-samples.md) 來瞭解更多資訊。 |

有關 [!DNL Query Service]，請參閱 [[!DNL Query Service] 概述](../../query-service/home.md)。

查看 [查詢警報文檔](../../query-service/api/alert-subscriptions.md) 來瞭解更多資訊。

## 來源 {#sources}

Adobe Experience Platform可以從外部源接收資料，同時允許您使用平台服務來構建、標籤和增強資料。 您可以從多種來源(如Adobe應用程式、基於雲的儲存、第三方軟體和您的CRM系統)接收資料。

Experience Platform提供REST風格的API和互動式UI，讓您能夠輕鬆地為各種資料提供程式設定源連接。 通過這些源連接，您可以驗證並連接到外部儲存系統和CRM服務，設定接收運行時間，並管理資料接收吞吐量。

**已更新功能**

| 功能 | 說明 |
| --- | --- |
| Audience Manager段人口對即時客戶配置檔案的影響 | 當您首次使用Audience Manager源將Audience Manager段發送到平台時，大量Audience Manager段的接收會直接影響您的總配置檔案計數。 這意味著選擇所有段可能會導致配置檔案計數超過許可證使用權限。 有關詳細資訊，請閱讀 [Audience Manager源概述](../../sources/connectors/adobe-applications/audience-manager.md)。 有關許可證使用情況的資訊，請閱讀 [使用許可證使用儀表板](../../dashboards/guides/license-usage.md)。 |
| 支援Adobe Campaign管理Cloud Service | 使用Adobe Campaign托管Cloud Service源將您的Adobe Campaignv8.4交付和跟蹤日誌資料帶到Experience Platform。 閱讀上的指南 [在UI中建立Adobe Campaign托管Cloud Service源連接](../../sources/tutorials/ui/create/adobe-applications/campaign.md) 的子菜單。 |
| 對批源的按需接收的API支援 | 使用按需接收為給定資料流建立專用流運行， [!DNL Flow Service] API。 建立的流運行必須設定為一次性接收。 有關詳細資訊，請閱讀上的指南 [使用API建立用於按需接收的流運行](../../sources/tutorials/api/on-demand-ingestion.md) 的子菜單。 |
| 對批處理源重試失敗資料流運行的API支援 | 使用 `re-trigger` 通過API重試失敗的資料流。 閱讀上的指南 [使用API重試失敗的資料流運行](../../sources/tutorials/api/retry-flows.md) 的子菜單。 |
| API支援篩選 [!DNL Google BigQuery] 和 [!DNL Snowflake] 來源 | 使用邏輯運算子和比較運算子篩選 [!DNL Google BigQuery] 和 [!DNL Snowflake] 源。 閱讀上的指南 [使用API篩選源的資料](../../sources/tutorials/api/filter.md) 的子菜單。 |

要瞭解有關源的詳細資訊，請閱讀 [源概述](../../sources/home.md)。
