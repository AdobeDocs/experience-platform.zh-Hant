---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 建立資料使用原則
topic: policies
translation-type: tm+mt
source-git-commit: da4fe8be360d5530d96078e4ef024bccf7f080f5

---


# 建立資料使用原則

資料使用標籤與實施(DULE)是Adobe Experience Platform資料治理的核心機制。 DULE Policy Service API [](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dule-policy-service.yaml) （DULE原則服務API）可讓您建立和管理DULE原則，以決定可針對包含特定DULE標籤的資料採取哪些行銷動作。

本檔案提供使用Policy Service API建立DULE原則的逐步教學課程。 如需API中可用不同作業的更完整指南，請參閱「原則服務開 [發人員指南」](../api/getting-started.md)。

## 快速入門

本教程需要對建立和評估DULE策略時涉及的以下關鍵概念有充分的瞭解：

* [資料治理](../home.md):平台實施資料使用合規性的框架。
* [資料使用標籤](../labels/overview.md):資料使用標籤會套用至XDM資料欄位，指定資料存取限制。
* [體驗資料模型(XDM)](../../xdm/home.md):平台組織客戶體驗資料的標準化架構。
* [沙盒](../../sandboxes/home.md):Experience Platform提供虛擬沙盒，可將單一Platform實例分割為不同的虛擬環境，以協助開發和發展數位體驗應用程式。

在開始本教學課程之前，請先閱讀開發人員指南 [](../api/getting-started.md) ，以取得成功呼叫DULE Policy Service API所需的重要資訊，包括必要的標題以及如何讀取範例API呼叫。

## 定義行銷動作 {#define-action}

在資料治理架構中，行銷動作是Experience Platform資料使用者採取的動作，需要檢查是否有違反資料使用政策的行為。

建立DULE原則的第一步是決定該原則將評估的行銷動作。 您可以使用下列其中一個選項來完成此作業：

