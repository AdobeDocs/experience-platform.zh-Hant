---
keywords: Experience Platform;profile;real-time customer profile;troubleshooting;API
solution: Adobe Experience Platform
title: 即時客戶個人檔案API開發人員指南
topic: guide
translation-type: tm+mt
source-git-commit: 21935bb36d8c2a0ef17e586c0909cf316ef026cf

---


# 合併原則

Adobe Experience Platform可讓您從多個來源匯整資料並加以匯整，以全面瞭解每個客戶。 將這些資料整合在一起時，合併原則是平台用來決定資料的優先順序以及將哪些資料合併以建立統一檢視的規則。 使用REST風格的API或用戶介面，您可以建立新的合併策略、管理現有策略，並為組織設定預設的合併策略。 本指南說明使用API處理合併原則的步驟。 要使用UI使用合併策略，請參閱合 [並策略使用手冊](../ui/merge-policies.md)。

## 快速入門

本指南中使用的API端點是即時客戶個人檔案API的一部分。 在繼續之前，請先閱讀 [即時客戶個人檔案API開發人員指南](getting-started.md)。 尤其是，「描述檔開 [發人員指南](getting-started.md#getting-started) 」的「快速入門」區段包含相關主題的連結、閱讀本檔案中範例API呼叫的指南，以及成功呼叫任何Experience Platform API所需之必要標題的重要資訊。

## 合併策略的元件 {#components-of-merge-policies}

合併原則是IMS組織專用的，可讓您建立不同的原則，以所需的特定方式合併結構。 任何存取描述檔資料的API都需要合併原則，但若未明確提供，則會使用預設原則。 平台提供預設的合併策略，或者，您可以為特定方案建立合併策略，並將其標籤為組織的預設策略。 每個組織可能每個方案有多個合併策略，但每個方案只能有一個預設的合併策略。 在提供方案名稱且需要但未提供合併策略的情況下，將使用任何設定為預設的合併策略集。 當您將合併策略設定為預設值時，任何先前設定為預設值的現有合併策略都將自動更新為不再用作預設值。

### 完整合併策略對象

完整的合併策略對象表示一組控制合併配置檔案片段的偏好。

**合併策略對象**

```json
    {
        "id": "{MERGE_POLICY_ID}",
        "name": "{NAME}",
        "imsOrgId": "{IMS_ORG}",
        "schema": {
            "name": "{SCHEMA_NAME}"
        },
        "version": 1,
        "identityGraph": {
            "type": "{IDENTITY_GRAPH_TYPE}"
        },
        "attributeMerge": {
            "type": "{ATTRIBUTE_MERGE_TYPE}"
        },
        "default": {BOOLEAN},
        "updateEpoch": {UPDATE_TIME}
    }
```

| 屬性 | 說明 |
|---|---|
| `id` | 系統生成在建立時分配的唯一標識符 |
| `name` | 可在清單檢視中識別合併原則的好記名稱。 |
| `imsOrgId` | 此合併策略所屬的組織ID |
| `identityGraph` | [標識圖對象](#identity-graph) ，指示將從中獲取相關標識的身份圖。 將合併所有相關身份的配置檔案片段。 |
| `attributeMerge` | [屬性合併](#attribute-merge) 對象，指示在發生資料衝突時合併策略優先配置檔案屬性值的方式。 |
| `schema` | 可 [以使用](#schema) 合併策略的方案對象。 |
| `default` | 指示此合併策略是否為指定方案的預設布爾值。 |
| `version` | 平台維護的合併原則版本。 每當合併策略更新時，此唯讀值都會增加。 |
| `updateEpoch` | 合併策略的上次更新日期。 |

**合併策略示例**

```json
    {
        "id": "10648288-cda5-11e8-a8d5-f2801f1b9fd1",
        "name": "profile-default",
        "imsOrgId": "{IMS_ORG}",
        "schema": {
            "name": "_xdm.context.profile"
        },
        "version": 1,
        "identityGraph": {
            "type": "none"
        },
        "attributeMerge": {
            "type": "timestampOrdered"
        },
        "default": true,
        "updateEpoch": 1551660639
    }
```

### 身分圖 {#identity-graph}

[Adobe Experience Platform Identity Service](../../identity-service/home.md) 管理Experience Platform上全球及每個組織使用的識別圖。 合併 `identityGraph` 策略的屬性定義了如何確定用戶的相關身份。

**identityGraph物件**

```json
    "identityGraph": {
        "type": "{IDENTITY_GRAPH_TYPE}"
    }
```

其中 `{IDENTITY_GRAPH_TYPE}` 是下列其中一項：

* **「無」:** 不執行身份聯繫。
* **「pdg」:** 根據您的個人身分圖表執行身分識別接合。

**範例`identityGraph`**

```json
    "identityGraph": {
        "type": "pdg"
    }
```

### 屬性合併 {#attribute-merge}

描述檔片段是特定使用者在身分清單中僅有一個身分的描述檔資訊。 當使用身份圖形類型導致多個身份時，配置檔案屬性和優先順序的值可能會發生衝突。 使用 `attributeMerge`時，您可以指定在發生合併衝突時要排定優先順序的資料集描述檔值。

**attributeMerge物件**

```json
    "attributeMerge": {
        "type": "{ATTRIBUTE_MERGE_TYPE}"
    }
```

其中 `{ATTRIBUTE_MERGE_TYPE}` 是下列其中一項：

* **&quot;timestampOrdered&quot;**:（預設值）優先處理在發生衝突時最後更新的描述檔。 使用此合併類型時， `data` 不需要屬性。
* **&quot;dataSetPrecerance&quot;** :根據個人資料片段的來源資料集，為描述檔片段提供優先順序。 當一個資料集中的資訊比另一個資料集的資料更偏好或受信任時，就可使用此功能。 使用此合併類型時，需 `order` 要屬性，因為它按優先順序順序列出資料集。
   * **「訂單」**:使用&quot;dataSetPrecense&quot;時，必須 `order` 向陣列提供資料集清單。 清單中未包含的任何資料集都不會合併。 換言之，必須明確列出資料集才能合併至描述檔。 陣 `order` 列按優先順序列出資料集的ID。

**使用dataSetPrecence類型的attributeMerge對象示例**

```json
    "attributeMerge": {
        "type": "dataSetPrecedence",
        "order" : [
            "dataSetId_2", 
            "dataSetId_3", 
            "dataSetId_1", 
            "dataSetId_4"
        ]
    }
```

**使用timestampOrdered類型的attributeMerge對象示例**

```json
    "attributeMerge": {
        "type": "timestampOrdered"
    }
```

### 架構 {#schema}

模式對象指定為此合併策略建立的XDM模式。

**`schema`物件&#x200B;**

```json
    "schema": {
        "name": "{SCHEMA_NAME}"
    }
```

其中的值 `name` 是與合併策略關聯的模式所基於的XDM類的名稱。

**範例`schema`**

```json
    "schema": {
        "name": "_xdm.context.profile"
    }
```

## 訪問合併策略 {#access-merge-policies}

使用即時客戶描述檔API，端點可讓您執行查閱請求，以依其ID檢視特定合併原則，或存取您IMS組織中所有依特定條件篩選的合併原則。 `/config/mergePolicies`

### 依ID存取單一合併原則

您可以透過單一合併原則的ID來存取，方法是向端點提出GET請求， `/config/mergePolicies` 並在請求路 `mergePolicyId` 徑中加入。

**API格式**

```http
GET /config/mergePolicies/{mergePolicyId}
```

| 參數 | 說明 |
|---|---|
| `{mergePolicyId}` | 要刪除的合併策略的標識符。 |

**請求**

```shell
curl -X GET \
  'https://platform.adobe.io/data/core/ups/config/mergePolicies/10648288-cda5-11e8-a8d5-f2801f1b9fd1' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}
```

**回應**

成功的回應會傳回合併原則的詳細資訊。

```json
{
    "id": "10648288-cda5-11e8-a8d5-f2801f1b9fd1",
    "imsOrgId": "{IMS_ORG}",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "version": 1,
    "identityGraph": {
        "type": "pdg"
    },
    "attributeMerge": {
        "type": "timestampOrdered"
    },
    "default": false,
    "updateEpoch": 1551127597
}
```

有關 [](#components-of-merge-policies) 組成合併策略的各個元素的詳細資訊，請參閱本文檔開頭的合併策略元件部分。

### 按標準列出多個合併策略

您可以在IMS組織內，透過向端點發出GET請求，並使用選用的查詢參數來篩選、排序和分頁回應，列出多個合併原則。 `/config/mergePolicies` 可包含多個參數，以&amp;符號分隔。 在沒有參數的情況下呼叫此端點將會擷取組織所有可用的合併原則。

**API格式**

```http
GET /config/mergePolicies?{QUERY_PARAMS}
```

| 參數 | 說明 |
|---|---|
| `default` | 一個布爾值，它根據合併策略是否是模式類的預設策略來過濾結果。 |
| `limit` | 指定頁面大小限制，以控制包含在頁面中的結果數。 預設值：20 |
| `orderBy` | 指定按照欄位對結果進行排序，或 `orderBy=name` 按名 `orderBy=+name` 稱按升序排序，或 `orderBy=-name`按降序排序。 省略此值會導致預設的遞增 `name` 順序排序。 |
| `schema.name` | 要為其檢索可用合併策略的方案的名稱。 |
| `identityGraph.type` | 依身分圖形類型篩選結果。 可能的值包括「無」和「pdg」（專用圖形）。 |
| `attributeMerge.type` | 依使用的屬性合併類型篩選結果。 可能的值包括&quot;timestampOrdered&quot;和&quot;dataSetPrecense&quot;。 |
| `start` | 頁面偏移——指定要擷取資料的起始ID。 預設值：0 |
| `version` | 如果您想要使用特定版本的合併原則，請指定此選項。 依預設，會使用最新版本。 |

有關、和的 `schema.name`詳 `identityGraph.type`細信 `attributeMerge.type`息，請參閱本指 [南前面提供的合併策略部分](#components-of-merge-policies) 。


**請求**

以下請求列出了給定方案的所有合併策略：

```shell
curl -X GET \
  'https://platform.adobe.io/data/core/ups/config/mergePolicies?schema.name=_xdm.context.profile' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}
```

**回應**

成功的回應會傳回符合請求中傳送之查詢參數所指定條件之合併原則的編頁清單。

```json
{
    "_page": {
        "totalCount": 2,
        "pageSize": 2
    },
    "children": [
        {
            "id": "0bf16e61-90e9-4204-b8fa-ad250360957b",
            "name": "Profile Default Merge Policy",
            "imsOrgId": "{IMS_ORG}",
            "sandbox": {
                "sandboxId": "ff0f6870-c46d-11e9-8ca3-036939a64204",
                "sandboxName": "prod",
                "type": "production",
                "default": true
            },
            "schema": {
                "name": "_xdm.context.profile"
            },
            "version": 1,
            "identityGraph": {
                "type": "none"
            },
            "attributeMerge": {
                "type": "timestampOrdered"
            },
            "default": true,
            "updateEpoch": 1552086578
        },
        {
            "id": "42d4a596-b1c6-46c0-994e-ca5ef1f85130",
            "name": "Dataset Precedence Merge Policy",
            "imsOrgId": "{IMS_ORG}",
            "sandbox": {
                "sandboxId": "ff0f6870-c46d-11e9-8ca3-036939a64204",
                "sandboxName": "prod",
                "type": "production",
                "default": true
            },
            "schema": {
                "name": "_xdm.context.profile"
            },
            "version": 1,
            "identityGraph": {
                "type": "pdg"
            },
            "attributeMerge": {
                "type": "dataSetPrecedence",
                "order": [
                    "5b76f86b85d0e00000be5c8b",
                    "5b76f8d787a6af01e2ceda18"
                ]
            },
            "default": false,
            "updateEpoch": 1576099719
        }
    ],
    "_links": {
        "next": {
            "href": "@/mergePolicies?start=K1JJRDpFaWc5QUpZWHY1c2JBQUFBQUFBQUFBPT0jUlQ6MSNUUkM6MiNGUEM6QWdFQUFBQldBQkVBQVBnaFFQLzM4VUIvL2tKQi8rLysvMUpBLzMrMi8wRkFmLzR4UUwvL0VrRC85em4zRTBEcmNmYi92Kzh4UUwvL05rQVgzRi8rMStqNS80WHQwN2NhUUVzQUFBUUFleGpLQ1JnVXRVcEFCQUFFQVBBRA==&orderBy=&limit=2"
        }
    }
}
```

| 屬性 | 說明 |
|---|---|
| `_links.next.href` | 下一頁結果的URI地址。 使用此URI作為另一個API呼叫的請求參數，以檢視頁面。 如果沒有下一頁，此值將是空字串。 |

## 建立合併策略

您可以向端點發出POST請求，為組織建立新的合併策 `/config/mergePolicies` 略。

**API格式**

```http
POST /config/mergePolicies
```

**請求**&#x200B;下列請求會建立新的合併原則，此原則由裝載中提供的屬性值設定：

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/config/mergePolicies \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
    "name": "Loyalty members ordered by ID",
    "identityGraph" : {
        "type": "none"
    },
    "attributeMerge" : {
        "type":"dataSetPrecedence",
        "order" : [
            "5b76f86b85d0e00000be5c8b",
            "5b76f8d787a6af01e2ceda18"
        ]
    },
    "schema": {
        "name":"_xdm.context.profile"
    },
    "default": true
}'
```

| 屬性 | 說明 |
|---|---|
| `name` | 可在清單檢視中識別合併原則的人性化名稱。 |
| `identityGraph.type` | 要從中獲取相關身份的身份圖類型。 可能的值：「無」或「pdg」（私用圖形）。 |
| `attributeMerge` | 在發生資料衝突時，設定描述檔屬性值優先順序的方式。 |
| `schema` | 與合併策略關聯的XDM模式類。 |
| `default` | 指定此合併策略是否為方案的預設策略。 |

有關詳細信 [息，請參閱合併策略](#components-of-merge-policies) 部分的元件。

**回應**

成功的回應會傳回新建立之合併原則的詳細資料。

```json
{
    "id": "e5bc94de-cd14-4cdf-a2bc-88b6e8cbfac2",
    "name": "Loyalty members ordered by ID",
    "imsOrgId": "{IMS_ORG}",
    "sandbox": {
        "sandboxId": "ff0f6870-c46d-11e9-8ca3-036939a64204",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "schema": {
        "name": "_xdm.context.profile"
    },
    "version": 1,
    "identityGraph": {
        "type": "none"
    },
    "attributeMerge": {
        "type": "dataSetPrecedence",
        "order": [
            "5b76f86b85d0e00000be5c8b",
            "5b76f8d787a6af01e2ceda18"
        ]
    },
    "default": true,
    "updateEpoch": 1551898378
}
```

有關 [](#components-of-merge-policies) 組成合併策略的各個元素的詳細資訊，請參閱本文檔開頭的合併策略元件部分。

## 更新合併策略 {#update}

通過編輯單個屬性(PATCH)或用新屬性(PUT)覆寫整個合併策略，可以修改現有的合併策略。 各示例如下所示。

### 編輯個別合併原則欄位

通過向端點發出PATCH請求，可以編輯合併策略的各個 `/config/mergePolicies/{mergePolicyId}` 欄位：

**API格式**

```http
PATCH /config/mergePolicies/{mergePolicyId}
```

| 參數 | 說明 |
|---|---|
| `{mergePolicyId}` | 要刪除的合併策略的標識符。 |

**請求**

下列請求會將其屬性的值變更為指定的合併 `default` 原則 `true`:

```shell
curl -X PATCH \
  https://platform.adobe.io/data/core/ups/config/mergePolicies/e5bc94de-cd14-4cdf-a2bc-88b6e8cbfac2 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
    "op": "add",
    "path": "/default",
    "value": "true"
  }'
```

| 屬性 | 說明 |
|---|---|
| `op` | 指定要執行的操作。 其他PATCH作業的範例可在 [JSON修補程式檔案中找到](http://jsonpatch.com) |
| `path` | 要更新的欄位路徑。 接受的值為：&quot;/name&quot;、&quot;/identityGraph.type&quot;、&quot;/attributeMerge.type&quot;、&quot;/schema.name&quot;、&quot;/version&quot;、&quot;/default&quot; |
| `value` | 將指定欄位設定為的值。 |

有關詳細信 [息，請參閱合併策略](#components-of-merge-policies) 部分的元件。


**回應**

成功的回應會傳回新更新的合併原則的詳細資料。

```json
{
    "id": "e5bc94de-cd14-4cdf-a2bc-88b6e8cbfac2",
    "name": "Loyalty members ordered by ID",
    "imsOrgId": "{IMS_ORG}",
    "sandbox": {
        "sandboxId": "ff0f6870-c46d-11e9-8ca3-036939a64204",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "schema": {
        "name": "_xdm.context.profile"
    },
    "version": 1,
    "identityGraph": {
        "type": "none"
    },
    "attributeMerge": {
        "type": "dataSetPrecedence",
        "order": [
            "5b76f86b85d0e00000be5c8b",
            "5b76f8d787a6af01e2ceda18"
        ]
    },
    "default": true,
    "updateEpoch": 1551898378
}
```

### 覆寫合併原則

修改合併策略的另一種方法是使用PUT請求，該請求覆蓋整個合併策略。

**API格式**

```http
PUT /config/mergePolicies/{mergePolicyId}
```

| 參數 | 說明 |
|---|---|
| `{mergePolicyId}` | 您要覆寫之合併原則的識別碼。 |

**請求**

下列請求會覆寫指定的合併原則，將其屬性值取代為裝載中提供的屬性值。 由於此請求完全替換了現有的合併策略，因此您必須提供最初定義合併策略時所需的所有相同欄位。 但是，這次您要為要變更的欄位提供更新值。

```shell
curl -X PUT \
  https://platform.adobe.io/data/core/ups/config/mergePolicies/e5bc94de-cd14-4cdf-a2bc-88b6e8cbfac2 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
        "name": "Loyalty members ordered by ID",
        "imsOrgId": "{IMS_ORG}",
        "schema": {
            "name": "_xdm.context.profile"
        },
        "version": 1,
        "identityGraph": {
            "type": "none"
        },
        "attributeMerge": {
            "type": "dataSetPrecedence",
            "order": [
                "5b76f86b85d0e00000be5c8b",
                "5b76f8d787a6af01e2ceda18"
            ]
        },
        "default": true,
        "updateEpoch": 1551898378
    }'
```

| 屬性 | 說明 |
|---|---|
| `name` | 可在清單檢視中識別合併原則的人性化名稱。 |
| `identityGraph` | 要從中獲取相關身份以進行合併的身份圖。 |
| `attributeMerge` | 在發生資料衝突時，設定描述檔屬性值優先順序的方式。 |
| `schema` | 與合併策略關聯的XDM模式類。 |
| `default` | 指定此合併策略是否為方案的預設策略。 |

有關詳細信 [息，請參閱合併策略](#components-of-merge-policies) 部分的元件。


**回應**

成功的回應會傳回更新的合併原則的詳細資料。

```json
{
    "id": "e5bc94de-cd14-4cdf-a2bc-88b6e8cbfac2",
    "name": "Loyalty members ordered by ID",
    "imsOrgId": "{IMS_ORG}",
    "sandbox": {
        "sandboxId": "ff0f6870-c46d-11e9-8ca3-036939a64204",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "schema": {
        "name": "_xdm.context.profile"
    },
    "version": 1,
    "identityGraph": {
        "type": "none"
    },
    "attributeMerge": {
        "type": "dataSetPrecedence",
        "order": [
            "5b76f86b85d0e00000be5c8b",
            "5b76f8d787a6af01e2ceda18"
        ]
    },
    "default": true,
    "updateEpoch": 1551898378
}
```

## 刪除合併策略

可通過向端點發出DELETE請求並在請求路徑中 `/config/mergePolicies` 包括要刪除的合併策略的ID來刪除合併策略。

**API格式**

```http
DELETE /config/mergePolicies/{mergePolicyId}
```

| 參數 | 說明 |
|---|---|
| `{mergePolicyId}` | 要刪除的合併策略的標識符。 |

**請求**

以下請求會刪除合併策略。

```shell
curl -X DELETE \
  https://platform.adobe.io/data/core/ups/config/mergePolicies/e5bc94de-cd14-4cdf-a2bc-88b6e8cbfac2 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**回應**

成功的刪除請求會傳回HTTP狀態200（確定）和空回應主體。 要確認刪除成功，可以執行GET請求以按合併策略的ID查看合併策略。 如果合併策略已刪除，您會收到HTTP狀態404（找不到）錯誤。

## 後續步驟

現在您知道如何為IMS組織建立及設定合併原則，您可以使用這些原則從即時客戶個人檔案資料建立受眾細分。 請參閱 [Adobe Experience Platform細分服務檔案](../../segmentation/home.md) ，開始定義和使用細分。



