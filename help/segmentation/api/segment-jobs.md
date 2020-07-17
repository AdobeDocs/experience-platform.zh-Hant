---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 區段工作
topic: developer guide
translation-type: tm+mt
source-git-commit: 2327ce9a87647fb2416093d4a27eb7d4dc4aa4d7
workflow-type: tm+mt
source-wordcount: '994'
ht-degree: 3%

---


# 區段作業端點指南

區段工作是建立新讀者區段的非同步程式。 它引用段定 [義](./segment-definitions.md)，以及任何合併策略 [，以控制如何合併配置檔案片段](../../profile/api/merge-policies.md)[!DNL Real-time Customer Profile] 中的重疊屬性。 當區段工作成功完成時，您可以收集區段的各種資訊，例如處理期間可能發生的任何錯誤，以及您的受眾的最終規模。

本指南提供相關資訊，以協助您進一步瞭解區段工作，並包含使用API執行基本動作的範例API呼叫。

## 快速入門

本指南中使用的端點是 [!DNL Adobe Experience Platform Segmentation Service] API的一部分。 在繼續之前，請先檢閱 [快速入門手冊](./getting-started.md) ，以取得成功呼叫API所需的重要資訊，包括必要的標題和如何讀取範例API呼叫。

## 擷取區段工作清單 {#retrieve-list}

您可以向端點提出GET請求，以擷取IMS組織所有區段工作的清 `/segment/jobs` 單。

**API格式**

端點 `/segment/jobs` 支援數個查詢參數，以協助篩選結果。 雖然這些參數是可選的，但強烈建議使用這些參數以幫助降低昂貴的開銷。 在沒有參數的情況下呼叫此端點將會擷取組織所有可用的匯出工作。 可包含多個參數，由&amp;符號(`&`)分隔。

```http
GET /segment/jobs
GET /segment/jobs?{QUERY_PARAMETERS}
```

**查詢參數**

| 參數 | 說明 | 範例 |
| --------- | ----------- | ------- |
| `start` | 指定返回的段作業的起始偏移。 | `start=1` |
| `limit` | 指定每頁傳回的區段工作數。 | `limit=20` |
| `status` | 根據狀態篩選結果。 支援的值有新值、排隊、處理、成功、失敗、取消、取消 | `status=NEW` |
| `sort` | 訂購傳回的區段工作。 以格式寫入 `[attributeName]:[desc|asc]`。 | `sort=creationTime:desc` |
| `property` | 篩選群體工作，並取得指定篩選的完全相符項目。 它可以以下列任一格式編寫： <ul><li>`[jsonObjectPath]==[value]` -對對象鍵進行篩選</li><li>`[arrayTypeAttributeName]~[objectKey]==[value]` -陣列內的篩選</li></ul> | `property=segments~segmentId==workInUS` |

**請求**

