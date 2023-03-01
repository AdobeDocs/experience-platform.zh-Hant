---
keywords: Experience Platform；設定檔；即時客戶設定檔；疑難排解；API
title: 計算屬性API端點
type: Documentation
description: 在Adobe Experience Platform中，計算屬性是用來將事件層級資料匯總至設定檔層級屬性的函式。 系統會自動計算這些函式，以便用於不同區段、啟動和個人化。 本指南說明如何使用即時客戶設定檔API來建立、檢視、更新和刪除計算屬性。
exl-id: 6b35ff63-590b-4ef5-ab39-c36c39ab1d58
source-git-commit: 1c4da50b2c211aae06d6702d75e5650447fae0eb
workflow-type: tm+mt
source-wordcount: '2275'
ht-degree: 2%

---

# (Alpha)計算屬性API端點

>[!IMPORTANT]
>
>本文檔中概述的計算屬性功能當前為Alpha格式，不適用於所有用戶。 文件和功能可能會有所變更。

計算屬性是用於將事件層級資料匯總到設定檔層級屬性的函式。 系統會自動計算這些函式，以便用於不同區段、啟動和個人化。 本指南包含使用執行基本CRUD作業的範例API呼叫 `/computedAttributes` 端點。

若要進一步了解運算屬性，請先閱讀 [計算屬性概述](overview.md).

## 快速入門

