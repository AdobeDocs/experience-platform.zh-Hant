---
description: Adobe Experience Platform Destination SDK是一組配置API，允許您配置目標整合模式，以便根據您選擇的資料和身份驗證格式將受眾和配置檔案資料傳送到您的端點或儲存位置。 這些配置儲存在Experience Platform中，並可通過API檢索，以進行其他更新。
title: Adobe Experience Platform Destination SDK
exl-id: 7aca9f40-98c8-47c2-ba88-4308fc2b1798
source-git-commit: 118ff85a9fceb8ee81dbafe2c381d365b813da29
workflow-type: tm+mt
source-wordcount: '854'
ht-degree: 4%

---

# Adobe Experience Platform Destination SDK

Adobe Experience Platform Destination SDK是一套配置API，允許您配置目標整合模式，以便根據您選擇的資料和身份驗證格式將受眾和配置檔案資料傳送到您的端點或儲存位置。 這些配置儲存在Experience Platform中，並可通過API檢索，以進行其他更新。

Destination SDK文檔為您提供了使用Adobe Experience Platform Destination SDK配置、test和發佈與Adobe Experience Platform產品化目標整合的說明，並讓您的目標成為不斷增長的目標目錄的一部分。 通過使用Destination SDK，您還可以建立自己的自定義專用目標以導出根據需要定製的資料。

![Experience PlatformUI的螢幕快照，顯示目標目錄](assets/destinations-catalog-overview.png)

## 產品化和定制整合 {#productized-custom-integrations}

>[!IMPORTANT]
>
> 建立專用自定義目標的此功能僅適用於 [Adobe Real-time Customer Data Platform旗艦](https://helpx.adobe.com/jp/legal/product-descriptions/real-time-customer-data-platform.html) 客戶。

作為Destination SDK合作夥伴，您可以將已生產的目標添加到 [Experience Platform目錄](../catalog/overview.md):

1. 使用預先配置的參數標準化客戶之間的整合配置，並簡化客戶的設定體驗。
2. 在Experience Platform目標目錄中引入品牌目標卡，以簡化客戶設定和認識。
3. 作為與Adobe Experience Platform和Adobe Real-time Customer Data Platform的產品化目的地整合。

作為Experience Platform客戶，您還可以建立自己的私人自定義目標，這最適合您的激活需要。

![概覽圖，顯示目標開發商如何與Destination SDK交互，以及Real-Time CDP客戶如何從產品化和私有目標中獲益。](assets/destination-sdk-visual.png)

## 支援的整合類型 {#supported-integration-types}

### 即時（流）整合 {#real-time-integrations}

通過Destination SDK,Adobe Experience Platform支援與具有REST API端點的目標的即時（也稱為流）整合。 與Experience Platform的即時整合支援以下功能：

* 消息轉換和聚合
* 配置檔案回填
* 可配置元資料整合以初始化受眾設定和資料傳輸
* 可配置的身份驗證
* 一套測試和驗證API，供您test和迭代目標配置

### 基於檔案的整合 {#file-based-integrations}

通過Destination SDK，您還可以設定整合，以定期將檔案導出到您選擇的儲存位置。 基於檔案的與Experience Platform的整合支援以下功能：

* 以多種支援格式(CSV、Parce、JSON)導出檔案
* 可配置的檔案格式設定選項，允許您根據下游要求對導出檔案的格式進行結構化。

閱讀中目標端的技術要求 [整合先決條件](integration-prerequisites.md) 文章並閱讀有關中所有支援的配置 [配置選項](functionality/configuration-options.md) 文章

## 獲取Destination SDK {#get-access}

Destination SDK訪問因您作為合作夥伴或Experience Platform(Real-Time CDP客戶)的狀態而異。 有關詳細資訊，請參閱下表。

| 合作夥伴或客戶的類型 | 如何訪問Destination SDK |
---------|----------|
| 獨立軟體供應商(ISV) | 加入 [Adobe技術合作夥伴計畫](https://partners.adobe.com/technologyprogram/experiencecloud.html) 並請求獲取預配的Experience Platform沙盒以訪問Destination SDK。 |
| 系統整合商(SI) | 您需要在2015年的黃金或白金級別 [Adobe解決方案合作夥伴計畫](https://solutionpartners.adobe.com/home.html)，您將獲得Experience Platform沙盒的預配和Destination SDK。 |
| Experience Platform客戶 [Real-Time CDP終極包](https://helpx.adobe.com/jp/legal/product-descriptions/real-time-customer-data-platform.html) | 預設情況下，您可以訪問Experience Platform沙箱和Destination SDK，從而為您的組織構建私有目標。 |

{style="table-layout:auto"}

## 高級流程 {#process}

在Experience Platform中配置目標的過程概述如下：

1. 如果您是ISV或SI，請參閱 [獲取](#get-access) 資訊。 [Real-Time CDP終極包](https://helpx.adobe.com/jp/legal/product-descriptions/real-time-customer-data-platform.html) 客戶可以跳過此步驟。
2. [請求設定Experience Platform沙箱](https://adobeexchangeec.zendesk.com/hc/en-us/articles/360037457812-Adobe-Experience-Platform-Sandbox-Accounts-Access-Adding-Users-and-Support) 並啟用目標創作權限。
3. 構建整合。 按照產品文檔中的說明進行配置 [流目標](guides/configure-destination-instructions.md) 或 [基於檔案的目標](guides/configure-file-based-destination-instructions.md)。
4. Test您的整合。 按照產品文檔中的說明進行test [流目標](testing-api/streaming-destinations/streaming-destination-testing-overview.md) 或 [基於檔案的目標](testing-api/batch-destinations/file-based-destination-testing-overview.md)。
5. 如果您是ISV或SI建立 [產品化整合](./overview.md#productized-custom-integrations)。 [提交整合](guides/submit-destination.md) Adobe審閱（標準響應時間為五個工作日）。
6. 如果您是ISV或SI建立產品化整合，請使用 [自助文檔處理](docs-framework/documentation-instructions.md) 建立目標Experience League上的產品文檔頁面。
7. 對於產品化整合，一旦獲得Adobe批准，您的整合將顯示在 [Experience Platform目錄](../catalog/overview.md)。
8. 如果要更新整合，請遵循相同的流程。

## 參考 {#reference}

Adobe建議您閱讀並瞭解以下Experience Platform文檔：

* [Adobe Experience Platform目標概述](https://experienceleague.adobe.com/docs/experience-platform/destinations/home.html?lang=en)
* [XDM架構組合的基礎](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/composition.html?lang=zh-Hant)
* [Identity命名空間概述](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=en)
