---
title: 追蹤資料訊號以產生客戶期限值
description: 本指南提供端對端示範，說明如何搭配使用Data Distiller和使用者定義的儀表板與Real-Time Customer Data Platform，以測量及視覺化客戶期限值。
exl-id: c74b5bff-feb2-4e21-9ee4-1e0973192570
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1266'
ht-degree: 0%

---

# 追蹤資料訊號以產生您的客戶期限值

您可以使用Real-Time Customer Data Platform追蹤客戶期限值(CLV)，並使用使用者定義的儀表板將該量度視覺化。 透過使用Data Distiller和使用者定義儀表板，您可以測量客戶在整個關係中對您公司的價值。 瞭解CLV可協助您制定企業策略，以爭取新客戶，同時保留現有客戶，並維持利潤率。

下列資訊圖表說明產生高效能資料，以改善行銷活動的資料收集、操控、分析和執行的週期。

![從觀察到分析再到動作的資料往返資訊圖。](../images/use-cases/infographic-use-case-cycle.png)

此端對端使用案例示範如何擷取及修改資料訊號，以計算客戶期限值衍生屬性。 這些衍生的資料集可接著套用至您的Real-Time CDP設定檔資料，並可用於使用者定義的控制面板，以建置用於insight分析的控制面板。 透過Data Distiller，您可以擴充Real-Time CDP見解資料模型，並使用CLV衍生的資料集和儀表板見解來建立新受眾，並將其啟用至所需的目的地。 然後，這些高效能受眾可用於支援您的下一個行銷活動。

本指南旨在協助您透過測量推動CLV的關鍵接觸點上的資料訊號，以及在您的環境中實作類似的使用案例，來更好地瞭解您的客戶體驗。 下圖會摘要說明整個程式。

![使用客戶期限值所需之廣泛步驟的資訊圖。](../images/use-cases/implementation-steps.png)

## 快速入門 {#getting-started}

本指南需要您實際瞭解下列Adobe Experience Platform元件：

* [查詢服務](../home.md)：提供使用者介面和RESTful API，您可以使用SQL查詢來分析和擴充資料。
* [分段服務](../../segmentation/home.md)：可讓您從即時客戶設定檔資料產生對象。

## 先決條件

本指南要求您擁有[資料Distiller](../data-distiller/overview.md) SKU，作為套件方案的一部分。 如果您不確定您是否擁有此服務，請洽詢您的Adobe服務代表。

## 建立衍生的資料集 {#create-derived-dataset}

建立CLV的第一步是從使用者動作擷取的資料訊號建立衍生資料集。 此特定使用案例記錄於有關航空公司忠誠度方案的獨立檔案中。 請參閱指南以瞭解如何[使用查詢服務來建立以十等位元為基礎的衍生資料集，以搭配您的設定檔資料使用](./deciles-use-case.md)。 檔案中提供完整範例和說明，說明下列步驟：

* 建立結構描述以允許十等分分組。
* 使用查詢服務來建立十等分。
* 產生十等分資料集。
* 啟用結構以用於Real-Time Customer Profile。
* 建立身分名稱空間並將其標示為主要識別碼。
* 建立查詢以計算回顧期間的十分位數。

## 擴充見解資料模型和排程更新 {#extend-data-model-and-set-refresh-schedule}

