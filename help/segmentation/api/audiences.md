---
keywords: Experience Platform；主題；熱門主題；分段；分段；分段服務；受眾；受眾；API;api;
title: 訪問群API終結點
topic-legacy: developer guide
description: Adobe Experience Platform分段服務API中的受眾終結點允許您以寫程式方式管理組織的受眾。
source-git-commit: 2a0c1f55115c541962f7bd3b7b11d367da50ff3b
workflow-type: tm+mt
source-wordcount: '1492'
ht-degree: 3%

---


# 受眾終結點

受眾是具有相似行為和/或特徵的人的集合。 這些人的集合可以通過使用Adobe Experience Platform或從外部來源生成。 您可以使用 `/audiences` 分段API中的端點，它允許您以寫程式方式檢索、建立、更新和刪除受眾。

## 快速入門

本指南中使用的端點是 [!DNL Adobe Experience Platform Segmentation Service] API。 在繼續之前，請查看 [入門指南](./getting-started.md) 要成功調用API，您需要瞭解的重要資訊，包括必需的標頭以及如何讀取示例API調用。

## 檢索受眾清單 {#list}

通過向組織發出GET請求，可以檢索組織的所有受眾清單 `/audiences` 端點。

**API格式**

的 `/audiences` 終結點支援多個查詢參數以幫助篩選結果。 雖然這些參數是可選的，但強烈建議使用它們以幫助減少列出資源時的昂貴開銷。 如果您在沒有參數的情況下調用此終結點，則將檢索組織的所有可用訪問群體。 可以包括多個參數，用和符號分隔(`&`)。

```http
GET /audiences
GET /audiences?{QUERY_PARAMETERS}
```

檢索訪問群體清單時可以使用以下查詢參數：

| 查詢參數 | 說明 | 範例 |
| --------------- | ----------- | ------- |
| `start` | 指定返回的受眾的起始偏移。 | `start=5` |
| `limit` | 指定每頁返回的最大訪問群體數。 | `limit=10` |
| `sort` | 指定結果排序依據的順序。 這是以格式寫的 `attributeName:[desc/asc]`。 | `sort=updateTime:desc` |
| `property` | 允許您指定受眾的篩選器 **正確** 匹配屬性的值。 這是以格式寫的 `property=` | `property=audienceId==test-audience-id` |
| `name` | 允許您指定其名稱的受眾的篩選器 **含** 提供的值。 此值不區分大小寫。 | `name=Sample` |
| `description` | 一個篩選器，允許您指定其說明的受眾 **含** 提供的值。 此值不區分大小寫。 | `description=Test Description` |
| `withMetrics` | 除訪問群體之外還返回度量的篩選器。 | `property=withMetrics==true` |

>[!IMPORTANT]
>
>對於受眾，在 `metrics` 屬性，並包含有關配置檔案計數、建立和更新時間戳的資訊。

**無度量**

在 `withMetrics` 查詢參數不存在。

**要求**

以下請求將檢索您組織中建立的最後五個受眾。

```shell
curl -X GET https: //platform.adobe.io/data/core/ups/audiences?limit=5 \
 -H 'Authorization:  Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id:  {IMS_ORG}' \
 -H 'x-api-key:  {API_KEY}' \
 -H 'x-sandbox-name:  {SANDBOX_NAME}'
```

