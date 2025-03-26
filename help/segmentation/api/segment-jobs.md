---
solution: Experience Platform
title: 區段作業API端點
description: Adobe Experience Platform Segmentation Service API中的區段作業端點可讓您以程式設計方式管理組織的區段作業。
role: Developer
exl-id: 105481c2-1c25-4f0e-8fb0-c6577a4616b3
source-git-commit: 9eb5ccc24db58a887473f61c66a83aa92e16efa7
workflow-type: tm+mt
source-wordcount: '1232'
ht-degree: 2%

---

# 區段作業端點

區段作業為非同步程式，可依需求建立對象區段。 它參考[區段定義](./segment-definitions.md)，以及任何[合併原則](../../profile/api/merge-policies.md)，可控制[!DNL Real-Time Customer Profile]如何在您的設定檔片段中合併重疊的屬性。 當區段作業成功完成時，您可以收集關於區段的各種資訊，例如處理期間可能發生的任何錯誤以及您的對象的最終規模。

本指南提供的資訊可協助您更清楚瞭解區段作業，並提供使用API執行基本動作的範例API呼叫。

## 快速入門

本指南中使用的端點是[!DNL Adobe Experience Platform Segmentation Service] API的一部分。 繼續之前，請檢閱[快速入門手冊](./getting-started.md)以取得您成功呼叫API所需瞭解的重要資訊，包括必要的標頭以及如何讀取範例API呼叫。

## 擷取區段作業清單 {#retrieve-list}

您可以向`/segment/jobs`端點發出GET要求，以擷取貴組織的所有區段工作清單。

**API格式**

`/segment/jobs`端點支援數個查詢引數，以協助篩選結果。 雖然這些引數是選用的，但強烈建議使用這些引數來協助減少昂貴的額外負荷。 在不使用引數的情況下呼叫此端點將會擷取您的組織可用的所有匯出作業。 可以包含多個引數，以&amp;符號(`&`)分隔。

```http
GET /segment/jobs
GET /segment/jobs?{QUERY_PARAMETERS}
```

**查詢引數**

+++ 可用查詢引數的清單。

| 參數 | 說明 | 範例 |
| --------- | ----------- | ------- |
| `start` | 指定傳回之區段作業的開始位移。 | `start=1` |
| `limit` | 指定每頁傳回的區段工作數。 | `limit=20` |
| `status` | 根據狀態篩選結果。 支援的值為NEW、QUEUED、PROCESSING、SUCCEEDED、FAILED、CANCELING、CANCELED | `status=NEW` |
| `sort` | 已傳回區段作業的訂單。 是以`[attributeName]:[desc|asc]`格式撰寫。 | `sort=creationTime:desc` |
| `property` | 篩選區段作業，並取得指定篩選器的完全相符專案。 它可採用下列其中一種格式撰寫： <ul><li>`[jsonObjectPath]==[value]` — 篩選物件金鑰</li><li>`[arrayTypeAttributeName]~[objectKey]==[value]` — 在陣列中篩選</li></ul> | `property=segments~segmentId==workInUS` |

+++

**要求**

+++ 檢視區段作業清單的範例請求。

