---
title: Adobe Experience Platform發行說明2022年8月
description: 2022年8月Adobe Experience Platform發行說明。
exl-id: dbf1e7a3-8599-4991-8932-f57d3b1c640d
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '2131'
ht-degree: 7%

---

# Adobe Experience Platform 發行說明

**發行日期：2022 年 24 月 8 日**

Adobe Experience Platform 現有功能更新：

- [[!DNL Artificial Intelligence and Machine Learning Services]](#ai-and-ml-services)
- [[!DNL Dashboards]](#dashboards)
- [[!DNL Data Prep]](#data-prep)
- [[!DNL Destinations]](#destinations)
- [Experience Data Model(XDM)](#xdm)
- [即時客戶個人檔案](#profile)
- [細分服務](#segmentation)
- [來源](#sources)

## [!DNL Artificial Intelligence/Machine Learning services] {#ai-and-ml-services}

AI/ML服務讓行銷分析師和從業人員能夠在客戶體驗使用案例中運用人工智慧和機器學習的強大功能。 這可讓行銷分析人員使用業務層級設定，針對公司的需求設定特定的模型，而不需要資料科學的專業知識。

### Attribution AI

Attribution AI 可將點數歸因到促成轉換事件的接觸點。 行銷人員可善用此工具，協助量化客戶歷程中各個獨立行銷接觸點對行銷的影響。

**更新功能**

| 功能 | 說明 |
| ------- | ----------- |
| 隱私權支援 | <ul><li> Attribution AI現在支援定義使用者角色和存取原則，以管理 [權限](../../../help/access-control/abac/ui/permissions.md) 用於產品應用程式中的功能和對象。 </li><li>稽核記錄資源會在活動發生時自動記錄。</li><li> 通過 [基於屬性的訪問控制](../../access-control/abac/overview.md)，管理員可以根據特定屬性控制對特定對象和/或功能的訪問，這些屬性可以是添加到對象（如標籤）的元資料。管理員還可以定義只能訪問與這些欄位對應的特定欄位和資料的用戶角色。</li><li>Attribution AI可運用Platform資料集。 為支援品牌可能收到的消費者權利請求，品牌應使用PlatformPrivacy Service來提交消費者存取和刪除請求，以在資料湖、Identity Service和即時客戶設定檔中移除其資料。  </li><li>用於輸入/輸出模型的所有資料集都將遵循Platform准則。 平台資料加密適用於閒置和傳輸中的資料。 請參閱本檔案以深入了解 [資料加密](../../../help/landing/governance-privacy-security/encryption.md).</li></ul> |

{style=&quot;table-layout:auto&quot;}

**附註**:在進一步通知之前，現有Healthcare Shield客戶將無法使用Attribution AI。

如需Attribution AI的詳細資訊，請參閱 [Attribution AI](../../intelligent-services/attribution-ai/overview.md) 概述。

### Customer AI

Real-time Customer Data Platform提供的Customer AI可產生自訂傾向分數，例如大規模個別設定檔的流失和轉換。

**更新功能**

| 功能 | 說明 |
| ------- | ----------- |
| 隱私權支援 | <ul><li> Customer AI現在支援定義要管理的使用者角色和存取原則 [權限](../../../help/access-control/abac/ui/permissions.md) 用於產品應用程式中的功能和對象。 </li><li>稽核記錄資源會在活動發生時自動記錄。</li><li> 通過 [基於屬性的訪問控制](../../access-control/abac/overview.md)，管理員可以根據特定屬性控制對特定物件和/或功能的存取。 這些屬性可以是新增至物件的中繼資料，例如標籤。 管理員也可以定義只有特定欄位和與這些欄位對應的資料才能存取的使用者角色。</li><li>Customer AI運用Platform資料集。 為支援品牌可能收到的消費者權利請求，品牌應使用PlatformPrivacy Service來提交消費者存取和刪除請求，以在資料湖、Identity Service和即時客戶設定檔中移除其資料。 </li><li>用於輸入/輸出模型的所有資料集都將遵循Platform准則。 平台資料加密適用於閒置和傳輸中的資料。 請參閱本檔案以深入了解 [資料加密](../../../help/landing/governance-privacy-security/encryption.md).</li></ul> |

{style=&quot;table-layout:auto&quot;}

**附註**:在進一步通知之前，現有Healthcare Shield客戶將無法使用客戶AI。

如需Customer AI的詳細資訊，請參閱 [Customer AI](../../intelligent-services/customer-ai/overview.md) 概述。

## [!DNL Dashboards] {#dashboards}

Adobe Experience Platform提供多個 [!DNL dashboards] 您可以透過此檢視在每日快照期間擷取的組織資料重要深入分析。

**更新功能**

| 功能 | 說明 |
| --- | --- |
| 已排程的啟動介面工具集 | 此 [!UICONTROL 已排程的啟動] 介面工具集可提供最近啟動之目的地的表格檢視。 對於每個區段，其中包含名稱、目的地平台，以及啟動的開始和結束日期。 此介面工具集可讓您一目瞭然地探索對象啟動的位置和時機，讓重複或不必要的啟動更加透明。 此累積的資訊還突出顯示了任何激活被遺漏的位置。 |

如需 [!DNL Dashboards]，請參閱 [[!DNL Dashboards] 概述](../../dashboards/home.md).

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] 可讓資料工程師將資料對應、轉換及驗證至Experience Data Model(XDM)。

**更新功能**

| 功能 | 說明 |
| --- | --- |
| 支援使用警告擷取記錄 | 「資料準備」現在會將警告（非嚴重錯誤）本地化到欄位，並允許擷取行的其餘部分。 現在，所有映射器轉換錯誤都會回報為警告，而部分擷取的列會視為成功，並顯示警告。  對含有警告和診斷詳細資訊的記錄也支援監視。 部分擷取含有警告的記錄目前僅適用於串流資料。 查看 [使用警告對記錄進行捕獲](../../sources/tutorials/ui/monitor-streaming.md) 以取得更多資訊。 |

{style=&quot;table-layout:auto&quot;}

若要深入了解 [!DNL Data Prep]，請參閱 [[!DNL Data Prep] 概述](../../data-prep/home.md).

## [!DNL Destinations] {#destinations}

[!DNL Destinations] 預先建置與目的地平台的整合，可順暢地從Adobe Experience Platform啟動資料。 您可以使用目的地來針對跨通路行銷活動、電子郵件行銷活動、目標廣告和其他許多使用案例，啟用已知和未知的資料。

**新功能或更新功能**

| 功能 | 說明 |
| ----------- | ----------- |
| （測試版）個人化目的地的屬性型個人化支援 | 隨著屬性型個人化測試版發行，您會在 [目的地目錄](../../destinations/catalog/overview.md): <ul><li>**[!UICONTROL Adobe Target V2]**:此連接器目前為測試版，僅適用於特定數量的客戶。 除了Adobe Target V1卡提供的功能外，Target V2連接器還新增 [對應步驟](/help/destinations/ui/activate-profile-request-destinations.md#map-attributes) 啟用工作流程，此工作流程可讓您將設定檔屬性對應至Adobe Target，啟用以屬性為基礎的同頁和下一頁個人化。</li><li>**[!UICONTROL 使用屬性的自訂個人化]**:此連接器目前為測試版，僅適用於特定數量的客戶。 除了 **[!UICONTROL 自訂個人化]**, **[!UICONTROL 使用屬性的自訂個人化]** 連接器新增可選 [對應步驟](../../destinations/ui/activate-profile-request-destinations.md#map-attributes) 啟用工作流程，此工作流程可讓您將設定檔屬性對應至自訂個人化目的地，啟用以屬性為基礎的同頁和下一頁個人化。</li></ul> <br> 設定檔屬性可能包含敏感資料。 為保護此資料， **[!UICONTROL 使用屬性的自訂個人化]** 目的地需要您使用 [邊緣網路伺服器API](../../server-api/overview.md) 用於資料收集。 此外，所有伺服器API呼叫都必須在 [驗證內容](../../server-api/authentication.md). |

{style=&quot;table-layout:auto&quot;}

**新目的地**

| 目的地 | 說明 |
| ----------- | ----------- |
| [[!DNL Outreach]](../..//destinations/catalog/crm/outreach.md) | [[!DNL Outreach]](https://www.outreach.io/) 是銷售執行平台，具有世界上最多的B2B買方 — 賣方交互資料，以及對專有AI技術的大量投資，用於將銷售資料轉換為智慧。 [!DNL Outreach] 幫助組織實現銷售互動的自動化，並對收入情報採取行動，以提高其效率、可預測性和增長性。 |

{style=&quot;table-layout:auto&quot;}

如需目的地的詳細一般資訊，請參閱 [目的地概述](../../destinations/home.md).

## Experience Data Model(XDM) {#xdm}

XDM是開放原始碼規格，可針對匯入Adobe Experience Platform的資料提供通用結構和定義（結構）。 遵循XDM標準，所有客戶體驗資料皆可整合至通用表示法，以更快速、更整合的方式提供深入分析。 您可以從客戶動作中獲得寶貴的深入分析、透過區段定義客戶受眾，以及將客戶屬性用於個人化目的。

**新XDM元件**

| 元件類型 | 名稱 | 說明 |
| --- | --- | --- |
| 全局架構 | [[!UICONTROL AJO實體結構]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/customerJourneyManagement/ajo-entity.schema.json) | 說明Adobe Journey Optimizer的非正常實體。 |
| 類別 | [[!UICONTROL AJO執行實體]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/customerJourneyManagement/ajo-execution-entity.schema.json) | 說明要用於細分的Adobe Journey Optimizer執行實體。 |
| 欄位群組 | [[!UICONTROL Workfront工作物件]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/workfront/workobjects-all.schema.json) | 一個包裝欄位組，它引用Adobe Workfront的所有較低級別的對象特定欄位組。 |

{style=&quot;table-layout:auto&quot;}

**更新XDM元件**

| 元件類型 | 名稱 | 說明 |
| --- | --- | --- |
| 欄位群組 | [[!UICONTROL Journey Orchestration步驟事件常見欄位]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/journeyOrchestration/stepEvents/journeyStepEventCommonFieldsMixin.schema.json) | 已新增兩個新屬性： `origTimeStamp` 和 `experienceID`. |
| 欄位群組 | [[!UICONTROL 區段成員資格詳細資料]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/shared/segmentation.schema.json) | 除 [!UICONTROL XDM個別設定檔]，此欄位群組現在也可以用於以XDM商業帳戶類別為基礎的結構描述中。 |
| 欄位群組 | （多個） | 與Marketo B2B活動相關的數個欄位群組已更新至穩定狀態。 請參閱下列內容 [提取請求](https://github.com/adobe/xdm/pull/1593/files) 以取得詳細資訊。 |
| 欄位群組 | （多個） | 已更新數個氣象相關欄位群組，以修正 `uvIndex` 和 `sunsetTime`. 請參閱下列內容 [提取請求](https://github.com/adobe/xdm/pull/1602/files) 以取得詳細資訊。 |
| 資料類型 | [[!UICONTROL 產品清單項目]](https://github.com/adobe/xdm/blob/master/components/datatypes/productlistitem.schema.json) | 新屬性 `productImageUrl` 已新增。 |
| 資料類型 | [[!UICONTROL Qoe資料詳細資訊]](https://github.com/adobe/xdm/blob/master/components/datatypes/qoedatadetails.schema.json) | 新屬性 `framesPerSecond` 已新增。 |
| 資料類型 | [[!UICONTROL 工作階段詳細資訊]](https://github.com/adobe/xdm/blob/master/components/datatypes/sessiondetails.schema.json) | `sdkVersion` 已重新命名為 `appVersion`。`meta:enum` 和 `description` 欄位也已更新。 |
| 資料類型和欄位群組 | （多個） | 數種媒體資料類型和欄位群組都有新欄位和更新的說明。 請參閱下列內容 [提取請求](https://github.com/adobe/xdm/pull/1582/files) 以取得詳細資訊。 |
| (全部) | （多個） | 包含 `enum` 欄位現在也包含對應的 `meta:enum` 欄位來表示每個約束的顯示值。 請參閱下列內容 [提取請求](https://github.com/adobe/xdm/pull/1601/files) 以取得詳細資訊。 |

{style=&quot;table-layout:auto&quot;}

如需Platform中XDM的詳細資訊，請參閱 [XDM系統概觀](../../xdm/home.md).

## 即時客戶個人檔案 {#profile}

Adobe Experience Platform可讓您為客戶提供協調、一致且相關的體驗，無論客戶在何處或何時與您的品牌互動。 透過即時客戶個人檔案，您可以全面了解各個客戶，其中結合來自多個管道的資料，包括線上、離線、CRM和第三方資料。 設定檔可讓您將客戶資料併入統一檢視中，提供每個客戶互動的可操作、時間戳記帳戶。

| 功能 | 說明 |
| ------- | ----------- |
| 合併策略硬限制 | Platform現在會強制執行 **五** 合併每個沙箱的原則。 如果您的沙箱目前有五個以上的合併原則，您將 **not** 能夠建立新的合併原則，直到沙箱的合併原則少於五個。 |
| 孤立的設定檔邊緣屬性清除 | 針對所有組織，Profile Service現在會每天移除使用者活動區域的剩餘邊緣屬性，以更精確地呈現您在系統中的設定檔。 指定設定檔的所有設定檔片段都遭刪除後，才會進行此清理，這應會影響從合併的資料集中合併的設定檔 `com_adobe_aep_profile_region_dataset` 標示為 `true`. 這可能會在授權使用控制面板中顯示「可定址的受眾」量度的下降，也可能在設定檔控制面板中顯示「設定檔計數」量度的下降，因為這些量度包含此版本之前剩餘的邊緣屬性片段。 |

{style=&quot;table-layout:auto&quot;}

若要進一步了解即時客戶個人檔案，包括使用個人檔案資料的教學課程和最佳實務，請先閱讀 [即時客戶個人檔案概觀](../../profile/home.md).

## 分段服務 {#segmentation}

[!DNL Segmentation Service] 會透過說明區分客戶群中可行銷人員群組的條件，來定義特定設定檔子集。 區段可以根據記錄資料（例如人口統計資訊）或代表客戶與您品牌互動的時間序列事件。

**新功能**

| 功能 | 說明 |
| ------- | ----------- |
| 支援4000個區段 | 所有使用Platform的組織現在都可支援最多4000個區段定義。 如需此變更如何影響區段工作API的詳細資訊，請參閱 [segment job endpoint guide（段作業端點指南）](../../segmentation/api/segment-jobs.md) |

如需 [!DNL Segmentation Service]，請參閱 [區段概觀](../../segmentation/home.md).

## 來源 {#sources}

Adobe Experience Platform可內嵌來自外部來源的資料，同時允許您使用Platform服務來建構、加標籤及增強該資料。 您可以內嵌來自各種來源的資料，例如Adobe應用程式、雲端儲存、協力廠商軟體和您的CRM系統。

Experience Platform提供RESTful API和互動式UI，讓您輕鬆為各種資料提供者設定來源連線。 這些源連接允許您驗證並連接到外部儲存系統和CRM服務、設定獲取運行時間以及管理資料獲取吞吐量。

**新功能**

| 功能 | 說明 |
| --- | --- |
| 自助來源（批次SDK）正式發行 | 開發、測試和整合您的REST API型資料來源，使用易於配置的來源規格將批次資料內嵌至Experience Platform中。 使用Sources SDK，您可以： <ul><li>為Experience Platform目錄配置新源。</li><li>定義源的規範，包括與支援的驗證類型、計畫以及如何獲取資源資料相關的資訊。</li><li>為新來源建立面向使用者的檔案。</li></ul> 如需詳細資訊，請參閱 [自助來源（批次SDK）](../../sources/sources-sdk/overview.md). |
| 全面可用 [!DNL Google BigQuery] 來源 | 使用 [!DNL Google BigQuery] 來源：從 [!DNL Google BigQuery] 資料倉庫Experience Platform。 如需詳細資訊，請參閱 [[!DNL Google BigQuery] 來源](../../sources/connectors/databases/bigquery.md). |
| [!DNL Teradata Vantage] 來源（測試版） | 使用 [!DNL Teradata Vantage] 來源，從混合式多雲環境內嵌資料至Experience Platform。 如需詳細資訊，請參閱 [[!DNL Teradata Vantage] 來源](../../sources/connectors/databases/teradata-vantage.md). |
| Adobe Analytics來源的跨地區支援 | 您現在可以從任何區域擷取報告套裝 (美國、英國或新加坡)。報表套裝必須對應至與建立來源連線的Experience Platform沙箱例項相同的組織。 如需詳細資訊，請參閱 [在UI中建立Adobe Analytics來源連線](../../sources/tutorials/ui/create/adobe-applications/analytics.md). |

{style=&quot;table-layout:auto&quot;}

若要進一步了解來源，請參閱 [來源概觀](../../sources/home.md).
