---
title: Adobe Experience Platform 發行說明 (2024 年 9 月)
description: Adobe Experience Platform 2024 年 9 月版發行說明。
exl-id: f854f9e5-71be-4d56-a598-cfeb036716cb
source-git-commit: 059ed53ace6d54a0c0fb406c2f0379588fea2c44
workflow-type: tm+mt
source-wordcount: '2149'
ht-degree: 84%

---

# Adobe Experience Platform 發行說明

**發行日期：2024 年 9 月 24 日**

Adobe Experience Platform 現有功能及文件的更新：

- [Adobe Experience Platform 發行說明](#adobe-experience-platform-release-notes)
   - [警報 {#alerts}](#alerts-alerts)
   - [儀表板{#dashboards}](#dashboards-dashboards)
   - [資料準備{#data-prep}](#data-prep-data-prep)
   - [目的地 {#destinations}](#destinations-destinations)
   - [體驗資料模型(XDM) {#xdm}](#experience-data-model-xdm-xdm)
   - [身分識別服務{#identity-service}](#identity-service-identity-service)
   - [查詢服務{#query-service}](#query-service-query-service)
   - [分段服務{#segmentation-service}](#segmentation-service-segmentation-service)
   - [來源 {#sources}](#sources-sources)

## 警示 {#alerts}

Experience Platform 可讓您訂閱各種 Platform 活動的事件型警示。您可以透過 Platform 使用者介面中的「[!UICONTROL 警示]」索引標籤訂閱不同的警示規則，而且可以選擇在使用者介面本身內或透過電子郵件通知接收警示訊息。

**新功能或更新功能**

| 功能 | 說明 |
| --- | --- |
| 開發沙箱支援 | 您現在能夠於生產和開發沙箱兩者中[訂閱警示](../../observability/alerts/ui.md)，可以橫跨所有環境進行無縫監視。 |
| 電子郵件範本 | [電子郵件警示](../../observability/alerts/ui.md)現在包含詳細的資產資訊，確保您輕鬆掌握所有的關鍵細節。 |
| 增強的自訂功能 | 您現在可以設定[警示臨界值](../../observability/alerts/ui.md#alert-threshold)，擁有更大的彈性可以針對您的特定需求，按照以下警示類型來量身打造警示：<br><ul><li>客戶細分工作延遲</li><li>客戶細分匯出延遲</li><li>目標資料流執行延遲</li><li>身分服務資料流執行延遲</li><li>輪廓資料流執行延遲</li><li>來源資料流執行延遲</li><li>查詢執行延遲</li><li>超出啟用略過率</li><li>超出來源攝取錯誤率</ul> |
| 擴充警示 | 現在可以訂閱以下[警示規則](../../observability/alerts/rules.md)的稽核事件資訊警示：<br><ul><li>客群建立</li><li>客群更新</li><li>客群刪除</li><li>資料集建立</li><li>資料集更新</li><li>資料集刪除</li><li>綱要建立</li><li>綱要更新</li><li>綱要刪除。 |

{style="table-layout:auto"}

如需有關警示的詳細資訊，請參閱[[!DNL Observability Insights] 概觀](../../observability/home.md)。

## 儀表板 {#dashboards}

Experience Platform 提供多個儀表板，您可以透過這些儀表板檢視每日快照期間擷取之組織資料的重要分析。

**新功能或更新功能**

| 功能 | 說明 |
| --- | --- |
| 授權使用附加元件表格 | 透過核心產品和附加元件的專用表格，取得授權使用情況的精細可見度，並管理您的平台資源。 透過沙箱層級的鑽研檢視追蹤和分析每個核心產品的關鍵量度。 附加量度可與核心產品量度緊密整合，提供使用的全面檢視。 增強的可見度可協助您最佳化授權管理，並根據組織需求調整資源。 如需詳細資訊，請參閱[[!UICONTROL 授權使用情況]儀表板指南](../../dashboards/guides/license-usage.md#overview-tab)。 |
| 查詢專業模式 - 全域篩選器升級 | 利用查詢專業模式的新日期篩選器增強分析功能。使用 SQL 查詢中的動態日期參數來調整深入分析，並依特定時間段篩選資料。透過直覺的使用者介面選擇預設集或自訂日期範圍，使儀表板與所有使用者保持相關性。簡化工作流程、維持準確性，並及時做出決策。如需詳細資訊，請參閱[建立日期篩選器的指南](../../dashboards/data-distiller/query-pro-mode/filters/global-filter.md)。 |
| 查詢專業模式 - 鑽研 | 使用查詢專業模式的鑽研功能進行更深層的深入分析，並從高層次圖表順暢導覽至詳細的儀表板。透過此功能可以輕鬆地將摘要變成深入分析，並探索趨勢、客戶行為和 KPI。自動篩選器傳遞和多層次鑽研能夠使資料保持一致，確保順利進行探索。簡化工作流程、保留情境，並加快決策。如需詳細資訊，請閱讀[建立鑽研的逐步指南](../../dashboards/data-distiller/query-pro-mode/drill-through.md)。 |
| 查詢專業模式 - 進階表格屬性 | 使用查詢專業模式進階表格屬性來簡化資料視覺化、促進工作流程效率，以及提升資料清晰度。直接從自訂儀表板將自動排序、調整大小和分頁功能新增至您的表格中。將欄位進行排序以優先處理關鍵資料、調整大小以達到最佳的可讀性，以及在不修改 SQL 查詢的情況下無縫導覽大型資料集。請參閱「[檢視更多](../../dashboards/data-distiller/query-pro-mode/view-more.md)」指南，了解如何整合這些功能並提升您的資料深入分析。 |
| 總資料量 | 「平均設定檔豐富度」量度已替換為「總資料量」量度。 總資料量是指可用於即時客戶個人檔案的參與和個人化工作流程的總資料量。 您可以在[總計資料磁碟區指南](../../landing/license-usage-and-guardrails/total-data-volume.md)中找到有關這項變更的更多詳細資料。 |

{style="table-layout:auto"}

如需有關儀表板的詳細資訊，包括如何授予存取權限和建立自訂 Widget，請先詳閱[儀表板概觀](../../dashboards/home.md)。

## 資料準備 {#data-prep}

使用資料準備可在體驗資料模型 (XDM) 之間對應、轉換和驗證資料。

**新功能或更新功能**

| 功能 | 說明 |
| --- | --- |
| [!BADGE Beta]{type=Informative} 新的資料準備功能，可供目標使用 | 您現在可以將以下陣列函數用於目標使用案例：<ul><li>`array_to_string`</li><li>`filterArray`</li><li>`transformArray`</li><li>`flattenArray`</li></ul> 如需詳細資訊，請閱讀[資料準備功能指南](../../data-prep/functions.md#arrays)。 |

{style="table-layout:auto"}

如需有關資料準備的詳細資訊，請閱讀[資料準備概觀](../../data-prep/home.md)。

## 目標 {#destinations}

[!DNL Destinations] 是預先建立的和目標平台的整合，可讓來自 Adobe Experience Platform 的資料順暢啟動。您可使用目標啟用已知和未知的資料，以進行跨通路行銷活動、電子郵件行銷活動、設定目標的廣告活動和其他諸多使用案例。

**新目標或更新的目標** {#new-updated-destinations}

| 目標 | 說明 |
| --- | --- |
| [Amazon Ads](/help/destinations/catalog/advertising/amazon-ads.md) | 2024 年 9 月的版本新增了對應選項，用於將 `countryCode` 參數匯出至 Amazon Ads 中。使用 `countryCode` (在[對應步驟](/help/destinations/catalog/advertising/amazon-ads.md#map)中) 來提高您與 Amazon 的身份符合率。 |

{style="table-layout:auto"}

**新功能或更新的功能** {#destinations-new-updated-functionality}

| 功能 | 說明 |
| --- | --- |
| [資料集匯出](/help/destinations/ui/export-datasets.md)增強功能 | 2024 年 9 月版本的 Experience Platform 在資料集匯出功能方面進行了多項增強，為各種資料輸出使用案例提供更好的支援。這些功能增強包括： <ul><li>新的資料夾可設定選項，包括新增和移除子資料夾的選項。</li><li>新的匯出選項，包括完整檔案匯出 (一次) 和指定結束日期的能力</li><li>備註：針對 9 月版本以前建立的所有資料集匯出資料流，Adobe 設定 2025 年 5 月 1 日為預設結束日期。對於任何一項資料流，客戶都必須在結束日期之前手動更新資料流中的結束日期，否則匯出動作將在這個日期停止。</li></ul> <br> ![影像：Experience Platform 使用者介面，特別標示出排程步驟中的「編輯排程」和「編輯資料夾」選項。](../2024/assets/september/edit-schedule-folders.png "在排程步驟中的編輯排程和編輯資料夾選項。"){width="250" align="center" zoomable="yes"} |

{style="table-layout:auto"}

如需詳細資訊，請閱讀[目標概觀](../../destinations/home.md)。

## 體驗資料模式 (XDM) {#xdm}

XDM 是一種開放原始碼的規格，可為帶到 Adobe Experience Platform 中的資料提供通用結構和定義 (結構描述)。若遵守 XDM 標準，即可將所有客戶體驗資料合併到一個常用表述中，以更快速、更整合的方式傳遞分析。您可以從客戶行為中獲得有價值的分析，透過區段定義客戶客群，並使用客戶屬性實現個人化的目的。

**更新的功能**

| 功能 | 說明 |
| --- | --- |
| 綱要編輯器的增強功能 | 透過綱要編輯器中更新的關係工作流程來控制您的綱要關係。直接從 Experience Platform 使用者介面輕鬆更新或移除現有關係，讓綱要管理更順暢、更直覺。自信地調整參考綱要並重新命名關係，確保橫跨不同細分與其他關鍵流程的無縫資料完整性。若要了解更多關於有效管理綱要關係的內容，請參閱[在使用者介面中定義關係欄位](../../xdm/tutorials/relationship-ui.md#create-a-relationship-field-group)以及 [B2B 關係](../../xdm/tutorials/relationship-b2b.md#edit-a-b2b-schema-relationship)的指南。 |

{style="table-layout:auto"}

如需有關 XDM 的詳細資訊，請參閱「[XDM 系統概觀](../../xdm/home.md)」。

## 身分服務 {#identity-service}

使用 Adobe Experience Platform 身分服務，可在裝置及系統間進行身分橋接來建立客戶及其行為的全方位檢視，從而讓您即時實現具影響力的個人數位體驗。

**更新的功能**

| 功能 | 說明 |
| --- | --- |
| 身分圖表連結規則可用性限制 | 身分圖表連結規則是Identity Service中的一套工具，可用來確保使用者的精確個人化。 <ul><li>您現在可以使用[身分最佳化演演算法](../../identity-service/identity-graph-linking-rules/identity-optimization-algorithm.md)來確保身分圖表代表單一人員，因此可防止即時客戶個人檔案中不需要的身分合併。</li><li>設定[名稱空間優先順序](../../identity-service/identity-graph-linking-rules/namespace-priority.md)以定義個別名稱空間的重要性，並影響設定檔的形成和分段方式。</li><li>在UI](../../identity-service/identity-graph-linking-rules/graph-simulation.md)中使用[圖表模擬工具來模擬具有不同組態的身分圖表。</li><li>使用[身分設定介面](../../identity-service/identity-graph-linking-rules/identity-settings-ui.md)指定您唯一的名稱空間，並為您組織中的所有名稱空間建立優先順序。</li><li>有關圖表資料的量度和趨勢，請參閱[身分識別儀表板](../../identity-service/identity-graph-linking-rules/implementation-guide.md#validate-your-graphs)。</li></ul> 若要嘗試使用身分圖表連結規則，請聯絡您的Adobe帳戶團隊，以取得開發沙箱的存取權。 |

**更新的文件**

| 功能 | 說明 |
| --- | --- |
| 識別圖連結規則疑難排解指南 | 請參閱新的[識別圖連結規則疑難排解指南](../../identity-service/identity-graph-linking-rules/troubleshooting.md)，了解您可以採取哪些方法和偵錯解決方案，以解決使用識別圖連結規則時可能遇到的常見問題。 |
| 識別圖連結規則常見問題 | 請參閱新的[識別圖連結規則常見問題](../../identity-service/identity-graph-linking-rules/troubleshooting.md#frequently-asked-questions)，查看有關命名空間優先順序、身分最佳化演算法，以及識別圖連結規則其他方面的常見問題清單。 |

{style="table-layout:auto"}

若要了解更多有關身分服務的資訊，請閱讀「[身分服務概觀](../../identity-service/home.md)」。

## 查詢服務 {#query-service}

查詢服務可讓您使用標準的 SQL 查詢 Adobe Experience Platform 中的資料[!DNL data lake]。您可以加入任何資料湖的資料集，並將查詢結果擷取為新資料集，以用於報表、資料科學工作區或擷取至即時客戶輪廓。

**更新的功能**

| 功能 | 說明 |
| --- | --- |
| 資料蒸餾器客群 | 使用 Experience Platform 資料蒸餾器中的 SQL 客群擴充功能輕鬆建立、管理和啟動客群。直接從資料湖使用 SQL 指令定義客群細分群體，無需使用到輪廓中的原始資料。透過這種彈性的資料驅動方法，調整目標選擇策略並自動將客群同步至檔案型目標。簡化工作流程、最佳化客群管理，並發揮資料的全部潛力。請參閱 [SQL 客群擴充功能使用指南](../../query-service/data-distiller-audiences/overview.md)來提升您的客群策略。 |
| 資料蒸餾器統計 - 超立方體 | 利用超立方體使巨量資料分析最佳化。處理複雜的計算 (例如不重複計數和多維度分析)，無需重新處理歷史資料。以增量方式更新資料、簡化工作流程並縮短處理時間，同時保持準確性和效率。獲得更快速、可擴展且具有成本效益的深入分析，進而改變決策過程。探索[超立方體使用指南](../../query-service/hypercubes/overview.md)，瞭解進階分析。 |
| 查詢編輯器物件瀏覽器 | 使用查詢編輯器中的新物件瀏覽器來提高查詢效率。快速搜尋、篩選和存取資料集，以更快地編寫和調整查詢。透過即時綱要更新和即時表格中繼資料，您可以簡化工作流程、縮短導覽時間並增強您的查詢體驗。發揮資料潛力並將分析最佳化。如需詳細資訊，請參閱[使用物件瀏覽器的指南](../../query-service/ui/user-guide.md#object-browser)。 |
| 計算時數 | 透過已排程查詢的新可見計算時數量度來控制資源使用量。檢視查詢執行層級的計算時數，以監視 CTAS/ITAS 批次查詢的資源使用情況並使其最佳化。追蹤每個查詢執行的開始時間、完成狀態和計算時數。輕鬆微調效能並降低成本。請參閱[計算時數的指南](../../query-service/ui/query-schedules.md#compute-hours-at-job-level)，了解如何發揮最高的查詢效率。 |

{style="table-layout:auto"}

若要了解更多有關查詢服務的資訊，請參閱「[查詢服務概觀](../../query-service/home.md)」。

## Segmentation Service {#segmentation-service}

[!DNL Segmentation Service] 會說明區分客戶群中可行銷的一群人的標準，從而定義輪廓的特定子集。區段的基礎可能是記錄資料 (例如人口統計資訊) 或表示客戶與您的品牌互動的時間序列事件。

**新功能或更新功能**

| 功能 | 說明 |
| ------- | ----------- |
| 串流區段條件更新 | 從2024年9月版本開始，已更新受眾符合串流細分資格的條件。 如需有關這些變更的詳細資訊，請參閱[串流區段適用性准則更新](../../segmentation/eligibility-criteria-update.md)。 |
| 實施整合式搜尋 | 客戶細分工具中的搜尋行為現在開始使用整合式搜尋。此項轉變使得在管理和搜尋客群以重複使用細分群體會籍時能擁有更強大的體驗。如需有關此變更的詳細資訊，請參閱「[客戶細分工具指南](../../segmentation/ui/segment-builder.md#rule-builder-canvas)」。 |

{style="table-layout:auto"}

如需有關 [!DNL Segmentation Service] 的詳細資訊，請參閱「[客戶細分概觀](../../segmentation/home.md)」。

## 來源 {#sources}

Experience Platform 可提供 RESTful API 和互動式 UI，可讓您輕鬆為各種資料提供者設定來源連線。這些來源連線可讓您進行驗證並連線到外部儲存系統和 CRM 服務、設定攝取執行的時間並管理資料攝取輸送量。

使用 Experience Platform 中的來源，即可從 Adobe 應用程式或第三方資料來源攝取資料。

**更新的功能**

| 功能 | 說明 |
| --- | --- |
| [!BADGE Beta]{type=Informative} 使用者介面中攝取加密資料的支援 | 您現在可以使用 Experience Platform 使用者介面中的來源工作區，從雲端儲存空間批次來源攝取加密資料。如需詳細資訊，請參閱[在使用者介面中攝取加密資料](../../sources/tutorials/ui/encryped-ingestion.md)的教學課程。 |
| [!DNL Snowflake Streaming]來源的一般可用性 | [!DNL Snowflake Streaming] 來源現已正式推出。使用此來源將資料自您的 [!DNL Snowflake] 帳戶串流至 Experience Platform。如需詳細資訊，請參閱[[!DNL Snowflake Streaming] 概觀](../../sources/connectors/databases/snowflake-streaming.md)。 |
| [!DNL Google BigQuery] 服務帳戶驗證支援 | 您現在可以使用服務帳戶驗證將您的 [!DNL Google BigQuery] 帳戶連接至 Experience Platform。如需詳細資訊，請參閱[[!DNL Google BigQuery] 概觀](../../sources/connectors/databases/bigquery.md#generate-your-google-bigquery-credentials)。<br> ![影像：Experience Platform 使用者介面，特別標示出排程步驟中的「編輯排程」和「編輯資料夾」選項。](../2024/assets/september/service_auth.png "Google BigQuery 的服務驗證。"){width="250" align="center" zoomable="yes"} |
| 支援跳過樣本資料預覽 | 您現在可以選擇在使用下列來源建立來源連線時跳過資料預覽： <ul><li>[[!DNL Google BigQuery]](../../sources/tutorials/ui/create/databases/bigquery.md#skip-preview-of-sample-data)</li><li>[[!DNL Salesforce]](../../sources/tutorials/ui/create/crm/salesforce.md#skip-preview-of-sample-data)</li><li>[[!DNL Snowflake]](../../sources/tutorials/ui/create/databases/snowflake.md#skip-preview-of-sample-data)</li></ul> 您可以跳過資料預覽，以避免攝取大量批次資料時可能發生的逾時情況。這樣做可能會使已計算欄位和必要欄位停止自動驗證。如果您選擇跳過資料預覽，則您可能必須在對應期間手動驗證已計算欄位和必要欄位。 |
| 支援 [!DNL SFTP] 的禁用分塊功能 | 現在您可以配置一個設定，讓您能夠在 [!DNL SFTP] 來源禁用分塊功能。如需詳細資訊，請參閱[[!DNL SFTP] 概觀](../../sources/connectors/cloud-storage/sftp.md)。 |

{style="table-layout:auto"}

如需詳細資訊，請參閱[來源概觀](../../sources/home.md)。
