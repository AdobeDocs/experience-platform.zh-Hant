---
keywords: Experience Platform；設定檔；即時客戶設定檔；疑難排解；API
title: 合併原則API端點
type: Documentation
description: Adobe Experience Platform可讓您將多個來源的資料片段彙整在一起，並將它們合併，以便檢視每個個別客戶的完整檢視。 彙總此資料時，合併原則是Experience Platform用來判斷資料優先順序的方式，以及將合併哪些資料以建立統一檢視的規則。
role: Developer
exl-id: fb49977d-d5ca-4de9-b185-a5ac1d504970
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '2468'
ht-degree: 1%

---

# 合併原則端點

Adobe Experience Platform可讓您將多個來源的資料片段彙整在一起，並將它們合併，以便檢視每個個別客戶的完整檢視。 將這個資料集合在一起時，合併原則是[!DNL Experience Platform]用來決定資料優先順序的方式以及將合併哪些資料以建立統一檢視的規則。

例如，如果客戶跨多個管道與您的品牌互動，則您的組織將會有多個與該單一客戶相關的設定檔片段出現在多個資料集中。 這些片段在擷取至Experience Platform時，會合併在一起，以便為該客戶建立單一設定檔。 當來自多個來源的資料衝突時（例如，一個片段將客戶列為「單身」，而另一個片段將客戶列為「已婚」），合併原則會決定要包含在個人設定檔中的資訊。

使用RESTful API或使用者介面，您可以建立新的合併原則、管理現有原則，並為您的組織設定預設合併原則。 本指南提供使用API處理合併原則的步驟。

若要使用UI來使用合併原則，請參閱[合併原則UI指南](../merge-policies/ui-guide.md)。 若要進一步瞭解一般合併原則及其在Experience Platform中的角色，請先閱讀[合併原則概觀](../merge-policies/overview.md)。

## 快速入門

