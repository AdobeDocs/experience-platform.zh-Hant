---
description: Adobe Experience Platform Destination SDK是一組設定API，可讓您根據您選擇的資料和驗證格式，設定用於Experience Platform的目的地整合模式，以將對象和設定檔資料傳送至您的端點或儲存位置。 設定儲存在Experience Platform中，並可透過API擷取以取得其他更新。
title: Adobe Experience Platform Destination SDK
exl-id: 7aca9f40-98c8-47c2-ba88-4308fc2b1798
source-git-commit: 9c59f6edd51c61c1fe2ff69e0adea49e6efb8745
workflow-type: tm+mt
source-wordcount: '1012'
ht-degree: 0%

---

# Adobe Experience Platform Destination SDK

Adobe Experience Platform Destination SDK是一套設定API，可讓您根據您選擇的資料和驗證格式，設定用於Experience Platform的目的地整合模式，以將對象和設定檔資料傳送至您的端點或儲存位置。 設定儲存在Experience Platform中，並可透過API擷取以取得其他更新。

Destination SDK檔案會提供指示，讓您使用Adobe Experience Platform Destination SDK來設定、測試和發行與Adobe Experience Platform的生產化目的地整合，並讓您的目的地成為不斷成長的目的地目錄的一部分。 透過使用Destination SDK，您也可以建立自己的自訂私人目的地，以匯出符合您需求的資料。

![Experience PlatformUI的熒幕擷圖，顯示目的地目錄。](assets/destinations-catalog-overview.png)

## 快速入門 — 探索基本資訊 {#quick-start}

請檢閱下列連結中的檔案，以快速開始透過Destination SDK設定和提交您的目的地。

>[!BEGINSHADEBOX]

<table style="border: 0;">
  <tbody>
    <tr>
        <td>
            <p><b>設定頁面</b></p>
            <ul>
                <li><a href="/help/destinations/destination-sdk/functionality/configuration-options.md">說明所有組態選項</a></li>
                <li> 目的地伺服器組態 — <a href="/help/destinations/destination-sdk/functionality/destination-server/server-specs.md">伺服器規格</a>和<a href="/help/destinations/destination-sdk/functionality/destination-server/templating-specs.md">範本規格</a></li>
                <li><a href="/help/destinations/destination-sdk/functionality/destination-configuration/customer-data-fields.md">客戶資料欄位和其他目的地設定元件</a></li>
                <li><a href="https://experienceleague.adobe.com/en/docs/experience-platform/destinations/destination-sdk/functionality/destination-server/message-format">範本化和巨集</a></li>
            </ul>
        </td>
        <td>
            <p><b>指南</b></p>
            <ul>
                <li><a href="/help/destinations/destination-sdk/overview.md#process">高階整合程式</a></li>
                <li><a href="/help/destinations/destination-sdk/guides/configure-destination-instructions.md">設定串流目的地</a></li>
                <li><a href="/help/destinations/destination-sdk/guides/configure-file-based-destination-instructions.md">設定以檔案為基礎的目的地</a></li>
                <li><a href="/help/destinations/destination-sdk/guides/batch/configure-prospect-audience-destination.md">設定匯出潛在客戶設定檔的目的地</a></li>
                <li><a href="/help/destinations/destination-sdk/guides/submit-destination.md">提交目的地以進行發佈</a></li>
            </ul>
        </td>
                <td>
            <p><b>API參考</b></p>
            <ul>
                <li><a href="https://developer.adobe.com/experience-platform-apis/references/destination-authoring/#tag/Destination-servers-and-templates">目的地伺服器端點API參考</a></li>
                <li><a href="https://developer.adobe.com/experience-platform-apis/references/destination-authoring/#tag/Destination-configurations">目的地端點API參考</a></li>
                <li><a href="https://developer.adobe.com/experience-platform-apis/references/destination-authoring/#tag/Audience-metadata-templates">對象中繼資料API參考</a></li>
                <li><a href="https://developer.adobe.com/experience-platform-apis/references/destination-authoring/#tag/Destination-testing">測試API參考</a></li>
                <li><a href="https://developer.adobe.com/experience-platform-apis/references/destination-authoring/#tag/Destination-publishing">Destination publishing API參考</a></li>
            </ul>
        </td>
    </tr>
  </tbody>
