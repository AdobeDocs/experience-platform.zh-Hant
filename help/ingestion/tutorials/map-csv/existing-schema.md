---
keywords: Experience Platform；首頁；熱門主題；對應csv；對應csv檔案；將csv檔案對應至xdm；將csv對應至xdm;ui指南；
solution: Experience Platform
title: 將CSV檔案對應至現有的XDM結構
type: Tutorial
description: 本教學課程說明如何使用Adobe Experience Platform使用者介面，將CSV檔案對應至現有的XDM架構。
exl-id: 15f55562-269d-421d-ad3a-5c10fb8f109c
source-git-commit: e802932dea38ebbca8de012a4d285eab691231be
workflow-type: tm+mt
source-wordcount: '945'
ht-degree: 1%

---

# 將CSV檔案對應至現有的XDM結構

>[!NOTE]
>
>本檔案說明如何將CSV檔案對應至現有的XDM結構。 如需如何使用AI產生的架構建議工具（目前為測試版）的資訊，請參閱 [使用機器學習建議對應CSV檔案](./recommendations.md).

若要將CSV資料內嵌至 [!DNL Adobe Experience Platform]，資料必須對應至 [!DNL Experience Data Model] (XDM)結構。 本教學課程說明如何使用將CSV檔案對應至XDM架構 [!DNL Platform] 使用者介面。

## 快速入門

本教學課程需要妥善了解以下元件： [!DNL Platform]:

- [[!DNL Experience Data Model (XDM System)]](../../../xdm/home.md):標準化框架 [!DNL Platform] 組織客戶體驗資料。
- [批次內嵌](../../batch-ingestion/overview.md):透過 [!DNL Platform] 從用戶提供的資料檔案中獲取資料。
- [Adobe Experience Platform資料準備](../../batch-ingestion/overview.md):這套功能可讓您對應並轉換擷取的資料，以符合XDM結構。 上的檔案 [資料準備函式](../../../data-prep/functions.md) 與架構對應特別相關。

本教學課程也要求您已建立資料集，將CSV資料內嵌至。 如需在UI中建立資料集的步驟，請參閱 [資料內嵌教學課程](../ingest-batch-data.md).

## 選擇目的地

