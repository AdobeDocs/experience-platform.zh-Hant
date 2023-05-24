---
keywords: Experience Platform；配置；即時客戶配置；故障排除；API
title: 合併策略API終結點
type: Documentation
description: Adobe Experience Platform使您能夠將來自多個來源的資料片段組合在一起，並將它們組合起來，以便查看您每個客戶的完整視圖。 將此資料整合在一起時，合併策略是平台用來確定資料優先順序和組合哪些資料以建立統一視圖的規則。
exl-id: fb49977d-d5ca-4de9-b185-a5ac1d504970
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '2468'
ht-degree: 1%

---

# 合併策略終結點

Adobe Experience Platform使您能夠將來自多個來源的資料片段組合在一起，並將它們組合起來，以便查看您每個客戶的完整視圖。 將此資料整合在一起時，合併策略是 [!DNL Platform] 用於確定資料的優先順序以及將組合哪些資料以建立統一視圖。

例如，如果客戶通過多個渠道與您的品牌進行交互，您的組織將具有多個與該單個客戶相關的配置檔案片段，這些配置檔案片段出現在多個資料集中。 當這些片段被放入平台中時，它們會合併在一起，以便為該客戶建立單個配置檔案。 當來自多個源的資料發生衝突時（例如，一個片段將客戶列為「單一」，而另一個片段將客戶列為「已婚」），合併策略將確定要包括在個人配置檔案中的資訊。

使用REST風格的API或用戶介面，您可以建立新的合併策略、管理現有策略以及為組織設定預設的合併策略。 本指南提供了使用API使用合併策略的步驟。

要使用UI使用合併策略，請參閱 [合併策略UI指南](../merge-policies/ui-guide.md)。 要瞭解有關合併策略的一般資訊及其在Experience Platform中的作用的詳細資訊，請首先閱讀 [合併策略概述](../merge-policies/overview.md)。

## 快速入門

