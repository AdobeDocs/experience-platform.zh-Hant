---
keywords: Experience Platform;home;popular topics;configure dataflow;advertising connector
solution: Experience Platform
title: 在UI中為廣告連接器配置資料流
topic: overview
type: Tutorial
description: 資料流是從來源擷取資料並將資料擷取至Adobe Experience Platform資料集的排程任務。 本教學課程提供使用廣告帳戶配置新資料流的步驟。
translation-type: tm+mt
source-git-commit: f86f7483e7e78edf106ddd34dc825389dadae26a
workflow-type: tm+mt
source-wordcount: '1462'
ht-degree: 0%

---


# 在UI中為廣告連接器配置資料流

資料流是從來源擷取資料並將資料擷取至Adobe Experience Platform資料集的排程任務。 本教學課程提供使用廣告帳戶配置新資料流的步驟。

## 快速入門

本教學課程需要對Adobe Experience Platform的下列元件有正確的認識：

- [[!DNL Experience Data Model (XDM)] 系統](../../../../xdm/home.md):組織客戶體驗資料 [!DNL Experience Platform] 的標準化架構。
   - [架構構成基礎](../../../../xdm/schema/composition.md):瞭解XDM架構的基本建置區塊，包括架構組合的主要原則和最佳實務。
   - [架構編輯器教程](../../../../xdm/tutorials/create-schema-ui.md):瞭解如何使用架構編輯器UI建立自訂架構。
- [[!DNL Real-time Customer Profile]](../../../../profile/home.md):根據來自多個來源的匯整資料，提供統一、即時的消費者個人檔案。

此外，本教學課程要求您已建立廣告帳戶。 如需在UI中建立不同付款連接器的教學課程清單，請參閱來源連 [接器概觀](../../../home.md)。

## 選擇資料

建立廣告帳戶後，會出現「選 **[!UICONTROL 取資料]** 」步驟，提供互動式介面供您探索檔案階層。

- 介面的左半部分是目錄瀏覽器，顯示伺服器的檔案和目錄。
- 介面的右半部分可讓您從相容檔案中預覽最多100列資料。

您可以使 **[!UICONTROL 用頁面頂端的]** 「搜尋」選項，快速識別您要使用的來源資料。

>[!NOTE]
>
>搜索源資料選項可用於所有基於表格的源連接器，但Analytics、分類、事件集線器和Kinesis連接器除外。

找到源資料後，選擇目錄，然後按一下「下 **[!UICONTROL 一步]**」。

![select-data](../../../images/tutorials/dataflow/all-tabular/select-data.png)


## 將資料欄位對應至XDM架構

此時 **[!UICONTROL 會顯示]** 「映射」步驟，提供互動式介面，將來源資料映射至資料 [!DNL Platform] 集。

選擇要接收傳入資料的資料集。 您可以使用現有資料集或建立新資料集。

### 使用現有資料集

若要將資料內嵌至現有資料集，請選取「使 **[!UICONTROL 用現有資料集]**」，然後按一下資料集圖示。

![use-existing-dataset](../../../images/tutorials/dataflow/advertising/use-existing-target-dataset.png)

將出 **[!UICONTROL 現「選擇資料集]** 」對話框。 尋找您要使用的資料集，選取它，然後按一下「繼 **[!UICONTROL 續]**」。

![select-existing-dataset](../../../images/tutorials/dataflow/advertising/select-existing-dataset.png)

### 使用新資料集

若要將資料新增至新資料集，請選取「 **[!UICONTROL 建立新資料集]** 」，並在提供的欄位中輸入資料集的名稱和說明。

通過在「選擇方案」搜索欄中輸入方案名稱，可以附加 **[!UICONTROL 方案]** 欄位。 您也可以選擇下拉式圖示，查看現有結構的清單。 或者，您也可以選擇「 **[!UICONTROL 進階搜尋]** 」來存取現有結構的畫面，包括其各自的詳細資料。

