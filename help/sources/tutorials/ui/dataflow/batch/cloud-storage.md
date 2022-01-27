---
keywords: Experience Platform；首頁；熱門主題；資料流；資料流
solution: Experience Platform
title: 在UI中為雲儲存批處理連接器配置資料流
topic-legacy: overview
type: Tutorial
description: 資料流是從源資料集中檢索資料並將資料接收到平台資料集的計畫任務。 本教程提供了使用雲儲存帳戶配置新資料流的步驟。
exl-id: b327bbea-039d-4c04-afd3-f1d6a5f902a6
source-git-commit: 86d8313d7acea41e7b3bcea6554e91ea2190ae69
workflow-type: tm+mt
source-wordcount: '2083'
ht-degree: 0%

---

# 在UI中為雲儲存批處理連接配置資料流

資料流是從源中檢索資料並將資料接收到的計畫任務 [!DNL Platform] 資料集。 本教程提供了使用雲儲存帳戶配置新資料流的步驟。

## 快速入門

本教程需要對Adobe Experience Platform的以下部分進行有效的理解：

* [[!DNL Experience Data Model (XDM)] 系統](../../../../../xdm/home.md):標準化框架 [!DNL Experience Platform] 組織客戶體驗資料。
   * [架構組合的基礎](../../../../../xdm/schema/composition.md):瞭解XDM架構的基本構建基塊，包括架構組成中的關鍵原則和最佳做法。
   * [架構編輯器教程](../../../../../xdm/tutorials/create-schema-ui.md):瞭解如何使用架構編輯器UI建立自定義架構。
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md):基於來自多個源的聚合資料提供統一、即時的用戶配置檔案。

此外，本教程要求您已建立雲儲存帳戶。 有關在UI中建立不同雲儲存帳戶的教程清單，請參見 [源連接器概述](../../../../home.md)。

### 支援的檔案格式

[!DNL Experience Platform] 支援從外部儲存接收的以下檔案格式：

* 分隔符分隔的值(DSV):任何單字元值都可用作DSV格式資料檔案的分隔符。
* [!DNL JavaScript Object Notation] (JSON):JSON格式的資料檔案必須符合XDM。
* [!DNL Apache Parquet]:拼花格式的資料檔案必須符合XDM。
* 壓縮檔案：JSON和分隔的檔案可壓縮為： `bzip2`。 `gzip`。 `deflate`。 `zipDeflate`。 `tarGzip`, `tar`。

## 選擇資料

建立雲儲存帳戶後， **[!UICONTROL 選擇資料]** 步驟，為您提供一個介面以瀏覽雲儲存檔案層次結構。

* 介面的左側是目錄瀏覽器，顯示雲儲存檔案和目錄。
* 該介面的右側部分允許您從相容檔案中預覽多達100行資料。

![介面](../../../../images/tutorials/dataflow/cloud-storage/batch/interface.png)

選擇列出的資料夾允許您將資料夾層次結構遍歷到更深入的資料夾中。 您可以選擇單個資料夾以遞歸方式接收資料夾中的所有檔案。 在插入整個資料夾時，必須確保資料夾中的所有檔案共用同一架構。

選擇相容檔案或資料夾後，從 [!UICONTROL 選擇資料格式] 下拉菜單。

下表顯示了支援的檔案類型的相應資料格式：

| 檔案類型 | 資料格式 |
| --- | --- |
| CSV | [!UICONTROL 分隔] |
| JSON | [!UICONTROL JSON] |
| 鑲木 | [!UICONTROL XDM鑲木地板] |

選擇 **[!UICONTROL JSON]** 等待幾秒後，預覽介面將填充。

![選擇資料](../../../../images/tutorials/dataflow/cloud-storage/batch/select-data.png)

>[!NOTE]
>
>與分隔檔案和JSON檔案類型不同，Parfect格式的檔案不可用於預覽。

預覽介面允許您檢查檔案的內容和結構。 預設情況下，預覽介面將顯示所選資料夾中的第一個檔案。

要預覽其他檔案，請選擇要檢查的檔案名稱旁邊的預覽表徵圖。

