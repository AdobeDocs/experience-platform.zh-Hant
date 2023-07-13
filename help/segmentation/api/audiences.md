---
title: Audiences API端點
description: 使用Adobe Experience Platform Segmentation Service API中的受眾端點，以程式設計方式建立、管理和更新您組織的受眾。
exl-id: cb1a46e5-3294-4db2-ad46-c5e45f48df15
source-git-commit: dbb7e0987521c7a2f6512f05eaa19e0121aa34c6
workflow-type: tm+mt
source-wordcount: '2124'
ht-degree: 3%

---

# 受眾端點

對象是具有相同類似行為和/或特徵的人集合。 這些人員集合可以使用Adobe Experience Platform或從外部來源產生。 您可以使用 `/audiences` 區段API中的端點，可讓您以程式設計方式擷取、建立、更新和刪除對象。

## 快速入門

本指南中使用的端點是 [!DNL Adobe Experience Platform Segmentation Service] API。 在繼續之前，請檢閱 [快速入門手冊](./getting-started.md) 如需成功呼叫API所需的重要資訊，包括必要的標頭及如何讀取範例API呼叫。

## 擷取對象清單 {#list}

您可以透過向以下網站發出GET請求，擷取貴組織的所有對象清單： `/audiences` 端點。

**API格式**

此 `/audiences` 端點支援數個查詢引數，以協助篩選結果。 雖然這些引數是選用的，但強烈建議使用這些引數，以幫助在列出資源時減少昂貴的額外負荷。 如果您在不使用引數的情況下呼叫此端點，則會擷取貴組織可用的所有對象。 可包含多個引數，以&amp;符號(`&`)。

```http
GET /audiences
GET /audiences?{QUERY_PARAMETERS}
```

擷取對象清單時，可使用下列查詢引數：

| 查詢參數 | 說明 | 範例 |
| --------------- | ----------- | ------- |
| `start` | 指定傳回對象的開始位移。 | `start=5` |
| `limit` | 指定每頁傳回的最大對象數。 | `limit=10` |
| `sort` | 指定排序結果的順序。 這會以格式撰寫 `attributeName:[desc/asc]`. | `sort=updateTime:desc` |
| `property` | 可讓您指定受眾的篩選器 **完全符合** 符合屬性的值。 這會以格式撰寫 `property=` | `property=audienceId==test-audience-id` |
| `name` | 可讓您指定名稱為的對象的篩選器 **contain** 提供的值。 此值不區分大小寫。 | `name=Sample` |
| `description` | 可讓您指定其說明的對象的篩選器 **contain** 提供的值。 此值不區分大小寫。 | `description=Test Description` |

**要求**

以下請求會擷取貴組織中建立的最後兩個對象。

+++擷取對象清單的範例要求。

```shell
curl -X GET https: //platform.adobe.io/data/core/ups/audiences?limit=2 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**回應**

成功的回應會傳回HTTP狀態200，其中包含您的組織中建立為JSON的對象清單。

+++包含屬於您組織的最後兩個建立對象的範例回應

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
            "originName": "REAL_TIME_CUSTOMER_PROFILE",
            "overridePerformanceWarnings": false,
            "createdBy": "{CREATED_BY_ID}",
            "lifecycleState": "published",
            "labels": [
                "core/C1"
            ],
            "namespace": "AEPSegments"
        },
        {
            "id": "32a83b5d-a118-4bd6-b3cb-3aee2f4c30a1",
            "audienceId": "test-external-audience-id",
            "name": "externalSegment1",
            "namespace": "aam",
            "imsOrgId": "{ORG_ID}",
            "sandbox":{
                "sandboxId": "6ed34f6f-fe21-4a30-934f-6ffe21fa3075",
                "sandboxName": "prod",
                "type": "production",
                "default": true
            },
            "isSystem": false,
            "description": "Last 30 days",
            "type": "ExternalSegment",
            "originName": "CUSTOM_UPLOAD",
            "lifecycleState": "published",
            "createdBy": "{CREATED_BY_ID}",
            "datasetId": "6254cf3c97f8e31b639fb14d",
            "labels":[
                "core/C1"
            ],
            "linkedAudienceRef": {
                "flowId": "4685ea90-d2b6-11ec-9d64-0242ac120002"
            },
            "creationTime": 1642745034000000,
            "updateEpoch": 1649926314,
            "updateTime": 1649926314000,
            "createEpoch": 1642745034
        }
    ],
    "_page":{
      "totalCount": 111,
      "pageSize": 2,
      "next": "1"
   },
   "_links":{
      "next":{
         "href":"@/audiences?start=1&limit=2&totalCount=111"
      }
   }
}
```

