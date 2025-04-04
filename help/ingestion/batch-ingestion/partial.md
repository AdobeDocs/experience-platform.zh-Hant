---
keywords: Experience Platform；首頁；熱門主題；批次擷取；批次擷取；部分擷取；部分擷取錯誤；擷取錯誤；部分批次擷取；部分批次擷取；部分；擷取；擷取；
solution: Experience Platform
title: 部分批次擷取概觀
description: 本檔案提供管理部分批次擷取的教學課程。
exl-id: 25a34da6-5b7c-4747-8ebd-52ba516b9dc3
source-git-commit: b48c24ac032cbf785a26a86b50a669d7fcae5d97
workflow-type: tm+mt
source-wordcount: '946'
ht-degree: 7%

---

# 部分批次擷取

部分批次擷取是擷取包含錯誤的資料的能力，上限為特定臨界值。 有了這項功能，使用者可以成功地將其所有正確的資料擷取到Adobe Experience Platform，同時將其所有不正確的資料單獨分批處理，以及關於其無效原因的詳細資訊。

本檔案提供管理部分批次擷取的教學課程。

## 快速入門

本教學課程需要您具備與部分批次擷取相關的各種Adobe Experience Platform服務的運作知識。 在開始本教學課程之前，請先檢閱下列服務的檔案：

- [批次擷取](./overview.md)： [!DNL Experience Platform]從資料檔案（例如CSV和Parquet）擷取及儲存資料的方法。
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md)： [!DNL Experience Platform]用來組織客戶體驗資料的標準化架構。

下列章節提供您需瞭解的其他資訊，才能成功呼叫[!DNL Experience Platform] API。

### 讀取範例 API 呼叫

