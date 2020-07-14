---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 在UI中為協定連接器配置資料流
topic: overview
translation-type: tm+mt
source-git-commit: 168ac3a3ab9f475cb26dc8138cbc90a3e35c836d
workflow-type: tm+mt
source-wordcount: '1071'
ht-degree: 1%

---


# 在UI中為協定連接器配置資料流

資料集流程是排程的工作，可從來源擷取資料並將資料擷取至Adobe Experience Platform資料集。 本教學課程提供使用通訊協定帳戶設定新資料集流程的步驟。

## 快速入門

本教學課程需要對Adobe Experience Platform的下列元件有正確的認識：

- [體驗資料模型(XDM)系統](../../../../xdm/home.md): 組織客戶體驗資料 [!DNL Experience Platform] 的標準化架構。
   - [架構構成基礎](../../../../xdm/schema/composition.md): 瞭解XDM架構的基本建置區塊，包括架構組合的主要原則和最佳實務。
   - [架構編輯器教程](../../../../xdm/tutorials/create-schema-ui.md): 瞭解如何使用架構編輯器UI建立自訂架構。
- [即時客戶個人檔案](../../../../profile/home.md): 根據來自多個來源的匯整資料，提供統一、即時的消費者個人檔案。

此外，本教學課程要求您已建立通訊協定帳戶。 如需在UI中建立不同通訊協定連接器的教學課程清單，請參閱來源連 [接器概觀](../../../home.md)。

## 選擇資料

建立通訊協定帳戶後，會出 *[!UICONTROL 現「選取資料]* 」步驟，提供互動式介面供您探索檔案階層。

- 介面的左半部分是目錄瀏覽器，顯示伺服器的檔案和目錄。
- 介面的右半部分可讓您從相容檔案中預覽最多100列資料。

選擇您要使用的目錄，然後按一下「下 **[!UICONTROL 一步]**」。

![添加資料](../../../images/tutorials/dataflow/protocols/add-data.png)

## 將資料欄位對應至XDM架構

此時 *[!UICONTROL 會出現]* 「對應」步驟，提供互動式介面，將來源資料對應至 [!UICONTROL Platform] 資料集。

選擇要接收傳入資料的資料集。 您可以使用現有資料集或建立新資料集。

### 使用現有資料集

若要將資料內嵌至現有資料集，請選取「使 **[!UICONTROL 用現有資料集]**」，然後按一下資料集圖示。

![use-existing-dataset](../../../images/tutorials/dataflow/protocols/use-existing-dataset.png)

將出 *[!UICONTROL 現「選擇資料集]* 」對話框。 尋找您要使用的資料集，選取它，然後按一下「繼 **[!UICONTROL 續]**」。

![select-existing-dataset](../../../images/tutorials/dataflow/protocols/select-existing-dataset.png)

### 使用新資料集

若要將資料新增至新資料集，請選取「 **[!UICONTROL 建立新資料集]** 」，並在提供的欄位中輸入資料集的名稱和說明。

在此過程中，您還可以啟用「部 *[!UICONTROL 分提取]* 」和「 *[!UICONTROL 錯誤診斷」]*。 啟用 *[!UICONTROL 部分擷取]* ，可讓您擷取包含錯誤的資料，最多可設定特定臨界值。 啟用錯誤診斷可提供任何個別批次錯誤資料的詳細資訊。 如需詳細資訊，請參閱部 [分批次擷取概觀](../../../../ingestion/batch-ingestion/partial.md)。

完成後，按一下架構表徵圖。

![create-new-dataset](../../../images/tutorials/dataflow/protocols/use-new-dataset.png)

將出 *[!UICONTROL 現「選擇模式]* 」對話框。 選擇要應用於新資料集的模式，然後按一下「完 **[!UICONTROL 成」]**。

![select-schema](../../../images/tutorials/dataflow/protocols/select-existing-schema.png)

您可以根據需要選擇直接映射欄位，或使用映射器函式轉換源資料以導出計算值或計算值。 有關資料映射和映射器函式的詳細資訊，請參閱將CSV資料映 [射到XDM模式欄位的教程](../../../../ingestion/tutorials/map-a-csv-file.md)。

「映 *[!UICONTROL 射]* 」螢幕還允許您設定 *[!UICONTROL 「增量」列]*。 建立資料集流時，可以設定任何時間戳欄位作為基準，以決定在計畫增量提取中提取哪些記錄。

