---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 在UI中為資料庫連接器配置資料流
topic: overview
translation-type: tm+mt
source-git-commit: d3c725c4760acb3857a67d0d30b24732c963a030
workflow-type: tm+mt
source-wordcount: '1043'
ht-degree: 0%

---


# 在UI中為資料庫連接器配置資料流

資料流是從源中檢索資料並將資料帶入平台資料集的計畫任務。 本教程提供使用資料庫基礎連接器配置新資料流的步驟。

## 快速入門

本教學課程需要對Adobe Experience Platform的下列元件有正確的認識：

- [體驗資料模型(XDM)系統](../../../../xdm/home.md): Experience Platform組織客戶體驗資料的標準化架構。
   - [架構構成基礎](../../../../xdm/schema/composition.md): 瞭解XDM架構的基本建置區塊，包括架構組合的主要原則和最佳實務。
   - [架構編輯器教程](../../../../xdm/tutorials/create-schema-ui.md): 瞭解如何使用架構編輯器UI建立自訂架構。
- [即時客戶個人檔案](../../../../profile/home.md): 根據來自多個來源的匯整資料，提供統一、即時的消費者個人檔案。

此外，本教學課程要求您已建立資料庫連接器。 有關在UI中建立不同資料庫連接器的教學課程清單，請參閱來源連 [接器概觀](../../../home.md)。

## 選擇資料

建立資料庫連接器後，將出 *[!UICONTROL 現「選擇資料]* 」步驟，為您提供一個交互介面以瀏覽資料庫層次。

- 介面的左半部是瀏覽器，顯示您帳戶的資料庫清單。
- 介面的右半部分可讓您預覽最多100列資料。

選擇要使用的資料庫，然後按一下「下 **[!UICONTROL 一步]**」。

![](../../../images/tutorials/dataflow/databases/add-data.png)

## 將資料欄位對應至XDM架構

此時 *會出現* 「對應」步驟，提供互動式介面，將來源資料對應至平台資料集。

選擇要接收傳入資料的資料集。 您可以使用現有資料集或建立新資料集。

### 使用現有資料集

若要將資料內嵌至現有資料集，請選取「 **[!UICONTROL 現有資料集]**」，然後按一下資料集圖示。

![](../../../images/tutorials/dataflow/databases/existing-dataset.png)

將出 *[!UICONTROL 現「選擇資料集]* 」對話框。 尋找您要使用的資料集，選取它，然後按一下「繼 **[!UICONTROL 續]**」。

![](../../../images/tutorials/dataflow/databases/select-existing-dataset.png)

### 使用新資料集

若要將資料新增至新資料集，請選取「 **[!UICONTROL 新資料集]** 」，並在提供的欄位中輸入資料集的名稱和說明。

通過在「選擇方案」搜索欄中鍵入方案名稱，可以附加 **[!UICONTROL 方案欄位]** 。 您也可以選擇下拉式圖示，查看現有結構的清單。 或者，您也可以選擇「 **[!UICONTROL 進階搜尋]** 」來顯示現有結構的畫面，包括其各自的詳細資料。

![](../../../images/tutorials/dataflow/databases/new-dataset.png)

出現*[!UICONTROL Select schema] （選擇架構）對話框。 選擇要應用於新資料集的模式，然後按一下「完 **[!UICONTROL 成」]**。

![](../../../images/tutorials/dataflow/databases/select-existing-schema.png)

您可以根據需要選擇直接映射欄位，或使用映射器函式轉換源資料以導出計算值或計算值。 有關資料映射和映射器函式的詳細資訊，請參閱將CSV資料映 [射到XDM模式欄位的教程](../../../../ingestion/tutorials/map-a-csv-file.md)。

映射源資料後，按一下「下 **[!UICONTROL 一步]**」。

![](../../../images/tutorials/dataflow/databases/mapping.png)

## 排程擷取執行

此時 *[!UICONTROL 會顯示「排程]* 」步驟，允許您配置提取計畫，以使用配置的映射自動提取選定的源資料。 下表概述了用於計畫的不同可配置欄位：

