---
title: 跟蹤資料信號以生成客戶生存期價值
description: 本指南提供了一個端到端演示，說明如何使用資料Distiller和用戶定義的儀表板與Real-time Customer Data Platform一起衡量和直觀顯示客戶的生命週期價值。
exl-id: c74b5bff-feb2-4e21-9ee4-1e0973192570
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '1296'
ht-degree: 0%

---

# 跟蹤資料信號以生成客戶生命週期價值

您可以使用Real-time Customer Data Platform跟蹤客戶生存期值(CLV)，並使用用戶定義的儀表板直觀顯示該度量。 通過使用資料Distiller和用戶定義的儀表板，您可以衡量客戶在整個關係中對您公司的價值。 瞭解CLV有助於您制定業務戰略以收購新客戶，同時保留現有客戶並保持利潤率。

以下資訊圖描述了資料收集、操作、分析和操作的週期，這些週期可生成高效能資料以改進您的市場營銷活動。

![從觀察到分析再到行動的往返資料資訊圖。](../images/use-cases/infographic-use-case-cycle.png)

此端到端使用案例演示了如何捕獲和修改資料信號以計算客戶生存期值派生屬性。 然後，這些派生屬性可應用到您的Real-Time CDP配置檔案資料，並可與用戶定義的儀表板一起使用，以構建用於洞察分析的儀表板。 通過資料Distiller，您可以擴展Real-Time CDP透視資料模型，並使用CLV派生的屬性和儀表板透視來構建新段並將其激活到所需的目標。 然後，這些細分市場可用於建立高效能受眾，以推動您的下一次營銷活動。

本指南旨在幫助您通過測量驅動CLV的關鍵觸點上的資料信號，在您的環境中實施類似的使用案例，從而更好地瞭解您的客戶體驗。 整個過程在下圖中進行了總結。

![利用客戶生命週期價值所需的廣泛步驟的資訊圖。](../images/use-cases/implementation-steps.png)

## 快速入門 {#getting-started}

本指南要求您對Adobe Experience Platform的以下部分有正確的瞭解：

* [查詢服務](../home.md):提供用戶介面和REST風格的API，在其中可以使用SQL查詢來分析和豐富資料。
* [分段服務](../../segmentation/home.md):允許您構建網段並根據即時客戶配置檔案資料生成受眾。

## 先決條件

本指南要求您 [資料Distiller](../data-distiller/overview.md) SKU作為軟體包產品的一部分。 如果您不確定是否擁有此服務，請與Adobe服務代表聯繫。

## 建立派生屬性 {#create-derived-attribute}

建立CLV的第一步是根據從用戶操作捕獲的資料信號建立派生屬性。 該特定用例在關於航空公司忠誠度計畫的單獨文檔中捕獲。 請參閱指南以瞭解如何 [使用查詢服務建立基於檔案的派生屬性，以便與配置檔案資料一起使用](./deciles-use-case.md)。 文檔中提供了完整的示例和說明，說明了以下步驟：

* 建立允許分段的架構。
* 使用查詢服務建立檔案。
* 生成資料集。
* 啟用方案以在Real-Time Customer Profile中使用。
* 建立標識命名空間並將其標籤為主標識符。
* 建立查詢以計算回望期間的分檔。

## 擴展見解資料模型並計畫更新 {#extend-data-model-and-set-refresh-schedule}

