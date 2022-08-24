---
description: Adobe Experience Platform Destination SDK是一組配置API，允許您配置目標整合模式，以便根據您選擇的資料和身份驗證格式將受眾和配置檔案資料傳送到您的端點。 這些配置儲存在Experience Platform中，並可通過API檢索，以進行其他更新。
title: Adobe Experience Platform Destination SDK
exl-id: 7aca9f40-98c8-47c2-ba88-4308fc2b1798
source-git-commit: c207b6700a31c59b00af6d55264c7a345219d999
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# Adobe Experience Platform Destination SDK

## 總覽 {#destinations-sdk}

Adobe Experience Platform Destination SDK是一套配置API，允許您配置目標整合模式，以便根據您選擇的資料和身份驗證格式將受眾和配置檔案資料傳送到您的端點。 這些配置儲存在Experience Platform中，並可通過API檢索，以進行其他更新。

Destination SDK文檔為您提供了使用Adobe Experience Platform Destination SDK配置、test和發佈與Adobe Experience Platform產品化目標整合的說明，並讓您的目標成為不斷增長的目標目錄的一部分。

![目標目錄概述](./assets/destinations-catalog-overview.png)

## 產品化和定制整合 {#productized-custom-integrations}

作為Destination SDK合作夥伴，您可以將已生產的目標添加到 [Experience Platform目錄](/help/destinations/catalog/overview.md):
1. 使用預先配置的參數標準化客戶之間的整合配置，並簡化客戶的設定體驗。
2. 在Experience Platform目標目錄中引入品牌目標卡，以簡化客戶設定和認識。
3. 作為與Adobe Experience Platform和Real-time Customer Data Platform的產品化目的地整合。

作為Experience Platform客戶，您可以建立自己的私有自定義目標，這最適合您的激活需要。

![Destination SDK可視圖](./assets/destination-sdk-visual.png)

<!--

## Types of destinations in Adobe Experience Platform {#types-of-destinations}

In Adobe Experience Platform, we distinguish between two destination types - *connections* and *extensions*. In the user interface, customers can choose between two types of connection destinations, Profile Export destinations and Segment Export destinations. For more details around the difference between the different destination types, read [Destination Types and Categories](https://experienceleague.adobe.com/docs/experience-platform/destinations/destination-types.html?lang=en).

![Destination types](./assets/types-of-destinations.png)

This documentation set provides you with all the necessary information to add your destination to Adobe Experience Platform, as a *connection*, either Profile Export or Segment Export. To set up an extension, visit the [Experience Platform Launch developer portal](https://developer.adobelaunch.com/extensions/).

-->

## 支援的整合類型 {#supported-integration-types}

通過Destination SDK,Adobe Experience Platform支援與具有REST API端點的目標進行即時整合。 與Experience Platform的即時整合支援以下功能：
* 消息轉換和聚合
* 配置檔案回填
* 可配置元資料整合以初始化受眾設定和資料傳輸
* 可配置的身份驗證
* 一套測試和驗證API，供您test和迭代目標配置

閱讀中目標端的技術要求 [整合先決條件](./integration-prerequisites.md) 文章。

## 獲取Destination SDK {#get-access}

Destination SDK訪問因您作為合作夥伴或Experience Platform(Real-Time CDP客戶)的狀態而異。 有關詳細資訊，請參閱下表。


| 合作夥伴或客戶的類型 | 如何訪問Destination SDK |
---------|----------|
| 獨立軟體供應商(ISV) | 加入 [Adobe交換計畫](https://partners.adobe.com/exchangeprogram/experiencecloud.html) 並請求獲取預配的Experience Platform沙盒以訪問Destination SDK。 |
| 系統整合商(SI) | 您需要在2015年的黃金或白金級別 [Adobe解決方案合作夥伴計畫](https://solutionpartners.adobe.com/home.html)，您將獲得Experience Platform沙盒的預配和Destination SDK。 |
| Experience Platform客戶 [激活包](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-platform0.html) | 預設情況下，您可以訪問Experience Platform沙箱和Destination SDK。 <br> 您還可以訪問其他公司使用Destination SDK配置的所有已生產化目標，並可以跨Experience Platform組織發佈。 |
| Experience Platform客戶 [Real-Time CDP終極包](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform.html) | 預設情況下，您可以訪問Experience Platform沙箱和Destination SDK。 <br> 您還可以訪問其他公司使用Destination SDK配置的所有已生產化目標，並可以跨Experience Platform組織發佈。 |

{style=&quot;table-layout:auto&quot;}

## 高級流程 {#process}

在Experience Platform中配置目標的過程概述如下：

1. 如果您是ISV或SI，請參閱上面部分的獲取訪問資訊。 [Adobe Experience Platform激活](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-platform0.html) 客戶可以跳過此步驟。
2. [請求設定Experience Platform沙箱](https://adobeexchangeec.zendesk.com/hc/en-us/articles/360037457812-Adobe-Experience-Platform-Sandbox-Accounts-Access-Adding-Users-and-Support) 並啟用目標創作權限。
3. 構建整合。 按照產品文檔中的說明進行配置 [流目標](./configure-destination-instructions.md) 或 [基於檔案的目標(beta)](./configure-file-based-destination-instructions.md)。
4. Test您的整合。 按照產品文檔中的說明進行test [流目標](./test-destination.md) 或 [基於檔案的目標(beta)](./file-based-destination-testing-overview.md)。
5. 如果您是ISV或SI建立 [產品化整合](./overview.md#productized-custom-integrations)。 [提交整合](./submit-destination.md) Adobe審閱（標準響應時間為五個工作日）。
6. 如果您是ISV或SI建立產品化整合，請使用 [自助文檔處理](./docs-framework/documentation-instructions.md) 建立目標Experience League上的產品文檔頁面。
7. 對於產品化整合，一旦獲得Adobe批准，您的整合將顯示在 [Experience Platform目錄](/help/destinations/catalog/overview.md)。
8. 如果要更新整合，請遵循相同的流程。

## 參考 {#reference}

Adobe建議您閱讀並瞭解以下Experience Platform文檔：

* [Adobe Experience Platform目標概述](https://experienceleague.adobe.com/docs/experience-platform/destinations/home.html?lang=en)
* [XDM架構組合的基礎](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/composition.html?lang=zh-Hant)
* [Identity命名空間概述](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=en)
