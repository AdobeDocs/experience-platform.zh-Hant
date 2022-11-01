---
title: 使用AI產生的Recommendations(Beta)將CSV檔案對應至XDM結構
description: 本教學課程說明如何使用AI產生的建議，將CSV檔案對應至XDM架構。
source-git-commit: a8a7523c5b7f696ecc0ae89cb4e0474b44a222e7
workflow-type: tm+mt
source-wordcount: '1021'
ht-degree: 0%

---

# 使用AI產生的建議（測試版）將CSV檔案對應至XDM結構

>[!IMPORTANT]
>
>此功能目前仍在測試中，您的組織可能尚未取得存取權。 檔案和功能可能會有所變更。
>
>如需Platform中一般可用CSV對應功能的資訊，請參閱 [將CSV檔案對應至現有結構](./existing-schema.md).

若要將CSV資料內嵌至 [!DNL Adobe Experience Platform]，資料必須對應至 [!DNL Experience Data Model] (XDM)結構。 您可以選擇對應至 [現有架構](./existing-schema.md)，但如果您不確定要使用哪個結構，或應如何架構，則可改為在Platform UI中使用以機器學習(ML)模型為基礎的動態建議。

## 快速入門

本教學課程需要妥善了解以下元件： [!DNL Platform]:

* [[!DNL Experience Data Model (XDM System)]](../../../xdm/home.md):標準化框架 [!DNL Platform] 組織客戶體驗資料。
   * 至少，您必須了解 [XDM中的行為](../../../xdm/home.md#data-behaviors)，以便您決定是否將資料對應至 [!UICONTROL 設定檔] 類（記錄行為）或 [!UICONTROL ExperienceEvent] 類（時間序列行為）。
* [批次內嵌](../../batch-ingestion/overview.md):透過 [!DNL Platform] 從用戶提供的資料檔案中獲取資料。
* [Adobe Experience Platform資料準備](../../batch-ingestion/overview.md):這套功能可讓您對應並轉換擷取的資料，以符合XDM結構。 上的檔案 [資料準備函式](../../../data-prep/functions.md) 與架構對應有明確的相關性。

## 提供資料流詳細資訊

在Experience PlatformUI中，選取 **[!UICONTROL 來源]** 的下一頁。 在 **[!UICONTROL 目錄]** 檢視，導覽至 **[!UICONTROL 本地系統]** 類別。 在 **[!UICONTROL 本機檔案上傳]**，選取 **[!UICONTROL 新增資料]**.

![此 [!UICONTROL 來源] 平台UI中的目錄，搭配 [!UICONTROL 新增資料] 在 [!UICONTROL 本機檔案上傳] 已選取](../../images/tutorials/map-csv-recommendations/local-file-upload.png)

此 **[!UICONTROL 對應CSV XDM結構]** 工作流程隨即顯示，從 **[!UICONTROL 資料流詳細資訊]** 步驟。

選擇 **[!UICONTROL 使用ML建議建立新結構]**，會顯示新控制項。 選擇要映射的CSV資料的適當類([!UICONTROL 設定檔] 或 [!UICONTROL ExperienceEvent])，並使用下拉式功能表，選取貴公司的相關產業。 如果貴組織在 [企業對企業(B2B)](../../../xdm/tutorials/relationship-b2b.md) 模型，選取 **[!UICONTROL B2B資料]** 核取方塊。

![此 [!UICONTROL 資料流詳細資訊] 步驟，並選取ML建議選項。 [!UICONTROL 設定檔] 已為類和選擇 [!UICONTROL 電信] 為行業選擇](../../images/tutorials/map-csv-recommendations/select-class-and-industry.png)

從此處，提供將從CSV資料建立之結構的名稱，以及包含在該架構下擷取之資料的輸出資料集名稱。

您可以選擇為資料流配置以下附加功能：

| 輸入名稱 | 說明 |
| --- | --- |
| [!UICONTROL 說明] | 資料流的說明。 |
| [!UICONTROL 錯誤診斷] | 啟用後，會為新擷取的批次產生錯誤訊息，當擷取中的對應批次時，即可檢視這些訊息 [API](../../batch-ingestion/api-overview.md). |
| [!UICONTROL 部分擷取] | 啟用後，新批次資料的有效記錄將在指定的錯誤臨界值內擷取。 此臨界值可讓您在整個批次失敗前設定可接受錯誤的百分比。 |
| [!UICONTROL 資料流詳細資訊] | 為將CSV資料匯入Platform的資料流提供名稱和可選說明。 啟動此工作流時，系統會自動為資料流分配預設名稱。 可選擇變更名稱。 |
| [!UICONTROL 警示] | 從 [產品內警報](../../../observability/alerts/overview.md) 在資料流啟動後，您要接收有關資料流狀態的資訊。 |

完成資料流配置後，請選擇 **[!UICONTROL 下一個]**.

![此 [!UICONTROL 資料流詳細資訊] 部分已完成](../../images/tutorials/map-csv-recommendations/dataflow-detail-complete.png)

## 選擇資料

在 **[!UICONTROL 選擇資料]** 步驟中，使用左欄上傳CSV檔案。 您可以選取 **[!UICONTROL 選擇檔案]** 要開啟檔案資源管理器對話框以從中選擇檔案，或者可以直接將檔案拖放到列上。

![此 [!UICONTROL 選擇檔案] 按鈕和拖放區域(在 [!UICONTROL 選擇資料] 步驟](../../images/tutorials/map-csv-recommendations/upload-files.png)

上傳檔案後，會顯示範例資料區段，顯示收到資料的前10列，以便您驗證其已正確上傳。 選擇 **[!UICONTROL 下一個]** 繼續。

![範例資料列會填入工作區中](../../images/tutorials/map-csv-recommendations/data-uploaded.png)

## 配置架構映射

運行ML模型以根據您的資料流配置和上載的CSV檔案生成新架構。 程式完成後， [!UICONTROL 對應] 步驟會填入，以連同所產生結構的完全可導覽檢視，一併顯示每個個別欄位的對應。

![此 [!UICONTROL 對應] 步驟，顯示所有已映射的CSV欄位以及產生的結構](../../images/tutorials/map-csv-recommendations/schema-generated.png)

從這裡，您可以選擇 [編輯欄位對應](#edit-mappings) 或 [更改與其關聯的欄位組](#edit-schema) 根據你的需要。 滿足後，選擇 **[!UICONTROL 完成]** 完成映射並啟動您先前配置的資料流。 CSV資料會擷取至系統中，並根據產生的結構填入資料集，以供下游Platform服務使用。

![此 [!UICONTROL 完成] 按鈕，完成CSV對應程式](../../images/tutorials/map-csv-recommendations/finish-mapping.png)

### 編輯欄位對應 {#edit-mappings}

使用欄位對應預覽來編輯現有對應或完全移除它們。 如需如何管理UI中對應集的詳細資訊，請參閱 [資料準備對應的UI指南](../../../data-prep/ui/mapping.md#mapping-interface).

### 編輯欄位群組 {#edit-field-groups}

CSV欄位會使用ML模型自動對應至現有欄位群組。 如果要變更任何特定CSV欄位的欄位群組，請選取 **[!UICONTROL 編輯]** 在架構樹旁邊。

![此 [!UICONTROL 編輯] 在架構樹旁邊選擇的按鈕](../../images/tutorials/map-csv-recommendations/edit-schema-structure.png)

將出現一個對話框，允許您編輯映射中任何欄位的顯示名稱、資料類型和欄位組。 選取編輯圖示(![編輯圖示](../../images/tutorials/map-csv-recommendations/edit-icon.png))，以在選取前，編輯其右欄的詳細資訊 **[!UICONTROL 套用]**.

![要更改的源欄位的建議欄位組](../../images/tutorials/map-csv-recommendations/select-schema-field.png)

調整完來源欄位的結構建議後，請選取 **[!UICONTROL 儲存]** 來套用變更。

## 後續步驟

本指南說明如何使用AI產生的建議，將CSV檔案對應至XDM架構，讓您透過批次內嵌將資料匯入Platform。

如需將CSV檔案對應至現有結構的步驟，請參閱 [現有架構對應工作流程](./existing-schema.md). 有關透過預先建立的來源連線即時將資料串流至Platform的資訊，請參閱 [來源概觀](../../../sources/home.md).
