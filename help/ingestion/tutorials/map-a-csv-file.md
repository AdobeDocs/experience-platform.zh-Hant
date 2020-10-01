---
keywords: Experience Platform;home;popular topics;map csv;map csv file;map csv file to xdm;map csv to xdm;ui guide;
solution: Experience Platform
title: 將CSV檔案對應至XDM架構
topic: tutorial
type: Tutorial
description: 本教學課程涵蓋如何使用Adobe Experience Platform使用者介面，將CSV檔案對應至XDM架構。
translation-type: tm+mt
source-git-commit: 7adf18e4251f377fee586c8a0f23b89acd75afca
workflow-type: tm+mt
source-wordcount: '886'
ht-degree: 1%

---


# 將CSV檔案對應至XDM架構

為了將CSV資料內嵌 [!DNL Adobe Experience Platform]至中，資料必須對應至 [!DNL Experience Data Model] (XDM)架構。 本教學課程介紹如何使用使用者介面將CSV檔案對應至XDM [!DNL Platform] 架構。

此外，本教學課程的附錄還提供有關使用映射功能的 [詳細資訊](#mapping-functions)。

## 快速入門

本教學課程需要有效瞭解下列元件 [!DNL Platform]:

- [[!DNL體驗資料模型（XDM系統）]](../../xdm/home.md):組織客戶體驗資料 [!DNL Platform] 的標準化架構。
- [[!DNL批處理提取]](../batch-ingestion/overview.md):從用戶提供的數 [!DNL Platform] 據檔案中提取資料的方法。

本教學課程也要求您已建立資料集，以將CSV資料收錄至。 如需在UI中建立資料集的步驟，請參閱資料 [收錄教學課程](./ingest-batch-data.md)。

## 選擇目標

登入 [[!DNL Adobe Experience Platform]](https://platform.adobe.com) ，然後從左側導覽列選取「工作流程 **[!UICONTROL 」以存取「工]** 作流程 **** 」工作區。

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

此時將 **[!UICONTROL 顯示]** 「映射」步驟。 CSV檔案的欄位列在「來源欄位」 **[!UICONTROL 下]**，其對應的XDM架構欄位列在「目標欄位」 **[!UICONTROL 下]**。 未選取的目標欄位以紅色勾勒。 您可以使用篩選欄位選項來縮小可用來源欄位的清單。

>[!TIP]
>
>[!DNL Platform] 根據您選取的目標架構或資料集，為自動映射欄位提供智慧建議。 您可以手動調整對應規則，以符合您的使用案例。

要將CSV列映射到XDM欄位，請選擇該列相應目標欄位旁的架構表徵圖。

![](../images/tutorials/map-a-csv-file/mapping.png)

將出 **[!UICONTROL 現「選擇方案]** 」欄位窗口。 您可以在這裡導覽XDM架構的結構，並找出您要將CSV欄對應至的欄位。 按一下XDM欄位以選取它，然後按一下「選 **[!UICONTROL 取]**」。

![](../images/tutorials/map-a-csv-file/select-schema-field.png)

完成其餘未映射源欄位的步驟後，「 **[!UICONTROL Mapping]** 」螢幕將重新顯示，「Target」（目標）欄位下現在將顯示選定的XDM **[!UICONTROL 欄位]**。

![](../images/tutorials/map-a-csv-file/field-mapped.png)

在映射欄位時，您還可以包括函式，以便根據輸入源欄位計算值。 如需詳 [細資訊](#mapping-functions) ，請參閱附錄中的對應函式一節。

### 新增計算欄位

計算欄位允許根據輸入方案中的屬性建立值。 然後，這些值可以分配給目標方案中的屬性，並提供名稱和說明，以便更方便地引用。

選擇「添 **[!UICONTROL 加計算欄位]** 」按鈕以繼續。

![](../images/tutorials/map-a-csv-file/add-calculate-field.png)

此時將 **[!UICONTROL 出現「建立計算欄位]** 」面板。 左側對話方塊包含計算欄位中支援的欄位、函式和運算子。 選擇一個頁籤，開始向表達式編輯器添加函式、欄位或運算子。

![](../images/tutorials/map-a-csv-file/create-calculated-fields.png)

| 標籤 | 說明 |
| --------- | ----------- |
| 欄位 | 「欄位」頁籤列出了源方案中可用的欄位和屬性。 |
| 函數 | 函式頁籤列出了可用於轉換資料的函式。 |
| 運算子 | 運算子標籤會列出可用來轉換資料的運算子。 |

您可以使用中心的運算式編輯器手動新增欄位、函式和運算子。 選擇編輯器以開始建立表達式。

![](../images/tutorials/map-a-csv-file/expression-editor.png)

選擇「 **[!UICONTROL 保存]** 」繼續。

映射螢幕將重新顯示，並顯示新建立的源欄位。 應用相應的目標欄位並選擇 **[!UICONTROL 完成]** ，以完成映射。

![](../images/tutorials/map-a-csv-file/new-field.png)

## 監控資料流

一旦映射並建立CSV檔案後，您就可以監控透過它擷取的資料。 有關監視資料流的詳細資訊，請參見有關監視流資料流 [的教程](../../ingestion/quality/monitor-data-flows.md)。

## 使用映射函式

若要使用函式，請在「來源欄位」下方輸入 **[!UICONTROL 函式]** ，並輸入適當的語法和輸入。

例如，若要串連 **城市****CSV和國家／地區** CSV欄位，並將它們指派至 **城市** XDM欄位，請將來源欄位設為 `concat(city, ", ", county)`。

![](../images/tutorials/map-a-csv-file/mapping-function.png)

要瞭解有關將列映射到XDM欄位的詳細資訊，請閱讀有關使 [用資料準備（映射器）函式的指南](../../data-prep/functions.md)。

## 後續步驟

在本教學課程中，您已成功將平面CSV檔案對應至XDM架構，並將它加入其中 [!DNL Platform]。 此資料現在可供下游服務 [!DNL Platform] 使用，例如 [!DNL Real-time Customer Profile]。 如需詳細資 [訊，請參閱[!DNL即時客戶個人檔案]](../../profile/home.md) 的概觀。