* [尋找現有的行銷動作](#look-up)
* [建立新的行銷動作](#create-new)

### 尋找現有的行銷動作 {#look-up}

您可以對其中一個端點提出GET請求，以尋找由DULE政策評估的現有行銷動 `/marketingActions` 作。

**API格式**

視您要尋找的是Experience Platform提供的行銷動作或您的組織建立的自訂行銷動作，請分別使 `marketingActions/core` 用 `marketingActions/custom` 端點。

```http
GET /marketingActions/core
GET /marketingActions/custom
```

**請求**

下列請求使用端 `marketingActions/custom` 點，此端點會擷取您IMS組織所定義之所有行銷動作的清單。

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應會傳回找到(`count`)的行銷動作總數，並列出陣列中行銷動作本身的詳細 `children` 資訊。

```json
{
    "_page": {
        "start": "sampleMarketingAction",
        "count": 2
    },
    "_links": {
        "page": {
            "href": "https://platform.adobe.io/marketingActions/custom?{?limit,start,property}",
            "templated": true
        }
    },
    "children": [
        {
            "name": "sampleMarketingAction",
            "description": "Marketing Action description.",
            "imsOrg": "{IMS_ORG}",
            "created": 1550714012088,
            "createdClient": "{CREATED_CLIENT}",
            "createdUser": "{CREATED_USER}",
            "updated": 1550714012088,
            "updatedClient": "{UPDATED_CLIENT}",
            "updatedUser": "{UPDATED_USER}",
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io:443/data/foundation/dulepolicy/marketingActions/custom/sampleMarketingAction"
                }
            }
        },
        {
            "name": "newMarketingAction",
            "description": "Another marketing action.",
            "imsOrg": "{IMS_ORG}",
            "created": 1550793833224,
            "createdClient": "{CREATED_CLIENT}",
            "createdUser": "{CREATED_USER}",
            "updated": 1550793833224,
            "updatedClient": "{UPDATED_CLIENT}",
            "updatedUser": "{UPDATED_USER}",
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io:443/data/foundation/dulepolicy/marketingActions/custom/newMarketingAction"
                }
            }
        }
    ]
}
```

| 屬性 | 說明 |
| --- | --- |
| `_links.self.href` | 陣列中的每個項 `children` 目都包含列出的行銷動作的URI ID。 |

當您找到要使用的行銷動作時，請記錄其屬性的 `href` 值。 在建立DULE策略的下一步 [中使用此值](#create-policy)。

### 建立新的行銷動作 {#create-new}

您可以透過向端點提出PUT請求，並在請求路徑的 `/marketingActions/custom/` 末尾提供行銷動作的名稱，來建立新的行銷動作。

**API格式**

```http
PUT /marketingActions/custom/{MARKETING_ACTION_NAME}
```

| 參數 | 說明 |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | 您要建立之新行銷動作的名稱。 此名稱會當做行銷動作的主要識別碼，因此必須是唯一的。 最佳實務是為行銷動作指定描述性但簡明的名稱。 |

**請求**

下列請求會建立新的自訂行銷動作，稱為「exportToThirdParty」。 請注意， `name` 請求裝載中的名稱與請求路徑中提供的名稱相同。

```shell
curl -X PUT \  
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/exportToThirdParty \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "exportToThirdParty",
      "description": "Export data to a third party"
    }'
```

| 屬性 | 說明 |
| --- | --- |
| `name` | 您要建立之行銷動作的名稱。 此名稱必須符合請求路徑中提供的名稱，否則將發生400（錯誤請求）錯誤。 |
| `description` | 行銷動作的可人讀描述。 |

**回應**

成功的回應會傳回HTTP狀態201（已建立）和新建立行銷動作的詳細資訊。

```json
{
    "name": "exportToThirdParty",
    "description": "Export data to a third party",
    "imsOrg": "{IMS_ORG}",
    "created": 1550713341915,
    "createdClient": "{CREATED_CLIENT}",
    "createdUser": "{CREATED_USER",
    "updated": 1550713856390,
    "updatedClient": "{UPDATED_CLIENT}",
    "updatedUser": "{UPDATED_USER}",
    "_links": {
        "self": {
            "href": "https://platform.adobe.io:443/data/foundation/dulepolicy/marketingActions/custom/exportToThirdParty"
        }
    }
}
```

| 屬性 | 說明 |
| --- | --- |
| `_links.self.href` | 行銷動作的URI ID。 |

記錄新建立之行銷動作的URI ID，因為它將用於建立DULE原則的下一個步驟。

## 建立DULE策略 {#create-policy}

建立新原則時，您必須提供行銷動作的URI ID，並具有禁止該行銷動作的DULE標籤的運算式。

此表達式稱為策 **略表達式** ，是包含(A)DULE標籤或(B)運算子和操作數（但不同時包含兩者）的對象。 反過來，每個操作數也是策略表達式對象。 例如，如果標籤存在，則可能禁止將資料匯出至第三 `C1 OR (C3 AND C7)` 方的政策。 此表達式將指定為：

```json
"deny": {
  "operator": "OR",
  "operands": [
    {
      "label": "C1"
    },
    {
      "operator": "AND",
      "operands": [
        {
          "label": "C3"
        },
        {
          "label": "C7"
        }
      ]
    }
  ]
}
```

>[!NOTE] 僅支援OR和AND運算子。

配置策略表達式後，可以通過向端點發出POST請求來建立新的DULE策 `/policies/custom` 略。

**API格式**

```http
POST /policies/custom
```

**請求**

下列請求會在請求裝載中提供行銷動作和原則運算式，以建立稱為「將資料匯出至第三方」的DULE原則。

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/dulepolicy/policies/custom \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "name": "Export Data to Third Party",
    "status": "DRAFT",
    "marketingActionRefs": [
      "../marketingActions/custom/exportToThirdParty"
    ],
    "description": "Conditions under which data cannot be exported to a third party",
    "deny": {
      "operator": "OR",
      "operands": [
        {"label": "C1"},
        {
          "operator": "AND",
          "operands": [
            {"label": "C3"},
            {"label": "C7"}
          ]
        }
      ]
    }
  }'
```

| 屬性 | 說明 |
| --- | --- |
| `marketingActionRefs` | 一個陣列，包含 `href` 在上一步驟中獲取的行銷操作 [的值](#define-action)。 雖然上述範例僅列出一個行銷動作，但也可提供多個動作。 |
| `deny` | 策略表達式對象。 定義會導致策略拒絕中引用的行銷操作的DULE標籤和條件 `marketingActionRefs`。 |

**回應**

成功的回應會傳回HTTP狀態201（已建立）和新建立原則的詳細資訊。

```json
{
    "name": "Export Data to Third Party",
    "status": "DRAFT",
    "marketingActionRefs": [
        "https://platform-stage.adobe.io:443/data/foundation/dulepolicy/marketingActions/custom/exportToThirdParty"
    ],
    "description": "Conditions under which data cannot be exported to a third party",
    "deny": {
        "operator": "OR",
        "operands": [
            {
                "label": "C1"
            },
            {
                "operator": "AND",
                "operands": [
                    {
                        "label": "C3"
                    },
                    {
                        "label": "C7"
                    }
                ]
            }
        ]
    },
    "imsOrg": "{IMS_ORG}",
    "created": 1565651746693,
    "createdClient": "{CREATED_CLIENT}",
    "createdUser": "{CREATED_USER",
    "updated": 1565651746693,
    "updatedClient": "{UPDATED_CLIENT}",
    "updatedUser": "{UPDATED_USER}",
    "_links": {
        "self": {
            "href": "https://platform-stage.adobe.io/data/foundation/dulepolicy/policies/custom/5d51f322e553c814e67af1a3"
        }
    },
    "id": "5d51f322e553c814e67af1a3"
}
```

| 屬性 | 說明 |
| --- | --- |
| `id` | 唯讀、系統生成的值，可唯一標識DULE策略。 |

記錄新建立的DULE策略的URI ID，因為它用於下一步以啟用策略。

## 啟用DULE策略

>[!NOTE] 如果您希望將DULE策略保留為狀態，則此步驟是可選的， `DRAFT` 但請注意，預設情況下，策略必須將其狀態設定為 `ENABLED` ，才能參與評估。 有關如何對處於狀 [態的策略執行例外的資訊](../enforcement/api-enforcement.md) ，請參見有關強制執行DULE策略的 `DRAFT` 教程。

預設情況下，將其屬性設定為 `status` 的DULE策略 `DRAFT` 不參與評估。 通過向端點發出PATCH請求並在請求路徑的末尾為策略提供唯一標識符，您可以啟用 `/policies/custom/` 策略進行評估。

**API格式**

```http
PATCH /policies/custom/{POLICY_ID}
```

| 參數 | 說明 |
| --- | --- |
| `{POLICY_ID}` | 要 `id` 啟用的策略的值。 |

**請求**

以下請求對DULE策略的屬性執 `status` 行PATCH操作，將其值從更改為 `DRAFT``ENABLED`。

```shell
curl -X PATCH \
  https://platform.adobe.io/data/foundation/dulepolicy/policies/custom/5d51f322e553c814e67af1a3
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '[
    {
      "op": "replace",
      "path": "/status",
      "value": "ENABLED"
    }
  ]'
```

| 屬性 | 說明 |
| --- | --- |
| `op` | 要執行的PATCH操作的類型。 此請求會執行「取代」操作。 |
| `path` | 要更新的欄位的路徑。 啟用策略時，值必須設定為「/status」。 |
| `value` | 要分配給中指定屬性的新值 `path`。 此請求將策略的屬 `status` 性設定為「ENABLED」。 |

**回應**

成功的回應會傳回HTTP狀態200(OK)和更新的原則詳細資訊，其現 `status` 在設定為 `ENABLED`。

```json
{
    "name": "Export Data to Third Party",
    "status": "ENABLED",
    "marketingActionRefs": [
        "https://platform-stage.adobe.io:443/data/foundation/dulepolicy/marketingActions/custom/exportToThirdParty"
    ],
    "description": "Conditions under which data cannot be exported to a third party",
    "deny": {
        "operator": "OR",
        "operands": [
            {
                "label": "C1"
            },
            {
                "operator": "AND",
                "operands": [
                    {
                        "label": "C3"
                    },
                    {
                        "label": "C7"
                    }
                ]
            }
        ]
    },
    "imsOrg": "{IMS_ORG}",
    "created": 1565651746693,
    "createdClient": "{CREATED_CLIENT}",
    "createdUser": "{CREATED_USER}",
    "updated": 1565723012139,
    "updatedClient": "{UPDATED_CLIENT}",
    "updatedUser": "{UPDATED_USER}",
    "_links": {
        "self": {
            "href": "https://platform-stage.adobe.io/data/foundation/dulepolicy/policies/custom/5d51f322e553c814e67af1a3"
        }
    },
    "id": "5d51f322e553c814e67af1a3"
}
```

## 後續步驟

遵循本教學課程，您已成功建立行銷動作的資料使用原則。 您現在可以繼續學習如何強制使 [用資料原則的教學課程](../enforcement/api-enforcement.md) ，以瞭解如何檢查是否有違反原則的情況，並在您的體驗應用程式中加以處理。

如需Policy Service API中不同可用作業的詳細資訊，請參閱 [Policy Service開發人員指南](../api/getting-started.md)。 如需如何為即時客戶個人檔案資料實施原則的詳細資訊，請參閱關於為受眾區 [段實施資料使用合規性的教學課程](../../segmentation/tutorials/governance.md)。

若要瞭解如何在Experience Platform使用者介面中管理使用原則，請參閱原 [則使用指南](user-guide.md)。