```shell
curl -X GET https://platform.adobe.io/data/core/ups/segment/jobs?status=SUCCEEDED \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應會傳回HTTP狀態200，並將指定IMS組織的區段工作清單列為JSON。 下列回應會傳回IMS組織所有成功區段工作的清單。

>[!NOTE]
>
>下列回應已截斷空間，且只會顯示第一個傳回的工作。

```json
{
    "_page": {
        "totalCount": 14,
        "pageSize": 14
    },
    "children": [
        {
            "id": "b31aed3d-b3b1-4613-98c6-7d3846e8d48f",
            "imsOrgId": "E95186D65A28ABF00A495D82@AdobeOrg",
            "sandbox": {
                "sandboxId": "28e74200-e3de-11e9-8f5d-7f27416c5f0d",
                "sandboxName": "prod",
                "type": "production",
                "default": true
            },
            "profileInstanceId": "ups",
            "source": "scheduler",
            "status": "SUCCEEDED",
            "batchId": "678f53bc-e21d-4c47-a7ec-5ad0064f8e4c",
            "computeJobId": 8811,
            "computeGatewayJobId": "9ea97b25-a0f5-410e-ae87-b2d85e58f399",
            "segments": [
                {
                    "segmentId": "30230300-ccf1-48ad-8012-c5563a007069",
                    "segment": {
                        "id": "30230300-ccf1-48ad-8012-c5563a007069",
                        "expression": {
                            "type": "PQL",
                            "format": "pql/json",
                            "value": "{PQL_EXPRESSION}"
                        },
                        "mergePolicyId": "b83185bb-0bc6-489c-9363-0075eb30b4c8",
                        "mergePolicy": {
                            "id": "b83185bb-0bc6-489c-9363-0075eb30b4c8",
                            "version": 1
                        }
                    }
                }
            ],
            "metrics": {
                "totalTime": {
                    "startTimeInMs": 1573203617195,
                    "endTimeInMs": 1573204395655,
                    "totalTimeInMs": 778460
                },
                "profileSegmentationTime": {
                    "startTimeInMs": 1573204266727,
                    "endTimeInMs": 1573204395655,
                    "totalTimeInMs": 128928
                },
                "totalProfiles": 0,
                "segmentedProfileCounter": {
                    "30230300-ccf1-48ad-8012-c5563a007069": 0,
                    "ca763983-5572-4ea4-809c-b7dff7e0d79b": 0
                },
                "segmentedProfileByNamespaceCounter": {
                    "30230300-ccf1-48ad-8012-c5563a007069": {},
                    "ca763983-5572-4ea4-809c-b7dff7e0d79b": {}
                }
            },
            "requestId": "4e538382-dbd8-449e-988a-4ac639ebe72b-1573203600264",
            "schema": {
                "name": "_xdm.context.profile"
            },
            "properties": {
                "scheduleId": "4e538382-dbd8-449e-988a-4ac639ebe72b",
                "runId": "e6c1308d-0d4b-4246-b2eb-43697b50a149"
            },
            "_links": {
                "cancel": {
                    "href": "/segment/jobs/b31aed3d-b3b1-4613-98c6-7d3846e8d48f",
                    "method": "DELETE"
                },
                "checkStatus": {
                    "href": "/segment/jobs/b31aed3d-b3b1-4613-98c6-7d3846e8d48f",
                    "method": "GET"
                }
            },
            "updateTime": 1573204395000,
            "creationTime": 1573203600535,
            "updateEpoch": 1573204395
        }
    ],
    "_links": {
        "next": {}
    }
}
```

| 屬性 | 說明 |
| -------- | ----------- |
| `id` | 系統產生的區段作業唯讀識別碼。 |
| `status` | 區段工作的目前狀態。 狀態的潛在值包括「新」、「處理」、「取消」、「已取消」、「失敗」和「成功」。 |
| `segments` | 包含區段工作中傳回之區段定義資訊的物件。 |
| `segments.segment.id` | 區段定義的ID。 |
| `segments.segment.expression` | 包含有關段定義表達式的資訊的對象，用PQL編寫。 |
| `metrics` | 包含區段作業診斷資訊的物件。 |

## 建立新區段工作 {#create}

您可以透過向端點提出POST請求，並在內文中加入您要建立新對象的區段定義的ID，來建立新的區段工作。 `/segment/jobs`

**API格式**

```http
POST /segment/jobs
```

**請求**

```shell
curl -X POST https://platform.adobe.io/data/core/ups/segment/jobs \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
[
  {
    "segmentId": "4afe34ae-8c98-4513-8a1d-67ccaa54bc05",
  }
]'
```

| 屬性 | 說明 |
| -------- | ----------- |
| `segmentId` | 您要為其建立區段工作之區段定義的ID。 如需區段定義的詳細資訊，請參閱區段定 [義端點指南](./segment-definitions.md)。 |

**回應**

成功的回應會傳回HTTP狀態200，並包含您新建立之區段工作的詳細資訊。

```json
{
    "id": "d3b4a50d-dfea-43eb-9fca-557ea53771fd",
    "imsOrgId": "{IMS_ORG}",
    "sandbox": {
        "sandboxId": "28e74200-e3de-11e9-8f5d-7f27416c5f0d",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "profileInstanceId": "ups",
    "source": "api",
    "status": "NEW",
    "segments": [
        {
            "segmentId": "4afe34ae-8c98-4513-8a1d-67ccaa54bc05",
            "segment": {
                "id": "4afe34ae-8c98-4513-8a1d-67ccaa54bc05",
                "expression": {
                    "type": "PQL",
                    "format": "pql/text",
                    "value": "workAddress.country = \"US\""
                },
                "mergePolicyId": "e161dae9-52f0-4c7f-b264-dc43dd903d56",
                "mergePolicy": {
                    "id": "e161dae9-52f0-4c7f-b264-dc43dd903d56",
                    "version": 1
                }
            }
        }
    ],
    "requestId": "Hw1jdAHeuWHVKVxcAPFrLCbbjkriDl9v",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "_links": {
        "cancel": {
            "href": "/segment/jobs/d3b4a50d-dfea-43eb-9fca-557ea53771fd",
            "method": "DELETE"
        },
        "checkStatus": {
            "href": "/segment/jobs/d3b4a50d-dfea-43eb-9fca-557ea53771fd",
            "method": "GET"
        }
    },
    "updateTime": 1579304260000,
    "creationTime": 1579304260897,
    "updateEpoch": 1579304260
}
```

| 屬性 | 說明 |
| -------- | ----------- |
| `id` | 新建立之區段工作的系統產生唯讀識別碼。 |
| `status` | 區段工作的目前狀態。 由於區段工作是新建立的，因此狀態一律為「新增」。 |
| `segments` | 包含此段作業正在為其運行的段定義相關資訊的對象。 |
| `segments.segment.id` | 您提供的區段定義ID。 |
| `segments.segment.expression` | 包含有關段定義表達式的資訊的對象，用PQL編寫。 |

## 擷取特定區段工作 {#get}

您可以向端點發出GET請求，並提供您想在請求路徑中檢索的區段作業ID，以檢索有關特定區段作業的詳細資訊。 `/segment/jobs`

**API格式**

```http
GET /segment/jobs/{SEGMENT_JOB_ID}
```

| 屬性 | 說明 |
| -------- | ----------- | 
| `{SEGMENT_JOB_ID}` | 您 `id` 要擷取的區段工作值。 |

**請求**

```shell
curl -X GET https://platform.adobe.io/data/core/ups/segment/jobs/d3b4a50d-dfea-43eb-9fca-557ea53771fd \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應會傳回HTTP狀態200，其中包含指定區段工作的詳細資訊。

```json
{
    "id": "d3b4a50d-dfea-43eb-9fca-557ea53771fd",
    "imsOrgId": "{IMS_ORG}",
    "sandbox": {
        "sandboxId": "28e74200-e3de-11e9-8f5d-7f27416c5f0d",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "profileInstanceId": "ups",
    "source": "api",
    "status": "SUCCEEDED",
    "batchId": "651fc109-3963-48d2-aa98-9e3cc2003bac",
    "computeJobId": 39312,
    "computeGatewayJobId": "a0099ab6-11ab-4c2b-a0ea-6162e16806bd",
    "segments": [
        {
            "segmentId": "4afe34ae-8c98-4513-8a1d-67ccaa54bc05",
            "segment": {
                "id": "4afe34ae-8c98-4513-8a1d-67ccaa54bc05",
                "expression": {
                    "type": "PQL",
                    "format": "pql/text",
                    "value": "workAddress.country = \"US\""
                },
                "mergePolicyId": "e161dae9-52f0-4c7f-b264-dc43dd903d56",
                "mergePolicy": {
                    "id": "e161dae9-52f0-4c7f-b264-dc43dd903d56",
                    "version": 1
                }
            }
        }
    ],
    "metrics": {
        "totalTime": {
            "startTimeInMs": 1579304313411
        },
        "profileSegmentationTime": {}
    },
    "requestId": "Hw1jdAHeuWHVKVxcAPFrLCbbjkriDl9v",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "_links": {
        "cancel": {
            "href": "/segment/jobs/d3b4a50d-dfea-43eb-9fca-557ea53771fd",
            "method": "DELETE"
        },
        "checkStatus": {
            "href": "/segment/jobs/d3b4a50d-dfea-43eb-9fca-557ea53771fd",
            "method": "GET"
        }
    },
    "updateTime": 1579304339000,
    "creationTime": 1579304260897,
    "updateEpoch": 1579304339
}
```

| 屬性 | 說明 |
| -------- | ----------- |
| `id` | 系統產生的區段作業唯讀識別碼。 |
| `status` | 區段工作的目前狀態。 狀態的潛在值包括「新」、「處理」、「取消」、「已取消」、「失敗」和「成功」。 |
| `segments` | 包含區段工作中傳回之區段定義資訊的物件。 |
| `segments.segment.id` | 區段定義的ID。 |
| `segments.segment.expression` | 包含有關段定義表達式的資訊的對象，用PQL編寫。 |
| `metrics` | 包含區段作業診斷資訊的物件。 |

## 大量擷取區段工作 {#bulk-get}

您可以向端點提出POST請求，並在請求主體中提供段作業值，以檢 `/segment/jobs/bulk-get` 索多 `id` 個段作業的詳細資訊。

**API格式**

```http
POST /segment/jobs/bulk-get
```

**請求**

```shell
curl -X POST https://platform.adobe.io/data/core/ups/segment/jobs/bulk-get \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "ids": [
            {
                "id": "cc3419d3-0389-47f1-b174-fead6b3c830d"
            },
            {
                "id": "c527dc3f-07fe-4b96-be4e-23f38e734ff8"
            }
        ]
    }'
```

**回應**

成功的回應會傳回HTTP狀態207與請求的區段工作。

>[!NOTE]
>
>下列回應已截斷空間，僅顯示每個區段工作的部分詳細資料。 完整回應會列出所請求之區段工作的完整詳細資訊。

```json
{
    "results": {
        "cc3419d3-0389-47f1-b174-fead6b3c830d": {
            "id": "cc3419d3-0389-47f1-b174-fead6b3c830d",
            "imsOrgId": "{IMS_ORG}",
            "status": "SUCCEEDED",
            "segments": [
                {
                    "segmentId": "30230300-ccf1-48ad-8012-c5563a007069",
                    "segment": {
                        "id": "30230300-ccf1-48ad-8012-c5563a007069",
                        "expression": {
                            "type": "PQL",
                            "format": "pql/json",
                            "value": "{PQL_EXPRESSION}"
                        },
                        "mergePolicyId": "b83185bb-0bc6-489c-9363-0075eb30b4c8",
                        "mergePolicy": {
                            "id": "b83185bb-0bc6-489c-9363-0075eb30b4c8",
                            "version": 1
                        }
                    }
                }
            ],
            "updateTime": 1573204395000,
            "creationTime": 1573203600535,
            "updateEpoch": 1573204395
        },
        "c527dc3f-07fe-4b96-be4e-23f38e734ff8": {
            "id": "c527dc3f-07fe-4b96-be4e-23f38e734ff8",
            "imsOrgId": "{IMS_ORG}",
            "status": "SUCCEEDED",
            "segments": [
                {
                    "segmentId": "4afe34ae-8c98-4513-8a1d-67ccaa54bc05",
                    "segment": {
                        "id": "4afe34ae-8c98-4513-8a1d-67ccaa54bc05",
                        "expression": {
                            "type": "PQL",
                            "format": "pql/json",
                            "value": "{PQL_EXPRESSION}"
                        },
                        "mergePolicyId": "b83185bb-0bc6-489c-9363-0075eb30b4c8",
                        "mergePolicy": {
                            "id": "b83185bb-0bc6-489c-9363-0075eb30b4c8",
                            "version": 1
                        }
                    }
                }
            ],
            "updateTime": 1573204395000,
            "creationTime": 1573203600535,
            "updateEpoch": 1573204395
        }
    }
}
```

| 屬性 | 說明 |
| -------- | ----------- |
| `id` | 系統產生的區段作業唯讀識別碼。 |
| `status` | 區段工作的目前狀態。 狀態的潛在值包括「新」、「處理」、「取消」、「已取消」、「失敗」和「成功」。 |
| `segments` | 包含區段工作中傳回之區段定義資訊的物件。 |
| `segments.segment.id` | 區段定義的ID。 |
| `segments.segment.expression` | 包含有關段定義表達式的資訊的對象，用PQL編寫。 |

## 取消或刪除特定區段工作 {#delete}

您可以對端點進行DELETE請求，並在請求路徑中提供 `/segment/jobs` 您要刪除的區段作業ID，以刪除特定的區段作業。

>[!NOTE]
>
>API會立即回應刪除請求。 但是，實際刪除區段作業是非同步的。 換言之，對區段工作提出刪除要求與套用刪除要求之間有時差。

**API格式**

```http
DELETE /segment/jobs/{SEGMENT_JOB_ID}
```

| 屬性 | 說明 |
| -------- | ----------- | 
| `{SEGMENT_JOB_ID}` | 您 `id` 要刪除的區段工作值。 |

**請求**

```shell
curl -X DELETE https://platform.adobe.io/data/core/ups/segment/jobs/d3b4a50d-dfea-43eb-9fca-557ea53771fd \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應會傳回HTTP狀態204，並包含下列資訊。

```json
{
    "status": true,
    "message": "Segment job with id 'd3b4a50d-dfea-43eb-9fca-557ea53771fd' has been marked for cancelling"
}
```

## 後續步驟

閱讀本指南後，您現在可以深入瞭解細分工作的運作方式。