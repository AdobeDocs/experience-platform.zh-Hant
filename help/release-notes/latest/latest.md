---
title: Adobe Experience Platform 發行說明
description: Adobe Experience Platform的最新發行說明。
exl-id: f854f9e5-71be-4d56-a598-cfeb036716cb
source-git-commit: 1dc97fa33fa8cb46184e11d311ef8246199b4f03
workflow-type: tm+mt
source-wordcount: '2409'
ht-degree: 5%

---

# Adobe Experience Platform 發行說明

**發行日期：2022 年 5 月 25 日**

Adobe Experience Platform的新功能：

- [基於屬性的訪問控制](#abac)
- [資料衛生](#hygiene)

Adobe Experience Platform 現有功能更新：

- [警報](#alerts)
- [稽核記錄](#audit-logs)
- [儀表板](#dashbaords)
- [資料收集](#data-collection)
- [資料治理](#data-governance)
- [資料準備](#data-prep)
- [目的地](#destinations)
- [體驗資料模型(XDM)](#xdm)
- [查詢服務](#query-service)
- [來源](#sources)

## 基於屬性的訪問控制 {#abac}

>[!IMPORTANT]
>
>基於屬性的訪問控制目前在面向美國醫療保健客戶的有限版本中提供。 這一功能一旦完全發佈，將可供所有Real-time Customer Data Platform客戶使用。

基於屬性的訪問控制是Adobe Experience Platform的一種功能，它使管理員能夠基於屬性控制對特定對象和/或權能的訪問。 屬性可以是添加到對象的元資料，如添加到架構欄位或段的標籤。 管理員定義包括屬性的訪問策略以管理用戶訪問權限。

通過基於屬性的訪問控制，您組織的管理員可以控制用戶對所有平台工作流和資源中敏感個人資料(SPD)和個人識別資訊(PII)的訪問。 管理員可以定義只能訪問特定欄位和與這些欄位對應的資料的用戶角色。

| 功能 | 說明 |
| --- | --- |
| 基於屬性的訪問控制 | 基於屬性的訪問控制允許您使用定義組織或資料使用範圍的標籤來標籤體驗資料模型(XDM)架構欄位。 同時，管理員可以使用用戶和角色管理介面來定義涵蓋XDM架構欄位的訪問策略，並更好地管理提供給用戶或用戶組（內部、外部或第三方用戶）的訪問。 此外，基於屬性的訪問控制允許管理員管理對特定段的訪問。 有關詳細資訊，請參見 [基於屬性的訪問控制概述](../../access-control/abac/overview.md)。 |
| 權限 | 權限是Experience Cloud區域，管理員可以在該區域定義用戶角色和訪問策略，以管理產品應用程式中功能和對象的訪問權限。 通過權限，您可以建立和管理角色，並為這些角色分配所需的資源權限。 權限還允許您管理與特定角色關聯的標籤、沙箱和用戶。 有關詳細資訊，請參見 [權限UI指南](../../access-control/abac/ui/browse.md)。 |

有關基於屬性的訪問控制的詳細資訊，請參閱 [基於屬性的訪問控制概述](../../access-control/abac/overview.md)。

## 資料衛生 {#hygiene}

Experience Platform提供了一套資料衛生功能，允許您通過寫程式刪除消費者記錄和資料集來管理儲存的資料。 使用 [!UICONTROL 資料衛生] 在UI中或通過調用資料衛生API，您可以管理資料儲存以確保資訊按預期使用，在錯誤資料需要修復時更新，並在組織策略認為有必要時刪除。

>[!IMPORTANT]
>
>目前，資料衛生功能僅適用於已購買「Adobe保護保健」附加產品的組織。

**新功能**

| 功能 | 說明 |
| --- | --- |
| 資料集的生存時間(TTL) | [計畫TTL](../../hygiene/ui/ttl.md) 用於平台資料集。 |

{style=&quot;table-layout:auto&quot;}

有關平台中審核日誌的詳細資訊，請參閱 [資料衛生概述](../../hygiene/home.md)。

## 警報 {#alerts}

Experience Platform允許您訂閱各種平台活動的基於事件的警報。 您可以通過 [!UICONTROL 警報] 頁籤，並可以選擇在UI本身或通過電子郵件通知接收警報消息。

**已更新功能**

| 功能 | 警報規則 | 說明 |
| --- | --- | --- |
| 新建警報規則 | 跳頁率超過閾值 | 現在，當源資料流超過標識閾值時，您可以使用警報來接收通知。 請參閱 [警報規則](../../observability/alerts/rules.md) 的子菜單。 |

{style=&quot;table-layout:auto&quot;&quot;

有關警報的詳細資訊，請參閱 [[!DNL Observability Insights] 概述](../../observability/home.md)。

## 稽核記錄 {#audit-logs}

Experience Platform允許您審計用戶活動中的各種服務和功能。 審計日誌提供了有關誰執行了什麼和何時執行的資訊。

**已更新功能**

| 功能 | 名稱 | 說明 |
| --- | --- | --- |
| 已添加資源 | <ul><li> 訪問控制策略 </li><li> 角色 </li><li> 稽核記錄 </li><li> 工作單 </li><li> 標識命名空間 </li><li> 標識圖 </li><li> 查詢 </li><li> 資料集 </li><li> 源資料流 </li></ul> | 在活動發生時自動記錄審核日誌資源。 如果啟用了該功能，則無需手動啟用日誌收集。 |

{style=&quot;table-layout:auto&quot;&quot;

有關平台中審核日誌的詳細資訊，請參閱 [審核日誌概述](../../landing/governance-privacy-security/audit-logs/overview.md)。

## 儀表板 {#dashboards}

Adobe Experience Platform提供了多個儀表板，您可以通過這些儀表板查看有關組織資料的重要資訊，這些資訊在每日快照期間捕獲。

### 配置檔案儀表板

配置式控制面板顯示您的組織在配置式儲存Experience Platform中擁有的屬性（記錄）資料的快照。

**已更新功能**

| 功能 | 說明 |
| --- | --- |
| 按合併策略構件重疊的受眾 | 此小部件顯示段定義的可視交叉，並允許您通過研究段定義之間的相似性來優化分段策略。 |
| 按身份小部件列出的配置檔案計數更改趨勢 | 此小部件通過演示按所需身份篩選的配置檔案的增長模式，幫助您管理目標激活需求。 |

{style=&quot;table-layout:auto&quot;&quot;

有關配置式的詳細資訊，請參閱 [配置檔案儀表板文檔](../../dashboards/guides/profiles.md)。

### 目標儀表板

目標控制面板顯示您的組織在Experience Platform中啟用的目標的快照。

| 功能 | 說明 |
| --- | --- |
| 按目標小部件激活受眾 | 此小部件可幫助您根據激活的受眾數量快速瞭解目標值。 它還讓您能夠輕鬆訪問已映射到目標的段的詳細資訊。 |

{style=&quot;table-layout:auto&quot;&quot;

有關目標的詳細資訊，請參閱 [目標儀表板文檔](../../dashboards/guides/destinations.md)。

### 段儀表板

段控制板提供了用戶介面，您可以通過該介面查看有關段的重要資訊，這些資訊在每日快照期間捕獲。

**已更新功能**

| 功能 | 說明 |
| --- | --- |
| 受眾重疊構件 | 此小部件使您能夠通過可視化段定義結果中的相似性來優化分割策略。 |

{style=&quot;table-layout:auto&quot;&quot;

有關網段的詳細資訊，請參閱 [段儀表板文檔](../../dashboards/guides/segments.md)。

## 資料收集 {#data-collection}

Experience Platform提供了一套技術，使您能夠收集客戶端客戶體驗資料並將其發送到Adobe Experience Platform邊緣網路，在該網路中，資料可以得到豐富、轉換並分發到Adobe或非Adobe目的地。

**新功能**

| 功能 | 說明 |
| --- | --- |
| 複製資料流 | [建立現有資料流的副本](../../edge/datastreams/overview.md#copy) 根據需要調整其配置，避免從頭開始。 |
| 導入資料流映射規則 | 設定資料收集的資料準備時，您可以 [導入現有資料流的映射規則](../../edge/datastreams/data-prep.md#import-mapping) 而不是手動配置每個欄位映射。 |
| 支援Mobile SDK的資料團隊映射 | 現在，您可以在要與Experience PlatformMobile SDK一起使用的資料流上配置資料收集的資料準備。 |
| 支援XDM對象的資料團隊映射 | 將XDM對象與資料層對象映射為 [為資料收集配置資料準備](../../edge/datastreams/data-prep.md#select-data)。 |
| 與資料流整合 | 使用平台中的源目錄訪問平台邊緣網路上的資料，包括資料收集準備和改進對資料準備警告的支援。 查看 [Adobe資料收集源概述](../../sources/connectors/adobe-applications/data-collection.md) 的子菜單。 |

有關平台中資料收集的詳細資訊，請參閱 [資料收集概述](../../collection/home.md)。

## 資料治理 {#governance}

Adobe Experience Platform資料治理是用於管理客戶資料和確保遵守適用於資料使用的法規、限制和策略的一系列戰略和技術。 它在 [!DNL Experience Platform] 包括編目、資料沿襲、資料使用標籤、資料存取策略和對資料的訪問控制，以執行市場營銷操作。

**新功能**

| 功能 | 說明 |
| ------- | ----------- |
| 同意策略執行（可用性有限） | 如果您的組織已購買了「Adobe保護醫療保健」附加產品，您現在可以 [建立同意策略](../../data-governance/policies/user-guide.md#consent-policy) 自動 [在分部參與中強制客戶同意和偏好](../../data-governance/enforcement/auto-enforcement.md#consent-policy-evaluation)。 |

{style=&quot;table-layout:auto&quot;&quot;

查看 [資料治理概述](../../data-governance/home.md) 的子菜單。

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] 允許資料工程師將資料映射到體驗資料模型(XDM)並驗證資料。

**已更新功能**

| 功能 | 說明 |
| ------- | ----------- |
| 基於屬性的訪問控制 [!DNL Data Prep] | 您現在只能映射您有權訪問的屬性。 您無權訪問的屬性不能用於傳遞映射和計算欄位。 有關詳細資訊，請參見 [基於屬性的訪問控制 [!DNL Data Prep]](../../data-prep/home.md)。 **注釋**:基於屬性的訪問控制目前在面向美國醫療保健客戶的有限版本中提供。 這一功能一旦完全發佈，將可供所有Real-time Customer Data Platform客戶使用。 |
| 本地化資料錯誤 | [!DNL Data Prep] 現在將所有轉換錯誤鎖定到屬性級別（以前在行級別）。 現在，資料流將接收填充有沒有任何轉換錯誤的列的部分行，而不是忽略完整行。 |
| 向上插入流到 [!DNL Profile Service] | 流上插頁 [!DNL Data Prep] 將部分行更新發送到配置檔案服務 [[!DNL Amazon Kinesis]](../../sources/connectors/cloud-storage/kinesis.md)。 [[!DNL Azure Event Hubs]](../../sources/connectors/cloud-storage/eventhub.md)或 [[!DNL HTTP API]](../../sources/connectors/streaming/http.md) 源。 請參閱上的指南 [流式](../../data-prep/upserts.md) 的子菜單。 |

{style=&quot;table-layout:auto&quot;&quot;

有關 [!DNL Data Prep]，請參閱 [[!DNL Data Prep] 概述](../../data-prep/home.md)。

## [!DNL Destinations] {#destinations}

[!DNL Destinations] 是預先構建的與目標平台的整合，允許無縫激活來自Adobe Experience Platform的資料。 您可以使用目標來激活跨渠道市場營銷活動、電子郵件活動、目標廣告和許多其他使用案例的已知和未知資料。

**新增或更新的功能**

| 功能 | 說明 |
| ----------- | ----------- |
| 導出最新配置檔案資格 [日段評估](../../destinations/ui/activate-batch-profile-destinations.md#export-full-files) | 現在，您可以安排在完成每日段評估後，使用最新的配置檔案資格進行一次或每天一次的完整檔案導出。 |
| 可選的資料流ID [Adobe Target目的地](../../destinations/catalog/personalization/adobe-target-connection.md) | 為了為無法實現Experience PlatformWeb SDK的用戶啟用Adobe Target個性化，配置Adobe Target目標時，資料流ID選擇現在是可選的。 不使用資料流時，從Experience Platform導出到目標的段將僅支援下一會話個性化，同時禁用邊緣分割以及所有 [使用案例](../../destinations/ui/configure-personalization-destinations.md) 這取決於邊緣分割。 |

{style=&quot;table-layout:auto&quot;&quot;

## 體驗資料模型(XDM) {#xdm}

XDM是一種開源規範，它為傳入Adobe Experience Platform的資料提供通用結構和定義（架構）。 通過遵守XDM標準，所有客戶體驗資料都可以納入到共同的表示形式中，以更快、更整合的方式提供見解。 您可以從客戶操作中獲得有價值的見解，通過細分市場定義客戶受眾，並將客戶屬性用於個性化目的。

**新的XDM元件**

| 元件類型 | 名稱 | 說明 |
| --- | --- | --- |
| 欄位組 | [[!UICONTROL 更改集]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/shared/changeset.schema.json) | 捕獲對資料集和資料集的行級更改。 此欄位組可用於任何類。 |
| 欄位組 | [[!UICONTROL 引用鍵]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-reference-keys.schema.json) | 捕獲ExperienceEvent架構的引用鍵，允許您基於其他類與架構建立關係。 |

{style=&quot;table-layout:auto&quot;&quot;

**更新的XDM元件**

| 元件類型 | 名稱 | 更新說明 |
| --- | --- | --- |
| 行為 | [[!UICONTROL 時間序列架構]](https://github.com/surbhi114/xdm/blob/master/components/behaviors/time-series.schema.json) | 已更新 `eventType` 包括多個與媒體相關的新事件類型和用於Adobe Journey Optimizer的Web渠道入站使用案例。 |
| 全局架構 | [[!UICONTROL 目標]](https://github.com/tumulurik/xdm/blob/master/schemas/destinations/destination.schema.json) | 從中刪除枚舉值 `xdm:destinationCategory`。 |
| 欄位組 | [[!UICONTROL 記錄狀態]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/shared/record-status.schema.json) | 更新的欄位組狀態自 `experimental` 至 `stable`。 |
| 欄位組 | （幾個） | 已更新多個B2B欄位組，因此某些ID欄位被棄用，而使用 [[!UICONTROL B2B源]](../../xdm/data-types/b2b-source.md) 資料類型。 將來更新中不建議使用以前的ID欄位。 請參閱以下內容 [拉式請求](https://github.com/adobe/xdm/pull/1533/files#diff-720c0bb1d1cbaf622f5656c2a4b62d35830c75f6563794da72a280a6a520fbc1) 的子菜單。 |
| 資料類型 | [[!UICONTROL 瀏覽器詳細資訊]](https://github.com/liljenback/xdm/blob/master/components/datatypes/browserdetails.schema.json) | 添加新欄位 `xdm:userAgentClientHints` 它捕獲有關與瀏覽器交互的用戶代理的上下文資訊。 |
| 資料類型 | [[!UICONTROL 媒體資訊]](https://github.com/lidiaist/xdm/blob/master/components/datatypes/media.schema.json) | 已添加 `xdm:playhead` 的子菜單。 固定模式驗證 `xdm:videoSegment`。 |
| 資料類型 | [[!UICONTROL 評級]](https://github.com/lidiaist/xdm/blob/master/components/datatypes/external/iptc/rating.schema.json) | `iptc4xmpExt:RatingSourceLink` 不再是必填欄位。 |

{style=&quot;table-layout:auto&quot;&quot;

有關平台中XDM的詳細資訊，請參見 [XDM系統概述](../../xdm/home.md)。

## 查詢服務 {#query-service}

查詢服務允許您使用標準SQL查詢Adobe Experience Platform的資料 [!DNL data lake]。 您可以加入來自 [!DNL data lake] 並將查詢結果捕獲為新資料集，用於報告、Data Science Workspace或用於接收到即時客戶概要檔案。

**已更新功能**

| 功能 | 說明 |
| --- | --- |
| 查詢服務審核日誌整合 | 查詢服務審核日誌整合提供與查詢相關的用戶操作記錄，以便進行故障排除或遵守公司資料管理策略和法規要求。 查看 [審核日誌整合文檔](../../query-service/data-governance/audit-log-guide.md) 全面的資訊 |
| ALTER TABLE SQL構造 | 使用SQL在即席資料集中設定主標識。 Query Service允許您使用SQL直接將資料集列標籤為主標識或次標識 `ALTER TABLE` 的子菜單。 |

{style=&quot;table-layout:auto&quot;&quot;

有關查詢服務功能的詳細資訊，請參見 [查詢服務概述](../../query-service/home.md)

<!--For more information on data governance in Query Service, see the [data governance overview](../../query-service/data-governance/overview.md).-->

## 來源 {#sources}

Adobe Experience Platform可以從外部源接收資料，同時允許您使用平台服務來構建、標籤和增強資料。 您可以從多種來源(如Adobe應用程式、基於雲的儲存、第三方軟體和您的CRM系統)接收資料。

Experience Platform提供REST風格的API和互動式UI，讓您能夠輕鬆地為各種資料提供程式設定源連接。 通過這些源連接，您可以驗證並連接到外部儲存系統和CRM服務，設定接收運行時間，並管理資料接收吞吐量。

| 功能 | 說明 |
| --- | --- |
| 源中基於屬性的訪問控制 | 您現在可以在接收期間管理和控制對單個源欄位和屬性的訪問。 **注釋**:基於屬性的訪問控制目前在面向美國醫療保健客戶的有限版本中提供。 這一功能一旦完全發佈，將可供所有Real-time Customer Data Platform客戶使用。 |
| Beta版 [!DNL Zendesk] 源 | 使用 [!DNL Zendesk] 源，用於從您的 [!DNL Zendesk] 實例 [!DNL Profile] 濃縮。 查看 [[!DNL Zendesk] 源概述](../../sources/connectors/customer-success/zendesk.md) 的子菜單。 |
| B2B的普遍可用性 [!DNL Microsoft Dynamics] 源 | 您現在可以使用 [!DNL Microsoft Dynamics] 源，用於接收客戶、機會、市場活動、市場營銷清單和市場營銷清單成員等B2B對象。 查看 [[!DNL Microsoft Dynamics] 源概述](../../sources/connectors/crm/ms-dynamics.md) 的子菜單。 |
| 支援Adobe資料收集 | 使用平台中的源目錄訪問平台邊緣網路上的資料，包括資料收集準備和改進對資料準備警告的支援。 查看 [Adobe資料收集源概述](../../sources/connectors/adobe-applications/data-collection.md) 的子菜單。 |
| 支援使用 `ISO-8859-1` 編碼 | 使用 `encoding` 參數以進行攝取 `ISO-8859-1` 已編碼檔案，其中包含雲儲存源到平台 [!DNL Flow Service] API。 請參閱上的指南 [建立雲儲存源連接](../../sources/tutorials/api/collect/cloud-storage.md) 的子菜單。 |

{style=&quot;table-layout:auto&quot;&quot;

要瞭解有關源的詳細資訊，請參閱 [源概述](../../sources/home.md)。
