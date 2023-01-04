---
keywords: Experience Platform；設定檔；即時客戶設定檔；疑難排解；API
title: 合併策略API端點
topic-legacy: guide
type: Documentation
description: Adobe Experience Platform可讓您從多個來源將資料片段匯整在一起，並加以結合，以便查看每個客戶的完整檢視。 將這些資料整合在一起時，Platform會使用合併原則來判斷資料的優先順序，以及將哪些資料合併以建立統一檢視。
exl-id: fb49977d-d5ca-4de9-b185-a5ac1d504970
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '2472'
ht-degree: 1%

---

# 合併策略終結點

Adobe Experience Platform可讓您從多個來源將資料片段匯整在一起，並加以結合，以便查看每個客戶的完整檢視。 將這些資料放在一起時，合併策略是 [!DNL Platform] 用來決定資料的優先順序，以及將結合哪些資料以建立統一檢視。

例如，如果客戶跨多個管道與您的品牌互動，您的組織會在多個資料集中顯示與該單一客戶相關的多個設定檔片段。 將這些片段擷取至Platform時，會合併在一起，以便為該客戶建立單一設定檔。 當來自多個來源的資料發生衝突時（例如，一個片段將客戶列為「單一」，而另一個片段將客戶列為「已婚」），合併原則會決定要納入個人設定檔中的資訊。

使用RESTful API或用戶介面，您可以建立新的合併策略、管理現有策略，以及為組織設定預設的合併策略。 本指南提供使用API使用合併原則的步驟。

若要使用UI使用合併原則，請參閱 [合併策略UI指南](../merge-policies/ui-guide.md). 若要進一步了解一般合併原則及其在Experience Platform中的角色，請先閱讀 [合併策略概述](../merge-policies/overview.md).

## 快速入門

