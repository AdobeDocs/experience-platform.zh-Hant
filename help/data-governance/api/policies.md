---
keywords: Experience Platform；首頁；熱門主題；策略實施；基於API的實施；資料治理
solution: Experience Platform
title: 資料治理策略API終結點
description: 資料治理策略是您的組織所採用的規則，它描述了您在Experience Platform內允許或限制對資料執行的營銷操作的類型。 /policies終結點用於與查看、建立、更新或刪除資料治理策略相關的所有API調用。
exl-id: 62a6f15b-4c12-4269-bf90-aaa04c147053
source-git-commit: 7b15166ae12d90cbcceb9f5a71730bf91d4560e6
workflow-type: tm+mt
source-wordcount: '1865'
ht-degree: 2%

---

# 資料治理策略終結點

資料治理策略是描述允許或限制您對內部資料執行的營銷操作類型的規則 [!DNL Experience Platform]。 的 `/policies` 端點 [!DNL Policy Service API] 允許您以寫程式方式管理組織的資料治理策略。

>[!IMPORTANT]
>
>不要將治理策略與訪問控制策略混為一談，這些策略決定了組織中某些平台用戶可以訪問的特定資料屬性。 請參閱 `/policies` 端點指南 [訪問控制API](../../access-control/abac/api/policies.md) 有關如何以寫程式方式管理訪問控制策略的詳細資訊。

## 快速入門

