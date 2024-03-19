---
title: 使用UI從Snowflake資料庫串流資料以Experience Platform
type: Tutorial
description: 瞭解如何從Snwoflake資料庫將資料串流到Experience Platform
badgeUltimate: label="Ultimate" type="Positive"
source-git-commit: c80535cbb5dda55f1cf145f9f40bbcd40c78e63e
workflow-type: tm+mt
source-wordcount: '1604'
ht-degree: 2%

---

# 從您的串流資料 [!DNL Snowflake] 要使用UIExperience Platform的資料庫

瞭解如何使用使用者介面將資料從您的 [!DNL Snowflake] 資料庫至Adobe Experience Platform，請遵循本指南。

## 快速入門

本教學課程需要您實際瞭解下列Experience Platform元件：

* [[!DNL Experience Data Model (XDM)] 系統](../../../../../xdm/home.md)：作為依據的標準化架構 [!DNL Experience Platform] 組織客戶體驗資料。
   * [結構描述組合基本概念](../../../../../xdm/schema/composition.md)：瞭解XDM結構描述的基本建置區塊，包括結構描述組合中的關鍵原則和最佳實務。
   * [結構描述編輯器教學課程](../../../../../xdm/tutorials/create-schema-ui.md)：瞭解如何使用結構編輯器UI建立自訂結構描述。
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md)：根據來自多個來源的彙總資料，提供統一的即時消費者個人檔案。

### 驗證

閱讀指南： [必備條件設定 [!DNL Snowflake] 串流資料](../../../../connectors/databases/snowflake-streaming.md) 瞭解從擷取串流資料前，需要完成的步驟 [!DNL Snowflake] 以Experience Platform。

## 使用 [!DNL Snowflake Streaming] 要串流的來源 [!DNL Snowflake] 要Experience Platform的資料

在Platform UI中選取 **[!UICONTROL 來源]** 從左側導覽存取 [!UICONTROL 來源] 工作區。 您可以從熒幕左側的目錄中選取適當的類別。 或者，您可以使用搜尋選項來尋找您要使用的特定來源。

在 *資料庫* 類別，選取 **[!DNL Snowflake Streaming]**，然後選取 **[!UICONTROL 新增資料]**.

>[!TIP]
>
>來源目錄中無已驗證帳戶的來源會顯示 **[!UICONTROL 設定]** 選項。 一旦驗證帳戶存在，此選項就會變更為 **[!UICONTROL 新增資料]**.

![Experience PlatformUI中的來源目錄，且已選取Snowflake串流來源卡。](../../../../images/tutorials/create/snowflake-streaming/catalog.png)

此 **[!UICONTROL 連線Snowflake串流帳戶]** 頁面便會顯示。 您可以在此頁面使用新的或現有的證明資料。

>[!BEGINTABS]

>[!TAB 建立新帳戶]

若要建立新帳戶，請選取 **[!UICONTROL 新帳戶]** 並提供名稱、選擇性說明和您的認證。

完成後，選取 **[!UICONTROL 連線到來源]** 然後等待一段時間以建立新連線。

![來源工作流程的新帳戶建立介面。](../../../../images/tutorials/create/snowflake-streaming/new.png)

| 認證 | 說明 |
| --- | --- |
| 帳戶 | 您的名稱 [!DNL Snowflake] 帳戶。 |
| 倉儲 | 您的名稱 [!DNL Snowflake] 倉儲。 倉儲管理中查詢的執行 [!DNL Snowflake]. 每個 [!DNL Snowflake] warehouse彼此獨立，必須個別存取以便Experience Platform資料。 |
| 資料庫 | 您的名稱 [!DNL Snowflake] 資料庫。 資料庫包含您要帶入Experience Platform的資料。 |
| 綱要 | （選擇性）與您的資料庫架構關聯的資料庫架構 [!DNL Snowflake] 帳戶。 |
| 使用者名稱 | 您的使用者名稱 [!DNL Snowflake] 帳戶。 |
| 密碼 | 您的密碼 [!DNL Snowflake] 帳戶。 |
| 角色 | （選用）可以為使用者提供的自訂角色，用於特定連線。 如果未提供，則此值預設為 `public`. |

