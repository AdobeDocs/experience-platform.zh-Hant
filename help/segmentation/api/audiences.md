---
keywords: Experience Platform；首頁；熱門主題；分段；分段服務；對象；對象；API; API;
title: Audiences API端點
description: Adobe Experience Platform細分服務API中的受眾端點可讓您以程式設計方式管理貴組織的受眾。
exl-id: cb1a46e5-3294-4db2-ad46-c5e45f48df15
hide: true
hidefromtoc: true
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '1515'
ht-degree: 4%

---

# Audiences端點

>[!IMPORTANT]
>
>對象端點目前為測試版，不適用於所有使用者。 文件和功能可能會有所變更。

受眾是具有類似行為和/或特徵之人的集合。 這些人員集合可透過Adobe Experience Platform或外部來源產生。 您可以使用 `/audiences` 區段API中的端點，可讓您以程式設計方式擷取、建立、更新和刪除對象。

## 快速入門

本指南中使用的端點屬於 [!DNL Adobe Experience Platform Segmentation Service] API。 繼續之前，請檢閱 [快速入門手冊](./getting-started.md) 若要成功對API進行呼叫，您必須知道的重要資訊，包括必要的標題以及如何讀取範例API呼叫。

## 擷取對象清單 {#list}

您可以向 `/audiences` 端點。

**API格式**

此 `/audiences` 端點支援數個查詢參數，可協助篩選結果。 雖然這些參數為可選參數，但強烈建議使用這些參數，以在列出資源時幫助降低昂貴的開銷。 如果您在沒有參數的情況下呼叫此端點，則會擷取您組織的所有可用對象。 可包含多個參數，以&amp;符號分隔(`&`)。

```http
GET /audiences
GET /audiences?{QUERY_PARAMETERS}
```

擷取對象清單時，可使用下列查詢參數：

| 查詢參數 | 說明 | 範例 |
| --------------- | ----------- | ------- |
| `start` | 指定傳回對象的起始位移。 | `start=5` |
| `limit` | 指定每頁傳回的對象數上限。 | `limit=10` |
| `sort` | 指定結果排序依據的順序。 這是以格式撰寫 `attributeName:[desc/asc]`. | `sort=updateTime:desc` |
| `property` | 可讓您指定對象的篩選器 **恰好** 符合屬性的值。 這是以格式撰寫 `property=` | `property=audienceId==test-audience-id` |
| `name` | 可讓您指定其名稱的對象的篩選器 **cont** 提供的值。 此值不區分大小寫。 | `name=Sample` |
| `description` | 一種篩選器，可讓您指定其說明的對象 **cont** 提供的值。 此值不區分大小寫。 | `description=Test Description` |
| `withMetrics` | 除了對象外，還傳回量度的篩選器。 | `property=withMetrics==true` |

>[!IMPORTANT]
>
>若為對象，量度會在 `metrics` 屬性，並包含設定檔計數、建立和更新時間戳記的相關資訊。

**無量度**

下列請求/回應配對會在 `withMetrics` 查詢參數不存在。

**要求**

下列請求會擷取您組織中建立的最後五個對象。

```shell
curl -X GET https: //platform.adobe.io/data/core/ups/audiences?limit=5 \
 -H 'Authorization:  Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id:  {IMS_ORG}' \
 -H 'x-api-key:  {API_KEY}' \
 -H 'x-sandbox-name:  {SANDBOX_NAME}'
```