```shell
curl -X GET https://platform.adobe.io/data/core/ups/segment/jobs?status=SUCCEEDED \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**回應**

成功的回應會傳回HTTP狀態200，其中包含指定組織的區段作業清單，格式為JSON。 所有區段定義的完整清單將顯示在`children.segments`屬性中。

>[!NOTE]
>
>下列回應已因空間而截斷，且僅會顯示第一個傳回的工作。

+++ 擷取區段作業清單時的範例回應。

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
                        "mergePolicyId": "25c548a0-ca7f-4dcd-81d5-997642f178b9",
                        "mergePolicy": {
                            "id": "25c548a0-ca7f-4dcd-81d5-997642f178b9",
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
                "totalProfiles":13146432,
                "segmentedProfileCounter":{
                    "94509dba-7387-452f-addc-5d8d979f6ae8":1033
                },
                "segmentedProfileByNamespaceCounter":{
                    "94509dba-7387-452f-addc-5d8d979f6ae8":{
                        "tenantiduserobjid":1033,
                        "campaign_profile_mscom_mkt_prod2":1033
                    }
                },
                "segmentedProfileByStatusCounter":{
                    "94509dba-7387-452f-addc-5d8d979f6ae8":{
                        "exited":144646,
                        "realized":2056
                    }
                },
                "totalProfilesByMergePolicy":{
                    "25c548a0-ca7f-4dcd-81d5-997642f178b9":13146432
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
| `id` | 區段作業的系統產生唯讀識別碼。 |
| `status` | 區塊作業的目前狀態。 狀態的潛在值包括「NEW」、「PROCESSING」、「CANCELING」、「CANCELLED」、「FAILED」和「SUCCEEDED」。 |
| `segments` | 此物件包含區段作業中傳回之區段定義的相關資訊。 |
| `segments.segment.id` | 區段定義的ID。 |
| `segments.segment.expression` | 一個物件，包含有關在PQL中寫入的區段定義運算式的資訊。 |
| `metrics` | 包含區段作業之診斷資訊的物件。 |
| `metrics.totalTime` | 一個物件，包含細分工作開始和結束的時間以及花費的總時間資訊。 |
| `metrics.profileSegmentationTime` | 一個物件，包含區段評估開始和結束的時間以及花費的總時間資訊。 |
| `metrics.segmentProfileCounter` | 每個區段限定的設定檔數。 |
| `metrics.segmentedProfileByNamespaceCounter` | 以每個區段定義為基礎，適用於每個身分名稱空間的設定檔數。 |
| `metrics.segmentProfileByStatusCounter` | 每個狀態的設定檔計數。 支援下列三種狀態： <ul><li>「已實現」 — 符合區段定義的設定檔數。</li><li>「已退出」 — 區段定義中不再存在的設定檔數。</li></ul> |
| `metrics.totalProfilesByMergePolicy` | 根據合併原則合併的設定檔總數。 |

+++

## 建立新的區段工作 {#create}

您可以對`/segment/jobs`端點發出POST要求，並在要求內文中包含區段定義的ID，藉此建立新的區段作業。

**API格式**

```http
POST /segment/jobs
```

**要求**

+++建立新區段作業的範例請求

```shell
curl -X POST https://platform.adobe.io/data/core/ups/segment/jobs \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '[
    {
        "segmentId": "7863c010-e092-41c8-ae5e-9e533186752e"
    },
    {
        "segmentId": "07d39471-05d1-4083-a310-d96978fd7c85"
    }
 ]'