如需建立帳戶的詳細資訊，請參閱以下章節： [設定角色設定](../../../../connectors/databases/snowflake-streaming.md#configure-role-settings) 在 [!DNL Snowflake Streaming] 概述。

>[!TAB 使用現有帳戶]

若要使用現有帳戶，請選取 **[!UICONTROL 現有帳戶]** 然後從現有帳戶目錄中選取所需的帳戶。

選取 **[!UICONTROL 下一個]** 以繼續進行。

![來源目錄的現有帳戶選擇頁面。](../../../../images/tutorials/create/snowflake-streaming/existing.png)

>[!ENDTABS]

## 選取資料 {#select-data}

>[!IMPORTANT]
>
>時間戳記欄必須存在於您的來源表格中，才能建立串流資料流。 Experience Platform需有時間戳記，才能知道何時會擷取資料，以及何時會串流增量資料。 您可以回溯性地為現有連線新增時間戳記欄，並建立新的資料流。

此 [!UICONTROL 選取資料] 步驟隨即顯示。 在此步驟中，您必須選取要匯入至Experience Platform的資料、設定時間戳記和時區，並提供用於擷取原始資料的範例來源資料檔案。

使用畫面左側的資料庫目錄，並選取您要匯入以Experience Platform的表格。

![選取資料介面，其中已選取資料庫表格。](../../../../images/tutorials/create/snowflake-streaming/select-table.png)

接著，選取表格的時間戳記欄型別。 您可以在兩種時間戳記欄型別之間進行選取： `TIMESTAMP_NTZ` 或  `TIMESTAMP_LTZ`. 如果您選取欄型別 `TIMESTAMP_NTZ`，那麼您也必須提供時區。 您的欄應該有非null的限制。 如需詳細資訊，請閱讀以下章節： [限制和常見問答]

您也可以在此步驟中設定回填設定。 回填會決定最初要擷取的資料。 如果已啟用回填，則會在第一次排程擷取期間擷取指定路徑中的所有目前檔案。 如果沒有，則只會擷取在第一次內嵌執行與開始時間之間載入的檔案。 將不會擷取在開始時間之前載入的檔案。

選取 **[!UICONTROL 回填]** 切換以啟用回填。

![時間戳記、時區和回填設定步驟。](../../../../images/tutorials/create/snowflake-streaming/timezone.png)

最後，選取 **[!UICONTROL 選擇檔案]** 上傳範例來源資料以幫助建立對應集，這將在後續步驟中用於將原始資料對應到Experience Data Model (XDM)。

完成後，選取 **[!UICONTROL 下一個]** 以繼續進行。

![來源範例資料的預覽。](../../../../images/tutorials/create/snowflake-streaming/preview.png)

## 提供資料集和資料流詳細資料 {#provide-dataset-and-dataflow-details}

接下來，您必須提供有關資料集和資料流的資訊。

### 資料集詳細資訊 {#dataset-details}

資料集是資料集合的儲存和管理結構，通常是包含方案 (欄) 和欄位 (列) 的表格。 成功擷取至Experience Platform的資料會以資料集的形式保留在資料湖中。 在此步驟中，您可以建立新資料集或使用現有資料集。

>[!BEGINTABS]

>[!TAB 使用新資料集]

若要使用新資料集，請選取「 」 **[!UICONTROL 新資料集]**，然後為資料集提供名稱和說明（選用）。 您也必須選取您的資料集所要遵守的Experience Data Model (XDM)結構。

![新的資料集選取介面。](../../../../images/tutorials/create/snowflake-streaming/new-dataset.png)

| 新資料集詳細資料 | 說明 |
| --- | --- |
| 輸出資料集名稱 | 新資料集的名稱。 |
| 說明 | （選用）新資料集的簡短總覽。 |
| 綱要 | 貴組織中現有的結構描述下拉式清單。 您也可以在來源設定程式之前建立自己的結構描述。 如需詳細資訊，請閱讀以下指南： [在UI中建立XDM結構描述](../../../../../xdm/tutorials/create-schema-ui.md). |

>[!TAB 使用現有的資料集]

如果您已有現有的資料集，請選取「 」 **[!UICONTROL 現有資料集]** 然後使用 **[!UICONTROL 進階搜尋]** 選項可檢視貴組織中所有資料集的視窗，包括其個別詳細資訊，例如是否啟用這些資料集以擷取至Real-Time Customer Profile。

![現有的資料集選取介面。](../../../../images/tutorials/create/snowflake-streaming/existing-dataset.png)

>[!ENDTABS]

+++選取步驟以啟用設定檔擷取、錯誤診斷及部分擷取。

如果您的資料集已啟用即時客戶個人檔案，那麼在此步驟中，您可以切換 **[!UICONTROL 設定檔資料集]** 啟用您的資料以供設定檔擷取。 您也可以使用此步驟來啟用 **[!UICONTROL 錯誤診斷]** 和 **[!UICONTROL 部分擷取]**.

* **[!UICONTROL 錯誤診斷]**：選取 **[!UICONTROL 錯誤診斷]** 指示來源產生錯誤診斷，以便您稍後在監控資料集活動和資料流狀態時參考。
* **[!UICONTROL 部分擷取]**：部分批次擷取是指擷取包含錯誤的資料的能力，上限為特定可設定的臨界值。 此功能可讓您將所有精確資料成功擷取到Experience Platform，同時所有不正確的資料會個別批次處理，並提供無效原因的資訊。

+++

### 資料流詳細資料 {#dataflow-details}

設定資料集後，您必須提供資料流的詳細資訊，包括名稱、選用的說明和警報設定。

![資料流詳細資料設定步驟。](../../../../images/tutorials/create/snowflake-streaming/dataflow-details.png)

| 資料流設定 | 說明 |
| --- | --- |
| 資料流名稱 | 資料流的名稱。  依預設，這將使用正在匯入的檔案名稱。 |
| 說明 | （選用）資料流的簡短說明。 |
| 警報 | Experience Platform可產生使用者可訂閱的事件型警報。 這些選項需要執行中的資料流才能觸發。 如需詳細資訊，請閱讀 [警報概觀](../../alerts.md) <ul><li>**來源資料流執行開始**：選取此警報以在資料流執行開始時收到通知。</li><li>**來源資料流執行成功**：選取此警報可在您的資料流結束且沒有任何錯誤時收到通知。</li><li>**來源資料流執行失敗**：選取此警報可在您的資料流執行結束時，收到任何錯誤的通知。</li></ul> |

完成後，選取 **[!UICONTROL 下一個]** 以繼續進行。

## 將欄位對應至XDM結構描述 {#mapping}

此 [!UICONTROL 對應] 步驟隨即顯示。 使用對應介面將來源資料對應到適當的結構描述欄位，然後再將資料擷取到Experience Platform，然後選取 **[!UICONTROL 下一個]**. 如需如何使用對應介面的詳細指南，請參閱 [資料準備UI指南](../../../../../data-prep/ui/mapping.md) 以取得詳細資訊。

![來源工作流程的對應介面。](../../../../images/tutorials/create/snowflake-streaming/mapping.png)

## 檢閱您的資料流 {#review}

資料流建立流程的最後一步是在執行資料流之前進行檢閱。 使用 **[!UICONTROL 檢閱]** 執行此步驟前，請先檢閱新資料流的詳細資訊。 詳細資料會分組到以下類別中：

* **連線**：顯示來源型別、所選來源檔案的相關路徑，以及該來源檔案中的欄數。
* **指派資料集並對映欄位**：顯示要將來源資料擷取到哪個資料集中，包括資料集所堅持的結構描述。

檢閱資料流後，選取「 」 **[!UICONTROL 完成]** 並留出一些時間建立資料流。

![來源工作流程的「檢閱」步驟。](../../../../images/tutorials/create/snowflake-streaming/review.png)

## 後續步驟

依照本教學課程，您已成功建立的串流資料流 [!DNL Snowflake] 資料。 如需其他資源，請閱讀以下檔案。

### 監視資料流

建立資料流後，您可以監視透過它擷取的資料，以檢視擷取率、成功和錯誤的資訊。 如需如何監視串流資料流的詳細資訊，請瀏覽上的教學課程 [在UI中監視串流資料流](../../monitor-streaming.md).

### 更新您的資料流

若要更新資料流排程、對應和一般資訊的設定，請造訪本教學課程： [在UI中更新來源資料流程](../../update-dataflows.md).

### 刪除您的資料流

您可以刪除不再需要的資料流，或是使用建立的資料流不正確。 **[!UICONTROL 刪除]** 函式位於 **[!UICONTROL 資料流]** 工作區。 如需如何刪除資料流的詳細資訊，請前往上的教學課程： [在UI中刪除資料流](../../delete.md).