在此步驟中，您可以啟用資料集， [!DNL Real-time Customer Profile] 並建立實體屬性和行為的整體檢視。 所有啟用資料集的資料都將包含在中，並 [!DNL Profile] 在保存資料流時應用更改。

切換描 **[!UICONTROL 述檔資料集]** 按鈕，以啟用您的目標資料集 [!DNL Profile]。

![create-new-dataset](../../../images/tutorials/dataflow/advertising/target-dataset.png)

將出 **[!UICONTROL 現「選擇模式]** 」對話框。 選擇要應用到新資料集的模式，然後按一下 **[!DNL Done]**。

![select-schema](../../../images/tutorials/dataflow/advertising/select-existing-schema.png)

根據您的需求，您可以選擇直接映射欄位，或使用映射器函式轉換來源資料以衍生計算或計算值。 有關資料映射和映射器函式的詳細資訊，請參閱將CSV資料映 [射到XDM模式欄位的教程](../../../../ingestion/tutorials/map-a-csv-file.md)。

>[!TIP]
>
>[!DNL Platform] 根據您選取的目標架構或資料集，為自動映射欄位提供智慧建議。 您可以手動調整對應規則，以符合您的使用案例。

![](../../../images/tutorials/dataflow/all-tabular/mapping.png)

選 **[!UICONTROL 取預覽資料]** ，查看從選取資料集中最多100列範例資料的對應結果。

在預覽期間，身分欄會優先化為第一個欄位，因為這是驗證映射結果時所需的關鍵資訊。

![](../../../images/tutorials/dataflow/all-tabular/mapping-preview.png)

映射源資料後，選擇「關 **[!UICONTROL 閉」]**。

## 排程擷取執行

此時 **[!UICONTROL 會顯示「排程]** 」步驟，允許您配置提取計畫，以使用配置的映射自動提取選定的源資料。 下表概述了用於計畫的不同可配置欄位：

| 欄位 | 說明 |
| --- | --- |
| 頻率 | 可選頻率 `Once`包括 `Minute`、 `Hour`、 `Day`和 `Week`。 |
| 間隔 | 一個整數，用於設定所選頻率的間隔。 |
| 開始時間 | UTC時間戳記，指示何時設定進行第一次擷取。 |
| 回填 | 一個布爾值，可決定最初收錄的資料。 如果 **[!UICONTROL 啟用回填]** ，則指定路徑中的所有目前檔案將在第一次排程擷取期間被擷取。 如果 **[!UICONTROL 停用「回填]** 」，則只會收錄在首次擷取執行和開始時間之間載入的檔案。 在開始時間之前載入的檔案將不會被收錄。 |
| 增量列 | 具有類型、日期或時間的一組已篩選源架構欄位的選項。 此欄位用於區分新資料和現有資料。 增量資料將根據選取欄的時間戳記進行擷取。 |

資料流設計為在計畫基礎上自動收錄資料。 從選取擷取頻率開始。 接著，設定間隔，以指定兩個流程執行之間的期間。 間隔的值應為非零整數，且應設定為大於或等於15。

若要設定擷取的開始時間，請調整顯示在開始時間方塊中的日期和時間。 或者，您也可以選取日曆圖示來編輯開始時間值。 開始時間必須大於或等於當前UTC時間。

選擇 **[!UICONTROL 載入增量資料]** ，以分配增量列。 此欄位可區分新資料和現有資料。

![調度間隔](../../../images/tutorials/dataflow/databases/schedule-interval-on.png)

### 設定一次性提取資料流

若要設定一次性擷取，請選取頻率下拉箭頭，然後選取「 **[!UICONTROL Once]**」。

>[!TIP]
>
>**[!UICONTROL 在單]** 次擷取期間 **** ，不會顯示間隔和回填。

在為計畫提供適當值後，選擇「下 **[!UICONTROL 一步」]**。

