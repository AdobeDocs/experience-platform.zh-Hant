---
keywords: Experience Platform；配置檔案；即時客戶配置檔案；故障排除；API
title: 合併策略API端點
topic-legacy: guide
type: Documentation
description: Adobe Experience Platform可讓您從多個來源匯整資料片段，並加以結合，以全面瞭解每個客戶。 將這些資料整合在一起時，合併原則是平台用來決定資料的優先順序以及將哪些資料合併以建立統一檢視的規則。
exl-id: fb49977d-d5ca-4de9-b185-a5ac1d504970
translation-type: tm+mt
source-git-commit: ab0798851e5f2b174d9f4241ad64ac8afa20a938
workflow-type: tm+mt
source-wordcount: '2569'
ht-degree: 1%

---

# 合併策略端點

Adobe Experience Platform可讓您從多個來源匯整資料片段，並加以結合，以全面瞭解每個客戶。 合併策略是[!DNL Platform]用於確定資料的優先順序以及將哪些資料合併以建立統一視圖的規則。

例如，如果客戶透過多個通道與您的品牌互動，您的組織將會在多個資料集中顯示與該單一客戶相關的多個描述檔片段。 當這些片段被收錄到Platform中時，會將它們合併在一起，以便為該客戶建立單一個人檔案。 當來自多個來源的資料發生衝突（例如，一個片段將客戶列為「單一」，而另一個片段將客戶列為「已婚」）時，合併原則會決定要包含在個人描述檔中的資訊。

使用REST風格的API或用戶介面，您可以建立新的合併策略、管理現有策略，並為組織設定預設的合併策略。 本指南提供使用API使用合併原則的步驟。

要使用UI使用合併策略，請參閱[合併策略UI指南](../ui/merge-policies.md)。

## 快速入門

