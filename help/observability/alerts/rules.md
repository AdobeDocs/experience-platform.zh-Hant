---
keywords: Experience Platform；首頁；熱門主題；日期範圍
title: 標準警報規則
description: 本檔案涵蓋由Experience Platform提供的預先定義警報規則。
feature: Alerts
exl-id: b4af1c15-b1bc-4e4b-a447-09cc17a63988
source-git-commit: d82487f34c0879ed27ac55e42d70346f45806131
workflow-type: tm+mt
source-wordcount: '148'
ht-degree: 12%

---

# 標準警報規則

Adobe Experience Platform提供數個預先定義的警報規則，您可為組織啟用。 下表涵蓋這些Adobe提供之警報規則的詳細資訊。 如需Experience Platform中警報的更一般資訊，請參閱[警報概述](./overview.md)。

| 規則 | 說明 | 評估頻率 | 重複窗口 |
| --- | --- | --- | --- |
| 源流運行成功 | 從來源連線成功擷取資料時，就會觸發此警報。 | 不適用 | 不適用 |
| 源流運行失敗 | 從來源連線擷取資料時發生錯誤時，就會觸發此警報。 | 不適用 | 不適用 |
| 區段工作延遲 | 當區段作業完成時間超過150分鐘時，就會觸發此警報。 | 30秒 | 3 小時 |
| 區段定義已停用 | 區段定義停用時，就會觸發此警報。 | 不適用 | 不適用 |

{style=&quot;table-layout:auto&quot;}

<!-- (Definitions to be added once available)
| Entitlement Threshold Exceeded | This alert triggers when the number of created profiles exceeds 80% of your organization's entitlement. | 30 seconds | N/A |
| No ingestion activity in past 24 hours | This alert triggers when no new data has been ingested in the last 24-hour period. | 1 day | 1 day |
| SFTP source has not ingested data | This alert triggers when an [SFTP source](../../sources/connectors/cloud-storage/sftp.md) has not ingested any data within a certain time period. | 1 day | 1 day |
| Ingestion error rate exceeded | This alert triggers when the error rate for data ingestion exceeds 20%. | 30 seconds | 30 seconds |
| Feed Message | This alert when an identity sharing feed message has been sent to a user using [Segment Match](../../segmentation/ui/segment-match.md). | N/A | N/A |
| Feed Access Revoked | This alert triggers when another Platform user revokes access to an identity sharing feed using [Segment Match](../../segmentation/ui/segment-match.md). | N/A | N/A |
| Feed Modified | This alert triggers when an identity sharing feed is modified by a user using [Segment Match](../../segmentation/ui/segment-match.md). | N/A | N/A |
| Feed Shared | This alert triggers when a user shares a new feed in [Segment Match](../../segmentation/ui/segment-match.md). | N/A | N/A |
| Link Request | This alert triggers when a user requests to connect for partner sharing. | N/A | N/A |
| Link Action | This alert triggers when a user accepts a request to connect for partner sharing. | N/A | N/A |
-->
