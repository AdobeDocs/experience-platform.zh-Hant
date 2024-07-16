---
keywords: Experience Platform；首頁；熱門主題；對應csv；對應csv檔案；將csv檔案對應至xdm；將csv對應至xdm；ui指南；
solution: Experience Platform
title: 將CSV檔案對應至現有的XDM結構描述
type: Tutorial
description: 本教學課程涵蓋如何使用Adobe Experience Platform使用者介面將CSV檔案對應至現有的XDM結構描述。
exl-id: 15f55562-269d-421d-ad3a-5c10fb8f109c
source-git-commit: e802932dea38ebbca8de012a4d285eab691231be
workflow-type: tm+mt
source-wordcount: '944'
ht-degree: 1%

---

# 將CSV檔案對應至現有的XDM結構描述

>[!NOTE]
>
>本文介紹如何將CSV檔案對應至現有的XDM結構描述。 如需有關如何使用AI產生的結構描述建議工具（目前為測試版）的資訊，請參閱[使用機器學習建議對應CSV檔案](./recommendations.md)上的檔案。

為了將CSV資料擷取到[!DNL Adobe Experience Platform]，資料必須對應到[!DNL Experience Data Model] (XDM)結構描述。 本教學課程涵蓋如何使用[!DNL Platform]使用者介面將CSV檔案對應到XDM結構描述。

## 快速入門

此教學課程需要您實際瞭解[!DNL Platform]的下列元件：

- [[!DNL Experience Data Model (XDM System)]](../../../xdm/home.md)： [!DNL Platform]用來組織客戶體驗資料的標準化架構。
- [批次擷取](../../batch-ingestion/overview.md)： [!DNL Platform]從使用者提供的資料檔擷取資料的方法。
- [Adobe Experience Platform資料準備](../../batch-ingestion/overview.md)：功能套件，可讓您對應及轉換擷取的資料，以符合XDM結構描述。 有關[資料準備函式](../../../data-prep/functions.md)的檔案與結構描述對應特別相關。

本教學課程也要求您已建立資料集以將CSV資料擷取到。 如需在UI中建立資料集的步驟，請參閱[資料擷取教學課程](../ingest-batch-data.md)。

## 選擇目的地