![預設預覽](../../../../images/tutorials/dataflow/cloud-storage/batch/default-preview.png)

檢查資料夾中檔案的內容和結構後，選擇 **[!UICONTROL 下一個]** 以遞歸方式接收資料夾中的所有檔案。

![選擇資料夾](../../../../images/tutorials/dataflow/cloud-storage/batch/select-folder.png)

如果希望選擇特定檔案，請選擇要接收的檔案，然後選擇 **[!UICONTROL 下一個]**。

![選擇檔案](../../../../images/tutorials/dataflow/cloud-storage/batch/select-file.png)

### 為分隔檔案設定自定義分隔符

可以在插入分隔檔案時設定自定義分隔符。 選擇 **[!UICONTROL 分隔符]** 選項，然後從下拉菜單中選擇分隔符。 該菜單顯示分隔符最常用的選項，包括逗號(`,`)，頁籤(`\t`)和管道(`|`)。 如果希望使用自定義分隔符，請選擇 **[!UICONTROL 自定義]** 並在彈出輸入欄中輸入您選擇的單字元分隔符。

選擇資料格式並設定分隔符後，選擇 **[!UICONTROL 下一個]**。

![](../../../../images/tutorials/dataflow/cloud-storage/batch/delimiter.png)

### 正在攝取壓縮檔案

可以通過指定壓縮類型來接收壓縮的JSON或分隔檔案。

在 [!UICONTROL 選擇資料] 步驟，選擇壓縮檔案以進行接收，然後選擇其適當的檔案類型以及是否符合XDM。 下一步，選擇 **[!UICONTROL 壓縮類型]** 然後為源資料選擇適當的壓縮檔案類型。

如果標識了壓縮檔案類型，請選擇 **[!UICONTROL 下一個]** 繼續。

![](../../../../images/tutorials/dataflow/cloud-storage/batch/compressed-files.png)

## 將資料欄位映射到XDM架構

的 **[!UICONTROL 映射]** 步驟，提供交互介面將源資料映射到 [!DNL Platform] 資料集。 以Parce格式化的源檔案必須符合XDM要求，並且不要求您手動配置映射，而CSV檔案要求您顯式配置映射，但允許您選擇要映射的源資料欄位。 JSON檔案（如果標籤為XDM投訴）不需要手動配置。 但是，如果未將其標籤為符合XDM，則需要顯式配置映射。

為要接收到的入站資料選擇資料集。 可以使用現有資料集或建立新資料集。

**使用現有資料集**

要將資料插入現有資料集，請選擇 **[!UICONTROL 現有資料集]**，然後選擇資料集表徵圖。

![](../../../../images/tutorials/dataflow/cloud-storage/batch/use-existing-data.png)

的 **[!UICONTROL 選擇資料集]** 對話框。 查找要使用的資料集，選擇它，然後按一下 **[!UICONTROL 繼續]**。

![](../../../../images/tutorials/dataflow/cloud-storage/batch/select-existing-dataset.png)

**使用新資料集**

要將資料插入新資料集，請選擇 **[!UICONTROL 新資料集]** 並在提供的欄位中輸入資料集的名稱和說明。 要添加方案，可以在 **[!UICONTROL 選擇架構]** 對話框。 或者，可以選取 **[!UICONTROL 架構高級搜索]** 以搜索適當的架構。

在此步驟中，您可以為 [!DNL Real-time Customer Profile] 並建立實體屬性和行為的整體視圖。 來自所有已啟用的資料集的資料將包含在 [!DNL Profile] 並在保存資料流時應用更改。

切換 **[!UICONTROL 配置檔案資料集]** 按鈕啟用目標資料集 [!DNL Profile]。

![](../../../../images/tutorials/dataflow/cloud-storage/batch/new-dataset.png)

的 **[!UICONTROL 選擇架構]** 對話框。 選擇要應用到新資料集的架構，然後選擇 **[!UICONTROL 完成]**。

![](../../../../images/tutorials/dataflow/cloud-storage/batch/select-schema.png)

根據您的需要，您可以選擇直接映射欄位，或使用資料準備函式轉換源資料以導出計算值或計算值。 有關使用映射器介面和計算欄位的全面步驟，請參見 [資料準備UI指南](../../../../../data-prep/ui/mapping.md)。

