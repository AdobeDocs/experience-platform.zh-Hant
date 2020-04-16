---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Analytics資料連接器
topic: overview
translation-type: tm+mt
source-git-commit: 9f0200af0310eafbcc1851b089cfc254cb34af8f

---


# Analytics資料連接器

Adobe Experience Platform可讓您透過Analytics資料連接器(ADC)來內嵌Adobe Analytics資料。 ADC將Adobe Analytics收集的資料即時串流至Platform，將SCDS格式的Analytics資料轉換為Experience Data Model(XDM)欄位，供Platform使用。

本檔案提供Adobe Analytics的概觀，並說明Analytics資料的使用案例。

## Adobe Analytics與Analytics資料

Adobe Analytics是一款功能強大的引擎，可協助您進一步瞭解客戶、客戶與網頁屬性的互動方式、瞭解數位行銷支出的成效，並找出改善的方面。 Adobe Analytics每年處理數兆筆Web交易，而ADC可讓您在幾分鐘內輕鬆利用此豐富的行為資料，豐富即時客戶個人檔案。

![](./images/analytics-data-experience-platform.png)

Adobe Analytics從高層次上收集來自全球不同數位通道和多個資料中心的資料。 收集資料後，會套用訪客識別、分段與轉換架構(VISTA)規則和處理規則來塑造傳入資料的形狀。 在原始資料經過此輕量型處理後，即時客戶個人檔案會視為可供使用。 在與上述程式平行的過程中，相同的處理資料被微批處理並吸收到平台資料集中，以供資料科學工作區、查詢服務和其他資料發現應用程式使用。

如需VISTA和處理規則的詳細資訊，請參閱下列檔案：
* [VISTA規則概觀](https://marketing.adobe.com/resources/help/en_US/reference/VISTA.html)
* [處理規則概觀](https://docs.adobe.com/content/help/zh-Hant/analytics/admin/admin-tools/processing-rules/processing-rules.html)

## 體驗資料模型(XDM)

XDM是公開記載的規格，可為應用程式提供通用結構和定義，以便與Adobe Experience Platform上的服務通訊。

遵守XDM標準可讓資料統一整合，讓資料傳送和收集資訊變得更輕鬆。

若要進一步瞭解XDM，請參閱 [XDM系統概觀](../../../xdm/home.md)。

## 如何將欄位從Adobe Analytics對應至XDM?

當建立來源連線以使用平台使用者介面將Analytics資料帶入Experience Platform時，資料欄位會在數分鐘內自動對應並收錄至即時客戶個人檔案。 如需使用平台UI建立Adobe Analytics來源連線的指示，請參閱 [Analytics資料連接器教學課程](https://www.adobe.io/apis/experienceplatform/home/tutorials/sources-ui-tutorials.html#!api-specification/markdown/narrative/tutorials/sources_tutorial/ui/adobe-applications/adobe-analytics-ui-tutorial.md)。

如需Analytics與Experience Platform之間發生之欄位對應的詳細資訊，請造訪 [Adobe Analytics欄位對應指南](./analytics-mapping.md) 。

## 平台上的Analytics資料預期延遲為何？

| Analytics 資料 | 預期延遲 |
| -------------- | ---------------- |
| 即時客戶個人檔案的新資料(未啟 **用** A4T) | &lt; 2 分鐘 |
| 即時客戶個人檔案的新資料(啟 **用** A4T) | &lt; 15 分鐘 |
| 資料湖的新資料 | &lt; 45 分鐘 |
| 回填資料（13個月的資料或100億個事件，以較低者為準） | &lt; 4週 |

>[!NOTE] 延遲會視客戶配置、資料量和消費性應用程式而有所不同。 例如，如果Analytics實作設定了「管 `A4T` 線」的延遲，則會增加至5-10分鐘。