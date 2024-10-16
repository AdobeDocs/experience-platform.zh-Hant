---
keywords: Experience Platform；疑難排解；護欄；指南；
title: 資料擷取的護欄
description: 瞭解Adobe Experience Platform中資料擷取的護欄。
exl-id: f07751cb-f9d3-49ab-bda6-8e6fec59c337
source-git-commit: b8f64793b7f869e50c33ead3a5f02f3a8af51ff4
workflow-type: tm+mt
source-wordcount: '810'
ht-degree: 0%

---

# 資料擷取的護欄

>[!IMPORTANT]
>
>批次和串流擷取的護欄會在組織層級進行計算，而不是沙箱層級。 這表示您的每個沙箱資料使用量都會與對應至您整個組織的授權使用量權利總數繫結。 此外，開發沙箱中的資料使用量限製為您的設定檔總數的10%。 如需授權使用權益的詳細資訊，請閱讀[資料管理最佳實務指南](../landing/license-usage-and-guardrails/data-management-best-practices.md)。

護欄是臨界值，可為Adobe Experience Platform中的資料和系統使用、效能最佳化，以及避免錯誤或意外結果提供指引。 護欄可指您與授權權益相關的資料使用或消費與處理。

>[!IMPORTANT]
>
>除了此護欄頁面之外，還請檢查銷售訂單中的授權權益以及實際使用限制的對應[產品說明](https://helpx.adobe.com/legal/product-descriptions.html)。

本文提供Adobe Experience Platform中資料擷取護欄的相關指示。

## 批次擷取的護欄

下表概述使用[批次擷取API](./batch-ingestion/overview.md)或來源時應考慮的護欄：

| 擷取型別 | 准則 | 附註 |
| --- | --- | --- |
| 使用批次擷取API擷取資料湖 | <ul><li>您可以使用批次擷取API，每小時可擷取最多20 GB的資料至Data Lake。</li><li>每個批次的最大檔案數為1500。</li><li>最大批次大小為100 GB。</li><li>每列的屬性或欄位數上限為10000。</li><li>每分鐘每個使用者的批次數量上限為2000。</li></ul> | |
| 使用批次來源擷取資料湖 | <ul><li>您可以使用批次擷取來源（例如[!DNL Azure Blob]、[!DNL Amazon S3]和[!DNL SFTP]），每小時最多可擷取200 GB的資料至資料湖。</li><li>批次大小應介於256 MB和100 GB之間。 這同時適用於未壓縮和壓縮的資料。 若在資料湖中解壓縮壓縮壓縮的資料，將套用這些限制。</li><li>每個批次的最大檔案數為1500。</li><li>檔案或資料夾的最小大小為1個位元組。 您無法擷取0位元組大小的檔案或資料夾。</li></ul> | 請閱讀[來源概觀](../sources/home.md)，瞭解您可以用於資料擷取的來源目錄。 |
| 批次內嵌至設定檔 | <ul><li>記錄類別的大小上限為100 KB （硬式）。</li><li>ExperienceEvent類別的大小上限為10 KB （硬式）。</li></ul> | |
| 每天擷取的設定檔或ExperienceEvent批次數量 | **每天擷取的Profile或ExperienceEvent批次數量上限為90。**&#x200B;這表示每天擷取的Profile和ExperienceEvent批次總數不能超過90。 擷取其他批次將會影響系統效能。 | 這是軟性限制。 雖然可能會超過軟性限制，但軟性限制提供系統效能的建議指引。 |
| 加密的資料擷取 | 支援的單一加密檔案大小上限為1 GB。 例如，雖然您可以在單一資料流執行中擷取2GB以上的資料，但資料流執行中的個別檔案都不能超過1GB。 | 擷取加密資料的處理程式可能會比一般資料擷取需要更長的時間。 如需詳細資訊，請參閱[加密資料擷取API指南](../sources/tutorials/api/encrypt-data.md)。 |
| 更新插入批次擷取 | 更新插入批次的擷取速度最多可比一般批次慢10倍，因此，您應&#x200B;**將您的更新插入批次保留在200萬筆記錄下**，以確保有效率的執行階段，並避免封鎖其他批次在沙箱中處理。 | 雖然您毫無疑問可以擷取超過200萬筆記錄的批次，但由於小型沙箱的限制，您的擷取時間將會大幅延長。 |

{style="table-layout:auto"}

## 串流擷取的護欄

閱讀[串流擷取總覽](./streaming-ingestion/overview.md)，瞭解串流擷取的護欄資訊。

## 串流來源的護欄

下表概述使用串流來源時應考慮的護欄：

| 擷取型別 | 准則 | 附註 |
| --- | --- | --- |
| 串流來源 | <ul><li>最大記錄大小為1 MB，建議大小為10 KB。</li><li>擷取至資料湖時，串流來源支援每秒有4000到5000個請求。 除了現有的來源連線外，這同時適用於新建立的來源連線。 **注意**：串流資料最多可能需要30分鐘才能完全處理至資料湖。</li><li>串流來源在將資料擷取至設定檔或串流細分時，支援每秒最多1500個請求。</li></ul> | 串流來源（例如[!DNL Kafka]、[!DNL Azure Event Hubs]和[!DNL Amazon Kinesis]）不使用[!DNL Data Collection Core Service] (DCCS)路由，而且可能有不同的輸送量限制。 如需您可以用於資料擷取的來源目錄，請參閱[來源概觀](../sources/home.md)。 |

{style="table-layout:auto"}

## 後續步驟

請參閱下列檔案，深入瞭解其他Experience Platform服務護欄、端對端延遲資訊，以及Real-Time CDP產品說明檔案的授權資訊：

* [Real-Time CDP護欄](/help/rtcdp/guardrails/overview.md)
* [各種Experience Platform服務的端對端延遲圖表](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/architecture-overview/deployment/guardrails.html?lang=en#end-to-end-latency-diagrams)。
* [Real-time Customer Data Platform （B2C Edition - Prime與Ultimate套件）](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2c-edition-prime-and-ultimate-packages.html)
* [Real-time Customer Data Platform （B2P - Prime與Ultimate套件）](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2p-edition-prime-and-ultimate-packages.html)
* [Real-time Customer Data Platform （B2B - Prime與Ultimate套件）](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2b-edition-prime-and-ultimate-packages.html)