**回應** {#no-metrics}

成功的回應會傳回HTTP狀態200，以及貴組織中以JSON建立的對象清單。

>[!NOTE]
>
>下列回應已因空間而截斷，且只顯示傳回的第一個對象。

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

| 屬性 | 對象類型 | 說明 |
| -------- | ------------- | ----------- | 
| `id` | 兩者 | 對象的系統產生唯讀識別碼。 |
| `audienceId` | 兩者 | 如果對象是平台產生的對象，則此值與 `id`. 如果對象是外部產生的，則此值由用戶端提供。 |
| `schema` | 兩者 | 對象的體驗資料模型(XDM)結構。 |
| `imsOrgId` | 兩者 | 對象所屬組織的ID。 |
| `sandbox` | 兩者 | 對象所屬沙箱的相關資訊。 如需沙箱的詳細資訊，請參閱 [沙箱概述](../../sandboxes/home.md). |
| `name` | 兩者 | 對象名稱。 |
| `description` | 兩者 | 對象的說明。 |
| `expression` | 平台產生 | 對象的設定檔查詢語言(PQL)運算式。 有關PQL表達式的更多資訊，請參見 [PQL運算式指南](../pql/overview.md). |
| `mergePolicyId` | 平台產生 | 對象關聯的合併策略ID。 有關合併策略的詳細資訊，請參見 [合併策略指南](../../profile/api/merge-policies.md). |
| `evaluationInfo` | 平台產生 | 顯示如何評估對象。 可能的評估方法包括批次、串流或邊緣。 有關評估方法的詳細資訊，請參閱 [細分概述](../home.md) |
| `dependents` | 兩者 | 取決於目前受眾的受眾ID陣列。 如果您要建立屬於區段的對象，則會使用此選項。 |
| `dependencies` | 兩者 | 對象所仰賴的對象ID陣列。 如果您要建立屬於區段的對象，則會使用此選項。 |
| `type` | 兩者 | 系統產生的欄位，可顯示對象是平台產生的還是外部產生的對象。 可能的值包括 `SegmentDefinition` 和 `ExternalAudience`. A `SegmentDefinition` 是指在Platform中產生的對象，而 `ExternalAudience` 是指未在Platform中產生的對象。 |
| `createdBy` | 兩者 | 建立對象的使用者ID。 |
| `labels` | 兩者 | 與對象相關的物件層級資料使用方式和以屬性為基礎的存取控制標籤。 |
| `namespace` | 兩者 | 對象所屬的命名空間。 可能的值包括 `AAM`, `AAMSegments`, `AAMTraits`，和 `AEPSegments`. |
| `audienceMeta` | 外部 | 從外部建立的對象建立的中繼資料。 |

**使用量度**

下列請求/回應配對會在 `withMetrics` 查詢參數存在。

**要求**

下列請求會擷取您組織中建立的最後五個對象（含量度）。

```shell
curl -X GET https://platform.adobe.io/data/core/ups/audiences?propoerty=withMetrics==true&limit=5&sort=totalProfiles:desc \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應會傳回HTTP狀態200，其中包含指定組織的對象清單（連同量度），顯示為JSON。

>[!NOTE]
>
>下列回應已因空間而截斷，且只顯示傳回的第一個對象。

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

下列列出屬性 **專屬** 到 `withMetrics` 回應。 如果您想了解標準受眾屬性，請閱讀 [上一節](#no-metrics).

| 屬性 | 說明 |
| -------- | ----------- |
| `metrics.imsOrgId` | 對象的組織ID。 |
| `metrics.sandbox` | 與對象相關的沙箱資訊。 |
| `metrics.jobId` | 處理對象之區段工作的ID。 |
| `metrics.type` | 區段作業類型。 這可以是 `export` 或 `batch_segmentation`. |
| `metrics.id` | 對象的ID。 |
| `metrics.data` | 與對象相關的量度。 這包括對象中包含的設定檔總數、每個命名空間的設定檔總數，以及每個狀態的設定檔總數等資訊。 |
| `metrics.createEpoch` | 顯示對象建立時間的時間戳記。 |
| `metrics.updateEpoch` | 顯示對象上次更新時間的時間戳記。 |

## 建立新受眾 {#create}

您可以向 `/audiences` 端點。

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
| `description` | 對象的說明。 |
| `type` | 顯示對象是平台產生的還是外部產生的對象的欄位。 可能的值包括 `SegmentDefinition` 和 `ExternalAudience`. A `SegmentDefinition` 是指在Platform中產生的對象，而 `ExternalAudience` 是指未在Platform中產生的對象。 |
| `expression` | 對象的設定檔查詢語言(PQL)運算式。 有關PQL表達式的更多資訊，請參見 [PQL運算式指南](../pql/overview.md). |
| `schema` | 對象的體驗資料模型(XDM)結構。 |
| `labels` | 與對象相關的物件層級資料使用方式和以屬性為基礎的存取控制標籤。 |

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

## 查詢指定的對象 {#get}

您可以向提出GET要求，以尋找特定對象的詳細資訊 `/audiences` 端點，並提供您要在請求路徑中擷取之對象的ID。

**API格式**

```http
GET /audiences/{AUDIENCE_ID}
GET /audiences/{AUDIENCE_ID}?property=withmetrics==true
```

| 參數 | 說明 |
| --------- | ----------- | 
| `{AUDIENCE_ID}` | 您嘗試擷取的對象ID。 |
| `property=withmetrics==true` | 如果想使用對象量度擷取指定對象，可使用的選用查詢參數。 |

**要求**

```shell
curl -X GET https://platform.adobe.io/data/core/ups/audiences/60ccea95-1435-4180-97a5-58af4aa285ab \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應會傳回HTTP狀態200，並包含指定對象的相關資訊。 如果對象是使用Adobe Experience Platform或外部來源產生，回應會有所不同。

**平台產生**

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

## 更新對象中的欄位 {#update-field}

您可以向發出PATCH要求，以更新特定對象的欄位 `/audiences` 端點，並提供您要在請求路徑中更新之對象的ID。

**API格式**

```http
PATCH /audiences/{AUDIENCE_ID}
```

| 參數 | 說明 |
| --------- | ----------- |
| `{AUDIENCE_ID}` | 您要更新的對象ID。 |

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
| `op` | 若是更新對象，此值一律為 `add`. |
| `path` | 要更新的欄位路徑。 |
| `value` | 要將欄位更新為的值。 |

**回應**

成功的回應會傳回HTTP狀態200，並包含您新更新對象的相關資訊。

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

## 更新對象 {#put}

您可以向 `/audiences` 端點，並提供您要在請求路徑中更新之對象的ID。

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
| `audienceId` | 對象ID。 外部對象會使用此功能 |
| `name` | 對象名稱。 |
| `namespace` |  |
| `description` | 對象的說明。 |
| `type` | 系統產生的欄位，可顯示對象是平台產生的還是外部產生的對象。 可能的值包括 `SegmentDefinition` 和 `ExternalAudience`. A `SegmentDefinition` 是指在Platform中產生的對象，而 `ExternalAudience` 是指未在Platform中產生的對象。 |
| `lifecycle` | 對象的狀態。 可能的值包括 `draft`, `published`, `inactive`，和 `archived`. `draft` 代表建立對象時， `published` 發佈對象時， `inactive` 當對象不再作用中時， `archived` 如果對象已刪除。 |
| `datasetId` | 可找到對象資料的資料集ID。 |
| `labels` | 與對象相關的物件層級資料使用方式和以屬性為基礎的存取控制標籤。 |

**回應**

成功的回應會傳回HTTP狀態200，並包含您新更新對象的詳細資訊。 請注意，您的對象詳細資訊會因為是平台產生的對象或是外部產生的對象而有所不同。

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

## 刪除對象 {#delete}

您可以對 `/audiences` 端點，並在請求路徑中提供您要刪除之對象的ID。

**API格式**

```http
DELETE /audiences/{AUDIENCE_ID}
```

| 參數 | 說明 |
| --------- | ----------- |
| `{AUDIENCE_ID}` | 您要刪除的對象ID。 |

**要求**

```shell
curl -X DELETE https://platform.adobe.io/data/core/ups/audiences/60ccea95-1435-4180-97a5-58af4aa285ab5 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應會傳回HTTP狀態204，但沒有訊息。
