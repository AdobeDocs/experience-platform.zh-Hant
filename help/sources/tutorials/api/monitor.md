---
keywords: Experience Platform；首頁；熱門主題；監視資料流；流服務api；流服務
solution: Experience Platform
title: 使用流服務API監視資料流
topic-legacy: overview
type: Tutorial
description: 本教程介紹使用流服務API監視流運行資料的完整性、錯誤和度量的步驟。
exl-id: 5b7d1aa4-5e6d-48f4-82bd-5348dc0e890d
source-git-commit: a51c878bbfd3004cb597ce9244a9ed2f2318604b
workflow-type: tm+mt
source-wordcount: '629'
ht-degree: 1%

---

# 使用流服務API監視資料流

Adobe Experience Platform允許從外部源接收資料，同時讓您能夠使用 [!DNL Platform] 服務。 您可以從多種源(如Adobe應用程式、基於雲的儲存、資料庫和許多其他源)接收資料。

[!DNL Flow Service] 用於收集和集中Adobe Experience Platform內不同來源的客戶資料。 該服務提供了用戶介面和REST風格的API，所有支援的源都可從中連接。

本教程介紹了使用以下工具監控流運行資料的步驟： [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/)。

## 快速入門

本教程要求您具有有效資料流的ID值。 如果沒有有效的資料流ID，請從 [源概述](../../home.md) 在嘗試本教程之前，請按照上述步驟操作。

本教程還要求您對以下Adobe Experience Platform元件有一定的瞭解：

* [源](../../home.md): [!DNL Experience Platform] 允許從各種源接收資料，同時讓您能夠使用 [!DNL Platform] 服務。
* [沙箱](../../../sandboxes/home.md): [!DNL Experience Platform] 提供虛擬沙箱，將單個沙箱 [!DNL Platform] 實例到獨立的虛擬環境，以幫助開發和發展數字型驗應用程式。

以下各節提供了您需要瞭解的其他資訊，以便使用 [!DNL Flow Service] API。

### 讀取示例API調用

