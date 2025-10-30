---
keywords: Experience Platform；首頁；熱門主題；批次擷取；批次擷取；部分擷取；部分擷取錯誤；擷取錯誤；部分批次擷取；部分批次擷取；部分；擷取；擷取；
solution: Experience Platform
title: 部分批次擷取概觀
description: 本檔案提供管理部分批次擷取的教學課程。
exl-id: 25a34da6-5b7c-4747-8ebd-52ba516b9dc3
source-git-commit: bc72f77b1b4a48126be9b49c5c663ff11e9054ea
workflow-type: tm+mt
source-wordcount: '1209'
ht-degree: 9%

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

本指南提供範例 API 呼叫，示範如何格式化您的請求。 這些包括路徑、必要的標頭和正確格式化的請求承載。 此外，也提供 API 回應中傳回的範例 JSON。 如需文件中用於範例 API 呼叫的慣例相關資訊，請參閱 [!DNL Experience Platform] 疑難排解指南中的[如何讀取範例 API 呼叫](../../landing/troubleshooting.md#how-do-i-format-an-api-request)一節。

### 收集所需標頭的值

為了對 [!DNL Experience Platform] API 進行呼叫，您必須先完成[驗證教學課程](https://www.adobe.com/go/platform-api-authentication-en)。完成驗證教學課程會提供所有 [!DNL Experience Platform] API 呼叫中每個必要標頭的值，如下所示：

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

若要建立新批次，請依照[批次擷取開發人員指南](./api-overview.md)中的步驟操作。 到達&#x200B;**[!UICONTROL Create batch]**&#x200B;步驟後，在請求內文中新增下列欄位：

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

若要透過[!DNL Experience Platform] UI啟用部分擷取的批次，您可以透過來源連線建立新批次、在現有資料集中建立新批次，或透過&quot;[!UICONTROL Map CSV to XDM flow]&quot;建立新批次。

### 建立新的來源連線 {#new-source}

若要建立新的來源連線，請依照[來源概觀](../../sources/home.md)中列出的步驟操作。 到達&#x200B;**[!UICONTROL Dataflow detail]**&#x200B;步驟後，記下&#x200B;**[!UICONTROL Partial ingestion]**&#x200B;和&#x200B;**[!UICONTROL Error diagnostics]**&#x200B;欄位。

![](../images/batch-ingestion/partial-ingestion/configure-batch.png)

**[!UICONTROL Partial ingestion]**&#x200B;切換可讓您啟用或停用部分批次擷取的使用。

**[!UICONTROL Error diagnostics]**&#x200B;切換僅在&#x200B;**[!UICONTROL Partial ingestion]**&#x200B;切換關閉時顯示。 此功能可讓[!DNL Experience Platform]產生有關您擷取批次的詳細錯誤訊息。 如果已開啟&#x200B;**[!UICONTROL Partial ingestion]**&#x200B;切換，則會自動強制增強錯誤診斷。

![](../images/batch-ingestion/partial-ingestion/configure-batch-partial-ingestion-focus.png)

**[!UICONTROL Error threshold]**&#x200B;可讓您在整個批次失敗之前設定可接受的錯誤百分比。 預設情況下，此值會設為5%。

### 使用現有的資料集 {#existing-dataset}

若要使用現有的資料集，請從選取資料集開始。 右側邊欄會填入資料集的相關資訊。

![](../images/batch-ingestion/partial-ingestion/monitor-dataset.png)

**[!UICONTROL Partial ingestion]**&#x200B;切換可讓您啟用或停用部分批次擷取的使用。

**[!UICONTROL Error diagnostics]**&#x200B;切換僅在&#x200B;**[!UICONTROL Partial ingestion]**&#x200B;切換關閉時顯示。 此功能可讓[!DNL Experience Platform]產生有關您擷取批次的詳細錯誤訊息。 如果已開啟&#x200B;**[!UICONTROL Partial ingestion]**&#x200B;切換，則會自動強制增強錯誤診斷。

![](../images/batch-ingestion/partial-ingestion/monitor-dataset-partial-ingestion-focus.png)

**[!UICONTROL Error threshold]**&#x200B;可讓您在整個批次失敗之前設定可接受的錯誤百分比。 預設情況下，此值會設為5%。

現在，您可以使用&#x200B;**新增資料**&#x200B;按鈕上傳資料，並將使用部分擷取來擷取資料。

### 使用&quot;[!UICONTROL Map CSV to XDM schema]&quot;流程 {#map-flow}

若要使用&quot;[!UICONTROL Map CSV to XDM schema]&quot;流程，請依照[對應CSV檔案教學課程](../tutorials/map-csv/overview.md)中列出的步驟操作。 到達&#x200B;**[!UICONTROL Add data]**&#x200B;步驟後，記下&#x200B;**[!UICONTROL Partial ingestion]**&#x200B;和&#x200B;**[!UICONTROL Error diagnostics]**&#x200B;欄位。

![](../images/batch-ingestion/partial-ingestion/xdm-csv-workflow.png)

**[!UICONTROL Partial ingestion]**&#x200B;切換可讓您啟用或停用部分批次擷取的使用。

**[!UICONTROL Error diagnostics]**&#x200B;切換僅在&#x200B;**[!UICONTROL Partial ingestion]**&#x200B;切換關閉時顯示。 此功能可讓[!DNL Experience Platform]產生有關您擷取批次的詳細錯誤訊息。 如果已開啟&#x200B;**[!UICONTROL Partial ingestion]**&#x200B;切換，則會自動強制增強錯誤診斷。

![](../images/batch-ingestion/partial-ingestion/xdm-csv-workflow-partial-ingestion-focus.png)

**[!UICONTROL Error threshold]**&#x200B;可讓您在整個批次失敗之前設定可接受的錯誤百分比。 預設情況下，此值會設為5%。

## 啟用現有資料流的部分擷取和錯誤診斷

如果Experience Platform中的資料流是在未啟用部分擷取或錯誤診斷的情況下建立的，您仍然可以啟用這些功能而不重新建立資料流。 透過啟用部分擷取和強大的錯誤診斷，您可以大幅增強資料擷取工作流程的可靠性並簡化疑難排解。 請閱讀以下章節，瞭解如何使用[!DNL Flow Service] API為現有資料流啟用部分擷取和錯誤診斷。

依預設，資料流可能不會啟用部分擷取或錯誤診斷。 這些功能有助於識別和隔離資料擷取期間的問題。 使用[!DNL Flow Service] API，您可以擷取目前的資料流組態，並使用PATCH要求套用必要的變更。

請依照下列步驟，為現有的資料流啟用部分擷取和錯誤診斷。

### 擷取流程詳細資料

若要擷取您的資料流設定，請對`/flows/{FLOW_ID}`端點提出GET要求，並提供資料流的ID。 如需擷取資料流詳細資料的詳細資訊，請參閱[使用 [!DNL Flow Service] API](../../sources/tutorials/api/update-dataflows.md)更新資料流指南。

請確定儲存回應中傳回的`etag`欄位值。 這對更新請求是必要的，以確保版本一致性。

### 更新流程設定

接下來，向`/flows/`端點發出PATCH請求，並提供您要為其啟用部分擷取和錯誤診斷的資料流ID。

>[!IMPORTANT]
>
>- 使用If-Match索引鍵將先前儲存的`etag`值加入請求標頭中。
>- 您可以修改`partialIngestionPercent`值以符合您的特定需求。

**API格式**

```http
PATCH /flows/{FLOW_ID}
```

**要求**

```shell
curl -X PATCH \
    'https://platform.adobe.io/data/foundation/flowservice/flows/2edc08ac-4df5-4fe6-936f-81a19ce92f5c' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
    -H 'If-Match: "1a0037e4-0000-0200-0000-602e06f60000"' \
    -d '[
        {
            "op": "add",
            "path": "/options",
            "value": {
                "partialIngestionPercent": "10"
            }
        },
        {
            "op": "add",
            "path": "/options/errorDiagnosticsEnabled",
            "value": true
        }
    ]'
```

**回應**

成功的回應會傳回資料流的`id`和更新的`etag`。

```json
{
    "id": "2edc08ac-4df5-4fe6-936f-81a19ce92f5c",
    "etag": "\"2c000802-0000-0200-0000-613976440000\""
}
```

### 驗證更新

PATCH完成後，請提出GET請求並擷取您的資料流，以確認變更已成功完成。

**API格式**

```http
GET /flows/{FLOW_ID}
```

**要求**

以下請求會擷取有關您的流程ID的更新資訊。

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/flows/2edc08ac-4df5-4fe6-936f-81a19ce92f5c' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應會傳回您的資料流詳細資料，確認已在`options`區段中啟用部分擷取和錯誤診斷。

```json
"options": {
    "partialIngestionPercent": 10,
    "errorDiagnosticsEnabled": true
}
```

## 後續步驟 {#next-steps}

本教學課程說明如何建立或修改資料集以啟用部分批次擷取。 如需批次擷取的詳細資訊，請參閱[批次擷取開發人員指南](./api-overview.md)。

如需有關監控部分擷取錯誤的資訊，請參閱[批次擷取錯誤診斷指南](../quality/error-diagnostics.md)。
