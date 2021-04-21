---
keywords: Experience Platform;home；熱門主題；監視器帳戶；監視器資料流；資料流；源
description: 本教程提供了使用聚合監視視圖和跨服務監視來監視資料流的步驟。
solution: Experience Platform
title: 在UI中監視源的資料流
topic-legacy: overview
type: Tutorial
exl-id: 53fa4338-c5f8-4e1a-8576-3fe13d930846
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1527'
ht-degree: 0%

---

# 監視UI中源的資料流

在Adobe Experience Platform，資料是從各種來源中提取的，在Experience Platform中分析，並激活到各種目的地。 平台提供資料流透明度，讓追蹤這種可能非線性的資料流程變得更輕鬆。

監控儀表板提供資料流歷程的直觀表示。 您可以使用聚合的監視視圖，並從源級別垂直導航到資料流，以及到資料流運行，從而查看對資料流成功或失敗有貢獻的相應度量。 您還可以使用監控儀表板的跨服務監控能力來監控資料流從源到[!DNL Identity Service]和[!DNL Profile]的過程。

本教程提供了使用聚合監視視圖和跨服務監視來監視資料流的步驟。

## 快速入門

本教學課程需要對Adobe Experience Platform的下列部分有正確的理解：

* [資料流](../home.md):資料流是跨平台移動資料的資料作業的表示。資料流是跨不同服務配置的，有助於將資料從源連接器移動到目標資料集、移動到[!DNL Identity]和[!DNL Profile]以及移動到[!DNL Destinations]。
   * [資料流運行](../../sources/notifications.md):資料流運行是基於所選資料流的頻率配置的循環調度作業。
* [來源](../../sources/home.md):Experience Platform可讓您從各種來源擷取資料，同時讓您能夠使用平台服務來建構、標示並增強傳入資料。
* [身分服務](../../identity-service/home.md):跨裝置和系統橋接身分，以更全面地瞭解個別客戶及其行為。
* [即時客戶個人檔案](../../profile/home.md):根據來自多個來源的匯整資料，提供統一、即時的消費者個人檔案。
* [沙盒](../../sandboxes/home.md):Experience Platform提供虛擬沙盒，可將單一平台實例分割為獨立的虛擬環境，以協助開發和發展數位體驗應用程式。

## 聚合監控視圖

