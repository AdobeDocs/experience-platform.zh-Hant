---
title: Adobe Experience Platform 發行說明
description: Adobe Experience Platform的最新發行說明。
exl-id: f854f9e5-71be-4d56-a598-cfeb036716cb
source-git-commit: 70bc3d8743dfa6c14e8a5c467775faa0c3c5a767
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# Adobe Experience Platform 發行說明

**發行日期：2022 年 24 月 8 日**

Adobe Experience Platform 現有功能更新：

- [[!DNL Artificial Intelligence and Machine Learning Services]](#ai-and-ml-services)
- [[!DNL Dashboards]](#dashboards)
- [[!DNL Data Prep]](#data-prep)
- [[!DNL Destinations]](#destinations)
- [體驗資料模型(XDM)](#xdm)
- [即時客戶個人檔案](#profile)
- [分段服務](#segmentation)
- [來源](#sources)

## [!DNL Artificial Intelligence/Machine Learning services] {#ai-and-ml-services}

AI/ML服務使營銷分析員和從業人員能夠利用人工智慧和機器學習在客戶體驗使用案例中的力量。 這使市場營銷分析員能夠使用業務級配置來設定特定於公司需要的模型，而無需資料科學專業知識。

### Attribution AI

Attribution AI 可將點數歸因到促成轉換事件的接觸點。 行銷人員可善用此工具，協助量化客戶歷程中各個獨立行銷接觸點對行銷的影響。

**已更新功能**

| 功能 | 說明 |
| ------- | ----------- |
| 隱私支援 | <li>Attribution AI現在支援定義用戶角色和訪問策略來管理 [權限](../../../help/access-control/abac/ui/permissions.md) 用於產品應用程式中的功能和對象。</li><li>在活動發生時自動記錄審核日誌資源。</li><li>通過 [基於屬性的訪問控制](../../../help/access-control/abac/overview.md)，管理員可以根據某些屬性控制對特定對象和/或權能的訪問，這些屬性可以添加到對象（如標籤）中的元資料。管理員還可以定義只有權訪問與這些欄位對應的特定欄位和資料的用戶角色。</li><li>[資料衛生](../../../help/hygiene/home.md) Attribution AI中的功能允許您僅使用更新的資料進行進一步的培訓和評分。 同樣，當您請求刪除資料時，Attribution AI也不會使用刪除的資料。</li><li>Attribution AI利用平台資料集。 為幫助促進GDPR法規遵從性，您可以使用Adobe Experience Platform Privacy Service設定協定來滿足客戶訪問和刪除資料湖、身份服務和即時客戶配置檔案中的資料的請求。 所有資料都在傳輸和靜止時被加密。</li> |

{style=&quot;table-layout:auto&quot;}

**注釋**:到2022年第4季度末， Healthcare Shield客戶才能獲得Attribution AI。

有關Attribution AI的詳細資訊，請參閱 [Attribution AI](../../intelligent-services/attribution-ai/overview.md) 概述。

### 客戶AI

在Real-time Customer Data Platform提供的客戶AI用於生成定制傾向得分，如按比例對單個配置檔案進行流失和轉換。

**已更新功能**

| 功能 | 說明 |
| ------- | ----------- |
| 隱私支援 | <li>客戶AI現在支援定義用戶角色和訪問策略以管理 [權限](../../../help/access-control/abac/ui/permissions.md) 用於產品應用程式中的功能和對象。</li><li>在活動發生時自動記錄審核日誌資源。</li><li> 通過 [基於屬性的訪問控制](../../access-control/abac/overview.md)，管理員可以根據特定屬性控制對特定對象和/或權能的訪問。 這些屬性可以是添加到對象（如標籤）的元資料。 管理員還可以定義用戶角色，這些用戶角色只能訪問與這些欄位對應的特定欄位和資料。</li><li>[資料衛生](../../../help/hygiene/home.md) 客戶AI中的功能允許您僅使用更新的資料進行進一步的培訓和評分。 同樣，當您請求刪除資料時，客戶AI不會使用刪除的資料。</li><li>客戶AI利用平台資料集。 為幫助促進GDPR法規遵從性，您可以使用Adobe Experience Platform Privacy Service設定協定來滿足客戶訪問和刪除資料湖、身份服務和即時客戶配置檔案中的資料的請求。 所有資料都在傳輸和靜止時被加密。</li> |

{style=&quot;table-layout:auto&quot;&quot;

**注釋**:在2022年第4季度末之前， Healthcare Shield客戶將無法獲得客戶AI。

有關客戶AI的詳細資訊，請參閱 [客戶AI](../../intelligent-services/customer-ai/overview.md) 概述。

## [!DNL Dashboards] {#dashboards}

Adobe Experience Platform提供 [!DNL dashboards] 通過這些資訊，您可以查看有關組織資料的重要見解，如在每日快照中捕獲的。

**已更新功能**

| 功能 | 說明 |
| --- | --- |
| 計畫激活小部件 | 的 [!UICONTROL 計畫激活] 小部件提供了最近激活的目標的表格化視圖。 對於每個段，它包括名稱、目標平台和激活開始和結束日期。 通過此小部件，您可以快速發現激活受眾的位置和時間，並使重複或不必要的激活更加透明。 這些累積的資訊還突出顯示了任何激活被排除的地方。 |

有關 [!DNL Dashboards]，請參閱 [[!DNL Dashboards] 概述](../../dashboards/home.md)。

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] 允許資料工程師將資料映射到體驗資料模型(XDM)並驗證資料。

**已更新功能**

| 功能 | 說明 |
| --- | --- |
| 支援插入帶警告的記錄 | Data Prep現在將警告（非嚴重錯誤）本地化到欄位，並允許接收行的其餘部分。 現在，所有映射器轉換錯誤都會報告為警告，部分攝取的行被視為成功，並帶有警告。  對包含警告和診斷詳細資訊的記錄也支援監視。 當前，只有流資料才能部分接收帶有警告的記錄。 查看文檔 [正在接收帶警告的記錄](../../sources/tutorials/ui/monitor-streaming.md) 的子菜單。 |

{style=&quot;table-layout:auto&quot;&quot;

瞭解有關 [!DNL Data Prep]，請參見 [[!DNL Data Prep] 概述](../../data-prep/home.md)。

## [!DNL Destinations] {#destinations}

[!DNL Destinations] 是預先構建的與目標平台的整合，允許無縫激活來自Adobe Experience Platform的資料。 您可以使用目標來激活跨渠道市場營銷活動、電子郵件活動、目標廣告和許多其他使用案例的已知和未知資料。

<!--

**New or updated features**

| Feature | Description |
| ----------- | ----------- |
|  ||

{style="table-layout:auto"}

-->

**新目標**

| 目的地 | 說明 |
| ----------- | ----------- |
| [[!DNL Outreach]](../..//destinations/catalog/crm/outreach.md) | [[!DNL Outreach]](https://www.outreach.io/) 是一個銷售執行平台，擁有世界上最多的B2B買方 — 賣方交互資料，並對專有AI技術進行大量投資，以將銷售資料轉換為智慧。 [!DNL Outreach] 幫助企業實現銷售參與的自動化，並採取收入智慧措施，以提高效率、可預測性和增長。 |

{style=&quot;table-layout:auto&quot;&quot;

有關目標的更多一般資訊，請參閱 [目標概述](../../destinations/home.md)。

## 體驗資料模型(XDM) {#xdm}

XDM是一種開源規範，它為傳入Adobe Experience Platform的資料提供通用結構和定義（架構）。 通過遵守XDM標準，所有客戶體驗資料都可以納入到共同的表示形式中，以更快、更整合的方式提供見解。 您可以從客戶操作中獲得有價值的見解，通過細分市場定義客戶受眾，並將客戶屬性用於個性化目的。

**新的XDM元件**

| 元件類型 | 名稱 | 說明 |
| --- | --- | --- |
| 全局架構 | [[!UICONTROL AJO實體架構]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/customerJourneyManagement/ajo-entity.schema.json) | 描述Adobe Journey Optimizer的非正常實體。 |
| 類 | [[!UICONTROL AJO執行實體]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/customerJourneyManagement/ajo-execution-entity.schema.json) | 描述用於分段的Adobe Journey Optimizer執行實體。 |
| 欄位群組 | [[!UICONTROL Workfront工作對象]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/workfront/workobjects-all.schema.json) | 引用Adobe Workfront的所有低級對象特定欄位組的包裝欄位組。 |

{style=&quot;table-layout:auto&quot;&quot;

**更新的XDM元件**

| 元件類型 | 名稱 | 說明 |
| --- | --- | --- |
| 欄位群組 | [[!UICONTROL Journey Orchestration步驟事件公用欄位]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/journeyOrchestration/stepEvents/journeyStepEventCommonFieldsMixin.schema.json) | 添加了兩個新屬性： `origTimeStamp` 和 `experienceID`。 |
| 欄位群組 | [[!UICONTROL 段成員身份詳細資訊]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/shared/segmentation.schema.json) | 除 [!UICONTROL XDM個人配置檔案]，此欄位組現在也可以用於基於XDM業務帳戶類的架構中。 |
| 欄位群組 | （多個） | 一些與MarketoB2B活動有關的外地小組已更新為穩定狀態。 請參閱以下內容 [拉式請求](https://github.com/adobe/xdm/pull/1593/files) 的雙曲餘切值。 |
| 欄位群組 | （多個） | 已更新幾個與天氣有關的現場組，以修復為 `uvIndex` 和 `sunsetTime`。 請參閱以下內容 [拉式請求](https://github.com/adobe/xdm/pull/1602/files) 的雙曲餘切值。 |
| 資料類型 | [[!UICONTROL 產品清單項]](https://github.com/adobe/xdm/blob/master/components/datatypes/productlistitem.schema.json) | 新屬性 `productImageUrl` 已添加。 |
| 資料類型 | [[!UICONTROL Qoe資料詳細資訊]](https://github.com/adobe/xdm/blob/master/components/datatypes/qoedatadetails.schema.json) | 新屬性 `framesPerSecond` 已添加。 |
| 資料類型 | [[!UICONTROL 會話詳細資訊資訊]](https://github.com/adobe/xdm/blob/master/components/datatypes/sessiondetails.schema.json) | `sdkVersion` 已重新命名為 `appVersion`。`meta:enum` 和 `description` 欄位也已更新。 |
| 資料類型和欄位組 | （多個） | 多個媒體資料類型和欄位組具有新欄位和更新的說明。 請參閱以下內容 [拉式請求](https://github.com/adobe/xdm/pull/1582/files) 的雙曲餘切值。 |
| (全部) | （多個） | 包含 `enum` 欄位現在還包含相應的 `meta:enum` 欄位，以表示每個約束的顯示值。 請參閱以下內容 [拉式請求](https://github.com/adobe/xdm/pull/1601/files) 的雙曲餘切值。 |

{style=&quot;table-layout:auto&quot;&quot;

有關平台中XDM的詳細資訊，請參見 [XDM系統概述](../../xdm/home.md)。

## 即時客戶個人檔案 {#profile}

Adobe Experience Platform使您能夠為您的客戶提供協調、一致和相關的體驗，無論客戶在何處或何時與您的品牌進行交互。 通過即時客戶概要資訊，您可以看到每個客戶的整體視圖，該視圖將來自多個渠道的資料組合在一起，包括線上、離線、CRM和第三方資料。 配置檔案允許您將客戶資料整合到一個統一視圖中，為每次客戶交互提供一個可操作且時間戳記的帳戶。

| 功能 | 說明 |
| ------- | ----------- |
| 合併策略硬限制 | 平台現在將強制執行 **五** 合併每個沙盒的策略。 如果您的沙盒當前有五個以上的合併策略，您將 **不** 能夠建立新的合併策略，直到沙盒的合併策略少於五個。 |
| 孤立配置檔案邊緣屬性清理 | 對於所有組織，配置檔案服務現在每天刪除用戶活動區域的剩餘邊緣屬性，以便更準確地表示您在系統中的配置檔案。 在刪除給定配置檔案的所有配置檔案片段後進行此清理，並且應影響從其中合併的資料集中合併的配置檔案 `com_adobe_aep_profile_region_dataset` 標籤為 `true`。 這可能顯示許可證使用儀表板中「可定址受眾」度量的下落，也可能顯示配置檔案儀表板中「配置檔案計數」度量的下落，因為這些度量包括此版本之前剩餘的邊緣屬性片段。 |

{style=&quot;table-layout:auto&quot;&quot;

要瞭解有關即時客戶概要資訊的更多資訊，包括有關使用概要資訊資料的教程和最佳做法，請首先閱讀 [即時客戶概要資訊概述](../../profile/home.md)。

## 分段服務 {#segmentation}

[!DNL Segmentation Service] 通過描述區分客戶群中可銷售人員組的標準來定義特定配置檔案子集。 段可以基於記錄資料（如人口統計資訊）或表示客戶與您品牌的交互的時間序列事件。

**新功能**

| 功能 | 說明 |
| ------- | ----------- |
| 支援4000個段 | 所有使用平台的組織現在可支援多達4000個段定義。 有關此更改如何影響段作業API的詳細資訊，請閱讀 [段作業終結點指南](../../segmentation/api/segment-jobs.md) |

有關 [!DNL Segmentation Service]，請參閱 [分段概述](../../segmentation/home.md)。

## 來源 {#sources}

Adobe Experience Platform可以從外部源接收資料，同時允許您使用平台服務來構建、標籤和增強資料。 您可以從多種來源(如Adobe應用程式、基於雲的儲存、第三方軟體和您的CRM系統)接收資料。

Experience Platform提供REST風格的API和互動式UI，讓您能夠輕鬆地為各種資料提供程式設定源連接。 通過這些源連接，您可以驗證並連接到外部儲存系統和CRM服務，設定接收運行時間，並管理資料接收吞吐量。

**新功能**

| 功能 | 說明 |
| --- | --- |
| 自助源的一般可用性（批SDK） | 開發、test和整合基於REST API的資料源，以便使用易於配置的源規範將批資料Experience Platform。 使用Sources SDK，您可以： <ul><li>為Experience Platform目錄配置新源。</li><li>定義源的規範，包括與支援的驗證類型、計畫以及獲取資源資料的方式有關的資訊。</li><li>為新源建立面向用戶的文檔。</li></ul> 有關詳細資訊，請閱讀 [自助源（批處理SDK）](../../sources/sources-sdk/overview.md)。 |
| 2004年12月 [!DNL Google BigQuery] 源 | 使用 [!DNL Google BigQuery] 從您的 [!DNL Google BigQuery] 資料倉庫到Experience Platform。 有關詳細資訊，請閱讀 [[!DNL Google BigQuery] 源](../../sources/connectors/databases/bigquery.md)。 |
| [!DNL Teradata Vantage] 源(Beta) | 使用 [!DNL Teradata Vantage] 將資料從混合多雲環境中接收到Experience Platform。 有關詳細資訊，請閱讀 [[!DNL Teradata Vantage] 源](../../sources/connectors/databases/teradata-vantage.md)。 |
| 跨區域支助Adobe Analytics來源 | 您現在可以從任何區域擷取報告套裝 (美國、英國或新加坡)。報表套件必須映射到與正在其中建立源連接的Experience Platform沙盒實例相同的組織。 有關詳細資訊，請閱讀上的指南 [在UI中建立Adobe Analytics源連接](../../sources/tutorials/ui/create/adobe-applications/analytics.md)。 |

{style=&quot;table-layout:auto&quot;&quot;

要瞭解有關源的詳細資訊，請參閱 [源概述](../../sources/home.md)。