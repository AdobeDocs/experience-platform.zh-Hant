---
title: 目標中的可配置和常用導出設定
description: 瞭解目標中的哪些導出設定可以在目標級別上配置，哪些設定是固定的且無法編輯。
exl-id: 3f4706cb-6d51-4567-81f6-5b2bf167b576
source-git-commit: a0400ab255b3b6a7edb4dcfd5c33a0f9e18b5157
workflow-type: tm+mt
source-wordcount: '845'
ht-degree: 0%

---

# 目標中的可配置和常用導出設定

在考慮將導出行為導出到Experience Platform目標時，需要考慮在哪三個不同級別上對配置進行操作。

* 在第一級，與配置檔案導出行為和配置設定相關的某些設定在屬於目標類型的所有目標上是通用的。 這些設定指的是哪些觸發了目標導出，哪些觸發了目標導出，哪些包含在導出中，目標開發人員或即時CDP用戶無法編輯。
* 在第二級，當創作使用Destination SDK的目標時，目標開發者可以在目標級別上自定義某些設定。
* 在第三級，即時CDP用戶可以在激活工作流中設定配置設定。

![顯示目標常用和可配置導出設定之間相互作用的圖](/help/destinations/assets/how-destinations-work/profile-export-behavior-diagram.png)

本頁在上面概述的三個級別上描述或連結到目標的所有常用和可配置的導出設定。

## 目標類型之間的常用導出設定 {#common-settings-across-destination-types}

目標導出行為在屬於目標類型的目標之間是一致的 *觸發目標導出的因素* 和 *目標導出中包含的內容*。 目標導出由目標服務從 [上游即時客戶概要資訊服務](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/architecture-overview/platform-applications.html?lang=en#adobe-experience-platform-%26-applications-detailed-architecture-diagram)。

目標導出中包含的內容因目標類型而略有不同。 閱讀有關 [每個目標類型的公共導出行為模式](/help/destinations/how-destinations-work/profile-export-behavior.md)。 目標開發人員或即時CDP用戶無法編輯這些設定。

## 目標開發人員可自定義的導出設定 {#customizable-settings-by-destination-developers}

目標開發人員可以使用 [Destination SDK](/help/destinations/destination-sdk/overview.md) 建立自定義或產品化（私有或公共）目標。 Destination SDK為開發人員提供了基於其API端點和檔案接收系統的下游功能配置目標的極大靈活性。 根據下游功能，目標開發人員在使用Destination SDK配置目標時可以使用以下配置選項：

* 確定哪些屬性和標識可以從Experience Platform導出到目標。 還確定目標需要哪些身份才能成功導出資料。
* 設定聚合策略，該策略確定聚合要發送到API整合的HTTP消息時Experience Platform應等待多長時間。 目標開發人員可以配置不同的聚合類型，以確定在傳出HTTP消息中應包括多少個配置式，以及Experience Platform應等待多長時間，直到發送HTTP消息。 查找有關 [聚合策略配置選項](../destination-sdk/functionality/destination-configuration/aggregation-policy.md) 可供目標開發人員使用的Destination SDK文檔。
* 確定HTTP消息導出是否應包括符合段條件的配置檔案、從段中刪除的配置檔案或兩者。
* 確定導出檔案時用戶應使用哪些檔案名和檔案格式配置。

## 用戶可自定義的資料流級別上的設定 {#settings-on-dataflow-level}

除了取決於目標類型和目標開發人員配置的設定的不可編輯設定之外，用戶還可以在激活工作流中配置某些導出設定。 這些設定與特定資料流到目標的導出計畫、應在資料流中導出的屬性和標識欄位，或導出檔案的檔案格式選項相關。

連接到目標時用戶可用的設定取決於目標開發人員如何配置目標以及用戶可以使用哪些設定。

例如， [流目標](/help/destinations/destination-types.md#streaming-destinations)，目標開發人員可以配置其目標接受的標識，並且只將這些標識顯示給 [激活工作流的映射步驟](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping)，如下所示：

![在激活工作流的映射步驟中，螢幕記錄目標欄位的身份選擇。 ](/help/destinations/assets/how-destinations-work/identity-mapping-example.gif)

同樣， [基於檔案的目標](/help/destinations/destination-types.md#file-based)，目標開發人員可以確定 [檔案名附加選項](/help/destinations/ui/activate-batch-profile-destinations.md#file-names) 他們想為目的地提供，或者 [檔案格式選項](/help/destinations/destination-sdk/guides/batch/configure-file-formatting-options.md) 他們希望可用，並且用戶只能從這些選項中進行選擇，如下所示：

![連接到基於檔案的目標時，檔案格式選項的螢幕錄制。](/help/destinations/assets/how-destinations-work/file-formatting-options.gif)

![在激活工作流的調度步驟中對檔案名附加選項進行螢幕錄制。 ](/help/destinations/assets/how-destinations-work/filename-append-options.gif)

閱讀有關激活工作流中可用的不同選項和步驟的更多資訊：

* [將受眾資料激活到批配置檔案導出目標](/help/destinations/ui/activate-batch-profile-destinations.md)
* [將受眾資料激活到企業目標](/help/destinations/ui/activate-streaming-profile-destinations.md)
* [將受眾資料激活到流段導出目標](/help/destinations/ui/activate-segment-streaming-destinations.md)
* [按需將檔案導出到批處理目標](/help/destinations/ui/export-file-now.md)
* [(Beta)將資料集導出到雲儲存目標](/help/destinations/ui/export-datasets.md)

## 後續步驟 {#next-steps}

閱讀本文檔後，您現在知道目標的導出設定在目標類型之間是通用的，開發人員可以在單個目標級別上配置這些設定，以及哪些設定可以由激活工作流中的用戶編輯。

接下來，您可以閱讀有關 [每個目標類型的公共導出行為模式](/help/destinations/how-destinations-work/profile-export-behavior.md)。

對於目標開發人員，您可以 [開始](/help/destinations/destination-sdk/getting-started.md) Destination SDK。 對於希望激活資料的用戶，您可以簽出中的所有可用目標 [目錄](/help/destinations/catalog/overview.md)。