| 屬性 | 對象型別 | 說明 |
| -------- | ------------- | ----------- | 
| `id` | 兩者 | 系統產生的對象唯讀識別碼。 |
| `audienceId` | 兩者 | 如果對象是平台產生的對象，則此值與的值相同。 `id`. 如果對象是外部產生的，此值由使用者端提供。 |
| `schema` | 兩者 | 對象的Experience Data Model (XDM)結構描述。 |
| `imsOrgId` | 兩者 | 對象所屬組織的ID。 |
| `sandbox` | 兩者 | 受眾所屬沙箱的相關資訊。 有關沙箱的更多資訊可在以下網址找到： [沙箱總覽](../../sandboxes/home.md). |
| `name` | 兩者 | 對象名稱。 |
| `description` | 兩者 | 對象說明。 |
| `expression` | 平台產生 | 對象的設定檔查詢語言(PQL)運算式。 如需PQL運算式的詳細資訊，請參閱 [PQL運算式指南](../pql/overview.md). |
| `mergePolicyId` | 平台產生 | 與對象相關聯的合併原則ID。 有關合併原則的更多資訊可在以下網址找到： [合併原則指南](../../profile/api/merge-policies.md). |
| `evaluationInfo` | 平台產生 | 顯示評估對象的方式。 可能的評估方法包括批次、同步（串流）或連續（邊緣）。 有關評估方法的詳細資訊，請參閱 [區段概述](../home.md) |
| `dependents` | 兩者 | 相依於目前受眾的受眾ID陣列。 如果您建立的對象是區段的區段，則會使用此屬性。 |
| `dependencies` | 兩者 | 受眾相依的受眾ID陣列。 如果您建立的對象是區段的區段，則會使用此屬性。 |
| `type` | 兩者 | 系統產生的欄位，顯示對象是平台產生的還是外部產生的對象。 可能的值包括 `SegmentDefinition` 和 `ExternalSegment`. A `SegmentDefinition` 指在Platform中產生的對象，而 `ExternalSegment` 指不是在Platform中產生的對象。 |
| `originName` | 兩者 | 參照對象來源名稱的欄位。 對於平台產生的對象，此值將為 `REAL_TIME_CUSTOMER_PROFILE`. 若為在Audience Orchestration中產生的對象，此值將為 `AUDIENCE_ORCHESTRATION`. 若為在Adobe Audience Manager中產生的對象，此值將為 `AUDIENCE_MANAGER`. 對於其他外部產生的對象，此值將為 `CUSTOM_UPLOAD`. |
| `createdBy` | 兩者 | 建立受眾之使用者的ID。 |
| `labels` | 兩者 | 與對象相關的物件層級資料使用情況和屬性型存取控制標籤。 |
| `namespace` | 兩者 | 對象所屬的名稱空間。 可能的值包括 `AAM`， `AAMSegments`， `AAMTraits`、和 `AEPSegments`. |
| `linkedAudienceRef` | 兩者 | 包含其他對象相關系統識別碼的物件。 |

+++

## 建立新受眾 {#create}

您可以透過向以下傳送POST請求來建立新受眾： `/audiences` 端點。

**API格式**

```http
POST /audiences
```

**要求**

>[!BEGINTABS]

>[!TAB 平台產生的對象]

+++ 用於建立平台產生受眾的範例請求

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
        ],
        "ttlInDays": 60
    }'
