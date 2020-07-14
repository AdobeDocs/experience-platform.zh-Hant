---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 在UI中為雲儲存流連接器配置資料流
topic: overview
translation-type: tm+mt
source-git-commit: 168ac3a3ab9f475cb26dc8138cbc90a3e35c836d
workflow-type: tm+mt
source-wordcount: '676'
ht-degree: 0%

---


# 在UI中為雲儲存流連接器配置資料流

資料流是從源中檢索資料並將資料收錄到資料集的計畫 [!DNL Platform] 任務。 本教學課程提供使用雲端儲存空間連接器來設定新資料流的步驟。

## 快速入門

本教學課程需要對Adobe Experience Platform的下列元件有正確的認識：

- [體驗資料模型(XDM)系統](../../../../../xdm/home.md): 組織客戶體驗資料 [!DNL Experience Platform] 的標準化架構。
   - [架構構成基礎](../../../../../xdm/schema/composition.md): 瞭解XDM架構的基本建置區塊，包括架構組合的主要原則和最佳實務。
   - [架構編輯器教程](../../../../../xdm/tutorials/create-schema-ui.md): 瞭解如何使用架構編輯器UI建立自訂架構。
- [即時客戶個人檔案](../../../../../profile/home.md): 根據來自多個來源的匯整資料，提供統一、即時的消費者個人檔案。

此外，本教學課程要求您已建立雲端儲存空間連接器。 如需在UI中建立不同雲端儲存空間連接器的教學課程清單，請參閱來源連 [接器概觀](../../../../home.md)。

## 選擇資料

在建立雲端儲存連接器後，會出現「選 *取資料* 」步驟，提供介面供您選擇要從哪個串流串流傳送資料。

![](../../../../images/tutorials/dataflow/cloud-storage/streaming/select-data.png)

## 將資料欄位對應至XDM架構

此時 *會顯示* 「映射」步驟，提供互動式介面，將來源資料映射至資料 [!DNL Platform] 集。

選擇要接收傳入資料的資料集。 您可以使用現有資料集或建立新資料集。

**使用現有資料集**

若要將資料內嵌至現有資料集，請選取「使 **[!UICONTROL 用現有資料集]**」，然後按一下資料集圖示。

![](../../../../images/tutorials/dataflow/cloud-storage/streaming/use-existing-data.png)

將出 _現「選擇資料集_ 」對話框。 尋找您要使用的資料集，選取它，然後按一下「繼 **[!UICONTROL 續]**」。

![](../../../../images/tutorials/dataflow/cloud-storage/streaming/select-existing-data.png)

**使用新資料集**

若要將資料新增至新資料集，請選取「 **[!UICONTROL 建立新資料集]** 」，並在提供的欄位中輸入資料集的名稱和說明。 然後，在下拉式清單下選擇您要使用的架構。

![](../../../../images/tutorials/dataflow/cloud-storage/streaming/use-new-dataset.png)

## 命名資料流

此時將顯示 *[!UICONTROL 資料流詳細資訊]* ，允許您命名新資料流並提供有關新資料流的簡要說明。

提供資料流的值，然後按一下「下 **[!UICONTROL 一步]**」。

![](../../../../images/tutorials/dataflow/cloud-storage/streaming/name-your-dataflow.png)

### 查看資料流

此時 *會出現* 「查看」步驟，允許您在建立新資料流之前對其進行查看。 詳細資訊會分組在下列類別中：

- *[!UICONTROL 來源詳細資訊]*: 顯示源類型和有關源的其他相關詳細資訊。
- *[!UICONTROL 目標詳細資訊]*: 顯示源資料被吸收到的資料集，包括資料集所附的模式。

複查資料流後，按一下 **[!UICONTROL 完成]** ，並為建立資料流留出一些時間。

![](../../../../images/tutorials/dataflow/cloud-storage/streaming/review.png)

## 監視和刪除資料流

建立雲儲存資料流後，您可以監視通過其獲取的資料。 有關監視和刪除資料流的詳細資訊，請參見有關監視資料 [流的教程](../../../../../ingestion/quality/monitor-data-flows.md)。

## 後續步驟

在本教程中，您成功建立了一個資料流，以便從外部雲儲存中導入資料，並獲得了對監控資料集的深入瞭解。 現在，下游服務（例如和）可 [!DNL Platform] 以使用傳入 [!DNL Real-time Customer Profile] 的資料 [!DNL Data Science Workspace]。 如需詳細資訊，請參閱下列檔案：

- [即時客戶個人檔案總覽](../../../../../profile/home.md)
- [資料科學工作區概觀](../../../../../data-science-workspace/home.md)

## 附錄

以下各節提供了使用源連接器的附加資訊。

### 禁用資料流

建立資料流時，它會立即變為活動狀態，並根據給定的時間表收集資料。 您可以隨時按照以下說明禁用活動資料流。

在「來源 *[!UICONTROL 」工作]* 區中，按一下「 **[!UICONTROL 瀏覽]** 」標籤。 接下來，按一下與要禁用的活動資料流關聯的基本連接的名稱。

![](../../../../images/tutorials/dataflow/cloud-storage/streaming/browse.png)

此時將 *[!UICONTROL 顯示「源]* 」活動頁。 從清單中選擇活動資料流，以在螢幕右側開啟其 *Properties* （屬性）列，該列包含 **** Enabled（啟用）切換按鈕。 按一下切換以禁用資料流。 在禁用資料流後，可以使用相同的切換來重新啟用資料流。

![](../../../../images/tutorials/dataflow/cloud-storage/streaming/disable-source.png)

### 啟用傳入的人口資 [!DNL Profile] 料

來自來源連接器的傳入資料可用於豐富和填入資 [!DNL Real-time Customer Profile] 料。 如需填入資料的詳細資 [!DNL Real-time Customer Profile] 訊，請參閱描述檔填 [入教學課程](../../profile.md)。
