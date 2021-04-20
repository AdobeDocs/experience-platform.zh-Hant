---
keywords: Experience Platform;Profile；即時客戶配置檔案；故障排除；API
title: 計算屬性API端點
topic: guide
type: Documentation
description: 在Adobe Experience Platform中，計算屬性是用來將事件層級資料匯整為描述檔層級屬性的函式。 這些函式會自動計算，以便跨區段、啟動和個人化使用。 本指南說明如何使用即時客戶描述檔API來建立、檢視、更新和刪除計算的屬性。
translation-type: tm+mt
source-git-commit: 4ed2b80ebfd87f8920462ae0a918b01bb13d4210
workflow-type: tm+mt
source-wordcount: '2279'
ht-degree: 2%

---


# (Alpha)計算屬性API端點

>[!IMPORTANT]
>
>本文中概述的計算屬性功能目前為alpha格式，並非所有使用者都能使用。 文件和功能可能會有所變更。

計算屬性是用於將事件級別資料聚合到配置檔案級別屬性的函式。 這些函式會自動計算，以便跨區段、啟動和個人化使用。 本指南包含使用`/computedAttributes`端點執行基本CRUD操作的範例API調用。

若要進一步瞭解計算屬性，請先閱讀[計算屬性概述](overview.md)。

## 快速入門

本指南中使用的API端點是[即時客戶設定檔API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/real-time-customer-profile.yaml)的一部分。

在繼續之前，請先閱讀[描述檔API快速入門手冊](../api/getting-started.md)，以取得建議檔案的連結、閱讀本檔案中顯示之範例API呼叫的指南，以及成功呼叫任何Experience Platform API所需之必要標題的重要資訊。

## 配置計算屬性欄位

為了建立計算屬性，首先需要標識將保存計算屬性值的方案中的欄位。

請參閱[配置計算屬性](configure-api.md)的文檔，以獲得在架構中建立計算屬性欄位的完整端到端指南。

>[!WARNING]
>
>為了繼續使用API指南，您必須配置了計算屬性欄位。

## 建立計算屬性{#create-a-computed-attribute}

在啟用配置檔案的方案中定義計算屬性欄位後，您現在可以配置計算屬性。 如果您尚未執行此操作，請遵循[配置計算屬性](configure-api.md)文檔中概述的工作流。

要建立計算屬性，首先對`/config/computedAttributes`端點發出POST請求，請求主體包含要建立的計算屬性的詳細資訊。

**API格式**

```http
POST /config/computedAttributes
```

**請求**

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/config/computedAttributes \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}'\
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "name" : "birthdayCurrentMonth",
        "path" : "_{TENANT_ID}",
        "description" : "Computed attribute to capture if the customer birthday is in the current month.",
        "expression" : {
            "type" : "PQL", 
            "format" : "pql/text", 
            "value":  "person.birthDate.getMonth() = currentMonth()"
        },
        "schema": 
          {
            "name":"_xdm.context.profile"
          }
          
      }'