本教程提供了示例API調用，以演示如何格式化請求。 這些包括路徑、必需的標頭和正確格式化的請求負載。 還提供了API響應中返回的示例JSON。 有關示例API調用文檔中使用的約定的資訊，請參見上的 [如何讀取示例API調用](../../../landing/troubleshooting.md#how-do-i-format-an-api-request) 的 [!DNL Experience Platform] 疑難解答指南。

### 收集所需標題的值

為了呼叫 [!DNL Platform] API，必須首先完成 [驗證教程](https://www.adobe.com/go/platform-api-authentication-en)。 完成身份驗證教程將提供所有中每個必需標頭的值 [!DNL Experience Platform] API調用，如下所示：

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

中的所有資源 [!DNL Experience Platform]包括那些 [!DNL Flow Service]，與特定虛擬沙箱隔離。 所有請求 [!DNL Platform] API需要一個標頭，該標頭指定操作將在以下位置進行的沙盒的名稱：

* `x-sandbox-name: {SANDBOX_NAME}`

所有包含負載(POST、PUT、PATCH)的請求都需要附加的媒體類型報頭：

* `Content-Type: application/json`

## 監視流運行

一旦建立了資料流，請向執行GET請求 [!DNL Flow Service] API。

**API格式**

```http
GET /runs?property=flowId=={FLOW_ID}
```

| 參數 | 說明 |
| --------- | ----------- |
| `{FLOW_ID}` | 獨特 `id` 要監視的資料流的值。 |

**要求**

以下請求檢索現有資料流的規範。

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/runs?property=flowId==c9cef9cb-c934-4467-8ef9-cbc934546741' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的響應將返回有關流運行的詳細資訊，包括有關其建立日期、源和目標連接以及流運行的唯一標識符(`id`)。

```json
{
    "items": [
        {
            "createdAt": 1596656079576,
            "updatedAt": 1596656113526,
            "createdBy": "{CREATED_BY}",
            "updatedBy": "{UPDATED_BY}",
            "createdClient": "{CREATED_CLIENT}",
            "updatedClient": "{UPDATED_CLIENT}",
            "sandboxId": "1bd86660-c5da-11e9-93d4-6d5fc3a66a8e",
            "sandboxName": "prod",
            "id": "9830305a-985f-47d0-b030-5a985fd7d004",
            "flowId": "c9cef9cb-c934-4467-8ef9-cbc934546741",
            "etag": "\"b8003af1-0000-0200-0000-5f2b09f10000\"",
            "metrics": {
                "durationSummary": {
                    "startedAtUTC": 1596656058198,
                    "completedAtUTC": 1596656113306
                },
                "sizeSummary": {
                    "inputBytes": 24012,
                    "outputBytes": 17128
                },
                "recordSummary": {
                    "inputRecordCount": 100,
                    "outputRecordCount": 99,
                    "failedRecordCount": 1
                },
                "fileSummary": {
                    "inputFileCount": 1,
                    "outputFileCount": 1,
                    "activityRefs": [
                        "promotionActivity"
                    ]
                },
                "statusSummary": {
                    "status": "success",
                    "errors": [
                        {
                            "code": "CONNECTOR-2001-500",
                            "message": "Error occurred at promotion activity."
                        }
                    ],
                    "activityRefs": [
                        "promotionActivity"
                    ]
                }
            },
            "activities": [
                {
                    "id": "copyActivity",
                    "updatedAtUTC": 1596656095088,
                    "durationSummary": {
                        "startedAtUTC": 1596656058198,
                        "completedAtUTC": 1596656089650,
                        "extensions": {
                            "windowStart": 1596653708000,
                            "windowEnd": 1596655508000
                        }
                    },
                    "sizeSummary": {
                        "inputBytes": 24012,
                        "outputBytes": 24012
                    },
                    "recordSummary": {},
                    "fileSummary": {
                        "inputFileCount": 1,
                        "outputFileCount": 1
                    },
                    "statusSummary": {
                        "status": "success",
                        "extensions": {
                            "type": "one-time"
                        }
                    },
                    "sourceInfo": [
                        {
                            "id": "c0e18602-f9ea-44f9-a186-02f9ea64f9ac",
                            "type": "SourceConnection",
                            "reference": {
                                "type": "AdfRunId",
                                "ids": [
                                    "8a8eb0cc-e283-4605-ac70-65a5adb1baef"
                                ]
                            }
                        }
                    ]
                },
                {
                    "id": "promotionActivity",
                    "updatedAtUTC": 1596656113485,
                    "durationSummary": {
                        "startedAtUTC": 1596656095333,
                        "completedAtUTC": 1596656113306
                    },
                    "sizeSummary": {
                        "inputBytes": 24012,
                        "outputBytes": 17128
                    },
                    "recordSummary": {
                        "inputRecordCount": 100,
                        "outputRecordCount": 99,
                        "failedRecordCount": 1
                    },
                    "fileSummary": {
                        "inputFileCount": 2,
                        "outputFileCount": 1,
                        "extensions": {
                            "manifest": {
                                "fileInfo": "https://platform.adobe.io/data/foundation/export/batches/01EF01X41KJD82Y9ZX6ET54PCZ/meta?path=input_files"
                            }
                        }
                    },
                    "statusSummary": {
                        "status": "success",
                        "errors": [
                            {
                                "code": "CONNECTOR-2001-500",
                                "message": "Error occurred at promotion activity."
                            }
                        ],
                        "extensions": {
                            "manifest": {
                                "failedRecords": "https://platform.adobe.io/data/foundation/export/batches/01EF01X41KJD82Y9ZX6ET54PCZ/meta?path=row_errors",
                                "sampleErrors": "https://platform.adobe.io/data/foundation/export/batches/01EF01X41KJD82Y9ZX6ET54PCZ/meta?path=row_error_samples.json"
                            },
                            "errors": [
                                {
                                    "code": "INGEST-1212-400",
                                    "message": "Encountered 1 errors in the data. Successfully ingested 99 rows. Review the associated diagnostic files for additional details."
                                },
                                {
                                    "code": "MAPPER-3700-400",
                                    "recordCount": 1,
                                    "message": "Mapper Transform Error"
                                }
                            ]
                        }
                    },
                    "targetInfo": [
                        {
                            "id": "47166b83-01c7-4b65-966b-8301c70b6562",
                            "type": "TargetConnection",
                            "reference": {
                                "type": "Batch",
                                "ids": [
                                    "01EF01X41KJD82Y9ZX6ET54PCZ"
                                ]
                            }
                        }
                    ]
                }
            ]
        }
    ],
    "_links": {}
}
```

| 屬性 | 說明 |
| -------- | ----------- |
| `items` | 包含與特定流運行關聯的元資料的單個負載。 |
| `metrics` | 定義流運行中資料的特徵。 |
| `activities` | 定義資料的轉換方式。 |
| `durationSummary` | 定義流運行的開始和結束時間。 |
| `sizeSummary` | 定義資料的卷（以位元組為單位）。 |
| `recordSummary` | 定義資料的記錄計數。 |
| `fileSummary` | 定義資料的檔案計數。 |
| `statusSummary` | 定義流運行是成功還是失敗。 |

## 後續步驟

按照本教程，您已使用 [!DNL Flow Service] API。 現在，您可以繼續監視資料流，以跟蹤其狀態和攝取速率。 有關如何使用用戶介面執行相同任務的資訊，請參見上的教程 [使用用戶介面監視資料流](../ui/monitor.md)
