---
description: Adobe Experience Platform目標SDK是一組設定API，可讓您設定目標整合模式，讓Experience Platform根據您選擇的資料和驗證格式，將對象和設定檔資料傳送至端點。 設定會儲存在Experience Platform中，並可透過API擷取以取得其他更新。
title: Adobe Experience Platform目的地SDK
exl-id: 7aca9f40-98c8-47c2-ba88-4308fc2b1798
source-git-commit: bd65cfa557fb42d23022578b98bc5482e8bd50b1
workflow-type: tm+mt
source-wordcount: '702'
ht-degree: 2%

---

# Adobe Experience Platform目的地SDK

## 概覽 {#destinations-sdk}

Adobe Experience Platform目的地SDK是一組設定API，可讓您設定目的地整合模式，讓Experience Platform根據您選擇的資料和驗證格式，將對象和設定檔資料傳送至端點。 設定會儲存在Experience Platform中，並可透過API擷取以取得其他更新。

目的地SDK檔案提供相關指示，供您使用Adobe Experience Platform目的地SDK來設定、測試及發行與Adobe Experience Platform的已產品化目的地整合，並讓您的目的地成為不斷增長的目的地目錄的一部分。

![目的地目錄概觀](./assets/destinations-catalog-overview.png)

## 產品化和自訂整合 {#productized-custom-integrations}

作為目的地SDK合作夥伴，您可以將已產品化的目的地新增至[Experience Platform目錄](/help/destinations/catalog/overview.md)，讓您受益：
1. 使用預先設定的參數標準化客戶的整合設定，並簡化客戶的設定體驗。
2. 在Experience Platform目的地目錄中引入品牌目的地卡，以簡化客戶設定和了解。
3. 可作為與Adobe Experience Platform和即時客戶資料平台的產品化目的地整合。

身為Experience Platform客戶，您可以撰寫自己的私人自訂目的地，最符合您的啟動需求。

![目的地SDK視覺化圖表](./assets/destination-sdk-visual.png)

<!--

## Types of destinations in Adobe Experience Platform {#types-of-destinations}

In Adobe Experience Platform, we distinguish between two destination types - *connections* and *extensions*. In the user interface, customers can choose between two types of connection destinations, Profile Export destinations and Segment Export destinations. For more details around the difference between the different destination types, read [Destination Types and Categories](https://experienceleague.adobe.com/docs/experience-platform/destinations/destination-types.html?lang=en).

![Destination types](./assets/types-of-destinations.png)

This documentation set provides you with all the necessary information to add your destination to Adobe Experience Platform, as a *connection*, either Profile Export or Segment Export. To set up an extension, visit the [Experience Platform Launch developer portal](https://developer.adobelaunch.com/extensions/).

-->

## 支援的整合類型 {#supported-integration-types}

透過目的地SDK,Adobe Experience Platform支援與具有REST API端點的目的地即時整合。 與Experience Platform的即時整合支援下列功能：
* 消息轉換和聚合
* 設定檔回填
* 可設定的中繼資料整合，以初始化受眾設定和資料傳輸
* 可配置驗證
* 一套測試與驗證API，供您測試和反覆驗證您的目的地設定

閱讀[整合必要條件](./integration-prerequisites.md)文章中目的地端的技術需求。


## 存取目的地SDK {#get-access}

目的地SDK的存取權會因您身為合作夥伴或Experience Platform客戶的狀態而異。 如需詳細資訊，請參閱下表。


| 合作夥伴或客戶的類型 | 如何存取目的地SDK |
---------|----------|
| 獨立軟體供應商(ISV) | 加入[AdobeExchange程式](https://partners.adobe.com/exchangeprogram/experiencecloud.html)並請求取得布建的Experience Platform沙箱以存取目的地SDK。 |
| 系統整合商(SI) | 您必須處於[Adobe解決方案合作夥伴計畫](https://solutionpartners.adobe.com/home.html)的金級或白金級，且您將會獲得布建的Experience Platform沙箱，並可存取目的地SDK。 |
| Experience Platform[激活包](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-platform0.html)上的客戶 | 依預設，您可存取Experience Platform沙箱和目的地SDK。 |
| Experience Platform[Real-time CDP包上的客戶](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform.html) | 您無權存取目的地SDK，但可存取其他使用目的地SDK的公司所設定並發佈至Experience Platform組織的所有已產品化目的地。 |

{style=&quot;table-layout:auto&quot;}

## 高級流程 {#process}

在Experience Platform中設定您目的地的程式概述如下：

1. 如果您是ISV或SI，請參閱上節中的獲取訪問資訊。 [Adobe Experience Platform ](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-platform0.html) Activation客戶可以略過此步驟。
2. [請求布建Experience Platform沙](https://adobeexchangeec.zendesk.com/hc/en-us/articles/360037457812-Adobe-Experience-Platform-Sandbox-Accounts-Access-Adding-Users-and-Support) 箱並啟用目標編寫權限。
3. [依照產品](./configure-destination-instructions.md) 檔案建立整合。
4. [在產品檔](./test-destination.md) 案之後測試您的整合。
5. [提交您](./destination-publish-api.md) 的整合以供Adobe審核（標準回應時間為5個工作天）。
6. 如果您是ISV或SI建立[產品化整合](./overview.md#productized-custom-integrations)，請使用[自助文檔流程](./docs-framework/documentation-instructions.md)建立目標Experience League的產品文檔頁。
7. Adobe核准後，您的整合會顯示在[Experience Platform目錄](/help/destinations/catalog/overview.md)中。
8. 如果您想要更新整合，請遵循相同的程式。

## 參考 {#reference}

Adobe建議您閱讀並了解下列Experience Platform檔案：

* [Adobe Experience Platform目的地概觀](https://experienceleague.adobe.com/docs/experience-platform/destinations/home.html?lang=en)
* [XDM架構組合的基礎](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/composition.html?lang=en)
* [身分命名空間概觀](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=en)
