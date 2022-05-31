---
title: Adobe Experience Platform 發行說明
description: Adobe Experience Platform的最新發行說明。
exl-id: f854f9e5-71be-4d56-a598-cfeb036716cb
source-git-commit: 1b417935d557f7d58039c508544ed768f6ad1cc4
workflow-type: tm+mt
source-wordcount: '1719'
ht-degree: 6%

---

# Adobe Experience Platform 發行說明

**發行日期：2022 年 5 月 25 日**

<!-- New features in Adobe Experience Platform: -->

<!-- - [Attribute-based access control](#abac) -->
<!-- - [Data hygiene](#hygiene) -->

Adobe Experience Platform 現有功能更新：

- [警報](#alerts)
- [稽核記錄](#audit-logs)
- [儀表板](#dashbaords)
- [資料收集](#data-collection)
<!-- - [Data Governance](#data-governance) -->
- [資料準備](#data-prep)
- [目的地](#destinations)
- [體驗資料模型(XDM)](#xdm)
- [查詢服務](#query-service)
- [來源](#sources)

## 警報 {#alerts}

Experience Platform允許您訂閱各種平台活動的基於事件的警報。 您可以通過 [!UICONTROL 警報] 頁籤，並可以選擇在UI本身或通過電子郵件通知接收警報消息。

**已更新功能**

| 功能 | 警報規則 | 說明 |
| --- | --- | --- |
| 新建警報規則 | 跳頁率超過閾值 | 現在，當源資料流超過標識閾值時，您可以使用警報來接收通知。 請參閱 [警報規則](../../observability/alerts/rules.md) 的子菜單。 |

{style=&quot;table-layout:auto&quot;}


<!-- ## Attribute-based access control {#abac}

>[!IMPORTANT]
>
>Attribute-based access control is currently available in a limited release for US-based healthcare customers. This capability will be available to all Real-time Customer Data Platform customers once it is fully released.

Attribute-based access control is a capability of Adobe Experience Platform that enables administrators to control access to specific objects and/or capabilities based on attributes. Attributes can be metadata added to an object, such as a label added to a schema field or segment. An administrator defines access policies that include attributes to manage user access permissions.

Through attribute-based access control, administrators of your organization can control users’ access to both sensitive personal data (SPD) and personally identifiable information (PII) across all Platform workflows and resources. Administrators can define user roles that have access only to specific fields and data that correspond to those fields.

| Feature | Description |
| --- | --- |
| Attribute-based access control | Attribute-based access control allows you to label Experience Data Model (XDM) schema fields with labels that define organizational or data usage scopes. In parallel, administrators can use the user and role administration interface to define access policies covering XDM schema fields and better manage the access given to users or groups of users (internal, external, or third-party users). Additionally, attribute-based access control allows administrators to manage access to specific segments. |
| Permissions | Permissions is the area of Experience Cloud where administrators can define user roles and access policies to manage access permissions for features and objects within a product application. Through Permissions, you can create and manage roles, as well as assign the desired resource permissions for these roles. Permissions also allow you to manage the labels, sandboxes, and users associated with a specific role. For more information, see the [Permissions UI guide](../../access-control/abac/ui/browse.md). |

For more information on attribute-based access control, see the [attribute-based access control overview](../../access-control/abac/overview.md). -->

<!-- ## Data hygiene {#hygiene}

Experience Platform provides a suite of data hygiene capabilities that allow you manage your stored data through programmatic deletions of consumer records and datasets. Using either the [!UICONTROL Data Hygiene] workspace in the UI or through calls to the Data Hygiene API, you can manage your data stores to ensure that information is used as expected, is updated when incorrect data needs fixing, and is deleted when organizational policies deem it necessary.

>[!IMPORTANT]
>
>Data hygiene capabilities are currently only available for organizations that have purchased the Adobe Shield for Healthcare add-on offering.

**New features**

| Feature | Description |
| --- | --- |
| Consumer deletion | [Delete consumer records](../../hygiene/ui/delete-consumer.md) from the data lake and Profile store based on primary identity data. |
| Time to live (TTL) for datasets | [Schedule TTLs](../../hygiene/ui/ttl.md) for Platform datasets.  |

For more information on audit logs in Platform, refer to the [data hygiene overview](../../hygiene/home.md). -->

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

<!-- ## Data Governance {#governance}

Adobe Experience Platform Data Governance is a series of strategies and technologies used to manage customer data and ensure compliance with regulations, restrictions, and policies applicable to data usage. It plays a key role within [!DNL Experience Platform] at various levels, including cataloging, data lineage, data usage labeling, data access policies, and access control on data for marketing actions.

**New features**

| Feature | Description | 
| ------- | ----------- |
| Consent policy enforcement (limited availability) | If your organization has purchased the Adobe Shield for Healthcare add-on offering, you can now [create consent policies](../../data-governance/policies/user-guide.md#consent-policy) to automatically [enforce customer consents and preferences in segment participation](../../data-governance/enforcement/auto-enforcement.md#consent-policy-evaluation). |

{style="table-layout:auto"}

See the [Data Governance overview](../../data-governance/home.md) for more information on the service. -->

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] 允許資料工程師將資料映射到體驗資料模型(XDM)並驗證資料。

**已更新功能**

| 功能 | 說明 |
| ------- | ----------- |
| 本地化資料錯誤 | [!DNL Data Prep] 現在將所有轉換錯誤鎖定到屬性級別（以前在行級別）。 現在，資料流將接收填充有沒有任何轉換錯誤的列的部分行，而不是忽略完整行。 |
| 向上插入流到 [!DNL Profile Service] | 流上插頁 [!DNL Data Prep] 將部分行更新發送到配置檔案服務 [[!DNL Amazon Kinesis]](../../sources/connectors/cloud-storage/kinesis.md)。 [[!DNL Azure Event Hubs]](../../sources/connectors/cloud-storage/eventhub.md)或 [[!DNL HTTP API]](../../sources/connectors/streaming/http.md) 源。 請參閱上的指南 [流式](../../data-prep/upserts.md) 的子菜單。 |

{style=&quot;table-layout:auto&quot;&quot;

<!-- | Attribute-based access control in [!DNL Data Prep] | You will now only be able to map attributes that you have access to. Attributes that you do not have access to can not be used in pass-through mappings and calculated fields. For more information, see [attribute-based access control in [!DNL Data Prep]](../../data-prep/home.md). **Note**: Attribute-based access control is currently available in a limited release for US-based healthcare customers. This capability will be available to all Real-time Customer Data Platform customers once it is fully released. | -->

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

<!-- For more information on data governance in Query Service, see the [data governance overview](../../query-service/data-governance/overview.md). -->

有關查詢服務功能的詳細資訊，請參見 [查詢服務概述](../../query-service/home.md)

## 來源 {#sources}

Adobe Experience Platform可以從外部源接收資料，同時允許您使用平台服務來構建、標籤和增強資料。 您可以從多種來源(如Adobe應用程式、基於雲的儲存、第三方軟體和您的CRM系統)接收資料。

Experience Platform提供REST風格的API和互動式UI，讓您能夠輕鬆地為各種資料提供程式設定源連接。 通過這些源連接，您可以驗證並連接到外部儲存系統和CRM服務，設定接收運行時間，並管理資料接收吞吐量。

| 功能 | 說明 |
| --- | --- |
| Beta版 [!DNL Zendesk] 源 | 使用 [!DNL Zendesk] 源，用於從您的 [!DNL Zendesk] 實例 [!DNL Profile] 濃縮。 查看 [[!DNL Zendesk] 源概述](../../sources/connectors/customer-success/zendesk.md) 的子菜單。 |
| B2B的普遍可用性 [!DNL Microsoft Dynamics] 源 | 您現在可以使用 [!DNL Microsoft Dynamics] 源，用於接收客戶、機會、市場活動、市場營銷清單和市場營銷清單成員等B2B對象。 查看 [[!DNL Microsoft Dynamics] 源概述](../../sources/connectors/crm/ms-dynamics.md) 的子菜單。 |
| 支援Adobe資料收集 | 使用源目錄訪問資料收集體驗邊緣資料，包括資料收集的資料準備和對資料準備中資料警告的改進支援。 查看 [Adobe資料收集源概述](../../sources/connectors/adobe-applications/data-collection.md) 的子菜單。 |
| 支援使用 `ISO-8859-1` 編碼 | 使用 `encoding` 參數以進行攝取 `ISO-8859-1` 已編碼檔案，其中包含雲儲存源到平台 [!DNL Flow Service] API。 請參閱上的指南 [建立雲儲存源連接](../../sources/tutorials/api/collect/cloud-storage.md) 的子菜單。 |

{style=&quot;table-layout:auto&quot;&quot;

<!-- | Attribute-based access control in sources | You can now manage and control access to individual source fields and attributes during ingestion. **Note**: Attribute-based access control is currently available in a limited release for US-based healthcare customers. This capability will be available to all Real-time Customer Data Platform customers once it is fully released.  | -->

要瞭解有關源的詳細資訊，請參閱 [源概述](../../sources/home.md)。
