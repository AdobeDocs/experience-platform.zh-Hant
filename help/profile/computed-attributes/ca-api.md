---
keywords: Experience Platform；配置；即時客戶配置；故障排除；API
title: 計算屬性API終結點
type: Documentation
description: 在Adobe Experience Platform，計算屬性是用於將事件級資料聚合到配置檔案級屬性中的函式。 這些函式被自動計算，以便可以跨分段、激活和個性化使用。 本指南說明如何使用Real-Time Customer Profile API建立、查看、更新和刪除計算屬性。
exl-id: 6b35ff63-590b-4ef5-ab39-c36c39ab1d58
hide: true
hidefromtoc: true
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '2274'
ht-degree: 2%

---

# (Alpha)計算屬性API終結點

>[!IMPORTANT]
>
>本文檔中概述的計算屬性功能當前位於Alpha中，並且不適用於所有用戶。 文件和功能可能會有所變更。

計算屬性是用於將事件級資料聚合到配置檔案級屬性中的函式。 這些函式被自動計算，以便可以跨分段、激活和個性化使用。 本指南包括使用 `/computedAttributes` 端點。

要瞭解有關計算屬性的詳細資訊，請首先閱讀 [計算屬性概述](overview.md)。

## 快速入門

本指南中使用的API終結點是 [即時客戶配置檔案API](https://www.adobe.com/go/profile-apis-en)。

在繼續之前，請查看 [配置檔案API入門指南](../api/getting-started.md) 有關指向推薦文檔的連結、閱讀本文檔中顯示的示例API調用的指南，以及有關成功調用任何Experience PlatformAPI所需的標頭的重要資訊。

## 配置計算屬性欄位

要建立計算屬性，首先需要標識將保存計算屬性值的架構中的欄位。

請參閱上 [配置計算屬性](configure-api.md) 的子目錄。

>[!WARNING]
>
>要繼續執行API指南，必須配置計算屬性欄位。

## 建立計算屬性 {#create-a-computed-attribute}

在啟用配置檔案的方案中定義了計算屬性欄位後，現在可以配置計算屬性。 如果您尚未完成此操作，請按照中概述的工作流操作 [配置計算屬性](configure-api.md) 文檔。

要建立計算屬性，請首先向 `/config/computedAttributes` 端點，請求主體包含要建立的計算屬性的詳細資訊。

**API格式**

```http
POST /config/computedAttributes
```

**要求**

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/config/computedAttributes \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}'\
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "name": "birthdayCurrentMonth",
        "path": "_{TENANT_ID}",
        "description": "Computed attribute to capture if the customer birthday is in the current month.",
        "expression": {
            "type": "PQL", 
            "format": "pql/text", 
            "value": "person.birthDate.getMonth() = currentMonth()"
        },
        "schema": 
          {
            "name":"_xdm.context.profile"
          }
          
      }'
