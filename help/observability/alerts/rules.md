---
keywords: Experience Platform；首頁；熱門主題；日期範圍
title: 標準警報規則
description: 本文檔涵蓋由Experience Platform提供的預定義警報規則。
feature: Alerts
exl-id: b4af1c15-b1bc-4e4b-a447-09cc17a63988
source-git-commit: 6650894c145fd1f42731fd5ed8aeb6e38062aa61
workflow-type: tm+mt
source-wordcount: '943'
ht-degree: 1%

---

# 標準警報規則

Adobe Experience Platform提供了幾個預定義的警報規則，您可以為組織啟用這些規則。 本文檔介紹這些Adobe提供的警報規則的詳細資訊。 有關Experience Platform中警報的更多一般資訊，請參見 [警報概述](./overview.md)。

當 [查看平台UI中的警報規則](./ui.md)，您可以單獨訂閱每個規則。 訂閱警報時 [I/O事件通知](./subscribe.md)但是，警報規則被組織到不同的訂閱包中。 在下表中，每個規則都顯示其相應的I/O事件訂閱名稱。

## 資料擷取

以下警報規則特定於 [資料接收](../../ingestion/home.md) 和  [來源](../../sources/home.md):

| I/O事件訂閱 | 警報規則 | 說明 |
| --- | --- | --- |
| 源流運行資訊 | 源流運行啟動 | 當源連接開始處理資料時，此警報會觸發。 |
| 源流運行資訊 | 源流運行成功 | 從源連接成功接收資料時，此警報會觸發。 |
| 源流運行延遲、失敗和錯誤 | 源流運行失敗 | 當從源連接接收資料時發生錯誤時，此警報會觸發。 |
| 源流運行延遲、失敗和錯誤 | 攝取延遲 | 當批處理接收流運行超過150分鐘時，此警報會觸發。 |
| 源流運行延遲、失敗和錯誤 | 攝取失敗 | 當失敗記錄與所有記錄的比率超過閾值0.5%時，此警報將觸發。 |

{style="table-layout:auto"}

如果您以前訂閱了以下警報類型，則不再接收警報，因為此警報已被棄用：

| I/O事件訂閱 | 警報規則 | 說明 |
| --- | --- | --- |
| 源流運行延遲、失敗和錯誤 | 缺乏攝取 | 如果接收延遲超過七小時且未向平台接收任何資料，則此警報會向您發送消息。 |

{style="table-layout:auto"}

## 身份識別服務

以下警報規則特定於 [身份服務](../../identity-service/home.md):

| I/O事件訂閱 | 警報規則 | 說明 |
| --- | --- | --- |
| 身份接收資訊 | Identity Service流運行啟動 | 當Identity Service流運行開始處理資料時，此警報會觸發。 換句話說，正在將所攝取的資料從資料湖載入到身份服務。 |
| 身份接收資訊 | Identity Service流運行成功 | 當資料從資料湖成功載入到身份服務時，此警報會觸發。 |
| 身份接收延遲、故障和錯誤 | 身份服務流運行延遲 | 當Identity Service流運行需要超過150分鐘才能處理時，此警報會觸發。 |
| 身份接收延遲、故障和錯誤 | Identity Service流運行失敗 | 將資料插入Identity Service時出錯時，此警報會觸發。 |

{style="table-layout:auto"}

## 即時客戶設定檔

以下警報規則特定於 [即時客戶配置檔案](../../profile/home.md):

| I/O事件訂閱 | 警報規則 | 說明 |
| --- | --- | --- |
| 配置檔案接收資訊 | 配置檔案流運行啟動 | 當配置檔案流運行開始處理資料時，此警報會觸發。 |
| 配置檔案接收資訊 | 配置檔案流運行成功 | 當資料從資料湖成功載入到配置檔案時，此警報會觸發。 |
| 配置檔案接收延遲、故障和錯誤 | 配置檔案流運行延遲 | 將資料從資料湖載入到配置檔案時，此警報將觸發，處理時間超過150分鐘。 |
| 配置檔案接收延遲、故障和錯誤 | 配置檔案流運行失敗 | 將資料插入配置檔案時出錯時，此警報會觸發。 |

{style="table-layout:auto"}

## 區段

以下警報規則特定於 [分段服務](../../segmentation/home.md):

