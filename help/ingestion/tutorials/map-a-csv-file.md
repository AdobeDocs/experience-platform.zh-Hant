---
keywords: Experience Platform;home;popular topics;map csv;map csv file;map csv file to xdm;map csv to xdm;ui guide;
solution: Experience Platform
title: 將CSV檔案對應至XDM架構
topic: tutorial
type: Tutorial
description: 本教學課程涵蓋如何使用Adobe Experience Platform使用者介面，將CSV檔案對應至XDM架構。
translation-type: tm+mt
source-git-commit: d69d0dd8c5a3d3a5e92cc88e390c079ed46aba32
workflow-type: tm+mt
source-wordcount: '860'
ht-degree: 1%

---


# 將CSV檔案對應至XDM架構

為了將CSV資料內嵌 [!DNL Adobe Experience Platform]至中，資料必須對應至 [!DNL Experience Data Model] (XDM)架構。 本教學課程介紹如何使用使用者介面將CSV檔案對應至XDM [!DNL Platform] 架構。

此外，本教學課程的附錄還提供有關使用映射功能的 [詳細資訊](#mapping-functions)。

## 快速入門

本教學課程需要有效瞭解下列元件 [!DNL Platform]:

- [[!DNL Experience Data Model (XDM System)]](../../xdm/home.md):組織客戶體驗資料 [!DNL Platform] 的標準化架構。
- [[!DNL Batch ingestion]](../batch-ingestion/overview.md):從用戶提供的數 [!DNL Platform] 據檔案中提取資料的方法。

本教學課程也要求您已建立資料集，以將CSV資料收錄至。 如需在UI中建立資料集的步驟，請參閱資料 [收錄教學課程](./ingest-batch-data.md)。

## 選擇目標

登入，然 [[!DNL Adobe Experience Platform]](https://platform.adobe.com) 後從左側導 **[!UICONTROL 覽列選取「工作流程]** 」以存取「工作 **[!UICONTROL 流程]** 」工作區。

在「工 **[!UICONTROL 作流程]** 」螢幕中，選擇 **[!UICONTROL 「]** Data ingestion **[!UICONTROL 」部分下的「將CSV映射到XDM模式」，然後選]******&#x200B;擇LaunchChec。

![](../images/tutorials/map-a-csv-file/workflows.png)

將 **[!UICONTROL CSV對應至XDM架構]** ，從「目標」步驟 **[!UICONTROL 開始]** 。 選擇要接收傳入資料的資料集。 您可以使用現有資料集或建立新資料集。

**使用現有資料集**

若要將CSV資料內嵌至現有資料集，請選取「使 **[!UICONTROL 用現有資料集」]**。 您可以使用搜尋函式或捲動面板中現有資料集的清單來擷取現有資料集。

![](../images/tutorials/map-a-csv-file/use-existing-dataset.png)

若要將CSV資料內嵌至新資料集，請選取「 **[!UICONTROL Create new dataset]** 」（建立新資料集），並在提供的欄位中輸入資料集的名稱和說明。 使用搜索函式或滾動提供的方案清單來選擇方案。 選擇 **[!UICONTROL 下一步]** ，繼續。

![](../images/tutorials/map-a-csv-file/create-new-dataset.png)

## 新增資料

此時將 **[!UICONTROL 顯示「添加資料]** 」步驟。 將CSV檔案拖放至提供的空間，或選取「選 **[!UICONTROL 擇檔案]** 」以手動輸入CSV檔案。

![](../images/tutorials/map-a-csv-file/add-data.png)

上 **[!UICONTROL 傳檔案後]** ,「範例資料」區段就會出現，顯示前10列資料。 確認資料已如預期上傳後，請選取「下一 **[!UICONTROL 步」]**。

![](../images/tutorials/map-a-csv-file/sample-data.png)

## 將CSV欄位對應至XDM結構欄位

此時將 **[!UICONTROL 顯示]** 「映射」步驟。 CSV檔案的欄位列在「來源欄位」 **[!UICONTROL 下]**，其對應的XDM架構欄位列在「目標欄位」 **[!UICONTROL 下]**。

[!DNL Platform] 根據您選取的目標架構或資料集，自動為自動映射欄位提供智慧建議。 您可以手動調整對應規則，以符合您的使用案例。

![](../images/tutorials/map-a-csv-file/mapping-with-suggestions.png)

要接受所有自動生成映射值，請選中標有「接受所有目[!UICONTROL 標欄位]」的複選框。

![](../images/tutorials/map-a-csv-file/filled-mapping-with-suggestions.png)

有時，源架構有多個建議可用。 發生此情況時，對應卡會顯示最顯著的建議，後面接著藍色圓圈，其中包含可用的其他建議數目。 選取燈泡圖示將會顯示其他建議的清單。 您可以選擇其中一個替代建議，方法是選取您要對應至之建議旁的核取方塊。

![](../images/tutorials/map-a-csv-file/multiple-recommendations.png)

或者，您可以選擇手動將源方案映射到目標方案。 將滑鼠指標暫留在您要映射的來源架構上，然後選取加號圖示。

![](../images/tutorials/map-a-csv-file/mapping-with-suggestions-and-buttons.png)

此時 **[!UICONTROL 會顯示「將來源對應至目標」欄]** 位快顯視窗。 在此處，您可以選擇要映射的欄位，然後選擇「保 **[!UICONTROL 存]** 」以添加新映射。

![](../images/tutorials/map-a-csv-file/manual-mapping.png)

如果要移除其中一個映射，請將滑鼠指標暫留在該映射上，然後選取減號圖示。

### 新增計算欄位

計算欄位允許根據輸入方案中的屬性建立值。 然後，這些值可以分配給目標方案中的屬性，並提供名稱和說明，以便更方便地引用。

選擇「添 **[!UICONTROL 加計算欄位]** 」按鈕以繼續。

![](../images/tutorials/map-a-csv-file/add-calculated-field.png)

此時將 **[!UICONTROL 出現「建立計算欄位]** 」面板。 左側對話方塊包含計算欄位中支援的欄位、函式和運算子。 選擇一個頁籤，開始向表達式編輯器添加函式、欄位或運算子。

![](../images/tutorials/map-a-csv-file/create-calculated-fields.png)

| 標籤 | 說明 |
| --------- | ----------- |
| 欄位 | 「欄位」頁籤列出了源方案中可用的欄位和屬性。 |
| 函數 | 函式頁籤列出了可用於轉換資料的函式。 要瞭解有關在計算欄位中可以使用的函式的更多資訊，請閱讀有關使用資料準 [備（映射器）函式的指南](../../data-prep/functions.md)。 |
| 運算子 | 運算子標籤會列出可用來轉換資料的運算子。 |

您可以使用中心的運算式編輯器手動新增欄位、函式和運算子。 選擇編輯器以開始建立表達式。

![](../images/tutorials/map-a-csv-file/create-calculated-field.png)

選擇「 **[!UICONTROL 保存]** 」繼續。

映射螢幕將重新顯示，並顯示新建立的源欄位。 應用相應的目標欄位並選擇 **[!UICONTROL 完成]** ，以完成映射。

![](../images/tutorials/map-a-csv-file/new-calculated-field.png)

## 監控資料流

一旦映射並建立CSV檔案後，您就可以監控透過它擷取的資料。 有關監視資料流的詳細資訊，請參見有關監視流資料流 [的教程](../../ingestion/quality/monitor-data-flows.md)。

## 後續步驟

在本教學課程中，您已成功將平面CSV檔案對應至XDM架構，並將它加入其中 [!DNL Platform]。 此資料現在可供下游服務 [!DNL Platform] 使用，例如 [!DNL Real-time Customer Profile]。 See the overview for [[!DNL Real-time Customer Profile]](../../profile/home.md) for more information.
