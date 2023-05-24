---
title: 使用AI生成的Recommendations將CSV檔案映射到XDM架構
description: 本教程介紹如何使用AI生成的建議案將CSV檔案映射到XDM架構。
exl-id: 1daedf0b-5a25-4ca5-ae5d-e9ee1eae9e4d
source-git-commit: df6f76be6beba962b1795bd33dc753ef04267734
workflow-type: tm+mt
source-wordcount: '1014'
ht-degree: 1%

---

# 使用AI生成的建議將CSV檔案映射到XDM架構

>[!NOTE]
>
>有關平台中通常可用的CSV映射功能的資訊，請參閱上的文檔 [將CSV檔案映射到現有架構](./existing-schema.md)。

為了將CSV資料 [!DNL Adobe Experience Platform]，資料必須映射到 [!DNL Experience Data Model] (XDM)架構。 您可以選擇映射到 [現有架構](./existing-schema.md)，但如果您不確切知道要使用哪個架構或應如何構建它，則可以在平台UI中使用基於機器學習(ML)模型的動態建議。

## 快速入門

本教程需要對以下元件進行有效的瞭解 [!DNL Platform]:

* [[!DNL Experience Data Model (XDM System)]](../../../xdm/home.md):標準化框架 [!DNL Platform] 組織客戶體驗資料。
   * 至少，你必須理解 [XDM中的行為](../../../xdm/home.md#data-behaviors)，這樣您就可以決定是否將資料映射到 [!UICONTROL 配置檔案] 類（記錄行為）或 [!UICONTROL 體驗事件] 類（時間序列行為）。
* [批量攝取](../../batch-ingestion/overview.md):方法 [!DNL Platform] 從用戶提供的資料檔案中接收資料。
* [Adobe Experience Platform資料準備](../../batch-ingestion/overview.md):一套功能，允許您映射和轉換所攝取的資料以符合XDM架構。 有關 [資料準備功能](../../../data-prep/functions.md) 與架構映射特別相關。

## 提供資料流詳細資訊

在Experience PlatformUI中，選擇 **[!UICONTROL 源]** 的子菜單。 在 **[!UICONTROL 目錄]** 視圖，導航至 **[!UICONTROL 本地系統]** 的子菜單。 下 **[!UICONTROL 本地檔案上載]**&#x200B;選中 **[!UICONTROL 添加資料]**。

![的 [!UICONTROL 源] 平台UI中的目錄， [!UICONTROL 添加資料] 在 [!UICONTROL 本地檔案上載] 的子菜單。](../../images/tutorials/map-csv-recommendations/local-file-upload.png)

的 **[!UICONTROL 映射CSV XDM架構]** 工作流」(workflow)，從 **[!UICONTROL 資料流詳細資訊]** 的子菜單。

選擇 **[!UICONTROL 使用ML建議建立新架構]**，導致出現新控制項。 為要映射的CSV資料選擇適當的類([!UICONTROL 配置檔案] 或 [!UICONTROL 體驗事件])。 您可以選擇使用下拉菜單為您的業務選擇相關行業，如果提供的類別不適用於您，則將其留空。 如果您的組織在 [企業對企業(B2B)](../../../xdm/tutorials/relationship-b2b.md) 模型，選擇 **[!UICONTROL B2B資料]** 複選框。

![的 [!UICONTROL 資料流詳細資訊] 步驟，選擇ML建議選項。 [!UICONTROL 配置檔案] 為類和選擇 [!UICONTROL 電信] 為行業選擇](../../images/tutorials/map-csv-recommendations/select-class-and-industry.png)

在此處，提供將從CSV資料建立的架構的名稱，以及將包含在該架構下接收的資料的輸出資料集的名稱。

您可以選擇在繼續之前為資料流配置以下附加功能：

| 輸入名稱 | 說明 |
| --- | --- |
| [!UICONTROL 說明] | 資料流的說明。 |
| [!UICONTROL 錯誤診斷] | 啟用後，將為新接收的批生成錯誤消息，在獲取中的相應批時可以查看這些消息 [API](../../batch-ingestion/api-overview.md)。 |
| [!UICONTROL 部分攝取] | 啟用後，將在指定的錯誤閾值內接收新批資料的有效記錄。 此閾值允許您在整個批失敗之前配置可接受錯誤的百分比。 |
| [!UICONTROL 資料流詳細資訊] | 提供將CSV資料引入平台的資料流的名稱和可選說明。 啟動此工作流時，將自動為資料流分配預設名稱。 更改名稱是可選的。 |
| [!UICONTROL 警示] | 從 [產品內警報](../../../observability/alerts/overview.md) 啟動資料流後要接收的有關資料流狀態的資訊。 |

{style="table-layout:auto"}

配置完資料流後，選擇 **[!UICONTROL 下一個]**。

![的 [!UICONTROL 資料流詳細資訊] 的子菜單。](../../images/tutorials/map-csv-recommendations/dataflow-detail-complete.png)

## 選擇資料

在 **[!UICONTROL 選擇資料]** 步驟，使用左欄上載CSV檔案。 可以選擇 **[!UICONTROL 選擇檔案]** 開啟檔案資源管理器對話框以從中選擇檔案，或者可以直接將檔案拖放到列上。

![的 [!UICONTROL 選擇檔案] 按鈕和在 [!UICONTROL 選擇資料] 的子菜單。](../../images/tutorials/map-csv-recommendations/upload-files.png)

上載檔案後，將出現一個示例資料部分，其中顯示接收資料的前十行，以便您能夠驗證其已正確上載。 選取&#x200B;**[!UICONTROL 「下一步」]**&#x200B;以繼續。

![示例資料行填充在工作區中](../../images/tutorials/map-csv-recommendations/data-uploaded.png)

## 配置架構映射

運行ML模型以根據資料流配置和上載的CSV檔案生成新模式。 當流程完成時， [!UICONTROL 映射] 步驟填充以在生成的架構結構的完全可導航視圖旁邊顯示每個單個欄位的映射。

![的 [!UICONTROL 映射] 步驟，顯示映射的所有CSV欄位和生成的架構結構。](../../images/tutorials/map-csv-recommendations/schema-generated.png)

從這裡，您可以選擇 [編輯欄位映射](#edit-mappings) 或 [更改與其關聯的欄位組](#edit-schema) 根據你的需要。 滿足後，選擇 **[!UICONTROL 完成]** 完成映射並啟動您先前配置的資料流。 CSV資料被接收到系統中，並基於所生成的模式結構填充資料集，該資料集準備由下游平台服務使用。

![的 [!UICONTROL 完成] 按鈕，完成CSV映射過程。](../../images/tutorials/map-csv-recommendations/finish-mapping.png)

### 編輯欄位映射 {#edit-mappings}

使用欄位映射預覽可編輯現有映射或完全刪除它們。 有關如何管理UI中映射集的詳細資訊，請參閱 [資料準備映射的UI指南](../../../data-prep/ui/mapping.md#mapping-interface)。

### 編輯欄位組 {#edit-field-groups}

使用ML模型將CSV欄位自動映射到現有XDM欄位組。 如果要更改任何特定CSV欄位的欄位組，請選擇 **[!UICONTROL 編輯]** 模式樹旁邊。

![的 [!UICONTROL 編輯] 按鈕。](../../images/tutorials/map-csv-recommendations/edit-schema-structure.png)

此時將出現一個對話框，允許您編輯映射中任何欄位的顯示名稱、資料類型和欄位組。 選擇編輯表徵圖(![編輯表徵圖](../../images/tutorials/map-csv-recommendations/edit-icon.png))旁邊的，以在右列中編輯其詳細資訊，然後選擇 **[!UICONTROL 應用]**。

![正在更改的源欄位的建議欄位組。](../../images/tutorials/map-csv-recommendations/select-schema-field.png)

調整源欄位的架構建議案後，選擇 **[!UICONTROL 保存]** 按鈕。

## 後續步驟

本指南介紹了如何使用AI生成的建議案將CSV檔案映射到XDM架構，從而允許您通過批處理接收將資料引入平台。

有關將CSV檔案映射到現有架構的步驟，請參閱 [現有架構映射工作流](./existing-schema.md)。 有關通過預構建的源連接即時將資料流式傳輸到平台的資訊，請參閱 [源概述](../../../sources/home.md)。