映射源資料後，按一下「下 **[!UICONTROL 一步]**」。

![](../../../images/tutorials/dataflow/protocols/mapping.png)

此時 *[!UICONTROL 會顯示「排程]* 」步驟，允許您配置提取計畫，以使用配置的映射自動提取選定的源資料。 下表概述了用於計畫的不同可配置欄位：

| 欄位 | 說明 |
| --- | --- |
| 頻率 | 可選頻率包括分鐘、小時、日和周。 |
| 間隔 | 一個整數，用於設定所選頻率的間隔。 |
| 開始時間 | UTC時間戳記，將會發生第一次擷取。 |
| 回填 | 一個布爾值，可決定最初收錄的資料。 如果 *[!UICONTROL 啟用回填]* ，則指定路徑中的所有目前檔案將在第一次排程擷取期間被擷取。 如果 *[!UICONTROL 停用]* 「回填」 *[!UICONTROL ，則只會收錄在首次擷取執行和開始時間之間載入的]* 檔案。 在開始時間之前載 *[!UICONTROL 入的檔案]* ，將不會收錄。 |

資料流設計為在計畫基礎上自動收錄資料。 如果您只想在此工作流程中收錄一次，可以將 **[!UICONTROL Frequency]** （頻率）設為「Day」（日），並套用很大的 **[!UICONTROL Interval]**（例如10000或類似）。

提供計畫值，然後按一下「下 **[!UICONTROL 一步]**」。

![調度](../../../images/tutorials/dataflow/protocols/scheduling.png)

## 命名資料流

此時 *[!UICONTROL 會顯示資料集流程詳細資料]* ，您必須在其中提供資料集流程的名稱和選用說明。 完成後，按&#x200B;**[!UICONTROL 「下一步」]**。

![dataset-flow-details](../../../images/tutorials/dataflow/protocols/dataset-flow-details.png)

## 查看資料流

此時 *[!UICONTROL 會出現]* 「查看」步驟，允許您在建立新資料流之前對其進行查看。 詳細資訊會分組在下列類別中：

- *[!UICONTROL 連接]*: 顯示源檔案的類型、所選源檔案的相關路徑，以及該源檔案中的列數。
- *[!UICONTROL 指派資料集與地圖欄位]*: 顯示源資料被吸收到的資料集，包括資料集所附的模式。
- *[!UICONTROL 排程]*: 顯示接收調度的活動期間、頻率和間隔。

複查資料流後，按一下 **[!UICONTROL 完成]** ，並為建立資料流留出一些時間。

![審查](../../../images/tutorials/dataflow/protocols/review.png)

## 監視和刪除資料流

建立資料流後，您可以監視通過其獲取的資料。 有關如何監視和刪除資料流的詳細資訊，請參見有關監視和刪 [除資料流的教程](../monitor.md)。

## 後續步驟

透過本教學課程，您已成功建立資料集流程，從行銷自動化系統匯入資料，並深入瞭解監控資料集。 現在，下游服務（例如和）可 [!DNL Platform] 以使用傳入 [!DNL Real-time Customer Profile] 的資料 [!DNL Data Science Workspace]。 如需詳細資訊，請參閱下列檔案：

- [即時客戶個人檔案總覽](../../../../profile/home.md)
- [資料科學工作區概觀](../../../../data-science-workspace/home.md)

## 附錄

以下各節提供了使用源連接器的附加資訊。

### 停用資料集流

當建立資料集流程時，資料集流程會立即變為作用中，並依據給定的排程來擷取資料。 您隨時都可以依照下列指示停用作用中的資料集流程。

在「資 *[!UICONTROL 料集流]* 」畫面中，選取您要停用的資料集流程名稱。

![browse-dataset-flow](../../../images/tutorials/dataflow/protocols/view-dataset-flows.png)

「 *[!UICONTROL 屬性]* 」欄會出現在畫面的右側。 此面板包含「啟 **[!UICONTROL 用]** 」切換按鈕。 按一下切換以禁用資料流。 在禁用資料流後，可以使用相同的切換來重新啟用資料流。

![disable](../../../images/tutorials/dataflow/protocols/disable.png)

### 啟用傳入的人口資 [!DNL Profile] 料

來自來源連接器的傳入資料可用於豐富和填入資 [!DNL Real-time Customer Profile] 料。 如需填入資料的詳細資 [!DNL Real-time Customer Profile] 訊，請參閱描述檔填 [入教學課程](../profile.md)。