```

| 屬性 | 說明 |
| -------- | ----------- | 
| `name` | 對象名稱。 |
| `description` | 對象說明。 |
| `type` | 此欄位會顯示對象是平台產生的受眾，還是外部產生的受眾。 可能的值包括 `SegmentDefinition` 和 `ExternalSegment`. A `SegmentDefinition` 指在Platform中產生的對象，而 `ExternalSegment` 指不是在Platform中產生的對象。 |
| `expression` | 對象的設定檔查詢語言(PQL)運算式。 如需PQL運算式的詳細資訊，請參閱 [PQL運算式指南](../pql/overview.md). |
| `schema` | 對象的Experience Data Model (XDM)結構描述。 |
| `labels` | 與對象相關的物件層級資料使用情況和屬性型存取控制標籤。 |
| `ttlInDays` | 代表對象的資料到期值（以天為單位）。 |

+++

>[!TAB 外部產生的對象]

+++ 建立外部產生對象的範例請求

```shell
curl -X POST https://platform.adobe.io/data/core/ups/audiences
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '{
        "audienceId":"test-external-audience-id",
        "name":"externalAudience",
        "namespace":"aam",
        "description":"Last 30 days",
        "type":"ExternalSegment",
        "originName":"CUSTOM_UPLOAD",
        "lifecycleState":"published",
        "datasetId":"6254cf3c97f8e31b639fb14d",
        "labels":[
            "core/C1"
        ],
        "linkedAudienceRef":{
            "flowId": "4685ea90-d2b6-11ec-9d64-0242ac120002"
        }
    }'
```

| 屬性 | 說明 |
| -------- | ----------- | 
| `audienceId` | 使用者提供給對象的ID。 |
| `name` | 對象名稱。 |
| `namespace` | 對象的名稱空間。 |
| `description` | 對象說明。 |
| `type` | 此欄位會顯示對象是平台產生的受眾，還是外部產生的受眾。 可能的值包括 `SegmentDefinition` 和 `ExternalSegment`. A `SegmentDefinition` 指在Platform中產生的對象，而 `ExternalSegment` 指不是在Platform中產生的對象。 |
| `originName` | 對象來源的名稱。 對於外部產生的對象，其預設值為 `CUSTOM_UPLOAD`. 其他支援的值包括 `REAL_TIME_CUSTOMER_PROFILE`， `CUSTOM_UPLOAD`， `AUDIENCE_ORCHESTRATION`、和 `AUDIENCE_MATCH`. |
| `lifecycleState` | 選擇性欄位，可決定您嘗試建立的對象初始狀態。 支援的值包括 `draft`， `published`、和 `inactive`. |
| `datasetId` | 資料集的ID，您可以在其中找到組成對象的資料。 |
| `labels` | 與對象相關的物件層級資料使用情況和屬性型存取控制標籤。 |
| `audienceMeta` | 屬於外部產生對象的中繼資料。 |
| `linkedAudienceRef` | 包含其他對象相關系統識別碼的物件。 其中可能包括： <ul><li>`flowId`：此ID可用來將受眾連線至用來匯入受眾資料的資料流。 如需有關所需ID的詳細資訊，請參閱 [建立資料流指南](../../sources/tutorials/api/collect/cloud-storage.md).</li><li>`aoWorkflowId`：此ID可用來將受眾連結至相關的Audience Orchestration構成。&lt;/li/> <li>`payloadFieldGroupRef`：此ID用於參照描述對象結構的XDM欄位群組結構描述。 有關此欄位值的詳細資訊，請參閱 [XDM欄位群組端點指南](../../xdm/api/field-groups.md).</li><li>`audienceFolderId`：此ID是用來參考Adobe Audience Manager中對象的資料夾ID。 有關此API的更多資訊可在以下網址找到： [Adobe Audience Manager API指南](https://bank.demdex.com/portal/swagger/index.html#/Segment%20Folder%20API).</ul> |

+++

>[!ENDTABS]

**回應**

成功的回應會傳回HTTP狀態200，其中包含您新建立受眾的相關資訊。

>[!BEGINTABS]

>[!TAB 平台產生的對象]

+++建立Platform產生的對象時的範例回應。

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
    "originName": "REAL_TIME_CUSTOMER_PROFILE",
    "overridePerformanceWarnings": false,
    "createdBy": "{CREATED_BY_ID}",
    "lifecycleState": "active",
    "labels": [
      "core/C1"
    ],
    "namespace": "AEPSegments"
}
```

