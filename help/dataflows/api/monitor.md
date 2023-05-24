---
keywords: Experience Platform；首頁；熱門主題；監視資料流；流服務api；流服務
solution: Experience Platform
title: 使用流服務API監視資料流
type: Tutorial
description: 本教程介紹使用流服務API監視流運行資料的完整性、錯誤和度量的步驟。
exl-id: c4b2db97-eba4-460d-8c00-c76c666ed70e
source-git-commit: 1a7ba52b48460d77d0b7695aa0ab2d5be127d921
workflow-type: tm+mt
source-wordcount: '718'
ht-degree: 1%

---

# 使用流服務API監視資料流

Adobe Experience Platform允許從外部源接收資料，同時讓您能夠使用 [!DNL Platform] 服務。 您可以從多種源(如Adobe應用程式、基於雲的儲存、資料庫和許多其他源)接收資料。 此外，Experience Platform允許將資料激活給外部合作夥伴。

[!DNL Flow Service] 用於收集和集中Adobe Experience Platform內不同來源的客戶資料。 該服務提供用戶介面和REST風格的API，所有支援的源和目標都可從中連接。

本教程介紹了使用以下工具監控流運行資料的步驟： [[!DNL Flow Service API]](https://www.adobe.io/experience-platform-apis/references/flow-service/)。

## 快速入門

本教程要求您具有有效資料流的ID值。 如果沒有有效的資料流ID，請從 [源概述](../../sources/home.md) 或 [目標概述](../../destinations/catalog/overview.md) 在嘗試本教程之前，請按照上述步驟操作。

本教程還要求您對以下Adobe Experience Platform元件有一定的瞭解：

- [目標](../../destinations/home.md):目標是預構建的與常用應用程式的整合，這些整合允許從平台無縫激活資料，用於跨渠道營銷活動、電子郵件活動、目標廣告和許多其他使用案例。
- [源](../../sources/home.md): [!DNL Experience Platform] 允許從各種源接收資料，同時讓您能夠使用 [!DNL Platform] 服務。
- [沙箱](../../sandboxes/home.md): [!DNL Experience Platform] 提供虛擬沙箱，將單個沙箱 [!DNL Platform] 實例到獨立的虛擬環境，以幫助開發和發展數字型驗應用程式。

以下各節提供了您需要瞭解的其他資訊，以便使用 [!DNL Flow Service] API。

### 讀取示例API調用

本教程提供了示例API調用，以演示如何格式化請求。 這些包括路徑、必需的標頭和正確格式化的請求負載。 還提供了API響應中返回的示例JSON。 有關示例API調用文檔中使用的約定的資訊，請參見上的 [如何讀取示例API調用](../../landing/troubleshooting.md#how-do-i-format-an-api-request) 的 [!DNL Experience Platform] 疑難解答指南。

### 收集所需標題的值

為了呼叫 [!DNL Platform] API，必須首先完成 [驗證教程](https://www.adobe.com/go/platform-api-authentication-en)。 完成身份驗證教程將提供所有中每個必需標頭的值 [!DNL Experience Platform] API調用，如下所示：

- `Authorization: Bearer {ACCESS_TOKEN}`
- `x-api-key: {API_KEY}`
- `x-gw-ims-org-id: {ORG_ID}`

中的所有資源 [!DNL Experience Platform]包括那些 [!DNL Flow Service]，與特定虛擬沙箱隔離。 所有請求 [!DNL Platform] API需要一個標頭，該標頭指定操作將在以下位置進行的沙盒的名稱：

- `x-sandbox-name: {SANDBOX_NAME}`

所有包含負載(POST、PUT、PATCH)的請求都需要附加的媒體類型報頭：

- `Content-Type: application/json`

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
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的響應將返回有關流運行的詳細資訊，包括有關其建立日期、源和目標連接以及流運行的唯一標識符(`id`)。

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
| `items` | 包含與特定流運行關聯的元資料的單個負載。 |
| `metrics` | 流運行中資料的特徵。 |
| `activities` | 顯示資料如何轉換。 |
| `durationSummary` | 流運行的開始和結束時間。 |
| `sizeSummary` | 資料的卷（位元組）。 |
| `recordSummary` | 資料的記錄計數。 |
| `fileSummary` | 資料的檔案計數。 |
| `fileSummary.extensions` | 包含特定於活動的資訊。 比如說， `manifest` 只是「促銷活動」的一部分，因此它包含在 `extensions` 的雙曲餘切值。 |
| `statusSummary` | 顯示流運行是成功還是失敗。 |

## 後續步驟

按照本教程，您已使用 [!DNL Flow Service] API。 現在，您可以繼續監視資料流，以跟蹤其狀態和攝取速率。 有關如何監視源的資料流的資訊，請閱讀 [使用用戶介面監視源的資料流](../ui/monitor-sources.md) 教程。 有關如何監視目標的資料流的詳細資訊，請閱讀 [使用用戶介面監視目標的資料流](../ui/monitor-destinations.md) 教程。
