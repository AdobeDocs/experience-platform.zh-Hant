---
title: Edge Network伺服器API的效能護欄
description: 瞭解如何在最佳效能護欄內使用伺服器API。
exl-id: 063d0fbb-26d1-4727-9dea-8e7223b2173d
source-git-commit: 6414168c1deb047af30d8636ef8d61316f56aecf
workflow-type: tm+mt
source-wordcount: '569'
ht-degree: 2%

---


# Edge Network伺服器API的效能護欄

## 概觀 {#overview}

效能護欄會定義與伺服器API使用案例相關的使用量限制。 超過本文所述的效能護欄可能會導致效能降低。

Adobe對超過使用量限制所造成的效能降低不負責任。 持續超過效能護欄的客戶可請求額外的處理容量，以避免效能降低。

>[!IMPORTANT]
>
>除了此護欄頁面之外，還請檢查銷售訂單中的授權權益以及實際使用限制的對應[產品說明](https://helpx.adobe.com/legal/product-descriptions.html)。

本頁中說明的所有效能護欄皆適用於IMS組織層級。 對於已設定多個IMS組織的使用者，每個組織個別而言皆須受下方效能護欄的約束。 請參閱[Experience Platform字彙表](../landing/glossary.md)，以取得有關[!DNL IMS Organizations]的詳細資料。

## 定義

* **可用性**&#x200B;是按照每個五分鐘間隔計算的，作為Experience PlatformEdge Network處理的要求百分比，這些要求不會因錯誤而失敗，且僅與布建的Edge NetworkAPI有關。 如果租使用者未在指定的五分鐘間隔內提出任何請求，則該間隔會視為100%可用。
* 指定區域的&#x200B;**每月連續運作時間百分比**&#x200B;是以每個月所有五分鐘間隔的可用性平均值計算。
* **上游**&#x200B;是Edge Network背後的服務，可針對特定資料流啟用，例如Adobe伺服器端轉送、Adobe Edge Segmentation或Adobe Target。
* **請求單位**&#x200B;對應至請求的8 KB片段，以及針對資料流設定的上游片段。
* **要求**&#x200B;是客戶擁有的應用程式傳送給[!DNL Server API]的單一訊息。 請求可包含一或多個請求單位。
* **錯誤**&#x200B;是指任何因Edge Network[內部服務錯誤](error-handling.md)而失敗的要求。

## 服務限制

所有資料串流都會強制執行某些使用量限制，其主要功能是控制可同時傳送多少事件、其大小，以及這些要求路由至的上游服務數目。

### 請求單位

所有限制皆會套用並正規化至&#x200B;**要求單位(RU)**，定義為&#x200B;**8 KB片段**，其要求會傳送到資料流中設定的上游服務。

#### 範例

| 根據資料流設定的上游 | 平均請求大小 | 請求單位 |
| --- | --- | --- |
| 1 (Adobe平台) | 8 KB （1個片段） | 1 |
| 2 (Adobe平台、Adobe Target) | 8 KB （1個片段） | 2 |
| 2 (Adobe平台、Adobe Target) | 16 KB （2個片段） | 4 |
| 2 (Adobe平台、Adobe Target) | 64 KB （8個片段） | 16 |

### 要求單位限制

下表顯示預設限制值。 如果您需要更高的請求單位限制，請聯絡您的客戶代表。

| 端點 | 每秒要求單位數 |
| --- | --- |
| `/v2/interact` | 4000 |
| `/v2/collect` | 6000 |

### HTTP要求大小限制

| 裝載格式 | 請求的大小上限 | 最多8 KB請求片段 |
| --- | --- | --- |
| JSON純文字 | 64 KB | 8 |


>[!NOTE]
>
>根據裝載本身，二進位格式通常較壓縮達20-40%，可讓您推送的資料多於純文字JSON的資料。 如果您需要更高的資料串流容量，請聯絡客戶服務代表。

## 後續步驟

請參閱下列檔案，深入瞭解其他Experience Platform服務護欄、端對端延遲資訊，以及Real-Time CDP產品說明檔案的授權資訊：

* [Real-Time CDP護欄](/help/rtcdp/guardrails/overview.md)
* [各種Experience Platform服務的端對端延遲圖表](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/architecture-overview/deployment/guardrails.html?lang=en#end-to-end-latency-diagrams)。
* [Real-time Customer Data Platform （B2C Edition - Prime與Ultimate套件）](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2c-edition-prime-and-ultimate-packages.html)
* [Real-time Customer Data Platform （B2P - Prime與Ultimate套件）](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2p-edition-prime-and-ultimate-packages.html)
* [Real-time Customer Data Platform （B2B - Prime與Ultimate套件）](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2b-edition-prime-and-ultimate-packages.html)