+++

>[!TAB 外部產生的對象]

+++建立外部產生對象時的範例回應。

```json
{
   "id": "322f9f62-cd27-11ec-9d64-0242ac120002",
   "audienceId": "test-external-audience-id",
   "name": "externalAudience",
   "namespace": "aam",
   "imsOrgId": "{ORG_ID}",
   "sandbox":{
      "sandboxId": "6ed34f6f-fe21-4a30-934f-6ffe21fa3075",
      "sandboxName": "prod",
      "type": "production",
      "default": true
   },
   "isSystem": false,
   "description": "Last 30 days",
   "type": "ExternalSegment",
   "originName": "CUSTOM_UPLOAD",
   "lifecycleState": "published",
   "createdBy": "{CREATED_BY_ID}",
   "datasetId": "6254cf3c97f8e31b639fb14d",
   "labels": [
      "core/C1"
   ],
   "linkedAudienceRef": {
      "flowId": "4685ea90-d2b6-11ec-9d64-0242ac120002"
   },
   "_etag": "\"f4102699-0000-0200-0000-625cd61a0000\"",
   "creationTime": 1650251290000,
   "updateEpoch": 1650251290,
   "updateTime": 1650251290000,
   "createEpoch": 1650251290
}
```

+++

## 查詢指定的對象 {#get}

您可以透過向以下網站發出GET要求，查詢有關特定對象的詳細資訊： `/audiences` 端點，並提供您想要在請求路徑中擷取之對象的ID。

**API格式**

```http
GET /audiences/{AUDIENCE_ID}
```

| 參數 | 說明 |
| --------- | ----------- | 
| `{AUDIENCE_ID}` | 您嘗試擷取的對象ID。 請注意，這是 `id` 欄位，而是 **not** 此 `audienceId` 欄位。 |

**要求**

+++擷取對象的範例要求

```shell
curl -X GET https://platform.adobe.io/data/core/ups/audiences/60ccea95-1435-4180-97a5-58af4aa285ab \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**回應**

成功的回應會傳回HTTP狀態200，其中包含指定對象的資訊。 回應將因對象是使用Adobe Experience Platform還是外部來源產生而異。

>[!BEGINTABS]

>[!TAB 平台產生的對象]

+++擷取平台產生的對象時的範例回應。

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
    "lifecycleState": "active",
    "labels": [
        "core/C1"
    ],
    "namespace": "AEPSegments"
}
```

+++

>[!TAB 外部產生的對象]

+++擷取外部產生的對象時的範例回應。

```json
{
    "id": "60ccea95-1435-4180-97a5-58af4aa285ab",
    "audienceId": "test-external-audience-id",
    "name": "externalAudience",
    "namespace": "aam",
    "imsOrgId": "{ORG_ID}",
    "sandbox": {
        "sandboxId": "6ed34f6f-fe21-4a30-934f-6ffe21fa3075",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "isSystem": false,
    "description": "Last 30 days",
    "type": "ExternalSegment",
    "lifecycleState": "active",
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

+++

>[!ENDTABS]

## 更新對象中的欄位 {#update-field}

您可以透過向以下連結發出PATCH請求，更新特定對象的欄位： `/audiences` 端點，並在請求路徑中提供您要更新的對象ID。

**API格式**

```http
PATCH /audiences/{AUDIENCE_ID}
```

| 參數 | 說明 |
| --------- | ----------- |
| `{AUDIENCE_ID}` | 您要更新的對象ID。 請注意，這是 `id` 欄位，而是 **not** 此 `audienceId` 欄位。 |

**要求**

+++更新對象中欄位的範例請求。

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
| `op` | 若要更新對象，此值一律為 `add`. |
| `path` | 您要更新的欄位路徑。 |
| `value` | 您要更新欄位的值。 |

+++

**回應**

成功回應會傳回HTTP狀態200，其中包含您新更新對象的資訊。

+++更新對象中欄位時的範例回應。

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
    "lifecycleState": "active",
    "labels": [
      "core/C1"
    ],
    "namespace": "AEPSegments"
}
```

