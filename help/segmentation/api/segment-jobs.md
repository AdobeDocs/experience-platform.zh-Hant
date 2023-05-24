---
keywords: Experience Platform；首頁；熱門主題；分段；分段；分段服務；分段作業；分段作業；API;api;
solution: Experience Platform
title: 段作業API終結點
description: Adobe Experience Platform分段服務API中的段作業終結點允許您以寫程式方式管理組織的段作業。
exl-id: 105481c2-1c25-4f0e-8fb0-c6577a4616b3
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '1497'
ht-degree: 2%

---

# 段作業終結點

段作業是一個非同步過程，可按需建立訪問群體段。 它引用 [段定義](./segment-definitions.md)，以及 [合併策略](../../profile/api/merge-policies.md) 控制方式 [!DNL Real-Time Customer Profile] 合併配置檔案片段中重疊的屬性。 當網段作業成功完成時，您可以收集有關網段的各種資訊，如處理過程中可能發生的任何錯誤以及受眾的最終大小。

本指南提供資訊以幫助您更好地瞭解段作業，並包括使用API執行基本操作的示例API調用。

## 快速入門

本指南中使用的端點是 [!DNL Adobe Experience Platform Segmentation Service] API。 在繼續之前，請查看 [入門指南](./getting-started.md) 要成功調用API，您需要瞭解的重要資訊，包括必需的標頭以及如何讀取示例API調用。

## 檢索段作業清單 {#retrieve-list}

您可以通過向以下站點發出GET請求來檢索組織的所有段作業清單 `/segment/jobs` 端點。

**API格式**

的 `/segment/jobs` 終結點支援多個查詢參數以幫助篩選結果。 雖然這些參數是可選的，但強烈建議使用它們以幫助降低昂貴的開銷。 調用此終結點時沒有參數將檢索組織可用的所有導出作業。 可以包括多個參數，用和符號分隔(`&`)。

```http
GET /segment/jobs
GET /segment/jobs?{QUERY_PARAMETERS}
```

**查詢參數**

| 參數 | 說明 | 範例 |
| --------- | ----------- | ------- |
| `start` | 指定返回的段作業的起始偏移。 | `start=1` |
| `limit` | 指定每頁返回的段作業數。 | `limit=20` |
| `status` | 根據狀態篩選結果。 支援的值為NEW、QUEUDED、PROCESSING、SUCCEEDED、FAILED、CANCELED、CANCELED | `status=NEW` |
| `sort` | 對返回的段作業進行訂單。 以格式寫入 `[attributeName]:[desc|asc]`。 | `sort=creationTime:desc` |
| `property` | 篩選器分段作業並獲取給定篩選器的準確匹配項。 它可以以下列格式之一寫入： <ul><li>`[jsonObjectPath]==[value]`  — 篩選對象鍵</li><li>`[arrayTypeAttributeName]~[objectKey]==[value]`  — 在陣列中篩選</li></ul> | `property=segments~segmentId==workInUS` |

**要求**