本指南中使用的API端點屬於 [即時客戶個人檔案API](https://www.adobe.com/go/profile-apis-en).

繼續之前，請檢閱 [設定檔API快速入門手冊](../api/getting-started.md) 若為建議檔案的連結，請參閱閱讀本檔案中顯示之範例API呼叫的指南，以及成功呼叫任何Experience PlatformAPI所需之必要標題的重要資訊。

## 配置計算屬性欄位

若要建立計算屬性，您首先需要識別架構中包含計算屬性值的欄位。

請參閱 [配置計算屬性](configure-api.md) ，了解在架構中建立計算屬性欄位的完整端到端指南。

>[!WARNING]
>
>若要繼續使用API指南，您必須設定計算屬性欄位。

## 建立計算屬性 {#create-a-computed-attribute}

在啟用「設定檔」的結構中定義了計算屬性欄位，您現在可以設定計算屬性。 如果您尚未執行此作業，請依照 [配置計算屬性](configure-api.md) 檔案。

若要建立計算屬性，請從向 `/config/computedAttributes` 端點為請求內文，其中包含您要建立之計算屬性的詳細資訊。

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
| `name` | 計算屬性欄位的名稱，作為字串。 |
| `path` | 包含計算屬性的欄位路徑。 此路徑位於 `properties` 屬性，且「不應」在路徑中包含欄位名稱。 寫入路徑時，忽略 `properties` 屬性。 |
| `{TENANT_ID}` | 若您不熟悉租用戶ID，請參閱 [Schema Registry開發人員指南](../../xdm/api/getting-started.md#know-your-tenant_id). |
| `description` | 計算屬性的說明。 一旦定義了多個計算屬性，這特別有用，因為它將幫助IMS組織內的其他人決定要使用的正確計算屬性。 |
| `expression.value` | 有效 [!DNL Profile Query Language] (PQL)表達式。 計算屬性當前支援以下函式：總和、計數、最小值、最大值和布林值。 如需範例運算式的清單，請參閱 [PQL表達式示例](expressions.md) 檔案。 |
| `schema.name` | 包含計算屬性欄位的架構所基於的類。 範例： `_xdm.context.experienceevent` ，以根據XDM ExperienceEvent類別的結構。 |

**回應**

成功建立的計算屬性返回HTTP狀態200(OK)，並返回包含新建立的計算屬性詳細資訊的響應正文。 這些詳細資訊包括唯一、唯讀、系統產生的 `id` 可在其他API作業期間用於參考計算屬性。

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
| `id` | 唯一、唯讀、系統產生的ID，可在其他API作業期間用於參考計算的屬性。 |
| `imsOrgId` | 與計算屬性相關的IMS組織應符合請求中傳送的值。 |
| `sandbox` | 沙箱物件包含沙箱的詳細資訊，計算屬性是在其中設定的。 此資訊取自於請求中傳送的沙箱標題。 如需詳細資訊，請參閱 [沙箱概述](../../sandboxes/home.md). |
| `positionPath` | 包含被解構的 `path` 至請求中傳送的欄位。 |
| `returnSchema.meta:xdmType` | 儲存計算屬性的欄位類型。 |
| `definedOn` | 顯示已定義計算屬性的聯合結構的陣列。 每個聯合架構包含一個對象，這表示如果計算的屬性已根據不同類添加到多個架構中，陣列中可能存在多個對象。 |
| `active` | 顯示計算屬性當前是否處於活動狀態的布爾值。 預設情況下，值為 `true`. |
| `type` | 建立的資源類型，在此例中，「ComputedAttribute」是預設值。 |
| `createEpoch` 和 `updateEpoch` | 分別建立和上次更新計算屬性的時間。 |

## 建立引用現有計算屬性的計算屬性

也可以建立引用現有計算屬性的計算屬性。 若要這麼做，請先向 `/config/computedAttributes` 端點。 請求內文將包含對 `expression.value` 欄位，如下列範例所示。

**API格式**

```http
POST /config/computedAttributes
```

**要求**

在此示例中，已建立兩個計算屬性，將用於定義第三個屬性。 現有的計算屬性包括：

* **`totalSpend`:** 擷取客戶已花費的總金額。
* **`countPurchases`:** 計算客戶已進行的購買次數。

以下請求會參考兩個現有的計算屬性，使用有效的PQL進行除以計算新屬性 `averageSpend` 計算屬性。

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
| `name` | 計算屬性欄位的名稱，作為字串。 |
| `path` | 包含計算屬性的欄位路徑。 此路徑位於 `properties` 屬性，且「不應」在路徑中包含欄位名稱。 寫入路徑時，忽略 `properties` 屬性。 |
| `{TENANT_ID}` | 若您不熟悉租用戶ID，請參閱 [Schema Registry開發人員指南](../../xdm/api/getting-started.md#know-your-tenant_id). |
| `description` | 計算屬性的說明。 一旦定義了多個計算屬性，這特別有用，因為它將幫助IMS組織內的其他人決定要使用的正確計算屬性。 |
| `expression.value` | 有效的PQL表達式。 計算屬性當前支援以下函式：總和、計數、最小值、最大值和布林值。 如需範例運算式的清單，請參閱 [PQL表達式示例](expressions.md) 檔案。<br/><br/>在此示例中，表達式引用兩個現有的計算屬性。 系統會使用 `path` 和 `name` 在定義計算屬性的架構中顯示的計算屬性。 例如， `path` 第一個引用的計算屬性為 `_{TENANT_ID}.purchaseSummary` 和 `name` is `totalSpend`. |
| `schema.name` | 包含計算屬性欄位的架構所基於的類。 範例： `_xdm.context.experienceevent` ，以根據XDM ExperienceEvent類別的結構。 |

**回應**

成功建立的計算屬性返回HTTP狀態200(OK)，並返回包含新建立的計算屬性詳細資訊的響應正文。 這些詳細資訊包括唯一、唯讀、系統產生的 `id` 可在其他API作業期間用於參考計算屬性。

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
| `id` | 唯一、唯讀、系統產生的ID，可在其他API作業期間用於參考計算的屬性。 |
| `imsOrgId` | 與計算屬性相關的IMS組織應符合請求中傳送的值。 |
| `sandbox` | 沙箱物件包含沙箱的詳細資訊，計算屬性是在其中設定的。 此資訊取自於請求中傳送的沙箱標題。 如需詳細資訊，請參閱 [沙箱概述](../../sandboxes/home.md). |
| `positionPath` | 包含被解構的 `path` 至請求中傳送的欄位。 |
| `returnSchema.meta:xdmType` | 儲存計算屬性的欄位類型。 |
| `definedOn` | 顯示已定義計算屬性的聯合結構的陣列。 每個聯合架構包含一個對象，這表示如果計算的屬性已根據不同類添加到多個架構中，陣列中可能存在多個對象。 |
| `active` | 顯示計算屬性當前是否處於活動狀態的布爾值。 預設情況下，值為 `true`. |
| `type` | 建立的資源類型，在此例中，「ComputedAttribute」是預設值。 |
| `createEpoch` 和 `updateEpoch` | 分別建立和上次更新計算屬性的時間。 |

## 訪問計算屬性

使用API處理計算屬性時，有兩個選項可存取您的組織已定義的計算屬性。 第一個是列出所有計算屬性，第二個是按其唯一查看特定計算屬性 `id`.

本檔案中概述了兩種存取模式的步驟。 選取下列其中一項以開始：

* **[列出所有現有的計算屬性](#list-all-computed-attributes):** 返回您的組織已建立的所有現有計算屬性的清單。
* **[查看特定計算屬性](#view-a-computed-attribute):** 在請求期間指定ID，以傳回單一計算屬性的詳細資訊。

### 列出所有計算屬性 {#list-all-computed-attributes}

您的IMS組織可以建立多個計算屬性，並對 `/config/computedAttributes` 端點可讓您列出組織的所有現有計算屬性。

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

成功的回應包含 `_page` 提供計算屬性總數的屬性(`totalCount`)和頁面上的計算屬性數(`pageSize`)。

回應也包含 `children` 由一個或多個對象組成的陣列，每個對象都包含一個計算屬性的詳細資訊。 如果您的組織沒有任何計算屬性，則 `totalCount` 和 `pageSize` 將為0（零），而 `children` 陣列將為空。

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
| `_page.totalCount` | 由您的IMS組織定義的計算屬性總數。 |
| `_page.pageSize` | 此結果頁返回的計算屬性數。 若 `pageSize` 等於 `totalCount`，這表示只有一個結果頁面，且已傳回所有計算屬性。 如果不相等，則可存取其他結果頁面。 請參閱 `_links.next` 以取得詳細資訊。 |
| `children` | 由一個或多個對象組成的陣列，每個對象都包含單個計算屬性的詳細資訊。 如果尚未定義計算屬性，則 `children` 陣列為空。 |
| `id` | 建立計算屬性時自動分配給該屬性的唯一隻讀系統生成值。 有關計算屬性對象的元件的詳細資訊，請參閱 [建立計算屬性](#create-a-computed-attribute) 本教學課程的前面部分。 |
| `_links.next` | 如果返回了計算屬性的單一頁， `_links.next` 是空白物件，如上方範例回應所示。 如果您的組織有許多計算屬性，則會在多個頁面上傳回，您可以透過向 `_links.next` 值。 |

### 查看計算屬性 {#view-a-computed-attribute}

您可以向 `/config/computedAttributes` 端點，並在請求路徑中納入計算的屬性ID。

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

如果您發現需要更新現有的計算屬性，您可以透過向 `/config/computedAttributes` 端點，並包含您要在請求路徑中更新之計算屬性的ID。

**API格式**

```http
PATCH /config/computedAttributes/{ATTRIBUTE_ID}
```

| 參數 | 說明 |
|---|---|
| `{ATTRIBUTE_ID}` | 要更新的計算屬性ID。 |

**要求**

此請求使用 [JSON修補程式格式](https://datatracker.ietf.org/doc/html/rfc6902) 更新「運算式」欄位的「值」。

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
| `{NEW_EXPRESSION_VALUE}` | 有效 [!DNL Profile Query Language] (PQL)表達式。 計算屬性當前支援以下函式：總和、計數、最小值、最大值和布林值。 如需範例運算式的清單，請參閱 [PQL表達式示例](expressions.md) 檔案。 |

**回應**

成功更新會傳回HTTP狀態204（無內容）和空白回應內文。 如果要確認更新是否成功，可以執行GET請求以按ID查看計算屬性。

## 刪除計算的屬性

您也可以使用API刪除計算的屬性。 若要這麼做，請向 `/config/computedAttributes` 端點，並在請求路徑中包含您要刪除之計算屬性的ID。

>[!NOTE]
>
>刪除計算的屬性時請小心，因為該屬性可能在多個架構中使用，並且DELETE操作無法撤消。

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

成功的刪除請求會傳回HTTP狀態200(OK)和空的回應內文。 若要確認刪除是否成功，您可以執行GET請求，以依其ID來查閱計算的屬性。 如果刪除屬性，您會收到HTTP狀態404（找不到）錯誤。

## 建立參考計算屬性的區段定義

Adobe Experience Platform可讓您建立區段，從一組設定檔中定義一組特定屬性或行為。 段定義包含的表達式封裝了寫入PQL的查詢。 這些運算式也可參考計算屬性。

下面的示例建立引用現有計算屬性的段定義。 若要進一步了解區段定義，以及如何在區段服務API中使用這些定義，請參閱 [區段定義API端點指南](../../segmentation/api/segment-definitions.md).

若要開始，請向 `/segment/definitions` 端點，在請求內文中提供計算屬性。

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
| `name` | 區段的唯一名稱，作為字串。 |
| `description` | 人類看得懂的定義說明。 |
| `schema.name` | 與區段中的實體相關聯的架構。 包含 `id` 或 `name` 欄位。 |
| `expression` | 包含欄位的物件，內含區段定義的相關資訊。 |
| `expression.type` | 指定運算式類型。 目前僅支援「PQL」。 |
| `expression.format` | 指示值中表達式的結構。 目前，僅 `pql/text` 支援。 |
| `expression.value` | 有效的PQL表達式，在此示例中，它包含對現有計算屬性的引用。 |

如需結構定義屬性的詳細資訊，請參閱 [區段定義API端點指南](../../segmentation/api/segment-definitions.md).

**回應**

成功的回應會傳回HTTP狀態200，並包含您新建立之區段定義的詳細資訊。 若要進一步了解區段定義回應物件，請參閱 [區段定義API端點指南](../../segmentation/api/segment-definitions.md).

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

現在您已了解運算屬性的基本知識，可以開始為組織定義這些屬性了。
