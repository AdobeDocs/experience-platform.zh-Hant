---
keywords: Experience Platform；啟動；疑難排解；護欄；准則；限制
title: 激活資料的預設護欄
solution: Experience Platform
product: experience platform
type: Documentation
description: 進一步了解資料啟用的預設使用量和比率限制。
source-git-commit: 69496d2e00ce866413786160d4524cabd03ae350
workflow-type: tm+mt
source-wordcount: '1198'
ht-degree: 3%

---

# 激活資料的護欄

此頁面提供與啟動行為相關的預設使用量和比率限制。 在查看以下護欄時，假定您已正確 [已連線至目的地](/help/destinations/ui/connect-destination.md).

>[!NOTE]
>
>* 大部分客戶未超過這些預設限制。 若您想了解自訂限制，請聯絡客戶服務代表。
>* 本檔案中概述的限制正在不斷改進。 請定期回來查看更新。
>* 根據個別的下游限制，某些目的地的護欄可能比本頁記錄的更嚴格。 也務必檢查 [目錄](/help/destinations/catalog/overview.md) 連線和啟用資料的目標頁面。


## 限制類型 {#limit-types}

本文檔中有兩種預設限制類型：

* **軟限制：** 可能超出軟限制，但軟限制為系統效能提供建議的准則。
* **硬限制：** 硬限制提供絕對最大值。 Experience PlatformUI或API不允許超過此限制，若超過此限制，則會傳回錯誤。


## 啟用限制 {#activation-limits}

在將即時客戶設定檔資料啟用至目的地時，以下護欄提供建議的限制。

### 一般激活護欄 {#general-activation-guardrails}

