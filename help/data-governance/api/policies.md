---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 策略
topic: developer guide
translation-type: tm+mt
source-git-commit: 12c53122d84e145a699a2a86631dc37ee0073578
workflow-type: tm+mt
source-wordcount: '1756'
ht-degree: 2%

---


# 策略端點

資料使用原則是描述您允許或限制對內資料執行之行銷動作類型的規則 [!DNL Experience Platform]。 中的 `/policies` 端點允許您 [!DNL Policy Service API] 以寫程式方式管理組織的資料使用策略。

## 快速入門

本指南中使用的API端點是 [[!DNL Policy Service] API的一部分](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dule-policy-service.yaml)。 在繼續之前，請先閱讀快速入門 [指南](getting-started.md) ，以取得相關檔案的連結、閱讀本檔案中範例API呼叫的指南，以及成功呼叫任何 [!DNL Experience Platform] API所需之必要標題的重要資訊。

## 檢索策略清單 {#list}

您可以分別向 `core` 或 `custom` 分別發出GET請求，以列 `/policies/core` 出所有或 `/policies/custom`策略。

**API格式**

```http
GET /policies/core
GET /policies/custom
```

**請求**

下列請求會擷取您組織所定義的自訂原則清單。

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/dulepolicy/policies/custom \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的響應包括一 `children` 個陣列，該陣列列出每個檢索到的策略的詳細資訊，包括其 `id` 值。 您可以使用特 `id` 定原則的欄位來執行 [查閱](#lookup)、 [更新和刪](#update)除該原則 [的請求](#delete) 。

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
            "imsOrg": "{IMS_ORG}",
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
            "imsOrg": "{IMS_ORG}",
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
| `name` | 原則的顯示名稱。 |
| `status` | 策略的當前狀態。 有三種可能的狀態： `DRAFT`、 `ENABLED`或 `DISABLED`。 預設情況下，只 `ENABLED` 有策略參與評估。 如需詳細資訊，請 [參閱政策評](../enforcement/overview.md) 估概觀。 |
| `marketingActionRefs` | 列出策略所有適用行銷動作的URI的陣列。 |
| `description` | 可選說明，提供策略使用案例的進一步上下文。 |
| `deny` | 一種對象，它描述了策略的關聯行銷操作無法對其執行的特定資料使用標籤。 有關此屬性的 [詳細資訊](#create-policy) ，請參閱建立策略一節。 |

## 查找策略 {#look-up}

您可以在GET請求的路徑中加入該策略 `id` 的屬性，以查找特定策略。

**API格式**

```http
GET /policies/core/{POLICY_ID}
GET /policies/custom/{POLICY_ID}
```

| 參數 | 說明 |
| --- | --- |
| `{POLICY_ID}` | 你 `id` 要查的政策。 |

**請求**

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/dulepolicy/policies/custom/5c6dacdf685a4913dc48937c \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
    "imsOrg": "{IMS_ORG}",
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
| `status` | 策略的當前狀態。 有三種可能的狀態： `DRAFT`、 `ENABLED`或 `DISABLED`。 預設情況下，只 `ENABLED` 有策略參與評估。 如需詳細資訊，請 [參閱政策評](../enforcement/overview.md) 估概觀。 |
| `marketingActionRefs` | 列出策略所有適用行銷操作的URI的陣列。 |
| `description` | 可選說明，提供策略使用案例的進一步上下文。 |
| `deny` | 一種對象，它描述了策略的關聯行銷操作無法對其執行的特定資料使用標籤。 有關此屬性的 [詳細資訊](#create-policy) ，請參閱建立策略一節。 |

## Create a custom policy {#create-policy}

在 [!DNL Policy Service] API中，原則由下列項目定義：

* 特定行銷動作的參考
* 描述限制行銷動作執行之資料使用標籤的運算式

為滿足後一個要求，策略定義必須包含關於資料使用標籤存在的布爾表達式。 此表達式稱為策 **略表達式**。

在每個策略定義中以屬性的形 `deny` 式提供策略表達式。 僅檢查單一標 `deny` 簽是否存在的簡單對象示例如下所示：

```json
"deny": {
    "label": "C1"
}
```

但是，許多策略會針對資料使用標籤的存在指定更複雜的條件。 若要支援這些使用案例，您也可以包含布林運算，以說明原則運算式。 策略表達式對象必須包 _含標籤_ , _或運算_ 符和操作數，但不能同時包含兩者。 反過來，每個操作數也是策略表達式對象。

例如，為了定義禁止對存在標籤的資料執行行銷動作的原則， `C1 OR (C3 AND C7)` 原則的屬 `deny` 性會指定為：

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
| `operator` | 指示同級陣列中提供的標籤之間的條件 `operands` 關係。 接受的值為： <ul><li>`OR`:如果陣列中有任何標籤存在，表達式會解 `operands` 析為true。</li><li>`AND`:運算式只會在陣列中所有標籤都存在時解析 `operands` 為true。</li></ul> |
| `operands` | 對象陣列，每個對象表示單個標籤或另一對和屬 `operator` 性 `operands` 。 陣列中標籤和／或操作的存在會根 `operands` 據其同級屬性的值解析為true或false `operator` 。 |
| `label` | 套用至原則的單一資料使用標籤的名稱。 |

您可以向端點發出POST請求，以建立新的自訂 `/policies/custom` 原則。

**API格式**

```http
POST /policies/custom
```

**請求**

下列請求會建立新原則，限制對包含標籤的 `exportToThirdParty` 資料執行行銷動作 `C1 OR (C3 AND C7)`。

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
| `status` | 策略的當前狀態。 有三種可能的狀態： `DRAFT`、 `ENABLED`或 `DISABLED`。 預設情況下，只 `ENABLED` 有策略參與評估。 如需詳細資訊，請 [參閱政策評](../enforcement/overview.md) 估概觀。 |
| `marketingActionRefs` | 列出策略所有適用行銷操作的URI的陣列。 行銷動作的URI是在查詢行 `_links.self.href` 銷動作的回 [應下提供的](./marketing-actions.md#look-up)。 |
| `description` | 可選說明，提供策略使用案例的進一步上下文。 |
| `deny` | 描述策略相關行銷動作之特定資料使用標籤的原則運算式，會限制其無法執行。 |

**回應**

成功的回應會傳回新建立之原則的詳細資料，包括其詳細資訊 `id`。 此值是唯讀的，在建立原則時會自動指派。

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
    "imsOrg": "{IMS_ORG}",
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
>您只能更新自訂原則。 如果要啟用或禁用核心策略，請參閱有關更 [新已啟用核心策略清單的部分](#update-enabled-core)。

您可以在PUT請求路徑中提供現有自訂原則的ID，以包含完整原則的更新形式的裝載，借此更新現有自訂原則。 換句話說，PUT請求實質上 _重寫_ 了策略。

>[!NOTE]
>
>如果您只想 [要更新策略的一個或多個欄位](#patch) ，而不是覆寫策略，請參閱更新自定義策略部分的章節。

**API格式**

```http
PUT /policies/custom/{POLICY_ID}
```

| 參數 | 說明 |
| --- | --- |
| `{POLICY_ID}` | 您 `id` 要更新的原則。 |

**請求**

在此範例中，將資料匯出至第三方的條件已經變更，現在您需要建立的原則才能在資料標籤存在時拒絕 `C1 AND C5` 此行銷動作。

以下請求會更新現有策略以包含新策略表達式。 請注意，由於此請求實際上會重寫原則，因此所有欄位都必須包含在裝載中，即使部分欄位值未更新亦然。

```shell
curl -X PUT \
  https://platform.adobe.io/data/foundation/dulepolicy/policies/custom/5c6dacdf685a4913dc48937c \
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
| `status` | 策略的當前狀態。 有三種可能的狀態： `DRAFT`、 `ENABLED`或 `DISABLED`。 預設情況下，只 `ENABLED` 有策略參與評估。 如需詳細資訊，請 [參閱政策評](../enforcement/overview.md) 估概觀。 |
| `marketingActionRefs` | 列出策略所有適用行銷操作的URI的陣列。 行銷動作的URI是在查詢行 `_links.self.href` 銷動作的回 [應下提供的](./marketing-actions.md#look-up)。 |
| `description` | 可選說明，提供策略使用案例的進一步上下文。 |
| `deny` | 描述策略相關行銷動作之特定資料使用標籤的原則運算式，會限制其無法執行。 有關此屬性的 [詳細資訊](#create-policy) ，請參閱建立策略一節。 |

**回應**

成功的回應會傳回更新之原則的詳細資料。

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
    "imsOrg": "{IMS_ORG}",
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

## 更新自訂原則的一部分 {#patch}

>[!IMPORTANT]
>
>您只能更新自訂原則。 如果要啟用或禁用核心策略，請參閱有關更 [新已啟用核心策略清單的部分](#update-enabled-core)。

策略的特定部分可以使用PATCH請求進行更新。 與重寫策略的PUT請求不同，PATCH請求只更新請求主體中指定的屬性。 當您想要啟用或停用原則時，這特別有用，因為您只需要提供適當屬性(`/status`)及其值(`ENABLED` 或 `DISABLED`)的路徑。

>[!NOTE]
>
>PATCH請求的裝載會遵循JSON修補程式格式。 如需接受 [語法的詳細資訊](../../landing/api-fundamentals.md) ，請參閱API基礎指南。

API [!DNL Policy Service] 支援JSON修補程式 `add`、 `remove``replace`和，並可讓您將多個更新合併為單一呼叫，如以下範例所示。

**API格式**

```http
PATCH /policies/custom/{POLICY_ID}
```

| 參數 | 說明 |
| --- | --- |
| `{POLICY_ID}` | 要 `id` 更新其屬性的策略。 |

**請求**

以下請求使用兩 `replace` 個操作將策略狀態從 `DRAFT` 更 `ENABLED`改為，並使用新說明更 `description` 新欄位。

>[!IMPORTANT]
>
>在單個請求中發送多個PATCH操作時，將按照它們在陣列中的顯示順序進行處理。 請務必視需要以正確順序傳送請求。

```SHELL
curl -X PATCH \
  https://platform.adobe.io/data/foundation/dulepolicy/policies/custom/5c6dacdf685a4913dc48937c \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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

成功的回應會傳回更新之原則的詳細資料。


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
    "imsOrg": "{IMS_ORG}",
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

您可以將自訂原則納入DELETE請 `id` 求的路徑，以刪除該原則。

>[!WARNING]
>
>刪除後，將無法恢復策略。 最好先執行查 [閱(GET)請求](#lookup) ，以檢視原則並確認這是您要移除的正確原則。

**API格式**

```http
DELETE /policies/custom/{POLICY_ID}
```

| 參數 | 說明 |
| --- | --- |
| `{POLICY_ID}` | 您要刪除之原則的ID。 |

**請求**

```shell
curl -X DELETE \
  https://platform.adobe.io/data/foundation/dulepolicy/policies/custom/5c6ddb56eb60ca13dbf8b9a8 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應會傳回HTTP狀態200（確定），但會傳回空白的內文。

您可以嘗試再次查找(GET)原則，以確認刪除。 如果策略已成功刪除，您應該會收到HTTP 404（找不到）錯誤。

## 檢索已啟用的核心策略清單 {#list-enabled-core}

依預設，只有啟用的資料使用政策才會參與評估。 您可以向端點發出GET請求，以擷取組織目前啟用的核心原則清 `/enabledCorePolicies` 單。

**API格式**

```http
GET /enabledCorePolicies
```

**請求**

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/dulepolicy/enabledCorePolicies \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的響應返回陣列下啟用的核心策略 `policyIds` 清單。

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
  "imsOrg": "{IMS_ORG}",
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

## 更新已啟用核心原則的清單 {#update-enabled-core}

依預設，只有啟用的資料使用政策才會參與評估。 通過向端點發出PUT請 `/enabledCorePolicies` 求，您可以使用單次調用更新組織的已啟用核心策略清單。

>[!NOTE]
>
>此端點只能啟用或禁用核心策略。 要啟用或禁用自定義策略，請參 [閱更新策略部分一節](#patch)。

**API格式**

```http
PUT /enabledCorePolicies
```

**請求**

下列請求會根據裝載中提供的ID更新已啟用核心原則的清單。

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/dulepolicy/enabledCorePolicies \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
| `policyIds` | 要啟用的核心原則ID清單。 未包含的任何核心政策都設為 `DISABLED` 狀態，不會參與評估。 |

**回應**

成功的響應返回陣列下啟用的核心策略的更新 `policyIds` 清單。

```json
{
  "policyIds": [
    "corepolicy_0001",
    "corepolicy_0002",
    "corepolicy_0007",
    "corepolicy_0008"
  ],
  "imsOrg": "{IMS_ORG}",
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

定義新策略或更新現有策略後，您可以使用 [!DNL Policy Service] API測試針對特定標籤或資料集的行銷動作，並查看您的策略是否如預期提高違規。 如需詳細資訊，請參 [閱政策評估端點](./evaluation.md) 的指南。