```

| 屬性 | 說明 |
| -------- | ----------- |
| `segmentId` | 您要評估之區段定義的ID。 這些區段定義可屬於不同的合併原則。 如需區段定義的詳細資訊，請參閱[區段定義端點指南](./segment-definitions.md)。 |

+++

**回應**

成功的回應會傳回HTTP狀態200，其中包含您新建立區段作業的相關資訊。

+++ 建立新區段作業時的範例回應。

```json
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
    "status": "PROCESSING",
    "batchId": "678f53bc-e21d-4c47-a7ec-5ad0064f8e4c",
    "computeJobId": 8811,
    "computeGatewayJobId": "9ea97b25-a0f5-410e-ae87-b2d85e58f399",
    "segments": [
        {
            "segmentId": "7863c010-e092-41c8-ae5e-9e533186752e",
            "segment": {
                "id": "7863c010-e092-41c8-ae5e-9e533186752e",
                "expression": {
                    "type": "PQL",
                    "format": "pql/json",
                    "value": "workAddress.country = \"US\""
                },
                "mergePolicyId": "25c548a0-ca7f-4dcd-81d5-997642f178b9",
                "mergePolicy": {
                    "id": "25c548a0-ca7f-4dcd-81d5-997642f178b9",
                    "version": 1
                }
            }
        },
        {
            "segmentId": "07d39471-05d1-4083-a310-d96978fd7c85",
            "segment": {
                "id": "07d39471-05d1-4083-a310-d96978fd7c85",
                "expression": {
                    "type": "PQL",
                    "format": "pql/json",
                    "value": "workAddress.country = \"US\""
                },
                "mergePolicyId": "25c548a0-ca7f-4dcd-81d5-997642f178b9",
                "mergePolicy": {
                    "id": "25c548a0-ca7f-4dcd-81d5-997642f178b9",
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
        "segmentedProfileCounter":{
            "7863c010-e092-41c8-ae5e-9e533186752e":1033
        },
        "segmentedProfileByNamespaceCounter":{
            "7863c010-e092-41c8-ae5e-9e533186752e":{
                "tenantiduserobjid":1033,
                "campaign_profile_mscom_mkt_prod2":1033
            }
        },
        "segmentedProfileByStatusCounter":{
            "7863c010-e092-41c8-ae5e-9e533186752e":{
                "exited":144646,
                "realized":2056
            }
        },
        "totalProfiles":13146432,
        "totalProfilesByMergePolicy":{
            "25c548a0-ca7f-4dcd-81d5-997642f178b9":13146432
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
```

| 屬性 | 說明 |
| -------- | ----------- |
| `id` | 新建立區段作業的系統產生唯讀識別碼。 |
| `status` | 區塊作業的目前狀態。 由於區段作業是新建的，因此狀態將一律為「NEW」。 |
| `segments` | 一個物件，其中包含此區段工作執行的目標區段定義相關資訊。 |
| `segments.segment.id` | 您提供的區段定義的ID。 |
| `segments.segment.expression` | 一個物件，包含有關在PQL中寫入的區段定義運算式的資訊。 |

+++

## 擷取特定區段工作 {#get}

您可以向`/segment/jobs`端點發出GET請求，並提供您要在請求路徑中擷取之區段作業的ID，藉此擷取特定區段作業的詳細資訊。

**API格式**

```http
GET /segment/jobs/{SEGMENT_JOB_ID}
```

| 屬性 | 說明 |
| -------- | ----------- | 
| `{SEGMENT_JOB_ID}` | 您要擷取之區段作業的`id`值。 |

**要求**

+++ 擷取區段作業的範例要求。

```shell
curl -X GET https://platform.adobe.io/data/core/ups/segment/jobs/d3b4a50d-dfea-43eb-9fca-557ea53771fd \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**回應**

成功的回應會傳回HTTP狀態200，其中包含指定區段工作的詳細資訊。 所有區段定義的完整清單將顯示在`children.segments`屬性中。

+++ 擷取區段作業的範例回應。

```json
{
    "id": "d3b4a50d-dfea-43eb-9fca-557ea53771fd",
    "imsOrgId": "{ORG_ID}",
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
| `id` | 區段作業的系統產生唯讀識別碼。 |
| `status` | 區塊作業的目前狀態。 狀態的潛在值包括「NEW」、「PROCESSING」、「CANCELING」、「CANCELLED」、「FAILED」和「SUCCEEDED」。 |
| `segments` | 此物件包含區段作業中傳回之區段定義的相關資訊。 |
| `segments.segment.id` | 區段定義的ID。 |
| `segments.segment.expression` | 一個物件，包含有關在PQL中寫入的區段定義運算式的資訊。 |
| `metrics` | 包含區段作業之診斷資訊的物件。 |

+++

>[!ENDTABS]

## 大量擷取區段作業 {#bulk-get}

您可以對`/segment/jobs/bulk-get`端點發出POST要求，並在要求內文中提供區段作業的`id`值，以擷取有關多個區段作業的詳細資訊。

**API格式**

```http
POST /segment/jobs/bulk-get
```

**要求**

+++ 使用大量擷取端點的範例要求。

```shell
curl -X POST https://platform.adobe.io/data/core/ups/segment/jobs/bulk-get \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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

+++

**回應**

成功的回應會傳回HTTP狀態207以及請求的區段作業。

>[!NOTE]
>
>以下回應已截斷空間，僅顯示每個區段工作的部分詳細資訊。 完整回應將列出請求區段作業的完整詳細資料。

+++ 使用大量取得回應時的範例回應。

```json
{
    "results": {
        "cc3419d3-0389-47f1-b174-fead6b3c830d": {
            "id": "cc3419d3-0389-47f1-b174-fead6b3c830d",
            "imsOrgId": "{ORG_ID}",
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
            "imsOrgId": "{ORG_ID}",
            "status": "SUCCEEDED",
            "segments": [
                {
                    "segmentId": "30230300-d78c-48ad-8012-c5563a007069",
                    "segment": {
                        "id": "30230300-d78c-48ad-8012-c5563a007069",
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
| `id` | 區段作業的系統產生唯讀識別碼。 |
| `status` | 區塊作業的目前狀態。 狀態的潛在值包括「NEW」、「PROCESSING」、「CANCELING」、「CANCELLED」、「FAILED」和「SUCCEEDED」。 |
| `segments` | 此物件包含區段作業中傳回之區段定義的相關資訊。 |
| `segments.segment.id` | 區段定義的ID。 |
| `segments.segment.expression` | 一個物件，包含有關在PQL中寫入的區段定義運算式的資訊。 |

+++

## 取消或刪除特定區段工作 {#delete}

您可以向`/segment/jobs`端點發出DELETE請求，並在請求路徑中提供您要刪除之區段作業的ID，藉此刪除特定區段作業。

>[!NOTE]
>
>對刪除請求的API回應是立即的。 然而，實際刪除區段作業為非同步。 換言之，對區段作業提出刪除請求與套用請求之間會存在時間差異。

**API格式**

```http
DELETE /segment/jobs/{SEGMENT_JOB_ID}
```

| 屬性 | 說明 |
| -------- | ----------- | 
| `{SEGMENT_JOB_ID}` | 您要刪除之區段作業的`id`值。 |

**要求**

+++ 刪除區段作業的範例請求。

```shell
curl -X DELETE https://platform.adobe.io/data/core/ups/segment/jobs/d3b4a50d-dfea-43eb-9fca-557ea53771fd \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**回應**

成功的回應會傳回HTTP狀態204和空白的回應本文。

## 後續步驟

閱讀本指南後，您現在已能更清楚瞭解區段工作的運作方式。
