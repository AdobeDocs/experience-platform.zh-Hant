---
title: 目的地中可設定的和常用的匯出設定
description: 瞭解目的地中哪些匯出設定可在目的地層級設定，哪些是固定的且無法編輯。
exl-id: 3f4706cb-6d51-4567-81f6-5b2bf167b576
source-git-commit: be2ad7a02d4bdf5a26a0847c8ee7a9a93746c2ad
workflow-type: tm+mt
source-wordcount: '834'
ht-degree: 0%

---

# 目的地中可設定的和常用的匯出設定

在考慮匯出至Experience Platform目的地的行為時，您需要考慮針對哪些設定採取行動的三個單獨層級。

* 在第一個層級，與設定檔匯出行為和組態設定相關的某些設定，在屬於某個目的地型別的所有目的地中都是通用的。 這些設定指會觸發目的地匯出的專案，以及匯出中包含的專案，這些設定無法由目的地開發人員或Real-Time CDP使用者編輯。
* 在第二層級，目的地開發人員在使用Destination SDK編寫目的地時，可以在目的地層級上自訂某些設定。
* 第三個層級是Real-Time CDP使用者可在啟動工作流程中設定的組態設定。

![顯示一般與可設定之目的地匯出設定之間互動的圖表](/help/destinations/assets/how-destinations-work/profile-export-behavior-diagram.png)

此頁面說明或連結至上述三個層級上目標的所有常見及可設定之匯出設定。

## 各種目的地型別通用的匯出設定 {#common-settings-across-destination-types}

目的地匯出行為在屬於目的地型別的目的地之間是一致的，這與&#x200B;*觸發目的地匯出的專案*&#x200B;和&#x200B;*目的地匯出專案中所包含的專案有關*。 目的地匯出是由目的地服務從[上游即時客戶設定檔服務](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/architecture-overview/platform-applications.html?lang=zh-Hant#adobe-experience-platform-%26-applications-detailed-architecture-diagram)收到的通知觸發。

目的地匯出中包含的內容會因目的地型別而略有不同。 深入瞭解每個目的地型別[的](/help/destinations/how-destinations-work/profile-export-behavior.md)常見匯出行為模式。 目的地開發人員或Real-Time CDP使用者無法編輯這些設定。

## 目的地開發人員可自訂的匯出設定 {#customizable-settings-by-destination-developers}

目的地開發人員可使用[Destination SDK](/help/destinations/destination-sdk/overview.md)建立自訂或產品化（私人或公用）目的地。 Destination SDK可讓開發人員根據其API端點和檔案接收系統的下游功能，以極為靈活地設定目的地。 根據下游功能，目的地開發人員在使用Destination SDK設定目的地時，有下列可用的設定選項：

* 決定哪些屬性和身分可以從Experience Platform匯出至目的地。 同時決定要成功匯出資料，其目的地需要哪些身分。
* 設定彙總原則，以決定Experience Platform在彙總要傳送給API整合的HTTP訊息時應等候多久。 目的地開發人員可設定不同的彙總型別，以判斷傳出HTTP訊息中應包含多少設定檔，以及Experience Platform應等候多久才傳送HTTP訊息。 在Destination SDK檔案中尋找目的地開發人員可用的有關[彙總原則設定選項](../destination-sdk/functionality/destination-configuration/aggregation-policy.md)的詳細資訊。
* 判斷HTTP訊息匯出是否應該包含符合區段資格和/或從區段移除的設定檔。
* 決定匯出檔案時，使用者應該可以使用哪些檔案名稱和檔案格式設定。

## 使用者可自訂的資料流層級設定 {#settings-on-dataflow-level}

根據目的地型別和目的地開發人員所設定的設定，除了無法編輯的設定之外，使用者也可以在啟動工作流程中設定某些匯出設定。 這些設定與特定資料流匯出至目的地的排程相關、應匯出至資料流中的屬性和身分欄位，或是匯出檔案的檔案格式選項。

使用者在連線至目的地時可使用的設定，取決於目的地開發人員設定目的地的方式，以及使用者可使用的設定。

例如，針對[串流目的地](/help/destinations/destination-types.md#streaming-destinations)，目的地開發人員可設定其目的地接受哪些身分，並且只會在啟動工作流程的[對應步驟](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping)中向使用者顯示這些身分，如下所示：

![在啟動工作流程的對應步驟中，針對目標欄位選取的身分進行熒幕錄製。](/help/destinations/assets/how-destinations-work/identity-mapping-example.gif)

同樣地，對於[以檔案為基礎的目的地](/help/destinations/destination-types.md#file-based)，目的地開發人員可以決定要為其目的地提供哪些[檔案名稱附加選項](/help/destinations/ui/activate-batch-profile-destinations.md#file-names)，或要為其提供哪些[檔案格式選項](/help/destinations/destination-sdk/guides/batch/configure-file-formatting-options.md)，而且使用者只能從這些選項中進行選取，如下所示：

![連線到以檔案為基礎的目的地時，熒幕錄製檔案格式選項。](/help/destinations/assets/how-destinations-work/file-formatting-options.gif)

![在啟動工作流程的排程步驟中，熒幕錄製檔案名稱附加選項。](/help/destinations/assets/how-destinations-work/filename-append-options.gif)

深入瞭解啟動工作流程中可用的不同選項和步驟：

* [啟用對象資料至批次設定檔匯出目的地](/help/destinations/ui/activate-batch-profile-destinations.md)
* [將受眾資料啟用至企業目的地](/help/destinations/ui/activate-streaming-profile-destinations.md)
* [啟用受眾資料至串流受眾匯出目的地](/help/destinations/ui/activate-segment-streaming-destinations.md)
* [隨選將檔案匯出至批次目的地](/help/destinations/ui/export-file-now.md)
* [將資料集匯出至雲端儲存空間目的地](/help/destinations/ui/export-datasets.md)

## 後續步驟 {#next-steps}

閱讀本檔案後，您現在瞭解哪些目的地的匯出設定是各目的地型別通用的匯出設定、開發人員可在個別目的地層級進行設定，以及使用者可在啟動工作流程中編輯哪些設定。

接著，您可以閱讀有關每個目的地型別[的](/help/destinations/how-destinations-work/profile-export-behavior.md)常見匯出行為模式的詳細資訊。

目的地開發人員可以[開始使用Destination SDK](/help/destinations/destination-sdk/getting-started.md)。 對於想要啟用資料的使用者，您可以簽出[目錄](/help/destinations/catalog/overview.md)中的所有可用目的地。
