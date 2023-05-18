---
keywords: Experience Platform；資料控管；customer ai；熱門主題
solution: Experience Platform
feature: Customer AI
title: Customer AI中的資料控管
description: Adobe Experience Platform提供數種服務和工具，讓您放心地控制收集的體驗資料，以符合您的業務實務、法律義務和開發程式。
exl-id: de0836a4-7bc2-4f9c-95a9-c01dd9e2b03f
source-git-commit: 0fcdb358882fba7f7923e5d6fc1a947699276e18
workflow-type: tm+mt
source-wordcount: '302'
ht-degree: 9%

---

# Customer AI與資料控管

Customer AI中任何與資料控管相關的設定皆繼承自Adobe Experience Platform。

## 資料治理 {#governance}

Customer AI與Adobe Experience Platform資料控管之間的整合，可讓您透過Platform在資料的整個歷程中控制並理解資料。 這包括維護資料質量、資料處理、資料編目等。

在Platform使用的資料集上建立的資料使用量標籤和原則，可在Customer AI設定工作流程中呈現。 這些標籤會停止或警告使用已標籤欄位的使用者。

此整合允許您更高效地管理法規遵從性。 在您組織中的資料監管員可以設定限制使用的原則。因此，您可以使用符合資料管理員所定義原則的資料。 請參閱 [標籤和原則](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-dataviews/data-governance.html) 了解更多。

## 同意政策 {#consent-policy}

Customer AI會遵守您的同意偏好設定。 一旦您 [設定並啟用您的同意政策](https://experienceleague.adobe.com/docs/experience-platform/data-governance/policies/user-guide.html?lang=zh-Hant#consent-policy)，客戶AI會遵守從您收集的同意資料。 只有同意的資料才會用於在後續的模型執行中對模型進行計分。 新分數將取代舊分數，且可用於細分。 此功能目前僅適用於HealthCare Shield客戶，以及Privacy and Security Shield客戶。

您可以在此處深入了解此功能：

[Customer AI快速入門](../../customer-ai/getting-started.md)
[Adobe Experience Platform和應用程式](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/architecture-overview/platform-applications.html)
[Adobe Experience Cloud架構圖](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/architecture-overview/experience-cloud.html)