| 欄位 | 說明 |
| --- | --- |
| 頻率 | 可選頻率包括分鐘、小時、日和周。 |
| 間隔 | 一個整數，用於設定所選頻率的間隔。 |
| 開始時間 | UTC時間戳記，將會發生第一次擷取。 |
| 回填 | 一個布爾值，可決定最初收錄的資料。 如果 *啟用回填* ，則指定路徑中的所有目前檔案將在第一次排程擷取期間被擷取。 如果 *停用* 「回填」 *，則只會收錄在首次擷取執行和開始時間之間載入的* 檔案。 在開始時間之前載 *入的檔案* ，將不會收錄。 |
| 增量列 | 具有類型、日期或時間的一組已篩選源架構欄位的選項。 此欄位用於區分新資料和現有資料。 增量資料將根據選取欄的時間戳記進行擷取。 |

資料流設計為在計畫基礎上自動收錄資料。 如果您只想在此工作流程中收錄一次，可以將 **[!UICONTROL Frequency]** （頻率）設為「Day」（日），並套用很大的 **[!UICONTROL Interval]**（例如10000或類似）。

為調度提供值並選擇「下 **[!UICONTROL 一步]**」。

![](../../../images/tutorials/dataflow/databases/schedule.png)

## 命名資料流

出現 *[!UICONTROL 資料流詳細資訊]* ，您必須在其中為資料流提供名稱和可選說明。 完成後 **[!UICONTROL 選擇]** 「下一步」。

![](../../../images/tutorials/dataflow/databases/dataflow-detail.png)

## 查看資料流

此時 *[!UICONTROL 會出現]* 「查看」步驟，允許您在建立新資料流之前對其進行查看。 詳細資訊會分組在下列類別中：

- *連接*: 顯示源檔案的類型、所選源檔案的相關路徑，以及該源檔案中的列數。
- *指派資料集與地圖欄位*: 顯示源資料被吸收到的資料集，包括資料集所附的模式。
- *排程*: 顯示接收調度的活動期間、頻率和間隔。

複查資料流後，按一下 **[!UICONTROL 完成]** ，並為建立資料流留出一些時間。

![](../../../images/tutorials/dataflow/databases/review.png)

## 監控資料流

建立資料流後，您可以監視通過其獲取的資料。 有關如何監視資料流的詳細資訊，請參見有關帳戶和數 [據流的教程](../monitor.md)。

## 後續步驟

通過本教程，您成功建立了一個資料流，以便從外部資料庫導入資料並獲得了對監控資料集的深入瞭解。 現在，下游平台服務（例如即時客戶個人檔案和資料科學工作區）可以使用傳入的資料。 如需詳細資訊，請參閱下列檔案：

- [即時客戶個人檔案總覽](../../../../profile/home.md)
- [資料科學工作區概觀](../../../../data-science-workspace/home.md)

## 附錄

以下各節提供了使用源連接器的附加資訊。

### 禁用資料流

建立資料流時，它會立即變為活動狀態，並根據給定的時間表收集資料。 您可以隨時按照以下說明禁用活動資料流。

在Sources工 *[!UICONTROL 作區]* ，選擇 **[!UICONTROL Dataflows]** 標籤。 接下來，選擇要禁用的資料流。

![](../../../images/tutorials/dataflow/databases/list-of-dataflows.png)

「 *[!UICONTROL 屬性]* 」欄會顯示在畫面的右側，包括「啟用 **** 」切換按鈕。 選擇切換以禁用資料流。 在禁用資料流後，可以使用相同的切換來重新啟用資料流。

![](../../../images/tutorials/dataflow/databases/disable.png)

### 啟用傳入的人口資 [!DNL Profile] 料

來自來源連接器的傳入資料可用於豐富和填入資 [!DNL Real-time Customer Profile] 料。 如需填入資料的詳細資 [!DNL Real-time Customer Profile] 訊，請參閱描述檔填 [入教學課程](../profile.md)。