登入[[!DNL Adobe Experience Platform]](https://platform.adobe.com)，然後從左側導覽列中選取&#x200B;**[!UICONTROL 工作流程]**&#x200B;以存取&#x200B;**[!UICONTROL 工作流程]**&#x200B;工作區。

在&#x200B;**[!UICONTROL 工作流程]**&#x200B;畫面中，選取&#x200B;**[!UICONTROL 資料擷取]**&#x200B;區段下的&#x200B;**[!UICONTROL 將CSV對應至XDM結構描述]**，然後選取&#x200B;**[!UICONTROL 啟動]**。

![](../../images/tutorials/map-a-csv-file/workflows.png)

**[!UICONTROL 將CSV對應至XDM結構描述]**&#x200B;工作流程隨即出現，從&#x200B;**[!UICONTROL 目的地]**&#x200B;步驟開始。 選擇要將傳入資料擷取的資料集。 您可以使用現有的資料集或建立新的資料集。

**使用現有的資料集**

若要將CSV資料內嵌到現有的資料集中，請選取「**[!UICONTROL 使用現有的資料集]**」。 您可以使用搜尋函式，或透過捲動面板中的現有資料集清單來擷取現有資料集。

![](../../images/tutorials/map-a-csv-file/use-existing-dataset.png)

若要將CSV資料擷取至新資料集，請選取&#x200B;**[!UICONTROL 建立新資料集]**，然後在提供的欄位中輸入資料集的名稱和說明。 使用搜尋功能或捲動提供的結構描述清單，以選取結構描述。 選取&#x200B;**[!UICONTROL 下一步]**&#x200B;以繼續。

![](../../images/tutorials/map-a-csv-file/create-new-dataset.png)

## 新增資料

**[!UICONTROL 新增資料]**&#x200B;步驟隨即顯示。 將CSV檔案拖放至提供的空間，或選取&#x200B;**[!UICONTROL 選擇檔案]**&#x200B;以手動輸入您的CSV檔案。

![](../../images/tutorials/map-a-csv-file/add-data.png)

上傳檔案後，**[!UICONTROL 範例資料]**&#x200B;區段就會顯示，顯示前10列的資料。 確認資料已如預期上傳後，請選取&#x200B;**[!UICONTROL 下一步]**。

![](../../images/tutorials/map-a-csv-file/sample-data.png)

## 將CSV欄位對應至XDM結構描述欄位

**[!UICONTROL 對應]**&#x200B;步驟出現。 CSV檔案的欄列在&#x200B;**[!UICONTROL Source欄位]**&#x200B;下，其對應的XDM結構描述欄位列在&#x200B;**[!UICONTROL 目標欄位]**&#x200B;下。

[!DNL Platform]會根據您選取的目標結構描述或資料集，自動提供智慧型建議給自動對應的欄位。 您可以手動調整對應規則以符合您的使用案例。

![](../../images/tutorials/map-a-csv-file/mapping-with-suggestions.png)

若要接受所有自動產生的對應值，請選取標示為「[!UICONTROL 接受所有目標欄位]」的核取方塊。

![](../../images/tutorials/map-a-csv-file/filled-mapping-with-suggestions.png)

有時候，來源結構描述會提供多個建議。 發生此情況時，對應卡片會顯示最顯著的建議，後面跟著包含其他可用建議數量的藍色圓圈。 選取燈泡圖示會顯示其他建議的清單。 您可以選取要對應的建議旁邊的核取方塊，以選擇其中一個替代建議。

![](../../images/tutorials/map-a-csv-file/multiple-recommendations.png)

或者，您可以選擇手動將來源結構描述對應到目標結構描述。 將游標停留在您要對應的來源結構描述上，然後選取加號圖示。

![](../../images/tutorials/map-a-csv-file/mapping-with-suggestions-and-buttons.png)

出現&#x200B;**[!UICONTROL 將來源對應到目標欄位]**&#x200B;彈出視窗。 從這裡，您可以選取要對應的欄位，然後按一下&#x200B;**[!UICONTROL 儲存]**&#x200B;以新增對應。

![](../../images/tutorials/map-a-csv-file/manual-mapping.png)

如果要移除其中一個對應，請將游標移至該對應上，然後選取減號圖示。

### 新增計算欄位 {#add-calculated-field}

計算欄位允許根據輸入結構描述中的屬性建立值。 然後可以將這些值指派給目標架構中的屬性，並提供名稱和說明以便更輕鬆地參考。

選取&#x200B;**[!UICONTROL 新增計算欄位]**&#x200B;按鈕以繼續。

![](../../images/tutorials/map-a-csv-file/add-calculated-field.png)

**[!UICONTROL 建立計算欄位]**&#x200B;面板隨即顯示。 左側對話方塊包含計算欄位支援的欄位、函式和運運算元。 選取其中一個標籤，以開始將函式、欄位或運運算元新增至運算式編輯器。

![](../../images/tutorials/map-a-csv-file/create-calculated-fields.png)

| 標記 | 說明 |
| --------- | ----------- |
| 欄位 | 欄位索引標籤會列出來源結構描述中可用的欄位和屬性。 |
| 函數 | 函式標籤會列出可用來轉換資料的函式。 若要深入瞭解您可以在計算欄位中使用的函式，請參閱[使用資料準備（對應程式）函式](../../../data-prep/functions.md)的指南。 |
| 操作者 | 運運算元索引標籤會列出可用於轉換資料的運運算元。 |

您可以使用中央的運算式編輯器，手動新增欄位、函式和運運算元。 選取編輯器以開始建立運算式。

![](../../images/tutorials/map-a-csv-file/create-calculated-field.png)

選取&#x200B;**[!UICONTROL 儲存]**&#x200B;以繼續。

對應畫面會重新出現，並顯示您新建立的來源欄位。 套用適當的對應目標欄位並選取&#x200B;**[!UICONTROL 完成]**&#x200B;以完成對應。

![](../../images/tutorials/map-a-csv-file/new-calculated-field.png)

## 監視資料擷取

對應和建立CSV檔案後，您就可以監視透過該檔案擷取的資料。 如需有關監視資料擷取的詳細資訊，請參閱有關[監視資料擷取](../../../ingestion/quality/monitor-data-ingestion.md)的教學課程。

## 後續步驟

依照本教學課程中的指示，您已成功將一般CSV檔案對應至XDM結構描述，並將其擷取至[!DNL Platform]。 此資料現在可供下游[!DNL Platform]服務（例如[!DNL Real-Time Customer Profile]）使用。 如需詳細資訊，請參閱[[!DNL Real-Time Customer Profile]](../../../profile/home.md)的概觀。