</table>

<table style="border: 0;">
  <tbody>
    <tr>
        <td>
            <p><b>設定串流目的地 — 速查表</b></p>
            <ul>
                <li><a href="/help/destinations/destination-sdk/guides/configure-destination-instructions.md">設定串流目的地的端對端指南</a></li>
                <li><a href="/help/destinations/destination-sdk/functionality/destination-server/message-format.md">透過Pebble範本瞭解資料轉換</a>和<a href="/help/destinations/destination-sdk/functionality/destination-server/supported-functions.md">檢視支援的範本功能</a></li>
                <li><a href="/help/destinations/destination-sdk/functionality/destination-configuration/aggregation-policy.md">瞭解資料彙總原則</a></li>
                <li><a href="https://experienceleague.adobe.com/en/docs/experience-platform/destinations/destination-sdk/functionality/destination-server/message-format">即時設定範例</a></li>
                <li><a href="/help/destinations/destination-sdk/testing-api/streaming-destinations/streaming-destination-testing-overview.md">測試您的串流目的地</a></li>
            </ul>
        </td>
        <td>
            <p><b>設定以檔案為基礎的目的地 — 速查表</b></p>
            <ul>
                <li><a href="/help/destinations/destination-sdk/guides/configure-file-based-destination-instructions.md">設定以檔案為基礎的目的地端對端指南</a></li>
                <li><a href="/help/destinations/destination-sdk/guides/batch/configure-file-formatting-options.md">設定匯出檔案的檔案格式</a></li>
                <li><a href="/help/destinations/destination-sdk/guides/batch/configure-amazon-s3-destination-with-predefined-file-formatting.md">Amazon S3目的地的即時設定範例</a></li>
                <li>檔案匯出排程和檔案命名的<a href="/help/destinations/destination-sdk/functionality/destination-configuration/batch-configuration.md">批次組態</a></li>
                <li><a href="/help/destinations/destination-sdk/testing-api/batch-destinations/file-based-destination-testing-overview.md">測試以檔案為基礎的目的地</a></li>
            </ul>
        </td>
        <td>
            <p><b>其他重要資訊</b></p>
            <ul>
                <li><a href="/help/destinations/destination-sdk/getting-started.md#obtain-authentication-credentials">取得使用API所需的驗證認證</a></li>
                <li><a href="/help/destinations/destination-sdk/integration-prerequisites.md">整合必要條件</a></li>
                <li><a href="/help/destinations/destination-sdk/glossary.md">Destination SDK辭彙表</a></li>                
                <li><a href="/help/destinations/destination-sdk/functionality/rate-limiting-retry-policy.md">速率限制和重試原則</a></li>
                <li><a href="/help/destinations/destination-sdk/docs-framework/self-service-template.md">記錄您的目的地的自助服務範本</a></li>
            </ul>
        </td>
    </tr>
  </tbody>
</table>


>[!ENDSHADEBOX]

## 產品化和自訂整合 {#productized-custom-integrations}

