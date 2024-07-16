---
keywords: Experience Platform；首頁；熱門主題；原則執行；API型執行；資料控管
solution: Experience Platform
title: 資料控管原則API端點
description: 資料治理原則是您的組織採用的規則，可說明允許或限制您在Experience Platform內對資料執行的行銷動作型別。 /policies端點用於與檢視、建立、更新或刪除資料治理原則相關的所有API呼叫。
role: Developer
exl-id: 62a6f15b-4c12-4269-bf90-aaa04c147053
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
workflow-type: tm+mt
source-wordcount: '1863'
ht-degree: 2%

---

# 資料治理原則端點

資料治理原則是描述允許或限制您在[!DNL Experience Platform]內對資料執行的行銷動作型別的規則。 [!DNL Policy Service API]中的`/policies`端點可讓您以程式設計方式管理組織的資料治理原則。

>[!IMPORTANT]
>
>治理原則不應與存取控制原則混淆，存取控制原則會決定貴組織中特定Platform使用者可存取的特定資料屬性。 如需如何以程式設計方式管理存取控制原則的詳細資訊，請參閱[存取控制API](../../access-control/abac/api/policies.md)的`/policies`端點指南。

## 快速入門

本指南中使用的API端點是[[!DNL Policy Service] API](https://www.adobe.io/experience-platform-apis/references/policy-service/)的一部分。 繼續之前，請先檢閱[快速入門手冊](getting-started.md)，以取得相關檔案的連結、閱讀本檔案中範例API呼叫的手冊，以及有關成功呼叫任何[!DNL Experience Platform] API所需必要標題的重要資訊。

## 擷取原則清單 {#list}

您可以分別向`/policies/core`或`/policies/custom`發出GET要求，以列出所有`core`或`custom`原則。

**API格式**

```http
GET /policies/core
GET /policies/custom
```

**要求**

以下請求會擷取貴組織定義的自訂原則清單。

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/dulepolicy/policies/custom \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應包括`children`陣列，列出每個擷取原則的詳細資料，包括其`id`值。 您可以使用特定原則的`id`欄位，為該原則執行[查詢](#lookup)、[更新](#update)和[刪除](#delete)要求。

```JSON
{
    "_page": {
        "start": "5c6dacdf685a4913dc48937c",
        "count": 2
    },
    "_links": {
        "page": {
            "href": "https://platform.adobe.io/policies/custom?{?limit,start,property}",
            "templated": true
        }
    },
    "children": [
        {
            "name": "Export Data to Third Party",
            "status": "DRAFT",
            "marketingActionRefs": [
                "https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/exportToThirdParty"
            ],
            "description": "Conditions under which data cannot be exported to a third party",
            "deny": {
                "operator": "AND",
                "operands": [
                    {
                        "label": "C1"
                    },
                    {
                        "operator": "OR",
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
            "imsOrg": "{ORG_ID}",
            "created": 1550691551888,
            "createdClient": "{CLIENT_ID}",
            "createdUser": "{USER_ID}",
            "updated": 1550701472910,
            "updatedClient": "{CLIENT_ID}",
            "updatedUser": "{USER_ID}",
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io/data/foundation/dulepolicy/policies/custom/5c6dacdf685a4913dc48937c"
                }
            },
            "id": "5c6dacdf685a4913dc48937c"
        },
        {
            "name": "Combine Data",
            "status": "ENABLED",
            "marketingActionRefs": [
                "https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/combineData"
            ],
            "description": "Data that meets these conditions cannot be combined.",
            "deny": {
                "operator": "AND",
                "operands": [
                    {
                        "label": "C3"
                    },
                    {
                        "label": "I1"
                    }
                ]
            },
            "imsOrg": "{ORG_ID}",
            "created": 1550703519823,
            "createdClient": "{CLIENT_ID}",
            "createdUser": "{USER_ID}",
            "updated": 1550714340335,
            "updatedClient": "{CLIENT_ID}",
            "updatedUser": "{USER_ID}",
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io/data/foundation/dulepolicy/policies/custom/5c6ddb9f5c404513dc2dc454"
                }
            },
            "id": "5c6ddb9f5c404513dc2dc454"
        }
    ]
}
```

| 屬性 | 說明 |
| --- | --- |
| `_page.count` | 擷取的原則總數。 |
| `name` | 原則的顯示名稱。 |
| `status` | 原則的目前狀態。 有三個可能的狀態： `DRAFT`、`ENABLED`或`DISABLED`。 依預設，只有`ENABLED`個原則參與評估。 如需詳細資訊，請參閱[原則評估](../enforcement/overview.md)的概觀。 |
| `marketingActionRefs` | 列出原則之所有適用行銷動作的URI的陣列。 |
| `description` | 選擇性說明，提供原則使用案例的後續內容。 |
| `deny` | 說明原則的相關行銷動作限制執行的特定資料使用標籤的物件。 如需此屬性的詳細資訊，請參閱[建立原則](#create-policy)的相關章節。 |

## 查詢原則 {#look-up}

您可以在GET要求的路徑中包含特定原則的`id`屬性，以查詢該原則。

**API格式**

```http
GET /policies/core/{POLICY_ID}
GET /policies/custom/{POLICY_ID}
```

| 參數 | 說明 |
| --- | --- |
| `{POLICY_ID}` | 您要查閱之原則的`id`。 |

**要求**

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/dulepolicy/policies/custom/5c6dacdf685a4913dc48937c \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應會傳回原則的詳細資訊。

```JSON
{
    "name": "Export Data to Third Party",
    "status": "DRAFT",
    "marketingActionRefs": [
        "https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/exportToThirdParty"
    ],
    "description": "Conditions under which data cannot be exported to a third party",
    "deny": {
        "operator": "AND",
        "operands": [
            {
                "label": "C1"
            },
            {
                "operator": "OR",
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
    "imsOrg": "{ORG_ID}",
    "created": 1550703519823,
    "createdClient": "{CLIENT_ID}",
    "createdUser": "{USER_ID}",
    "updated": 1550714340335,
    "updatedClient": "{CLIENT_ID}",
    "updatedUser": "{USER_ID}",
    "_links": {
        "self": {
            "href": "https://platform.adobe.io/data/foundation/dulepolicy/policies/custom/5c6dacdf685a4913dc48937c"
        }
    },
    "id": "5c6dacdf685a4913dc48937c"
}
```

| 屬性 | 說明 |
| --- | --- |
| `name` | 原則的顯示名稱。 |
| `status` | 原則的目前狀態。 有三個可能的狀態： `DRAFT`、`ENABLED`或`DISABLED`。 依預設，只有`ENABLED`個原則參與評估。 如需詳細資訊，請參閱[原則評估](../enforcement/overview.md)的概觀。 |
| `marketingActionRefs` | 此陣列會列出原則所有適用行銷動作的URI。 |
| `description` | 選擇性說明，提供原則使用案例的後續內容。 |
| `deny` | 說明原則相關行銷動作限制執行的特定資料使用標籤的物件。 如需此屬性的詳細資訊，請參閱[建立原則](#create-policy)的相關章節。 |

## 建立自訂原則 {#create-policy}

在[!DNL Policy Service] API中，原則由以下定義：

* 特定行銷動作的參考
* 描述行銷動作被限制執行的資料使用標籤的運算式

為了滿足後一要求，原則定義必須包括關於資料使用標籤存在的布林運算式。 此運算式稱為原則運算式。

原則運算式是以`deny`屬性的形式在每個原則定義中提供。 僅檢查單一標籤是否存在的簡單`deny`物件範例如下所示：

```json
"deny": {
    "label": "C1"
}
```

不過，許多原則會針對資料使用標籤的出現指定更複雜的條件。 若要支援這些使用案例，您也可以包含布林運算來說明您的原則運算式。 原則運算式物件必須包含標籤或運運算元與運算元，但不能同時包含兩者。 反過來，每個運算元也是原則運算式物件。

例如，為了定義禁止對存在`C1 OR (C3 AND C7)`標籤的資料執行行銷動作的原則，原則的`deny`屬性將指定為：

```JSON
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
```

| 屬性 | 說明 |
| --- | --- |
| `operator` | 表示同層級`operands`陣列中提供的標籤之間的條件式關係。 接受的值包括： <ul><li>`OR`：如果`operands`陣列中有任何標籤存在，運算式會解析為true。</li><li>`AND`：只有在`operands`陣列中的所有標籤都存在時，運算式才會解析為true。</li></ul> |
| `operands` | 物件陣列，每個物件代表單一標籤或額外的`operator`和`operands`屬性組。 `operands`陣列中存在標籤和/或作業會根據其同層級`operator`屬性的值解析為true或false。 |
| `label` | 套用至原則的單一資料使用標籤的名稱。 |

您可以對`/policies/custom`端點發出POST要求，以建立新的自訂原則。

**API格式**

```http
POST /policies/custom
```

**要求**

下列要求會建立新原則，限制在包含標籤`C1 OR (C3 AND C7)`的資料上執行行銷動作`exportToThirdParty`。

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/dulepolicy/policies/custom \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "name": "Export Data to Third Party",
        "status": "DRAFT",
        "marketingActionRefs": [
          "https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/exportToThirdParty"
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
| `name` | 原則的顯示名稱。 |
| `status` | 原則的目前狀態。 有三個可能的狀態： `DRAFT`、`ENABLED`或`DISABLED`。 依預設，只有`ENABLED`個原則參與評估。 如需詳細資訊，請參閱[原則評估](../enforcement/overview.md)的概觀。 |
| `marketingActionRefs` | 此陣列會列出原則所有適用行銷動作的URI。 在[查詢行銷動作](./marketing-actions.md#look-up)的回應中，`_links.self.href`下提供了行銷動作的URI。 |
| `description` | 選擇性說明，提供原則使用案例的後續內容。 |
| `deny` | 說明特定資料使用標籤的原則運算式，其會限制對其執行原則的相關行銷動作。 |

**回應**

成功的回應會傳回新建立原則的詳細資料，包括其`id`。 此值是唯讀的，會在建立原則時自動指定。

```JSON
{
    "name": "Export Data to Third Party",
    "status": "DRAFT",
    "marketingActionRefs": [
        "https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/exportToThirdParty"
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
    "imsOrg": "{ORG_ID}",
    "created": 1550691551888,
    "createdClient": "{CLIENT_ID}",
    "createdUser": "{USER_ID}",
    "updated": 1550691551888,
    "updatedClient": "{CLIENT_ID}",
    "updatedUser": "{USER_ID}",
    "_links": {
        "self": {
            "href": "https://platform.adobe.io/data/foundation/dulepolicy/policies/custom/5c6dacdf685a4913dc48937c"
        }
    },
    "id": "5c6dacdf685a4913dc48937c"
}
```

## 更新自訂原則 {#update}

>[!IMPORTANT]
>
>您只能更新自訂原則。 如果要啟用或停用核心原則，請參閱[更新已啟用的核心原則清單](#update-enabled-core)中的章節。

您可以在PUT請求的路徑中提供其ID，並使用包含完整原則更新形式的裝載，以更新現有的自訂原則。 換言之，PUT要求基本上會重寫原則。

>[!NOTE]
>
>如果您只想更新原則的一或多個欄位，而不是覆寫原則，請參閱[更新部分自訂原則](#patch)的相關章節。

**API格式**

```http
PUT /policies/custom/{POLICY_ID}
```

| 參數 | 說明 |
| --- | --- |
| `{POLICY_ID}` | 您要更新的原則之`id`。 |

**要求**

在此範例中，將資料匯出至協力廠商的條件已變更，現在您需要您建立的原則，才能在出現`C1 AND C5`資料標籤時拒絕此行銷動作。

以下請求會更新現有原則以包含新的原則運算式。 請注意，由於此請求基本上會重寫原則，因此所有欄位都必須包含在裝載中，即使其部分值未更新。

```shell
curl -X PUT \
  https://platform.adobe.io/data/foundation/dulepolicy/policies/custom/5c6dacdf685a4913dc48937c \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "name": "Export Data to Third Party",
        "status": "DRAFT",
        "marketingActionRefs": [
          "../marketingActions/custom/exportToThirdParty"
        ],
        "description": "Conditions under which data cannot be exported to a third party",
        "deny": {
          "operator": "AND",
          "operands": [
            {"label": "C1"},
            {"label": "C5"}
          ]
        }
      }'
```

| 屬性 | 說明 |
| --- | --- |
| `name` | 原則的顯示名稱。 |
| `status` | 原則的目前狀態。 有三個可能的狀態： `DRAFT`、`ENABLED`或`DISABLED`。 依預設，只有`ENABLED`個原則參與評估。 如需詳細資訊，請參閱[原則評估](../enforcement/overview.md)的概觀。 |
| `marketingActionRefs` | 此陣列會列出原則所有適用行銷動作的URI。 在[查詢行銷動作](./marketing-actions.md#look-up)的回應中，`_links.self.href`下提供了行銷動作的URI。 |
| `description` | 選擇性說明，提供原則使用案例的後續內容。 |
| `deny` | 說明特定資料使用標籤的原則運算式，其會限制對其執行原則的相關行銷動作。 如需此屬性的詳細資訊，請參閱[建立原則](#create-policy)的相關章節。 |

**回應**

成功的回應會傳回已更新原則的詳細資料。

```JSON
{
    "name": "Export Data to Third Party",
    "status": "DRAFT",
    "marketingActionRefs": [
        "https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/core/exportToThirdParty"
    ],
    "description": "Conditions under which data cannot be exported to a third party",
    "deny": {
        "operator": "AND",
        "operands": [
            {
                "label": "C1"
            },
            {
                "label": "C5"
            }
        ]
    },
    "imsOrg": "{ORG_ID}",
    "created": 1550691551888,
    "createdClient": "{CLIENT_ID}",
    "createdUser": "{USER_ID}",
    "updated": 1550701472910,
    "updatedClient": "{CLIENT_ID}",
    "updatedUser": "{USER_ID}",
    "_links": {
        "self": {
            "href": "https://platform.adobe.io/data/foundation/dulepolicy/policies/custom/5c6dacdf685a4913dc48937c"
        }
    },
    "id": "5c6dacdf685a4913dc48937c"
}
```

## 更新部分自訂原則 {#patch}

>[!IMPORTANT]
>
>您只能更新自訂原則。 如果要啟用或停用核心原則，請參閱[更新已啟用的核心原則清單](#update-enabled-core)中的章節。

可以使用PATCH請求更新原則的特定部分。 不同於重寫原則的PUT要求，PATCH要求只更新要求內文中指定的屬性。 當您想要啟用或停用原則時，這個功能特別有用，因為您只需要提供適當屬性(`/status`)及其值（`ENABLED`或`DISABLED`）的路徑。

>[!NOTE]
>
>PATCH請求的裝載遵循JSON修補程式格式。 請參閱[API基礎指南](../../landing/api-fundamentals.md)，以取得接受語法的詳細資訊。

[!DNL Policy Service] API支援JSON修補程式作業`add`、`remove`和`replace`，並允許您將數個更新合併成單一呼叫，如下列範例所示。

**API格式**

```http
PATCH /policies/custom/{POLICY_ID}
```

| 參數 | 說明 |
| --- | --- |
| `{POLICY_ID}` | 您要更新其屬性的原則之`id`。 |

**要求**

下列要求使用兩個`replace`作業將原則狀態從`DRAFT`變更為`ENABLED`，並以新描述更新`description`欄位。

>[!IMPORTANT]
>
>在單一請求中傳送多個PATCH作業時，將會依照作業在陣列中出現的順序進行處理。 確保您在必要時以正確的順序傳送請求。

```SHELL
curl -X PATCH \
  https://platform.adobe.io/data/foundation/dulepolicy/policies/custom/5c6dacdf685a4913dc48937c \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d ' [
          {
            "op": "replace",
            "path": "/status",
            "value": "ENABLED"
          },
          {
            "op": "replace",
            "path": "/description",
            "value": "New policy description."
          }
        ]'
```

**回應**

成功的回應會傳回已更新原則的詳細資料。


```JSON
{
    "name": "Export Data to Third Party",
    "status": "ENABLED",
    "marketingActionRefs": [
        "https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/exportToThirdParty"
    ],
    "description": "New policy description.",
    "deny": {
        "operator": "AND",
        "operands": [
            {
                "label": "C1"
            },
            {
                "operator": "OR",
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
    "imsOrg": "{ORG_ID}",
    "created": 1550703519823,
    "createdClient": "{CLIENT_ID}",
    "createdUser": "{USER_ID}",
    "updated": 1550712163182,
    "updatedClient": "{CLIENT_ID}",
    "updatedUser": "{USER_ID}",
    "_links": {
        "self": {
            "href": "https://platform.adobe.io/data/foundation/dulepolicy/policies/custom/5c6dacdf685a4913dc48937c"
        }
    },
    "id": "5c6dacdf685a4913dc48937c"
}
```

## 刪除自訂原則 {#delete}

您可以在DELETE要求的路徑中包含自訂原則的`id`，以刪除自訂原則。

>[!WARNING]
>
>一旦刪除，原則就無法復原。 最佳實務是先[執行查詢(GET)要求](#lookup)以檢視原則，並確認它是您要移除的正確原則。

**API格式**

```http
DELETE /policies/custom/{POLICY_ID}
```

| 參數 | 說明 |
| --- | --- |
| `{POLICY_ID}` | 您要刪除的原則識別碼。 |

**要求**

```shell
curl -X DELETE \
  https://platform.adobe.io/data/foundation/dulepolicy/policies/custom/5c6ddb56eb60ca13dbf8b9a8 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應會傳回HTTP狀態200 （確定），並帶有空白內文。

您可以再次嘗試查閱(GET)原則以確認刪除。 如果原則已成功刪除，您應該會收到HTTP 404 （找不到）錯誤。

## 擷取已啟用的核心原則清單 {#list-enabled-core}

依預設，只有已啟用的資料治理原則會參與評估。 您可以向`/enabledCorePolicies`端點發出GET要求，以擷取貴組織目前啟用的核心原則清單。

**API格式**

```http
GET /enabledCorePolicies
```

**要求**

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/dulepolicy/enabledCorePolicies \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應會傳回`policyIds`陣列下啟用的核心原則清單。

```json
{
  "policyIds": [
    "corepolicy_0001",
    "corepolicy_0002",
    "corepolicy_0003",
    "corepolicy_0004",
    "corepolicy_0005",
    "corepolicy_0006",
    "corepolicy_0007",
    "corepolicy_0008"
  ],
  "imsOrg": "{ORG_ID}",
  "created": 1529696681413,
  "createdClient": "{CLIENT_ID}",
  "createdUser": "{USER_ID}",
  "updated": 1529697651972,
  "updatedClient": "{CLIENT_ID}",
  "updatedUser": "{USER_ID}",
  "_links": {
    "self": {
      "href": "https://platform.adobe.io:443/data/foundation/dulepolicy/enabledCorePolicies"
    }
  }
}
```

## 更新已啟用的核心原則清單 {#update-enabled-core}

依預設，只有已啟用的資料治理原則會參與評估。 透過向`/enabledCorePolicies`端點發出PUT要求，您可以使用單一呼叫來更新貴組織的已啟用核心原則清單。

>[!NOTE]
>
>此端點只能啟用或停用核心原則。 若要啟用或停用自訂原則，請參閱[更新部分原則](#patch)的相關章節。

**API格式**

```http
PUT /enabledCorePolicies
```

**要求**

以下請求會根據承載中提供的ID更新已啟用的核心原則清單。

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/dulepolicy/enabledCorePolicies \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "policyIds": [
          "corepolicy_0001",
          "corepolicy_0002",
          "corepolicy_0007",
          "corepolicy_0008"
        ]
      }'
```

| 屬性 | 說明 |
| --- | --- |
| `policyIds` | 要啟用的核心原則ID清單。 任何未包含的核心原則都會設為`DISABLED`狀態，且不會參與評估。 |

**回應**

成功的回應會傳回`policyIds`陣列下啟用的核心原則更新清單。

```json
{
  "policyIds": [
    "corepolicy_0001",
    "corepolicy_0002",
    "corepolicy_0007",
    "corepolicy_0008"
  ],
  "imsOrg": "{ORG_ID}",
  "created": 1529696681413,
  "createdClient": "{CLIENT_ID}",
  "createdUser": "{USER_ID}",
  "updated": 1595876052649,
  "updatedClient": "{CLIENT_ID}",
  "updatedUser": "{USER_ID}",
  "_links": {
    "self": {
      "href": "https://platform.adobe.io:443/data/foundation/dulepolicy/enabledCorePolicies"
    }
  }
}
```

## 後續步驟

定義新原則或更新現有原則後，您就可以使用[!DNL Policy Service] API針對特定標籤或資料集測試行銷動作，並檢視原則是否如預期引發違規。 如需詳細資訊，請參閱[原則評估端點](./evaluation.md)的指南。