接下來，您必須建立自訂資料模型或擴充現有的Adobe Real-Time CDP資料模型，以參與您的CLV報表深入分析。 請參閱檔案，瞭解如何透過Query Service [建立報告見解資料模型，以搭配加速商店資料和使用者定義儀表板](../data-distiller/sql-insights/reporting-insights-data-model.md#build-a-reporting-insights-data-model)使用。 本教學課程涵蓋下列步驟：

* 使用Data Distiller建立模型以報告深入分析。
* 建立表格、關係及填入資料。
* 查詢報表insight資料模型。
* 使用Real-Time CDP見解資料模型擴充您的資料模型。
* 建立維度表格以擴充您的報表見解模型。
* 查詢您的擴充式加速存放區報告見解資料模型

請參閱Real-Time Customer Data Platform前瞻分析資料模型檔案，瞭解如何[自訂您的SQL查詢範本，為您的行銷和關鍵績效指標(KPI)使用案例建立Real-Time CDP報告](../../dashboards/data-models/cdp-insights-data-model-b2c.md)。

請務必設定排程，定期重新整理您的自訂資料模型。 這可確保資料會視需要傳回作為您擷取管道的一部分，並填入您的使用者定義儀表板。 請參閱[排程查詢指南](../ui/query-schedules.md#create-schedule)以瞭解如何設定排程。

## 建立儀表板以擷取深入分析 {#build-a-custom-dashboard}

現在您已建立自訂資料模型，您已準備好使用自訂查詢和使用者定義儀表板將您的資料視覺化。 如需如何[建立自訂儀表板](../../dashboards/standard-dashboards.md)的完整指引，請參閱使用者定義儀表板概觀。 UI指南包括下列專案的詳細資訊：

* 如何建立Widget。
* 如何使用Widget撰寫器。

以下提供使用十等分儲存貯體的自訂CLV Widget範例。

![自訂十等分的CLTV Widget集合。](../images/use-cases/deciles-user-defined-dashboard.png)

## 建立並啟用高效能對象 {#create-and-activate-audiences}

下一步是建立區段定義，並從您的即時客戶設定檔資料產生對象。 請參閱區段產生器UI指南，瞭解如何[在Experience Platform](../../segmentation/ui/segment-builder.md)中建立和啟用對象。 本指南提供幾個小節，說明如何：

* 使用屬性、事件和現有對象的組合作為建置區塊來建立區段定義。
* 使用規則產生器畫布和容器來控制分段規則的執行順序。
* 檢視潛在對象的預估值，讓您視需要調整區段定義。
* 啟用已排程區段的所有區段定義。
* 啟用串流區段的指定區段定義。

或者，您也可以參閱[區段產生器教學影片](https://experienceleague.adobe.com/docs/platform-learn/tutorials/audiences/create-segments.html)以取得詳細資訊。

## 為電子郵件行銷活動啟用對象 {#activate-audience-for-campaign}

當您建立對象後，您就可以將其啟用至目的地。 Experience Platform支援各種電子郵件服務提供者(ESP)，可讓您管理電子郵件行銷活動，例如傳送促銷電子郵件行銷活動。

檢查[電子郵件行銷目的地概觀](../../destinations/catalog/email-marketing/overview.md#connect-destination)，以取得您要將資料匯出至的支援目的地清單(例如[Oracle Eloqua](../../destinations/catalog/email-marketing/oracle-eloqua-api.md)頁面)。

## 檢視從行銷活動傳回的分析資料 {#post-campaign-data-analysis}

來源資料現在可以進行[逐步處理](../key-concepts/incremental-load.md)，做為加速資料存放區中資料模型排程重新整理的一部分。 客戶的任何回應事件都可在發生時或批次中擷取到Adobe Experience Platform。 您的資料模型可能會重新整理一次，或一天重新整理多次，視您的設定或來源聯結器而定。 如需詳細資訊，請參閱[批次擷取API總覽](../../ingestion/batch-ingestion/api-overview.md)或[串流擷取總覽](../../ingestion/streaming-ingestion/overview.md)。

更新資料模型後，您的自訂儀表板Widget就會提供有意義的訊號，讓您測量並視覺化客戶期限值。

![自訂Widget，根據對象和電子郵件行銷活動顯示開啟的電子郵件數量。](../images/use-cases/post-activation-and-email-response-kpis.png)

為您的自訂分析提供各種視覺效果選項。

![行銷活動貯體Widget開啟的電子郵件。](../images/use-cases/email-opened-by-campaign-buckets.png)

這些見解進而可協助您為後續行銷活動制定業務策略。

![四個自訂Widget的集合，詳細說明電子郵件行銷活動的結果。](../images/use-cases/example-widgets.png)

## 後續步驟

閱讀本檔案後，您應該就能更加瞭解如何使用Real-Time Customer Data Platform追蹤及視覺化客戶期限值(CLV)量度。 若要進一步瞭解透過查詢服務和Experience Platform提供的許多業務使用案例，建議您閱讀以下檔案：

* [已放棄的瀏覽使用案例的端對端範例，可示範Query Service的多功能性及優點。](./abandoned-browse.md)
* [如何使用查詢服務和機器學習來判斷並篩選真正線上網站訪客流量的機器人活動](./bot-filtering.md)
* [如何在您的Experience Platform資料上執行比對，並透過大致比對您選擇的字串來合併來自多個資料集的結果。](./fuzzy-match.md)

<!-- "Data signals are actions taken by consumers while online that offer clues about intent that can be acted upon. This includes anything from visiting a website to filling out a change of address or clicking an ad."  -->

<!-- "Customer touchpoints are your brand's points of customer contact, from start to finish." -->
