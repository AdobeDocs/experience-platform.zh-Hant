---
keywords: Experience Platform；首頁；熱門主題；資料流；資料流
title: 配置資料流以從UI中的雲儲存源接收批處理資料
description: 本教程提供了有關如何配置新資料流以從UI中的雲儲存源接收批處理資料的步驟
exl-id: b327bbea-039d-4c04-afd3-f1d6a5f902a6
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '1795'
ht-degree: 0%

---

# 配置資料流以從UI中的雲儲存源接收批處理資料

本教程介紹如何配置資料流以將批資料從雲儲存源傳輸到Adobe Experience Platform。

## 快速入門

>[!NOTE]
>
>為了建立資料流以從雲儲存中提供批處理資料，您必須已經擁有對經過身份驗證的雲儲存源的訪問權限。 如果您沒有訪問權限，請轉到 [源概述](../../../../home.md#cloud-storage) 的子目錄。

本教程需要對以下Experience Platform組成部分進行有效理解：

* [[!DNL Experience Data Model (XDM)] 系統](../../../../../xdm/home.md):Experience Platform組織客戶體驗資料的標準化框架。
   * [架構組合的基礎](../../../../../xdm/schema/composition.md):瞭解XDM架構的基本構建基塊，包括架構組成中的關鍵原則和最佳做法。
   * [架構編輯器教程](../../../../../xdm/tutorials/create-schema-ui.md):瞭解如何使用架構編輯器UI建立自定義架構。
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md):基於來自多個源的聚合資料提供統一、即時的用戶配置檔案。

### 支援的檔案格式

批資料雲儲存源支援以下檔案格式進行接收：

* 分隔符分隔的值(DSV):任何單字元值都可用作DSV格式資料檔案的分隔符。
* [!DNL JavaScript Object Notation] (JSON):JSON格式的資料檔案必須符合XDM。
* [!DNL Apache Parquet]:拼花格式的資料檔案必須符合XDM。
* 壓縮檔案：JSON和分隔的檔案可壓縮為： `bzip2`。 `gzip`。 `deflate`。 `zipDeflate`。 `tarGzip`, `tar`。

## 添加資料

建立雲儲存帳戶後， **[!UICONTROL 添加資料]** 步驟，提供一個介面，供您瀏覽雲儲存檔案層次結構並選擇要帶到平台的資料夾或特定檔案。

* 介面的左側部分是目錄瀏覽器，顯示雲儲存檔案層次結構。
* 該介面的右側部分允許您從相容資料夾或檔案中預覽多達100行資料。

![](../../../../images/tutorials/dataflow/cloud-batch/select-data.png)

選擇要訪問資料夾層次結構的根資料夾。 在此處，您可以選擇一個資料夾以遞歸方式接收資料夾中的所有檔案。 在插入整個資料夾時，必須確保該資料夾中的所有檔案共用相同的資料格式和模式。

![](../../../../images/tutorials/dataflow/cloud-batch/folder-directory.png)

選擇資料夾後，右介面將更新到選定資料夾中第一個檔案的內容和結構的預覽。

![](../../../../images/tutorials/dataflow/cloud-batch/select-folder.png)

在此步驟中，您可以對資料進行多種配置，然後再繼續。 首先，選擇 **[!UICONTROL 資料格式]** 然後，在出現的下拉面板中為檔案選擇適當的資料格式。

下表顯示了支援的檔案類型的相應資料格式：

| 檔案類型 | 資料格式 |
| --- | --- |
| CSV | [!UICONTROL 分隔] |
| JSON | [!UICONTROL JSON] |
| 鑲木 | [!UICONTROL XDM鑲木地板] |

![](../../../../images/tutorials/dataflow/cloud-batch/data-format.png)

### 選擇列分隔符

配置資料格式後，可以在插入分隔檔案時設定列分隔符。 選擇 **[!UICONTROL 分隔符]** 選項，然後從下拉菜單中選擇分隔符。 該菜單顯示分隔符最常用的選項，包括逗號(`,`)，頁籤(`\t`)和管道(`|`)。

![](../../../../images/tutorials/dataflow/cloud-batch/delimiter.png)

如果希望使用自定義分隔符，請選擇 **[!UICONTROL 自定義]** 並在彈出輸入欄中輸入您選擇的單字元分隔符。

![](../../../../images/tutorials/dataflow/cloud-batch/custom.png)

### 正在攝取壓縮檔案

還可以通過指定壓縮類型來接收壓縮的JSON或分隔檔案。

