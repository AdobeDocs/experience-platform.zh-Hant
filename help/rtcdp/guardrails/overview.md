---
title: Real-Time CDP護欄
description: 瞭解Real-Time CDP各種服務和領域的資料護欄。
source-git-commit: ab2bb6f4cafe60aec7d8745cca9d2f7f0227a938
workflow-type: tm+mt
source-wordcount: '389'
ht-degree: 3%

---

# Real-Time CDP護欄

護欄是臨界值，可為Real-Time CDP中的資料和系統使用、效能最佳化，以及避免錯誤或意外結果提供指引。 護欄可指您與授權權益相關的資料使用或消費與處理。

從這裡開始，然後按照下面的連結來瞭解Real-Time CDP各種服務和區域的所有護欄：

* [資料擷取的護欄](/help/ingestion/guardrails.md)
* [的護欄 [!DNL Edge Network Server API]](/help/server-api/guardrails.md)
* [護欄 [!DNL Real-Time Customer Profile] 資料與細分](/help/profile/guardrails.md)
* [護欄 [!DNL Identity Service] 資料](/help/identity-service/guardrails.md)
* [護欄 [!DNL Query Service]](/help/query-service/guardrails.md)
* [透過目的地啟用資料的護欄](/help/destinations/guardrails.md)

>[!TIP]
>
>此外，另請參閱 [此頁面](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/architecture-overview/deployment/guardrails.html) 以取得其他Experience Platform應用程式(例如 [Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer.html?lang=zh-Hant) 和 [Customer Journey Analytics](https://experienceleague.adobe.com/docs/customer-journey-analytics.html)、和 [端對端延遲圖](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/architecture-overview/deployment/guardrails.html?lang=en#end-to-end-latency-diagrams) 用於各種Experience Platform服務。

## 護欄型別 {#guardrail-types}

請注意，橫跨所有Real-Time CDP區域與服務的兩種護欄型別為：

| 護欄型別 | 說明 |
|----------|---------|
| **效能護欄（軟性限制）** | 效能護欄是與使用案例範圍相關的使用限制。 超過效能護欄時，您可能會遇到效能降低和延遲的問題。 Adobe對這類效能降級概不負責。 客戶若持續超過效能護欄，可選擇授權額外的容量，以避免效能降低。 |
| **系統強制的護欄（硬限制）** | Real-Time CDP UI或API會強制執行系統強制的護欄。 這些限制不得超過，因為UI和API會阻止您這樣做或會傳回錯誤。 |

{style="table-layout:auto"}

## Real-Time CDP授權和權益資訊 {#product-descriptions}

此外，請參考以下產品說明連結，以取得根據您購買的Real-Time CDP版本和層級而設計的授權和權益資訊：

* [所有Adobe產品說明](https://helpx.adobe.com/legal/product-descriptions.html)
* [Real-time Customer Data Platform （B2C版本 — Prime和Ultimate套件）](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2c-edition-prime-and-ultimate-packages.html)
* [Real-time Customer Data Platform （B2P - Prime和Ultimate套件）](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2p-edition-prime-and-ultimate-packages.html)
* [Real-time Customer Data Platform （B2B - Prime和Ultimate套件）](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2b-edition-prime-and-ultimate-packages.html)

## 後續步驟

瞭解適用於Real-Time CDP各種區域和服務的「護欄」後，您可以遵循這些護欄，同時使用 [Real-Time CDP實作的範例使用案例](/help/rtcdp/get-started.md).