本指南中使用的API終結點是 [[!DNL Real-Time Customer Profile API]](https://www.adobe.com/go/profile-apis-en)。 在繼續之前，請查看 [入門指南](getting-started.md) 有關指向相關文檔的連結、閱讀本文檔中示例API調用的指南，以及成功調用任何文檔所需的標題的重要資訊 [!DNL Experience Platform] API。

## 合併策略的元件 {#components-of-merge-policies}

合併策略對您的組織是專用的，允許您建立不同的策略以按您需要的特定方式合併架構。 任何API訪問 [!DNL Profile] 資料需要合併策略，但如果未明確提供，則將使用預設策略。 [!DNL Platform] 為組織提供預設合併策略，或者您可以為特定體驗資料模型(XDM)架構類建立合併策略並將其標籤為組織的預設策略。

雖然每個組織可能每個架構類具有多個合併策略，但每個類只能有一個預設合併策略。 在提供架構類名稱且需要但未提供合併策略的情況下，將使用任何預設合併策略集。

>[!NOTE]
>
>將新合併策略設定為預設值時，先前設定為預設值的任何現有合併策略將自動更新為不再用作預設值。

為確保所有配置檔案使用者都使用相同的邊緣視圖，合併策略可標籤為邊緣上處於活動狀態。 要使段在邊上激活（標籤為邊段），必須將其綁定到在邊上標籤為活動的合併策略。 如果段為 **不** 綁定到標籤為邊緣上活動的合併策略，該段將不會標籤為邊緣上的活動段，並將標籤為流段。

此外，每個組織只能 **一個** 邊緣上處於活動狀態的合併策略。 如果合併策略在邊緣上處於活動狀態，則它可用於邊緣上的其他系統，如「邊緣輪廓」、「邊緣分割」和「邊緣上的目標」。

### 完成合併策略對象

完整的合併策略對象表示一組控制合併配置檔案片段的方面的首選項。

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
| `name` | 在清單視圖中標識合併策略的友好名稱。 |
| `imsOrgId` | 此合併策略所屬的組織ID |
| `schema.name` | 部分 [`schema`](#schema) 對象， `name` 欄位包含與合併策略相關的XDM架構類。 有關架構和類的詳細資訊，請閱讀 [XDM文檔](../../xdm/home.md)。 |
| `version` | [!DNL Platform] 維護的合併策略版本。 每當更新合併策略時，此只讀值都會遞增。 |
| `identityGraph` | [標識圖](#identity-graph) 對象指示將從中獲取相關標識的標識圖。 將合併所有相關標識的配置檔案片段。 |
| `attributeMerge` | [屬性合併](#attribute-merge) 對象，指示在發生資料衝突時合併策略將按何種方式優先處理配置檔案屬性。 |
| `isActiveOnEdge` | 指示此合併策略是否可用於邊緣的布爾值。 預設情況下，此值為 `false`。 |
| `default` | 指示此合併策略是否是指定架構的預設策略的布爾值。 |
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

### 識別圖 {#identity-graph}

[Adobe Experience Platform身份服務](../../identity-service/home.md) 管理全局使用的標識圖以及上的每個組織的標識圖 [!DNL Experience Platform]。 的 `identityGraph` 合併策略的屬性定義如何確定用戶的相關標識。

**identityGraph對象**

```json
    "identityGraph": {
        "type": "{IDENTITY_GRAPH_TYPE}"
    }
```

位置 `{IDENTITY_GRAPH_TYPE}` 是以下之一：

* **&quot;無&quot;:** 不執行身份拼接。
* **&quot;pdg&quot;:** 根據您的個人身份圖執行身份拼接。

**範例`identityGraph`**

```json
    "identityGraph": {
        "type": "pdg"
    }
```

### 屬性合併 {#attribute-merge}

配置檔案片段是特定用戶所存在的標識清單中只有一個標識的配置檔案資訊。 當使用的標識圖形類型導致產生多個標識時，可能存在衝突的配置檔案屬性，必須指定優先順序。 使用 `attributeMerge`，您可以指定在鍵值（記錄資料）類型資料集之間發生合併衝突時要優先排序的配置檔案屬性。

**attributeMerge對象**

```json
    "attributeMerge": {
        "type": "{ATTRIBUTE_MERGE_TYPE}"
    }
```

位置 `{ATTRIBUTE_MERGE_TYPE}` 是以下之一：

* **`timestampOrdered`**:（預設）優先於上次更新的配置檔案。 使用此合併類型， `data` 屬性不是必需的。
* **`dataSetPrecedence`**:根據從中獲取的資料集優先配置檔案片段。 當一個資料集中的資訊優先於另一個資料集中的資料，或者被信任時，可以使用此方法。 使用此合併類型時， `order` 屬性是必需的，因為它按優先順序順序列出資料集。
   * **`order`**:使用&quot;dataSetPrecence&quot;時， `order` 陣列必須提供資料集清單。 清單中未包含的任何資料集都不會合併。 換句話說，必須明確列出資料集才能合併到配置檔案中。 的 `order` 陣列按優先順序順序列出資料集的ID。

#### 示例 `attributeMerge` 對象使用 `dataSetPrecedence` 類型

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

#### 示例 `attributeMerge` 對象使用 `timestampOrdered` 類型

```json
    "attributeMerge": {
        "type": "timestampOrdered"
    }
```

### 方案 {#schema}

架構對象指定為其建立此合併策略的體驗資料模型(XDM)架構類。

**`schema`對象**

```json
    "schema": {
        "name": "{SCHEMA_NAME}"
    }
```

當 `name` 是與合併策略關聯的架構所基於的XDM類的名稱。

**範例`schema`**

```json
    "schema": {
        "name": "_xdm.context.profile"
    }
```

要瞭解有關XDM和使用Experience Platform中的架構的更多資訊，請首先閱讀 [XDM系統概述](../../xdm/home.md)。

## 訪問合併策略 {#access-merge-policies}

使用 [!DNL Real-Time Customer Profile] API, `/config/mergePolicies` 終結點允許您執行查找請求以按其ID查看特定合併策略，或訪問組織中按特定條件篩選的所有合併策略。 您還可以使用 `/config/mergePolicies/bulk-get` 終結點，以按其ID檢索多個合併策略。 以下各節概述了執行這些呼叫的步驟。

### 按ID訪問單個合併策略

您可以通過向ID發出GET請求來訪問單個合併策略 `/config/mergePolicies` 端點和包括 `mergePolicyId` 的子菜單。

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

查看 [合併策略的元件](#components-of-merge-policies) 的子菜單。

### 按ID檢索多個合併策略

您可以通過向執行以下操作的POST請求來檢索多個合併策略 `/config/mergePolicies/bulk-get` 端點，包括要在請求正文中檢索的合併策略的ID。

**API格式**

```http
POST /config/mergePolicies/bulk-get
```

**要求**

請求正文包括一個「ids」陣列，其中各個對象包含要檢索其詳細資訊的每個合併策略的「id」。

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

成功的響應返回HTTP狀態207（多狀態）和其ID在POST請求中提供的合併策略的詳細資訊。

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

查看 [合併策略的元件](#components-of-merge-policies) 的子菜單。

### 按條件列出多個合併策略

您可以通過向組織發出GET請求來列出組織內的多個合併策略 `/config/mergePolicies` 終結點，並使用可選查詢參數篩選、排序和分頁響應。 可以包括多個參數，用和符號(&amp;)分隔。 在沒有參數的情況下調用此終結點將檢索可用於您的組織的所有合併策略。

**API格式**

```http
GET /config/mergePolicies?{QUERY_PARAMS}
```

| 參數 | 說明 |
|---|---|
| `default` | 一個布爾值，它通過合併策略是否是架構類的預設值來篩選結果。 |
| `limit` | 指定頁面大小限制以控制頁面中包含的結果數。 預設值：20 |
| `orderBy` | 指定按中排序結果的欄位 `orderBy=name` 或 `orderBy=+name` 按名稱按升序排序，或 `orderBy=-name`，按降序排序。 省略此值將導致預設排序 `name` 按升序排列。 |
| `isActiveOnEdge` | 一個布爾值，它通過合併策略是否在邊緣上處於活動狀態來篩選結果。 |
| `schema.name` | 要為其檢索可用合併策略的架構的名稱。 |
| `identityGraph.type` | 按標識圖形類型篩選結果。 可能的值包括「無」和「pdg」（專用圖）。 |
| `attributeMerge.type` | 按使用的屬性合併類型篩選結果。 可能的值包括&quot;timestampOrdered&quot;和&quot;dataSetPrecerne&quot;。 |
| `start` | 頁偏移量 — 指定要檢索的資料的起始ID。 預設值：0 |
| `version` | 如果要使用合併策略的特定版本，請指定此選項。 預設情況下，將使用最新版本。 |

有關 `schema.name`。 `identityGraph.type`, `attributeMerge.type`，請參閱 [合併策略的元件](#components-of-merge-policies) 的子菜單。


**要求**

以下請求列出給定方案的所有合併策略：

```shell
curl -X GET \
  'https://platform.adobe.io/data/core/ups/config/mergePolicies?schema.name=_xdm.context.profile' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}
```

**回應**

成功的響應將返回符合請求中發送的查詢參數所指定的條件的合併策略的分頁清單。

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
| `_links.next.href` | 結果下一頁的URI地址。 將此URI用作對同一終結點的另一API調用的請求參數以查看該頁。 如果不存在下一頁，則此值將為空字串。 |

## 建立合併策略

您可以通過向以下站點發出POST請求，為您的組織建立新的合併策略 `/config/mergePolicies` 端點。

**API格式**

```http
POST /config/mergePolicies
```

**請求**
以下請求將建立新的合併策略，該策略由負載中提供的屬性值配置：

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
| `name` | 在清單視圖中標識合併策略的人性化名稱。 |
| `identityGraph.type` | 要從中獲取要合併的相關標識的標識圖形類型。 可能的值：&quot;none&quot;或&quot;pdg&quot;（專用圖）。 |
| `attributeMerge` | 在發生資料衝突時優先設定配置檔案屬性值的方式。 |
| `schema` | 與合併策略關聯的XDM架構類。 |
| `isActiveOnEdge` | 指定此合併策略是否在邊緣上處於活動狀態。 |
| `default` | 指定此合併策略是否是架構的預設策略。 |

請參閱 [合併策略的元件](#components-of-merge-policies) 的子菜單。

**回應**

成功的響應將返回新建立的合併策略的詳細資訊。

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

查看 [合併策略的元件](#components-of-merge-policies) 的子菜單。

## 更新合併策略 {#update}

可以通過編輯單個屬性(PATCH)或用新屬性覆蓋整個合併策略(PUT)來修改現有合併策略。 每個示例如下所示。

### 編輯單個合併策略欄位

通過向執行以下操作的PATCH請求，可以編輯合併策略的各個欄位 `/config/mergePolicies/{mergePolicyId}` 終結點：

**API格式**

```http
PATCH /config/mergePolicies/{mergePolicyId}
```

| 參數 | 說明 |
|---|---|
| `{mergePolicyId}` | 要刪除的合併策略的標識符。 |

**要求**

以下請求通過更改指定合併策略的值來更新其 `default` 屬性 `true`:

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
| `op` | 指定要執行的操作。 其他PATCH操作的示例可在 [JSON修補程式文檔](https://datatracker.ietf.org/doc/html/rfc6902) |
| `path` | 要更新的欄位的路徑。 接受的值為：&quot;/name&quot;、&quot;/identityGraph.type&quot;、&quot;/attributeMerge.type&quot;、&quot;/schema.name&quot;、&quot;/version&quot;、&quot;/default&quot;、&quot;/isActiveOnEdge&quot; |
| `value` | 將指定欄位設定為的值。 |

請參閱 [合併策略的元件](#components-of-merge-policies) 的子菜單。


**回應**

成功的響應將返回新更新的合併策略的詳細資訊。

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

修改合併策略的另一種方法是使用PUT請求，該請求覆蓋整個合併策略。

**API格式**

```http
PUT /config/mergePolicies/{mergePolicyId}
```

| 參數 | 說明 |
|---|---|
| `{mergePolicyId}` | 要覆蓋的合併策略的標識符。 |

**要求**

以下請求覆蓋指定的合併策略，將其屬性值替換為負載中提供的屬性值。 由於此請求完全替換了現有的合併策略，因此需要提供最初定義合併策略時所需的所有相同欄位。 但是，這次您將為要更改的欄位提供更新值。

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
| `name` | 在清單視圖中標識合併策略的人性化名稱。 |
| `identityGraph` | 要從中獲取要合併的相關標識的標識圖。 |
| `attributeMerge` | 在發生資料衝突時優先設定配置檔案屬性值的方式。 |
| `schema` | 與合併策略關聯的XDM架構類。 |
| `isActiveOnEdge` | 指定此合併策略是否在邊緣上處於活動狀態。 |
| `default` | 指定此合併策略是否是架構的預設策略。 |

請參閱 [合併策略的元件](#components-of-merge-policies) 的子菜單。

**回應**

成功的響應將返回更新的合併策略的詳細資訊。

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

通過向DELETE請求，可以刪除合併策略 `/config/mergePolicies` 端點，並包括要在請求路徑中刪除的合併策略的ID。

>[!NOTE]
>
>如果合併策略 `isActiveOnEdge` 設定為true時，合併策略 **不能** 刪除。 使用 [PATCH](#edit-individual-merge-policy-fields) 或 [PUT](#overwrite-a-merge-policy) 端點，以在刪除合併策略之前更新它。

**API格式**

```http
DELETE /config/mergePolicies/{mergePolicyId}
```

| 參數 | 說明 |
|---|---|
| `{mergePolicyId}` | 要刪除的合併策略的標識符。 |

**要求**

以下請求刪除合併策略。

```shell
curl -X DELETE \
  https://platform.adobe.io/data/core/ups/config/mergePolicies/e5bc94de-cd14-4cdf-a2bc-88b6e8cbfac2 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**回應**

成功的刪除請求返回HTTP狀態200(OK)和空響應正文。 要確認刪除成功，可以執行GET請求以按其ID查看合併策略。 如果刪除了合併策略，您將收到HTTP狀態404（未找到）錯誤。

## 後續步驟

現在，您知道如何為您的組織建立和配置合併策略，因此可以使用它們來調整平台中客戶配置檔案的視圖，並從您的 [!DNL Real-Time Customer Profile] 資料。

請參閱 [Adobe Experience Platform分段處檔案](../../segmentation/home.md) 開始定義和使用段。
