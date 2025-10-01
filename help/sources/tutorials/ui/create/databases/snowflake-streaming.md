---
title: 使用UI將資料從Snowflake資料庫串流到Experience Platform
description: 瞭解如何將資料從Snwoflake資料庫串流至Experience Platform
exl-id: 49d488f1-90d8-452a-9f3e-02afdcc79b09
source-git-commit: 0d646136da2c508fe7ce99a15787ee15c5921a6c
workflow-type: tm+mt
source-wordcount: '1451'
ht-degree: 3%

---

# 使用UI將資料從您的[!DNL Snowflake]資料庫串流到Experience Platform

閱讀本指南，瞭解如何使用UI中的來源工作區將資料從您的[!DNL Snowflake]資料庫串流到Experience Platform。

## 快速入門

本教學課程需要您實際瞭解下列Experience Platform元件：

* [[!DNL Experience Data Model (XDM)] 系統](../../../../../xdm/home.md)： [!DNL Experience Platform]用來組織客戶體驗資料的標準化架構。
   * [結構描述組合的基本概念](../../../../../xdm/schema/composition.md)：瞭解XDM結構描述的基本建置區塊，包括結構描述組合中的關鍵原則和最佳實務。
   * [結構描述編輯器教學課程](../../../../../xdm/tutorials/create-schema-ui.md)：瞭解如何使用結構描述編輯器使用者介面建立自訂結構描述。
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md)：根據來自多個來源的彙總資料，提供統一的即時消費者設定檔。

### Authentication

閱讀[串流資料 [!DNL Snowflake] 的](../../../../connectors/databases/snowflake-streaming.md)必要條件設定指南，瞭解從[!DNL Snowflake]擷取串流資料至Experience Platform前，您需要完成的步驟相關資訊。

## 使用[!DNL Snowflake Streaming]來源將[!DNL Snowflake]資料串流到Experience Platform

在Experience Platform UI中，從左側導覽選取&#x200B;**[!UICONTROL 來源]**&#x200B;以存取[!UICONTROL 來源]工作區。 您可以從熒幕左側的目錄中選取適當的類別。 或者，您可以使用搜尋選項來尋找您要使用的特定來源。

在&#x200B;*資料庫*&#x200B;類別下，選取&#x200B;**[!DNL Snowflake Streaming]**，然後選取&#x200B;**[!UICONTROL 設定]**。

>[!TIP]
>
>來源目錄中沒有已驗證帳戶的來源會顯示&#x200B;**[!UICONTROL 設定]**&#x200B;選項。 一旦驗證帳戶存在，此選項就會變更為&#x200B;**[!UICONTROL 新增資料]**。

![Experience Platform UI中的來源目錄，已選取Snowflake串流來源卡。](../../../../images/tutorials/create/snowflake-streaming/catalog.png)

**[!UICONTROL 連線Snowflake串流帳戶]**&#x200B;頁面隨即顯示。 您可以在此頁面使用新的或現有的證明資料。

### 建立新帳戶

若要建立新帳戶，請選取&#x200B;**[!UICONTROL 新帳戶]**，並為您的帳戶提供名稱和選擇性說明。

![來源工作流程的新帳戶建立介面。](../../../../images/tutorials/create/snowflake-streaming/new.png)

>[!BEGINTABS]

>[!TAB 基本驗證]

若要使用[!UICONTROL 基本驗證]，請選取&#x200B;**[!UICONTROL Snowflake的基本驗證]**，並提供您[!DNL Snowflake]帳戶的認證。 完成後，請選取&#x200B;**[!UICONTROL 連線到來源]**，並等待一段時間以建立連線。

