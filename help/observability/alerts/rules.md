---
keywords: Experience Platform；首頁；熱門主題；日期範圍
title: 標準警報規則
description: 本檔案涵蓋由Experience Platform提供的預先定義警報規則。
feature: Alerts
exl-id: b4af1c15-b1bc-4e4b-a447-09cc17a63988
source-git-commit: 6650894c145fd1f42731fd5ed8aeb6e38062aa61
workflow-type: tm+mt
source-wordcount: '943'
ht-degree: 1%

---

# 標準警報規則

Adobe Experience Platform提供數個預先定義的警報規則，您可為組織啟用。 本檔案涵蓋這些Adobe提供之警報規則的詳細資訊。 如需Experience Platform中警報的更一般資訊，請參閱 [警報概觀](./overview.md).

當 [在平台UI中檢視警報規則](./ui.md)，您可以個別訂閱每個規則。 訂閱警報時透過 [I/O事件通知](./subscribe.md)不過，警報規則會組織成不同的訂閱套件。 在下表中，每個規則都顯示其對應的I/O事件訂閱名稱。

## 資料擷取

以下是 [資料擷取](../../ingestion/home.md) 和  [來源](../../sources/home.md):

| I/O事件訂閱 | 警報規則 | 說明 |
| --- | --- | --- |
| 源流運行資訊 | 源流運行開始 | 當來源連線開始處理資料時，就會觸發此警報。 |
| 源流運行資訊 | 源流運行成功 | 從來源連線成功擷取資料時，就會觸發此警報。 |
| 源流運行延遲、故障和錯誤 | 源流運行失敗 | 從來源連線擷取資料時發生錯誤時，就會觸發此警報。 |
| 源流運行延遲、故障和錯誤 | 擷取延遲 | 批次內嵌流程執行需要超過150分鐘的時間來處理，就會觸發此警報。 |
| 源流運行延遲、故障和錯誤 | 擷取失敗 | 當失敗記錄與所有記錄的比率超過0.5%的臨界值時，就會觸發此警報。 |

{style="table-layout:auto"}

如果您先前已訂閱下列警報類型，您將不會再收到警報，因為此警報已淘汰：

| I/O事件訂閱 | 警報規則 | 說明 |
| --- | --- | --- |
| 源流運行延遲、故障和錯誤 | 缺乏擷取 | 如果擷取延遲超過七小時，且未將任何資料擷取至Platform，此警報會傳送訊息給您。 |

{style="table-layout:auto"}

## 身份識別服務

以下是 [Identity服務](../../identity-service/home.md):

| I/O事件訂閱 | 警報規則 | 說明 |
| --- | --- | --- |
| 身分擷取資訊 | 身份服務流運行開始 | 當Identity Service流程執行開始處理資料時，就會觸發此警報。 換言之，擷取的資料正從Data Lake載入Identity Service。 |
| 身分擷取資訊 | 身份服務流運行成功 | 當資料從資料湖成功載入Identity Service時，就會觸發此警報。 |
| 身份獲取延遲、失敗和錯誤 | 身份服務流運行延遲 | 當Identity Service流程執行需要超過150分鐘的時間來處理時，就會觸發此警報。 |
| 身份獲取延遲、失敗和錯誤 | 身份服務流運行失敗 | 將資料擷取至Identity Service時發生錯誤時，就會觸發此警報。 |

{style="table-layout:auto"}

## 即時客戶設定檔

以下是 [即時客戶個人檔案](../../profile/home.md):

| I/O事件訂閱 | 警報規則 | 說明 |
| --- | --- | --- |
| 設定檔擷取資訊 | 配置檔案流運行開始 | 設定檔流程執行開始處理資料時，就會觸發此警報。 |
| 設定檔擷取資訊 | 設定檔流程執行成功 | 資料從資料湖成功載入設定檔時，就會觸發此警報。 |
| 設定檔擷取延遲、失敗和錯誤 | 設定檔流程執行延遲 | 將資料從資料湖載入設定檔時，系統會觸發此警報，處理時間超過150分鐘。 |
| 設定檔擷取延遲、失敗和錯誤 | 配置檔案流運行失敗 | 將資料擷取至設定檔時發生錯誤時，就會觸發此警報。 |

{style="table-layout:auto"}

## 區段

以下是 [區段服務](../../segmentation/home.md):

| I/O事件訂閱 | 警報規則 | 說明 |
| --- | --- | --- |
| 區段評估作業資訊 | 區段作業開始 | 區段評估工作開始處理資料時，就會觸發此警報。 |
| 區段評估作業資訊 | 區段工作成功 | 區段評估作業成功完成時，就會觸發此警報。 |
| 區段評估作業延遲、失敗和錯誤 | 區段工作延遲 | 當區段評估工作完成時間超過150分鐘時，就會觸發此警報。 <br> 會出現下列其中一種狀態： <br> — 觸發 — 已滿足故障或延遲的條件（請將其視為活動狀態）。 <br> — 非作用中 — 條件未達到或未解決（請將其視為已解決狀態）。 |
| 區段評估作業延遲、失敗和錯誤 | 區段作業失敗 | 當區段評估工作導致錯誤時，就會觸發此警報。 |
| 區段評估作業延遲、失敗和錯誤 | 區段定義已停用 | 當區段定義因內部錯誤而停用時，就會觸發此警報。 這會自動觸發Adobe工程團隊的戰場，以調查問題。 此警報僅供參考，不需要您採取任何動作。 |

{style="table-layout:auto"}

## 目的地

以下是 [目的地](../../destinations/home.md):

| I/O事件訂閱 | 警報規則 | 說明 |
| --- | --- | --- |
| 目標流運行資訊 | 目標流運行開始 | 目的地流程執行開始啟用區段時，就會觸發此警報。 |
| 目標流運行資訊 | 目標流運行成功 | 區段成功啟動至目的地時，就會觸發此警報。 |
| 目標流運行延遲、故障和錯誤 | 目標流運行延遲 | 目的地流程執行需要超過150分鐘才啟動區段時，就會觸發此警報。 |
| 目標流運行延遲、故障和錯誤 | 目標流運行失敗 | 在啟動目的地區段時發生錯誤時，就會觸發此警報。 |
| 目標流運行延遲、故障和錯誤 | 跳過頁面速率超過臨界值 | 跳過的ID與總ID的比率超過臨界值時，就會觸發此警報。 |

{style="table-layout:auto"}

## 查詢服務

以下是 [查詢服務](../../query-service/home.md):

| I/O事件訂閱 | 警報規則 | 說明 |
| --- | --- | --- |
| 查詢服務計畫查詢資訊 | 查詢服務計畫查詢開始 | 排程查詢開始執行時，就會觸發此警報。 |
| 查詢服務計畫查詢資訊 | 查詢服務計畫查詢成功 | 排程查詢作業成功完成時，就會觸發此警報。 |
| 查詢服務計畫的查詢延遲、失敗和錯誤 | 查詢服務計畫查詢失敗 | 排程查詢作業失敗時，就會觸發此警報。 |

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
