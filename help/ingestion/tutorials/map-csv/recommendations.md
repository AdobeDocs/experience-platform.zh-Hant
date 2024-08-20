---
title: 使用AI產生的Recommendations將CSV檔案對應到XDM結構描述
description: 本教學課程涵蓋如何使用AI產生的建議將CSV檔案對應到XDM結構描述。
exl-id: 1daedf0b-5a25-4ca5-ae5d-e9ee1eae9e4d
source-git-commit: cbebee894d68f60f82e1154f41dcecc76c706a3b
workflow-type: tm+mt
source-wordcount: '1172'
ht-degree: 1%

---

# 使用AI產生的建議將CSV檔案對應到XDM結構描述

>[!NOTE]
>
>如需有關Platform中一般可用的CSV對應功能的資訊，請參閱[將CSV檔案對應到現有結構描述](./existing-schema.md)上的檔案。

為了將CSV資料擷取到[!DNL Adobe Experience Platform]，資料必須對應到[!DNL Experience Data Model] (XDM)結構描述。 您可以選擇對應到[現有的結構描述](./existing-schema.md)，但如果您不清楚要使用哪個結構描述或是應如何建構，可以改為在Platform UI中使用以機器學習(ML)模型為基礎的動態建議。

## 快速入門

此教學課程需要您實際瞭解[!DNL Platform]的下列元件：