本指南提供範例 API 呼叫，示範如何格式化您的請求。 這些包括路徑、必要的標頭和正確格式化的請求承載。 此外，也提供 API 回應中傳回的範例 JSON。 如需檔案中所使用範例API呼叫慣例的詳細資訊，請參閱[!DNL Experience Platform]疑難排解指南中[如何讀取範例API呼叫](../../landing/troubleshooting.md#how-do-i-format-an-api-request)一節。

### 收集所需標頭的值

若要呼叫[!DNL Experience Platform] API，您必須先完成[驗證教學課程](https://www.adobe.com/go/platform-api-authentication-en)。 完成驗證教學課程會提供所有 [!DNL Experience Platform] API 呼叫中每個必要標頭的值，如下所示：

- 授權：持有人`{ACCESS_TOKEN}`
- x-api-key： `{API_KEY}`
- x-gw-ims-org-id： `{ORG_ID}`

[!DNL Experience Platform]中的所有資源都與特定的虛擬沙箱隔離。 對[!DNL Experience Platform] API的所有請求都需要標頭，以指定將在其中執行作業的沙箱名稱：

- x-sandbox-name： `{SANDBOX_NAME}`

>[!NOTE]
>
>如需[!DNL Experience Platform]中沙箱的詳細資訊，請參閱[沙箱概觀檔案](../../sandboxes/home.md)。

## 在API中啟用部分批次擷取的批次 {#enable-api}

>[!NOTE]
>
>本節說明如何使用API為部分批次擷取啟用批次。 如需使用UI的說明，請閱讀[在UI](#enable-ui)步驟中啟用批次以進行部分批次擷取。

您可以建立已啟用部分擷取的新批次。

若要建立新批次，請依照[批次擷取開發人員指南](./api-overview.md)中的步驟操作。 到達&#x200B;**[!UICONTROL 建立批次]**&#x200B;步驟後，請在請求內文中新增下列欄位：

```json
{
    "enableErrorDiagnostics": true,
    "partialIngestionPercent": 5
}
```

| 屬性 | 說明 |
| -------- | ----------- |
| `enableErrorDiagnostics` | 允許[!DNL Experience Platform]產生批次詳細錯誤訊息的標幟。 |
| `partialIngestionPercent` | 整個批次失敗之前可接受的錯誤百分比。 因此，在此範例中，最多5%的批次可能是錯誤，然後才會失敗。 |


## 在UI中為部分批次擷取啟用批次 {#enable-ui}

>[!NOTE]
>
>本節說明如何使用UI為部分批次擷取啟用批次。 如果您已使用API為部分批次擷取啟用批次，則可以跳至下一節。

若要透過[!DNL Experience Platform] UI啟用部分擷取的批次，您可以透過來源連線建立新批次、在現有資料集中建立新批次，或透過&quot;[!UICONTROL 將CSV對應至XDM流程]&quot;建立新批次。

### 建立新的來源連線 {#new-source}

若要建立新的來源連線，請依照[來源概觀](../../sources/home.md)中列出的步驟操作。 到達&#x200B;**[!UICONTROL 資料流詳細資料]**&#x200B;步驟後，請記下&#x200B;**[!UICONTROL 部分擷取]**&#x200B;和&#x200B;**[!UICONTROL 錯誤診斷]**&#x200B;欄位。

![](../images/batch-ingestion/partial-ingestion/configure-batch.png)

**[!UICONTROL 部分擷取]**&#x200B;切換可讓您啟用或停用部分批次擷取。

**[!UICONTROL 錯誤診斷]**&#x200B;切換僅在&#x200B;**[!UICONTROL 部分擷取]**&#x200B;切換關閉時顯示。 此功能可讓[!DNL Experience Platform]產生有關您擷取批次的詳細錯誤訊息。 如果已開啟&#x200B;**[!UICONTROL 部分擷取]**&#x200B;切換，則會自動強制執行增強的錯誤診斷。

![](../images/batch-ingestion/partial-ingestion/configure-batch-partial-ingestion-focus.png)

**[!UICONTROL 錯誤臨界值]**&#x200B;可讓您在整個批次失敗之前設定可接受的錯誤百分比。 預設情況下，此值會設為5%。

### 使用現有的資料集 {#existing-dataset}

若要使用現有的資料集，請從選取資料集開始。 右側邊欄會填入資料集的相關資訊。

![](../images/batch-ingestion/partial-ingestion/monitor-dataset.png)

**[!UICONTROL 部分擷取]**&#x200B;切換可讓您啟用或停用部分批次擷取。

**[!UICONTROL 錯誤診斷]**&#x200B;切換僅在&#x200B;**[!UICONTROL 部分擷取]**&#x200B;切換關閉時顯示。 此功能可讓[!DNL Experience Platform]產生有關您擷取批次的詳細錯誤訊息。 如果已開啟&#x200B;**[!UICONTROL 部分擷取]**&#x200B;切換，則會自動強制執行增強的錯誤診斷。

![](../images/batch-ingestion/partial-ingestion/monitor-dataset-partial-ingestion-focus.png)

**[!UICONTROL 錯誤臨界值]**&#x200B;可讓您在整個批次失敗之前設定可接受的錯誤百分比。 預設情況下，此值會設為5%。

現在，您可以使用&#x200B;**新增資料**&#x200B;按鈕上傳資料，並將使用部分擷取來擷取資料。

### 使用&quot;[!UICONTROL 將CSV對應至XDM結構描述]&quot;流程 {#map-flow}

若要使用「[!UICONTROL 將CSV對應至XDM結構描述]」流程，請依照[將CSV檔案對應至教學課程](../tutorials/map-csv/overview.md)中列出的步驟操作。 完成&#x200B;**[!UICONTROL 新增資料]**&#x200B;步驟後，請記下&#x200B;**[!UICONTROL 部分擷取]**&#x200B;和&#x200B;**[!UICONTROL 錯誤診斷]**&#x200B;欄位。

![](../images/batch-ingestion/partial-ingestion/xdm-csv-workflow.png)

**[!UICONTROL 部分擷取]**&#x200B;切換可讓您啟用或停用部分批次擷取。

**[!UICONTROL 錯誤診斷]**&#x200B;切換僅在&#x200B;**[!UICONTROL 部分擷取]**&#x200B;切換關閉時顯示。 此功能可讓[!DNL Experience Platform]產生有關您擷取批次的詳細錯誤訊息。 如果已開啟&#x200B;**[!UICONTROL 部分擷取]**&#x200B;切換，則會自動強制執行增強的錯誤診斷。

![](../images/batch-ingestion/partial-ingestion/xdm-csv-workflow-partial-ingestion-focus.png)

**[!UICONTROL 錯誤臨界值]**&#x200B;可讓您在整個批次失敗之前設定可接受的錯誤百分比。 預設情況下，此值會設為5%。

## 後續步驟 {#next-steps}

本教學課程說明如何建立或修改資料集以啟用部分批次擷取。 如需批次擷取的詳細資訊，請參閱[批次擷取開發人員指南](./api-overview.md)。

如需有關監控部分擷取錯誤的資訊，請參閱[批次擷取錯誤診斷指南](../quality/error-diagnostics.md)。
