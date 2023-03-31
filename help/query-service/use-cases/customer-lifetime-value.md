---
title: 追蹤資料訊號以產生客戶期限值
description: 本指南提供端對端示範，說明如何搭配Real-time Customer Data Platform使用資料Distiller和使用者定義的控制面板，來測量和視覺化客戶期限值。
source-git-commit: 2346f2d9450bc24e10419c09ee3dbcfb35bd5778
workflow-type: tm+mt
source-wordcount: '1296'
ht-degree: 0%

---

# 追蹤資料訊號以產生客戶期限值

您可以使用Real-time Customer Data Platform來追蹤客戶期限值(CLV)，並透過使用者定義的控制面板將該量度視覺化。 透過使用資料Distiller和使用者定義的控制面板，您可以衡量客戶在整個關係中對您公司的價值。 了解CLV有助於您制定業務策略以贏取新客戶，同時保留現有客戶並保持利潤。

下列資訊圖表說明資料收集、操作、分析和動作的週期，這些循環會產生高效能資料以改善您的行銷活動。

![從觀察到分析到行動的往返資訊圖。](../images/use-cases/infographic-use-case-cycle.png)

此端對端使用案例示範如何擷取和修改資料訊號，以計算客戶期限值衍生屬性。 然後，這些衍生屬性可套用至您的Real-Time CDP設定檔資料，並可與使用者定義的控制面板搭配使用，以建立控制面板進行深入分析。 透過Data Distiller，您可以擴充Real-Time CDP前瞻分析資料模型，並使用CLV衍生屬性和控制面板前瞻分析來建立新區段，並將其啟用至所需的目的地。 然後，這些區段便可用來建立高效能受眾，以支援您的下一個行銷活動。

本指南旨在透過測量推動CLV的關鍵接觸點上的資料訊號，並在您的環境中實作類似的使用案例，協助您更清楚了解客戶體驗。 整個過程在下圖中匯總。

![利用客戶期限值所需廣泛步驟的資訊圖表。](../images/use-cases/implementation-steps.png)

## 快速入門 {#getting-started}

本指南要求您妥善了解下列Adobe Experience Platform元件：

* [查詢服務](../home.md):提供使用者介面和RESTful API，您可在其中使用SQL查詢來分析和豐富您的資料。
* [區段服務](../../segmentation/home.md):可讓您透過即時客戶設定檔資料建立區段並產生受眾。

## 先決條件

本指南要求您 [資料Distiller](../data-distiller/overview.md) SKU是您套件產品的一部分。 如果您不確定自己是否擁有此功能，請洽詢您的Adobe服務代表。

## 建立衍生屬性 {#create-derived-attribute}

建立CLV的第一步是從從用戶操作捕獲的資料信號中建立派生屬性。 此特定使用案例會擷取至有關航空公司忠誠度方案的個別檔案中。 請參閱指南以了解如何 [使用Query Service建立資料型衍生屬性，以搭配您的設定檔資料使用](./deciles-use-case.md). 說明下列步驟的檔案提供了完整的範例和說明：

* 建立結構以允許分段。
* 使用查詢服務建立檔案。
* 產生十個資料集。
* 啟用結構以用於即時客戶設定檔。
* 建立身分命名空間並將其標示為主要識別碼。
* 建立查詢以計算回顧期間的分檔。

## 擴充前瞻分析資料模型並排程更新 {#extend-data-model-and-set-refresh-schedule}