![schedule-once](../../../images/tutorials/dataflow/databases/schedule-once.png)

## 提供資料流詳細資訊

此時將顯示 **[!UICONTROL 資料流詳細資訊]** ，允許您命名新資料流並提供有關新資料流的簡要說明。

在此過程中，您還可以啟用「部 **[!UICONTROL 分提取]** 」和「 **[!UICONTROL 錯誤診斷」]**。 啟用 **[!UICONTROL 部分擷取]** ，可讓您擷取包含錯誤至特定臨界值的資料。 啟用 **[!UICONTROL 部分提取]** ，請拖動「錯誤閾值% **** dial」以調整批的錯誤閾值。 或者，也可以通過選擇輸入框手動調整閾值。 如需詳細資訊，請參閱部 [分批次擷取概觀](../../../../ingestion/batch-ingestion/partial.md)。
為資料流提供值並選擇「下 **[!UICONTROL 一步]**」。

![dataflow-details](../../../images/tutorials/dataflow/all-tabular/dataflow-detail.png)

## 查看資料流

此時 **[!UICONTROL 會出現]** 「查看」步驟，允許您在建立新資料流之前對其進行查看。 詳細資訊會分組在下列類別中：

- **[!UICONTROL 連接]**:顯示源檔案的類型、所選源檔案的相關路徑，以及該源檔案中的列數。
- **[!UICONTROL 指派資料集與地圖欄位]**:顯示源資料被吸收到的資料集，包括資料集所附的模式。
- **[!UICONTROL 排程]**:顯示接收調度的活動期間、頻率和間隔。

複查資料流後，按一下 **[!UICONTROL 完成]** ，並為建立資料流留出一些時間。

![審查](../../../images/tutorials/dataflow/advertising/review.png)

## 監控資料流

建立資料流後，您可以監視通過其獲取的資料，以查看有關提取率、成功和錯誤的資訊。 有關如何監視資料流的詳細資訊，請參見UI中有關監 [視帳戶和資料流的教程](../monitor.md)。

## 刪除資料流

您可以使用「資料流」工作區中的「刪除」功能刪除不再需要或 **[!UICONTROL 建立錯誤的]** 資料流 **** 。 有關如何刪除資料流的詳細資訊，請參見UI中有關 [刪除資料流的教程](../delete.md)。

## 後續步驟

遵循本教學課程，您已成功建立資料流，從行銷自動化系統匯入資料，並深入瞭解監控資料集。 現在，下游服務（例如和）可 [!DNL Platform] 以使用傳入 [!DNL Real-time Customer Profile] 的資料 [!DNL Data Science Workspace]。 如需詳細資訊，請參閱下列檔案：

- [即時客戶個人檔案總覽](../../../../profile/home.md)
- [資料科學工作區概觀](../../../../data-science-workspace/home.md)

## 附錄

以下各節提供了使用源連接器的附加資訊。

### 禁用資料流

建立資料流時，它會立即變為活動狀態，並根據給定的時間表收集資料。 您可以隨時按照以下說明禁用活動資料流。

在「數 **[!UICONTROL 據流]** 」螢幕中，選擇要禁用的資料流的名稱。

![browse-dataset-flow](../../../images/tutorials/dataflow/advertising/view-dataset-flows.png)

「 **[!UICONTROL 屬性]** 」欄會出現在畫面的右側。 此面板包含「啟 **[!UICONTROL 用]** 」切換按鈕。 按一下切換以禁用資料流。 在禁用資料流後，可以使用相同的切換來重新啟用資料流。

![disable](../../../images/tutorials/dataflow/advertising/disable.png)

### 啟用傳入的人口資 [!DNL Profile] 料

來自來源連接器的傳入資料可用於豐富和填入資 [!DNL Real-time Customer Profile] 料。 如需填入資料的詳細資 [!DNL Real-time Customer Profile] 訊，請參閱描述檔填 [入教學課程](../profile.md)。