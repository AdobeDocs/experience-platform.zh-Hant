---
keywords: Experience Platform；首頁；熱門主題；監控資料流；流服務api；流服務
solution: Experience Platform
title: 使用流服務API監視資料流
topic-legacy: overview
type: Tutorial
description: 本教學課程涵蓋使用Flow Service API監控流程執行資料的完整性、錯誤和度量的步驟。
exl-id: c4b2db97-eba4-460d-8c00-c76c666ed70e
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '722'
ht-degree: 1%

---

# 使用流服務API監視資料流

Adobe Experience Platform允許從外部來源接收資料，同時提供使用[!DNL Platform]服務構建、標籤和增強傳入資料的能力。 您可以從多種來源收錄資料，例如Adobe應用程式、雲端儲存空間、資料庫等。 此外，Experience Platform允許將資料激活給外部合作夥伴。

[!DNL Flow Service] 用於收集和集中Adobe Experience Platform內不同來源的客戶資料。該服務提供用戶介面和REST風格的API，所有支援的源和目標都可從中連接。

本教學課程涵蓋使用[[!DNL Flow Service API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml)監控流程執行資料的完整性、錯誤和度量的步驟。

## 快速入門

本教程要求您具有有效資料流的ID值。 如果您沒有有效的資料流ID，請從[源概述](../../sources/home.md)或[目標概述](../../destinations/catalog/overview.md)中選擇所選的連接器，並遵循在嘗試本教程之前概述的步驟。

本教學課程還要求您對Adobe Experience Platform的以下部分有切實的瞭解：

- [目標](../../destinations/home.md):目標是與常用應用程式預先建立的整合，可讓跨通道行銷宣傳、電子郵件宣傳、目標廣告和許多其他使用案例的平台資料順暢啟動。
- [來源](../../sources/home.md): [!DNL Experience Platform] 允許從各種來源接收資料，同時提供使用服務構建、標籤和增強傳入資料的 [!DNL Platform] 能力。
- [沙盒](../../sandboxes/home.md): [!DNL Experience Platform] 提供虛擬沙盒，可將單一執行個體分 [!DNL Platform] 割為不同的虛擬環境，以協助開發和發展數位體驗應用程式。

以下各節提供您需要瞭解的其他資訊，以便使用[!DNL Flow Service] API成功監控流程執行。

### 讀取範例API呼叫

本教學課程提供範例API呼叫，以示範如何設定請求的格式。 這些包括路徑、必要標題和正確格式化的請求負載。 也提供API回應中傳回的範例JSON。 如需範例API呼叫檔案中所用慣例的詳細資訊，請參閱[!DNL Experience Platform]疑難排解指南中[如何讀取範例API呼叫](../../landing/troubleshooting.md#how-do-i-format-an-api-request)一節。

### 收集必要標題的值

若要呼叫[!DNL Platform] API，您必須先完成[驗證教學課程](https://www.adobe.com/go/platform-api-authentication-en)。 完成驗證教學課程後，所有[!DNL Experience Platform] API呼叫中每個所需標題的值都會顯示在下面：

- `Authorization: Bearer {ACCESS_TOKEN}`
- `x-api-key: {API_KEY}`
- `x-gw-ims-org-id: {IMS_ORG}`

[!DNL Experience Platform]中的所有資源（包括屬於[!DNL Flow Service]的資源）都隔離到特定的虛擬沙盒。 對[!DNL Platform] API的所有請求都需要一個標題，該標題指定要在中執行操作的沙盒的名稱：

- `x-sandbox-name: {SANDBOX_NAME}`

所有包含裝載(POST、PUT、PATCH)的請求都需要附加的媒體類型標題：

- `Content-Type: application/json`

## 監控流程執行

進行資料流後，請對[!DNL Flow Service] API執行GET請求。

**API格式**

```http
GET /runs?property=flowId=={FLOW_ID}
```

| 參數 | 說明 |
| --------- | ----------- |
| `{FLOW_ID}` | 要監視的資料流的唯一`id`值。 |

**要求**

以下請求將檢索現有資料流的規範。

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/runs?property=flowId==c9cef9cb-c934-4467-8ef9-cbc934546741' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應會傳回有關您的流程執行的詳細資訊，包括有關其建立日期、來源和目標連線的資訊，以及流程執行的唯一識別碼(`id`)。

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
            "imsOrgId": "{IMS_ORG_ID}",
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
| `items` | 包含與特定流程執行相關聯之中繼資料的單一裝載。 |
| `metrics` | 流中資料的特性。 |
| `activities` | 顯示資料的轉換方式。 |
| `durationSummary` | 流運行的開始和結束時間。 |
| `sizeSummary` | 資料的卷（以位元組為單位）。 |
| `recordSummary` | 資料的記錄計數。 |
| `fileSummary` | 資料的檔案計數。 |
| `fileSummary.extensions` | 包含活動專屬的資訊。 例如，`manifest`僅是「促銷活動」的一部分，因此它隨`extensions`對象一起提供。 |
| `statusSummary` | 顯示流運行是成功還是失敗。 |

## 後續步驟

在本教程之後，您使用[!DNL Flow Service] API檢索了有關資料流的度量和錯誤資訊。 您現在可以根據您的接收計畫繼續監視資料流，以跟蹤其狀態和接收速率。 有關如何監視源的資料流的資訊，請閱讀使用用戶介面](../ui/monitor-sources.md)教程的[監視源的資料流。 有關如何監視目標的資料流的詳細資訊，請閱讀使用用戶介面](../ui/monitor-destinations.md)教程的[監視目標的資料流。