接下來，您必須建立自訂資料模型或擴充現有的Adobe Real-Time CDP資料模型，以與CLV報表分析互動。 請參閱檔案以了解如何 [透過Query Service建立報表前瞻分析資料模型，以與加速儲存資料和使用者定義的控制面板搭配使用](../data-distiller/query-accelerated-store/reporting-insights-data-model.md#build-a-reporting-insights-data-model). 本教學課程涵蓋下列步驟：

* 使用Data Distiller建立報表深入分析的模型。
* 建立表、關係和填充資料。
* 查詢報表分析資料模型。
* 使用Real-Time CDP前瞻分析資料模型擴充您的資料模型。
* 建立維度表格以擴充您的報表前瞻分析模型。
* 查詢延伸加速儲存報告深入分析資料模型

請參閱Real-time Customer Data Platform Insights資料模型檔案，了解如何 [自訂SQL查詢範本，為您的行銷和關鍵績效指標(KPI)使用案例建立Real-Time CDP報表](../../dashboards/cdp-insights-data-model.md).

請務必設定排程，以定期重新整理自訂資料模型。 這可確保視需要將資料傳回作為擷取管道的一部分，並填入您使用者定義的控制面板。 請參閱 [排程查詢指南](../ui/query-schedules.md#create-schedule) 了解如何設定排程。

## 建立控制面板以擷取深入分析 {#build-a-custom-dashboard}

現在您已建立自訂資料模型，可使用自訂查詢和使用者定義的控制面板將資料視覺化。 如需如何取得的完整指引，請參閱使用者定義的控制面板概觀 [建立自訂控制面板](../../dashboards/user-defined-dashboards.md). UI指南包含下列內容的詳細資訊：

* 如何建立介面工具集。
* 如何使用介面工具集撰寫器。

下面可以看到使用資料桶的自定義CLV小工具的示例。

![自訂分檔式CLTV小工具的集合。](../images/use-cases/deciles-user-defined-dashboard.png)

## 建立並啟用區段以建立高效能受眾 {#create-and-activate-segments}

下一步是建立區段，並從您的即時客戶設定檔資料產生對象。 請參閱區段產生器UI指南，了解如何 [在Platform中建立和啟用區段](../../segmentation/ui/segment-builder.md). 本指南提供以下章節：

* 使用屬性、事件和現有對象的組合作為建置區塊，建立區段定義。
* 使用規則產生器畫布和容器來控制執行區段規則的順序。
* 檢視潛在對象的預估值，以便您視需要調整區段定義。
* 啟用排程分段的所有區段定義。
* 為串流細分啟用指定的區段定義。

或者，此外， [區段產生器教學課程](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html) 供參考。

## 啟用電子郵件行銷活動的區段 {#activate-segment-for-campaign}

建立區段後，您就可以將其啟用至目的地。 Platform支援各種電子郵件服務提供者(ESP)，可讓您管理電子郵件行銷活動，例如傳送促銷電子郵件行銷活動。

檢查 [電子郵件行銷目的地概述](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/email-marketing/overview.html?lang=en#connect-destination) 以取得您要匯出資料的支援目的地清單(例如 [Oracle雄辯](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/email-marketing/oracle-eloqua-api.html?lang=en) 頁面)。

## 查看從促銷活動傳回的分析資料 {#post-campaign-data-analysis}

來自來源的資料現在可以是 [逐步處理](../essential-concepts/incremental-load.md) 作為加速資料存放區中資料模型的排程重新整理的一部分。 客戶的任何回應事件可在發生時或以批次方式擷取至Adobe Experience Platform。 視您的設定或來源連接器而定，您的資料模型可重新整理一次或一天重新整理多次。 請參閱 [批次擷取API概觀](../../ingestion/batch-ingestion/api-overview.md) 或 [串流獲取概觀](../../ingestion/streaming-ingestion/overview.md) 以取得更多資訊。

更新資料模型後，自訂控制面板Widget會提供有意義的訊號，讓您測量並視覺化客戶期限值。

![自訂介面工具集，可顯示根據其群體和電子郵件促銷活動開啟的電子郵件數量。](../images/use-cases/post-activation-and-email-response-kpis.png)

為您的自訂分析提供多種視覺效果選項。

![由促銷活動貯體工具集開啟的電子郵件。](../images/use-cases/email-opened-by-campaign-buckets.png)

這些深入分析反過來又可協助您為後續的行銷活動制定業務策略。

![四個自訂小工具的集合，詳細說明電子郵件促銷活動的結果。](../images/use-cases/example-widgets.png)

## 後續步驟

閱讀本檔案後，您應該更清楚了解如何使用Real-time Customer Data Platform來追蹤及視覺化客戶期限值(CLV)量度。 若要進一步了解透過Query Service和Experience Platform滿足的許多業務使用案例，建議您閱讀下列檔案：

* [放棄的瀏覽使用案例的端對端範例，展示Query Service的多功能性和優點。](./abandoned-browse.md)
* [如何使用Query Service和機器學習來判斷及篩選來自正版線上網站訪客流量的機器人活動](./bot-filtering.md)
* [如何對結合多個資料集結果的Platform資料執行比對，方法是大約比對您選擇的字串。](./fuzzy-match.md)

<!-- "Data signals are actions taken by consumers while online that offer clues about intent that can be acted upon. This includes anything from visiting a website to filling out a change of address or clicking an ad."  -->

<!-- "Customer touchpoints are your brand's points of customer contact, from start to finish." -->
