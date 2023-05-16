---
description: Adobe Experience Platform Destination SDK是一組設定API，可讓您設定目的地整合模式，讓Experience Platform根據您選擇的資料和驗證格式，將對象和設定檔資料傳送至端點或儲存位置。 設定會儲存在Experience Platform中，並可透過API擷取以取得其他更新。
title: Adobe Experience Platform Destination SDK
exl-id: 7aca9f40-98c8-47c2-ba88-4308fc2b1798
source-git-commit: 118ff85a9fceb8ee81dbafe2c381d365b813da29
workflow-type: tm+mt
source-wordcount: '854'
ht-degree: 4%

---

# Adobe Experience Platform Destination SDK

Adobe Experience Platform Destination SDK是一組設定API，可讓您設定目的地整合模式，讓Experience Platform根據您選擇的資料和驗證格式，將受眾和設定檔資料傳送至端點或儲存位置。 設定會儲存在Experience Platform中，並可透過API擷取以取得其他更新。

Destination SDK檔案提供相關指示，供您使用Adobe Experience Platform Destination SDK來設定、測試及發行與Adobe Experience Platform的已產品化目的地整合，並讓您的目的地成為不斷增長的目的地目錄的一部分。 透過使用Destination SDK，您也可以建立自己的自訂私人目的地，以匯出量身打造的資料。

![Experience PlatformUI的螢幕擷圖，顯示目的地目錄](assets/destinations-catalog-overview.png)

## 產品化和自訂整合 {#productized-custom-integrations}

>[!IMPORTANT]
>
> 建立私人自訂目的地的功能僅適用於 [Adobe Real-time Customer Data Platform Ultimate](https://helpx.adobe.com/jp/legal/product-descriptions/real-time-customer-data-platform.html) 客戶。

身為Destination SDK合作夥伴，您可以將已分類的目的地新增至 [Experience Platform目錄](../catalog/overview.md):

1. 使用預先設定的參數標準化客戶的整合設定，並簡化客戶的設定體驗。
2. 在Experience Platform目的地目錄中引入品牌目的地卡，以簡化客戶設定和了解。
3. 以產品化目的地整合Adobe Experience Platform與Adobe Real-time Customer Data Platform為特色。

身為Experience Platform客戶，您也可以撰寫自己的私人自訂目的地，以最符合您的啟動需求。

![概述圖表，顯示目的地開發人員如何與Destination SDK互動，以及Real-Time CDP客戶如何從產品化和私人目的地中獲益。](assets/destination-sdk-visual.png)

## 支援的整合類型 {#supported-integration-types}

### 即時（串流）整合 {#real-time-integrations}

透過Destination SDK,Adobe Experience Platform支援與具有REST API端點的目的地即時整合（也稱為串流）。 與Experience Platform的即時整合支援下列功能：

* 消息轉換和聚合
* 設定檔回填
* 可設定的中繼資料整合，以初始化受眾設定和資料傳輸
* 可配置驗證
* 一套測試與驗證API，供您測試和反覆驗證您的目的地設定

### 檔案式整合 {#file-based-integrations}

透過Destination SDK，您也可以設定整合，以定期將檔案匯出至您所選擇的儲存位置。 與Experience Platform的檔案式整合支援下列功能：

* 以數種支援格式匯出檔案(CSV、Parquet、JSON)
* 可配置的檔案格式選項，它允許您根據下游要求構建導出檔案的格式。

請參閱以下主題中目的地端的技術需求： [整合必要條件](integration-prerequisites.md) 文章，並閱讀 [配置選項](functionality/configuration-options.md) 文章

## 存取Destination SDK {#get-access}

Destination SDK存取權會因您身為Real-Time CDPExperience Platform或合作夥伴的狀態而異。 如需詳細資訊，請參閱下表。

| 合作夥伴或客戶的類型 | 如何存取Destination SDK |
---------|----------|
| 獨立軟體供應商(ISV) | 加入 [Adobe技術合作夥伴計畫](https://partners.adobe.com/technologyprogram/experiencecloud.html) 和請求取得布建的Experience Platform沙箱，以存取Destination SDK。 |
| 系統整合商(SI) | 您必須處於 [Adobe解決方案合作夥伴計畫](https://solutionpartners.adobe.com/home.html)，您將會獲得布建的Experience Platform沙箱，以及Destination SDK的存取權。 |
| Experience Platform客戶 [Real-Time CDP Ultimate套件](https://helpx.adobe.com/jp/legal/product-descriptions/real-time-customer-data-platform.html) | 依預設，您可以存取Experience Platform沙箱和Destination SDK，為組織建立私人目的地。 |

{style="table-layout:auto"}

## 高級流程 {#process}

在Experience Platform中設定您目的地的程式概述如下：

1. 如果您是ISV或SI，請參閱 [取得存取權](#get-access) 上節中的資訊。 [Real-Time CDP Ultimate套件](https://helpx.adobe.com/jp/legal/product-descriptions/real-time-customer-data-platform.html) 客戶可以略過此步驟。
2. [請求布建Experience Platform沙箱](https://adobeexchangeec.zendesk.com/hc/en-us/articles/360037457812-Adobe-Experience-Platform-Sandbox-Accounts-Access-Adding-Users-and-Support) 並啟用目標編寫權限。
3. 建立您的整合。 請依照產品檔案中的指示進行設定 [串流目的地](guides/configure-destination-instructions.md) 或 [檔案型目的地](guides/configure-file-based-destination-instructions.md).
4. 測試您的整合。 請依照產品檔案中的指示進行測試 [串流目的地](testing-api/streaming-destinations/streaming-destination-testing-overview.md) 或 [檔案型目的地](testing-api/batch-destinations/file-based-destination-testing-overview.md).
5. 如果您是ISV或SI建立 [產品化整合](./overview.md#productized-custom-integrations), [提交整合](guides/submit-destination.md) 供Adobe檢閱（標準回應時間為五個工作天）。
6. 如果您是ISV或SI建立產品化整合，請使用 [自助服務檔案程式](docs-framework/documentation-instructions.md) 若要在Experience League上建立目的地的產品檔案頁面。
7. 針對產品化整合，一旦Adobe核准，您的整合會顯示在 [Experience Platform目錄](../catalog/overview.md).
8. 如果您想要更新整合，請遵循相同的程式。

## 參考 {#reference}

Adobe建議您閱讀並了解下列Experience Platform檔案：

* [Adobe Experience Platform目的地概觀](https://experienceleague.adobe.com/docs/experience-platform/destinations/home.html?lang=en)
* [XDM架構組合的基礎](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/composition.html?lang=zh-Hant)
* [身分命名空間概觀](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=en)