在 [!UICONTROL 選擇資料] 步驟，選擇壓縮檔案以進行接收，然後選擇其適當的檔案類型以及是否符合XDM。 下一步，選擇 **[!UICONTROL 壓縮類型]** 然後為源資料選擇適當的壓縮檔案類型。

![](../../../../images/tutorials/dataflow/cloud-batch/custom.png)

要將特定檔案置於平台中，請選擇一個資料夾，然後選擇要接收的檔案。 在此步驟中，還可以使用檔案名旁邊的預覽表徵圖預覽給定資料夾中其他檔案的檔案內容。

完成後，選擇 **[!UICONTROL 下一個]**。

![](../../../../images/tutorials/dataflow/cloud-batch/select-file.png)

## 提供資料流詳細資訊

的 [!UICONTROL 資料流詳細資訊] 頁允許您選擇是使用現有資料集還是使用新資料集。 在此過程中，您還可以配置要接收到配置檔案的資料，並啟用設定，如 [!UICONTROL 錯誤診斷]。 [!UICONTROL 部分攝取], [!UICONTROL 警報]。

![](../../../../images/tutorials/dataflow/cloud-batch/dataflow-detail.png)

### 使用現有資料集

要將資料插入現有資料集，請選擇 **[!UICONTROL 現有資料集]**。 可以使用 [!UICONTROL 高級搜索] 選項，或通過在下拉菜單中滾動現有資料集清單來執行此操作。 選擇資料集後，請提供資料流的名稱和說明。

![](../../../../images/tutorials/dataflow/cloud-batch/existing.png)

### 使用新資料集

要插入新資料集，請選擇 **[!UICONTROL 新資料集]** 然後提供輸出資料集名稱和可選說明。 接下來，選擇要映射到的方案 [!UICONTROL 高級搜索] 選項，或通過在下拉菜單中滾動現有架構清單來執行。 選擇架構後，請提供資料流的名稱和說明。

![](../../../../images/tutorials/dataflow/cloud-batch/new.png)

### 啟用配置檔案和錯誤診斷

接下來，選擇 **[!UICONTROL 配置檔案資料集]** 切換以啟用配置檔案的資料集。 這允許您建立實體屬性和行為的整體視圖。 所有啟用配置檔案的資料集的資料都將包含在配置檔案中，並且在保存資料流時應用更改。

[!UICONTROL 錯誤診斷] 為資料流中出現的任何錯誤記錄啟用詳細的錯誤消息生成，同時 [!UICONTROL 部分攝取] 允許您接收包含錯誤的資料，最高可達您手動定義的特定閾值。 查看 [部分批處理接收概述](../../../../../ingestion/batch-ingestion/partial.md) 的子菜單。

![](../../../../images/tutorials/dataflow/cloud-batch/ingestion-configs.png)

### 啟用警報

您可以啟用警報來接收有關資料流狀態的通知。 從清單中選擇要訂閱的警報以接收有關資料流狀態的通知。 有關警報的詳細資訊，請參閱上的指南 [使用UI訂閱源警報](../../alerts.md)。

完成向資料流提供詳細資訊後，選擇 **[!UICONTROL 下一個]**。

![](../../../../images/tutorials/dataflow/cloud-batch/alerts.png)

## 將資料欄位映射到XDM架構

的 [!UICONTROL 映射] 步驟，提供一個介面，用於將源欄位從源架構映射到目標架構中相應的目標XDM欄位。

平台根據您選擇的目標架構或資料集為自動映射欄位提供智慧建議。 您可以手動調整映射規則以適合您的使用情形。 根據您的需要，您可以選擇直接映射欄位，或使用資料準備函式轉換源資料以導出計算值或計算值。 有關使用映射器介面和計算欄位的全面步驟，請參見 [資料準備UI指南](../../../../../data-prep/ui/mapping.md)。

成功映射源資料後，選擇 **[!UICONTROL 下一個]**。

![](../../../../images/tutorials/dataflow/cloud-batch/mapping.png)

## 計畫攝取運行

>[!IMPORTANT]
>
>強烈建議在使用 [FTP源](../../../../connectors/cloud-storage/ftp.md)。

的 [!UICONTROL 計畫] 步驟，允許您配置接收計畫以使用配置的映射自動接收選定的源資料。 預設情況下，計畫設定為 `Once`。 要調整攝取頻率，請選擇 **[!UICONTROL 頻率]** 然後從下拉菜單中選擇一個選項。

