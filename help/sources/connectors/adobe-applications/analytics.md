---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Analytics資料連接器
topic: overview
translation-type: tm+mt
source-git-commit: 662ca170b7416dfb55cfb6b8cbaef640c1f83d31
workflow-type: tm+mt
source-wordcount: '471'
ht-degree: 3%

---


# Analytics資料連接器

Adobe Experience Platform可讓您透過Analytics資料連接器(ADC)來內嵌Adobe Analytics資料。 ADC將所收集的數 [!DNL Analytics] 據流 [!DNL Platform] 即時化，將SCDS格式化的數 [!DNL Analytics] 據轉換為 [!DNL Experience Data Model] (XDM)欄位供用戶使用 [!DNL Platform]。

本檔案提供資料的概 [!DNL Analytics] 述，並說明資料的使用 [!DNL Analytics] 案例。

## Adobe Analytics與Analytics資料

[!DNL Analytics] 是一個強大的引擎，可協助您進一步瞭解客戶、客戶與Web屬性的互動方式、瞭解數位行銷支出的成效，並找出改善的方面。 [!DNL Analytics] 每年處理數以萬億計的Web交易，而ADC可讓您輕鬆利用這項豐富的行為資料，在幾分鐘內 [!DNL Real-time Customer Profile] 就豐富其內容。

![](./images/analytics-data-experience-platform.png)

從高層次上，收集 [!DNL Analytics] 來自全球不同數位通道和多個資料中心的資料。 收集資料後，會套用訪客識別、分段與轉換架構(VISTA)規則和處理規則，以塑造傳入資料的形狀。 在原始資料經過此輕量型處理後，就會視為可供使用 [!DNL Real-time Customer Profile]。 在與上述過程平行的過程中，相同的處理資料被微批處理並被吸收到Platform資料集中，以便由 [!DNL Data Science Workspace]、 [!DNL Query Service]和其他資料發現應用程式使用。

如需處 [理規則的詳細資訊](https://docs.adobe.com/content/help/zh-Hant/analytics/admin/admin-tools/processing-rules/processing-rules.html) ，請參閱處理規則概觀。

## 體驗資料模型(XDM)

XDM是公開記載的規格，為應用程式提供通用結構和定義，以便與上的服務通訊 [!DNL Experience Platform]。

遵守XDM標準可讓資料統一整合，讓資料傳送和收集資訊變得更輕鬆。

若要進一步瞭解XDM，請參閱 [XDM系統概觀](../../../xdm/home.md)。

## 如何將欄位從Adobe Analytics對應至XDM?

當建立來源連線以使用使用者介 [!DNL Analytics] 面將資 [!DNL Experience Platform] 料匯入 [!DNL Platform] 時，資料欄位會在幾分鐘內自動映射及 [!DNL Real-time Customer Profile] 吸收。 如需使用UI建立來源連線的 [!DNL Analytics] 指示 [!DNL Platform] ，請參閱 [Analytics資料連接器教學課程](../../tutorials/ui/create/adobe-applications/analytics.md)。

如需和之間發生之欄位對應的詳細資 [!DNL Analytics] 訊 [!DNL Experience Platform]，請造訪 [Adobe Analytics欄位對應指南](./mapping/analytics.md) 。

## 平台上的Analytics資料預期延遲為何？

| Analytics 資料 | 預期延遲 |
| -------------- | ---------------- |
| 新資料 [!DNL Real-time Customer Profile] 至(未啟 **用** A4T) | &lt; 2 分鐘 |
| 新資料 [!DNL Real-time Customer Profile] 至(A4T **已啟用** ) | &lt; 15 分鐘 |
| 資料湖的新資料 | &lt; 45 分鐘 |
| 回填資料（13個月的資料或100億個事件，以較低者為準） | &lt; 4 週 |

>[!NOTE] 延遲會視客戶配置、資料量和消費性應用程式而有所不同。 例如，如果Analytics實作設定了「管 `A4T` 線」的延遲，則會增加至5-10分鐘。

## Analytics資料中的主要識別碼

來自Analytics資料連接器的每次點擊都包含主要識別碼，此識別碼取決於ECID或AAID是否存在。 如果有ECID，則ECID會指定為主要識別碼。 如果有AAID，則AAID被指定為主AID。