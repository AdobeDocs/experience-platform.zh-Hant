---
keywords: Experience Platform；首頁；熱門主題；監控資料流；流程服務api；流程服務
solution: Experience Platform
title: 使用流量服務API監控資料流
type: Tutorial
description: 本教學課程涵蓋使用流程服務API監控流程執行資料的完整性、錯誤和量度的步驟。
exl-id: c4b2db97-eba4-460d-8c00-c76c666ed70e
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '712'
ht-degree: 8%

---

# 使用流量服務API監控資料流

Adobe Experience Platform允許從外部來源擷取資料，同時讓您能夠使用[!DNL Experience Platform]服務來建構、加標籤及增強傳入資料。 您可以從多種來源(例如Adobe應用程式、雲端儲存、資料庫和許多其他來源)內嵌資料。 此外，Experience Platform還允許向外部合作夥伴啟用資料。

[!DNL Flow Service]用於收集及集中來自Adobe Experience Platform內各種不同來源的客戶資料。 此服務提供使用者介面和RESTful API，所有支援的來源和目的地都可以從中連線。

本教學課程涵蓋使用[[!DNL Flow Service API]](https://www.adobe.io/experience-platform-apis/references/flow-service/)監控資料流程執行資料的完整性、錯誤和量度的步驟。

## 快速入門

本教學課程要求您具備有效資料流的ID值。 如果您沒有有效的資料流ID，請從[來源概觀](../../sources/home.md)或[目的地概觀](../../destinations/catalog/overview.md)中選取您選擇的聯結器，並依照在嘗試本教學課程之前概述的步驟進行。

本教學課程也要求您實際瞭解下列Adobe Experience Platform元件：

- [目的地](../../destinations/home.md)：目的地是預先建置的與常用應用程式的整合，可讓您順暢地從Experience Platform啟用資料，用於跨管道行銷活動、電子郵件行銷活動、目標定位廣告和許多其他使用案例。
- [來源](../../sources/home.md)： [!DNL Experience Platform]允許從各種來源擷取資料，同時讓您能夠使用[!DNL Experience Platform]服務來建構、加標籤以及增強傳入的資料。
- [沙箱](../../sandboxes/home.md)： [!DNL Experience Platform]提供可將單一[!DNL Experience Platform]執行個體分割成個別虛擬環境的虛擬沙箱，以利開發及改進數位體驗應用程式。

下列章節提供您需瞭解的其他資訊，才能使用[!DNL Flow Service] API成功監視流量執行。

### 讀取範例 API 呼叫

本教學課程提供範例API呼叫，示範如何格式化您的請求。 這些包括路徑、必要的標頭和正確格式化的請求承載。 此外，也提供 API 回應中傳回的範例 JSON。 如需檔案中所使用範例API呼叫慣例的詳細資訊，請參閱[!DNL Experience Platform]疑難排解指南中[如何讀取範例API呼叫](../../landing/troubleshooting.md#how-do-i-format-an-api-request)一節。

### 收集所需標頭的值

若要呼叫[!DNL Experience Platform] API，您必須先完成[驗證教學課程](https://www.adobe.com/go/platform-api-authentication-en)。 完成驗證教學課程會提供所有 [!DNL Experience Platform] API 呼叫中每個必要標頭的值，如下所示：

- `Authorization: Bearer {ACCESS_TOKEN}`
- `x-api-key: {API_KEY}`
- `x-gw-ims-org-id: {ORG_ID}`

[!DNL Experience Platform]中的所有資源（包括屬於[!DNL Flow Service]的資源）都與特定的虛擬沙箱隔離。 對[!DNL Experience Platform] API的所有請求都需要標頭，以指定將在其中執行作業的沙箱名稱：

- `x-sandbox-name: {SANDBOX_NAME}`

包含裝載(POST、PUT、PATCH)的所有請求都需要額外的媒體型別標頭：

- `Content-Type: application/json`

## 監視流程執行

建立資料流後，請對[!DNL Flow Service] API執行GET請求。

**API格式**

```http
GET /runs?property=flowId=={FLOW_ID}
```

| 參數 | 說明 |
| --------- | ----------- |
| `{FLOW_ID}` | 您要監視之資料流的唯一`id`值。 |

**要求**

以下請求會擷取現有資料流的規格。

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/runs?property=flowId==c9cef9cb-c934-4467-8ef9-cbc934546741' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應會傳回有關您的資料流執行的詳細資料，包括其建立日期、來源和目標連線以及資料流執行的唯一識別碼(`id`)的相關資訊。

```json
{
    "items": [
        {
            "id": "65b7cfcc-6b2e-47c8-8194-13005b792752",
            "createdAt": 1607520228894,
            "updatedAt": 1607520276948,
            "createdBy": "{CREATED_BY}",
            "updatedBy": "{UPDATED_BY}",
            "createdClient": "{CREATED_CLIENT}",
            "updatedClient": "{UPDATED_CLIENT}",
            "sandboxId": "{SANDBOX_ID}",
            "sandboxName": "prod",
            "imsOrgId": "{ORG_ID}",
            "flowId": "f00c8762-df2f-432b-a7d7-38999fef5e8e",
            "etag": "\"560266dc-0000-0200-0000-5fd0d0140000\"",
            "metrics": {
                "durationSummary": {
                    "startedAtUTC": 1607520205922,
                    "completedAtUTC": 1607520262413
                },
                "sizeSummary": {
                    "inputBytes": 87885,
                    "outputBytes": 56730
                },
                "recordSummary": {
                    "inputRecordCount": 26758,
                    "outputRecordCount": 26758,
                    "failedRecordCount": 0
                },
                "fileSummary": {
                    "inputFileCount": 11,
                    "outputFileCount": 11,
                    "activityRefs": [
                        "37b34f84-1ada-11eb-adc1-0242ac120002"
                    ]
                },
                "statusSummary": {
                    "status": "success"
                }
            },
            "activities": [
                {
                    "id": "4f008a00-3a04-11eb-adc1-0242ac120002",
                    "name": "Copy Activity",
                    "updatedAtUTC": 0,
                    "durationSummary": {
                        "startedAtUTC": 1607520205922,
                        "completedAtUTC": 1607520236968
                    },
                    "sizeSummary": {
                        "inputBytes": 87885,
                        "outputBytes": 87885
                    },
                    "recordSummary": {
                        "inputRecordCount": 26758,
                        "outputRecordCount": 26758
                    },
                    "fileSummary": {
                        "inputFileCount": 11,
                        "outputFileCount": 11
                    },
                    "statusSummary": {
                        "status": "success"
                    }
                },
                {
                    "id": "37b34f84-1ada-11eb-adc1-0242ac120002",
                    "name": "Promotion Activity",
                    "updatedAtUTC": 0,
                    "durationSummary": {
                        "startedAtUTC": 1607520244985,
                        "completedAtUTC": 1607520262413
                    },
                    "sizeSummary": {
                        "inputBytes": 26758,
                        "outputBytes": 56730
                    },
                    "recordSummary": {
                        "inputRecordCount": 26758,
                        "outputRecordCount": 26758,
                        "failedRecordCount": 0
                    },
                    "fileSummary": {
                        "inputFileCount": 11,
                        "outputFileCount": 2,
                        "extensions": {
                            "manifest": {
                                "fileInfo": "https://platform.adobe.io/data/foundation/export/batches/01ES3TRN69E9W2DZ770XCGYAH1/meta?path=input_files",
                                "pathPrefix": "bucket1/csv_test/"
                            }
                        }
                    },
                    "statusSummary": {
                        "status": "success"
                    }
                }
            ]
        }
    ]
}
```

| 屬性 | 說明 |
| -------- | ----------- |
| `items` | 包含與您特定流程執行相關聯之中繼資料的單一裝載。 |
| `metrics` | 資料流執行的資料特性。 |
| `activities` | 顯示資料的轉換方式。 |
| `durationSummary` | 流程執行的開始和結束時間。 |
| `sizeSummary` | 資料量（位元組）。 |
| `recordSummary` | 資料的記錄計數。 |
| `fileSummary` | 資料的檔案計數。 |
| `fileSummary.extensions` | 包含活動的特定資訊。 例如，`manifest`只是「促銷活動」的一部分，因此包含在`extensions`物件中。 |
| `statusSummary` | 顯示流程執行是成功還是失敗。 |

## 後續步驟

依照本教學課程，您已使用[!DNL Flow Service] API擷取資料流上的量度和錯誤資訊。 您現在可以繼續根據您的擷取排程監視資料流，以追蹤其狀態和擷取率。 如需有關如何監視來源資料流的資訊，請使用使用者介面](../ui/monitor-sources.md)教學課程閱讀來源的[監視資料流。 如需如何監視目的地的資料流的詳細資訊，請使用使用者介面](../ui/monitor-destinations.md)教學課程閱讀目的地的[監視資料流。
