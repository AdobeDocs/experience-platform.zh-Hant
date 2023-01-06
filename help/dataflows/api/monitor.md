---
keywords: Experience Platform；首頁；熱門主題；監視資料流；流服務api；流服務
solution: Experience Platform
title: 使用流服務API監視資料流
type: Tutorial
description: 本教學課程涵蓋使用流程服務API監控流程執行資料的完整性、錯誤和量度的步驟。
exl-id: c4b2db97-eba4-460d-8c00-c76c666ed70e
source-git-commit: 1a7ba52b48460d77d0b7695aa0ab2d5be127d921
workflow-type: tm+mt
source-wordcount: '718'
ht-degree: 1%

---

# 使用流服務API監視資料流

Adobe Experience Platform可讓您從外部來源擷取資料，同時使用來建構、加標籤及增強傳入資料 [!DNL Platform] 服務。 您可以從多種來源(如Adobe應用程式、雲儲存、資料庫等)內嵌資料。 此外，Experience Platform可讓資料啟動給外部合作夥伴。

[!DNL Flow Service] 可用來收集和集中Adobe Experience Platform中各種不同來源的客戶資料。 該服務提供用戶介面和RESTful API，所有受支援的源和目標都可從中連接。

本教學課程涵蓋監控流程執行資料的步驟，其內容包括使用 [[!DNL Flow Service API]](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## 快速入門

本教程要求您具有有效資料流的ID值。 如果您沒有有效的資料流ID，請從 [來源概觀](../../sources/home.md) 或 [目的地概述](../../destinations/catalog/overview.md) 並遵循在嘗試本教學課程之前概述的步驟。

本教學課程也需要您妥善了解下列Adobe Experience Platform元件：

- [目的地](../../destinations/home.md):目的地是與常用應用程式預先建立的整合，可順暢地啟動來自Platform的資料，以進行跨通路行銷活動、電子郵件行銷活動、目標廣告和許多其他使用案例。
- [來源](../../sources/home.md): [!DNL Experience Platform] 可讓您從各種來源擷取資料，同時使用來建構、加標籤及增強傳入資料 [!DNL Platform] 服務。
- [沙箱](../../sandboxes/home.md): [!DNL Experience Platform] 提供可分割單一沙箱的虛擬沙箱 [!DNL Platform] 例項放入個別的虛擬環境，以協助開發及改進數位體驗應用程式。

以下章節提供您需要知道的其他資訊，以便使用成功監控流程執行 [!DNL Flow Service] API。

### 讀取範例API呼叫

本教學課程提供範例API呼叫，以示範如何設定要求格式。 這些功能包括路徑、必要標題和格式正確的請求裝載。 也提供API回應中傳回的範例JSON。 如需範例API呼叫檔案中所使用慣例的相關資訊，請參閱 [如何閱讀API呼叫範例](../../landing/troubleshooting.md#how-do-i-format-an-api-request) 在 [!DNL Experience Platform] 疑難排解指南。

### 收集必要標題的值

若要對 [!DNL Platform] API，您必須先完成 [驗證教學課程](https://www.adobe.com/go/platform-api-authentication-en). 完成驗證教學課程會提供所有 [!DNL Experience Platform] API呼叫，如下所示：

- `Authorization: Bearer {ACCESS_TOKEN}`
- `x-api-key: {API_KEY}`
- `x-gw-ims-org-id: {ORG_ID}`

中的所有資源 [!DNL Experience Platform]，包括 [!DNL Flow Service]，會與特定虛擬沙箱隔離。 所有請求 [!DNL Platform] API需要標頭，以指定要在中執行操作的沙箱名稱：

- `x-sandbox-name: {SANDBOX_NAME}`

所有包含裝載(POST、PUT、PATCH)的請求都需要其他媒體類型標題：

- `Content-Type: application/json`

## 監視流運行

建立資料流後，請執行GET請求 [!DNL Flow Service] API。

**API格式**

```http
GET /runs?property=flowId=={FLOW_ID}
```

| 參數 | 說明 |
| --------- | ----------- |
| `{FLOW_ID}` | 唯一 `id` 要監視的資料流的值。 |

**要求**

以下請求將檢索現有資料流的規範。

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/runs?property=flowId==c9cef9cb-c934-4467-8ef9-cbc934546741' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應會傳回關於流程執行的詳細資訊，包括關於其建立日期、來源和目標連線的資訊，以及流程執行的唯一識別碼(`id`)。

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
| `items` | 包含與您特定流程執行相關聯的中繼資料的單一裝載。 |
| `metrics` | 流運行中資料的特性。 |
| `activities` | 顯示資料的轉換方式。 |
| `durationSummary` | 流運行的開始和結束時間。 |
| `sizeSummary` | 資料的卷（以位元組為單位）。 |
| `recordSummary` | 資料的記錄計數。 |
| `fileSummary` | 資料的檔案計數。 |
| `fileSummary.extensions` | 包含活動專屬的資訊。 例如， `manifest` 只是「促銷活動」的一部分，因此會隨 `extensions` 物件。 |
| `statusSummary` | 顯示流程執行是成功還是失敗。 |

## 後續步驟

依照本教學課程，您已使用 [!DNL Flow Service] API。 您現在可以根據您的獲取計畫繼續監視資料流，以跟蹤其狀態和獲取率。 有關如何監視源資料流的資訊，請閱讀 [使用用戶介面監視源的資料流](../ui/monitor-sources.md) 教學課程。 有關如何監視目標的資料流的詳細資訊，請閱讀 [使用用戶介面監視目標的資料流](../ui/monitor-destinations.md) 教學課程。