```

| 屬性 | 說明 |
|---|---|
| `name` | 計算的屬性欄位的名稱（字串）。 |
| `path` | 包含計算屬性的欄位的路徑。 在 `properties` 架構的屬性，不應在路徑中包含欄位名。 寫入路徑時，忽略 `properties` 屬性。 |
| `{TENANT_ID}` | 如果您對租戶ID不熟悉，請參閱中查找租戶ID的步驟 [架構註冊表開發人員指南](../../xdm/api/getting-started.md#know-your-tenant_id)。 |
| `description` | 計算屬性的說明。 在定義了多個計算屬性後，此功能特別有用，因為它將幫助組織內的其他人確定要使用的正確計算屬性。 |
| `expression.value` | 有效 [!DNL Profile Query Language] (PQL)表達式。 計算屬性當前支援以下函式：sum、count、min、max和boolean。 有關示例表達式的清單，請參閱 [示例PQL表達式](expressions.md) 文檔。 |
| `schema.name` | 包含計算屬性欄位的架構所基於的類。 示例： `_xdm.context.experienceevent` 用於基於XDM ExperienceEvent類的架構。 |

**回應**

成功建立的計算屬性返回HTTP狀態200(OK)和包含新建立的計算屬性詳細資訊的響應主體。 這些詳細資訊包括唯一的只讀系統生成的 `id` 可用於在其他API操作期間引用計算屬性。

```json
{
    "id": "2afcf410-450e-4a39-984d-2de99ab58877",
    "imsOrgId": "{ORG_ID}",
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
| `id` | 唯一的只讀系統生成的ID，可用於在其它API操作期間引用計算的屬性。 |
| `imsOrgId` | 與計算屬性相關的IMS組織應與請求中發送的值匹配。 |
| `sandbox` | 沙盒對象包含在其中配置計算屬性的沙盒的詳細資訊。 此資訊是從請求中發送的沙盒標頭中提取的。 有關詳細資訊，請參閱 [箱概述](../../sandboxes/home.md)。 |
| `positionPath` | 包含被解構的 `path` 發送到請求中的欄位。 |
| `returnSchema.meta:xdmType` | 儲存計算屬性的欄位的類型。 |
| `definedOn` | 一個陣列，其中顯示已定義計算屬性的聯合架構。 每個聯合架構包含一個對象，這意味著如果計算的屬性已基於不同的類添加到多個架構中，則陣列中可能存在多個對象。 |
| `active` | 一個布爾值，顯示計算的屬性當前是否處於活動狀態。 預設情況下，值為 `true`。 |
| `type` | 建立的資源類型（在本例中為「ComputedAttribute」）為預設值。 |
| `createEpoch` 和 `updateEpoch` | 分別建立和上次更新計算屬性的時間。 |

## 建立引用現有計算屬性的計算屬性

也可以建立引用現有計算屬性的計算屬性。 為此，請首先向 `/config/computedAttributes` 端點。 請求正文將包含對 `expression.value` 欄位，如下例所示。

**API格式**

```http
POST /config/computedAttributes
```

**要求**

在此示例中，已建立兩個計算屬性，並將用於定義第三個屬性。 現有計算屬性包括：

* **`totalSpend`:** 捕獲客戶已花費的總美元金額。
* **`countPurchases`:** 計算客戶已進行的採購數。

下面的請求引用兩個現有計算屬性，使用有效的PQL進行分配以計算新屬性 `averageSpend` 計算屬性。

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/config/computedAttributes \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}'\
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "name": "averageSpend",
        "path": "_{TENANT_ID}.purchaseSummary",
        "description": "Computed attribute to capture the average dollar amount that a customer spends on each purchase.",
        "expression": {
            "type": "PQL", 
            "format": "pql/text", 
            "value": "_{TENANT_ID}.purchaseSummary.totalSpend/_{TENANT_ID}.purchaseSummary.countPurchases"
        },
        "schema": 
          {
            "name":"_xdm.context.profile"
          }
          
      }'
