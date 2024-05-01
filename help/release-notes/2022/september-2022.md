---
title: Adobe Experience Platform發行說明2022年9月
description: Adobe Experience Platform 2022年9月版本注意事項。
exl-id: a7a4dcf8-2cf3-4e39-879d-bdfcbacb737a
source-git-commit: e0af1f0110ceb514a5b249c42a05bf780ea834c6
workflow-type: tm+mt
source-wordcount: '2762'
ht-degree: 23%

---

# Adobe Experience Platform 發行說明

**發行日期： 2022年9月28日**

Adobe Experience Platform中的新功能：

- [屬性型存取控制](#abac)

Adobe Experience Platform 現有功能的更新：

- [[!DNL Artificial Intelligence and Machine Learning Services]](#ai-and-ml-services)
- [稽核記錄](#audit-logs)
- [[!DNL Dashboards]](#dashboards)
- [資料集合](#data-collection)
- [目的地](#destinations)
- [體驗資料模式 (XDM)](#xdm)
- [身分識別服務](#identity-service)
- [查詢服務](#query-service)
- [來源](#sources)

## 屬性型存取控制 {#abac}

>[!IMPORTANT]
>
>以屬性為基礎的存取控制將從2022年10月開始啟用。 如果您想要成為率先採用者，請聯絡您的Adobe代表。

屬性型存取控制是 Adob&#x200B;&#x200B;e Experience Platform 的一項功能，此平台為注重隱私的品牌提供更大的靈活性來管理使用者存取。可以將結構描述欄位和分段等個別對象指派給使用者角色。此功能允許您授予或撤銷組織中特定平台使用者對個別物件的存取權限。

透過屬性型存取控制，組織的管理員可以控制使用者對所有平台工作流程和資源的存取權限，包括其中的敏感個人資料 (SPD)、個人身分資訊 (PII) 和其他自訂類型資料。管理員可以定義只能存取特定欄位以及這些欄位對應資料的使用者角色。

| 功能 | 說明 |
| --- | --- |
| 屬性型存取控制 | 以屬性為基礎的存取控制可讓您使用可定義組織或資料使用範圍的標籤，來標籤Experience Data Model (XDM)結構描述欄位和區段。 同時，管理員可以使用使用者和角色管理介面來定義涵蓋XDM結構描述欄位和區段的存取原則，以更好地管理使用者或使用者群組（內部、外部或第三方使用者）的存取許可權。 如需詳細資訊，請參閱 [屬性型存取控制概觀](../../access-control/abac/overview.md). |
| 權限 | 許可權是Experience Cloud的區域，管理員可以在其中定義使用者角色和存取原則，以管理產品應用程式內功能和物件的存取許可權。 透過許可權，您可以建立和管理角色、為這些角色指派所需的資源許可權，以及建立原則以運用標籤並定義哪些使用者角色有權存取特定Platform資源。 許可權也可讓您管理與特定角色相關聯的標籤、沙箱和使用者。 如需詳細資訊，請參閱 [許可權UI指南](../../access-control/abac/ui/browse.md). |

若要了解更多關於屬性型存取控制，請參閱[屬性型存取控制概觀](../../access-control/abac/overview.md)。關於屬性型存取控制工作流程的綜合指南，請閱讀[屬性型存取控制端對端指南](../../access-control/abac/end-to-end-guide.md)。

## [!DNL Artificial Intelligence/Machine Learning services] {#ai-and-ml-services}

AI/ML服務可讓行銷分析師和從業人員運用客戶體驗使用案例中人工智慧和機器學習的強大功能。 這可讓行銷分析人員使用業務層級設定，針對公司需求設定模型，而不需要資料科學的專業知識。

### Attribution AI

Attribution AI 可將點數歸因到促成轉換事件的接觸點。行銷人員可善用此工具，協助量化客戶歷程中各個獨立行銷接觸點對行銷的影響。

| 功能 | 說明 |
| --- | --- |
| 儲存草稿執行個體 | 此新功能可讓行銷分析人員將模型設定儲存為草稿執行個體，並繼續編輯直到完成才可進行訓練和評分。 此功能有用的情況包括：使用者在工作流程中有多個要定義的欄位，但由於時間限制而無法完成時。 另一個案例是一或多個資料集統計資料正在處理中，但尚未提供時。 閱讀 [Attribution AI使用手冊](../../intelligent-services/attribution-ai/user-guide.md#governance-policies) 以進一步瞭解。 |
| 治理政策 | 使用者透過設定工作流程提交以建立執行個體後，新的原則執行服務會檢查是否有任何資料使用的原則違規，並在彈出視窗中顯示詳細資訊。 它可確保資料作業和行銷動作符合Adobe Experience Platform上設定的資料使用原則。 |

如需Attribution AI的詳細資訊，請參閱 [Attribution AI概觀](../../intelligent-services/attribution-ai/overview.md). 如需資料治理原則的資訊，請參閱 [原則概觀](../../data-governance/policies/overview.md).

### Customer AI

Real-time Customer Data Platform中可用的Customer AI可產生自訂傾向分數，例如大規模個別設定檔的流失和轉換情形。

| 功能 | 說明 |
| --- | --- |
| 儲存草稿執行個體 | 此新功能可讓行銷分析人員將模型設定儲存為草稿執行個體，並繼續編輯直到完成才可進行訓練和評分。 此功能有用的情況包括：使用者在工作流程中有多個要定義的欄位，但由於時間限制而無法完成時。 另一個案例是一或多個資料集統計資料正在處理中，但尚未提供時。 閱讀 [Customer AI使用手冊](../../intelligent-services/customer-ai/user-guide/configure.md#governance-policies) 以進一步瞭解。 |
| 治理政策 | 使用者透過設定工作流程提交以建立執行個體後，新的原則執行服務會檢查是否有任何資料使用的原則違規，並在彈出視窗中顯示詳細資訊。 它可確保資料作業和行銷動作符合Adobe Experience Platform上設定的資料使用原則。 |

如需Customer AI的詳細資訊，請參閱 [Customer AI概述](../../intelligent-services/customer-ai/overview.md). 如需資料治理原則的資訊，請參閱 [原則概觀](../../data-governance/policies/overview.md).

## 稽核記錄 {#audit-logs}

Experience Platform可讓您稽核各種服務和功能的使用者活動。 稽核記錄會提供有關何時何地執行哪些操作的資訊。

**更新的功能**

| 功能 | 名稱 | 說明 |
| --- | --- | --- |
| 已新增資源 | <ul><li>Attribution AI執行個體</li><li>Customer AI執行個體</li><li>資料流</li></ul> | 活動發生時，會自動記錄稽核記錄資源。 如果已啟用此功能，您就不需要手動啟用記錄收集。 |

{style="table-layout:auto"}

如需Platform中稽核記錄所追蹤之不同資源特定事件型別的詳細資訊，請參閱 [稽核記錄概觀](../../landing/governance-privacy-security/audit-logs/overview.md).

## [!DNL Dashboards] {#dashboards}

Adobe Experience Platform 提供了多個儀表板，您可以透過這些儀表板檢視每日快照期間擷取的有關組織資料的重要分析。

| 功能 | 說明 |
| --- | --- |
| 使用中標籤 | 在Widget資料庫中檢視時，使用中標籤可輕鬆識別控制面板中是否存在現有Widget。 這可讓您輕鬆避免重複，不過您仍可依需要多次新增相同的Widget。 |
| 使用者定義的儀表板 | 使用者定義儀表板可讓您建置和管理自訂儀表板，有助於加速深入分析和自訂視覺效果。 透過使用者定義儀表板，您可以建立、新增和編輯客製化Widget，以視覺化方式呈現與貴組織相關的關鍵量度。 閱讀 [功能指南](../../dashboards/user-defined-dashboards.md) 以進一步瞭解。 |
| 客戶資料平台見解資料模型 | 客戶資料平台(CDP)見解資料模型功能會公開為各種設定檔、目的地和分段Widget提供見解的資料模型和SQL。 您可以自訂這些SQL查詢範本，為您的行銷和關鍵績效指標使用案例建立CDP報表。 這些深入分析接著可作為自訂Widget用於您使用者定義的儀表板。 閱讀 [CDP Insights資料模型功能指南](../../dashboards/data-models/cdp-insights-data-model-b2c.md) 以進一步瞭解。 |
| 對象重疊報表Widget | 此Widget同時適用於兩者 [!UICONTROL 設定檔] 和 [!UICONTROL 區段] 控制面板。 報表提供您所選區段按最高或最低重疊百分比排名的有序對象清單。 從 [!UICONTROL 設定檔] 控制面板您可以透過所有可用區段的合併原則，篩選及檢視對象重疊。 此 [!UICONTROL 區段] 控制面板可讓您依特定區段篩選對象重疊。<br>使用此分析來建立新的、高效能區段，並避免將相同的對象傳送到不同的目的地。 報表也有助於識別隱藏的深入分析，以改進細分或找出要追求的不重複設定檔。 閱讀個別 [設定檔](../../dashboards/guides/profiles.md#audience-overlap-report) 和 [區段](../../dashboards/guides/audiences.md#audience-overlap-report) Widget指南以進一步瞭解。 |

如需詳細資訊，請參閱 [!DNL Dashboards]，請參閱 [[!DNL Dashboards] 概述](../../dashboards/home.md).

## 資料收集 {#data-collection}

Adobe Experience Platform 提供了一套技術，讓您可收集用戶端客戶體驗資料並將其傳送到 Adobe Experience Platform Edge Network，在其中可擴充、轉換資料並將其分送至 Adobe 或非 Adobe 目的地。

**新功能或更新功能**

| 功能 | 說明 |
| --- | --- |
| 平台UI中的左側導覽整合 | 先前專屬資料收集UI的所有功能（包括標籤、事件轉送和資料串流）現在也可透過Experience Platform左側導覽的類別下使用 **[!UICONTROL 資料彙集]**. 如此一來，在Platform中使用資料收集功能時，就不需要在UI之間切換。 |
| 標籤和事件轉送中的使用者歸因 | 清單可用時 [!UICONTROL 屬性] 在標籤和事件轉送中，每個列出的屬性現在會顯示其上次更新時間，以及進行更新的使用者。 |
| [[!DNL Snap Conversions API] 副檔名](https://exchange.adobe.com/apps/ec/108550) 用於事件轉送 | 您現在可以將資料傳送至 [!DNL Snapchat Conversions API] 使用 [事件轉送](../../tags/ui/event-forwarding/overview.md) 副檔名。 有關如何驗證和使用API的詳細資訊，請參閱 [[!DNL Snapchat Marketing API] 檔案](https://marketingapi.snapchat.com/docs/conversion.html). |
| [Web SDK中的使用者代理使用者端提示](/help/web-sdk/use-cases/client-hints.md) | Web SDK現在支援 [使用者代理使用者端提示](https://developer.chrome.com/docs/privacy-sandbox/user-agent/). 使用者端提示可讓網站擁有者存取許多與 [!DNL User-Agent] 字串，但採用更能保護隱私的方式來進行。 |
| [Web SDK逐頁移轉](../../web-sdk/home.md#migrating-to-web-sdk) | 您現在可以從其他Experience Cloud程式庫移轉現有的Web屬性，例如 [!DNL at.js]，一次一個頁面。 如此可分階段移轉Web SDK，而不需一次移轉所有頁面。 |
| [[!DNL Adobe Journey Optimizer] 支援資料串流](../../datastreams/overview.md#aep) | 適用於資料串流的Adobe Experience Platform服務現在支援 [!DNL Adobe Journey Optimizer]. 此選項可讓您在中使用網頁和應用程式型傳入頻道 [!DNL Adobe Journey Optimizer]. |

{style="table-layout:auto"}

如需Platform資料收集的詳細資訊，請參閱 [資料收集概觀](../../collection/home.md).

## [!DNL Destinations] {#destinations}

[!DNL Destinations] 是預先建立的和目標平台的整合，可讓來自 Adobe Experience Platform 的資料順暢啟動。您可使用目的地啟用已知和未知的資料，以進行跨通路行銷活動、電子郵件行銷活動、設定目標的廣告活動和其他諸多使用案例。

**新功能或更新功能**

| 功能 | 說明 |
| ----------- | ----------- |
| Destination SDK | Destination SDK現在為建立批次（或檔案式）生產或私有目的地的合作夥伴和客戶提供完整支援。 如需詳細資訊，請參閱下列檔案頁面： <ul><li>[Destination SDK概觀](../../destinations/destination-sdk/overview.md)</li><li>[設定以檔案為基礎的目的地](../../destinations/destination-sdk/guides/configure-file-based-destination-instructions.md)</li><li>[設定檔案型目的地的檔案格式選項](../../destinations/destination-sdk/guides/batch/configure-file-formatting-options.md)</li><li>[測試以檔案為基礎的目的地](../../destinations/destination-sdk/testing-api/batch-destinations/file-based-destination-testing-overview.md)</li></ul> |

{style="table-layout:auto"}

**新的或更新目的地**

| 目的地 | 說明 |
| ----------- | ----------- |
| [[!DNL Adobe Campaign Managed Cloud Services]](../../destinations/catalog/email-marketing/adobe-campaign-managed-services.md) | Adobe Campaign Managed Cloud Services為跨頻道客戶體驗設計提供平台，並為視覺行銷活動的策劃、即時互動管理和跨頻道執行提供環境。 [開始使用行銷活動](https://experienceleague.adobe.com/docs/campaign/campaign-v8/start/get-started.html). 請注意，這項整合可搭配使用 [Adobe Campaign 8.4或更高版本](https://experienceleague.adobe.com/docs/campaign/campaign-v8/new/release-notes.html#release-8-4-1). |
| [[!DNL Salesforce CRM]](../../destinations/catalog/crm/salesforce.md) | 此 [!DNL Salesforce CRM] 目的地已更新，可支援聯絡人和潛在客戶更新，以及效能改善，以更快進行更新。 |

{style="table-layout:auto"}

**新檔案或更新檔案**

| 文件 | 說明 |
| ----------- | ----------- |
| 目的地流量服務API檔案 | 此 [目的地API參考檔案](https://developer.adobe.com/experience-platform-apis/references/destinations/) 已更新，加入如何對檔案型目的地執行作業的指引。 稍後將新增串流目的地的作業。 |

如需有關目的地的詳細一般資訊，請參閱[目的地概觀](../../destinations/home.md)。

## 體驗資料模式 (XDM) {#xdm}

XDM 是一種開放原始碼的規格，可為帶到 Adobe Experience Platform 中的資料提供通用結構和定義 (結構描述)。若遵守 XDM 標準，即可將所有客戶體驗資料合併到一個常用表述中，以更快速、更整合的方式傳遞分析。您可以從客戶行為中獲得有價值的分析，透過區段定義客戶對象，並使用客戶屬性實現個人化的目的。

**新功能**

| 功能 | 說明 |
| --- | --- |
| UI支援列舉和建議值 | 除了啟用資料驗證的列舉之外，您現在還可以 [新增或移除建議值](../../xdm/ui/fields/enum.md) 用於標準或自訂字串欄位，好讓Platform使用者在建立區段時可以從中選擇好記的值清單。 |

**新的 XDM 元件**

| 元件類型 | 名稱 | 說明 |
| --- | --- | --- |
| 欄位群組 | [[!UICONTROL ajo分類欄位]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/decisioning/proposition-action.schema.json) | 與導致主張事件被觸發之特定元素的屬性。 |
| 欄位群組 | [[!UICONTROL MediaAnalytics 互動的詳細資料]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-media-analytics.schema.json) | 追蹤一段時間內的媒體互動。 |
| 欄位群組 | [[!UICONTROL 媒體細節資訊]](https://github.com/adobe/xdm/blob/master/components/datatypes/mediadetails.schema.json) | 追蹤媒體詳細資訊。 |
| 欄位群組 | [[!UICONTROL AdobeCJM ExperienceEvent — 表面]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/customerJourneyManagement/surfaces.schema.json) | 說明Adobe Journey Optimizer中體驗事件的介面。 |

{style="table-layout:auto"}

**已更新的 XDM 元件**

| 元件類型 | 名稱 | 說明 |
| --- | --- | --- |
| 行為 | [[!UICONTROL 時間序列]](https://github.com/adobe/xdm/blob/master/components/behaviors/time-series.schema.json) | <ul><li>已新增以下專案的值： `eventType`：<ul><li>`decisioning.propositionSend`</li><li>`decisioning.propositionDismiss`</li><li>`decisioning.propositionTrigger`</li><li>`media.downloaded`</li><li>`location.entry`</li><li>`location.exit`</li></ul></li><li>已移除下列專案的值： `eventType`：<ul><li>`decisioning.propositionDeliver`</li><li>`media.stateStart`</li><li>`media.stateEnd`</li></ul></li></ul> |
| 欄位群組 | (多個) | [已更新數個欄位說明](https://github.com/adobe/xdm/pull/1628/files) 橫跨Journey Orchestration元件。 |
| 欄位群組 | (多個) | [更新數個Adobe Workfront元件的標題](https://github.com/adobe/xdm/pull/1634/files) 以維持一致性。 |
| 欄位群組 | [[!UICONTROL ajo分類欄位]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/decisioning/proposition-event-type.schema.json) | 將數個欄位的名稱空間更新為 `xdm`. |
| 欄位群組 | [[!UICONTROL Journey Orchestration步驟事件常見欄位]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/journeyOrchestration/stepEvents/journeyStepEventCommonFieldsMixin.schema.json) | 新增欄位， `isReadSegmentTriggerStartEvent`. |
| 欄位群組 | [[!UICONTROL 預測氣象]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/shared/forecasted-weather.schema.json) | 已變更 `xdm:uvIndex` 欄位新增為整數型別，並將 `xdm` 名稱空間至缺少的多個欄位。 |
| 欄位群組 | [[!UICONTROL 媒體細節資訊]](https://github.com/adobe/xdm/blob/master/components/datatypes/mediadetails.schema.json) | `xdm:endUserIDs` 和 `xdm:implementationDetails` 已從欄位群組中移除。 |
| 資料類型 | (多個) | [更新數個媒體屬性名稱](https://github.com/adobe/xdm/pull/1626/files) 數種資料型別之間的一致性。 |
| 資料類型 | [[!UICONTROL 實作詳細資料]](https://github.com/adobe/xdm/blob/master/components/datatypes/industry-verticals/implementationdetails.schema.json) | 新增顫振的已知名稱。 |
| 資料類型 | [[!UICONTROL 興趣點細節]](https://github.com/adobe/xdm/blob/master/components/datatypes/poi-detail.schema.json) | 資料型別現在可以接受與地標關聯的中繼資料索引鍵/值組清單。 |
| 資料類型 | [[!UICONTROL 主張動作]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/decisioning/proposition-action.schema.json) | [!DNL AJO Classification Fields] 已重新命名為 [!UICONTROL 主張動作]. |
| 資料類型 | [[!UICONTROL 主張事件型別]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/decisioning/proposition-event-type.schema.json) | [!DNL AJO Classification Fields] 已重新命名為 [!UICONTROL 主張動作]. |
| (多個) | (多個) | 實驗性屬性已被 [已在所有B2B元件中穩定](https://github.com/adobe/xdm/pull/1617/files). |
| (多個) | (多個) | Adobe Journey Optimizer實體已 [已穩定](https://github.com/adobe/xdm/pull/1625/files). |
| (多個) | (多個) | 跨多個實驗元件的特定欄位名稱空間已 [已更新一致性](https://github.com/adobe/xdm/pull/1626/files). |

{style="table-layout:auto"}

如需有關 Platform 中 XDM 的詳細資訊，請參閱 [XDM 系統概觀](../../xdm/home.md)。

## 身分識別服務 {#identity-service}

提供相關的數位體驗需要完全瞭解您的客戶。 當您的客戶資料分散於不同的系統時，這會使工作變得更困難，導致每個客戶似乎都有多個「身分」。

Adobe Experience Platform Identity Service可跨裝置和系統橋接身分，讓您即時提供具影響力的個人數位體驗，協助您更清楚瞭解客戶及其行為。

**更新的功能**

| 功能 | 說明 |
| --- | --- |
| 支援資料集刪除 | 透過提出請求時，Identity Service現在支援資料集刪除 [目錄服務API](https://developer.adobe.com/experience-platform-apis/references/catalog/)、UI或資料衛生。 閱讀指南： [刪除UI中的資料集](../../catalog/datasets/user-guide.md#delete-a-dataset) 以取得詳細資訊。 |

若要進一步瞭解Identity Service，請閱讀 [Identity Service總覽](../../identity-service/home.md).

## 查詢服務 {#query-service}

查詢服務可讓您使用標準的 SQL 查詢 Adobe Experience Platform 中的資料[!DNL Data Lake]。您可以從以下位置加入任何資料集： [!DNL Data Lake] 並將查詢結果擷取為新資料集，以用於報表、資料科學工作區或內嵌到即時客戶個人檔案中。

**更新的功能**

| 功能 | 說明 |
| --- | --- |
| 警示訂閱API | Adobe Experience Platform查詢服務可讓您針對臨時和已排程的查詢訂閱警報。 警報可透過電子郵件、Platform UI內或兩者來接收。 目前，查詢警報只能使用 [查詢服務API](https://developer.adobe.com/experience-platform-apis/references/query-service/). |
| 資料集範例 | 查詢服務資料集範例可讓您對巨量資料執行探索性查詢，大幅縮短處理時間，但代價是查詢準確性。 請參閱 [資料集範例指南](../../query-service/key-concepts/dataset-samples.md) 以進一步瞭解。 |

如需詳細資訊，請參閱 [!DNL Query Service]，請參閱 [[!DNL Query Service] 概述](../../query-service/home.md).

請參閱 [查詢警報檔案](../../query-service/api/alert-subscriptions.md) 以進一步瞭解。

## 來源 {#sources}

Adobe Experience Platform可內嵌來自外部來源的資料，同時允許您使用Platform服務來建構、加標籤及增強這些資料。 您可以從各種來源擷取資料，例如 Adob&#x200B;&#x200B;e 應用程式、雲端型儲存空間、協力廠商軟體和 CRM 系統。

Experience Platform 可提供 RESTful API 和互動式 UI，可讓您輕鬆為各種資料提供者設定來源連線。這些來源連線可讓您進行驗證並連線到外部儲存系統和 CRM 服務、設定擷取執行的時間並管理資料擷取輸送量。

**更新的功能**

| 功能 | 說明 |
| --- | --- |
| Audience Manager區段母體對即時客戶個人檔案的影響 | 當您使用Audience Manager來源首次將Audience Manager區段傳送至Platform時，大量的Audience Manager區段母體的擷取會直接影響您的總設定檔計數。 這表示選取所有區段可能會導致設定檔計數超過您的授權使用權益。 如需詳細資訊，請閱讀 [Audience Manager來源概觀](../../sources/connectors/adobe-applications/audience-manager.md). 如需授權使用方式的詳細資訊，請參閱以下檔案： [使用授權使用情況儀表板](../../dashboards/guides/license-usage.md). |
| 支援Adobe Campaign ManagedCloud Service | 使用Adobe Campaign託管Cloud Service來源，將您的Adobe Campaign v8.4傳遞和追蹤記錄資料帶入Experience Platform。 閱讀指南： [在UI中建立Adobe Campaign ManagedCloud Service來源連線](../../sources/tutorials/ui/create/adobe-applications/campaign.md) 以取得詳細資訊。 |
| 批次來源的隨選擷取的API支援 | 使用隨選擷取為具有的指定資料流建立臨機操作流程執行 [!DNL Flow Service] API。 建立的流程執行必須設定為一次性內嵌。 如需詳細資訊，請閱讀以下指南： [使用API建立隨選擷取的流程執行](../../sources/tutorials/api/on-demand-ingestion.md) 以取得詳細資訊。 |
| API支援重試批次來源的失敗資料流執行 | 使用 `re-trigger` 操作，透過API重試失敗的資料流。 閱讀指南： [使用API重試失敗的資料流執行](../../sources/tutorials/api/retry-flows.md) 以取得詳細資訊。 |
| API支援篩選的列層級資料 [!DNL Google BigQuery] 和 [!DNL Snowflake] 來源 | 使用邏輯和比較運運算元來篩選的列層級資料 [!DNL Google BigQuery] 和 [!DNL Snowflake] 來源。 如需詳細資訊，請至「[使用 API 篩選來源的資料](../../sources/tutorials/api/filter.md)」詳閱指南。 |

若要了解有關來源的詳細資訊，請閱讀[來源概觀](../../sources/home.md)。
