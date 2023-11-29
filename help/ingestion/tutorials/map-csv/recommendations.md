---
title: 使用AI產生的Recommendations將CSV檔案對應到XDM結構描述
description: 本教學課程涵蓋如何使用AI產生的建議將CSV檔案對應到XDM結構描述。
exl-id: 1daedf0b-5a25-4ca5-ae5d-e9ee1eae9e4d
source-git-commit: 6632086641004c2b788a28cbc47ac6d8bd4eace3
workflow-type: tm+mt
source-wordcount: '1102'
ht-degree: 2%

---

# 使用AI產生的建議將CSV檔案對應到XDM結構描述

>[!NOTE]
>
>如需Platform中一般可用CSV對應功能的相關資訊，請參閱以下檔案： [將CSV檔案對應到現有結構描述](./existing-schema.md).

為了將CSV資料擷取至 [!DNL Adobe Experience Platform]，資料必須對應至 [!DNL Experience Data Model] (XDM)結構描述。 您可以選擇對應至 [現有結構描述](./existing-schema.md)，但如果您不確定要使用哪個結構描述或應如何建構，可以在Platform UI中使用根據機器學習(ML)模型的動態建議。

## 快速入門

本教學課程需要您實際瞭解下列元件 [!DNL Platform]：

* [[!DNL Experience Data Model (XDM System)]](../../../xdm/home.md)：[!DNL Platform] 據以組織客戶體驗資料的標準化框架。
   * 您至少必須瞭解 [XDM中的行為](../../../xdm/home.md#data-behaviors)，以便您可以決定是否將資料對應至 [!UICONTROL 個人資料] 類別（記錄行為）或 [!UICONTROL 體驗事件] 類別（時間序列行為）。
* [批次擷取](../../batch-ingestion/overview.md)：使用的方法 [!DNL Platform] 從使用者提供的資料檔擷取資料。
* [Adobe Experience Platform資料準備](../../batch-ingestion/overview.md)：可讓您對應及轉換已擷取資料以符合XDM結構描述的一套功能。 有關的檔案 [資料準備函式](../../../data-prep/functions.md) 與結構描述對應特別相關。

## 提供資料流詳細資料

在Experience Platform UI中，選取 **[!UICONTROL 來源]** ，位於左側導覽器中。 在 **[!UICONTROL 目錄]** 檢視，導覽至 **[!UICONTROL 本機系統]** 類別。 在 **[!UICONTROL 本機檔案上傳]**，選取 **[!UICONTROL 新增資料]**.

![此 [!UICONTROL 來源] Platform UI中的目錄，使用 [!UICONTROL 新增資料] 在 [!UICONTROL 本機檔案上傳] 已選取。](../../images/tutorials/map-csv-recommendations/local-file-upload.png)

此 **[!UICONTROL 對應CSV XDM結構描述]** 工作流程隨即出現，從 **[!UICONTROL 資料流詳細資料]** 步驟。

選取 **[!UICONTROL 使用ML建議建立新的結構描述]**，造成新控制項出現。 為您要對應的CSV資料選擇適當的類別([!UICONTROL 個人資料] 或 [!UICONTROL 體驗事件])。 您可以選擇使用下拉式選單來選取您企業的相關產業，或者如果提供的類別不適用於您，則將其留空。 如果您的組織在 [企業對企業(B2B)](../../../xdm/tutorials/relationship-b2b.md) 模型，選取 **[!UICONTROL B2B資料]** 核取方塊。

![此 [!UICONTROL 資料流詳細資料] 選取ML建議選項的步驟。 [!UICONTROL 個人資料] 已為類別選取，並且 [!UICONTROL 電信] 為業界選取](../../images/tutorials/map-csv-recommendations/select-class-and-industry.png)

從這裡，提供將從CSV資料建立的結構描述名稱，以及包含在該結構描述下擷取之資料的輸出資料集名稱。

您可以選擇在繼續之前為資料流設定以下附加功能：

| 輸入名稱 | 說明 |
| --- | --- |
| [!UICONTROL 說明] | 資料流的說明。 |
| [!UICONTROL 錯誤診斷] | 啟用後，系統會為新擷取的批次產生錯誤訊息，您可在擷取中對應批次時檢視這些錯誤訊息 [API](../../batch-ingestion/api-overview.md). |
| [!UICONTROL 部分擷取] | 啟用時，會在指定的錯誤臨界值內擷取新批次資料的有效記錄。 此臨界值可讓您設定整個批次失敗之前可接受的錯誤百分比。 |
| [!UICONTROL 資料流詳細資訊] | 為會將CSV資料帶入Platform的資料流提供名稱和可選說明。 啟動此工作流程時，資料流會自動被指派預設名稱。 變更名稱為選用。 |
| [!UICONTROL 警示] | 從清單中選取 [產品內警示](../../../observability/alerts/overview.md) 啟動資料流後，您想要收到的資料流狀態。 |

{style="table-layout:auto"}

完成資料流設定後，選取「 」 **[!UICONTROL 下一個]**.

![此 [!UICONTROL 資料流詳細資料] 區段已完成。](../../images/tutorials/map-csv-recommendations/dataflow-detail-complete.png)

## 選擇資料

在 **[!UICONTROL 選取資料]** 步驟，使用左欄上傳您的CSV檔案。 您可以選取 **[!UICONTROL 選擇檔案]** 開啟檔案總管對話方塊以從中選取檔案，或者您可以直接將檔案拖放到欄中。

![此 [!UICONTROL 選擇檔案] 內反白顯示的按鈕和拖放區域 [!UICONTROL 選取資料] 步驟。](../../images/tutorials/map-csv-recommendations/upload-files.png)

上傳檔案後，範例資料區段隨即顯示，顯示前10列收到的資料，以便您驗證其是否已正確上傳。 選取&#x200B;**[!UICONTROL 「下一步」]**&#x200B;以繼續。

![範例資料列會在工作區中填入](../../images/tutorials/map-csv-recommendations/data-uploaded.png)

## 設定結構描述對應

ML模型會根據您的資料流設定和您上傳的CSV檔案來執行，以產生新的結構描述。 當程式完成時， [!UICONTROL 對應] 步驟會填入，以顯示每個個別欄位的對應，以及產生之結構描述結構的完整可導覽檢視。

![此 [!UICONTROL 對應] 在UI中執行步驟，顯示已對應的所有CSV欄位以及產生的結構描述結構。](../../images/tutorials/map-csv-recommendations/schema-generated.png)

>[!NOTE]
>
>在來源與目標欄位對應工作流程期間，您可以根據各種條件篩選結構描述中的所有欄位。 預設行為是顯示所有對應的欄位。 若要變更顯示的欄位，請選取搜尋輸入欄位旁的篩選圖示，然後從下拉式清單選項中選擇。<br> ![CSV至XDM結構描述建立工作流程的對應階段，其中篩選圖示和下拉式功能表會強調顯示。](../../images/tutorials/map-csv-recommendations/source-field-to-target-mapping-filter.png "CSV至XDM結構描述建立工作流程的對應階段，其中篩選圖示和下拉式功能表會強調顯示。"){width="100" zoomable="yes"}

從這裡，您可以選擇使用 [編輯欄位對應](#edit-mappings) 或 [變更與其關聯的欄位群組](#edit-schema) 根據您的需求。 滿意後，選取 **[!UICONTROL 完成]** 完成對應並起始您先前設定的資料流。 CSV資料會內嵌至系統中，並根據產生的結構描述結構填入資料集，以備下游平台服務使用。

![此 [!UICONTROL 完成] 按鈕進行選取，完成CSV對應程式。](../../images/tutorials/map-csv-recommendations/finish-mapping.png)

### 編輯欄位對應 {#edit-mappings}

使用欄位對應預覽來編輯現有對應或將其完全移除。 如需有關如何管理UI中對應集的詳細資訊，請參閱 [資料準備對應的UI指南](../../../data-prep/ui/mapping.md#mapping-interface).

### 編輯欄位群組 {#edit-field-groups}

CSV欄位會使用ML模型自動對應到現有XDM欄位群組。 如果您想要變更任何特定CSV欄位的欄位群組，請選取 **[!UICONTROL 編輯]** 架構樹狀結構旁邊。

![此 [!UICONTROL 編輯] 在結構描述樹旁邊選取的按鈕。](../../images/tutorials/map-csv-recommendations/edit-schema-structure.png)

會出現一個對話方塊，讓您編輯對應中任何欄位的顯示名稱、資料型別和欄位群組。 選取編輯圖示(![編輯圖示](../../images/tutorials/map-csv-recommendations/edit-icon.png))來編輯其右側欄中的詳細資訊，然後再選取 **[!UICONTROL 套用]**.

![要變更之來源欄位的建議欄位群組。](../../images/tutorials/map-csv-recommendations/select-schema-field.png)

當您完成調整來源欄位的結構描述建議時，請選取 **[!UICONTROL 儲存]** 以套用變更。

## 後續步驟

本指南說明如何使用AI產生的建議將CSV檔案對應到XDM結構描述，讓您透過批次擷取將該資料匯入Platform。

有關將CSV檔案對應到現有結構的步驟，請參閱 [現有結構描述對應工作流程](./existing-schema.md). 如需有關透過預先建立的來源連線將資料即時串流到Platform的資訊，請參閱 [來源概觀](../../../sources/home.md).
