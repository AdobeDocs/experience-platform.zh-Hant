---
title: 探索、疑難排解及驗證SQL的批次擷取
description: 瞭解如何瞭解及管理Adobe Experience Platform中的資料擷取流程。 本檔案包含如何驗證批次和查詢擷取的資料。
exl-id: 8f49680c-42ec-488e-8586-50182d50e900
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1170'
ht-degree: 0%

---

# 探索、疑難排解及驗證SQL的批次擷取

本檔案說明如何使用SQL驗證及驗證所擷取批次中的記錄。 本檔案會教導您：

- 存取資料集批次中繼資料
- 透過查詢批次進行疑難排解並確保資料完整性

>[!NOTE]
>
>本指南中的部分熒幕擷取畫面取自[!DNL DBVisualizer]。 若要瞭解如何[連線查詢服務與DBVisualizer](../clients/dbvisulaizer.md)或其他[第三方BI工具](../clients/overview.md)，請參閱連結的檔案。

## 先決條件

為了協助您瞭解本檔案中討論的概念，您應該瞭解下列主題：

- **資料擷取**：請參閱[資料擷取總覽](../../ingestion/home.md)，瞭解資料如何擷取到Experience Platform的基礎知識，包括所涉及的各種方法和程式。
- **批次擷取**：請參閱[批次擷取API總覽](../../ingestion/batch-ingestion/overview.md)，瞭解批次擷取的基本概念。 具體來說，什麼是「批次」，以及它在Experience Platform資料擷取流程中的運作方式。
- **資料集中的系統中繼資料**：請參閱[目錄服務總覽](../../catalog/home.md)，瞭解如何使用系統中繼資料欄位來追蹤和查詢擷取的資料。
- **Experience Data Model (XDM)**：請參閱[結構描述UI總覽](../../xdm/ui/overview.md)和結構描述組合的基本概念[&#128279;](../../xdm/schema/composition.md)，以瞭解XDM結構描述以及它們如何呈現和驗證擷取到Experience Platform的資料結構和格式。

## 存取資料集批次中繼資料 {#access-dataset-batch-metadata}

若要確保查詢結果中包含系統資料行（中繼資料資料行），請在查詢編輯器中使用SQL命令`set drop_system_columns=false`。 這會設定SQL查詢工作階段的行為。 如果您啟動新的工作階段，則必須重複此輸入。

接下來，若要檢視資料集的系統欄位，請執行SELECT all陳述式以顯示資料集的結果，例如`select * from movie_data`。 結果在右側`_acp_system_metadata`和`_ACP_BATCHID`包含兩個新欄。 中繼資料資料行`_acp_system_metadata`和`_ACP_BATCHID`可協助識別所擷取資料的邏輯和實體資料分割。

![顯示並反白顯示movie_data表格及其中繼資料資料欄的DBVisualizer UI。](../images/use-cases/movie_data-table-with-metadata-columns.png)

將資料內嵌至Experience Platform時，會根據傳入的資料為其指派邏輯分割區。 此邏輯分割由`_acp_system_metadata.sourceBatchId`表示。 此ID可協助您在處理和儲存資料批次之前，依邏輯將其分組和識別。

在處理資料並擷取到資料湖後，會指派給它以`_ACP_BATCHID`表示的實體分割。 此ID反映所擷取資料所在的資料湖中的實際儲存分割區。

### 使用SQL來瞭解邏輯和實體分割區 {#understand-partitions}

若要瞭解資料在擷取後如何分組和分配，請使用下列查詢來計算每個邏輯分割區(`_acp_system_metadata.sourceBatchId`)的不同實體分割區(`_ACP_BATCHID`)數目。

```SQL
SELECT  _acp_system_metadata, COUNT(DISTINCT _ACP_BATCHID) FROM movie_data
GROUP BY _acp_system_metadata
```

此查詢的結果如下圖所示。

![查詢結果會顯示每個邏輯分割區的不同實體分割區數目。](../images/use-cases/logical-and-physical-partition-count.png)

這些結果顯示輸入批次的數量並不一定與輸出批次的數量相符，因為系統決定了批次和在Data Lake中儲存資料的最有效方式。

在此範例中，假設您已將CSV檔案擷取至Experience Platform，並建立名為`drug_checkout_data`的資料集。

`drug_checkout_data`檔案是包含35,000筆記錄的深度巢狀集合。 使用SQL陳述式`SELECT * FROM drug_orders;`來預覽JSON型`drug_orders`資料集中的第一組記錄。

下圖顯示檔案及其記錄的預覽。

![JSON型drug_orders資料集中的第一組記錄預覽。](../images/use-cases/drug-orders-preview.png)

### 使用SQL產生批次擷取程式的深入分析 {#sql-insights-on-batch-ingestion}

使用下列SQL陳述式，深入分析資料擷取程式如何將輸入記錄分組並處理為批次。

```sql
SELECT _acp_system_metadata,
       Count(DISTINCT _acp_batchid) AS numoutputbatches,
       Count(_acp_batchid)          AS recordcount
FROM   drug_orders
GROUP  BY _acp_system_metadata 
```

查詢結果如下圖所示。

![顯示一次使用記錄計數控制輸入批次之分配情況的表格。](../images/use-cases/distribution-of-input-batches.png)

此結果說明資料擷取程式的效率和行為。 雖然已建立三個輸入批次(每個都包含2000、24000和9000筆記錄)，但合併記錄並去除重複資料時，只剩下一個唯一批次。

>[!NOTE]
>
>資料集中可見的所有記錄都是已成功擷取的記錄。 成功的批次擷取並不意味著從來源輸入傳送的所有記錄都存在。 您必須檢查資料擷取失敗，以尋找未擷取的批次/記錄。

## 使用SQL驗證批次 {#validate-a-batch-with-SQL}

接下來，驗證並驗證已使用SQL擷取到資料集中的記錄。

>[!TIP]
>
>若要擷取與該批次ID相關聯的批次ID和查詢記錄，您必須先在Experience Platform中建立批次。 如果您想自行測試此程式，可將CSV資料內嵌至Experience Platform。 閱讀如何使用AI產生的建議[&#128279;](../../ingestion/tutorials/map-csv/recommendations.md)將CSV檔案對應到現有XDM結構描述的指南。

擷取批次後，您必須針對您擷取資料的資料集，導覽至[!UICONTROL 資料集活動標籤]。

在Experience Platform UI中，選取左側導覽中的&#x200B;**[!UICONTROL 資料集]**&#x200B;以開啟[!UICONTROL 資料集]儀表板。 接下來，從[!UICONTROL 瀏覽]索引標籤中選取資料集名稱，以存取[!UICONTROL 資料集活動]畫面。

![左側導覽中反白顯示資料集的Experience Platform UI資料集儀表板。](../images/use-cases/datasets-workspace.png)

[!UICONTROL 資料集活動]檢視即會顯示。 此檢視包含您所選資料集的詳細資料。 其中包含以表格格式顯示的任何擷取批次。

從可用批次清單中選取批次，然後從右側的詳細資訊面板複製[!UICONTROL 批次ID]。

![Experience Platform資料集UI會顯示反白顯示批次ID的內嵌記錄。](../images/use-cases/batch-id.png)

接下來，使用以下查詢來擷取該批次中包含在資料集中的所有記錄：

```sql
SELECT * FROM movie_data
WHERE  _acp_batchid='01H00BKCTCADYRFACAAKJTVQ8P' 
LIMIT 1;
```

`_ACP_BATCHID`關鍵字用於篩選[!UICONTROL 批次ID]。

>[!TIP]
>
>如果您想要限制顯示的列數，則`LIMIT`子句會很有幫助，但更需要篩選條件。

當您在查詢編輯器中執行此查詢時，結果將被截斷為100列。 查詢編輯器專為快速預覽和調查而設計。 若要擷取最多50,000列，您可以使用第三方工具，例如DBVisualizer或DBeaver。

## 後續步驟 {#next-steps}

閱讀本檔案後，您已瞭解在資料擷取程式中，驗證及驗證擷取批次中記錄的基本知識。 您也深入瞭解了存取資料集批次中繼資料、瞭解邏輯和實體分割區，以及使用SQL命令查詢特定批次。 這些知識可協助您確保資料完整性，並最佳化Experience Platform上的資料儲存空間。

接下來，您應該練習資料擷取，以套用所學的概念。 使用提供的範例檔案或您自己的資料將範例資料集擷取到Experience Platform。 如果您尚未這麼做，請閱讀教學課程，瞭解如何[將資料內嵌至Adobe Experience Platform](../../ingestion/tutorials/ingest-batch-data.md)。

或者，您可以學習如何[使用各種案頭使用者端應用程式連線及驗證查詢服務](../clients/overview.md)，以增強您的資料分析功能。