**回應** {#no-metrics}

成功的響應返回HTTP狀態200，其中包含在您的組織中建立為JSON的受眾清單。

>[!NOTE]
>
>以下響應已被截斷為空間，並且僅顯示返回的第一個受眾。

```json
{
    "children": [
        {
            "id": "60ccea95-1435-4180-97a5-58af4aa285ab",
            "audienceId": "60ccea95-1435-4180-97a5-58af4aa285ab",
            "schema": {
                "name": "_xdm.context.profile"
            },
            "ttlInDays": 60,
            "profileInstanceId": "ups",
            "imsOrgId": "{ORG_ID}",
            "sandbox": {
                "sandboxId": "6ed34f6f-fe21-4a30-934f-6ffe21fa3075",
                "sandboxName": "prod",
                "type": "production",
                "default": true
            },
            "name": "People who ordered in the last 30 days",
            "description": "Last 30 days",
            "expression": {
                "type": "PQL",
                "format": "pql/text",
                "value": "workAddress.country = \"US\""
            },
            "mergePolicyId": "ef006bbe-750e-4e81-85f0-0c6902192dcc",
            "evaluationInfo": {
                "batch": {
                    "enabled": false
                },
                "continuous": {
                    "enabled": true
                },
                "synchronous": {
                    "enabled": false
                }
            },
            "dataGovernancePolicy": {
                "excludeOptOut": true
            },
            "isSystem": false,
            "creationTime": 1650374572000,
            "updateEpoch": 1650374573,
            "updateTime": 1650374573000,
            "createEpoch": 1650374572,
            "_etag": "\"33120d7c-0000-0200-0000-625eb7ad0000\"",
            "dependents": [],
            "definedOn": [
                {
                    "meta: resourceType": "unions",
                    "meta: containerId": "tenant",
                    "$ref": "https: //ns.adobe.com/xdm/context/profile__union"
                }
            ],
            "dependencies": [],
            "type": "SegmentDefinition",
            "overridePerformanceWarnings": false,
            "createdBy": "{CREATED_BY_ID}",
            "lifecycle": "published",
            "labels": [
                "core/C1"
            ],
            "namespace": "AEPSegments"
        }
    ]
}
```

| 屬性 | 受眾類型 | 說明 |
| -------- | ------------- | ----------- | 
| `id` | 兩者 | 系統生成的受眾的只讀標識符。 |
| `audienceId` | 兩者 | 如果受眾是平台生成的受眾，則此值與 `id`。 如果受眾是外部生成的，則此值由客戶端提供。 |
| `schema` | 兩者 | 受眾的體驗資料模型(XDM)架構。 |
| `imsOrgId` | 兩者 | 受眾所屬組織的ID。 |
| `sandbox` | 兩者 | 有關受眾所屬的沙盒的資訊。 有關沙箱的詳細資訊，請參閱 [箱概述](../../sandboxes/home.md)。 |
| `name` | 兩者 | 對象名稱。 |
| `description` | 兩者 | 受眾的描述。 |
| `expression` | 平台生成 | 訪問群體的配置檔案查詢語言(PQL)表達式。 有關PQL表達式的詳細資訊，請參閱 [PQL表達式指南](../pql/overview.md)。 |
| `mergePolicyId` | 平台生成 | 訪問群體所關聯的合併策略的ID。 有關合併策略的詳細資訊，請參閱 [合併策略指南](../../profile/api/merge-policies.md)。 |
| `evaluationInfo` | 平台生成 | 顯示如何評估受眾。 可能的評估方法包括批處理、流處理或邊緣處理。 有關評估方法的詳細資訊，請參閱 [分段概述](../home.md) |
| `dependents` | 兩者 | 取決於當前受眾的一系列受眾ID。 如果建立的受眾是段的段，則將使用此選項。 |
| `dependencies` | 兩者 | 受眾所依賴的受眾ID。 如果建立的受眾是段的段，則將使用此選項。 |
| `type` | 兩者 | 系統生成的欄位，顯示受眾是平台生成的還是外部生成的受眾。 可能的值包括 `SegmentDefinition` 和 `ExternalAudience`。 A `SegmentDefinition` 是指在平台中生成的受眾，而 `ExternalAudience` 是指未在平台中生成的受眾。 |
| `createdBy` | 兩者 | 建立訪問群體的用戶的ID。 |
| `labels` | 兩者 | 對象級資料使用和與受眾相關的基於屬性的訪問控制標籤。 |
| `namespace` | 兩者 | 訪問群體所屬的命名空間。 可能的值包括 `AAM`。 `AAMSegments`。 `AAMTraits`, `AEPSegments`。 |
| `audienceMeta` | 外部 | 從外部建立的受眾中外部建立的元資料。 |

**使用度量**

在 `withMetrics` 查詢參數存在。

**要求**

以下請求檢索在您的組織中建立的最後五個受眾（包括度量）。

```shell
curl -X GET https://platform.adobe.io/data/core/ups/audiences?propoerty=withMetrics==true&limit=5&sort=totalProfiles:desc \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的響應返回HTTP狀態200，其中包含指定組織的JSON訪問群體清單和度量。

>[!NOTE]
>
>以下響應已被截斷為空間，並且僅顯示返回的第一個受眾。

```json
{
    "children": [
        {
            "id": "60ccea95-1435-4180-97a5-58af4aa285ab",
            "audienceId": "60ccea95-1435-4180-97a5-58af4aa285ab",
            "schema": {
                "name": "_xdm.context.profile"
            },
            "ttlInDays": 60,
            "profileInstanceId": "ups",
            "imsOrgId": "{ORG_ID}",
            "sandbox": {
                "sandboxId": "6ed34f6f-fe21-4a30-934f-6ffe21fa3075",
                "sandboxName": "prod",
                "type": "production",
                "default": true
            },
            "isSystem": false,
            "name": "People who ordered in the last 30 days",
            "description": "Last 30 days",
            "expression": {
                "type": "PQL",
                "format": "pql/text",
                "value": "workAddress.country = \"US\""
            },
            "mergePolicyId": "ef006bbe-750e-4e81-85f0-0c6902192dcc",
            "evaluationInfo": {
                "batch": {
                    "enabled": false
                },
                "continuous": {
                    "enabled": true
                },
                "synchronous": {
                    "enabled": false
                }
            },
            "dataGovernancePolicy": {
                "excludeOptOut": true
            },
            "creationTime": 1650374572000,
            "updateEpoch": 1650374573,
            "updateTime": 1650374573000,
            "createEpoch": 1650374572,
            "_etag": "\"33120d7c-0000-0200-0000-625eb7ad0000\"",
            "dependents": [],
            "definedOn": [
                {
                    "meta: resourceType": "unions",
                    "meta: containerId": "tenant",
                    "$ref": "https: //ns.adobe.com/xdm/context/profile__union"
                }
            ],
            "dependencies": [],
            "metrics": {
                "type": "export",
                "jobId": "test-job-id",
                "id": "32a83b5d-a118-4bd6-b3cb-3aee2f4c30a1",
                "data": {
                    "totalProfiles": 11200769,
                    "totalProfilesByNamespace": {
                        "crmid": 11400769
                    },
                    "totalProfilesByStatus": {
                        "existing": 11400769
                    }
                },
                "createEpoch": 1653583927,
                "updateEpoch": 1653583927
            },
            "type": "SegmentDefinition",
            "overridePerformanceWarnings": false,
            "createdBy": "{CREATED_BY_ID}",
            "lifecycle": "published",
            "labels": [
                "core/C1"
            ],
            "namespace": "AEPSegments"
        }
   ],
   "_page": {
      "totalCount": 111,
      "pageSize": 5,
      "next": "1"
   },
   "_links": {
      "next": {
         "href": "@/audiences?start=1&limit=5&totalCount=111"
      }
   }
}
```

以下列出屬性 **獨佔** 到 `withMetrics` 回應。 如果您想瞭解標準受眾屬性，請閱讀 [上一節](#no-metrics)。

| 屬性 | 說明 |
| -------- | ----------- |
| `metrics.imsOrgId` | 受眾的組織ID。 |
| `metrics.sandbox` | 與受眾相關的沙盒資訊。 |
| `metrics.jobId` | 處理受眾的段作業的ID。 |
| `metrics.type` | 段作業類型。 這可以是 `export` 或 `batch_segmentation`。 |
| `metrics.id` | 觀眾的身份證。 |
| `metrics.data` | 與受眾相關的指標。 這包括以下資訊：包括在受眾中的配置檔案總數、基於每個命名空間的配置檔案總數以及基於每個狀態的配置檔案總數。 |
| `metrics.createEpoch` | 顯示建立訪問群體的時間戳。 |
| `metrics.updateEpoch` | 顯示上次更新訪問群體的時間的時間戳。 |

## 建立新受眾 {#create}

您可以通過向 `/audiences` 端點。

**API格式**

```http
POST /audiences
```

**要求**

```shell
curl -X POST https://platform.adobe.io/data/core/ups/audiences
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '{
        "name": "People who ordered in the last 30 days",
        "profileInstanceId": "ups",
        "description": "Last 30 days",
        "type": "SegmentDefinition",
        "expression": {
            "type": "PQL",
            "format": "pql/text",
            "value": "workAddress.country = \"US\""
        },
        "schema": {
            "name": "_xdm.context.profile"
        },
        "labels": [
          "core/C1"
        ]
    }'