登入 [[!DNL Adobe Experience Platform]](https://platform.adobe.com) 然後選取 **[!UICONTROL 工作流程]** 從左側導覽列存取 **[!UICONTROL 工作流程]** 工作區。

從 **[!UICONTROL 工作流程]** 螢幕，選擇 **[!UICONTROL 將CSV對應至XDM結構]** 在 **[!UICONTROL 資料擷取]** 區段，然後選取 **[!UICONTROL Launch]**.

![](../../images/tutorials/map-a-csv-file/workflows.png)

此 **[!UICONTROL 將CSV對應至XDM結構]** 工作流程隨即顯示，從 **[!UICONTROL 目的地]** 步驟。 選擇要內嵌入的傳入資料的資料集。 您可以使用現有資料集或建立新資料集。

**使用現有資料集**

若要將CSV資料內嵌至現有資料集，請選取 **[!UICONTROL 使用現有資料集]**. 您可以使用搜尋函式或捲動面板中現有資料集的清單，以擷取現有資料集。

![](../../images/tutorials/map-a-csv-file/use-existing-dataset.png)

若要將CSV資料內嵌至新資料集，請選取 **[!UICONTROL 建立新資料集]** 並在提供的欄位中輸入資料集的名稱和說明。 使用搜索函式或滾動查看提供的架構清單來選擇架構。 選擇 **[!UICONTROL 下一個]** 繼續。

![](../../images/tutorials/map-a-csv-file/create-new-dataset.png)

## 新增資料

此 **[!UICONTROL 新增資料]** 步驟。 將CSV檔案拖放至提供的空間，或選取 **[!UICONTROL 選擇檔案]** 來手動輸入CSV檔案。

![](../../images/tutorials/map-a-csv-file/add-data.png)

此 **[!UICONTROL 範例資料]** 區段會在檔案上傳後顯示，並顯示前10列資料。 確認資料已如預期上傳後，請選取 **[!UICONTROL 下一個]**.

![](../../images/tutorials/map-a-csv-file/sample-data.png)

## 將CSV欄位對應至XDM結構欄位

此 **[!UICONTROL 對應]** 步驟。 CSV檔案的欄會列在 **[!UICONTROL 源欄位]**，其對應的XDM架構欄位列於 **[!UICONTROL 目標欄位]**.

[!DNL Platform] 根據您選取的目標結構或資料集，自動為自動對應欄位提供智慧型建議。 您可以手動調整對應規則以符合您的使用案例。

![](../../images/tutorials/map-a-csv-file/mapping-with-suggestions.png)

要接受所有自動生成映射值，請選中標籤為「」的複選框[!UICONTROL 接受所有目標欄位]」。

![](../../images/tutorials/map-a-csv-file/filled-mapping-with-suggestions.png)

有時，來源結構有多個建議可供使用。 發生此情況時，對應卡片會顯示最顯著的建議，後面接著一個藍色圓圈，裡面包含可用的其他建議數量。 選取燈泡圖示會顯示其他建議的清單。 您可以選取您要對應至之建議旁的核取方塊，以選擇其中一個替代建議。

![](../../images/tutorials/map-a-csv-file/multiple-recommendations.png)

或者，您可以選擇手動將源架構映射到目標架構。 暫留在您要對應的來源架構上，然後選取加號圖示。

![](../../images/tutorials/map-a-csv-file/mapping-with-suggestions-and-buttons.png)

此 **[!UICONTROL 將源映射到目標欄位]** 彈出視窗隨即出現。 您可以在此選取要對應的欄位，後面接著 **[!UICONTROL 儲存]** 來新增新對應。

![](../../images/tutorials/map-a-csv-file/manual-mapping.png)

如果要移除其中一個對應，請將滑鼠指標暫留在該對應上，然後選取減號圖示。

### 新增計算欄位 {#add-calculated-field}

計算欄位允許根據輸入架構中的屬性建立值。 然後，可將這些值指派給目標架構中的屬性，並提供名稱和說明，以便更輕鬆參考。

選取 **[!UICONTROL 新增計算欄位]** 按鈕繼續。

![](../../images/tutorials/map-a-csv-file/add-calculated-field.png)

此 **[!UICONTROL 建立計算欄位]** 框。 左側對話方塊包含計算欄位中支援的欄位、函式和運算子。 選取其中一個索引標籤，以開始將函式、欄位或運算子新增至運算式編輯器。

![](../../images/tutorials/map-a-csv-file/create-calculated-fields.png)

| 標記 | 說明 |
| --------- | ----------- |
| 欄位 | 「欄位」頁簽列出源架構中可用的欄位和屬性。 |
| 函式 | 函式索引標籤列出可用於轉換資料的函式。 若要進一步了解可在計算欄位中使用的函式，請參閱 [使用資料準備（映射器）函式](../../../data-prep/functions.md). |
| 操作者 | 運算子索引標籤會列出可用於轉換資料的運算子。 |

您可以使用中心的運算式編輯器手動新增欄位、函式和運算子。 選取要開始建立運算式的編輯器。

![](../../images/tutorials/map-a-csv-file/create-calculated-field.png)

選擇 **[!UICONTROL 儲存]** 繼續。

映射螢幕將隨新建立的源欄位重新顯示。 應用相應的目標欄位並選擇 **[!UICONTROL 完成]** 填寫對應。

![](../../images/tutorials/map-a-csv-file/new-calculated-field.png)

## 監視資料內嵌

CSV檔案一旦對應並建立後，您就可以監控透過它擷取的資料。 如需監控資料擷取的詳細資訊，請參閱 [監控資料擷取](../../../ingestion/quality/monitor-data-ingestion.md).

## 後續步驟

依照本教學課程，您已成功將一般CSV檔案對應至XDM結構，並將其擷取至 [!DNL Platform]. 此資料現在可供下游使用 [!DNL Platform] 服務，例如 [!DNL Real-Time Customer Profile]. 請參閱以下概觀： [[!DNL Real-Time Customer Profile]](../../../profile/home.md) 以取得更多資訊。