閱讀[!DNL Snowflake Streaming]概觀，以取得有關[收集所需認證](../../../../connectors/databases/snowflake-streaming.md#gather-required-credentials)的詳細資訊。

![來源工作流程中的新帳戶介面，已選取基本驗證。](../../../../images/tutorials/create/snowflake-streaming/basic-auth.png)

>[!TAB KeyPair驗證]

若要使用[!UICONTROL KeyPair驗證]，請選取Snowflake的&#x200B;**[!UICONTROL KeyPair驗證]**，並提供您[!DNL Snowflake]帳戶的認證。 完成後，請選取&#x200B;**[!UICONTROL 連線到來源]**，並等待一段時間以建立連線。

閱讀[!DNL Snowflake Streaming]概觀，以取得有關[收集所需認證](../../../../connectors/databases/snowflake-streaming.md#gather-required-credentials)的詳細資訊。

![來源工作流程中的新帳戶介面，已選取金鑰組驗證](../../../../images/tutorials/create/snowflake-streaming/key-pair.png)

>[!ENDTABS]

若要使用現有帳戶，請選擇&#x200B;**[!UICONTROL 現有帳戶]**，從清單中選取您的帳戶，然後選取&#x200B;**[!UICONTROL 下一步]**。

## 選取資料 {#select-data}

>[!IMPORTANT]
>
>* 時間戳記欄必須存在於您的來源表格中，才能建立串流資料流。 Experience Platform需要時間戳記才能知道何時會擷取資料，以及何時會串流增量資料。 您可以回溯性地為現有連線新增時間戳記欄，並建立新的資料流。
>
>* 確保範例來源資料檔中的資料欄位大小寫符合[!DNL Snowflake]對於識別碼大小寫解決的指引。 如需詳細資訊，請閱讀識別碼大小寫[[!DNL Snowflake] 上的](https://docs.snowflake.com/en/sql-reference/identifiers-syntax#label-identifier-casing)檔案。

[!UICONTROL 選取資料]步驟隨即顯示。 在此步驟中，您必須選取要匯入Experience Platform的資料、設定時間戳記和時區，並提供用於擷取原始資料的範例來源資料檔案。

使用畫面左側的資料庫目錄，並選取您要匯入至Experience Platform的表格。

接著，選取表格的時間戳記欄型別。 您可以在兩種時間戳記資料行型別之間選取： `TIMESTAMP_NTZ`或`TIMESTAMP_LTZ`。 如果您選取`TIMESTAMP_NTZ`的欄型別，則必須也提供時區。 您的欄應該有非null的限制。 如需詳細資訊，請閱讀有關[限制和常見問題](../../../../connectors/databases/snowflake-streaming.md#limitations-and-frequently-asked-questions)的章節。

您也可以在此步驟中設定回填設定。 回填會決定最初要擷取的資料。 如果已啟用回填，則會在第一次排程擷取期間擷取指定路徑中的所有目前檔案。 如果沒有，則只會擷取在第一次內嵌執行與開始時間之間載入的檔案。 將不會擷取在開始時間之前載入的檔案。

選取&#x200B;**[!UICONTROL 回填]**&#x200B;切換以啟用回填。

![時間戳記、時區和回填設定步驟。](../../../../images/tutorials/create/snowflake-streaming/timezone.png)

最後，選取&#x200B;**[!UICONTROL 選擇檔案]**&#x200B;以上傳範例來源資料以協助建立對應集，該對應集將在後續步驟中用於將原始資料對應至Experience Data Model (XDM)。

完成後，選取&#x200B;**[!UICONTROL 下一步]**&#x200B;以繼續。

![來源範例資料的預覽。](../../../../images/tutorials/create/snowflake-streaming/preview.png)

## 提供資料集和資料流詳細資料 {#provide-dataset-and-dataflow-details}

接下來，您必須提供有關資料集和資料流的資訊。

### 資料集詳細資料 {#dataset-details}

資料集是資料集合的儲存和管理結構，通常是包含方案 (欄) 和欄位 (列) 的表格。 成功內嵌至Experience Platform的資料會以資料集的形式保留在資料湖中。 在此步驟中，您可以建立新資料集或使用現有資料集。

如果您有現有的資料集，請選取「**[!UICONTROL 現有的資料集]**」，然後使用「**[!UICONTROL 進階搜尋]**」選項來檢視貴組織中所有資料集的視窗，包括其個別詳細資訊，例如是否啟用這些資料集以擷取至Real-Time Customer Profile。

![現有的資料集選取介面。](../../../../images/tutorials/create/snowflake-streaming/dataset.png)

若要使用新的資料集，請選取&#x200B;**[!UICONTROL 新資料集]**，然後為您的資料集提供名稱和選擇性描述。 您也必須選取您的資料集所要遵守的Experience Data Model (XDM)結構。

| 新資料集詳細資料 | 說明 |
| --- | --- |
| 輸出資料集名稱 | 新資料集的名稱。 |
| 說明 | （選用）新資料集的簡短總覽。 |
| 結構描述 | 貴組織中現有的結構描述下拉式清單。 您也可以在來源設定程式之前建立自己的結構描述。 如需詳細資訊，請閱讀[在UI](../../../../../xdm/tutorials/create-schema-ui.md)中建立XDM結構描述的指南。 |

### 資料流詳細資料 {#dataflow-details}

設定資料集後，您必須提供資料流的詳細資訊，包括名稱、選用的說明和警報設定。

![資料流詳細資料設定步驟。](../../../../images/tutorials/create/snowflake-streaming/dataflow-detail.png)

| 資料流設定 | 說明 |
| --- | --- |
| 資料流名稱 | 資料流的名稱。  依預設，這將使用正在匯入的檔案名稱。 |
| 說明 | （選用）資料流的簡短說明。 |
| 警報 | Experience Platform可產生使用者可訂閱的事件型警報。 這些選項需要執行中的資料流才能觸發。 如需詳細資訊，請閱讀[警示概述](../../alerts.md) <ul><li>**來源資料流執行開始**：選取此警示以在您的資料流執行開始時收到通知。</li><li>**來源資料流執行成功**：選取此警示以在您的資料流結束且沒有任何錯誤時接收通知。</li><li>**來源資料流執行失敗**：選取此警示以在您的資料流執行結束時發生任何錯誤時接收通知。</li></ul> |

完成後，選取&#x200B;**[!UICONTROL 下一步]**&#x200B;以繼續。

## 將欄位對應至XDM結構描述 {#mapping}

[!UICONTROL 對應]步驟出現。 使用對應介面將您的來源資料對應到適當的結構描述欄位，然後再將該資料擷取到Experience Platform，然後選取&#x200B;**[!UICONTROL 下一步]**。 如需如何使用對應介面的詳細指南，請閱讀[資料準備UI指南](../../../../../data-prep/ui/mapping.md)以取得詳細資訊。

![來源工作流程的對應介面。](../../../../images/tutorials/create/snowflake-streaming/mapping.png)

## 檢閱您的資料流 {#review}

資料流建立流程的最後一步是在執行資料流之前進行檢閱。 使用&#x200B;**[!UICONTROL 檢閱]**&#x200B;步驟，在執行新資料流之前先檢閱其詳細資料。 詳細資料會分組到以下類別中：

* **連線**：顯示來源型別、所選來源檔案的相關路徑，以及該來源檔案中的欄數。
* **指派資料集與對應欄位**：顯示要將來源資料擷取到哪個資料集，包括資料集所堅持的結構描述。

檢閱您的資料流後，請選取&#x200B;**[!UICONTROL 完成]**，並等待一些時間來建立資料流。

![來源工作流程的稽核步驟。](../../../../images/tutorials/create/snowflake-streaming/review.png)

## 後續步驟

依照此教學課程，您已成功建立[!DNL Snowflake]資料的串流資料流。 如需其他資源，請閱讀以下檔案。

### 監視資料流

建立資料流後，您可以監視透過它擷取的資料，以檢視擷取率、成功和錯誤的資訊。 如需有關如何監視串流資料流的詳細資訊，請瀏覽有關[在UI中監視串流資料流的教學課程](../../monitor-streaming.md)。

### 更新您的資料流

若要更新資料流排程、對應和一般資訊的設定，請瀏覽有關[在UI中更新來源資料流的教學課程](../../update-dataflows.md)。

### 刪除您的資料流

您可以刪除不再需要的資料流，或使用&#x200B;**[!UICONTROL 資料流]**&#x200B;工作區中可用的&#x200B;**[!UICONTROL 刪除]**&#x200B;功能建立錯誤的資料流。 如需有關如何刪除資料流的詳細資訊，請瀏覽教學課程，瞭解如何在UI[中刪除資料流](../../delete.md)。