![](../../../../images/tutorials/dataflow/cloud-storage/batch/mapping.png)

對於JSON檔案，除了直接將欄位映射到其他欄位外，您還可以將對象直接映射到其他對象和陣列到其他陣列。您還可以使用雲儲存源連接器預覽和映射JSON檔案中的陣列等複雜資料類型。

![](../../../../images/tutorials/dataflow/cloud-storage/batch/source-field-json.png)

![](../../../../images/tutorials/dataflow/cloud-storage/batch/target-field-json.png)

請注意，您不能跨不同類型進行映射。 例如，不能將對象映射到陣列，或將欄位映射到對象。

>[!TIP]
>
>平台根據您選擇的目標架構或資料集為自動映射欄位提供智慧建議。 您可以手動調整映射規則以適合您的使用情形。

選擇 **[!UICONTROL 預覽資料]** 查看所選資料集中最多100行示例資料的映射結果。

在預覽期間，標識列作為第一個欄位按優先順序排列，因為它是驗證映射結果時所必需的關鍵資訊。

![](../../../../images/tutorials/dataflow/cloud-storage/batch/mapping-preview.png)

映射源資料後，選擇 **[!UICONTROL 關閉]**。

## 計畫攝取運行

的 **[!UICONTROL 計畫]** 步驟，允許您配置接收計畫以使用配置的映射自動接收選定的源資料。 下表概述了計畫的不同可配置欄位：

| 欄位 | 說明 |
| --- | --- |
| 頻率 | 可選頻率包括 `Once`。 `Minute`。 `Hour`。 `Day`, `Week`。 |
| 間隔 | 設定所選頻率的間隔的整數。 |
| 開始時間 | UTC時間戳，指示第一次攝取的時間設定為何時發生。 |
| 回填 | 一個布爾值，它確定最初接收的資料。 如果 **[!UICONTROL 回填]** 啟用後，指定路徑中的所有當前檔案將在首次計畫接收期間被接收。 如果 **[!UICONTROL 回填]** 禁用，將只接收在第一次接收運行和開始時間之間載入的檔案。 在開始時間之前載入的檔案將不會被攝取。 |

資料流設計為按計畫自動接收資料。 從選擇攝取頻率開始。 接下來，設定間隔以指定兩個流運行之間的時段。 間隔的值應為非零整數，並應設定為大於或等於15。

要設定攝取的開始時間，請調整在開始時間框中顯示的日期和時間。 或者，可以選擇日曆表徵圖以編輯開始時間值。 開始時間必須大於或等於當前時間（以UTC表示）。

提供計畫值並選擇 **[!UICONTROL 下一個]**。

>[!NOTE]
>
>對於批處理接收，每個後續資料流都會根據源檔案選擇要從源檔案接收的檔案 **上次修改** 時間戳。 這意味著批處理資料流從源中選擇新檔案或自上次流運行以來已修改的檔案。 此外，您必須確保檔案上載和計畫流運行之間有足夠的時間跨度，因為在計畫流運行時間之前，可能無法提取未完全上載到雲儲存帳戶的檔案以進行接收。

![](../../../../images/tutorials/dataflow/cloud-storage/batch/scheduling-interval-on.png)

### 設定一次性接收資料流

要設定一次性接收，請選擇頻率下拉箭頭並選擇 **[!UICONTROL 一次]**。 只要開始時間在將來保持不變，您就可以繼續編輯用於一次性頻率接收的資料流集。 一旦開始時間過去，就不能再編輯一次性頻率值。 **[!UICONTROL 間隔]** 和 **[!UICONTROL 回填]** 設定一次性接收資料流時不可見。

>[!IMPORTANT]
>
>強烈建議在使用 [FTP連接器](../../../../connectors/cloud-storage/ftp.md)。

為計畫提供適當值後，選擇 **[!UICONTROL 下一個]**。

![](../../../../images/tutorials/dataflow/cloud-storage/batch/scheduling-once.png)

## 提供資料流詳細資訊

的 **[!UICONTROL 資料流詳細資訊]** 步驟，使您可以命名並簡要描述新資料流。