```

| 屬性 | 說明 |
|---|---|
| `name` | 計算的屬性欄位的名稱（字串）。 |
| `path` | 包含計算屬性的欄位的路徑。 在 `properties` 架構的屬性，不應在路徑中包含欄位名。 寫入路徑時，忽略 `properties` 屬性。 |
| `{TENANT_ID}` | 如果您對租戶ID不熟悉，請參閱中查找租戶ID的步驟 [架構註冊表開發人員指南](../../xdm/api/getting-started.md#know-your-tenant_id)。 |
| `description` | 計算屬性的說明。 在定義了多個計算屬性後，這特別有用，因為它將幫助IMS組織中的其他人確定要使用的正確計算屬性。 |
| `expression.value` | 有效的PQL表達式。 計算屬性當前支援以下函式：sum、count、min、max和boolean。 有關示例表達式的清單，請參閱 [示例PQL表達式](expressions.md) 文檔。<br/><br/>在此示例中，表達式引用兩個現有的計算屬性。 使用 `path` 和 `name` 在定義計算屬性的架構中顯示的計算屬性。 例如， `path` 第一個引用的計算屬性 `_{TENANT_ID}.purchaseSummary` 和 `name` 是 `totalSpend`。 |
| `schema.name` | 包含計算屬性欄位的架構所基於的類。 示例： `_xdm.context.experienceevent` 用於基於XDM ExperienceEvent類的架構。 |

**回應**

成功建立的計算屬性返回HTTP狀態200(OK)和包含新建立的計算屬性詳細資訊的響應主體。 這些詳細資訊包括唯一的只讀系統生成的 `id` 可用於在其他API操作期間引用計算屬性。

```json
{
    "id": "2afcf410-450e-4a39-984d-2de99ab58877",
    "imsOrgId": "{ORG_ID}",
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
    "expression": {
            "type": "PQL", 
            "format": "pql/text", 
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
| `id` | 唯一的只讀系統生成的ID，可用於在其它API操作期間引用計算的屬性。 |
| `imsOrgId` | 與計算屬性相關的IMS組織應與請求中發送的值匹配。 |
| `sandbox` | 沙盒對象包含在其中配置計算屬性的沙盒的詳細資訊。 此資訊是從請求中發送的沙盒標頭中提取的。 有關詳細資訊，請參閱 [箱概述](../../sandboxes/home.md)。 |
| `positionPath` | 包含被解構的 `path` 發送到請求中的欄位。 |
| `returnSchema.meta:xdmType` | 儲存計算屬性的欄位的類型。 |
| `definedOn` | 一個陣列，其中顯示已定義計算屬性的聯合架構。 每個聯合架構包含一個對象，這意味著如果計算的屬性已基於不同的類添加到多個架構中，則陣列中可能存在多個對象。 |
| `active` | 一個布爾值，顯示計算的屬性當前是否處於活動狀態。 預設情況下，值為 `true`。 |
| `type` | 建立的資源類型（在本例中為「ComputedAttribute」）為預設值。 |
| `createEpoch` 和 `updateEpoch` | 分別建立和上次更新計算屬性的時間。 |

## 訪問計算屬性

使用API處理計算屬性時，有兩個選項用於訪問您的組織定義的計算屬性。 第一種是列出所有計算屬性，第二種是通過特定計算屬性的唯一性來查看特定計算屬性 `id`。

本文檔概述了兩種訪問模式的步驟。 選擇以下選項之一開始：

* **[列出所有現有計算屬性](#list-all-computed-attributes):** 返回組織已建立的所有現有計算屬性的清單。
* **[查看特定計算屬性](#view-a-computed-attribute):** 通過在請求期間指定單個計算屬性的ID來返回其詳細資訊。

### 列出所有計算屬性 {#list-all-computed-attributes}

您的IMS組織可以建立多個計算屬性，並對 `/config/computedAttributes` 終結點允許您列出組織的所有現有計算屬性。

**API格式**

```http
GET /config/computedAttributes
```

**要求**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/config/computedAttributes/ \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \ 
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**回應**

成功響應包括 `_page` 提供計算屬性總數的屬性(`totalCount`)和頁上計算的屬性數(`pageSize`)。

響應還包括 `children` 由一個或多個對象組成的陣列，每個對象都包含一個計算屬性的詳細資訊。 如果您的組織沒有任何計算屬性， `totalCount` 和 `pageSize` 將為0（零） `children` 陣列將為空。

```json
{
    "_page": {
        "totalCount": 2,
        "pageSize": 2
    },
    "children": [
        {
            "id": "2afcf410-450e-4a39-984d-2de99ab58877",
            "imsOrgId": "{ORG_ID}",
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
            "imsOrgId": "{ORG_ID}",
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
                "type": "PQL", 
                "format": "pql/text", 
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
| `_page.pageSize` | 在此結果頁上返回的計算屬性數。 如果 `pageSize` 等於 `totalCount`，這意味著只有一個結果頁，並且已返回所有計算屬性。 如果它們不相等，則可以訪問其他結果頁。 請參閱 `_links.next` 的雙曲餘切值。 |
| `children` | 由一個或多個對象組成的陣列，每個對象都包含單個計算屬性的詳細資訊。 如果尚未定義計算屬性， `children` 陣列為空。 |
| `id` | 建立計算屬性時自動為其分配的唯一隻讀系統生成值。 有關計算屬性對象元件的詳細資訊，請參見上的部分 [建立計算屬性](#create-a-computed-attribute) 在本教程的前面部分。 |
| `_links.next` | 如果返回單頁計算屬性， `_links.next` 是空對象，如上面的示例響應所示。 如果您的組織具有許多計算屬性，則這些屬性將在多個頁面上返回，您可以通過向GET發出請求來訪問這些頁面 `_links.next` 值。 |

### 查看計算屬性 {#view-a-computed-attribute}

您可以通過向GET發出請求來查看特定計算屬性 `/config/computedAttributes` 終結點，並在請求路徑中包括計算的屬性ID。

**API格式**

```http
GET /config/computedAttributes/{ATTRIBUTE_ID}
```

| 參數 | 說明 |
|---|---|
| `{ATTRIBUTE_ID}` | 要查看的計算屬性的ID。 |

**要求**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/config/computedAttributes/2afcf410-450e-4a39-984d-2de99ab58877 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \ 
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**回應**

```json
{
    "id": "2afcf410-450e-4a39-984d-2de99ab58877",
    "imsOrgId": "{ORG_ID}",
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

如果您發現需要更新現有計算屬性，可以通過向 `/config/computedAttributes` 端點，並包括要在請求路徑中更新的計算屬性的ID。

**API格式**

```http
PATCH /config/computedAttributes/{ATTRIBUTE_ID}
```

| 參數 | 說明 |
|---|---|
| `{ATTRIBUTE_ID}` | 要更新的計算屬性的ID。 |

**要求**

此請求使用 [JSON修補程式格式](https://datatracker.ietf.org/doc/html/rfc6902) 更新「expression」欄位的「value」。

```shell
curl -X PATCH \
  https://platform.adobe.io/data/core/ups/config/computedAttributes/ae0c6552-cf49-4725-8979-116366e8e8d3 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}'\
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \  
  -d '[
        {
          "op": "add",
          "path": "/expression",
          "value": 
          {
            "type": "PQL", 
            "format": "pql/text", 
            "value":  "{NEW_EXPRESSION_VALUE}"
          }
        }
      ]'
```

| 屬性 | 說明 |
|---|---|
| `{NEW_EXPRESSION_VALUE}` | 有效 [!DNL Profile Query Language] (PQL)表達式。 計算屬性當前支援以下函式：sum、count、min、max和boolean。 有關示例表達式的清單，請參閱 [示例PQL表達式](expressions.md) 文檔。 |

**回應**

成功更新會返回HTTP狀態204（無內容）和空的響應正文。 如果要確認更新成功，可以執行GET請求以按計算屬性的ID查看計算屬性。

## 刪除計算屬性

也可以使用API刪除計算屬性。 這是通過向 `/config/computedAttributes` 端點，並包括要在請求路徑中刪除的計算屬性的ID。

>[!NOTE]
>
>刪除計算屬性時請小心，因為該屬性可能正在多個架構中使用，並且DELETE操作無法撤消。

**API格式**

```http
DELETE /config/computedAttributes/{ATTRIBUTE_ID}
```

| 參數 | 說明 |
|---|---|
| `{ATTRIBUTE_ID}` | 要刪除的計算屬性的ID。 |

**要求**

```shell
curl -X DELETE \
  https://platform.adobe.io/data/core/ups/config/computedAttributes/ae0c6552-cf49-4725-8979-116366e8e8d3 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}'
  -H 'x-sandbox-name: {SANDBOX_NAME}' \ 
```

**回應**

成功的刪除請求返回HTTP狀態200(OK)和空響應正文。 要確認刪除成功，可以執行GET請求以按計算屬性的ID查找該屬性。 如果刪除了該屬性，您將收到HTTP Status 404（未找到）錯誤。

## 建立引用計算屬性的段定義

Adobe Experience Platform允許您建立段，從一組配置檔案中定義一組特定屬性或行為。 段定義包括封裝PQL中寫入的查詢的表達式。 這些表達式還可以引用計算屬性。

下面的示例建立引用現有計算屬性的段定義。 要瞭解有關段定義的詳細資訊，以及如何在分段服務API中使用這些定義，請參閱 [段定義API終結點指南](../../segmentation/api/segment-definitions.md)。

要開始，請向 `/segment/definitions` 端點，在請求體中提供計算屬性。

**API格式**

```http
POST /segment/definitions
```

**要求**

```shell
curl -X POST https://platform.adobe.io/data/core/ups/segment/definitions
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
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
        }
    }'
```

| 屬性 | 說明 |
| -------- | ----------- |
| `name` | 段的唯一名稱（字串）。 |
| `description` | 定義的人可讀描述。 |
| `schema.name` | 與段中的實體關聯的架構。 由 `id` 或 `name` 的子菜單。 |
| `expression` | 包含包含有關段定義資訊的欄位的對象。 |
| `expression.type` | 指定表達式類型。 目前只支援&quot;PQL&quot;。 |
| `expression.format` | 指示值中表達式的結構。 當前，僅 `pql/text` 支援。 |
| `expression.value` | 有效的PQL表達式，在本示例中它包括對現有計算屬性的引用。 |

有關架構定義屬性的詳細資訊，請參閱中提供的示例 [段定義API終結點指南](../../segmentation/api/segment-definitions.md)。

**回應**

成功的響應返回HTTP狀態200，其中包含新建立的段定義的詳細資訊。 要瞭解有關段定義響應對象的詳細資訊，請參閱 [段定義API終結點指南](../../segmentation/api/segment-definitions.md)。

```json
{
    "id": "add3933f-ac5c-4240-8259-3a4528ee4885",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "ttlInDays": 60,
    "id": "119835c3-5fab-4c18-ae01-4ccab328fc5c",
    "imsOrgId": "{ORG_ID}",
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

現在，您已經瞭解了計算屬性的基本知識，您已準備好開始為組織定義這些屬性。
