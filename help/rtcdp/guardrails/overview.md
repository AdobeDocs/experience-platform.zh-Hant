---
title: Real-Time CDP護欄
description: 瞭解Real-Time CDP各種服務和領域的資料護欄。
feature: Guardrails, Data Management, Data Ingestion, Data Export
exl-id: 377499b4-5707-4d50-94e3-02f88ad5bf2c
source-git-commit: 5d6b70e397a252e037589c3200053ebcb7eb8291
workflow-type: tm+mt
source-wordcount: '392'
ht-degree: 1%

---

# Real-Time CDP護欄

護欄是臨界值，可為Real-Time CDP中的資料和系統使用、效能最佳化，以及避免錯誤或意外結果提供指引。 護欄可指您與授權權益相關的資料使用或消費與處理。

>[!IMPORTANT]
>
>檢查您的銷售訂單中的授權權利以及對應的 [產品說明](https://helpx.adobe.com/legal/product-descriptions.html) 除了此護欄頁面之外，還受到實際使用量限制。

從這裡開始，然後按照下面的連結來瞭解Real-Time CDP各種服務和區域的所有護欄：

* [資料擷取的護欄](/help/ingestion/guardrails.md)
* [的護欄 [!DNL Edge Network Server API]](/help/server-api/guardrails.md)
* [護欄 [!DNL Real-Time Customer Profile] 資料與細分](/help/profile/guardrails.md)
* [護欄 [!DNL Identity Service] 資料](/help/identity-service/guardrails.md)
* [護欄 [!DNL Query Service]](/help/query-service/guardrails.md)
* [透過目的地啟用資料的護欄](/help/destinations/guardrails.md)
* [Real-Time CDP B2B的護欄](/help/rtcdp/b2b-guardrails.md)

>[!TIP]
>
>此外，造訪 [數位體驗藍圖](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/architecture-overview/deployment/guardrails.html) 以取得進一步資訊，例如 [端對端延遲圖](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/architecture-overview/deployment/guardrails.html?lang=en#end-to-end-latency-diagrams) 用於各種Experience Platform服務。

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
* [Real-time Customer Data Platform （B2P版本 — Prime和Ultimate套件）](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2p-edition-prime-and-ultimate-packages.html)
* [Real-time Customer Data Platform （B2B版本 — Prime和Ultimate套件）](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2b-edition-prime-and-ultimate-packages.html)

## 其他Experience Platform應用程式的護欄  {#guardrails-other-aep-apps}

其他Experience Platform應用程式也有類似的護欄。 如需詳細資訊，請造訪下列連結：

* [Adobe Journey Optimizer護欄](https://experienceleague.adobe.com/docs/journey-optimizer/using/get-started/guardrails.html?lang=en)
* [Customer Journey Analytics護欄](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-admin/guardrails.html)

## 後續步驟

瞭解適用於Real-Time CDP各種區域和服務的「護欄」後，您可以遵循這些護欄，同時使用 [Real-Time CDP實作的範例使用案例](/help/rtcdp/get-started.md).