在此過程中，您還可以 **[!UICONTROL 部分攝取]** 和 **[!UICONTROL 錯誤診斷]**。 啟用 **[!UICONTROL 部分攝取]** 提供了接收包含錯誤的資料的能力，可以設定一定閾值。 啟用 **[!UICONTROL 錯誤診斷]** 將提供有關單獨批處理的任何不正確資料的詳細資訊。 有關詳細資訊，請參見 [部分批處理接收概述](../../../../../ingestion/batch-ingestion/partial.md)。

為資料流提供值並選擇 **[!UICONTROL 下一個]**。

![](../../../../images/tutorials/dataflow/cloud-storage/batch/dataflow-detail.png)

## 查看資料流

的 **[!UICONTROL 審閱]** 步驟，允許您在建立新資料流之前查看它。 詳細資訊按以下類別分組：

* **[!UICONTROL 連接]**:顯示源類型、所選源檔案的相關路徑以及該源檔案中的列數。
* **[!UICONTROL 分配資料集和映射欄位]**:顯示源資料正被攝取到的資料集，包括該資料集所遵循的架構。
* **[!UICONTROL 計畫]**:顯示接收計畫的活動期間、頻率和間隔。

查看資料流後，按一下 **[!UICONTROL 完成]** 並為建立資料流留出一些時間。

![](../../../../images/tutorials/dataflow/cloud-storage/batch/review.png)

## 監視資料流

建立資料流後，您可以監視通過它攝取的資料，以查看有關攝取率、成功和錯誤的資訊。 有關如何監視資料流的詳細資訊，請參見上的教程 [監視UI中的帳戶和資料流](../../monitor.md)。

## 刪除資料流

您可以刪除不再需要或使用 **[!UICONTROL 刪除]** 函式 **[!UICONTROL 資料流]** 工作區。 有關如何刪除資料流的詳細資訊，請參見上的教程 [刪除UI中的資料流](../../delete.md)。

## 後續步驟

按照本教程，您成功建立了資料流，以從外部雲儲存中導入資料，並深入瞭解了監視資料集。 要瞭解有關建立資料流的詳細資訊，您可以通過觀看下面的視頻來補充學習內容。 此外，現在下游可以使用傳入資料 [!DNL Platform] 服務，如 [!DNL Real-time Customer Profile] 和 [!DNL Data Science Workspace]。 有關詳細資訊，請參閱以下文檔：

* [[!DNL Real-time Customer Profile] 概觀](../../../../../profile/home.md)
* [[!DNL Data Science Workspace] 概觀](../../../../../data-science-workspace/home.md)

>[!WARNING]
>
> 的 [!DNL Platform] 以下視頻中顯示的UI已過期。 有關最新的UI螢幕截圖和功能，請參閱上面的文檔。

>[!VIDEO](https://video.tv.adobe.com/v/29695?quality=12&learn=on)

## 附錄

以下各節提供了有關使用源連接器的其他資訊。

### 禁用資料流

建立資料流時，它會立即變為活動狀態，並根據給定的時間表接收資料。 您可以隨時按照以下說明禁用活動資料流。

在 **[!UICONTROL 源]** 工作區，按一下 **[!UICONTROL 瀏覽]** 頁籤。 接下來，按一下與要禁用的活動資料流關聯的帳戶名稱。

![](../../../../images/tutorials/dataflow/cloud-storage/batch/browse.png)

的 **[!UICONTROL 源活動]** 的子菜單。 從清單中選擇活動資料流以開啟其 **[!UICONTROL 屬性]** 框中，該框包含 **[!UICONTROL 已啟用]** 切換按鈕。 按一下切換以禁用資料流。 禁用資料流後，可以使用相同的切換功能重新啟用資料流。

![](../../../../images/tutorials/dataflow/cloud-storage/batch/disable-source.png)

### 激活入站資料 [!DNL Profile] 人口

來自源連接器的入站資料可用於豐富和填充 [!DNL Real-time Customer Profile] 資料。 有關填充的詳細資訊 [!DNL Real-time Customer Profile] 資料，請參見上的教程 [概況填充](../../profile.md)。
