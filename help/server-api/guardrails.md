---
title: Edge Network伺服器API的效能護欄
description: 瞭解如何在最佳效能護欄內使用伺服器API。
exl-id: 063d0fbb-26d1-4727-9dea-8e7223b2173d
source-git-commit: 3bf13c3f5ac0506ac88effc56ff68758deb5f566
workflow-type: tm+mt
source-wordcount: '508'
ht-degree: 2%

---


# Edge Network伺服器API的效能護欄

## 概觀 {#overview}

效能護欄會定義與伺服器API使用案例相關的使用量限制。 超過本文所述的效能護欄可能會導致效能降低。

Adobe對超過使用量限制所造成的效能降低不負責任。 持續超過效能護欄的客戶可請求額外的處理容量，以避免效能降低。

## 定義

* **可用性** 每個五分鐘間隔的計算方式為Experience PlatformEdge Network所處理之未因錯誤而失敗且僅與布建的Edge Network API相關的要求的百分比。 如果租使用者未在指定的五分鐘間隔內提出任何請求，則該間隔會視為100%可用。
* **每月連續運作時間百分比** 特定區域的計算方式為每月所有五分鐘間隔的可用性平均值。
* 一個 **上游** 是Edge Network背後的服務，可針對特定資料流啟用，例如Adobe伺服器端轉送、Adobe Edge Segmentation或Adobe Target。
* A **請求單位** 對應至8 KB的請求片段，以及針對資料流設定的一個上游。
* A **請求** 是客戶擁有的應用程式傳送給的單一訊息 [!DNL Server API]. 請求可包含一或多個請求單位。
* 一個 **錯誤** 是任何因邊緣網路而失敗的要求 [內部服務錯誤](error-handling.md).

## 服務限制

所有資料串流都會強制執行某些使用量限制，其主要功能是控制可同時傳送多少事件、其大小，以及這些要求路由至的上游服務數目。

### 請求單位

所有限制都會套用並標準化 **請求單位(RU)**，定義為 **8 KB片段** 請求傳送到資料流中設定的一個上游服務。

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
* [端對端延遲圖](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/architecture-overview/deployment/guardrails.html?lang=en#end-to-end-latency-diagrams) 用於各種Experience Platform服務。
* [Real-time Customer Data Platform （B2C版本 — Prime和Ultimate套件）](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2c-edition-prime-and-ultimate-packages.html)
* [Real-time Customer Data Platform （B2P - Prime和Ultimate套件）](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2p-edition-prime-and-ultimate-packages.html)
* [Real-time Customer Data Platform （B2B - Prime和Ultimate套件）](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2b-edition-prime-and-ultimate-packages.html)