>[!IMPORTANT]
>
> 僅[Adobe Real-time Customer Data Platform Ultimate](https://helpx.adobe.com/jp/legal/product-descriptions/real-time-customer-data-platform.html)客戶可使用這項建立私人自訂目的地的功能。

作為Destination SDK合作夥伴，您可以將產品化的目的地新增至[Experience Platform目錄](../catalog/overview.md)，從中受益：

1. 透過預先設定的引數標準化跨客戶的整合設定，並簡化客戶的設定體驗。
2. 在Experience Platform目的地目錄中推出品牌目的地卡，以簡化客戶設定和認知作業。
3. 成為與Adobe Experience Platform和Adobe Real-time Customer Data Platform整合的生產化目的地。

身為Experience Platform客戶，您也可以編寫自己的私人自訂目的地，以最符合您的啟用需求。

![概觀圖表，顯示目的地開發人員如何與Destination SDK互動，以及Real-Time CDP客戶如何從產品化和私人目的地獲益。](assets/destination-sdk-visual.png)

## 支援的整合型別 {#supported-integration-types}

### 即時（串流）整合 {#real-time-integrations}

透過Destination SDK，Adobe Experience Platform支援與具有REST API端點的目的地的即時整合（也稱為串流）。 與Experience Platform的即時整合支援如下的功能：

* 訊息轉換和彙總
* 設定檔回填
* 可設定的中繼資料整合，用於初始化對象設定和資料傳輸
* 可設定的驗證
* 一套測試和驗證API，可供您測試和疊代目的地設定

### 檔案式整合 {#file-based-integrations}

透過Destination SDK，您還可以設定整合以定期將檔案匯出至您選擇的儲存位置。 與Experience Platform的檔案式整合支援如下的功能：

* 匯出支援的檔案格式(CSV、Parquet、JSON)
* 可設定的檔案格式選項，可讓您根據下游需求來建構匯出檔案的格式。

閱讀[整合必要條件](integration-prerequisites.md)文章中目標端的技術需求，並閱讀[組態選項](functionality/configuration-options.md)文章中支援的所有組態

## 存取Destination SDK {#get-access}

Destination SDK存取權會因您身為合作夥伴或Experience Platform、Real-Time CDP客戶的身份而異。 如需詳細資訊，請參閱下表。

| 合作夥伴或客戶型別 | 如何存取Destination SDK |
---------|----------|
| 獨立軟體廠商(ISV) | 加入[Adobe技術合作夥伴計畫](https://partners.adobe.com/technologyprogram/experiencecloud.html)，並請求布建Experience Platform沙箱以存取Destination SDK。 |
| 系統整合商(SI) | 您必須是[Adobe解決方案合作夥伴計畫](https://solutionpartners.adobe.com/home.html)的金級或白金級，才能布建Experience Platform沙箱並存取Destination SDK。 |
| 在[Real-Time CDP Ultimate套件](https://helpx.adobe.com/jp/legal/product-descriptions/real-time-customer-data-platform.html)上Experience Platform客戶 | 依預設，您可以存取Experience Platform沙箱和Destination SDK，讓您為組織建立私人目的地。 |

{style="table-layout:auto"}

## 高階流程 {#process}

在Experience Platform中設定目的地的程式概述如下：

1. 如果您是ISV或SI，請參閱上節中的[取得存取權](#get-access)資訊。 [Real-Time CDP Ultimate套件](https://helpx.adobe.com/jp/legal/product-descriptions/real-time-customer-data-platform.html)客戶可略過此步驟。
2. [請求布建Experience Platform沙箱](https://adobeexchangeec.zendesk.com/hc/en-us/articles/360037457812-Adobe-Experience-Platform-Sandbox-Accounts-Access-Adding-Users-and-Support)並啟用目的地編寫許可權。
3. 建置您的整合。 依照產品檔案中的指示，設定[串流目的地](guides/configure-destination-instructions.md)或[以檔案為基礎的目的地](guides/configure-file-based-destination-instructions.md)。
4. 測試您的整合。 依照產品檔案中的指示，測試[串流目的地](testing-api/streaming-destinations/streaming-destination-testing-overview.md)或[以檔案為基礎的目的地](testing-api/batch-destinations/file-based-destination-testing-overview.md)。
5. 如果您是ISV或SI，正在建立[產品化整合](./overview.md#productized-custom-integrations)，請[提交您的整合](guides/submit-destination.md)以供Adobe檢閱（標準回應時間為5個工作日）。
6. 如果您是ISV或SI，正在建立產品化整合，請使用[自助服務檔案程式](docs-framework/documentation-instructions.md)來建立有關目的地Experience League的產品檔案頁面。
7. 針對產品化整合，Adobe核准後，您的整合將會顯示在[Experience Platform目錄](../catalog/overview.md)中。
8. 如果您想要更新整合，請遵循相同程式。

## 參考 {#reference}

Adobe建議您閱讀並瞭解下列Experience Platform檔案：

* [Adobe Experience Platform目的地概觀](https://experienceleague.adobe.com/docs/experience-platform/destinations/home.html?lang=zh-Hant)
* [XDM結構描述組合的基礎](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/composition.html?lang=zh-Hant)
* [身分名稱空間總覽](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=zh-Hant)
