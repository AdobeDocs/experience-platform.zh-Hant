---
keywords: Experience Platform；首頁；熱門主題；雲儲存連接器；雲儲存
solution: Experience Platform
title: 在UI中為雲儲存流連接器配置資料流
topic-legacy: overview
type: Tutorial
description: 資料流是從源中檢索資料並將資料帶入平台資料集的計畫任務。 本教學課程提供使用雲端儲存空間連接器來設定新資料流的步驟。
exl-id: 75deead6-ef3c-48be-aed2-c43d1f432178
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '680'
ht-degree: 1%

---

# 在UI中為雲儲存流連接配置資料流

資料流是從源中檢索資料並將資料帶入[!DNL Platform]資料集的計畫任務。 本教學課程提供使用雲端儲存空間連接器來設定新資料流的步驟。

## 快速入門

本教學課程需要對Adobe Experience Platform的下列部分有正確的理解：

- [[!DNL Experience Data Model (XDM)] 系統](../../../../../xdm/home.md):組織客戶體驗資 [!DNL Experience Platform] 料的標準化架構。
   - [架構構成基礎](../../../../../xdm/schema/composition.md):瞭解XDM架構的基本建置區塊，包括架構組合的主要原則和最佳實務。
   - [架構編輯器教程](../../../../../xdm/tutorials/create-schema-ui.md):瞭解如何使用架構編輯器UI建立自訂架構。
- [[!DNL Real-time Customer Profile]](../../../../../profile/home.md):根據來自多個來源的匯整資料，提供統一、即時的消費者個人檔案。

此外，本教學課程要求您已建立雲端儲存空間連接器。 有關在UI中建立不同雲端儲存空間連接器的教學課程清單，請參閱[來源連接器概述](../../../../home.md)。

## 選擇資料

在建立雲端儲存連接器後，會出現「選取資料&#x200B;*」步驟，提供介面供您選取要從哪個串流串流傳送資料。*

![](../../../../images/tutorials/dataflow/cloud-storage/streaming/select-data.png)

## 將資料欄位對應至XDM架構

出現&#x200B;**[!UICONTROL Mapping]**&#x200B;步驟，提供互動式介面，將來源資料對應至[!DNL Platform]資料集。

選擇要接收傳入資料的資料集。 您可以使用現有資料集或建立新資料集。

**使用現有資料集**

若要將資料內嵌至現有資料集，請選取&#x200B;**[!UICONTROL Use existing dataset]**，然後按一下資料集圖示。

![](../../../../images/tutorials/dataflow/cloud-storage/streaming/use-existing-data.png)

出現&#x200B;**[!UICONTROL Select dataset]**&#x200B;對話框。 尋找您要使用的資料集，選取它，然後按一下&#x200B;**[!UICONTROL Continue]**。

![](../../../../images/tutorials/dataflow/cloud-storage/streaming/select-existing-data.png)

**使用新資料集**

若要將資料內嵌至新資料集，請選取&#x200B;**[!UICONTROL Create new dataset]**，並在提供的欄位中輸入資料集的名稱和說明。 然後，在下拉式清單下選擇您要使用的架構。

![](../../../../images/tutorials/dataflow/cloud-storage/streaming/use-new-dataset.png)

## 命名資料流

出現&#x200B;**[!UICONTROL Dataflow detail]**&#x200B;步驟，允許您命名新資料流並提供有關新資料流的簡要說明。

提供資料流的值，然後按一下&#x200B;**[!UICONTROL Next]**。

![](../../../../images/tutorials/dataflow/cloud-storage/streaming/name-your-dataflow.png)

### 查看資料流

出現&#x200B;**[!UICONTROL Review]**&#x200B;步驟，允許您在建立新資料流之前對其進行查看。 詳細資訊會分組在下列類別中：

- **[!UICONTROL Source details]**:顯示源類型和有關源的其他相關詳細資訊。
- **[!UICONTROL Target details]**:顯示源資料被吸收到的資料集，包括資料集所附的模式。

複查資料流後，按一下&#x200B;**[!UICONTROL Finish]** ，並為建立資料流留出一些時間。

![](../../../../images/tutorials/dataflow/cloud-storage/streaming/review.png)

## 監視和刪除資料流

建立雲儲存資料流後，您可以監視通過其獲取的資料。 有關監視和刪除資料流的詳細資訊，請參見[監視資料流](../../../../../ingestion/quality/monitor-data-ingestion.md)的教程。

## 後續步驟

在本教程中，您成功建立了一個資料流，以便從外部雲儲存中導入資料，並獲得了對監控資料集的深入瞭解。 現在，下游[!DNL Platform]服務（例如[!DNL Real-time Customer Profile]和[!DNL Data Science Workspace]）可以使用傳入的資料。 如需詳細資訊，請參閱下列檔案：

- [[!DNL Real-time Customer Profile] 概觀](../../../../../profile/home.md)
- [[!DNL Data Science Workspace] 概觀](../../../../../data-science-workspace/home.md)

## 附錄

以下各節提供了使用源連接器的附加資訊。

### 禁用資料流

建立資料流時，它會立即變為活動狀態，並根據給定的時間表收集資料。 您可以隨時按照以下說明禁用活動資料流。

在&#x200B;**[!UICONTROL Sources]**&#x200B;工作區中，按一下&#x200B;**[!UICONTROL Browse]**&#x200B;頁籤。 接著，按一下與要禁用的活動資料流關聯的連接的名稱。

![](../../../../images/tutorials/dataflow/cloud-storage/streaming/browse.png)

此時將顯示&#x200B;**[!UICONTROL Source activity]**&#x200B;頁。 從清單中選擇活動資料流，以在螢幕右側開啟其&#x200B;**[!UICONTROL Properties]**&#x200B;列，該列包含&#x200B;**[!UICONTROL Enabled]**&#x200B;切換按鈕。 按一下切換以禁用資料流。 在禁用資料流後，可以使用相同的切換來重新啟用資料流。

![](../../../../images/tutorials/dataflow/cloud-storage/streaming/disable-source.png)

### 啟用[!DNL Profile]人口的傳入資料

來自源連接器的入站資料可用於豐富和填充[!DNL Real-time Customer Profile]資料。 如需填入[!DNL Real-time Customer Profile]資料的詳細資訊，請參閱[描述檔填入](../../profile.md)的教學課程。