* [[!DNL Experience Data Model (XDM System)]](../../../xdm/home.md)： [!DNL Platform]用來組織客戶體驗資料的標準化架構。
   * 您至少必須瞭解XDM](../../../xdm/home.md#data-behaviors)中[行為的概念，才能決定要將資料對應至[!UICONTROL 設定檔]類別（記錄行為）或[!UICONTROL ExperienceEvent]類別（時間序列行為）。
* [批次擷取](../../batch-ingestion/overview.md)： [!DNL Platform]從使用者提供的資料檔擷取資料的方法。
* [Adobe Experience Platform資料準備](../../batch-ingestion/overview.md)：功能套件，可讓您對應及轉換擷取的資料，以符合XDM結構描述。 有關[資料準備函式](../../../data-prep/functions.md)的檔案與結構描述對應特別相關。

## 提供資料流詳細資料

在Experience PlatformUI中，選取左側導覽中的&#x200B;**[!UICONTROL 來源]**。 在&#x200B;**[!UICONTROL 目錄]**&#x200B;檢視中，瀏覽至&#x200B;**[!UICONTROL 本機系統]**&#x200B;類別。 在&#x200B;**[!UICONTROL 本機檔案上傳]**&#x200B;下，選取&#x200B;**[!UICONTROL 新增資料]**。

![平台UI中的[!UICONTROL 來源]目錄，已選取[!UICONTROL 本機檔案上傳]下的[!UICONTROL 新增資料]。](../../images/tutorials/map-csv-recommendations/local-file-upload.png)

**[!UICONTROL 對應CSV XDM結構描述]**&#x200B;工作流程隨即出現，從&#x200B;**[!UICONTROL 資料流詳細資料]**&#x200B;步驟開始。

選取&#x200B;**[!UICONTROL 使用ML Recommendations建立新結構描述]**，以顯示新的控制項。 為您要對應的CSV資料選擇適當的類別（[!UICONTROL 設定檔]或[!UICONTROL ExperienceEvent]）。 您可以選擇使用下拉式選單來選取您企業的相關產業，或者如果提供的類別不適用於您，則將其留空。 如果您的組織在[企業對企業(B2B)](../../../xdm/tutorials/relationship-b2b.md)模型下運作，請選取&#x200B;**[!UICONTROL B2B data]**&#x200B;核取方塊。

![已選取ML建議選項的[!UICONTROL 資料流詳細資料]步驟。 已為該類別選取[!UICONTROL 設定檔]，並為產業選取[!UICONTROL 電信]](../../images/tutorials/map-csv-recommendations/select-class-and-industry.png)

從這裡，提供將從CSV資料建立的結構描述名稱，以及包含在該結構描述下擷取之資料的輸出資料集名稱。

您可以選擇在繼續之前為資料流設定以下附加功能：

| 輸入名稱 | 說明 |
| --- | --- |
| [!UICONTROL 說明] | 資料流的說明。 |
| [!UICONTROL 錯誤診斷] | 啟用時，會為新擷取的批次產生錯誤訊息，以便在[API](../../batch-ingestion/api-overview.md)中擷取對應批次時檢視。 |
| [!UICONTROL 部分擷取] | 啟用時，會在指定的錯誤臨界值內擷取新批次資料的有效記錄。 此臨界值可讓您設定整個批次失敗之前可接受的錯誤百分比。 |
| [!UICONTROL 資料流詳細資料] | 為會將CSV資料帶入Platform的資料流提供名稱和可選說明。 啟動此工作流程時，資料流會自動被指派預設名稱。 變更名稱為選用。 |
| [!UICONTROL 警示] | 從[產品內警示](../../../observability/alerts/overview.md)的清單中選取您要在資料流啟動後接收的有關資料流狀態的警示。 |

{style="table-layout:auto"}

完成資料流設定後，選取&#x200B;**[!UICONTROL 下一步]**。

![ [!UICONTROL 資料流詳細資料]區段已完成。](../../images/tutorials/map-csv-recommendations/dataflow-detail-complete.png)

## 選取資料

在&#x200B;**[!UICONTROL 選取資料]**&#x200B;步驟中，使用左欄上傳您的CSV檔案。 您可以選取&#x200B;**[!UICONTROL 選擇檔案]**&#x200B;以開啟檔案總管對話方塊來選取檔案，或是直接將檔案拖放到資料行上。

![在[!UICONTROL 選取資料]步驟中反白顯示的[!UICONTROL 選擇檔案]按鈕和拖放區域。](../../images/tutorials/map-csv-recommendations/upload-files.png)

上傳檔案後，範例資料區段隨即顯示，顯示前10列收到的資料，以便您驗證其是否已正確上傳。 選取&#x200B;**[!UICONTROL 「下一步」]**&#x200B;以繼續。

![範例資料列已填入工作區](../../images/tutorials/map-csv-recommendations/data-uploaded.png)

## 設定結構描述對應

ML模型會根據您的資料流設定和您上傳的CSV檔案來執行，以產生新的結構描述。 當程式完成時，[!UICONTROL 對應]步驟會填入，以顯示每個個別欄位的對應，以及產生之結構描述結構的完全可導覽檢視。

![UI中的[!UICONTROL 對應]步驟，顯示所有對應的CSV欄位以及產生的結構描述結構。](../../images/tutorials/map-csv-recommendations/schema-generated.png)

>[!NOTE]
>
>在來源與目標欄位對應工作流程期間，您可以根據各種條件篩選結構描述中的所有欄位。 預設行為是顯示所有對應的欄位。 若要變更顯示的欄位，請選取搜尋輸入欄位旁的篩選圖示，然後從下拉式清單選項中選擇。<br> ![CSV至XDM結構描述建立工作流程的對映階段，篩選器圖示和下拉式功能表會醒目提示。](../../images/tutorials/map-csv-recommendations/source-field-to-target-mapping-filter.png "CSV至XDM結構描述建立工作流程的對映階段，其中篩選圖示和下拉式功能表已反白顯示。"){width="100" zoomable="yes"}

從這裡，您可以視需要[編輯欄位對應](#edit-mappings)或[變更它們關聯的欄位群組](#edit-schema)。 滿意後，選取&#x200B;**[!UICONTROL 完成]**&#x200B;以完成對應，並起始您先前設定的資料流。 CSV資料會內嵌至系統中，並根據產生的結構描述結構填入資料集，以備下游平台服務使用。

![正在選取[!UICONTROL 完成]按鈕，正在完成CSV對應程式。](../../images/tutorials/map-csv-recommendations/finish-mapping.png)

### 編輯欄位對應 {#edit-mappings}

使用欄位對應預覽來編輯現有對應或將其完全移除。 如需有關如何管理UI中對應集的詳細資訊，請參閱[資料準備對應](../../../data-prep/ui/mapping.md#mapping-interface)的UI指南。

### 編輯欄位群組 {#edit-field-groups}

CSV欄位會使用ML模型自動對應到現有XDM欄位群組。 如果您想要變更任何特定CSV欄位的欄位群組，請選取結構描述樹狀結構旁的&#x200B;**[!UICONTROL 編輯]**。

![正在選取結構描述樹狀結構旁的[!UICONTROL Edit]按鈕。](../../images/tutorials/map-csv-recommendations/edit-schema-structure.png)

會出現一個對話方塊，讓您編輯對應中任何欄位的顯示名稱、資料型別和欄位群組。 選取來源欄位旁的編輯圖示（![編輯圖示](/help/images/icons/edit.png)），在選取&#x200B;**[!UICONTROL 套用]**&#x200B;之前，編輯其右欄中的詳細資料。

![正在變更之來源欄位的建議欄位群組。](../../images/tutorials/map-csv-recommendations/select-schema-field.png)

當您完成調整來源欄位的結構描述建議時，請選取&#x200B;**[!UICONTROL 儲存]**&#x200B;以套用變更。

## 後續步驟

本指南說明如何使用AI產生的建議將CSV檔案對應到XDM結構描述，讓您透過批次擷取將該資料匯入Platform。

如需將CSV檔案對應到現有結構描述的步驟，請參閱[現有結構描述對應工作流程](./existing-schema.md)。 如需透過預先建立的來源連線將資料即時串流到Platform的資訊，請參閱[來源概觀](../../../sources/home.md)。

您也可以使用機器學習(ML)演演算法，從範例CSV資料&#x200B;**產生結構描述**。 此工作流程會根據CSV檔案的結構和內容自動建立新結構描述。 這個新建立的結構描述符合您資料的格式，可為您節省時間並提高定義大型複雜資料集的結構、欄位和資料型別時的準確性。 如需此工作流程的詳細資訊，請參閱[ML輔助結構描述建立指南](../../../xdm/ui/ml-assisted-schema-creation.md)。