```shell
curl -X GET https://platform.adobe.io/data/core/ups/segment/jobs?status=SUCCEEDED \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的響應返回HTTP狀態200，其中指定組織的段作業清單為JSON。 但是，響應會因段任務中段數而不同。

**在段任務中小於或等於1500個段**

如果段作業中運行的段少於1500個，則所有段的完整清單將顯示在 `children.segments` 屬性。

>[!NOTE]
>
>以下響應已被截斷空間，將只顯示第一個返回的作業。

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

**超過1500個段**

如果段作業中運行的段數超過1500個， `children.segments` 顯示屬性 `*`，表示正在評估所有段。

>[!NOTE]
>
>以下響應已被截斷空間，將只顯示第一個返回的作業。

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
                    "segmentId": "*",
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
                "totalProfiles": 13146432,
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
| `id` | 段作業的系統生成的只讀標識符。 |
| `status` | 段任務的當前狀態。 狀態的潛在值包括「NEW」、「PROCESSING」、「CANCELLED」、「CANCELLED」、「FAILED」和「SUCCEEDED」。 |
| `segments` | 包含有關在段作業中返回的段定義的資訊的對象。 |
| `segments.segment.id` | 段定義的ID。 |
| `segments.segment.expression` | 包含有關段定義表達式的資訊的對象，用PQL編寫。 |
| `metrics` | 包含有關段作業的診斷資訊的對象。 |
| `metrics.totalTime` | 包含分段作業啟動和結束時間以及所用總時間的資訊的對象。 |
| `metrics.profileSegmentationTime` | 包含分段評估開始和結束的時間以及所用總時間的資訊的對象。 |
| `metrics.segmentProfileCounter` | 按段基準限定的配置檔案數。 |
| `metrics.segmentedProfileByNamespaceCounter` | 每個段上每個標識命名空間限定的配置檔案數。 |
| `metrics.segmentProfileByStatusCounter` | 每個狀態的配置檔案計數。 支援以下三種狀態： <ul><li>「已實現」 — 符合段條件的配置檔案數。</li><li>「已退出」 — 段中不再存在的配置檔案段數。</li></ul> |
| `metrics.totalProfilesByMergePolicy` | 每個合併策略的合併配置檔案總數。 |

## 建立新段任務 {#create}

您可以通過向以下站點發出POST請求來建立新段任務 `/segment/jobs` 端點，並在主體中包括要從中建立新受眾的段定義的ID。

**API格式**

```http
POST /segment/jobs
```

在建立新段任務時，請求和響應將因段任務中段的數量而不同。

**在段任務中小於或等於1500個段**

**要求**

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
    }
 ]'
```

| 屬性 | 說明 |
| -------- | ----------- |
| `segmentId` | 要為其建立段作業的段定義的ID。 這些段定義可以屬於不同的合併策略。 有關段定義的詳細資訊，請參閱 [段定義端點指南](./segment-definitions.md)。 |

**回應**

成功的響應返回HTTP狀態200，其中包含有關新建立的段作業的資訊。

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
| `id` | 新建立的段作業的系統生成的只讀標識符。 |
| `status` | 段任務的當前狀態。 由於段作業是新建立的，因此狀態始終為「NEW」。 |
| `segments` | 包含有關此段作業正為其運行的段定義的資訊的對象。 |
| `segments.segment.id` | 提供的段定義的ID。 |
| `segments.segment.expression` | 包含有關段定義表達式的資訊的對象，用PQL編寫。 |

**超過1500個段**

**要求**

>[!NOTE]
>
>雖然您可以建立具有1500個以上段的段任務，但是 **不推薦**。

```shell
curl -X POST https://platform.adobe.io/data/core/ups/segment/jobs \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '{
    "schema": {
        "name": "_xdm.context.profile"
    },
    "segments": [
        {
            "segmentId": "*"
        }
    ]
 }'
```

| 屬性 | 說明 |
| -------- | ----------- |
| `schema.name` | 段的架構名稱。 |
| `segments.segmentId` | 運行具有超過1500個段的段作業時，需要通過 `*` 作為段ID表示要運行具有所有段的分段作業。 |

**回應**

成功的響應返回HTTP狀態200，其中包含新建立的段作業的詳細資訊。

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
            "segmentId": "*"
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
| `id` | 新建立的段作業的系統生成的只讀標識符。 |
| `status` | 段任務的當前狀態。 由於段作業是新建立的，因此狀態將始終為 `NEW`。 |
| `segments` | 包含有關此段作業正為其運行的段定義的資訊的對象。 |
| `segments.segment.id` | 的 `*` 表示此段作業正在為組織內的所有段運行。 |

## 檢索特定段作業 {#get}

通過向Web站點發出GET請求，可檢索有關特定段作業的詳細資訊 `/segment/jobs` 端點，並提供要在請求路徑中檢索的段作業的ID。

**API格式**

```http
GET /segment/jobs/{SEGMENT_JOB_ID}
```

