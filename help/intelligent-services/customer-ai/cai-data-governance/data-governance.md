---
keywords: Experience Platform；資料治理；客戶ai；熱門主題
solution: Experience Platform
feature: Customer AI
title: 客戶AI中的資料治理
description: Adobe Experience Platform提供了多種服務和工具，讓您能夠放心地控制收集的體驗資料，以便遵守您的業務實踐、法律義務和開發流程。
exl-id: de0836a4-7bc2-4f9c-95a9-c01dd9e2b03f
source-git-commit: 0fcdb358882fba7f7923e5d6fc1a947699276e18
workflow-type: tm+mt
source-wordcount: '302'
ht-degree: 9%

---

# 客戶AI和資料治理

客戶AI中與資料治理相關的任何設定都繼承自Adobe Experience Platform。

## 資料治理 {#governance}

客戶AI與Adobe Experience Platform資料治理的整合使您能夠在整個平台過程中控制和理解您的資料。 這包括維護資料質量、資料沿襲、資料編目等。

在平台使用的資料集上建立的資料使用標籤和策略可以在客戶AI配置工作流中顯示。 這些標籤會停止或警告使用已標籤欄位的用戶。

此整合使您能夠更高效地管理法規遵從性。 在您組織中的資料監管員可以設定限制使用的原則。因此，您可以使用符合資料管理員定義的策略的資料。 閱讀有關 [標籤和策略](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-dataviews/data-governance.html) 來瞭解更多資訊。

## 同意策略 {#consent-policy}

客戶AI尊重您的同意偏好。 一旦你 [設定並啟用您的同意策略](https://experienceleague.adobe.com/docs/experience-platform/data-governance/policies/user-guide.html?lang=zh-Hant#consent-policy)，客戶AI將執行從您收集的同意資料。 在模型的後續運行中，只使用同意的資料對模型進行評分。 新分數將取代舊分數，可用於分詞。 此功能目前僅適用於HealthCare Shield客戶和Privacy and Security Shield客戶。

您可以在此處瞭解有關此功能的更多資訊：

[客戶AI入門](../../customer-ai/getting-started.md)
[Adobe Experience Platform和應用程式](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/architecture-overview/platform-applications.html)
[Adobe Experience Cloud體系結構圖](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/architecture-overview/experience-cloud.html)