本指南中使用的API端點屬於 [[!DNL Real-Time Customer Profile API]](https://www.adobe.com/go/profile-apis-en). 繼續之前，請檢閱 [快速入門手冊](getting-started.md) 如需相關檔案的連結、閱讀本檔案中範例API呼叫的指南，以及成功呼叫任何呼叫所需的必要標題的重要資訊 [!DNL Experience Platform] API。

## 合併策略的元件 {#components-of-merge-policies}

合併原則是IMS組織專用的，可讓您建立不同的原則，以便以您需要的特定方式合併結構。 任何API存取 [!DNL Profile] 資料需要合併策略，但如果未明確提供，則會使用預設策略。 [!DNL Platform] 為組織提供預設的合併原則，或者您可以為特定Experience Data Model(XDM)結構類別建立合併原則，並將其標示為組織的預設值。

雖然每個組織可能具有每個架構類的多個合併策略，但每個類只能有一個預設的合併策略。 如果提供架構類名稱，但需要但未提供合併策略，則將使用任何設定為預設的合併策略。

>[!NOTE]
>
>當您將新合併策略設定為預設時，先前設定為預設的任何現有合併策略將自動更新為不再作為預設使用。

為確保所有配置檔案使用者在邊緣上使用相同的視圖，可以將合併策略標籤為邊緣上的活動策略。 要在邊緣上激活段（標籤為邊緣段），必須將其綁定到標籤為邊緣上活動的合併策略。 如果區段為 **not** 系結至標示為在邊緣處於作用中狀態的合併原則，區段不會標示為在邊緣處於作用中狀態，且會標示為串流區段。

此外，每個IMS組織只能 **one** 在邊緣處活動的合併策略。 如果合併策略在邊緣處於活動狀態，則該策略可用於邊緣處的其他系統，如邊緣配置檔案、邊緣分段和邊緣處的目標。

### 完整合併策略對象

完整的合併策略對象表示一組控制合併配置檔案片段方面的首選項。

**合併策略對象**

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
| `id` | 系統生成在建立時分配的唯一標識符 |
| `name` | 可在清單檢視中識別合併原則的易記名稱。 |
| `imsOrgId` | 此合併策略所屬的組織ID |
| `schema.name` | 部分 [`schema`](#schema) 對象， `name` 欄位包含與合併原則相關的XDM架構類別。 有關結構和類的詳細資訊，請閱讀 [XDM檔案](../../xdm/home.md). |
| `version` | [!DNL Platform] 維護的合併策略版本。 只要更新合併策略，此唯讀值就會增加。 |
| `identityGraph` | [身分圖](#identity-graph) 表示將從中獲取相關身份的標識圖的對象。 所有相關身分識別的設定檔片段將會合併。 |
| `attributeMerge` | [屬性合併](#attribute-merge) 對象，指示在發生資料衝突時合併策略優先處理配置檔案屬性的方式。 |
| `isActiveOnEdge` | 指示是否可以在邊緣上使用此合併策略的布爾值。 依預設，此值為 `false`. |
| `default` | 指示此合併策略是否為指定架構的預設策略的布爾值。 |
| `updateEpoch` | 合併策略的上次更新日期。 |

**合併策略示例**

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

### 身分圖 {#identity-graph}

[Adobe Experience Platform Identity Service](../../identity-service/home.md) 管理全域使用的身分圖表，以及 [!DNL Experience Platform]. 此 `identityGraph` 合併策略的屬性定義如何確定用戶的相關身份。

**identityGraph物件**

```json
    "identityGraph": {
        "type": "{IDENTITY_GRAPH_TYPE}"
    }
```

其中 `{IDENTITY_GRAPH_TYPE}` 是下列其中一項：

* **&quot;none&quot;:** 不執行身分匯整。
* **&quot;pdg&quot;:** 根據您的私人身分圖表執行身分拼接。

**範例`identityGraph`**

```json
    "identityGraph": {
        "type": "pdg"
    }
```

### 屬性合併 {#attribute-merge}

設定檔片段是特定使用者所在身分清單中，只有一個身分的設定檔資訊。 使用的身分圖表類型會產生多個身分時，可能會發生設定檔屬性衝突，且必須指定優先順序。 使用 `attributeMerge`，您可以指定在關鍵值（記錄資料）類型資料集之間發生合併衝突時，要排定優先順序的設定檔屬性。

**attributeMerge物件**

```json
    "attributeMerge": {
        "type": "{ATTRIBUTE_MERGE_TYPE}"
    }
```

其中 `{ATTRIBUTE_MERGE_TYPE}` 是下列其中一項：

* **`timestampOrdered`**:（預設）將優先順序設為上次更新的設定檔。 使用此合併類型， `data` 屬性不是必要項目。
* **`dataSetPrecedence`**:根據設定檔片段的來源資料集，為其指定優先順序。 當一個資料集中的資訊比另一個資料集中的資料更偏好或更受信任時，即可使用此方法。 使用此合併類型時， `order` 屬性為必要項目，因為它會依優先順序列出資料集。
   * **`order`**:使用&quot;dataSetPrecerance&quot;時， `order` 陣列必須隨附資料集清單。 清單中未包含的任何資料集都不會合併。 換言之，必須明確列出資料集，才能合併至設定檔中。 此 `order` 陣列會依優先順序列出資料集的ID。

#### 範例 `attributeMerge` 對象使用 `dataSetPrecedence` type

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

#### 範例 `attributeMerge` 對象使用 `timestampOrdered` type

```json
    "attributeMerge": {
        "type": "timestampOrdered"
    }
```

### 方案 {#schema}

架構物件會指定要建立此合併原則的Experience Data Model(XDM)架構類別。

**`schema`物件**

```json
    "schema": {
        "name": "{SCHEMA_NAME}"
    }
```

若 `name` 是XDM類的名稱，與合併策略關聯的架構是基於該類的。

**範例`schema`**

```json
    "schema": {
        "name": "_xdm.context.profile"
    }
```

若要進一步了解XDM以及運用Experience Platform中的結構，請先閱讀 [XDM系統概觀](../../xdm/home.md).

## 訪問合併策略 {#access-merge-policies}

使用 [!DNL Real-Time Customer Profile] API、 `/config/mergePolicies` 端點可讓您執行查詢請求，依其ID檢視特定的合併原則，或存取IMS組織中依特定條件篩選的所有合併原則。 您也可以使用 `/config/mergePolicies/bulk-get` 端點，通過其ID檢索多個合併策略。 以下各節將概述執行這些呼叫的步驟。

### 按ID訪問單個合併策略

您可以透過向 `/config/mergePolicies` 端點和包含 `mergePolicyId` 在請求路徑中。

**API格式**

```http
GET /config/mergePolicies/{mergePolicyId}
```

| 參數 | 說明 |
|---|---|
| `{mergePolicyId}` | 要刪除的合併策略的標識符。 |

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

成功的響應返回合併策略的詳細資訊。

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

請參閱 [合併策略的元件](#components-of-merge-policies) 一節，以了解組成合併策略的各個元素的詳細資訊。

### 通過其ID檢索多個合併策略

您可以向 `/config/mergePolicies/bulk-get` 端點，以及納入您要在要求內文中擷取之合併原則的ID。

**API格式**

```http
POST /config/mergePolicies/bulk-get
```

**要求**

請求內文包含「ids」陣列，內含個別物件，其中包含您要擷取詳細資料之每個合併原則的「id」。

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

成功的回應會傳回HTTP狀態207（多狀態），以及其ID已於POST請求中提供之合併原則的詳細資訊。

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

請參閱 [合併策略的元件](#components-of-merge-policies) 一節，以了解組成合併策略的各個元素的詳細資訊。

### 按條件列出多個合併策略

您可以向以下網站發出GET請求，列出IMS組織內的多個合併原則： `/config/mergePolicies` 端點，並使用選用的查詢參數來篩選、排序和分頁回應。 可包含多個參數，以&amp;符號分隔。 對此端點進行無參數呼叫將檢索組織可用的所有合併策略。

**API格式**

```http
GET /config/mergePolicies?{QUERY_PARAMS}
```

| 參數 | 說明 |
|---|---|
| `default` | 一個布爾值，通過合併策略是否為架構類的預設策略來篩選結果。 |
| `limit` | 指定頁面大小限制以控制頁面中包含的結果數量。 預設值：20 |
| `orderBy` | 指定要依其對結果排序的欄位，如 `orderBy=name` 或 `orderBy=+name` 按名稱升序排序，或 `orderBy=-name`，可依遞減順序排序。 省略此值會導致的預設排序為 `name` 按升序。 |
| `isActiveOnEdge` | 一個布林值，通過合併策略是否在邊緣處處於活動狀態來篩選結果。 |
| `schema.name` | 要為其檢索可用合併策略的架構的名稱。 |
| `identityGraph.type` | 依身分圖表類型篩選結果。 可能的值包括「無」和「pdg」（專用圖表）。 |
| `attributeMerge.type` | 按使用的屬性合併類型篩選結果。 可能的值包括「timestampOrdered」和「dataSetPrecerance」。 |
| `start` | 頁面偏移 — 指定要擷取資料的起始ID。 預設值：0 |
| `version` | 如果要使用合併策略的特定版本，請指定此選項。 依預設，會使用最新版本。 |

如需 `schema.name`, `identityGraph.type`，和 `attributeMerge.type`，請參閱 [合併策略的元件](#components-of-merge-policies) 本指南前面提供的章節。


**要求**

以下請求列出了給定架構的所有合併策略：

```shell
curl -X GET \
  'https://platform.adobe.io/data/core/ups/config/mergePolicies?schema.name=_xdm.context.profile' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}
```

**回應**

成功的回應會傳回符合要求中傳送之查詢參數所指定准則的合併原則編頁清單。

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
| `_links.next.href` | 結果下一頁的URI地址。 使用此URI作為向同一端點進行的另一個API調用的請求參數，以查看該頁。 如果沒有下一頁存在，則此值將為空字串。 |

## 建立合併策略

您可以向 `/config/mergePolicies` 端點。

**API格式**

```http
POST /config/mergePolicies
```

**要求**
以下請求會建立新的合併策略，該策略由有效負載中提供的屬性值配置：

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
| `name` | 一個好記的名稱，可在清單檢視中識別合併政策。 |
| `identityGraph.type` | 要從中獲取要合併的相關身份的標識圖類型。 可能的值：「無」或「pdg」（專用圖表）。 |
| `attributeMerge` | 在發生資料衝突時，設定檔屬性值優先順序的方式。 |
| `schema` | 與合併策略關聯的XDM架構類。 |
| `isActiveOnEdge` | 指定此合併策略是否在邊緣上處於活動狀態。 |
| `default` | 指定此合併策略是否為架構的預設策略。 |

請參閱 [合併策略的元件](#components-of-merge-policies) 一節以取得詳細資訊。

**回應**

成功的響應返回新建立的合併策略的詳細資訊。

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

請參閱 [合併策略的元件](#components-of-merge-policies) 一節，以了解組成合併策略的各個元素的詳細資訊。

## 更新合併策略 {#update}

通過編輯單個屬性(PATCH)或用新屬性(PUT)覆蓋整個合併策略，可以修改現有合併策略。 各個範例如下所示。

### 編輯單個合併策略欄位

您可以對 `/config/mergePolicies/{mergePolicyId}` 端點：

**API格式**

```http
PATCH /config/mergePolicies/{mergePolicyId}
```

| 參數 | 說明 |
|---|---|
| `{mergePolicyId}` | 要刪除的合併策略的標識符。 |

**要求**

以下請求通過更改其值來更新指定的合併策略 `default` 屬性 `true`:

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
| `op` | 指定要執行的操作。 如需其他PATCH操作的範例，請參閱 [JSON修補程式檔案](https://datatracker.ietf.org/doc/html/rfc6902) |
| `path` | 要更新的欄位路徑。 接受的值為：&quot;/name&quot;, &quot;/identityGraph.type&quot;, &quot;/attributeMerge.type&quot;, &quot;/schema.name&quot;, &quot;/version&quot;, &quot;/default&quot;, &quot;/isActiveOnEdge&quot; |
| `value` | 將指定欄位設為的值。 |

請參閱 [合併策略的元件](#components-of-merge-policies) 一節以取得詳細資訊。


**回應**

成功的響應返回新更新的合併策略的詳細資訊。

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

### 覆蓋合併策略

修改合併策略的另一種方法是使用PUT請求，該請求會覆蓋整個合併策略。

**API格式**

```http
PUT /config/mergePolicies/{mergePolicyId}
```

| 參數 | 說明 |
|---|---|
| `{mergePolicyId}` | 要覆蓋的合併策略的標識符。 |

**要求**

以下請求會覆寫指定的合併策略，將其屬性值替換為有效負載中提供的屬性值。 由於此請求完全替換了現有的合併策略，因此您必須提供最初定義合併策略時所需的所有相同欄位。 不過，這次您會提供您要變更之欄位的更新值。

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
| `name` | 一個好記的名稱，可在清單檢視中識別合併政策。 |
| `identityGraph` | 要從中獲取要合併的相關標識的標識圖。 |
| `attributeMerge` | 在發生資料衝突時，設定檔屬性值優先順序的方式。 |
| `schema` | 與合併策略關聯的XDM架構類。 |
| `isActiveOnEdge` | 指定此合併策略是否在邊緣上處於活動狀態。 |
| `default` | 指定此合併策略是否為架構的預設策略。 |

請參閱 [合併策略的元件](#components-of-merge-policies) 一節以取得詳細資訊。

**回應**

成功的響應返回更新的合併策略的詳細資訊。

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

## 刪除合併策略

可以刪除合併策略，方法是向 `/config/mergePolicies` 端點，並在請求路徑中包含您要刪除的合併原則ID。

>[!NOTE]
>
>如果合併策略已 `isActiveOnEdge` 設為true，則合併原則 **不能** 被刪除。 使用 [PATCH](#edit-individual-merge-policy-fields) 或 [PUT](#overwrite-a-merge-policy) 端點，以在刪除合併策略之前對其進行更新。

**API格式**

```http
DELETE /config/mergePolicies/{mergePolicyId}
```

| 參數 | 說明 |
|---|---|
| `{mergePolicyId}` | 要刪除的合併策略的標識符。 |

**要求**

以下請求將刪除合併策略。

```shell
curl -X DELETE \
  https://platform.adobe.io/data/core/ups/config/mergePolicies/e5bc94de-cd14-4cdf-a2bc-88b6e8cbfac2 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**回應**

成功的刪除請求會傳回HTTP狀態200(OK)和空的回應內文。 若要確認刪除是否成功，您可以執行GET請求，依其ID檢視合併原則。 如果刪除合併策略，您會收到HTTP狀態404（找不到）錯誤。

## 後續步驟

現在您知道如何為組織建立和設定合併原則，可以使用這些原則來調整Platform中客戶設定檔的檢視，並從您的 [!DNL Real-Time Customer Profile] 資料。

請參閱 [Adobe Experience Platform區段服務檔案](../../segmentation/home.md) 以開始定義和使用區段。