| 屬性 | 說明 |
| -------- | ----------- | 
| `{SEGMENT_JOB_ID}` | 的 `id` 要檢索的段作業的值。 |

**要求**

```shell
curl -X GET https://platform.adobe.io/data/core/ups/segment/jobs/d3b4a50d-dfea-43eb-9fca-557ea53771fd \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的響應返回HTTP狀態200，其中包含有關指定段作業的詳細資訊。  但是，響應會因段任務中段數而不同。

**在段任務中小於或等於1500個段**

如果段作業中運行的段少於1500個，則所有段的完整清單將顯示在 `children.segments` 屬性。

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

**超過1500個段**

如果段作業中運行的段數超過1500個， `children.segments` 顯示屬性 `*`，表示正在評估所有段。

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
    "status": "SUCCEEDED",
    "batchId": "678f53bc-e21d-4c47-a7ec-5ad0064f8e4c",
    "computeJobId": 8811,
    "computeGatewayJobId": "9ea97b25-a0f5-410e-ae87-b2d85e58f399",
    "segments": [
        {
            "segmentId": "*"
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
| `id` | 段作業的系統生成的只讀標識符。 |
| `status` | 段任務的當前狀態。 狀態的潛在值包括「NEW」、「PROCESSING」、「CANCELLED」、「CANCELLED」、「FAILED」和「SUCCEEDED」。 |
| `segments` | 包含有關在段作業中返回的段定義的資訊的對象。 |
| `segments.segment.id` | 段定義的ID。 |
| `segments.segment.expression` | 包含有關段定義表達式的資訊的對象，用PQL編寫。 |
| `metrics` | 包含有關段作業的診斷資訊的對象。 |

## 批量檢索段作業 {#bulk-get}

您可以通過向以下對象發出POST請求來檢索有關多個段作業的詳細資訊： `/segment/jobs/bulk-get` 端點和提供  `id` 請求正文中段作業的值。

**API格式**

```http
POST /segment/jobs/bulk-get
```

**要求**

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

**回應**

成功的響應將返回HTTP狀態207，並返回請求的段作業。 但是， `children.segments` 屬性不同，具體取決於段作業運行的段數是否超過1500個。

>[!NOTE]
>
>以下響應已被截斷，僅顯示每個段作業的部分詳細資訊。 完整響應將列出請求的段作業的完整詳細資訊。

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
                    "segmentId": "*"
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
| `id` | 段作業的系統生成的只讀標識符。 |
| `status` | 段任務的當前狀態。 狀態的潛在值包括「NEW」、「PROCESSING」、「CANCELLED」、「CANCELLED」、「FAILED」和「SUCCEEDED」。 |
| `segments` | 包含有關在段作業中返回的段定義的資訊的對象。 |
| `segments.segment.id` | 段定義的ID。 |
| `segments.segment.expression` | 包含有關段定義表達式的資訊的對象，用PQL編寫。 |

## 取消或刪除特定段作業 {#delete}

您可以通過向DELETE請求刪除特定段作業 `/segment/jobs` 端點，並提供要在請求路徑中刪除的段作業的ID。

>[!NOTE]
>
>對刪除請求的API響應是立即的。 但是，實際刪除段作業是非同步的。 換句話說，在對段作業發出刪除請求和應用刪除請求之間存在時間差。

**API格式**

```http
DELETE /segment/jobs/{SEGMENT_JOB_ID}
```

| 屬性 | 說明 |
| -------- | ----------- | 
| `{SEGMENT_JOB_ID}` | 的 `id` 要刪除的段作業的值。 |

**要求**

```shell
curl -X DELETE https://platform.adobe.io/data/core/ups/segment/jobs/d3b4a50d-dfea-43eb-9fca-557ea53771fd \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功響應返回HTTP狀態204，並返回以下資訊。

```json
{
    "status": true,
    "message": "Segment job with id 'd3b4a50d-dfea-43eb-9fca-557ea53771fd' has been marked for cancelling"
}
```

## 後續步驟

閱讀本指南後，您現在對細分工作的工作方式有了更深入的瞭解。