```

| 屬性 | 說明 |
|---|---|
| `name` | 計算屬性欄位的名稱，作為字串。 |
| `path` | 包含計算屬性的欄位的路徑。 此路徑位於架構的`properties`屬性中，不應在路徑中包含欄位名稱。 寫入路徑時，請忽略`properties`屬性的多個級別。 |
| `{TENANT_ID}` | 如果您不熟悉您的租用戶ID，請參閱[架構註冊開發人員指南](../../xdm/api/getting-started.md#know-your-tenant_id)中尋找租用戶ID的步驟。 |
| `description` | 計算屬性的說明。 當定義了多個計算屬性後，這特別有用，因為它將幫助IMS組織中的其他人決定要使用的正確計算屬性。 |
| `expression.value` | 有效的[!DNL Profile Query Language](PQL)表達式。 計算屬性當前支援以下函式：sum、count、min、max和boolean。 有關示例表達式的清單，請參閱[示例PQL表達式](expressions.md)文檔。 |
| `schema.name` | 包含計算屬性欄位的方案所基於的類。 範例：`_xdm.context.experienceevent`，用於基於XDM ExperienceEvent類的架構。 |

**回應**

成功建立的計算屬性返回HTTP狀態200(OK)，並返回包含新建計算屬性詳細資訊的響應主體。 這些詳細資訊包括唯一、唯讀、系統產生的`id`，可用於在其他API操作期間參考計算的屬性。

```json
{
    "id": "2afcf410-450e-4a39-984d-2de99ab58877",
    "imsOrgId": "{IMS_ORG}",
    "sandbox": {
        "sandboxId": "{SANDBOX_ID}",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "name": "birthdayCurrentMonth",
    "path": "_{TENANT_ID}",
    "positionPath": [
        "_{TENANT_ID}"
    ],
    "description": "Computed attribute to capture if the customer birthday is in the current month.",
    "expression": {
        "type": "PQL",
        "format": "pql/text",
        "value": "person.birthDate.getMonth() = currentMonth()"
    },
    "schema": {
        "name": "_xdm.context.profile"
    },
    "returnSchema": {
        "meta:xdmType": "string"
    },
    "definedOn": [
        {
            "meta:resourceType": "unions",
            "meta:containerId": "tenant",
            "$ref": "https://ns.adobe.com/xdm/context/profile__union"
        }
    ],
    "encodedDefinedOn":"?\b?VR)JMS?R?())(????+?KL?OJ?K???H??O??+I?(?/(?O??I??/????S?8{?E:",
    "dependencies": [],
    "dependents": [],
    "active": true,
    "type": "ComputedAttribute",
    "createEpoch": 1572555223,
    "updateEpoch": 1572555225
}
```

| 屬性 | 說明 |
|---|---|
| `id` | 唯一、唯讀、系統產生的ID，可用於在其他API操作期間引用計算的屬性。 |
| `imsOrgId` | 與計算屬性相關的IMS組織應符合在請求中傳送的值。 |
| `sandbox` | 沙盒物件包含沙盒的詳細資訊，此沙盒已設定計算屬性。 這項資訊是從請求中傳送的沙盒標題中擷取。 如需詳細資訊，請參閱[沙盒概述](../../sandboxes/home.md)。 |
| `positionPath` | 包含解構`path`的陣列，會傳送至請求中傳送的欄位。 |
| `returnSchema.meta:xdmType` | 儲存計算屬性的欄位的類型。 |
| `definedOn` | 顯示已定義計算屬性的聯合方案的陣列。 每個聯合方案包含一個對象，這表示如果計算的屬性已根據不同的類添加到多個方案，則陣列中可能有多個對象。 |
| `active` | 顯示計算屬性當前是否處於活動狀態的布爾值。 預設值為`true`。 |
| `type` | 建立的資源類型（在本例中為「ComputedAttribute」）是預設值。 |
| `createEpoch` 和 `updateEpoch` | 計算屬性的建立時間和上次更新時間。 |

## 建立引用現有計算屬性的計算屬性

還可以建立引用現有計算屬性的計算屬性。 若要這麼做，請先向`/config/computedAttributes`端點發出POST請求。 請求主體將在`expression.value`欄位中包含對計算屬性的引用，如下例所示。

**API格式**

```http
POST /config/computedAttributes
```

**請求**

在此示例中，已建立了兩個計算屬性，並將用於定義第三個屬性。 現有的計算屬性包括：

* **`totalSpend`:** 擷取客戶已花費的總金額。
* **`countPurchases`:** 計算客戶已購買的數量。

以下請求引用兩個現有的計算屬性，使用有效的PQL進行除法以計算新的`averageSpend`計算屬性。

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/config/computedAttributes \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}'\
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "name" : "averageSpend",
        "path" : "_{TENANT_ID}.purchaseSummary",
        "description" : "Computed attribute to capture the average dollar amount that a customer spends on each purchase.",
        "expression" : {
            "type" : "PQL", 
            "format" : "pql/text", 
            "value":  "_{TENANT_ID}.purchaseSummary.totalSpend/_{TENANT_ID}.purchaseSummary.countPurchases"
        },
        "schema": 
          {
            "name":"_xdm.context.profile"
          }
          
      }'
```

| 屬性 | 說明 |
|---|---|
| `name` | 計算屬性欄位的名稱，作為字串。 |
| `path` | 包含計算屬性的欄位的路徑。 此路徑位於架構的`properties`屬性中，不應在路徑中包含欄位名稱。 寫入路徑時，請忽略`properties`屬性的多個級別。 |
| `{TENANT_ID}` | 如果您不熟悉您的租用戶ID，請參閱[架構註冊開發人員指南](../../xdm/api/getting-started.md#know-your-tenant_id)中尋找租用戶ID的步驟。 |
| `description` | 計算屬性的說明。 當定義了多個計算屬性後，這特別有用，因為它將幫助IMS組織中的其他人決定要使用的正確計算屬性。 |
| `expression.value` | 有效的PQL表達式。 計算屬性當前支援以下函式：sum、count、min、max和boolean。 有關示例表達式的清單，請參閱[示例PQL表達式](expressions.md)文檔。<br/><br/>在此示例中，表達式引用兩個現有的計算屬性。使用計算屬性的`path`和`name`引用屬性，如同它們在定義計算屬性的模式中顯示一樣。 例如，第一個引用的計算屬性的`path`是`_{TENANT_ID}.purchaseSummary`，而`name`是`totalSpend`。 |
| `schema.name` | 包含計算屬性欄位的方案所基於的類。 範例：`_xdm.context.experienceevent`，用於基於XDM ExperienceEvent類的架構。 |

**回應**

成功建立的計算屬性返回HTTP狀態200(OK)，並返回包含新建計算屬性詳細資訊的響應主體。 這些詳細資訊包括唯一、唯讀、系統產生的`id`，可用於在其他API操作期間參考計算的屬性。

```json
{
    "id": "2afcf410-450e-4a39-984d-2de99ab58877",
    "imsOrgId": "{IMS_ORG}",
    "sandbox": {
        "sandboxId": "{SANDBOX_ID}",
        "sandboxName": "{SANDBOX_NAME}",
        "type": "production",
        "default": true
    },
    "name": "averageSpend",
    "path": "_{TENANT_ID}.purchaseSummary",
    "positionPath": [
        "_{TENANT_ID}",
        "purchaseSummary"
    ],
    "description": "Computed attribute to capture the average dollar amount that a customer spends on each purchase.",
    "expression" : {
            "type" : "PQL", 
            "format" : "pql/text", 
            "value":  "_{TENANT_ID}.purchaseSummary.totalSpend/_{TENANT_ID}.purchaseSummary.countPurchases"
    },
    "schema": {
        "name": "_xdm.context.profile"
    },
    "returnSchema": {
        "meta:xdmType": "number"
    },
    "definedOn": [
        {
          "meta:resourceType": "unions",
          "meta:containerId": "tenant",
          "$ref": "https://ns.adobe.com/xdm/context/profile__union"
        }
    ],
    "encodedDefinedOn":"\bVR)JMSR())(+KLOJKկHO+I(/(OI/S8{E:",
    "dependencies": [
        "c08a92f3-2418-4a3d-89d0-96f15fda3e5d",
        "4ed9e3aa-57ae-4705-9e8a-7fba9a6a7010"
    ],
    "dependents": [],
    "active": true,
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
    "type": "ComputedAttribute",
    "createEpoch": 1613696592,
    "updateEpoch": 1613696593
}
```

| 屬性 | 說明 |
|---|---|
| `id` | 唯一、唯讀、系統產生的ID，可用於在其他API操作期間引用計算的屬性。 |
| `imsOrgId` | 與計算屬性相關的IMS組織應符合在請求中傳送的值。 |
| `sandbox` | 沙盒物件包含沙盒的詳細資訊，此沙盒已設定計算屬性。 這項資訊是從請求中傳送的沙盒標題中擷取。 如需詳細資訊，請參閱[沙盒概述](../../sandboxes/home.md)。 |
| `positionPath` | 包含解構`path`的陣列，會傳送至請求中傳送的欄位。 |
| `returnSchema.meta:xdmType` | 儲存計算屬性的欄位的類型。 |
| `definedOn` | 顯示已定義計算屬性的聯合方案的陣列。 每個聯合方案包含一個對象，這表示如果計算的屬性已根據不同的類添加到多個方案，則陣列中可能有多個對象。 |
| `active` | 顯示計算屬性當前是否處於活動狀態的布爾值。 預設值為`true`。 |
| `type` | 建立的資源類型（在本例中為「ComputedAttribute」）是預設值。 |
| `createEpoch` 和 `updateEpoch` | 計算屬性的建立時間和上次更新時間。 |

## 訪問計算屬性

使用API處理計算屬性時，有兩個選項用於訪問您的組織已定義的計算屬性。 第一個是列出所有計算屬性，第二個是按其唯一`id`查看特定計算屬性。

本文檔概述了兩種訪問模式的步驟。 選擇以下選項之一開始：

* **[列出所有現有計算屬性](#list-all-computed-attributes):** 返回組織已建立的所有現有計算屬性的清單。
* **[檢視特定計算屬性](#view-a-computed-attribute):** 在請求期間指定單一計算屬性的ID，以傳回其詳細資料。

### 列出所有計算屬性{#list-all-computed-attributes}

您的IMS組織可以建立多個計算屬性，並對`/config/computedAttributes`端點執行GET請求，允許您列出組織的所有現有計算屬性。

**API格式**

```http
GET /config/computedAttributes
```

**請求**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/config/computedAttributes/ \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \ 
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**回應**

成功響應包括`_page`屬性，該屬性提供計算屬性的總數(`totalCount`)和頁上計算屬性的數(`pageSize`)。

該響應還包括由一個或多個對象組成的`children`陣列，每個對象包含一個計算屬性的詳細資訊。 如果您的組織沒有任何計算屬性，則`totalCount`和`pageSize`將為0（零），而`children`陣列將為空。

```json
{
    "_page": {
        "totalCount": 2,
        "pageSize": 2
    },
    "children": [
        {
            "id": "2afcf410-450e-4a39-984d-2de99ab58877",
            "imsOrgId": "{IMS_ORG}",
            "sandbox": {
                "sandboxId": "ff0f6870-c46d-11e9-8ca3-036939a64204",
                "sandboxName": "prod",
                "type": "production",
                "default": true
            },
            "name": "birthdayCurrentMonth",
            "path": "person._{TENANT_ID}",
            "positionPath": [
                "person",
                "_{TENANT_ID}"
            ],
            "description": "Computed attribute to capture if the customer birthday is in the current month.",
            "expression": {
                "type": "PQL",
                "format": "pql/text",
                "value": "person.birthDate.getMonth() = currentMonth()"
            },
            "schema": {
                "name": "_xdm.context.profile"
            },
            "returnSchema": {
                "meta:xdmType": "string"
            },
            "definedOn": [
                {
                    "meta:resourceType": "unions",
                    "meta:containerId": "tenant",
                    "$ref": "https://ns.adobe.com/xdm/context/profile__union"
                }
            ],
            "encodedDefinedOn":"?\b?VR)JMS?R?())(????+?KL?OJ?K???H??O??+I?(?/(?O??I??/????S?8{?E:",
            "dependencies": [],
            "dependents": [],
            "active": true,
            "type": "ComputedAttribute",
            "createEpoch": 1572555223,
            "updateEpoch": 1572555225
        },
        {
            "id": "ae0c6552-cf49-4725-8979-116366e8e8d3",
            "imsOrgId": "{IMS_ORG}",
            "sandbox": {
                "sandboxId": "",
                "sandboxName": "",
                "type": "production",
                "default": true
            },
            "name": "productDownloads",
            "path": "_{TENANT_ID}",
            "positionPath": [
                "_{TENANT_ID}"
            ],
            "description": "Calculate total product downloads.",
            "expression": {
                "type" : "PQL", 
                "format" : "pql/text", 
                "value":  "let Y = xEvent[_coresvc.event.subType = \"DOWNLOAD\"].groupBy(_coresvc.attributes[name = \"product\"].value).map({
                  \"downloaded\": this.head()._coresvc.attributes[name = \"product\"].head().value,
                  \"downloadsSum\": this.count(),
                  \"downloadsToday\": this[timestamp occurs today].count(),
                  \"downloadsPast30Days\": this[timestamp occurs < 30 days before now].count(),
                  \"downloadsPast60Days\": this[timestamp occurs < 60 days before now].count(),
                  \"downloadsPast90Days\": this[timestamp occurs < 90 days before now].count() }) in { \"uniqueProductDownloadSum\": Y.count(), \"products\": Y }"
            },
            "returnSchema": {
                "meta:xdmType": "string"
            },
            "definedOn": [
                {
                    "meta:resourceType": "unions",
                    "meta:containerId": "tenant",
                    "$ref": "https://ns.adobe.com/xdm/context/profile__union"
                }
            ],
            "schema": {
                "name": "_xdm.context.profile"
            },
            "encodedDefinedOn": "\u001f?\b\u0000\u0000\u0000\u0000\u0000\u0000\u0000?VR)JMS?R?())(????+?KL?OJ?K???H??O??+I?(?/(?O??I??/????S?\u0005\u00008{?E:\u0000\u0000\u0000",
            "dependencies": [],
            "dependents": [],
            "active": true,
            "type": "ComputedAttribute",
            "createEpoch": 1571945277,
            "updateEpoch": 1571945280
        }
    ],
    "_links": {
        "next": {}
    }
}
```

| 屬性 | 說明 |
|---|---|
| `_page.totalCount` | 由IMS組織定義的計算屬性總數。 |
| `_page.pageSize` | 在此結果頁返回的計算屬性數。 如果`pageSize`等於`totalCount`，表示只有一頁結果，且所有計算屬性都已傳回。 如果結果不相等，則可存取其他頁面的結果。 如需詳細資訊，請參閱`_links.next`。 |
| `children` | 由一個或多個對象組成的陣列，每個對象包含單個計算屬性的詳細資訊。 如果未定義任何計算屬性，則`children`陣列為空。 |
| `id` | 建立計算屬性時自動分配給其的唯一隻讀系統生成值。 有關計算屬性對象的元件的詳細資訊，請參閱本教程前面有關建立計算屬性的[一節。](#create-a-computed-attribute) |
| `_links.next` | 如果傳回單一頁的計算屬性，`_links.next`是空物件，如上述範例回應所示。 如果您的組織有許多計算屬性，則會在您可以透過對`_links.next`值提出GET請求而存取的多個頁面上傳回這些屬性。 |

### 查看計算屬性{#view-a-computed-attribute}

通過向`/config/computedAttributes`端點發出GET請求並在請求路徑中包含計算屬性ID，可以查看特定的計算屬性。

**API格式**

```http
GET /config/computedAttributes/{ATTRIBUTE_ID}
```

| 參數 | 說明 |
|---|---|
| `{ATTRIBUTE_ID}` | 要查看的計算屬性的ID。 |

**請求**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/config/computedAttributes/2afcf410-450e-4a39-984d-2de99ab58877 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \ 
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**回應**

```json
{
    "id": "2afcf410-450e-4a39-984d-2de99ab58877",
    "imsOrgId": "{IMS_ORG}",
    "sandbox": {
        "sandboxId": "ff0f6870-c46d-11e9-8ca3-036939a64204",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "name": "birthdayCurrentMonth",
    "path": "_{TENANT_ID}",
    "positionPath": [
        "_{TENANT_ID}"
    ],
    "description": "Computed attribute to capture if the customer birthday is in the current month.",
    "expression": {
        "type": "PQL",
        "format": "pql/text",
        "value": "person.birthDate.getMonth() = currentMonth()"
    },
    "schema": {
        "name": "_xdm.context.profile"
    },
    "returnSchema": {
        "meta:xdmType": "string"
    },
    "definedOn": [
        {
            "meta:resourceType": "unions",
            "meta:containerId": "tenant",
            "$ref": "https://ns.adobe.com/xdm/context/profile__union"
        }
    ],
    "encodedDefinedOn":"?\b?VR)JMS?R?())(????+?KL?OJ?K???H??O??+I?(?/(?O??I??/????S?8{?E:",
    "dependencies": [],
    "dependents": [],
    "active": true,
    "type": "ComputedAttribute",
    "createEpoch": 1572555223,
    "updateEpoch": 1572555225
}
```

## 更新計算屬性

如果您發現需要更新現有的計算屬性，可以通過向`/config/computedAttributes`端點發出PATCH請求並在請求路徑中包括要更新的計算屬性的ID來完成此操作。

**API格式**

```http
PATCH /config/computedAttributes/{ATTRIBUTE_ID}
```

| 參數 | 說明 |
|---|---|
| `{ATTRIBUTE_ID}` | 您要更新的計算屬性的ID。 |

**請求**

此請求使用[JSON修補程式格式](http://jsonpatch.com/)來更新「運算式」欄位的「值」。

```shell
curl -X PATCH \
  https://platform.adobe.io/data/core/ups/config/computedAttributes/ae0c6552-cf49-4725-8979-116366e8e8d3 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}'\
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \  
  -d '[
        {
          "op": "add",
          "path": "/expression",
          "value": 
          {
            "type" : "PQL", 
            "format" : "pql/text", 
            "value":  "{NEW_EXPRESSION_VALUE}"
          }
        }
      ]'
```

| 屬性 | 說明 |
|---|---|
| `{NEW_EXPRESSION_VALUE}` | 有效的[!DNL Profile Query Language](PQL)表達式。 計算屬性當前支援以下函式：sum、count、min、max和boolean。 有關示例表達式的清單，請參閱[示例PQL表達式](expressions.md)文檔。 |

**回應**

成功的更新會傳回HTTP狀態204（無內容）和空回應主體。 如果您想確認更新成功，可以執行GET請求，以依據其ID查看計算屬性。

## 刪除計算屬性

您也可以使用API刪除計算屬性。 這是通過向`/config/computedAttributes`端點發出DELETE請求並在請求路徑中包括要刪除的計算屬性的ID來完成的。

>[!NOTE]
>
>刪除計算屬性時請小心，因為該屬性可能在多個方案中使用，且DELETE操作無法撤消。

**API格式**

```http
DELETE /config/computedAttributes/{ATTRIBUTE_ID}
```

| 參數 | 說明 |
|---|---|
| `{ATTRIBUTE_ID}` | 要刪除的計算屬性的ID。 |

**請求**

```shell
curl -X DELETE \
  https://platform.adobe.io/data/core/ups/config/computedAttributes/ae0c6552-cf49-4725-8979-116366e8e8d3 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}'
  -H 'x-sandbox-name: {SANDBOX_NAME}' \ 
```

**回應**

成功的刪除請求會傳回HTTP狀態200（確定）和空回應主體。 若要確認刪除成功，您可以執行GET請求，以依其ID查閱計算的屬性。 如果刪除了屬性，您會收到HTTP狀態404（找不到）錯誤。

## 建立引用計算屬性的段定義

Adobe Experience Platform可讓您建立區段，從一組描述檔定義一組特定屬性或行為。 段定義包括用於封裝在PQL中寫入的查詢的表達式。 這些表達式還可以引用計算屬性。

下面的示例建立引用現有計算屬性的段定義。 若要進一步瞭解區段定義，以及如何在區段服務API中使用區段定義，請參閱[區段定義API端點指南](../../segmentation/api/segment-definitions.md)。

首先，向`/segment/definitions`端點發出POST請求，在請求主體中提供計算屬性。

**API格式**

```http
POST /segment/definitions
```

**請求**

```shell
curl -X POST https://platform.adobe.io/data/core/ups/segment/definitions
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '{
        "name": "downloadedInLast7Days",
        "description": "Has product been downloaded in last 7 days?",
        "schema": {
            "name": "_xdm.context.profile"
        },
        "ttlInDays": 30,
        "expression": {
            "type": "PQL",
            "format": "pql/text",
            "value": "_{TENANT_ID}.downloadsLast7Days > 0",
            "meta": "m"
        },
        "dataGovernancePolicy": {
            "excludeOptOut": true
        }
    }'
```

| 屬性 | 說明 |
| -------- | ----------- |
| `name` | 區段的唯一名稱，以字串形式顯示。 |
| `description` | 定義的人類可讀描述。 |
| `schema.name` | 與區段中的實體關聯的架構。 包含`id`或`name`欄位。 |
| `expression` | 包含欄位的對象，其中包含有關段定義的資訊。 |
| `expression.type` | 指定表達式類型。 目前僅支援「PQL」。 |
| `expression.format` | 指示值中表達式的結構。 目前僅支援`pql/text`。 |
| `expression.value` | 有效的PQL表達式，在此示例中它包括對現有計算屬性的引用。 |

有關架構定義屬性的詳細資訊，請參閱[段定義API端點指南](../../segmentation/api/segment-definitions.md)中提供的示例。

**回應**

成功的回應會傳回HTTP狀態200，並包含您新建立之區段定義的詳細資訊。 若要進一步瞭解區段定義回應物件，請參閱[區段定義API端點指南](../../segmentation/api/segment-definitions.md)。

```json
{
    "id": "add3933f-ac5c-4240-8259-3a4528ee4885",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "ttlInDays": 60,
    "id": "119835c3-5fab-4c18-ae01-4ccab328fc5c",
    "imsOrgId": "{IMS_ORG}",
    "sandbox": {
        "sandboxId": "{SANDBOX_ID}",
        "sandboxName": "{SANDBOX_NAME}",
        "type": "production",
        "default": true
    },
    "name": "segment-downloadedInLast7Days",
    "description": "Has product been downloaded in last 7 days?",
    "expression": {
        "type": "PQL",
        "format": "pql/text",
        "value": "_{TENANT_ID}.downloadsLast7Days > 0",
        "meta": "m"
    },
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
    "creationTime": 1602016581000,
    "updateEpoch": 1610609459,
    "updateTime": 1610609459000,
    "createEpoch": 1602016554,
    "_etag": "\"8b01611a-0000-0200-0000-5ffff3330000\"",
    "dependents": [
        "023d46c9-a27c-4ea9-a887-2c91ba83f2d1"
    ],
    "definedOn": [
        {
            "meta:resourceType": "unions",
            "meta:containerId": "tenant",
            "$ref": "https://ns.adobe.com/xdm/context/profile__union"
        }
    ],
    "dependencies": [
    "103d46c9-a27c-4ea9-a887-2c91ba83f2d1"
    ],
    "type": "SegmentDefinition"
}
```

## 後續步驟

現在您已瞭解計算屬性的基本知識，您可以開始為組織定義這些屬性。