下面的護欄通常適用於通過 [所有目的地類型](/help/destinations/destination-types.md#destination-types).

| 瓜德拉伊 | 限制 | 限制類型 | 說明 |
| --- | --- | --- | --- |
| 單一目的地的區段數上限 | 250 | 軟 | 建議最多將250個區段對應至資料流中的單一目的地。 <br><br> 如果您需要啟用超過250個區段至目的地，您可以： <ul><li> 取消對應您不想再啟用的區段，或</li><li>建立新資料流到所需的目標，並將段映射到此新資料流。</li></ul> <br> 請注意，某些目的地的對應區段數可能會限制在250個以內。 這些目的地在頁面下方各節的更多部分會呼叫。 |
| 目的地數上限 | 100 | 軟 | 建議您最多建立100個目標，以便連線並啟用資料 *每個沙箱*. [邊緣個人化目的地（自訂個人化）](#edge-destinations-activation) 在100個建議的目的地中，最多可組成10個。 |
| 映射到目標的最大屬性數 | 50 | 軟 | 若是數種目的地和目的地類型，您可以選取要對應以匯出的設定檔屬性和身分。 為了獲得最佳效能，資料流中最多應將50個屬性映射到目標。 |
| 已啟動至目的地的資料類型 | 設定檔資料，包括身分和身分對應 | 硬 | 目前，僅可匯出 *設定檔記錄屬性* 目的地。 目前不支援匯出描述事件資料的XDM屬性。 |
| 已啟動至目的地的資料類型 — 陣列和地圖屬性支援 | 未提供 | 硬 | 現在， **not** 可匯出 *陣列或地圖屬性* 目的地。 此規則的例外是 [身分圖](/help/xdm/field-groups/profile/identitymap.md)，會匯出至串流和檔案型啟用中。 |

{style=&quot;table-layout:auto&quot;}

### 串流啟動 {#streaming-activation}

下面的護欄適用於通過 [串流目的地](/help/destinations/ui/activate-segment-streaming-destinations.md).

| 瓜德拉伊 | 限制 | 限制類型 | 說明 |
| --- | --- | --- | --- |
| 每秒激活數（具有配置檔案導出的HTTP消息） | 不適用 | - | 目前，從Experience Platform傳送至合作夥伴目的地的API端點的訊息數目沒有限制。 <br> 任何限制或延遲由Experience Platform傳送資料的端點指定。 也務必檢查 [目錄](/help/destinations/catalog/overview.md) 連線和啟用資料的目標頁面。 |

{style=&quot;table-layout:auto&quot;}

### 批次（基於檔案）激活 {#batch-file-based-activation}

下面的護欄適用於通過 [批次（檔案型）目的地](/help/destinations/ui/activate-batch-profile-destinations.md).

| 瓜德拉伊 | 限制 | 限制類型 | 說明 |
| --- | --- | --- | --- |
| 激活頻率 | 每3、6、8或12小時一次完全導出或多次增量導出。 | 硬 | 閱讀 [導出完整檔案](/help/destinations/ui/activate-batch-profile-destinations.md#export-full-files) 和 [導出增量檔案](/help/destinations/ui/activate-batch-profile-destinations.md#export-incremental-files) 說明檔案章節，以取得批次匯出之頻率增量的詳細資訊。 |
| 在指定小時可匯出的區段數上限 | 100 | 軟 | 建議將最多100個區段新增至批次目標資料流。 |
| 每個檔案要激活的最大行數（記錄） | 500萬 | 硬 | Adobe Experience Platform會自動將每個檔案中500萬筆記錄（列）的匯出檔案分割。 每一列代表一個設定檔。 拆分檔案名後附加一個數字，表示該檔案是較大導出的一部分，例如： `filename.csv`, `filename_2.csv`, `filename_3.csv`. 如需詳細資訊，請閱讀 [排程區段](/help/destinations/ui/activate-batch-profile-destinations.md#scheduling) 啟動批次目的地教學課程中的「 」。 |

{style=&quot;table-layout:auto&quot;}

### 臨機啟動 {#ad-hoc-activation}

下面的護欄適用於 [臨機啟動](/help/destinations/api/ad-hoc-activation-api.md) 方法。

| 瓜德拉伊 | 限制 | 限制類型 | 說明 |
| --- | --- | --- | --- |
| 針對臨機啟動工作啟動的區段 | 80 | 硬 | 目前，每個臨機啟動工作最多可啟動80個區段。 嘗試啟動每個作業超過80個區段會導致作業失敗。 此行為在未來版本中可能會有所變更。 |
| 每個區段的同時臨機啟動工作 | 1 | 硬 | 每個區段請勿執行多個同時執行的臨機啟動工作。 |

{style=&quot;table-layout:auto&quot;}

### Edge個人化目的地啟用 {#edge-destinations-activation}

下面的護欄適用於通過 [邊緣個人化目的地](/help/destinations/destination-types.md#streaming-profile-export).

| 瓜德拉伊 | 限制 | 限制類型 | 說明 |
| --- | --- | --- | --- |
| 最大數量 [自訂個人化](/help/destinations/catalog/personalization/custom-personalization.md) 目的地 | 10 | 軟 | 您可以為每個沙箱設定10個自訂個人化目的地的資料流。 |
| 每個沙箱對應至個人化目的地的屬性數上限 | 20 | 硬 | 在資料流中，每個沙箱最多可將20個屬性對應至個人化目的地。 |
| 對應至單一的區段數上限 [Adobe Target](/help/destinations/catalog/personalization/adobe-target-connection.md) 目的地 | 50 | 軟 | 在啟動流程中，您最多可以對單一Adobe Target目的地啟動50個區段。 |

{style=&quot;table-layout:auto&quot;}

### Destination SDK護欄 {#destination-sdk-guardrails}

[Destination SDK](/help/destinations/destination-sdk/overview.md) 是一組設定API，可讓您根據所選的資料和驗證格式，設定目標整合模式，讓Experience Platform將對象和設定檔資料傳送至端點。 下面的護欄會套用至您使用Destination SDK設定的目的地。

| 瓜德拉伊 | 限制 | 限制類型 | 說明 |
| --- | --- | --- | --- |
| 最大數量 [私人自訂目的地](/help/destinations/destination-sdk/overview.md#productized-custom-integrations) | 5 | 軟 | 您可以使用Destination SDK，建立最多5個私人自訂串流或批次目的地。 如果您需要建立5個以上的此類目的地，請聯絡自訂服務代表。 |
| 配置檔案導出策略用於Destination SDK | <ul><li>`maxBatchAgeInSecs` （最少1.800個，最多3.600個）</li><li>`maxNumEventsInBatch` （最少1.000，最多10.000）</li></ul> | 硬 | 使用 [可配置聚合](/help/destinations/destination-sdk/destination-configuration.md#configurable-aggregation) 選項，請留意決定HTTP訊息傳送至API型目的地的頻率以及訊息應包含多少設定檔的最小值和最大值。 |

{style=&quot;table-layout:auto&quot;}

### 目標限制和重試策略 {#destination-throttling-and-retry-policy}

有關指定目的地的限制閾值或限制的詳細資訊。 本節還提供有關目標重試策略的資訊。

| 目的地類型 | 說明 |
| --- | --- |
| 企業目的地(HTTP API、Amazon Kinesis、Azure EventHubs) | 在95%的時間內，Experience Platform會嘗試為成功發送的報文提供少於10分鐘的吞吐量延遲，每個資料流每秒的請求速率小於10,000個。 <br> 如果向您的企業目的地發出失敗請求，Experience Platform會儲存失敗的請求並重試兩次，以將請求傳送至端點。 |

{style=&quot;table-layout:auto&quot;}

## 其他Experience Platform服務的護欄 {#guardrails-other-services}

查看其他Experience Platform服務的護欄資訊：

* 的護欄 [資料擷取](/help/ingestion/guardrails.md)
* 的護欄 [[!DNL Identity Service] 資料](/help/identity-service/guardrails.md)
* 的護欄 [[!DNL Real-time Customer Profile] 資料](/help/profile/guardrails.md)
* 的護欄 [[!DNL Query Service] 資料](/help/query-service/guardrails.md)