>[!TIP]
>
>在一次性攝取期間，間隔和回填不可見。

![調度](../../../../images/tutorials/dataflow/cloud-batch/scheduling.png)

如果你將攝入頻率設定為 `Minute`。 `Hour`。 `Day`或 `Week`，則必須設定一個間隔，以在每個接收之間建立一個設定的時間框架。 例如，接收頻率設定為 `Day` 間隔設定為 `15` 意味著資料流計畫每15天接收一次資料。

在此步驟中，您還可以 **回填** 並為資料增量接收定義一列。 回填用於接收歷史資料，而您為增量接收定義的列允許將新資料與現有資料區分。

有關計畫配置的詳細資訊，請參閱下表。

| 欄位 | 說明 |
| --- | --- |
| 頻率 | 攝入的頻率。 可選頻率包括 `Once`。 `Minute`。 `Hour`。 `Day`, `Week`。 |
| 間隔 | 設定所選頻率的間隔的整數。 間隔的值應為非零整數，並應設定為大於或等於15。 |
| 開始時間 | UTC時間戳，指示第一次攝取的時間設定為何時發生。 開始時間必須大於或等於當前UTC時間。 |
| 回填 | 一個布爾值，它確定最初接收的資料。 如果啟用回填，則在首次計畫接收期間將攝取指定路徑中的所有當前檔案。 如果禁用回填，則將只接收在第一次接收運行和開始時間之間載入的檔案。 在開始時間之前載入的檔案將不會被攝取。 |

>[!NOTE]
>
>對於批處理接收，每個後續資料流都會根據源檔案選擇要從源檔案接收的檔案 **上次修改** 時間戳。 這意味著批處理資料流從源中選擇新檔案或自上次流運行以來已修改的檔案。 此外，您必須確保檔案上載和計畫流運行之間有足夠的時間跨度，因為在計畫流運行時間之前，可能無法提取未完全上載到雲儲存帳戶的檔案以進行接收。

配置完接收計畫後，選擇 **[!UICONTROL 下一個]**。

![](../../../../images/tutorials/dataflow/cloud-batch/scheduling-configs.png)

## 查看資料流

的 **[!UICONTROL 審閱]** 步驟，允許您在建立新資料流之前查看它。 詳細資訊按以下類別分組：

* **[!UICONTROL 連接]**:顯示源類型、所選源檔案的相關路徑以及該源檔案中的列數。
* **[!UICONTROL 分配資料集和映射欄位]**:顯示源資料正被攝取到的資料集，包括該資料集所遵循的架構。
* **[!UICONTROL 計畫]**:顯示接收計畫的活動期間、頻率和間隔。

查看資料流後，按一下 **[!UICONTROL 完成]** 並為建立資料流留出一些時間。

![](../../../../images/tutorials/dataflow/cloud-batch/review.png)


## 後續步驟

按照本教程，您成功建立了資料流，以從外部雲儲存中導入資料，並深入瞭解了監視資料集。 要瞭解有關建立資料流的詳細資訊，您可以通過觀看下面的視頻來補充學習內容。 此外，現在下游可以使用傳入資料 [!DNL Platform] 服務，如 [!DNL Real-Time Customer Profile] 和 [!DNL Data Science Workspace]。 有關詳細資訊，請參閱以下文檔：

* [[!DNL Real-Time Customer Profile] 概覽](../../../../../profile/home.md)
* [[!DNL Data Science Workspace] 概覽](../../../../../data-science-workspace/home.md)

>[!WARNING]
>
> 的 [!DNL Platform] 以下視頻中顯示的UI已過期。 有關最新的UI螢幕截圖和功能，請參閱上面的文檔。

>[!VIDEO](https://video.tv.adobe.com/v/29695?quality=12&learn=on)

## 附錄

以下各節提供了有關使用源連接器的其他資訊。

## 監視資料流

建立資料流後，您可以監視通過它攝取的資料，以查看有關攝取率、成功和錯誤的資訊。 有關如何監視資料流的詳細資訊，請訪問上的教程 [監視UI中的帳戶和資料流](../../monitor.md)。

## 更新資料流

要更新資料流計畫、映射和一般資訊的配置，請訪問上的教程 [更新UI中的源資料流](../../update-dataflows.md)

## 刪除資料流

您可以刪除不再需要或使用 **[!UICONTROL 刪除]** 函式 **[!UICONTROL 資料流]** 工作區。 有關如何刪除資料流的詳細資訊，請訪問上的教程 [刪除UI中的資料流](../../delete.md)。