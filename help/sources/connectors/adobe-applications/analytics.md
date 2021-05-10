---
keywords: Experience Platform;home；熱門主題；Analytics Source Connector;analytics;Analytics
solution: Experience Platform
title: Adobe Analytics報表套裝資料的來源連接器
topic-legacy: overview
description: 本檔案提供Analytics的概觀，並說明Analytics資料的使用案例。
exl-id: c4887784-be12-40d4-83bf-94b31eccdc2e
translation-type: tm+mt
source-git-commit: af5ad975bbfd6a67fe66c90e33da1365d49c8899
workflow-type: tm+mt
source-wordcount: '513'
ht-degree: 3%

---

# Adobe Analytics報表套裝資料的來源連接器

Adobe Experience Platform可讓您透過Analytics來源連接器擷取Adobe Analytics資料。 [!DNL Analytics]源連接器將[!DNL Analytics]收集到的資料即時流到平台，將SCDS格式的[!DNL Analytics]資料轉換為[!DNL Experience Data Model](XDM)欄位供平台使用。

本文檔概述[!DNL Analytics]並說明[!DNL Analytics]資料的使用案例。

## Adobe Analytics與分析資料

[!DNL Analytics] 是一款功能強大的引擎，可協助您進一步瞭解客戶、客戶與Web屬性的互動方式、瞭解數位行銷支出的成效，並找出改善的方面。[!DNL Analytics] 每年處理數兆筆Web交易，而來 [!DNL Analytics] 源連接器可讓您輕鬆利用這項豐富的行為資料，在幾分鐘 [!DNL Real-time Customer Profile] 內豐富交易內容。

![](./images/analytics-data-experience-platform.png)

從高度來看，[!DNL Analytics]會收集來自全球不同數位通道和多個資料中心的資料。 收集資料後，會套用訪客識別、分段與轉換架構(VISTA)規則和處理規則來塑造傳入資料的形狀。 在原始資料經過此輕量型處理後，[!DNL Real-time Customer Profile]會視為可供使用。 在與上述過程平行的過程中，相同的處理資料被微批處理並被吸收到平台資料集中，以供[!DNL Data Science Workspace]、[!DNL Query Service]和其他資料發現應用程式使用。

如需處理規則的詳細資訊，請參閱[處理規則概觀](https://docs.adobe.com/content/help/zh-Hant/analytics/admin/admin-tools/processing-rules/processing-rules.html)。

## 體驗資料模型(XDM)

XDM是公開記載的規格，為應用程式提供通用結構和定義，以便與Experience Platform上的服務通訊。

遵守XDM標準可讓資料統一整合，讓資料傳送和收集資訊變得更輕鬆。

要瞭解有關XDM的更多資訊，請參閱[XDM系統概述](../../../xdm/home.md)。

## 從Adobe Analytics到XDM的欄位如何對應？

當建立來源連線以使用平台使用者介面將[!DNL Analytics]資料匯入Experience Platform時，資料欄位會在幾分鐘內自動映射並匯入至[!DNL Real-time Customer Profile]。 有關使用平台UI建立與[!DNL Analytics]源連接的說明，請參閱[Analytics源連接器教程](../../tutorials/ui/create/adobe-applications/analytics.md)。

有關[!DNL Analytics]和Experience Platform之間的欄位映射的詳細資訊，請參閱[Adobe Analytics欄位映射指南。](./mapping/analytics.md)

## 平台上的Analytics資料預期延遲為何？

| Analytics 資料 | 預期延遲 |
| -------------- | ---------------- |
| 新資料至[!DNL Real-time Customer Profile]（A4T **未啟用**） | &lt; 2 分鐘 |
| 新資料至[!DNL Real-time Customer Profile]（A4T **已啟用**） | &lt; 15 分鐘 |
| 資料湖的新資料 | &lt; 90 分鐘 |
| 回填資料（13個月的資料或100億個事件，以較低者為準） | &lt; 4 週 |

>[!NOTE]
>
>延遲會視客戶配置、資料量和消費性應用程式而有所不同。 例如，如果[!DNL Analytics]實作設定為`A4T`，則到Pipeline的延遲將增加到5-10分鐘。

## [!DNL Analytics]資料中的主要識別碼

來自[!DNL Analytics]來源連接器的每次點擊都包含主要識別碼，此識別碼取決於ECID或AAID是否存在。 如果有ECID，則ECID會指定為主要識別碼。 如果有AAID，則AAID被指定為主AID。