本指南中使用的API端點是[[!DNL Real-time Customer Profile API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/real-time-customer-profile.yaml)的一部分。 在繼續之前，請先閱讀[快速入門手冊](getting-started.md)，以取得相關檔案的連結、閱讀本檔案中範例API呼叫的指南，以及成功呼叫任何[!DNL Experience Platform] API所需之必要標題的重要資訊。

## 合併策略的元件{#components-of-merge-policies}

合併原則是IMS組織專用的，可讓您建立不同的原則，以所需的特定方式合併結構。 任何存取[!DNL Profile]資料的API都需要合併原則，但如果未明確提供預設原則，則會使用預設原則。 [!DNL Platform] 為組織提供預設的合併原則，或者您可以為特定的「體驗資料模型」(XDM)架構類別建立合併原則，並將其標籤為組織的預設。

雖然每個組織每個方案類可能有多個合併策略，但每個類只能有一個預設合併策略。 在提供方案類名和需要但未提供合併策略的情況下，將使用任何預設設定的合併策略。

>[!NOTE]
>
>當您將新合併策略設定為預設值時，先前設定為預設值的任何現有合併策略都將自動更新為不再用作預設值。

### 完整合併策略對象

完整的合併策略對象表示一組控制合併配置檔案片段的偏好。

**合併策略對象**

```json
    {
        "id": "{MERGE_POLICY_ID}",
        "name": "{NAME}",
        "imsOrgId": "{IMS_ORG}",
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
        "default": "{BOOLEAN}",
        "updateEpoch": "{UPDATE_TIME}"
    }
```

| 屬性 | 說明 |
|---|---|
| `id` | 系統生成在建立時分配的唯一標識符 |
| `name` | 可在清單檢視中識別合併原則的好記名稱。 |
| `imsOrgId` | 此合併策略所屬的組織ID |
| `identityGraph` | [標識](#identity-graph) 圖形對象，指示將從中獲取相關標識的身份圖。將合併所有相關身份的配置檔案片段。 |
| `attributeMerge` | [屬](#attribute-merge) 性mergeobject，指出在發生資料衝突時合併原則會依其方式來排列描述檔屬性的優先順序。 |
| `schema.name` | 作為[`schema`](#schema)對象的一部分，`name`欄位包含與合併策略相關的XDM方案類。 有關方案和類的詳細資訊，請閱讀[XDM文檔](../../xdm/home.md)。 |
| `default` | 指示此合併策略是否為指定方案的預設布爾值。 |
| `version` | [!DNL Platform] 合併策略的維護版本。每當合併策略更新時，此唯讀值都會增加。 |
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

### 身份圖{#identity-graph}

[Adobe Experience Platform身](../../identity-service/home.md) 分服務管理全球及每個組織使用的身分圖表 [!DNL Experience Platform]。合併策略的`identityGraph`屬性定義了如何確定用戶的相關身份。

**identityGraph物件**

```json
    "identityGraph": {
        "type": "{IDENTITY_GRAPH_TYPE}"
    }
```

其中`{IDENTITY_GRAPH_TYPE}`是下列其中一項：

* **&quot;none&quot;：不** 執行身份聯繫。
* **&quot;pdg&quot;：根** 據您的私人身分圖表執行身分聯繫。

**範例`identityGraph`**

```json
    "identityGraph": {
        "type": "pdg"
    }
```

### 屬性合併{#attribute-merge}

描述檔片段是特定使用者在身分清單中僅有一個身分的描述檔資訊。 當使用身份圖形類型導致多個身份時，可能存在衝突的配置檔案屬性，必須指定優先順序。 使用`attributeMerge`，您可以指定在關鍵值（記錄資料）類型資料集之間發生合併衝突時要優先排序的配置檔案屬性。

**attributeMerge物件**

```json
    "attributeMerge": {
        "type": "{ATTRIBUTE_MERGE_TYPE}"
    }
```

其中`{ATTRIBUTE_MERGE_TYPE}`是下列其中一項：

* **`timestampOrdered`**:（預設）為上次更新的設定檔指定優先順序。使用此合併類型時，不需要`data`屬性。 `timestampOrdered` 也支援在資料集內或跨資料集合併描述檔片段時優先使用的自訂時間戳記。如需詳細資訊，請參閱[使用自訂時間戳記](#custom-timestamps)的附錄一節。
* **`dataSetPrecedence`** :根據個人資料片段的來源資料集，為描述檔片段提供優先順序。當一個資料集中的資訊比另一個資料集的資料更偏好或受信任時，就可使用此功能。 使用此合併類型時，`order`屬性是必需的，因為它按優先順序順序列出資料集。
   * **`order`**:使用&quot;dataSetPrecense&quot;時，必須 `order` 向陣列提供資料集清單。清單中未包含的任何資料集都不會合併。 換言之，必須明確列出資料集才能合併至描述檔。 `order`陣列按優先順序列出資料集的ID。

#### 使用`dataSetPrecedence`類型的`attributeMerge`對象示例

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

#### 使用`timestampOrdered`類型的`attributeMerge`對象示例

```json
    "attributeMerge": {
        "type": "timestampOrdered"
    }
```

### 結構 {#schema}

架構對象指定為此合併策略建立的Experience Data Model(XDM)架構類。

**`schema`物件**

```json
    "schema": {
        "name": "{SCHEMA_NAME}"
    }
```

其中，`name`的值是與合併策略關聯的模式所基於的XDM類的名稱。

**範例`schema`**

```json
    "schema": {
        "name": "_xdm.context.profile"
    }
```

要瞭解有關XDM和在Experience Platform中使用架構的更多資訊，請首先閱讀[XDM系統概述](../../xdm/home.md)。

## 訪問合併策略{#access-merge-policies}

使用[!DNL Real-time Customer Profile] API, `/config/mergePolicies`端點可讓您執行查閱請求，以依其ID檢視特定合併原則，或存取IMS組織中依特定條件篩選的所有合併原則。 您也可以使用`/config/mergePolicies/bulk-get`端點，通過其ID檢索多個合併策略。 以下各節將說明執行這些呼叫的步驟。

### 依ID存取單一合併原則

通過向`/config/mergePolicies`端點發出GET請求並在請求路徑中包括`mergePolicyId`，可以通過其ID訪問單個合併策略。

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

有關組成合併策略的各個元素的詳細資訊，請參閱本文檔開頭的[合併策略的元件](#components-of-merge-policies)部分。

### 根據多個合併策略的ID檢索多個合併策略

通過向`/config/mergePolicies/bulk-get`端點發出POST請求並在請求主體中包括要檢索的合併策略的ID，可以檢索多個合併策略。

**API格式**

```http
POST /config/mergePolicies/bulk-get
```

**要求**

請求主體包含一個「ids」陣列，其中包含您要擷取詳細資料之每個合併原則的「id」個別物件。

```shell
curl -X POST \
  'https://platform.adobe.io/data/core/ups/config/mergePolicies/bulk-get' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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

成功的回應會傳回「HTTP狀態207」（多重狀態），以及合併原則的詳細資訊，這些原則的ID已在POST請求中提供。

```json
{ 
    "results": { 
        "0bf16e61-90e9-4204-b8fa-ad250360957b": {
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
        "42d4a596-b1c6-46c0-994e-ca5ef1f85130": {
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
    }
}
```

有關組成合併策略的各個元素的詳細資訊，請參閱本文檔開頭的[合併策略的元件](#components-of-merge-policies)部分。

### 按標準列出多個合併策略

您可以在IMS組織中，向`/config/mergePolicies`端點發出GET請求，並使用可選查詢參數來篩選、排序和分頁回應，以列出多個合併原則。 可包含多個參數，以&amp;符號分隔。 在沒有參數的情況下呼叫此端點將會擷取組織所有可用的合併原則。

**API格式**

```http
GET /config/mergePolicies?{QUERY_PARAMS}
```

| 參數 | 說明 |
|---|---|
| `default` | 一個布爾值，它根據合併策略是否是模式類的預設策略來過濾結果。 |
| `limit` | 指定頁面大小限制，以控制包含在頁面中的結果數。 預設值：20 |
| `orderBy` | 指定將結果排序（如`orderBy=name`或`orderBy=+name`）的欄位，以按名稱的升序排序，或按`orderBy=-name`的降序排序。 省略此值會導致預設排序`name`的遞增順序。 |
| `schema.name` | 要為其檢索可用合併策略的方案的名稱。 |
| `identityGraph.type` | 依身分圖形類型篩選結果。 可能的值包括「無」和「pdg」（專用圖形）。 |
| `attributeMerge.type` | 依使用的屬性合併類型篩選結果。 可能的值包括&quot;timestampOrdered&quot;和&quot;dataSetPrecense&quot;。 |
| `start` | 頁面偏移——指定要擷取資料的起始ID。 預設值：0 |
| `version` | 如果您想要使用特定版本的合併原則，請指定此選項。 依預設，會使用最新版本。 |

有關`schema.name`、`identityGraph.type`和`attributeMerge.type`的詳細資訊，請參閱本指南前面提供的[合併策略的元件](#components-of-merge-policies)部分。


**要求**

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

通過向`/config/mergePolicies`端點發出POST請求，可以為組織建立新的合併策略。

**API格式**

```http
POST /config/mergePolicies
```

**請**
求以下請求會建立新的合併原則，由裝載中提供的屬性值設定：

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

有關詳細資訊，請參閱合併策略的[元件](#components-of-merge-policies)部分。

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

有關組成合併策略的各個元素的詳細資訊，請參閱本文檔開頭的[合併策略的元件](#components-of-merge-policies)部分。

## 更新合併策略{#update}

您可以通過編輯單個屬性(PATCH)或用新屬性(PUT)覆寫整個合併策略來修改現有的合併策略。 各示例如下所示。

### 編輯個別合併原則欄位

通過向`/config/mergePolicies/{mergePolicyId}`端點發出PATCH請求，可以編輯合併策略的各個欄位：

**API格式**

```http
PATCH /config/mergePolicies/{mergePolicyId}
```

| 參數 | 說明 |
|---|---|
| `{mergePolicyId}` | 要刪除的合併策略的標識符。 |

**要求**

以下請求通過將其`default`屬性的值更改為`true`來更新指定的合併策略：

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
| `op` | 指定要執行的操作。 其他PATCH操作的範例可在[JSON修補程式檔案](http://jsonpatch.com)中找到 |
| `path` | 要更新的欄位路徑。 接受的值為：&quot;/name&quot;、&quot;/identityGraph.type&quot;、&quot;/attributeMerge.type&quot;、&quot;/schema.name&quot;、&quot;/version&quot;、&quot;/default&quot; |
| `value` | 將指定欄位設定為的值。 |

有關詳細資訊，請參閱合併策略的[元件](#components-of-merge-policies)部分。


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

**要求**

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

有關詳細資訊，請參閱合併策略的[元件](#components-of-merge-policies)部分。


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

通過向`/config/mergePolicies`端點發出DELETE請求並在請求路徑中包括要刪除的合併策略的ID，可以刪除合併策略。

**API格式**

```http
DELETE /config/mergePolicies/{mergePolicyId}
```

| 參數 | 說明 |
|---|---|
| `{mergePolicyId}` | 要刪除的合併策略的標識符。 |

**要求**

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

現在您知道如何為組織建立和設定合併原則，您可以使用這些原則來調整平台中客戶個人檔案的檢視，並從您的[!DNL Real-time Customer Profile]資料建立受眾區段。 請參閱[Adobe Experience Platform區段服務檔案](../../segmentation/home.md)，開始定義和使用區段。

## 附錄

本節提供與使用合併策略有關的補充資訊。

### 使用自訂時間戳記{#custom-timestamps}

當記錄被吸收到Experience Platform中時，在吸收時獲得系統時間戳並添加到記錄中。 當`timestampOrdered`被選為合併策略的`attributeMerge`類型時，將根據系統時間戳合併配置檔案。 換言之，合併是根據記錄被收錄到平台的時間戳記進行。

有時候，可能會有使用案例，例如回填資料，或在記錄未依順序擷取時，確保事件的正確順序，而需要提供自訂時間戳記，並讓合併原則遵守自訂時間戳記，而非系統時間戳記。

要使用自定義時間戳，[[!DNL External Source System Audit Details] 架構欄位組](#field-group-details)必須添加到您的配置檔案架構中。 新增後，可使用`xdm:lastUpdatedDate`欄位填入自訂時間戳記。 在`xdm:lastUpdatedDate`欄位填入記錄時，Experience Platform會使用該欄位來合併資料集內或跨資料集的記錄或描述檔片段。 如果`xdm:lastUpdatedDate`不存在或未填入，平台將繼續使用系統時間戳記。

>[!NOTE]
>
>在同一記錄上發送PATCH時，必須確保填入`xdm:lastUpdatedDate`時間戳。

有關使用方案註冊表API使用方案的逐步說明，包括如何向方案添加欄位組，請訪問[教程，以使用API](../../xdm/tutorials/create-schema-api.md)建立方案。

要使用UI使用自訂時間戳記，請參閱[合併原則使用指南](../ui/merge-policies.md)中使用自訂時間戳記[一節。](../ui/merge-policies.md#custom-timestamps)

#### [!DNL External Source System Audit Details] 欄位組詳細資訊  {#field-group-details}

以下範例顯示[!DNL External Source System Audit Details]欄位群組中正確填入的欄位。 完整欄位群組JSON也可在GitHub上的[public Experience Data Model(XDM)repo](https://github.com/adobe/xdm/blob/master/components/mixins/shared/external-source-system-audit-details.schema.json)中檢視。

```json
{
  "xdm:createdBy": "{CREATED_BY}",
  "xdm:createdDate": "2018-01-02T15:52:25+00:00",
  "xdm:lastUpdatedBy": "{LAST_UPDATED_BY}",
  "xdm:lastUpdatedDate": "2018-01-02T15:52:25+00:00",
  "xdm:lastActivityDate": "2018-01-02T15:52:25+00:00",
  "xdm:lastReferencedDate": "2018-01-02T15:52:25+00:00",
  "xdm:lastViewedDate": "2018-01-02T15:52:25+00:00"
 }
```