在[平台UI](https://platform.adobe.com)中，從左側導覽器選擇&#x200B;**[!UICONTROL Monitoring]**&#x200B;以存取[!UICONTROL Monitoring]控制面板。 [!UICONTROL Monitoring]控制面板包含所有來源資料流的度量和資訊，包括從來源到[!DNL Identity Service]和[!DNL Profile]之間資料流量狀況的深入資訊。

控制面板的中心是[!UICONTROL Source ingestion]面板，其中包含顯示已收錄記錄和記錄失敗之資料的量度和圖形。

![監控儀表板](../assets/ui/monitor-sources/monitoring-dashboard.png)

依預設，顯示的資料包含過去24小時的擷取率。 選擇&#x200B;**[!UICONTROL Last 24 hours]**&#x200B;以調整顯示的記錄時間範圍。

![變更日期](../assets/ui/monitor-sources/change-date.png)

此時會出現日曆彈出式視窗，提供您替代擷取時間範圍的選項。 選擇&#x200B;**[!UICONTROL Last 30 days]**，然後選擇&#x200B;**[!UICONTROL Apply]**

![調整時間幀](../assets/ui/monitor-sources/adjust-timeframe.png)

圖表預設為啟用，您可停用它們以展開下面的來源清單。 選擇&#x200B;**[!UICONTROL Metrics and graphs]**&#x200B;切換以停用圖形。

![metrics-and-graphs](../assets/ui/monitor-sources/metrics-graphs.png)

| 來源擷取 | 說明 |
| ---------------- | ----------- |
| [!UICONTROL Records ingested ] | 所吸收的記錄總數。 |
| [!UICONTROL Records failed] | 因資料中的錯誤而未收錄的記錄總數。 |
| [!UICONTROL Total failed dataflows] | 狀態為`failed`的資料流總數。 |

來源擷取清單會顯示至少包含一個現有帳戶的所有來源。 該清單還包括有關每個源的接收率、失敗記錄數以及基於所應用時間範圍的失敗資料流總數的資訊。

![源代謝](../assets/ui/monitor-sources/source-ingestion.png)

若要排序來源清單，請選取&#x200B;**[!UICONTROL My sources]**，然後從下拉式選單中選取您的選擇類別。 例如，若要將焦點放在雲端儲存空間，請選取&#x200B;**[!UICONTROL Cloud storage]**

![按類別排序](../assets/ui/monitor-sources/sort-by-category.png)

要查看所有源的所有現有資料流，請選擇&#x200B;**[!UICONTROL Dataflows]**。

![view-all-dataflows](../assets/ui/monitor-sources/view-all-dataflows.png)

或者，您可在搜尋列中輸入來源，以隔離單一來源。 在確定源後，選擇其旁邊的篩選器表徵圖![filter](../assets/ui/monitor-sources/filter.png) ，以查看其活動資料流的清單。

![搜尋](../assets/ui/monitor-sources/search.png)

此時將顯示資料流清單。 要縮小清單範圍並關注出錯的資料流，請選擇&#x200B;**[!UICONTROL Show failures only]**。

![僅顯示失敗](../assets/ui/monitor-sources/show-failures-only.png)

找到要監視的資料流，然後選擇旁邊的篩選器表徵圖![filter](../assets/ui/monitor-sources/filter.png) ，以查看其運行狀態的詳細資訊。

![資料流](../assets/ui/monitor-sources/dataflow.png)

「資料流」運行頁顯示了有關資料流運行開始日期、資料大小、狀態及其處理時間的資訊。 選擇資料流運行開始時間旁邊的過濾器表徵圖![filter](../assets/ui/monitor-sources/filter.png) ，以查看其資料流運行詳細資訊。

![dataflow-run-start](../assets/ui/monitor-sources/dataflow-run-start.png)

[!UICONTROL Dataflow run details]頁顯示資料流的元資料、部分接收狀態和錯誤摘要的資訊。 錯誤摘要包含特定頂層錯誤，顯示擷取程式在哪個步驟發生錯誤。

向下捲動，查看有關所發生錯誤的更多具體資訊。

![dataflow-run-details](../assets/ui/monitor-sources/dataflow-run-details.png)

[!UICONTROL Dataflow run errors]面板顯示導致資料流接收失敗的特定錯誤和錯誤代碼。 在此情形中，發生映射器轉換錯誤，導致24個記錄失敗。

選擇&#x200B;**[!UICONTROL Files]**&#x200B;以瞭解詳細資訊。

![dataflow-run-errors](../assets/ui/monitor-sources/dataflow-run-errors.png)

[!UICONTROL Files]面板包含有關檔案名和路徑的資訊。

如需錯誤的更詳細表示，請選取&#x200B;**[!UICONTROL Preview error diagnostics]**。

![檔案](../assets/ui/monitor-sources/files.png)

出現[!UICONTROL Error diagnostics preview]窗口，在資料流中顯示多達100個錯誤的預覽。 您可以選擇&#x200B;**[!UICONTROL Download]**&#x200B;來檢索捲曲命令，然後允許您下載錯誤診斷程式。

完成後，選擇&#x200B;**[!UICONTROL Close]**

![錯誤診斷](../assets/ui/monitor-sources/error-diagnostics.png)

您可以使用頂端標題的階層連結系統，以導覽回至[!UICONTROL Monitoring]控制面板。 選擇&#x200B;**[!UICONTROL Run start: 2/14/2021, 9:47 PM]**&#x200B;返回上一頁，然後選擇&#x200B;**[!UICONTROL Dataflow: Loyalty Data Ingestion Demo - Failed]**&#x200B;返回資料流頁。

![麵包屑](../assets/ui/monitor-sources/breadcrumbs.png)

## 跨服務監控

儀表板的上半部分包含從源級到[!DNL Identity Service]和[!DNL Profile]的接收流的表示。 每個儲存格包含一個點標籤，用以指出擷取階段發生的錯誤。 綠點表示無錯誤的擷取，而紅點表示該特定擷取階段發生錯誤。

![跨服務監控](../assets/ui/monitor-sources/cross-service-monitoring.png)

從「資料流」頁中，找到成功的資料流，並選擇其旁邊的篩選器表徵圖![filter](../assets/ui/monitor-sources/filter.png) ，以查看其資料流運行資訊。

![資料流成功](../assets/ui/monitor-sources/dataflow-success.png)

[!UICONTROL Source ingestion]頁包含確認資料流成功接收的資訊。 從這裡，您可以開始監控資料流從源級到[!DNL Identity Service] ，然後到[!DNL Profile]的過程。

選擇&#x200B;**[!UICONTROL Identities]**&#x200B;以查看[!UICONTROL Identities]階段中的攝取。

![來源](../assets/ui/monitor-sources/sources.png)

### [!DNL Identity] 量度

[!UICONTROL Identity processing]頁包含有關接收到[!DNL Identity Service]的記錄的資訊，包括添加的身份數、建立的圖形和更新的圖形。

選擇資料流運行開始時間旁邊的過濾器表徵圖![filter](../assets/ui/monitor-sources/filter.png) ，以查看有關[!DNL Identity]資料流運行的詳細資訊。

![身份](../assets/ui/monitor-sources/identities.png)

| 身分度量 | 說明 |
| ---------------- | ----------- |
| [!UICONTROL Records received] | 從[!DNL Data Lake]收到的記錄數。 |
| [!UICONTROL Records failed] | 因資料錯誤而未收錄到平台的記錄數。 |
| [!UICONTROL Records skipped] | 由於記錄行中只有一個標識符，所以已收錄但未收錄到[!DNL Identity Service]中的記錄數。 |
| [!UICONTROL Records ingested] | 接收到[!DNL Identity Service]的記錄數。 |
| [!UICONTROL Total records] | 所有記錄的總計計數，包括失敗記錄、跳過記錄、添加[!DNL Identities]和複製記錄。 |
| [!UICONTROL Identities added] | 新增至[!DNL Identity Service]的新識別碼淨額數。 |
| [!UICONTROL Graphs created] | 在[!DNL Identity Service]中建立的淨新身份圖數。 |
| [!UICONTROL Graphs updated] | 使用新邊更新的現有身份圖數。 |
| [!UICONTROL Failed dataflow runs] | 失敗的資料流運行數。 |
| [!UICONTROL Processing time] | 從擷取開始到完成的時間戳記。 |
| [!UICONTROL Status] | 定義資料流的整體狀態。 可能的狀態值為： <ul><li>`Success`:表示資料流處於活動狀態，並正在根據提供的時間表接收資料。</li><li>`Failed`:表示資料流的激活過程因錯誤而中斷。 </li><li>`Processing`:表示資料流尚未激活。建立新資料流後，通常會立即出現此狀態。</li></ul> |

「[!UICONTROL Dataflow run details]」頁顯示有關[!DNL Identity]資料流運行的詳細資訊，包括其IMS組織ID和資料流運行ID。 此頁還顯示[!DNL Identity Service]提供的對應錯誤代碼和錯誤消息，如果擷取過程中出現任何錯誤。

選擇&#x200B;**[!UICONTROL Run start: 2/14/2021, 9:47 PM]**&#x200B;返回上一頁。

![identity-dataflow run](../assets/ui/monitor-sources/identities-dataflow-run.png)

從[!UICONTROL Identity processing]頁面，選擇&#x200B;**[!UICONTROL Profiles]**&#x200B;以查看[!UICONTROL Profiles]階段中記錄提取的狀態。

![select-profiles](../assets/ui/monitor-sources/select-profiles.png)

### [!DNL Profile] 量度

[!UICONTROL Profile processing]頁包含有關接收到[!DNL Profile]的記錄的資訊，包括建立的配置檔案片段數、更新的配置檔案片段數以及配置檔案片段總數。

選擇資料流運行開始時間旁邊的過濾器表徵圖![filter](../assets/ui/monitor-sources/filter.png) ，以查看有關[!DNL Profile]資料流運行的詳細資訊。

![描述檔](../assets/ui/monitor-sources/profiles.png)

| 描述檔度量 | 說明 |
| --------------- | ----------- |
| [!UICONTROL Records received] | 從[!DNL Data Lake]收到的記錄數。 |
| [!UICONTROL Records failed ] | 由於錯誤而吸收但未放入[!DNL Profile]的記錄數。 |
| [!UICONTROL Profile fragments added] | 新增的淨新[!DNL Profile]片段數。 |
| [!UICONTROL Profile fragments updated] | 已更新的現有[!DNL Profile]片段數 |
| [!UICONTROL Total Profile fragments] | 寫入[!DNL Profile]的記錄總數，包括所有已更新的[!DNL Profile]片段和新的[!DNL Profile]片段。 |
| [!UICONTROL Failed dataflow runs] | 失敗的資料流運行數。 |
| [!UICONTROL Processing time] | 從擷取開始到完成的時間戳記。 |
| [!UICONTROL Status] | 定義資料流的整體狀態。 可能的狀態值為： <ul><li>`Success`:表示資料流處於活動狀態，並正在根據提供的時間表接收資料。</li><li>`Failed`:表示資料流的激活過程因錯誤而中斷。 </li><li>`Processing`:表示資料流尚未激活。建立新資料流後，通常會立即出現此狀態。</li></ul> |

「[!UICONTROL Dataflow run details]」頁顯示有關[!DNL Profile]資料流運行的詳細資訊，包括其IMS組織ID和資料流運行ID。 此頁還顯示[!DNL Profile]提供的對應錯誤代碼和錯誤消息，如果擷取過程中出現任何錯誤。

![profiles-dataflow run](../assets/ui/monitor-sources/profiles-dataflow-run.png)

## 後續步驟

通過本教程，您已使用&#x200B;**[!UICONTROL Monitoring]**&#x200B;儀表板成功監視從源級到[!DNL Identity Service]和[!DNL Profile]的接收資料流。 您還成功地識別了導致資料流在提取過程中失敗的錯誤。 如需詳細資訊，請參閱下列檔案：

* [即時客戶個人檔案總覽](../../profile/home.md)
* [資料科學工作區概觀](../../data-science-workspace/home.md)