| I/O事件訂閱 | 警報規則 | 說明 |
| --- | --- | --- |
| 段評估作業資訊 | 段任務開始 | 當段評估作業開始處理資料時，此警報會觸發。 |
| 段評估作業資訊 | 段作業成功 | 當段評估作業成功完成時，此警報將觸發。 |
| 段評估作業延遲、失敗和錯誤 | 段任務延遲 | 當段評估作業完成時間超過150分鐘時，此警報會觸發。 <br> 將顯示以下狀態之一： <br> — 觸發 — 已滿足故障或延遲條件（請將其視為活動狀態）。 <br> — 非活動 — 條件未滿足或未解決（請將其視為已解決狀態）。 |
| 段評估作業延遲、失敗和錯誤 | 段作業失敗 | 當段評估作業導致錯誤時，此警報會觸發。 |
| 段評估作業延遲、失敗和錯誤 | 段定義已禁用 | 當因內部錯誤而禁用段定義時，此警報會觸發。 這會自動觸發Adobe工程團隊的戰場，以調查此問題。 此警報僅用於提供資訊，不需要您執行任何操作。 |

{style="table-layout:auto"}

## 目的地

以下警報規則特定於 [目的地](../../destinations/home.md):

| I/O事件訂閱 | 警報規則 | 說明 |
| --- | --- | --- |
| 目標流運行資訊 | 目標流運行開始 | 當目標流運行開始激活段時，此警報會觸發。 |
| 目標流運行資訊 | 目標流運行成功 | 當網段成功激活到目標時，此警報會觸發。 |
| 目標流運行延遲、失敗和錯誤 | 目標流運行延遲 | 當目標流運行激活段所需時間超過150分鐘時，此警報會觸發。 |
| 目標流運行延遲、失敗和錯誤 | 目標流運行失敗 | 當激活到目標的段時發生錯誤時，此警報會觸發。 |
| 目標流運行延遲、失敗和錯誤 | 跳頁率超過閾值 | 當跳過的ID與總ID的比率超過閾值時，此警報會觸發。 |

{style="table-layout:auto"}

## 查詢服務

以下警報規則特定於 [查詢服務](../../query-service/home.md):

| I/O事件訂閱 | 警報規則 | 說明 |
| --- | --- | --- |
| 查詢服務計畫查詢資訊 | 查詢服務計畫查詢啟動 | 當計畫查詢開始運行時，此警報會觸發。 |
| 查詢服務計畫查詢資訊 | 查詢服務計畫查詢成功 | 當計畫查詢作業成功完成時，此警報將觸發。 |
| 查詢服務計畫的查詢延遲、失敗和錯誤 | 查詢服務計畫查詢失敗 | 當計畫查詢作業失敗時，此警報會觸發。 |

<!-- (Definitions to be added once available)
| Segment Job Delay | This alert triggers when a segment job takes longer than 150 minutes to complete. | N/A | 30 seconds | 3 hours |
| No Ingestion Activity in Past 24 Hours | This alert triggers when no new data has been ingested in the last 24-hour period. | N/A | 1 day | 1 day |
| Ingestion Error Rate Exceeded | This alert triggers when the error rate for data ingestion exceeds the allotted threshold. | 20% | 30 seconds | 30 seconds |
| Entitlement Threshold Exceeded | This alert triggers when the number of created profiles exceeds 80% of your organization's entitlement. | 30 seconds | N/A |
| SFTP source has not ingested data | This alert triggers when an [SFTP source](../../sources/connectors/cloud-storage/sftp.md) has not ingested any data within a certain time period. | 1 day | 1 day |
| Feed Message | This alert when an identity sharing feed message has been sent to a user using [Segment Match](../../segmentation/ui/segment-match.md). | N/A | N/A |
| Feed Access Revoked | This alert triggers when another Platform user revokes access to an identity sharing feed using [Segment Match](../../segmentation/ui/segment-match.md). | N/A | N/A |
| Feed Modified | This alert triggers when an identity sharing feed is modified by a user using [Segment Match](../../segmentation/ui/segment-match.md). | N/A | N/A |
| Feed Shared | This alert triggers when a user shares a new feed in [Segment Match](../../segmentation/ui/segment-match.md). | N/A | N/A |
| Link Request | This alert triggers when a user requests to connect for partner sharing. | N/A | N/A |
| Link Action | This alert triggers when a user accepts a request to connect for partner sharing. | N/A | N/A |
-->