+++

## 更新對象 {#put}

您可以透過向以下專案發出PUT請求，更新（覆寫）特定對象： `/audiences` 端點，並在請求路徑中提供您要更新的對象ID。

**API格式**

```http
PUT /audiences/{AUDIENCE_ID}
```

| 參數 | 說明 |
| --------- | ----------- |
| `{AUDIENCE_ID}` | 您要更新的對象ID。 請注意，這是 `id` 欄位，而是 **not** 此 `audienceId` 欄位。 |

**要求**

+++更新整個對象的範例請求。

```shell
curl -X PUT https://platform.adobe.io/data/core/ups/audiences/4afe34ae-8c98-4513-8a1d-67ccaa54bc05 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '{
    "audienceId": "test-external-audience-id",
    "name": "New external audience",
    "namespace": "aam",
    "description": "Last 30 days",
    "type": "ExternalSegment",
    "lifecycleState": "published",
    "datasetId": "6254cf3c97f8e31b639fb14d",
    "labels": [
        "core/C1"
    ]
}' 
```

| 屬性 | 說明 |
| -------- | ----------- | 
| `audienceId` | 對象的ID。 對於外部產生的對象，此值可由使用者提供。 |
| `name` | 對象名稱。 |
| `namespace` | 對象的名稱空間。 |
| `description` | 對象說明。 |
| `type` | 系統產生的欄位，顯示對象是平台產生的還是外部產生的對象。 可能的值包括 `SegmentDefinition` 和 `ExternalSegment`. A `SegmentDefinition` 指在Platform中產生的對象，而 `ExternalSegment` 指不是在Platform中產生的對象。 |
| `lifecycleState` | 對象的狀態。 可能的值包括 `draft`， `published`、和 `inactive`. `draft` 代表建立對象的時間， `published` 發佈對象時，以及 `inactive` 對象不再作用中時。 |
| `datasetId` | 可找到對象資料的資料集ID。 |
| `labels` | 與對象相關的物件層級資料使用情況和屬性型存取控制標籤。 |

+++

**回應**

成功回應會傳回HTTP狀態200以及您新更新對象的詳細資料。 請注意，您的對象詳細資訊會因平台產生的對象或外部產生的對象而有所不同。

+++更新整個對象時的範例回應。

```json
{
    "id": "4afe34ae-8c98-4513-8a1d-67ccaa54bc05",
    "audienceId": "test-external-audience-id",
    "name": "New external audience",
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
    "lifecycleState": "published",
    "createdBy": "{CREATED_BY_ID}",
    "datasetId": "6254cf3c97f8e31b639fb14d",
    "_etag": "\"f4102699-0000-0200-0000-625cd61a0000\"",
    "creationTime": 1650251290000,
    "updateEpoch": 1650251290,
    "updateTime": 1650251290000,
    "createEpoch": 1650251290
}
```

+++

## 刪除對象 {#delete}

您可以透過向以下專案發出DELETE請求來刪除特定對象： `/audiences` 端點並在請求路徑中提供您要刪除之對象的ID。

**API格式**

```http
DELETE /audiences/{AUDIENCE_ID}
```

| 參數 | 說明 |
| --------- | ----------- |
| `{AUDIENCE_ID}` | 您要刪除的對象ID。 請注意，這是 `id` 欄位，而是 **not** 此 `audienceId` 欄位。 |

**要求**

+++ 刪除對象的範例請求。

