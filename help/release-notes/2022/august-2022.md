---
title: Adobe Experience Platform發行說明2022年8月
description: 2022年8月發佈的Adobe Experience Platform說明。
source-git-commit: c3452dda554b3c7750ad1166cef598d51d739e02
workflow-type: tm+mt
source-wordcount: '1348'
ht-degree: 7%

---

# Adobe Experience Platform 發行說明

**發行日期：2022 年 24 月 8 日**

Adobe Experience Platform 現有功能更新：

- [[!DNL Dashboards]](#dashboards)
- [資料準備](#data-prep)
- [體驗資料模型(XDM)](#xdm)
- [即時客戶個人檔案](#profile)
- [分段服務](#segmentation)
- [來源](#sources)

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

{style=&quot;table-layout:auto&quot;}

瞭解有關 [!DNL Data Prep]，請參見 [[!DNL Data Prep] 概述](../../data-prep/home.md)。

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
| 孤立配置檔案邊緣屬性清理 | 對於所有組織，配置檔案服務現在每天刪除用戶活動區域的剩餘邊緣屬性，以便更準確地表示您在系統中的配置檔案。 在刪除給定配置檔案的所有配置檔案片段後進行此清理，並且應影響從其中合併的資料集中合併的配置檔案 `com_adobe_aep_profile_region_dataset` 標籤為 `true`。 這可能顯示許可證使用儀表板中「可定址受眾」度量的下降，也可能顯示配置檔案儀表板中「配置檔案計數」度量的下降，因為這些度量包括此版本之前剩餘的邊緣屬性片段。 |

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
| API支援按需接收 | 使用按需接收為給定資料流建立專用流運行， [!DNL Flow Service] API。 建立的流運行必須設定為一次性接收。 有關詳細資訊，請閱讀上的指南 [使用API建立用於按需接收的流運行](../../sources/tutorials/api/on-demand-ingestion.md) 的子菜單。 |

{style=&quot;table-layout:auto&quot;&quot;

要瞭解有關源的詳細資訊，請參閱 [源概述](../../sources/home.md)。
