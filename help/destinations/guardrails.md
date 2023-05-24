---
keywords: Experience Platform；激活；故障排除；護欄；指南；限制
title: 激活資料的預設護欄
solution: Experience Platform
product: experience platform
type: Documentation
description: 瞭解有關資料激活預設使用和速率限制的詳細資訊。
exl-id: a755f224-3329-42d6-b8a9-fadcf2b3ca7b
source-git-commit: 7c1d956e3b6a1314baa13fef823d73d42404516a
workflow-type: tm+mt
source-wordcount: '1177'
ht-degree: 1%

---

# 用於激活資料的護欄

此頁提供有關激活行為的預設使用和速率限制。 在查看以下護欄時，假定您已正確 [連接到目標](/help/destinations/ui/connect-destination.md)。

>[!NOTE]
>
>* 大多數客戶未超過這些預設限制。 如果您想瞭解自定義限制，請與您的客戶服務代表聯繫。
>* 本檔案中概述的限制正在不斷改進。 請定期回頭查看更新。
>* 根據各個下游限制，某些目標可能具有比本頁中記錄的目標更緊密的護欄。 確保同時檢查 [目錄](/help/destinations/catalog/overview.md) 連接和激活資料的目標的頁面。


## 限制類型 {#limit-types}

本文檔中有兩種預設限制類型：

* **軟限制：** 可以超出軟限制，但軟限制為系統效能提供了建議的准則。
* **硬限制：** 硬限制提供絕對最大值。 Experience PlatformUI或API不允許您超出此限制，或者，如果超出此限制，則返回錯誤。


## 激活限制 {#activation-limits}

以下護欄在將即時客戶配置檔案資料激活到目標時提供建議的限制。

### 一般激活護欄 {#general-activation-guardrails}