接下來，您必須構建自定義資料模型或擴展現有的Adobe Real-Time CDP資料模型，以與CLV報告洞察力進行溝通。 請參閱文檔以瞭解如何 [通過查詢服務生成報告見解資料模型，以便與加速的儲存資料和用戶定義的儀表板一起使用](../data-distiller/query-accelerated-store/reporting-insights-data-model.md#build-a-reporting-insights-data-model)。 本教程介紹以下步驟：

* 使用資料Distiller建立報告見解的模型。
* 建立表、關係和填充資料。
* 查詢報告真知灼見資料模型。
* 使用Real-Time CDP洞察力資料模型擴展您的資料模型。
* 建立維表以擴展報告見解模型。
* 查詢擴展的加速儲存報告見解資料模型

請參閱Real-time Customer Data Platform洞察力資料模型文檔以瞭解如何 [自定義SQL查詢模板，為您的市場營銷和關鍵績效指標(KPI)使用案例建立Real-Time CDP報表](../../dashboards/cdp-insights-data-model.md)。

確保設定計畫以在常規節奏上刷新自定義資料模型。 這可確保資料在需要時作為接收管道的一部分返回，並填充用戶定義的儀表板。 查看 [計畫查詢指南](../ui/query-schedules.md#create-schedule) 瞭解如何設定計畫。

## 生成儀表板以捕獲洞察 {#build-a-custom-dashboard}

現在，您已建立了自定義資料模型，您已準備好使用自定義查詢和用戶定義的儀表板來可視化資料。 請參閱用戶定義的儀表板概述，瞭解有關如何執行以下操作的完整指導 [生成自定義儀表板](../../dashboards/user-defined-dashboards.md)。 UI指南包括以下詳細資訊：

* 如何建立小部件。
* 如何使用小部件編寫器。

下面可以看到使用Decile儲存段的自定義CLV小部件的示例。

![基於十字型的定製CLTV小部件的集合。](../images/use-cases/deciles-user-defined-dashboard.png)

## 建立和激活段以構建高效能受眾 {#create-and-activate-segments}

下一步是構建網段並根據您的即時客戶配置檔案資料生成受眾。 請參閱段生成器UI指南，瞭解如何 [在平台中建立和激活段](../../segmentation/ui/segment-builder.md)。 本指南提供了有關如何執行以下操作的部分：

* 使用屬性、事件和現有受眾的組合作為構建塊建立段定義。
* 使用規則生成器畫布和容器來控制段規則的執行順序。
* 查看預期受眾的估計值，以便根據需要調整段定義。
* 啟用所有段定義以執行計劃分段。
* 為流分段啟用指定的段定義。

另外，還有 [段構建器視頻教程](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html) 的子菜單。

## 為電子郵件活動激活您的網段 {#activate-segment-for-campaign}

構建網段後，即可將其激活到目標。 平台支援多種電子郵件服務提供商(ESP)，使您能夠管理電子郵件營銷活動，如發送促銷電子郵件活動。

檢查 [電子郵件營銷目標概述](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/email-marketing/overview.html?lang=en#connect-destination) 要將資料導出到的受支援目標的清單(例如 [Oracle雄辯](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/email-marketing/oracle-eloqua-api.html?lang=en) )的正平方根。

## 查看市場活動返回的分析資料 {#post-campaign-data-analysis}

現在，源中的資料可以 [增量處理](../essential-concepts/incremental-load.md) 作為加速資料儲存中資料模型的計畫刷新的一部分。 客戶的任何響應事件都可以在發生時或批量接收到Adobe Experience Platform。 根據您的設定或源連接器，您的資料模型可以刷新一次或每天多次。 查看 [批處理接收API概述](../../ingestion/batch-ingestion/api-overview.md) 或 [流式處理概述](../../ingestion/streaming-ingestion/overview.md) 的子菜單。

資料模型更新後，您的自定義儀表板小部件將提供有意義的信號，使您能夠測量和直觀顯示客戶的生存期值。

![一個自定義小部件，用於顯示根據其段和電子郵件活動開啟的電子郵件數。](../images/use-cases/post-activation-and-email-response-kpis.png)

為您的自定義分析提供了多種可視化選項。

![由市場活動時段構件開啟的電子郵件。](../images/use-cases/email-opened-by-campaign-buckets.png)

這些見解反過來又有助於您為後續活動制定業務策略。

![一個由四個自定義小部件組成的集合，詳細列出電子郵件活動的結果。](../images/use-cases/example-widgets.png)

## 後續步驟

通過閱讀本文檔，您應更好地瞭解如何使用Real-time Customer Data Platform來跟蹤和可視化客戶生命週期價值(CLV)度量。 要瞭解有關通過查詢服務和Experience Platform滿足的許多業務使用案例的詳細資訊，建議您閱讀以下文檔：

* [已放棄瀏覽使用案例的端到端示例，演示了查詢服務的多用性和優點。](./abandoned-browse.md)
* [如何利用Query Service和機器學習來確定和過濾真實網站訪問流量中的bot活動](./bot-filtering.md)
* [如何對平台資料執行匹配，該匹配通過近似匹配您選擇的字串來組合來自多個資料集的結果。](./fuzzy-match.md)

<!-- "Data signals are actions taken by consumers while online that offer clues about intent that can be acted upon. This includes anything from visiting a website to filling out a change of address or clicking an ad."  -->

<!-- "Customer touchpoints are your brand's points of customer contact, from start to finish." -->
