---
description: Adobe Experience Platform Destination SDK是一組設定API，可讓您根據所選的資料和驗證格式，設定目標整合模式，讓Experience Platform將對象和設定檔資料傳送至端點。 設定會儲存在Experience Platform中，並可透過API擷取以取得其他更新。
title: Adobe Experience Platform Destination SDK
exl-id: 7aca9f40-98c8-47c2-ba88-4308fc2b1798
source-git-commit: af8718f7d5351993c5e4aa00822ed7d2b290b9f0
workflow-type: tm+mt
source-wordcount: '708'
ht-degree: 3%

---

# Adobe Experience Platform Destination SDK

## 總覽 {#destinations-sdk}

Adobe Experience Platform Destination SDK是一組設定API，可讓您根據所選的資料和驗證格式，設定目標整合模式，讓Experience Platform將對象和設定檔資料傳送至端點。 設定會儲存在Experience Platform中，並可透過API擷取以取得其他更新。

Destination SDK檔案提供相關指示，供您使用Adobe Experience Platform Destination SDK來設定、測試及發行與Adobe Experience Platform的已產品化目的地整合，並讓您的目的地成為不斷增長的目的地目錄的一部分。

![目的地目錄概觀](./assets/destinations-catalog-overview.png)

## 產品化和自訂整合 {#productized-custom-integrations}

身為Destination SDK合作夥伴，您可以將已分類的目的地新增至 [Experience Platform目錄](/help/destinations/catalog/overview.md):
1. 使用預先設定的參數標準化客戶的整合設定，並簡化客戶的設定體驗。
2. 在Experience Platform目的地目錄中引入品牌目的地卡，以簡化客戶設定和了解。
3. 以產品化目的地整合Adobe Experience Platform與Real-time Customer Data Platform為特色。

身為Experience Platform客戶，您可以撰寫自己的私人自訂目的地，最符合您的啟動需求。

![Destination SDK視覺圖](./assets/destination-sdk-visual.png)

<!--

## Types of destinations in Adobe Experience Platform {#types-of-destinations}

In Adobe Experience Platform, we distinguish between two destination types - *connections* and *extensions*. In the user interface, customers can choose between two types of connection destinations, Profile Export destinations and Segment Export destinations. For more details around the difference between the different destination types, read [Destination Types and Categories](https://experienceleague.adobe.com/docs/experience-platform/destinations/destination-types.html?lang=en).

![Destination types](./assets/types-of-destinations.png)

This documentation set provides you with all the necessary information to add your destination to Adobe Experience Platform, as a *connection*, either Profile Export or Segment Export. To set up an extension, visit the [Experience Platform Launch developer portal](https://developer.adobelaunch.com/extensions/).

-->

## 支援的整合類型 {#supported-integration-types}

透過Destination SDK,Adobe Experience Platform支援與具有REST API端點的目的地即時整合。 與Experience Platform的即時整合支援下列功能：
* 消息轉換和聚合
* 設定檔回填
* 可設定的中繼資料整合，以初始化受眾設定和資料傳輸
* 可配置驗證
* 一套測試與驗證API，供您測試和反覆驗證您的目的地設定

請參閱以下主題中目的地端的技術需求： [整合必要條件](./integration-prerequisites.md) 文章。

## 存取Destination SDK {#get-access}

Destination SDK存取權會因您身為Real-Time CDPExperience Platform或合作夥伴的狀態而異。 如需詳細資訊，請參閱下表。


| 合作夥伴或客戶的類型 | 如何存取Destination SDK |
---------|----------|
| 獨立軟體供應商(ISV) | 加入 [Adobe交換計畫](https://partners.adobe.com/exchangeprogram/experiencecloud.html) 和請求取得布建的Experience Platform沙箱，以存取Destination SDK。 |
| 系統整合商(SI) | 您必須處於 [Adobe解決方案合作夥伴計畫](https://solutionpartners.adobe.com/home.html)，您將會獲得布建的Experience Platform沙箱，以及Destination SDK的存取權。 |
| Experience Platform客戶 [Real-Time CDP Ultimate套件](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform.html) | 依預設，您可以存取Experience Platform沙箱和Destination SDK，為組織建立私人目的地。 |

{style=&quot;table-layout:auto&quot;}

## 高級流程 {#process}

在Experience Platform中設定您目的地的程式概述如下：

1. 如果您是ISV或SI，請參閱上節中的獲取訪問資訊。 [Adobe Experience Platform Activation](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-platform0.html) 客戶可以略過此步驟。
2. [請求布建Experience Platform沙箱](https://adobeexchangeec.zendesk.com/hc/en-us/articles/360037457812-Adobe-Experience-Platform-Sandbox-Accounts-Access-Adding-Users-and-Support) 並啟用目標編寫權限。
3. 建立您的整合。 請依照產品檔案中的指示進行設定 [串流目的地](./configure-destination-instructions.md) 或 [檔案型目的地（測試版）](./configure-file-based-destination-instructions.md).
4. 測試您的整合。 請依照產品檔案中的指示進行測試 [串流目的地](./test-destination.md) 或 [檔案型目的地（測試版）](./file-based-destination-testing-overview.md).
5. 如果您是ISV或SI建立 [產品化整合](./overview.md#productized-custom-integrations), [提交整合](./submit-destination.md) 供Adobe檢閱（標準回應時間為五個工作天）。
6. 如果您是ISV或SI建立產品化整合，請使用 [自助服務檔案程式](./docs-framework/documentation-instructions.md) 若要在Experience League上建立目的地的產品檔案頁面。
7. 針對產品化整合，一旦Adobe核准，您的整合會顯示在 [Experience Platform目錄](/help/destinations/catalog/overview.md).
8. 如果您想要更新整合，請遵循相同的程式。

## 參考 {#reference}

Adobe建議您閱讀並了解下列Experience Platform檔案：

* [Adobe Experience Platform目的地概觀](https://experienceleague.adobe.com/docs/experience-platform/destinations/home.html?lang=en)
* [XDM架構組合的基礎](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/composition.html?lang=zh-Hant)
* [身分命名空間概觀](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=en)