下面的護欄通常適用於通過 [所有目標類型](/help/destinations/destination-types.md#destination-types)。

| 瓜德賴爾 | 限制 | 限制類型 | 說明 |
| --- | --- | --- | --- |
| 到單個目標的最大段數 | 250 | 軟 | 建議將最多250個段映射到資料流中的單個目標。 <br><br> 如果需要激活到目標的250多個段，則可以執行以下任一操作： <ul><li> 取消映射您不想再激活的段，或</li><li>建立到所需目標的新資料流，並將段映射到此新資料流。</li></ul> <br> 請注意，對於某些目標，映射到目標的段數可能不足250個。 這些目的地在頁面下各節中進一步列出。 |
| 最大目標數 | 100 | 軟 | 建議最多建立100個目標，您可以將資料連接和激活到 *每個沙盒*。 [邊緣個性化目標（自定義個性化）](#edge-destinations-activation) 在100個建議的目的地中，最多可以佔10個。 |
| 映射到目標的最大屬性數 | 50 | 軟 | 對於多個目標和目標類型，您可以選擇要映射以導出的配置檔案屬性和標識。 為獲得最佳效能，資料流中最多應將50個屬性映射到目標。 |
| 已激活到目標的資料類型 | 配置檔案資料，包括身份和身份映射 | 硬 | 目前，只能導出 *配置檔案記錄屬性* 到目的地。 目前不支援導出描述事件資料的XDM屬性。 |
| 已激活到目標的資料類型 — 陣列和映射屬性支援 | 未提供 | 硬 | 這個時候， **不** 可能導出 *陣列或映射屬性* 到目的地。 此規則的例外是 [身份映射](/help/xdm/field-groups/profile/identitymap.md)，在流和基於檔案的激活中都導出。 |

{style="table-layout:auto"}

### 流激活 {#streaming-activation}

下面的護欄適用於通過 [流目標](/help/destinations/ui/activate-segment-streaming-destinations.md)。

| 瓜德賴爾 | 限制 | 限制類型 | 說明 |
| --- | --- | --- | --- |
| 每秒激活次數（帶有配置檔案導出的HTTP消息） | 不適用 | - | 當前對每秒從Experience Platform發送到夥伴目標的API終結點的消息數沒有限制。 <br> 任何限制或延遲都由Experience Platform發送資料的終結點指定。 確保同時檢查 [目錄](/help/destinations/catalog/overview.md) 連接和激活資料的目標的頁面。 |

{style="table-layout:auto"}

### 批（基於檔案）激活 {#batch-file-based-activation}

下面的護欄適用於通過 [批處理（基於檔案）目標](/help/destinations/ui/activate-batch-profile-destinations.md)。

| 瓜德賴爾 | 限制 | 限制類型 | 說明 |
| --- | --- | --- | --- |
| 激活頻率 | 每3、6、8或12小時進行一次完全出口或更頻繁的增量出口。 | 硬 | 閱讀 [導出完整檔案](/help/destinations/ui/activate-batch-profile-destinations.md#export-full-files) 和 [導出增量檔案](/help/destinations/ui/activate-batch-profile-destinations.md#export-incremental-files) 文檔部分，以瞭解有關批處理導出的頻率增量的詳細資訊。 |
| 可在給定小時導出的段的最大數 | 100 | 軟 | 建議將最多100個段添加到批處理目標資料流中。 |
| 每個要激活的檔案的最大行數（記錄） | 500萬 | 硬 | Adobe Experience Platform自動將每個檔案以500萬條記錄（行）的速度拆分導出的檔案。 每行代表一個配置檔案。 拆分檔案名後附加一個數字，表示檔案是較大導出的一部分，如下所示： `filename.csv`。 `filename_2.csv`。 `filename_3.csv`。 有關詳細資訊，請閱讀 [調度節](/help/destinations/ui/activate-batch-profile-destinations.md#scheduling) 的子菜單。 |

{style="table-layout:auto"}

### 即席激活 {#ad-hoc-activation}

下面的護欄適用於 [即席激活](/help/destinations/api/ad-hoc-activation-api.md) 的雙曲餘切值。

| 瓜德賴爾 | 限制 | 限制類型 | 說明 |
| --- | --- | --- | --- |
| 每個即席激活作業激活的段 | 80 | 硬 | 目前，每個即席激活作業最多可激活80個段。 嘗試激活每個作業超過80個段將導致作業失敗。 此行為在未來版本中可能會發生更改。 |
| 每個段的併發即席激活作業 | 1 | 硬 | 每個段不要運行多個併發點對點激活作業。 |

{style="table-layout:auto"}

### 邊緣個性化目標激活 {#edge-destinations-activation}

下面的護欄適用於通過 [邊緣個性化目標](/help/destinations/destination-types.md#streaming-profile-export)。

| 瓜德賴爾 | 限制 | 限制類型 | 說明 |
| --- | --- | --- | --- |
| 最大數量 [自定義個性化](/help/destinations/catalog/personalization/custom-personalization.md) 目的地 | 10 | 軟 | 您可以將資料流設定為每個沙箱的10個自定義個性化目標。 |
| 每個沙盒映射到個性化目標的最大屬性數 | 30 | 硬 | 每個沙箱在資料流中最多可將30個屬性映射到個性化目標。 |
| 映射到單個資料段的最大數 [Adobe Target](/help/destinations/catalog/personalization/adobe-target-connection.md) 目標 | 50 | 軟 | 在到單個Adobe Target目標的激活流中，最多可激活50個段。 |

{style="table-layout:auto"}

### Destination SDK護欄 {#destination-sdk-guardrails}

[Destination SDK](/help/destinations/destination-sdk/overview.md) 是一套配置API，允許您配置目標整合模式，以便根據您選擇的資料和身份驗證格式將受眾和配置檔案資料Experience Platform到您的終結點。 下面的護欄適用於您使用Destination SDK配置的目標。

| 瓜德賴爾 | 限制 | 限制類型 | 說明 |
| --- | --- | --- | --- |
| 最大數量 [私有自定義目標](/help/destinations/destination-sdk/overview.md#productized-custom-integrations) | 5 | 軟 | 您最多可以使用Destination SDK建立5個專用自定義流或批處理目標。 如果您需要建立超過5個此類目的地，請聯繫定制護理代表。 |
| 配置檔案導出策略以用於Destination SDK | <ul><li>`maxBatchAgeInSecs` （最少1.800和最多3.600）</li><li>`maxNumEventsInBatch` （最少1.000，最多10.000）</li></ul> | 硬 | 使用 [可配置聚合](destination-sdk/functionality/destination-configuration/aggregation-policy.md#configurable-aggregation) 選項，請注意確定HTTP消息發送到基於API的目標的頻率以及消息應包含的配置檔案的最小值和最大值。 |

{style="table-layout:auto"}

### 目標限制和重試策略 {#destination-throttling-and-retry-policy}

有關給定目標的限制閾值或限制的詳細資訊。 本節還提供有關目標的重試策略的資訊。

| 目標類型 | 說明 |
| --- | --- |
| 企業目標(HTTP API、AmazonKinesis、Azure EventHub) | 在95%的時間內，Experience Platform會嘗試為成功發送的消息提供少於10分鐘的吞吐量延遲，每個資料流的請求速率低於每秒1萬次。 <br> 如果向企業目標發送請求失敗，Experience Platform將儲存失敗的請求並重試兩次，以將請求發送到終結點。 |

{style="table-layout:auto"}

## 其他Experience Platform服務的護欄 {#guardrails-other-services}

查看其他Experience Platform服務的護欄資訊：

* 用於 [資料攝取](/help/ingestion/guardrails.md)
* 用於 [[!DNL Identity Service] 資料](/help/identity-service/guardrails.md)
* 用於 [[!DNL Real-Time Customer Profile] 資料](/help/profile/guardrails.md)
* 用於 [[!DNL Query Service] 資料](/help/query-service/guardrails.md)