```shell
curl -X DELETE https://platform.adobe.io/data/core/ups/audiences/60ccea95-1435-4180-97a5-58af4aa285ab5 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**回應**

成功的回應會傳回HTTP狀態204，但無訊息。

## 擷取多個對象 {#bulk-get}

您可以透過向以下專案發出POST請求來擷取多個對象： `/audiences/bulk-get` 端點，並提供您要擷取之對象的ID。

**API格式**

```http
POST /audiences/bulk-get
```

**要求**

+++ 擷取多個對象的範例要求。

```shell
curl -X POST https://platform.adobe.io/data/core/ups/audiences/bulk-get
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d ' {
    "ids": [
        {
            "id": "72c393ea-caed-441a-9eb6-5f66bb1bd6cd"
        },
        {
            "id": "QU9fLTEzOTgzNTE0MzY0NzY0NDg5NzkyOTkx_6ed34f6f-fe21-4a30-934f-6ffe21fa3075"
        }
    ]
 }
```

+++

**回應**

成功的回應會傳回HTTP狀態207，其中包含您所要求的對象資訊。

+++ 擷取多個對象時的範例回應。

```json
{
   "results":{
      "72c393ea-caed-441a-9eb6-5f66bb1bd6cd":{
         "id": "72c393ea-caed-441a-9eb6-5f66bb1bd6cd",
         "audienceId": "72c393ea-caed-441a-9eb6-5f66bb1bd6cd",
         "schema": {
            "name": "_xdm.context.profile"
         },
         "ttlInDays": 30,
         "imsOrgId": "{ORG_ID}",
         "sandbox": {
            "sandboxId": "6ed34f6f-fe21-4a30-934f-6ffe21fa3075",
            "sandboxName": "prod",
            "type": "production",
            "default": true
         },
         "name": "Sample audience",
         "expression": {
            "type": "pql",
            "format": "pql/text",
            "value": "_id = \"abc\""         
        },
         "mergePolicyId": "87c94d51-239c-4391-932c-29c2412100e5",
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
         "ansibleUiEnabled": false,
         "dataGovernancePolicy": {
            "excludeOptOut": true
         },
         "creationTime": 1623889553000000,
         "updateEpoch": 1674646369,
         "updateTime": 1674646369000,
         "createEpoch": 1623889552,
         "_etag": "\"61030ec7-0000-0200-0000-63d113610000\"",
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
         "state": "enabled",
         "overridePerformanceWarnings": false,
         "lastModifiedBy": "{CREATED_ID}",
         "lifecycleState": "published",
         "namespace": "AEPSegments",
         "isSystem": false,
         "saveSegmentMembership": true,
         "originName": "REAL_TIME_CUSTOMER_PROFILE"
      },
      "QU9fLTEzOTgzNTE0MzY0NzY0NDg5NzkyOTkx_6ed34f6f-fe21-4a30-934f-6ffe21fa3075":{
         "id": "QU9fLTEzOTgzNTE0MzY0NzY0NDg5NzkyOTkx_6ed34f6f-fe21-4a30-934f-6ffe21fa3075",
         "name": "label test24764489707692",
         "namespace": "AO",
         "imsOrgId": "{ORG_ID}",
         "sandbox":{
            "sandboxId": "6ed34f6f-fe21-4a30-934f-6ffe21fa3075",
            "sandboxName": "prod",
            "type": "production",
            "default": true
         },
         "type": "ExternalSegment",
         "lifecycleState": "published",
         "sourceId": "source-id",
         "createdBy": "{USER_ID}",
         "datasetId": "62bf31a105e9891b63525c92",
         "_etag": "\"3100da6d-0000-0200-0000-62bf31a10000\"",
         "creationTime": 1656697249000,
         "updateEpoch": 1656697249,
         "updateTime": 1656697249000,
         "createEpoch": 1656697249,
         "audienceId": "test-audience-id",
         "isSystem": false,
         "saveSegmentMembership": true,
         "linkedAudienceRef": {
            "aoWorkflowId": "62bf31858e87e34c8364befa"
         },
         "originName": "AUDIENCE_ORCHESTRATION"
      }
   }
}
```

+++

## 更新多個對象 {#bulk-patch}

您可以透過向以下網站發出POST請求，更新多個對象的設定檔和記錄計數： `/audiences/bulk-patch-metric` 端點，並提供您要更新的對象ID。

**API格式**

```http
POST /audiences/bulk-patch-metric
```

**要求**

+++ 更新多個對象的範例請求。

```shell
curl -X POST https://platform.adobe.io/data/core/ups/audiences/bulk-patch-metric
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d ' {
    "jobId": "12345",
    "jobType": "AO",
    "resources": [
        {
            "audienceId": "QUFNVHJhaXRzX2V4dGVybmFsU2VnbWVudC1hdWRpZW5jZS1pZA_6ed34f6f-fe21-4a30-934f-6ffe21fa3075",
            "namespace": "AAMTraits",
            "operations": [
                {
                    "op": "add",
                    "path": "/metrics/data",
                    "value": {
                        "totalProfiles": 11037
                    }
                },
            ]
        },
        {
            "audienceId": "QUFNVHJhaXRzX2V4dGVybmFsU2VnbWVudC1hdWRpZW5jZS1pZA_6ed34f6f-fe21-4a30-934f-6ffe21fa3075",
            "namespace": "AAMTraits",
            "operations": [
                {
                    "op": "add",
                    "path": "/metrics/data",
                    "value": {
                        "totalProfiles": 523
                    }
                }
            ]
        }
    ]
    }
