---
keywords: Experience Platform；首頁；熱門主題；map csv;map csv;map csv file;map csv file to xdm;map csv to xdm;ui指南；
solution: Experience Platform
title: 將CSV檔案對應至XDM架構
topic-legacy: tutorial
type: Tutorial
description: 本教學課程介紹如何使用Adobe Experience Platform用戶介面將CSV檔案映射到XDM架構。
exl-id: 15f55562-269d-421d-ad3a-5c10fb8f109c
translation-type: tm+mt
source-git-commit: 0e79d339ddc0301486ea3e53a3fd52877ff6a2c8
workflow-type: tm+mt
source-wordcount: '828'
ht-degree: 1%

---

# 將CSV檔案對應至XDM架構

為了將CSV資料內嵌至[!DNL Adobe Experience Platform]，資料必須對應至[!DNL Experience Data Model](XDM)架構。 本教學課程介紹如何使用[!DNL Platform]使用者介面將CSV檔案對應至XDM架構。

此外，本教學課程的附錄還提供了有關使用[映射函式](#mapping-functions)的詳細資訊。

## 快速入門

本教學課程需要對[!DNL Platform]的下列元件有正確的理解：

- [[!DNL Experience Data Model (XDM System)]](../../xdm/home.md):組織客戶體驗資 [!DNL Platform] 料的標準化架構。
- [[!DNL Batch ingestion]](../batch-ingestion/overview.md):從用戶提供的 [!DNL Platform] 資料檔案中收集資料的方法。

本教學課程也要求您已建立資料集，以將CSV資料收錄至。 如需在UI中建立資料集的步驟，請參閱[資料收錄教學課程](./ingest-batch-data.md)。

## 選擇目標

登入[[!DNL Adobe Experience Platform]](https://platform.adobe.com)，然後從左側導覽列選擇&#x200B;**[!UICONTROL Workflows]**&#x200B;以存取&#x200B;**[!UICONTROL Workflows]**&#x200B;工作區。

從&#x200B;**[!UICONTROL Workflows]**&#x200B;螢幕中，選擇&#x200B;**[!UICONTROL Data ingestion]**&#x200B;部分下的&#x200B;**[!UICONTROL Map CSV to XDM schema]** ，然後選擇&#x200B;**[!UICONTROL Launch]**。

![](../images/tutorials/map-a-csv-file/workflows.png)

將顯示&#x200B;**[!UICONTROL Map CSV to XDM schema]**&#x200B;工作流，從&#x200B;**[!UICONTROL Destination]**&#x200B;步驟開始。 選擇要接收傳入資料的資料集。 您可以使用現有資料集或建立新資料集。

**使用現有資料集**

若要將CSV資料內嵌至現有資料集，請選取&#x200B;**[!UICONTROL Use existing dataset]**。 您可以使用搜尋函式或捲動面板中現有資料集的清單來擷取現有資料集。

![](../images/tutorials/map-a-csv-file/use-existing-dataset.png)

若要將CSV資料內嵌至新資料集，請選取&#x200B;**[!UICONTROL Create new dataset]**，然後在提供的欄位中輸入資料集的名稱和說明。 使用搜索函式或滾動提供的方案清單來選擇方案。 選擇&#x200B;**[!UICONTROL Next]**&#x200B;繼續。

![](../images/tutorials/map-a-csv-file/create-new-dataset.png)

## 新增資料

出現&#x200B;**[!UICONTROL Add data]**&#x200B;步驟。 將CSV檔案拖放至提供的空間，或選取&#x200B;**[!UICONTROL Choose files]**&#x200B;以手動輸入CSV檔案。

![](../images/tutorials/map-a-csv-file/add-data.png)

上傳檔案後，會出現&#x200B;**[!UICONTROL Sample data]**&#x200B;區段，顯示前10列資料。 確認資料已如預期上傳後，請選取&#x200B;**[!UICONTROL Next]**。

![](../images/tutorials/map-a-csv-file/sample-data.png)

## 將CSV欄位對應至XDM結構欄位

出現&#x200B;**[!UICONTROL Mapping]**&#x200B;步驟。 CSV檔案的列列列在&#x200B;**[!UICONTROL Source Field]**&#x200B;下，其對應的XDM模式欄位列在&#x200B;**[!UICONTROL Target Field]**&#x200B;下。

[!DNL Platform] 根據您選取的目標架構或資料集，自動為自動映射欄位提供智慧建議。您可以手動調整對應規則，以符合您的使用案例。

![](../images/tutorials/map-a-csv-file/mapping-with-suggestions.png)

要接受所有自動生成映射值，請選擇標有「[!UICONTROL Accept all target fields]」的複選框。

![](../images/tutorials/map-a-csv-file/filled-mapping-with-suggestions.png)

有時，源架構有多個建議可用。 發生此情況時，對應卡會顯示最顯著的建議，後面接著藍色圓圈，其中包含可用的其他建議數目。 選取燈泡圖示將會顯示其他建議的清單。 您可以選擇其中一個替代建議，方法是選取您要對應至之建議旁的核取方塊。

![](../images/tutorials/map-a-csv-file/multiple-recommendations.png)

或者，您可以選擇手動將源方案映射到目標方案。 將滑鼠指標暫留在您要映射的來源架構上，然後選取加號圖示。

![](../images/tutorials/map-a-csv-file/mapping-with-suggestions-and-buttons.png)

出現&#x200B;**[!UICONTROL Map source to target field]**&#x200B;快顯視窗。 在此處，您可以選擇要映射的欄位，然後選擇&#x200B;**[!UICONTROL Save]**&#x200B;以添加新映射。

![](../images/tutorials/map-a-csv-file/manual-mapping.png)

如果要移除其中一個映射，請將滑鼠指標暫留在該映射上，然後選取減號圖示。

### 新增計算欄位{#add-calculated-field}

計算欄位允許根據輸入方案中的屬性建立值。 然後，這些值可以分配給目標方案中的屬性，並提供名稱和說明，以便更方便地引用。

選擇&#x200B;**[!UICONTROL Add calculated field]**&#x200B;按鈕繼續。

![](../images/tutorials/map-a-csv-file/add-calculated-field.png)

出現&#x200B;**[!UICONTROL Create calculated field]**&#x200B;面板。 左側對話方塊包含計算欄位中支援的欄位、函式和運算子。 選擇一個頁籤，開始向表達式編輯器添加函式、欄位或運算子。

![](../images/tutorials/map-a-csv-file/create-calculated-fields.png)

| 標籤 | 說明 |
| --------- | ----------- |
| 欄位 | 「欄位」頁籤列出了源方案中可用的欄位和屬性。 |
| 函數 | 函式頁籤列出了可用於轉換資料的函式。 要瞭解有關在計算欄位中可以使用的函式的更多資訊，請閱讀有關[使用資料準備（映射器）函式](../../data-prep/functions.md)的指南。 |
| 運算子 | 運算子標籤會列出可用來轉換資料的運算子。 |

您可以使用中心的運算式編輯器手動新增欄位、函式和運算子。 選擇編輯器以開始建立表達式。

![](../images/tutorials/map-a-csv-file/create-calculated-field.png)

選擇&#x200B;**[!UICONTROL Save]**&#x200B;繼續。

映射螢幕將重新顯示，並顯示新建立的源欄位。 應用相應的目標欄位並選擇&#x200B;**[!UICONTROL Finish]**&#x200B;以完成映射。

![](../images/tutorials/map-a-csv-file/new-calculated-field.png)

## 監控資料擷取

一旦映射並建立CSV檔案後，您就可以監控透過它擷取的資料。 有關監視資料攝取的詳細資訊，請參閱[監視資料攝取](../../ingestion/quality/monitor-data-ingestion.md)的教程。

## 後續步驟

在本教程中，您已成功將平面CSV檔案映射至XDM架構，並將其內嵌至[!DNL Platform]。 現在，下游[!DNL Platform]服務（例如[!DNL Real-time Customer Profile]）可使用此資料。 如需詳細資訊，請參閱[[!DNL Real-time Customer Profile]](../../profile/home.md)的概述。