本指南中使用的API終結點是 [[!DNL Policy Service] API](https://www.adobe.io/experience-platform-apis/references/policy-service/)。 在繼續之前，請查看 [入門指南](getting-started.md) 有關指向相關文檔的連結、閱讀本文檔中示例API調用的指南，以及成功調用任何文檔所需的標題的重要資訊 [!DNL Experience Platform] API。

## 檢索策略清單 {#list}

您可以列出所有 `core` 或 `custom` 策略：向 `/policies/core` 或 `/policies/custom`的下界。

**API格式**

```http
GET /policies/core
GET /policies/custom
```

**要求**

以下請求檢索由您的組織定義的自定義策略清單。

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/dulepolicy/policies/custom \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功響應包括 `children` 列出每個檢索到策略的詳細資訊（包括其詳細資訊）的陣列 `id` 值。 您可以使用 `id` 要執行的特定策略的欄位 [查找](#lookup)。 [更新](#update), [刪除](#delete) 要求執行該政策。

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
| `_page.count` | 檢索的策略總數。 |
| `name` | 策略的顯示名稱。 |
| `status` | 策略的當前狀態。 有三種可能的狀態： `DRAFT`。 `ENABLED`或 `DISABLED`。 預設情況下，僅 `ENABLED` 策略參與評估。 請參閱 [策略評價](../enforcement/overview.md) 的子菜單。 |
| `marketingActionRefs` | 列出策略所有適用市場營銷操作的URI的陣列。 |
| `description` | 提供策略使用案例的進一步上下文的可選說明。 |
| `deny` | 描述特定資料使用標籤的對象，策略的關聯市場營銷操作被限制在其上執行。 請參閱 [建立策略](#create-policy) 的子菜單。 |

## 查找策略 {#look-up}

您可以通過包含該策略 `id` 屬性。

**API格式**

```http
GET /policies/core/{POLICY_ID}
GET /policies/custom/{POLICY_ID}
```

| 參數 | 說明 |
| --- | --- |
| `{POLICY_ID}` | 的 `id` 你想查的政策。 |

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

成功的響應返回策略的詳細資訊。

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
| `name` | 策略的顯示名稱。 |
| `status` | 策略的當前狀態。 有三種可能的狀態： `DRAFT`。 `ENABLED`或 `DISABLED`。 預設情況下，僅 `ENABLED` 策略參與評估。 請參閱 [策略評價](../enforcement/overview.md) 的子菜單。 |
| `marketingActionRefs` | 列出策略所有適用市場營銷操作的URI的陣列。 |
| `description` | 提供策略使用案例的進一步上下文的可選說明。 |
| `deny` | 描述特定資料使用標籤的對象，該策略的關聯市場營銷操作被限制在其上執行。 請參閱 [建立策略](#create-policy) 的子菜單。 |

## 建立自定義策略 {#create-policy}

在 [!DNL Policy Service] API ，策略由以下定義：

* 對特定市場營銷活動的參考
* 描述限制市場營銷操作執行的資料使用標籤的表達式

為滿足後一要求，策略定義必須包含有關資料使用標籤存在性的布爾表達式。 此表達式稱為策略表達式。

策略表達式以 `deny` 屬性。 一個簡單 `deny` 僅檢查單個標籤是否存在的對象如下所示：

```json
"deny": {
    "label": "C1"
}
```

但是，許多策略指定了有關資料使用標籤存在的更複雜條件。 要支援這些使用情形，您還可以包括布爾操作來描述策略表達式。 策略表達式對象必須包含標籤或運算子和操作數，但不能同時包含兩者。 反過來，每個操作數也是策略表達式對象。

例如，為了定義禁止對資料執行市場營銷活動的策略， `C1 OR (C3 AND C7)` 標籤存在，策略 `deny` 屬性將指定為：

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
| `operator` | 指示同級中提供的標籤之間的條件關係 `operands` 陣列。 接受的值為： <ul><li>`OR`:如果中的任何標籤，表達式將解析為true `operands` 陣列存在。</li><li>`AND`:僅當位於 `operands` 陣列存在。</li></ul> |
| `operands` | 對象陣列，每個對象表示單個標籤或另一對 `operator` 和 `operands` 屬性。 標籤和/或操作在 `operands` 陣列根據其同級的值解析為true或false `operator` 屬性。 |
| `label` | 應用於策略的單個資料使用標籤的名稱。 |

您可以通過向POST請求建立新的自定義策略 `/policies/custom` 端點。

**API格式**

```http
POST /policies/custom
```

**要求**

以下請求將建立一個新策略，以限制市場營銷活動 `exportToThirdParty` 對包含標籤的資料執行 `C1 OR (C3 AND C7)`。

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
| `name` | 策略的顯示名稱。 |
| `status` | 策略的當前狀態。 有三種可能的狀態： `DRAFT`。 `ENABLED`或 `DISABLED`。 預設情況下，僅 `ENABLED` 策略參與評估。 請參閱 [策略評價](../enforcement/overview.md) 的子菜單。 |
| `marketingActionRefs` | 列出策略所有適用市場營銷操作的URI的陣列。 市場營銷操作的URI提供於 `_links.self.href` 在 [查看營銷行動](./marketing-actions.md#look-up)。 |
| `description` | 提供策略使用案例的進一步上下文的可選說明。 |
| `deny` | 描述特定資料使用情況的策略表達式將限制策略的關聯市場營銷操作在上執行。 |

**回應**

成功的響應返回新建立策略的詳細資訊，包括其 `id`。 此值為只讀，在建立策略時自動分配。

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

## 更新自定義策略 {#update}

>[!IMPORTANT]
>
>您只能更新自定義策略。 如果要啟用或禁用核心策略，請參閱上的 [更新已啟用的核心策略清單](#update-enabled-core)。

您可以通過在PUT請求路徑中提供現有自定義策略的ID來更新現有自定義策略，該策略的有效負載包括整個策略的更新形式。 換句話說，PUT請求實際上重寫策略。

>[!NOTE]
>
>請參閱 [更新自定義策略的一部分](#patch) 的子菜單。

**API格式**

```http
PUT /policies/custom/{POLICY_ID}
```

| 參數 | 說明 |
| --- | --- |
| `{POLICY_ID}` | 的 `id` 的子菜單。 |

**要求**

在本示例中，將資料導出到第三方的條件已發生更改，現在您需要建立的策略來拒絕此市場營銷操作 `C1 AND C5` 存在資料標籤。

以下請求更新現有策略以包括新策略表達式。 請注意，由於此請求實質上重寫了策略，因此即使某些欄位的值未更新，所有欄位也必須包括在負載中。

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
| `name` | 策略的顯示名稱。 |
| `status` | 策略的當前狀態。 有三種可能的狀態： `DRAFT`。 `ENABLED`或 `DISABLED`。 預設情況下，僅 `ENABLED` 策略參與評估。 請參閱 [策略評價](../enforcement/overview.md) 的子菜單。 |
| `marketingActionRefs` | 列出策略所有適用市場營銷操作的URI的陣列。 市場營銷操作的URI提供於 `_links.self.href` 在 [查看營銷行動](./marketing-actions.md#look-up)。 |
| `description` | 提供策略使用案例的進一步上下文的可選說明。 |
| `deny` | 描述特定資料使用情況的策略表達式將限制策略的關聯市場營銷操作在上執行。 請參閱 [建立策略](#create-policy) 的子菜單。 |

**回應**

成功的響應將返回更新策略的詳細資訊。

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

## 更新自定義策略的一部分 {#patch}

>[!IMPORTANT]
>
>您只能更新自定義策略。 如果要啟用或禁用核心策略，請參閱上的 [更新已啟用的核心策略清單](#update-enabled-core)。

可以使用PATCH請求更新策略的特定部分。 與重寫策略的PUT請求不同，PATCH請求只更新請求正文中指定的屬性。 當要啟用或禁用策略時，這特別有用，因為您只需提供指向相應屬性的路徑(`/status`)及其值(`ENABLED` 或 `DISABLED`)。

>[!NOTE]
>
>PATCH請求的負載遵循JSON修補程式格式。 查看 [API基礎指南](../../landing/api-fundamentals.md) 的子菜單。

的 [!DNL Policy Service] API支援JSON修補程式操作 `add`。 `remove`, `replace`，並允許您將多個更新合併到單個呼叫中，如下例所示。

**API格式**

```http
PATCH /policies/custom/{POLICY_ID}
```

| 參數 | 說明 |
| --- | --- |
| `{POLICY_ID}` | 的 `id` 要更新其屬性的策略。 |

**要求**

以下請求使用兩個 `replace` 更改策略狀態的操作 `DRAFT` 至 `ENABLED`，並更新 `description` 的子菜單。

>[!IMPORTANT]
>
>在單個請求中發送多個PATCH操作時，將按照它們在陣列中的顯示順序處理它們。 確保在必要時按正確順序發送請求。

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

成功的響應將返回更新策略的詳細資訊。


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

## 刪除自定義策略 {#delete}

可以通過包括自定義策略 `id` 的子菜單。

>[!WARNING]
>
>刪除後，無法恢復策略。 最佳做法是 [執行查找(GET)請求](#lookup) 首先查看策略，並確認它是您要刪除的正確策略。

**API格式**

```http
DELETE /policies/custom/{POLICY_ID}
```

| 參數 | 說明 |
| --- | --- |
| `{POLICY_ID}` | 要刪除的策略的ID。 |

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

成功響應返回HTTP狀態200(OK)，並返回空白正文。

您可以通過嘗試再次查找(GET)策略來確認刪除。 如果策略已成功刪除，則應收到HTTP 404（未找到）錯誤。

## 檢索啟用的核心策略清單 {#list-enabled-core}

預設情況下，只有啟用的資料治理策略才參與評估。 您可以通過向以下站點發出GET請求來檢索當前由您的組織啟用的核心策略清單 `/enabledCorePolicies` 端點。

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

成功的響應將返回以下項下啟用的核心策略清單 `policyIds` 陣列。

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

## 更新啟用的核心策略清單 {#update-enabled-core}

預設情況下，只有啟用的資料治理策略才參與評估。 通過向 `/enabledCorePolicies` 終結點，您可以使用一次呼叫來更新組織啟用的核心策略清單。

>[!NOTE]
>
>此終結點只能啟用或禁用核心策略。 要啟用或禁用自定義策略，請參閱上的部分 [更新策略的一部分](#patch)。

**API格式**

```http
PUT /enabledCorePolicies
```

**要求**

以下請求根據負載中提供的ID更新啟用的核心策略清單。

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
| `policyIds` | 要啟用的核心策略ID的清單。 未包括的任何核心策略都設定為 `DISABLED` 狀態，不參與評估。 |

**回應**

成功的響應將返回以下項的已啟用核心策略的更新清單： `policyIds` 陣列。

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

定義新策略或更新現有策略後，可以使用 [!DNL Policy Service] API，用於test針對特定標籤或資料集的營銷操作，並查看您的策略是否按預期引發違規。 請參閱 [策略評估終結點](./evaluation.md) 的子菜單。
