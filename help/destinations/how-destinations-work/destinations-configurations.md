---
title: 目的地中的可設定和通用匯出設定
description: 了解目標中的哪些匯出設定可在目標層級設定，哪些已修正且無法編輯。
exl-id: 3f4706cb-6d51-4567-81f6-5b2bf167b576
source-git-commit: a0400ab255b3b6a7edb4dcfd5c33a0f9e18b5157
workflow-type: tm+mt
source-wordcount: '845'
ht-degree: 0%

---

# 目的地中的可設定和通用匯出設定

在思考匯出至Experience Platform目的地的行為時，您需要考慮三個不同層級的設定動作。

* 在第一層，與設定檔匯出行為和組態設定相關的某些設定，在屬於目的地類型的所有目的地中都很常見。 這些設定指的是觸發目標匯出的因素，以及匯出中包含的因素，且無法由目標開發人員或即時CDP使用者編輯。
* 在第二層，當使用Destination SDK製作目的地時，目的地開發人員可在目的地層級自訂某些設定。
* 在第三個層級，即時CDP使用者可在啟動工作流程中設定組態設定。

![顯示目標的常見和可配置導出設定之間相互作用的圖表](/help/destinations/assets/how-destinations-work/profile-export-behavior-diagram.png)

本頁面在上述的三個層級上說明或連結至目的地的所有通用和可設定的匯出設定。

## 各目的地類型的常用匯出設定 {#common-settings-across-destination-types}

目的地匯出行為在屬於目的地類型的目的地之間一致， *觸發目標匯出的原因* 和 *目標匯出包含的項目*. 目的地匯出是由目的地服務從 [上游即時客戶設定檔服務](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/architecture-overview/platform-applications.html?lang=en#adobe-experience-platform-%26-applications-detailed-architecture-diagram).

目的地匯出包含的項目因目的地類型而異。 深入了解 [每個目標類型的常見導出行為模式](/help/destinations/how-destinations-work/profile-export-behavior.md). 目標開發人員或Real-time CDP使用者無法編輯這些設定。

## 由目的地開發人員自訂的匯出設定 {#customizable-settings-by-destination-developers}

目標開發人員可使用 [Destination SDK](/help/destinations/destination-sdk/overview.md) 建立自訂或產品化（私人或公用）目的地。 Destination SDK可讓開發人員根據其API端點和檔案接收系統的下游功能，有極大的彈性設定目的地。 根據下游功能，目標開發人員在使用Destination SDK設定目標時可使用下列設定選項：

* 決定哪些屬性和身分可從Experience Platform匯出至目的地。 也判斷目的地為成功匯出資料所需的身分。
* 設定匯總原則，決定Experience Platform在匯總要傳送至API整合的HTTP訊息時應等待多久。 目標開發人員可以配置不同的聚合類型，以確定傳出HTTP消息中應包含多少配置檔案，以及Experience Platform應等待多久才發送HTTP消息。 尋找有關 [聚合策略配置選項](../destination-sdk/functionality/destination-configuration/aggregation-policy.md) 可在Destination SDK檔案中供目的地開發人員使用。
* 判斷HTTP訊息匯出是否應包含符合區段、從區段移除或兩者皆移除的設定檔。
* 確定在導出檔案時，用戶應使用哪些檔案名和檔案格式配置。

## 用戶可自定義的資料流級別上的設定 {#settings-on-dataflow-level}

除了依目的地類型和目的地開發人員設定的不可編輯設定外，還有某些匯出設定可供使用者在啟動工作流程中設定。 這些設定與特定資料流到目標的導出計畫、應在資料流中導出的屬性和標識欄位，或導出檔案的檔案格式選項相關。

連線至目的地時，使用者可用的設定取決於目的地開發人員如何設定目的地，以及使用者可使用的設定。

例如， [串流目的地](/help/destinations/destination-types.md#streaming-destinations)，目的地開發人員可設定其目的地接受的身分識別，且只有這些身分識別會顯示給 [啟動工作流程的對應步驟](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping)，如下所示：

![在啟動工作流程的映射步驟中，目標欄位的身分選擇的螢幕記錄。 ](/help/destinations/assets/how-destinations-work/identity-mapping-example.gif)

同樣地， [檔案型目的地](/help/destinations/destination-types.md#file-based)，目的地開發人員可判斷 [檔案附加選項](/help/destinations/ui/activate-batch-profile-destinations.md#file-names) 他們想要提供目的地，或 [檔案格式選項](/help/destinations/destination-sdk/guides/batch/configure-file-formatting-options.md) 他們想要讓可供使用，而使用者只能從這些選項中選取，如下所示：

![連接到基於檔案的目標時，檔案格式選項的螢幕記錄。](/help/destinations/assets/how-destinations-work/file-formatting-options.gif)

![在啟動工作流程的排程步驟中，檔案名稱附加選項的畫面記錄。 ](/help/destinations/assets/how-destinations-work/filename-append-options.gif)

深入了解啟動工作流程中可用的不同選項和步驟：

* [啟用受眾資料以批次設定檔匯出目的地](/help/destinations/ui/activate-batch-profile-destinations.md)
* [對企業目的地啟用受眾資料](/help/destinations/ui/activate-streaming-profile-destinations.md)
* [對串流區段匯出目的地啟用受眾資料](/help/destinations/ui/activate-segment-streaming-destinations.md)
* [按需將檔案導出到批處理目標](/help/destinations/ui/export-file-now.md)
* [（測試版）將資料集匯出至雲端儲存目標](/help/destinations/ui/export-datasets.md)

## 後續步驟 {#next-steps}

閱讀本檔案後，您現在知道各目的地類型中哪些匯出設定是常見的，可由開發人員在個別目的地層級上設定，以及哪些設定可由使用者在啟動工作流程中編輯。

接下來，您可以閱讀 [每個目標類型的常見導出行為模式](/help/destinations/how-destinations-work/profile-export-behavior.md).

若為目的地開發人員，您可以 [快速入門](/help/destinations/destination-sdk/getting-started.md) Destination SDK。 若是想要啟用資料的使用者，您可以查看 [目錄](/help/destinations/catalog/overview.md).
