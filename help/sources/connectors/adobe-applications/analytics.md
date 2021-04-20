---
keywords: Experience Platform；首頁；熱門主題；Analytics資料連接器；分析；Analytics
solution: Experience Platform
title: Adobe Analytics報表套裝資料的來源連接器
topic: overview
description: 本檔案提供Analytics的概觀，並說明Analytics資料的使用案例。
translation-type: tm+mt
source-git-commit: 126b3d1cf6d47da73c6ab045825424cf6f99e5ac
workflow-type: tm+mt
source-wordcount: '504'
ht-degree: 3%

---


# Adobe Analytics報表套裝資料的連接器

Adobe Experience Platform可讓您透過Analytics資料連接器(ADC)來內嵌Adobe Analytics資料。 ADC將由[!DNL Analytics]收集的資料即時流化到[!DNL Platform]，將SCDS格式的[!DNL Analytics]資料轉換為[!DNL Experience Data Model](XDM)欄位，供[!DNL Platform]使用。

本文檔概述[!DNL Analytics]並說明[!DNL Analytics]資料的使用案例。

## Adobe Analytics與分析資料

[!DNL Analytics] 是一個強大的引擎，可協助您進一步瞭解客戶、客戶與Web屬性的互動方式、瞭解數位行銷支出的成效，並找出改善的方面。[!DNL Analytics] 每年處理數萬億筆Web交易，而ADC可讓您輕鬆利用這些豐富的行為資料，在幾分鐘內 [!DNL Real-time Customer Profile] 就豐富其內容。

![](./images/analytics-data-experience-platform.png)

從高度來看，[!DNL Analytics]會收集來自全球不同數位通道和多個資料中心的資料。 收集資料後，會套用訪客識別、分段與轉換架構(VISTA)規則和處理規則來塑造傳入資料的形狀。 在原始資料經過此輕量型處理後，[!DNL Real-time Customer Profile]會視為可供使用。 在與上述過程平行的過程中，相同的處理資料被微批處理並被吸收到平台資料集中，以供[!DNL Data Science Workspace]、[!DNL Query Service]和其他資料發現應用程式使用。

如需處理規則的詳細資訊，請參閱[處理規則概觀](https://docs.adobe.com/content/help/zh-Hant/analytics/admin/admin-tools/processing-rules/processing-rules.html)。

## 體驗資料模型(XDM)

XDM是公開記載的規格，提供應用程式與[!DNL Experience Platform]上的服務通訊的通用結構和定義。

遵守XDM標準可讓資料統一整合，讓資料傳送和收集資訊變得更輕鬆。

要瞭解有關XDM的更多資訊，請參閱[XDM系統概述](../../../xdm/home.md)。

## 從Adobe Analytics到XDM的欄位如何對應？

當建立源連接以使用[!DNL Platform]用戶介面將[!DNL Analytics]資料導入[!DNL Experience Platform]時，資料欄位將自動映射並在幾分鐘內被導入[!DNL Real-time Customer Profile]。 有關使用[!DNL Platform] UI建立與[!DNL Analytics]源連接的說明，請參閱[Analytics資料連接器教學課程](../../tutorials/ui/create/adobe-applications/analytics.md)。

有關[!DNL Analytics]和[!DNL Experience Platform]之間的欄位映射的詳細資訊，請訪問[Adobe Analytics欄位映射](./mapping/analytics.md)指南。

## 平台上的Analytics資料預期延遲為何？

| Analytics 資料 | 預期延遲 |
| -------------- | ---------------- |
| 新資料至[!DNL Real-time Customer Profile]（A4T **未啟用**） | &lt; 2 分鐘 |
| 新資料至[!DNL Real-time Customer Profile]（A4T **已啟用**） | &lt; 15 分鐘 |
| 資料湖的新資料 | &lt; 90 分鐘 |
| 回填資料（13個月的資料或100億個事件，以較低者為準） | &lt; 4 週 |

>[!NOTE]
>
>延遲會視客戶配置、資料量和消費性應用程式而有所不同。 例如，如果Analytics實作設定了`A4T`，則Pipeline的延遲將增加為5-10分鐘。

## Analytics資料中的主要識別碼

來自Analytics資料連接器的每次點擊都包含主要識別碼，此識別碼取決於ECID或AAID是否存在。 如果有ECID，則ECID會指定為主要識別碼。 如果有AAID，則AAID被指定為主AID。