```

<table>
<thead>
<tr>
<th>參數</th>
<th>說明</th>
</tr>
</thead>
<tbody>
<tr>
<td><code>jobId</code></td>
<td>將執行更新之工作的ID。</td>
</tr>
<tr>
<td><code>jobType</code></td>
<td>將執行更新的工作型別。 此值可以是 <code>export</code> 或 <code>AO</code>.</td>
</tr>
<tr>
<td><code>audienceId</code></td>
<td>您要更新的對象ID。 請注意，這是 <code>audienceId</code> 值，以及 <strong>not</strong> 此 <code>id</code> 對象的值。</td>
</tr>
<tr>
<td><code>namespace</code></td>
<td>您要更新的對象名稱空間。</td>
</tr>
<tr>
<td><code>operations</code></td>
<td>包含用來更新對象的資訊的物件。</td>
</tr>
<tr>
<td><code>operations.op</code></td>
<td>用於修補程式的作業。 更新多個對象時，此值為 <strong>一律</strong> <code>add</code>.</td>
</tr>
<tr>
<td><code>operations.path</code></td>
<td>要更新的欄位路徑。 目前僅支援兩個路徑： <code>/metrics/data</code> 當您更新 <strong>設定檔</strong> 計數和 <code>/recordMetrics/data</code> 當您更新 <strong>記錄</strong> 計數。</td>
</tr>
<tr>
<td><code>operations.value</code></td>
<td>
要更新的欄位值。 當您更新設定檔計數時，此值看起來會像這樣： 
<pre>
{ "totalProfiles"： 123456 }
</pre>
當您更新記錄計數時，此值看起來會像這樣： 
<pre>
{ "recordCount"： 123456 }
</pre>
</td>
</tr>
</tbody>
</table>

+++

**回應**

成功回應會傳回HTTP狀態207，其中包含有關已更新對象的詳細資訊。

+++ 更新多個對象的範例回應。

```json
{
   "resources":[
      {
         "audienceId":"QUFNVHJhaXRzX2V4dGVybmFsU2VnbWVudC1hdWRpZW5jZS1pZA_6ed34f6f-fe21-4a30-934f-6ffe21fa3075",

         "namespace": "AAMTraits",
         "status":200
      },
      {
         "audienceId":"QUFNVHJhaXRzX2V4dGVybmFsU2VnbWVudC1vcmlnaW4tdGVzdDE_6ed34f6f-fe21-4a30-934f-6ffe21fa3075",

         "namespace": "AAMTraits",
         "status":200
      }
   ]
}
```

| 參數 | 說明 |
| --------- | ----------- |
| `status` | 已更新對象的狀態。 如果傳回的狀態為200，表示對象已成功更新。 如果無法更新對象，則會傳回說明對象未更新的錯誤。 |

+++

## 後續步驟

閱讀本指南後，您現在已更瞭解如何使用Adobe Experience Platform API建立、管理和刪除對象。 如需使用UI進行對象管理的詳細資訊，請參閱 [分段UI指南](../ui/overview.md).