```

| 屬性 | 說明 |
| -------- | ----------- | 
| `name` | 對象名稱。 |
| `description` | 受眾的描述。 |
| `type` | 顯示受眾是平台生成的受眾還是外部生成的受眾的欄位。 可能的值包括 `SegmentDefinition` 和 `ExternalAudience`。 A `SegmentDefinition` 是指在平台中生成的受眾，而 `ExternalAudience` 是指未在平台中生成的受眾。 |
| `expression` | 訪問群體的配置檔案查詢語言(PQL)表達式。 有關PQL表達式的詳細資訊，請參閱 [PQL表達式指南](../pql/overview.md)。 |
| `schema` | 受眾的體驗資料模型(XDM)架構。 |
| `labels` | 對象級資料使用和與受眾相關的基於屬性的訪問控制標籤。 |

**回應**

```json
{
    "id": "60ccea95-1435-4180-97a5-58af4aa285ab",
    "audienceId": "60ccea95-1435-4180-97a5-58af4aa285ab",
     "schema": {
      "name": "_xdm.context.profile"
    },
    "ttlInDays": 60,
    "profileInstanceId": "ups",
    "imsOrgId": "{ORG_ID}",
    "sandbox": {
        "sandboxId": "6ed34f6f-fe21-4a30-934f-6ffe21fa3075",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "isSystem":false,     
    "name": "People who ordered in the last 30 days",
    "description": "Last 30 days",
    "expression": {
        "type": "PQL",
        "format": "pql/text",
        "value": "workAddress.country = \"US\""
    },
    "mergePolicyId": "ef006bbe-750e-4e81-85f0-0c6902192dcc",
    "evaluationInfo": {
        "batch": {
          "enabled": false
        },
        "continuous": {
          "enabled": true
        },
        "synchronous": {
          "enabled": false
        }
    },
    "dataGovernancePolicy": {
      "excludeOptOut": true
    },
    "creationTime": 1650374572000,
    "updateEpoch": 1650374573,
    "updateTime": 1650374573000,
    "createEpoch": 1650374572,
    "_etag": "\"33120d7c-0000-0200-0000-625eb7ad0000\"",
    "dependents": [],
    "definedOn": [
        {
          "meta:resourceType": "unions",
          "meta:containerId": "tenant",
          "$ref": "https://ns.adobe.com/xdm/context/profile__union"
        }
    ],
    "dependencies": [],
    "type": "SegmentDefinition",
    "overridePerformanceWarnings": false,
    "createdBy": "{CREATED_BY_ID}",
    "lifecycle": "active",
    "labels": [
      "core/C1"
    ],
    "namespace": "AEPSegments"
}
```

## 查找指定的受眾 {#get}

您可以通過向以下站點發出GET請求來查找有關特定受眾的詳細資訊： `/audiences` 端點，並提供您希望在請求路徑中檢索的訪問群體的ID。

**API格式**

```http
GET /audiences/{AUDIENCE_ID}
GET /audiences/{AUDIENCE_ID}?property=withmetrics==true
```

| 參數 | 說明 |
| --------- | ----------- | 
| `{AUDIENCE_ID}` | 您嘗試檢索的受眾的ID。 |
| `property=withmetrics==true` | 如果要用受眾度量檢索指定的受眾，可以使用的可選查詢參數。 |

**要求**

```shell
curl -X GET https://platform.adobe.io/data/core/ups/audiences/60ccea95-1435-4180-97a5-58af4aa285ab \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的響應返回HTTP狀態200，其中包含有關指定受眾的資訊。 響應會因為受眾是Adobe Experience Platform或外部來源而不同。

**平台生成**

```json
{
    "id": "60ccea95-1435-4180-97a5-58af4aa285ab",
    "audienceId": "60ccea95-1435-4180-97a5-58af4aa285ab",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "ttlInDays": 60,
    "profileInstanceId": "ups",
    "imsOrgId": "{ORG_ID}",
    "sandbox": {
        "sandboxId": "6ed34f6f-fe21-4a30-934f-6ffe21fa3075",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "isSystem": false,
    "name": "People who ordered in the last 30 days",
    "description": "Last 30 days",
    "expression": {
        "type": "PQL",
        "format": "pql/text",
        "value": "workAddress.country = \"US\""
    },
    "mergePolicyId": "ef006bbe-750e-4e81-85f0-0c6902192dcc",
    "evaluationInfo": {
        "batch": {
            "enabled": false
        },
        "continuous": {
            "enabled": true
        },
        "synchronous": {
            "enabled": false
        }
    },
    "dataGovernancePolicy": {
        "excludeOptOut": true
    },
    "creationTime": 1650374572000,
    "updateEpoch": 1650374573,
    "updateTime": 1650374573000,
    "createEpoch": 1650374572,
    "_etag": "\"33120d7c-0000-0200-0000-625eb7ad0000\"",
    "dependents": [],
    "definedOn": [
        {
            "meta:resourceType": "unions",
            "meta:containerId": "tenant",
            "$ref": "https://ns.adobe.com/xdm/context/profile__union"
        }
    ],
    "dependencies": [],
    "type": "SegmentDefinition",
    "overridePerformanceWarnings": false,
    "createdBy": "{CREATED_BY_ID}",
    "lifecycle": "active",
    "labels": [
        "core/C1"
    ],
    "namespace": "AEPSegments"
}
```

**外部生成**

```json
{
    "id": "4afe34ae-8c98-4513-8a1d-67ccaa54bc05",
    "audienceId": "test-external-audience-id",
    "name": "externalSegment1",
    "namespace": "aam",
    "imsOrgId": "{ORG_ID}",
    "sandbox": {
        "sandboxId": "6ed34f6f-fe21-4a30-934f-6ffe21fa3075",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "isSystem":false,
    "description": "Last 30 days",
    "type": "ExternalSegment",
    "lifecycle": "active",
    "createdBy": "{CREATED_BY_ID}",
    "datasetId": "6254cf3c97f8e31b639fb14d",
    "labels": [
        "core/C1"
    ],
    "_etag": "\"f4102699-0000-0200-0000-625cd61a0000\"",
    "creationTime": 1650251290000,
    "updateEpoch": 1650251290,
    "updateTime": 1650251290000,
    "createEpoch": 1650251290
}
```

## 更新受眾中的欄位 {#update-field}

您可以通過向以下站點發出PATCH請求來更新特定受眾的欄位 `/audiences` 終結點，並提供您希望在請求路徑中更新的訪問群體的ID。

**API格式**

```http
PATCH /audiences/{AUDIENCE_ID}
```

| 參數 | 說明 |
| --------- | ----------- |
| `{AUDIENCE_ID}` | 要更新的受眾的ID。 |

**要求**

```shell
curl -X PATCH https://platform.adobe.io/data/core/ups/audiences/4afe34ae-8c98-4513-8a1d-67ccaa54bc05 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
     [
        {
            "op": "add",
            "path": "/expression",
            "value": {
                "type": "PQL",
                "format": "pql/text",
                "value": "workAddress.country = \"CA\""
            }
        }
      ]'
```

| 屬性 | 說明 |
| -------- | ----------- |
| `op` | 對於更新受眾，此值始終 `add`。 |
| `path` | 要更新的欄位的路徑。 |
| `value` | 要將欄位更新為的值。 |

**回應**

成功的響應返回HTTP狀態200，其中包含有關新更新的受眾的資訊。

```json
{
    "id": "60ccea95-1435-4180-97a5-58af4aa285ab",
    "audienceId": "60ccea95-1435-4180-97a5-58af4aa285ab",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "ttlInDays": 60,
    "profileInstanceId": "ups",
    "imsOrgId": "{ORG_ID}",
    "sandbox": {
        "sandboxId": "6ed34f6f-fe21-4a30-934f-6ffe21fa3075",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "name": "People who ordered in the last 30 days",
    "description": "Last 30 days",
    "expression": {
        "type": "PQL",
        "format": "pql/text",
        "value": "workAddress.country = \"CA\""
    },
    "mergePolicyId": "ef006bbe-750e-4e81-85f0-0c6902192dcc",
    "evaluationInfo": {
        "batch": {
          "enabled": false
        },
        "continuous": {
          "enabled": true
        },
        "synchronous": {
          "enabled": false
        }
    },
    "dataGovernancePolicy": {
      "excludeOptOut": true
    },
    "creationTime": 1650374572000,
    "updateEpoch": 1650374573,
    "updateTime": 1650374573000,
    "createEpoch": 1650374572,
    "_etag": "\"33120d7c-0000-0200-0000-625eb7ad0000\"",
    "dependents": [],
    "definedOn": [
        {
          "meta:resourceType": "unions",
          "meta:containerId": "tenant",
          "$ref": "https://ns.adobe.com/xdm/context/profile__union"
        }
    ],
    "dependencies": [],
    "type": "SegmentDefinition",
    "overridePerformanceWarnings": false,
    "createdBy": "{CREATED_BY_ID}",
    "lifecycle": "active",
    "labels": [
      "core/C1"
    ],
    "namespace": "AEPSegments"
}
```

## 更新受眾 {#put}

您可以通過向以下站點發出PUT請求來更新（覆蓋）特定受眾 `/audiences` 終結點，並提供您希望在請求路徑中更新的訪問群體的ID。

**API格式**

```http
PUT /audiences/{AUDIENCE_ID}
```

**要求**

```shell
curl -X PUT https://platform.adobe.io/data/core/ups/audiences/4afe34ae-8c98-4513-8a1d-67ccaa54bc05 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '{
    "audienceId":"test-external-audience-id",
    "name":"new externalSegment",
    "namespace":"aam",
    "description":"Last 30 days",
    "type":"ExternalSegment",
    "lifecycle":"published",
    "datasetId":"6254cf3c97f8e31b639fb14d",
    "labels":[
        "core/C1"
    ]
}' 
```

| 屬性 | 說明 |
| -------- | ----------- | 
| `audienceId` | 觀眾的ID。 外部受眾使用 |
| `name` | 對象名稱。 |
| `namespace` |  |
| `description` | 受眾的描述。 |
| `type` | 系統生成的欄位，顯示受眾是平台生成的還是外部生成的受眾。 可能的值包括 `SegmentDefinition` 和 `ExternalAudience`。 A `SegmentDefinition` 是指在平台中生成的受眾，而 `ExternalAudience` 是指未在平台中生成的受眾。 |
| `lifecycle` | 受眾的狀態。 可能的值包括 `draft`。 `published`。 `inactive`, `archived`。 `draft` 表示建立受眾時， `published` 當觀眾發表時， `inactive` 當觀眾不再活躍時， `archived` 的子菜單。 |
| `datasetId` | 可找到受眾資料的資料集的ID。 |
| `labels` | 對象級資料使用和與受眾相關的基於屬性的訪問控制標籤。 |

**回應**

成功的響應返回HTTP狀態200，並返回您最近更新的受眾的詳細資訊。 請注意，您的受眾的詳細資訊將因平台生成的受眾或外部生成的受眾而異。

```json
{
    "id": "4afe34ae-8c98-4513-8a1d-67ccaa54bc05",
    "audienceId": "test-external-audience-id",
    "name": "new externalSegment",
    "namespace": "aam",
    "imsOrgId": "{ORG_ID}",
    "sandbox": {
        "sandboxId": "6ed34f6f-fe21-4a30-934f-6ffe21fa3075",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "description": "Last 30 days",
    "type": "ExternalSegment",
    "lifecycle": "published",
    "createdBy": "{CREATED_BY_ID}",
    "datasetId": "6254cf3c97f8e31b639fb14d",
    "_etag": "\"f4102699-0000-0200-0000-625cd61a0000\"",
    "creationTime": 1650251290000,
    "updateEpoch": 1650251290,
    "updateTime": 1650251290000,
    "createEpoch": 1650251290
}
```

## 刪除受眾 {#delete}

您可以通過向DELETE請求刪除特定受眾 `/audiences` 終結點，並提供要在請求路徑中刪除的訪問群體的ID。

**API格式**

```http
DELETE /audiences/{AUDIENCE_ID}
```

| 參數 | 說明 |
| --------- | ----------- |
| `{AUDIENCE_ID}` | 要刪除的受眾的ID。 |

**要求**

```shell
curl -X DELETE https://platform.adobe.io/data/core/ups/audiences/60ccea95-1435-4180-97a5-58af4aa285ab5 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的響應返回HTTP狀態204，無消息。
