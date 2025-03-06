---
keywords: Experience Platform；查詢；查詢服務；疑難排解；護欄；指引；限制；
title: 查詢服務的護欄
description: 本檔案提供查詢服務資料的使用量限制資訊，以協助您最佳化查詢使用。
exl-id: 1ad5dcf4-d048-49ff-97e3-07040392b65b
source-git-commit: 23c7a4590b365a49edb066567b6ebe2ac08c67e8
workflow-type: tm+mt
source-wordcount: '1168'
ht-degree: 2%

---

# 查詢服務的護欄

護欄是引導資料與系統使用、效能最佳化，以及在Adobe Experience Platform中避免錯誤或意外結果的臨界值。
本檔案提供查詢服務資料的預設使用限制，以協助您在查詢與授權權益相關的資料時最佳化系統效能。

>[!IMPORTANT]
>
>除了此護欄頁面之外，還請檢查銷售訂單中的授權權益以及實際使用限制的對應[產品說明](https://helpx.adobe.com/legal/product-descriptions.html)。

## 先決條件

在繼續本檔案之前，您應該對關鍵的查詢服務定義和功能有良好的瞭解。 其說明如下：

* **隨選查詢**：用於執行`SELECT`個查詢以探索、實驗及驗證資料，其中查詢的結果&#x200B;**未儲存在資料湖上**。

* **批次查詢**：用於執行`INSERT TABLE AS SELECT`和`CREATE TABLE AS SELECT`查詢，以清除、塑形、操縱和擴充資料。 這些查詢的結果&#x200B;**儲存在資料湖上**。 測量此功能耗用的量度是計算時數。

* **查詢服務使用者**：在您目前的Customer Journey Analytics、Adobe Real-Time Customer Data Platform及/或Adobe Journey Optimizer授權內提供的查詢服務使用者，也可以搭配Data Distiller使用。 查詢服務使用者在功能之間共用。

* **臨機操作使用者**：臨機操作使用者是執行臨機操作查詢的使用者。

* **批次使用者**：批次使用者是執行批次查詢的使用者。

* **報表API**：用於進行資料擷取呼叫的API （內部或外部）。 延伸報表資料模型衍生自Adobe Experience Platform中的原生報表資料模型，例如Real-Time CDP儀表板資料模型。

## 護欄型別

本檔案有兩種預設限制：

| 護欄型別 | 說明 |
|----------|---------|
| **效能護欄（軟性限制）** | 效能護欄是與使用案例範圍相關的使用限制。 超過效能護欄時，您可能會遇到效能降低和延遲的問題。 Adobe對這類效能降低不負任何責任。 客戶若持續超過效能護欄，可選擇授權額外的容量，以避免效能降低。 |
| **系統強制的護欄（硬限制）** | Real-Time CDP UI或API會強制執行系統強制的護欄。 這些限制不得超過，因為UI和API會阻止您這樣做或會傳回錯誤。 |

{style="table-layout:auto"}

>[!NOTE]
>
>本檔案中所概述的預設限制會持續改善。 請定期回來檢視更新。

## 主要實體效能護欄

下表提供在使用特定查詢模式時執行查詢的建議護欄限制和說明。

**隨機查詢**

| 護欄 | 限制 | 限制型別 | 說明 |
|---|---|---|---|
| 最長執行時間 | 10 分鐘 | 系統強制的護欄 | 這會定義臨機SQL查詢的最大輸出時間。 超過傳回結果的時間限制會擲回錯誤碼53400。 |
| 並行查詢服務使用者 | <ul><li>如應用程式產品說明中所指定。</li><li>+5 （每多購買一個Ad hoc query使用者附加套件）</li></ul> | 系統強制的護欄 | 這定義了在特定組織中，可同時建立工作階段的使用者數量。 如果超過並行限制，使用者會收到`Session Limit Reached`錯誤。 |
| 查詢並行 | <ul><li>如應用程式產品說明中所指定。</li><li>+1 （每購買一個額外的Ad Hoc Query使用者附加SKU套件）</li></ul> | 系統強制的護欄 | 這定義在特定組織中可同時執行多少個查詢。 如果超過並行限制，查詢會排入佇列。 |
| 使用者端聯結器和結果輸出限制 | 使用者端聯結器<ul><li>查詢UI （100列）</li><li>協力廠商使用者端(50,000)</li><li>[!DNL PostgresSQL]使用者端(50,000)</li></ul> | 系統強制的護欄 | 可透過下列方式接收查詢結果：<ul><li>查詢服務UI</li><li>第三方使用者端</li><li>[!DNL PostgresSQL]使用者端</li></ul>注意：對輸出計數新增限制可能會更快地傳回結果。 例如，`LIMIT 5`、`LIMIT 10`等。 |
| 傳回的結果來自 | 使用者端UI | 不適用 | 這會定義如何將結果提供給使用者。 |

{style="table-layout:auto"}

**批次查詢**

| **護欄** | **限制** | **限制型別** | **說明** |
|---|---|---|---|
| 最長執行時間 | 24 小時 | 系統強制的護欄 | 這會定義批次SQL查詢的最大執行時間。<br>查詢的處理時間取決於要處理的資料量和查詢複雜性。 |
| 未排定批次的並行查詢服務使用者 | <ul><li>如應用程式產品說明中所指定。</li><li>+5 （每多購買一個Ad hoc query使用者附加套件）</li></ul> | 系統強制的護欄 | 對於未排程的批次查詢（例如，互動模式的CTAS/ITAS查詢），這會定義在特定組織中可同時建立工作階段的使用者數量。 如果超過並行限制，使用者會收到`Session Limit Reached`錯誤。 |
| 排定批次的並行查詢服務使用者 | 無使用者限制 | 不適用 | 排程的批次查詢為非同步作業，因此沒有使用者限制。 |
| 批次資料處理的運算時數 | 如客戶的Adobe Experience Platform智慧查詢自訂SKU銷售訂單中所指定 | 效能護欄 | 這定義了每年允許客戶執行批次查詢以掃描、處理和將資料寫回Data Lake的運算時間範圍。 |
| 查詢並行 | 支援 | 不適用 | 排定的批次查詢為非同步作業，因此支援並行查詢。 |
| 使用者端聯結器和結果輸出限制 | 使用者端聯結器<ul><li>查詢UI （列數沒有上限）</li><li>協力廠商使用者端（列數沒有上限）</li><li>[!DNL PostgresSQL]使用者端（資料列沒有上限）</li><li>REST API （列數沒有上限）</li></ul> | 系統強制的護欄 | 可使用下列方法取得查詢的結果：<ul><li>可儲存為衍生資料集</li><li>可以插入現有的衍生資料集中</li></ul>備註：查詢結果的記錄計數沒有上限。 |
| 傳回的結果來自 | 資料集 | 不適用 | 這會定義如何將結果提供給使用者。 |

{style="table-layout:auto"}

## 查詢加速存放區 {#query-accelerated-store}

下表提供建議的護欄限制和查詢加速存放區的說明。

| 護欄 | 限制 | 限制型別 | 說明 |
|---|---|---|---|
| 查詢並行 | 4 | 系統強制的護欄 | 為確保透過報表API彙總資料的查詢(包括增強Real-Time CDP資料模型等資料模型的查詢)擁有有效執行的資源，報表API會透過為每個查詢指派並行時段來追蹤資源使用情況。 系統會將查詢放入佇列並等待併發位置可用或從快取中提供這些查詢。 在任何指定時間最多可同時使用四個查詢位置。<br>如果您透過BI工具存取報告API且需要更多並行存取，則需要BI伺服器。 |

{style="table-layout:auto"}

## 後續步驟

閱讀本檔案後，您應該更瞭解使用可用查詢模式執行查詢的預設限制。

請參閱下列檔案以取得有關查詢服務的詳細資訊：

* [查詢服務API](./api/getting-started.md)
* [查詢服務UI](./ui/overview.md)

請參閱下列檔案，深入瞭解其他Experience Platform服務護欄、端對端延遲資訊，以及Real-Time CDP產品說明檔案的授權資訊：

* [Real-Time CDP護欄](/help/rtcdp/guardrails/overview.md)
* [各種Experience Platform服務的端對端延遲圖表](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/architecture-overview/deployment/guardrails.html?lang=en#end-to-end-latency-diagrams)。
* [Real-Time Customer Data Platform (B2C版本 — Prime和Ultimate套件)](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2c-edition-prime-and-ultimate-packages.html)
* [Real-Time Customer Data Platform (B2P - Prime和Ultimate套件)](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2p-edition-prime-and-ultimate-packages.html)
* [Real-Time Customer Data Platform (B2B - Prime和Ultimate套件)](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2b-edition-prime-and-ultimate-packages.html)