本指南中使用的API端點是[[!DNL Real-Time Customer Profile API]](https://www.adobe.com/go/profile-apis-en)的一部分。 繼續之前，請先檢閱[快速入門手冊](getting-started.md)，以取得相關檔案的連結、閱讀本檔案中範例API呼叫的手冊，以及有關成功呼叫任何[!DNL Experience Platform] API所需必要標題的重要資訊。

## 合併原則的元件 {#components-of-merge-policies}

合併原則是您組織專屬的原則，可讓您建立不同的原則，以您所需的特定方式合併方案。 任何存取[!DNL Profile]資料的API都需要合併原則，但如果未明確提供合併原則，則會使用預設原則。 [!DNL Experience Platform]為組織提供預設的合併原則，或者您可以為特定Experience Data Model (XDM)結構描述類別建立合併原則，並將其標籤為組織的預設值。

雖然每個組織在每個結構描述類別中可能都有多個合併原則，但每個類別只能有一個預設合併原則。 若提供結構描述類別的名稱，但需要合併原則但未提供，則會使用任何設為預設的合併原則。

>[!NOTE]
>
>當您設定新的合併原則為預設值時，之前設為預設的任何現有合併原則會自動更新為不再使用作為預設值。

為確保所有設定檔消費者在邊緣上使用相同的檢視，可將邊緣上的合併原則標籤為使用中。 為了在Edge上啟用對象（標示為Edge對象），該對象必須繫結至Edge上標示為「作用中」的合併原則。 如果對象是&#x200B;**非**，繫結至在Edge上標示為「作用中」的合併原則，則該對象不會在Edge上標示為「作用中」，而會標示為串流對象。

此外，每個組織只能有&#x200B;**一個**&#x200B;在邊緣上有效的合併原則。 如果合併原則在Edge上為作用中，可用於Edge上的其他系統，例如Edge設定檔、Edge分段和Edge上的目的地。

### 完成合併原則物件

完整的合併原則物件代表一組偏好設定，可控制合併設定檔片段的各個層面。

**合併原則物件**

```json
    {
        "id": "{MERGE_POLICY_ID}",
        "name": "{NAME}",
        "imsOrgId": "{ORG_ID}",
        "schema": {
            "name": "{SCHEMA_CLASS_NAME}"
        },
        "version": 1,
        "identityGraph": {
            "type": "{IDENTITY_GRAPH_TYPE}"
        },
        "attributeMerge": {
            "type": "{ATTRIBUTE_MERGE_TYPE}"
        },
        "isActiveOnEdge": "{BOOLEAN}",
        "default": "{BOOLEAN}",
        "updateEpoch": "{UPDATE_TIME}"
    }
```

| 屬性 | 說明 |
|---|---|
| `id` | 系統產生的唯一識別碼在建立時指派 |
| `name` | 可在清單檢視中識別合併原則的易記名稱。 |
| `imsOrgId` | 此合併原則所屬的組織識別碼 |
| `schema.name` | `name`欄位是[`schema`](#schema)物件的一部分，包含與合併原則相關的XDM結構描述類別。 如需結構描述和類別的詳細資訊，請參閱[XDM檔案](../../xdm/home.md)。 |
| `version` | [!DNL Experience Platform]維護的合併原則版本。 此唯讀值在合併原則更新時遞增。 |
| `identityGraph` | [身分圖表](#identity-graph)物件，指出將從中取得相關身分的身分圖表。 將合併針對所有相關身分找到的設定檔片段。 |
| `attributeMerge` | [屬性合併](#attribute-merge)物件，指出當資料衝突時，合併原則優先處理設定檔屬性的方式。 |
| `isActiveOnEdge` | 表示此合併原則是否可用於Edge的布林值。 預設值為`false`。 |
| `default` | 表示此合併原則是否為指定之結構描述的預設值的布林值。 |
| `updateEpoch` | 上次更新合併原則的日期。 |

**合併原則範例**

```json
    {
        "id": "10648288-cda5-11e8-a8d5-f2801f1b9fd1",
        "name": "profile-default",
        "imsOrgId": "{ORG_ID}",
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
        "isActiveOnEdge": false,
        "default": true,
        "updateEpoch": 1551660639
    }
```

### 身分識別圖 {#identity-graph}

[Adobe Experience Platform Identity Service](../../identity-service/home.md)管理[!DNL Experience Platform]上每個組織全域使用的身分圖表。 合併原則的`identityGraph`屬性定義如何判斷使用者的相關身分。

**identityGraph物件**

```json
    "identityGraph": {
        "type": "{IDENTITY_GRAPH_TYPE}"
    }
```

其中`{IDENTITY_GRAPH_TYPE}`為下列其中一項：

* **「無」：**&#x200B;不執行任何身分拼接。
* **&quot;pdg&quot;：**&#x200B;根據您的私人身分圖表執行身分拼接。

**範例`identityGraph`**

```json
    "identityGraph": {
        "type": "pdg"
    }
```

### 屬性合併 {#attribute-merge}

設定檔片段是存在於特定使用者身分識別清單中，只有一個身分的設定檔資訊。 當使用的身分圖表型別導致多個身分時，可能會發生設定檔屬性衝突，必須指定優先順序。 使用`attributeMerge`，您可以指定在索引鍵值（記錄資料）型別資料集之間發生合併衝突時，要優先處理哪些設定檔屬性。

**attributeMerge物件**

```json
    "attributeMerge": {
        "type": "{ATTRIBUTE_MERGE_TYPE}"
    }
```

其中`{ATTRIBUTE_MERGE_TYPE}`為下列其中一項：

* **`timestampOrdered`**： （預設）為上次更新的設定檔指定優先順序。 使用此合併型別，`data`屬性不是必要的。
* **`dataSetPrecedence`**：根據設定檔片段來自的資料集為其指定優先順序。 當某個資料集中呈現的資訊優先於或受信任於另一個資料集中的資料時，就可以使用此功能。 使用此合併型別時，`order`屬性是必要的，因為它會依優先順序列出資料集。
   * **`order`**：使用「dataSetPrecedence」時，`order`陣列必須隨資料集清單提供。 不會合併清單中未包含的任何資料集。 換句話說，資料集必須明確列出，才能合併至設定檔中。 `order`陣列會依優先順序列出資料集的ID。

#### 使用`dataSetPrecedence`型別的範例`attributeMerge`物件

```json
    "attributeMerge": {
        "type": "dataSetPrecedence",
        "order": [
            "dataSetId_2", 
            "dataSetId_3", 
            "dataSetId_1", 
            "dataSetId_4"
        ]
    }
```

#### 使用`timestampOrdered`型別的範例`attributeMerge`物件

```json
    "attributeMerge": {
        "type": "timestampOrdered"
    }
```

### 結構描述 {#schema}

結構描述物件會指定為其建立此合併原則的Experience Data Model (XDM)結構描述類別。

**`schema`物件**

```json
    "schema": {
        "name": "{SCHEMA_NAME}"
    }
```

其中`name`的值是與合併原則相關聯之結構描述所依據的XDM類別名稱。

**範例`schema`**

```json
    "schema": {
        "name": "_xdm.context.profile"
    }
```

若要進一步瞭解XDM以及在Experience Platform中使用結構描述，請從閱讀[XDM系統總覽](../../xdm/home.md)開始。

## 存取合併原則 {#access-merge-policies}

使用[!DNL Real-Time Customer Profile] API，`/config/mergePolicies`端點可讓您執行查詢要求，以依據其ID檢視特定合併原則，或存取組織中依特定條件篩選的所有合併原則。 您也可以使用`/config/mergePolicies/bulk-get`端點，依其ID擷取多個合併原則。 以下各節將概述執行上述每個呼叫的步驟。

### 依ID存取單一合併原則

您可以透過單一合併原則的ID存取單一合併原則，方法是向`/config/mergePolicies`端點發出GET要求，並在要求路徑中加入`mergePolicyId`。

**API格式**

```http
GET /config/mergePolicies/{mergePolicyId}
```

| 參數 | 說明 |
|---|---|
| `{mergePolicyId}` | 您要刪除的合併原則識別碼。 |

**要求**

```shell
curl -X GET \
  'https://platform.adobe.io/data/core/ups/config/mergePolicies/10648288-cda5-11e8-a8d5-f2801f1b9fd1' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}
```

**回應**

成功的回應會傳回合併原則的詳細資料。

```json
{
    "id": "10648288-cda5-11e8-a8d5-f2801f1b9fd1",
    "imsOrgId": "{ORG_ID}",
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
    "isActiveOnEdge": "false",
    "default": false,
    "updateEpoch": 1551127597
}
```

請參閱本檔案開頭的[合併原則](#components-of-merge-policies)元件，瞭解組成合併原則的每一個個別元素的詳細資訊。

### 依其ID擷取多個合併原則

您可以對`/config/mergePolicies/bulk-get`端點發出POST要求，並在要求內文中包含您要擷取的合併原則ID，以擷取多個合併原則。

**API格式**

```http
POST /config/mergePolicies/bulk-get
```

**要求**

請求內文包含「ids」陣列，其中包含您要擷取詳細資料的每個合併原則之個別物件，其中包含「id」。

```shell
curl -X POST \
  'https://platform.adobe.io/data/core/ups/config/mergePolicies/bulk-get' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
        "ids": [
          {
            "id": "0bf16e61-90e9-4204-b8fa-ad250360957b"
          },
          {
            "id": "42d4a596-b1c6-46c0-994e-ca5ef1f85130"
          }
        ]
      }'
```

**回應**

成功的回應會傳回HTTP狀態207 （多重狀態）以及POST要求中提供ID之合併原則的詳細資料。

```json
{ 
    "results": { 
        "0bf16e61-90e9-4204-b8fa-ad250360957b": {
            "id": "0bf16e61-90e9-4204-b8fa-ad250360957b",
            "name": "Profile Default Merge Policy",
            "imsOrgId": "{ORG_ID}",
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
            "isActiveOnEdge": true,
            "default": true,
            "updateEpoch": 1552086578
        },
        "42d4a596-b1c6-46c0-994e-ca5ef1f85130": {
            "id": "42d4a596-b1c6-46c0-994e-ca5ef1f85130",
            "name": "Dataset Precedence Merge Policy",
            "imsOrgId": "{ORG_ID}",
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
            "isActiveOnEdge": false,
            "default": false,
            "updateEpoch": 1576099719
        }
    }
}
```

請參閱本檔案開頭的[合併原則](#components-of-merge-policies)元件，瞭解組成合併原則的每一個個別元素的詳細資訊。

### 依條件列出多個合併原則

您可以發出GET要求給`/config/mergePolicies`端點，並使用選用的查詢引數來篩選、排序及分頁回應，藉此列出組織內的多個合併原則。 可包含多個引數，以&amp;分隔。 在不使用引數的情況下呼叫此端點將會擷取您的組織可用的所有合併原則。

**API格式**

```http
GET /config/mergePolicies?{QUERY_PARAMS}
```

| 參數 | 說明 |
|---|---|
| `default` | 布林值，會依據合併原則是否為結構描述類別的預設值來篩選結果。 |
| `limit` | 指定頁面大小限制，以控制頁面中包含的結果數量。 預設值： 20 |
| `orderBy` | 指定排序結果所依據的欄位，如`orderBy=name`或`orderBy=+name`，以名稱遞增排序，或`orderBy=-name`，以遞減排序。 省略此值會導致`name`的預設排序（以遞增順序排列）。 |
| `isActiveOnEdge` | 布林值，會依據合併原則在Edge上是否有效來篩選結果。 |
| `schema.name` | 要擷取其可用合併原則的結構描述名稱。 |
| `identityGraph.type` | 依身分圖表型別篩選結果。 可能的值包括「none」和「pdg」（私密圖表）。 |
| `attributeMerge.type` | 依使用的屬性合併型別篩選結果。 可能的值包括「timestampOrdered」和「dataSetPrecedence」。 |
| `start` | 頁面位移 — 指定要擷取之資料的起始ID。 預設值： 0 |
| `version` | 如果您要使用特定版本的合併原則，請指定此專案。 依預設，將會使用最新版本。 |

如需`schema.name`、`identityGraph.type`和`attributeMerge.type`的詳細資訊，請參閱本指南前面提供的合併原則[&#128279;](#components-of-merge-policies)的元件。


**要求**

下列要求列出特定結構描述的所有合併原則：

```shell
curl -X GET \
  'https://platform.adobe.io/data/core/ups/config/mergePolicies?schema.name=_xdm.context.profile' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}
```

**回應**

成功的回應會傳回符合由請求中傳送的查詢引數所指定之條件的合併原則分頁清單。

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
            "imsOrgId": "{ORG_ID}",
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
            "isActiveOnEdge": true,
            "default": true,
            "updateEpoch": 1552086578
        },
        {
            "id": "42d4a596-b1c6-46c0-994e-ca5ef1f85130",
            "name": "Dataset Precedence Merge Policy",
            "imsOrgId": "{ORG_ID}",
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
            "isActiveOnEdge": false,
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
| `_links.next.href` | 結果下一頁的URI位址。 將此URI用作對相同端點的另一個API呼叫的請求引數，以檢視頁面。 如果下一頁不存在，則此值將為空字串。 |

## 建立合併原則

您可以透過對`/config/mergePolicies`端點發出POST要求，為您的組織建立新的合併原則。

**API格式**

```http
POST /config/mergePolicies
```

**要求**
以下請求會建立新的合併原則，此原則由承載中提供的屬性值設定：

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/config/mergePolicies \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
    "name": "Loyalty members ordered by ID",
    "identityGraph": {
        "type": "none"
    },
    "attributeMerge": {
        "type":"dataSetPrecedence",
        "order": [
            "5b76f86b85d0e00000be5c8b",
            "5b76f8d787a6af01e2ceda18"
        ]
    },
    "schema": {
        "name":"_xdm.context.profile"
    },
    "isActiveOnEdge": true,
    "default": true
}'
```

| 屬性 | 說明 |
|---|---|
| `name` | 人類易記的名稱，可在清單檢視中識別合併原則。 |
| `identityGraph.type` | 從中取得要合併之相關身分的身分圖表型別。 可能的值： 「無」或「pdg」（私密圖表）。 |
| `attributeMerge` | 當資料衝突時，設定檔屬性值的優先順序。 |
| `schema` | 與合併原則關聯的XDM結構描述類別。 |
| `isActiveOnEdge` | 指定此合併原則在Edge上是否有效。 |
| `default` | 指定此合併原則是否為結構描述的預設值。 |

如需詳細資訊，請參閱合併原則[&#128279;](#components-of-merge-policies)的元件。

**回應**

成功的回應會傳回新建立的合併原則的詳細資料。

```json
{
    "id": "e5bc94de-cd14-4cdf-a2bc-88b6e8cbfac2",
    "name": "Loyalty members ordered by ID",
    "imsOrgId": "{ORG_ID}",
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
    "isActiveOnEdge": true,
    "default": true,
    "updateEpoch": 1551898378
}
```

請參閱本檔案開頭的[合併原則](#components-of-merge-policies)元件，瞭解組成合併原則的每一個個別元素的詳細資訊。

## 更新合併原則 {#update}

您可以編輯個別屬性(PATCH)或使用新屬性覆寫整個合併原則(PUT)，以修改現有的合併原則。 每種的範例如下所示。

### 編輯個別合併原則欄位

您可以透過向`/config/mergePolicies/{mergePolicyId}`端點發出PATCH請求來編輯合併原則的個別欄位：

**API格式**

```http
PATCH /config/mergePolicies/{mergePolicyId}
```

| 參數 | 說明 |
|---|---|
| `{mergePolicyId}` | 您要刪除的合併原則識別碼。 |

**要求**

下列要求會將其`default`屬性的值變更為`true`，以更新指定的合併原則：

```shell
curl -X PATCH \
  https://platform.adobe.io/data/core/ups/config/mergePolicies/e5bc94de-cd14-4cdf-a2bc-88b6e8cbfac2 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `op` | 指定要執行的作業。 其他PATCH作業的範例可在[JSON修補程式檔案](https://datatracker.ietf.org/doc/html/rfc6902)中找到 |
| `path` | 要更新的欄位路徑。 接受的值為：「/name」、「/identityGraph.type」、「/attributeMerge.type」、「/schema.name」、「/version」、「/default」、「/isActiveOnEdge」 |
| `value` | 要設定指定欄位的值。 |

如需詳細資訊，請參閱合併原則[&#128279;](#components-of-merge-policies)的元件。


**回應**

成功的回應會傳回新更新的合併原則的詳細資料。

```json
{
    "id": "e5bc94de-cd14-4cdf-a2bc-88b6e8cbfac2",
    "name": "Loyalty members ordered by ID",
    "imsOrgId": "{ORG_ID}",
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
    "isActiveOnEdge": true,
    "default": true,
    "updateEpoch": 1551898378
}
```

### 覆寫合併原則

修改合併原則的另一種方法是使用PUT請求，該請求會覆寫整個合併原則。

**API格式**

```http
PUT /config/mergePolicies/{mergePolicyId}
```

| 參數 | 說明 |
|---|---|
| `{mergePolicyId}` | 您要覆寫之合併原則的識別碼。 |

**要求**

以下請求會覆寫指定的合併原則，將其屬性值取代為承載中提供的屬性值。 由於此請求會完全取代現有的合併原則，因此您必須提供原始定義合併原則時所需的所有相同欄位。 不過，這次您要變更的欄位會提供更新的值。

```shell
curl -X PUT \
  https://platform.adobe.io/data/core/ups/config/mergePolicies/e5bc94de-cd14-4cdf-a2bc-88b6e8cbfac2 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
        "name": "Loyalty members ordered by ID",
        "imsOrgId": "{ORG_ID}",
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
        "isActiveOnEdge": true,
        "default": true,
        "updateEpoch": 1551898378
    }'
```

| 屬性 | 說明 |
|---|---|
| `name` | 人類易記的名稱，可在清單檢視中識別合併原則。 |
| `identityGraph` | 從中取得要合併之相關身分的身分圖表。 |
| `attributeMerge` | 當資料衝突時，設定檔屬性值的優先順序。 |
| `schema` | 與合併原則關聯的XDM結構描述類別。 |
| `isActiveOnEdge` | 指定此合併原則在Edge上是否有效。 |
| `default` | 指定此合併原則是否為結構描述的預設值。 |

如需詳細資訊，請參閱合併原則[&#128279;](#components-of-merge-policies)的元件。

**回應**

成功的回應會傳回已更新合併原則的詳細資料。

```json
{
    "id": "e5bc94de-cd14-4cdf-a2bc-88b6e8cbfac2",
    "name": "Loyalty members ordered by ID",
    "imsOrgId": "{ORG_ID}",
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
    "isActiveOnEdge": true,
    "default": true,
    "updateEpoch": 1551898378
}
```

## 刪除合併原則

透過向`/config/mergePolicies`端點發出DELETE請求，並在請求路徑中包含您要刪除的合併原則ID，可以刪除合併原則。

>[!NOTE]
>
>如果合併原則已將`isActiveOnEdge`設定為true，則無法刪除合併原則&#x200B;**&#x200B;**。 使用[PATCH](#edit-individual-merge-policy-fields)或[PUT](#overwrite-a-merge-policy)端點更新合併原則，然後再刪除它。

**API格式**

```http
DELETE /config/mergePolicies/{mergePolicyId}
```

| 參數 | 說明 |
|---|---|
| `{mergePolicyId}` | 您要刪除的合併原則識別碼。 |

**要求**

以下請求會刪除合併原則。

```shell
curl -X DELETE \
  https://platform.adobe.io/data/core/ups/config/mergePolicies/e5bc94de-cd14-4cdf-a2bc-88b6e8cbfac2 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**回應**

成功的刪除請求會傳回HTTP狀態200 （確定）和空白的回應內文。 若要確認刪除成功，您可以執行GET要求，依其ID檢視合併原則。 如果刪除合併原則，您將會收到HTTP狀態404 （找不到）錯誤。

## 後續步驟

現在您知道如何為組織建立和設定合併原則，您可以使用這些原則來調整Experience Platform中客戶設定檔的檢視，以及從您的[!DNL Real-Time Customer Profile]資料建立對象。

請參閱[Adobe Experience Platform Segmentation Service檔案](../../segmentation/home.md)，以開始定義和使用對象。
