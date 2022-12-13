---
keywords: Experience Platform；首頁；熱門主題；原則執行；API型執行；資料控管
solution: Experience Platform
title: 資料控管原則API端點
topic-legacy: developer guide
description: 資料控管原則是貴組織採用的規則，可說明您可在Experience Platform內對資料執行或受限制的行銷動作類型。 /policys端點用於與檢視、建立、更新或刪除資料控管原則相關的所有API呼叫。
exl-id: 62a6f15b-4c12-4269-bf90-aaa04c147053
source-git-commit: 38447348bc96b2f3f330ca363369eb423efea1c8
workflow-type: tm+mt
source-wordcount: '1865'
ht-degree: 2%

---

# 資料控管原則端點

資料控管原則是一種規則，可說明您可對內的資料執行或限制的行銷動作類型 [!DNL Experience Platform]. 此 `/policies` 端點 [!DNL Policy Service API] 可讓您以程式設計方式管理貴組織的資料控管原則。

>[!IMPORTANT]
>
>控管原則與存取控制原則不容混淆，存取控制原則會決定貴組織中特定Platform使用者可存取的特定資料屬性。 請參閱 `/policies` 端點指南 [存取控制API](../../access-control/abac/api/policies.md) 有關如何以寫程式方式管理訪問控制策略的詳細資訊。

## 快速入門

本指南中使用的API端點屬於 [[!DNL Policy Service] API](https://www.adobe.io/experience-platform-apis/references/policy-service/). 繼續之前，請檢閱 [快速入門手冊](getting-started.md) 如需相關檔案的連結、閱讀本檔案中範例API呼叫的指南，以及成功呼叫任何呼叫所需的必要標題的重要資訊 [!DNL Experience Platform] API。

## 檢索策略清單 {#list}

您可以列出所有 `core` 或 `custom` 策略，方法是向 `/policies/core` 或 `/policies/custom`，分別為。

**API格式**

```http
GET /policies/core
GET /policies/custom
```

**要求**

下列請求會擷取您的組織定義的自訂原則清單。

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/dulepolicy/policies/custom \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應包含 `children` 列出每個檢索策略的詳細資訊（包括其詳細資訊）的陣列 `id` 值。 您可以使用 `id` 執行的特定策略欄位 [查閱](#lookup), [更新](#update)，和 [刪除](#delete) 要求執行該政策。

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
| `status` | 策略的當前狀態。 有三種可能的狀態： `DRAFT`, `ENABLED`，或 `DISABLED`. 依預設，僅 `ENABLED` 政策參與評價。 請參閱 [政策評估](../enforcement/overview.md) 以取得更多資訊。 |
| `marketingActionRefs` | 一個陣列，列出策略的所有適用市場營銷操作的URI。 |
| `description` | 提供策略使用案例的進一步上下文的可選說明。 |
| `deny` | 描述特定資料使用標籤的對象，策略的相關市場營銷操作被限制不執行。 請參閱 [建立原則](#create-policy) 以取得此屬性的詳細資訊。 |

## 查找策略 {#look-up}

您可以查找特定策略，方法是將 `id` 屬性(位於GET請求的路徑中)。

**API格式**

```http
GET /policies/core/{POLICY_ID}
GET /policies/custom/{POLICY_ID}
```

| 參數 | 說明 |
| --- | --- |
| `{POLICY_ID}` | 此 `id` 你要查的政策。 |

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
| `status` | 策略的當前狀態。 有三種可能的狀態： `DRAFT`, `ENABLED`，或 `DISABLED`. 依預設，僅 `ENABLED` 政策參與評價。 請參閱 [政策評估](../enforcement/overview.md) 以取得更多資訊。 |
| `marketingActionRefs` | 一個陣列，列出策略的所有適用市場營銷操作的URI。 |
| `description` | 提供策略使用案例的進一步上下文的可選說明。 |
| `deny` | 描述特定資料使用標籤的對象，策略的關聯市場營銷操作被限制不執行。 請參閱 [建立原則](#create-policy) 以取得此屬性的詳細資訊。 |

## 建立自訂原則 {#create-policy}

在 [!DNL Policy Service] API，則策略由以下項定義：

* 特定行銷動作的參考
* 描述資料使用標籤的運算式，限制對其執行行銷動作

為了滿足後一要求，策略定義必須包括有關資料使用標籤的布爾表達式。 此表達式稱為策略表達式。

策略表達式以 `deny` 屬性。 簡單的範例 `deny` 僅檢查單一標籤是否存在的物件看起來如下所示：

```json
"deny": {
    "label": "C1"
}
```

但是，許多策略都指定了與資料使用標籤是否存在相關的更複雜的條件。 要支援這些使用案例，您還可以包含布爾運算，以描述策略表達式。 策略表達式對象必須包含標籤或運算子和操作數，但不能同時包含這兩者。 反過來，每個操作數也是策略表達式對象。

例如，為了定義政策，禁止對資料執行行銷動作，其中 `C1 OR (C3 AND C7)` 標籤存在，策略 `deny` 屬性將指定為：

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
| `operator` | 指示同級中提供的標籤之間的條件關係 `operands` 陣列。 接受的值為： <ul><li>`OR`:如果 `operands` 陣列存在。</li><li>`AND`:只有在 `operands` 陣列存在。</li></ul> |
| `operands` | 物件陣列，每個物件分別代表單一標籤或一組額外的 `operator` 和 `operands` 屬性。 標籤和/或操作在 `operands` 陣列根據其同層級的值解析為true或false `operator` 屬性。 |
| `label` | 應用於策略的單個資料使用情況標籤的名稱。 |

您可以向 `/policies/custom` 端點。

**API格式**

```http
POST /policies/custom
```

**要求**

下列請求會建立新的政策以限制行銷動作 `exportToThirdParty` 從對包含標籤的資料執行 `C1 OR (C3 AND C7)`.

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
| `status` | 策略的當前狀態。 有三種可能的狀態： `DRAFT`, `ENABLED`，或 `DISABLED`. 依預設，僅 `ENABLED` 政策參與評價。 請參閱 [政策評估](../enforcement/overview.md) 以取得更多資訊。 |
| `marketingActionRefs` | 一個陣列，列出策略的所有適用市場營銷操作的URI。 行銷動作的URI提供於 `_links.self.href` 在 [查詢行銷動作](./marketing-actions.md#look-up). |
| `description` | 提供策略使用案例的進一步上下文的可選說明。 |
| `deny` | 描述特定資料使用情況標籤的策略表達式限制在上執行策略的關聯市場營銷操作。 |

**回應**

成功的響應返回新建立策略的詳細資訊，包括其 `id`. 此值為只讀值，在建立策略時自動分配。

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
>您只能更新自訂原則。 如果您想要啟用或停用核心原則，請參閱 [更新已啟用的核心原則清單](#update-enabled-core).

您可以在PUT請求的路徑中提供現有自定義策略的ID，該路徑中包含包含已更新策略整體形式的有效負載。 換句話說，PUT請求實際上會重寫策略。

>[!NOTE]
>
>請參閱 [更新自訂原則的一部分](#patch) 如果您只想更新策略的一個或多個欄位，而不是覆蓋它。

**API格式**

```http
PUT /policies/custom/{POLICY_ID}
```

| 參數 | 說明 |
| --- | --- |
| `{POLICY_ID}` | 此 `id` 要更新的策略。 |

**要求**

在此範例中，將資料匯出至第三方的條件已變更，現在您需要您建立的原則，以在 `C1 AND C5` 資料標籤存在。

以下請求將更新現有策略以包括新策略表達式。 請注意，由於此要求實際上會重新寫入原則，因此即使部分欄位值未更新，所有欄位也必須包含在裝載中。

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
| `status` | 策略的當前狀態。 有三種可能的狀態： `DRAFT`, `ENABLED`，或 `DISABLED`. 依預設，僅 `ENABLED` 政策參與評價。 請參閱 [政策評估](../enforcement/overview.md) 以取得更多資訊。 |
| `marketingActionRefs` | 一個陣列，列出策略的所有適用市場營銷操作的URI。 行銷動作的URI提供於 `_links.self.href` 在 [查詢行銷動作](./marketing-actions.md#look-up). |
| `description` | 提供策略使用案例的進一步上下文的可選說明。 |
| `deny` | 描述特定資料使用情況標籤的策略表達式限制在上執行策略的關聯市場營銷操作。 請參閱 [建立原則](#create-policy) 以取得此屬性的詳細資訊。 |

**回應**

成功的響應返回更新策略的詳細資訊。

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

## 更新自訂原則的一部分 {#patch}

>[!IMPORTANT]
>
>您只能更新自訂原則。 如果您想要啟用或停用核心原則，請參閱 [更新已啟用的核心原則清單](#update-enabled-core).

策略的特定部分可以使用PATCH請求進行更新。 與重寫策略的PUT請求不同，PATCH請求只更新請求正文中指定的屬性。 當要啟用或禁用策略時，這特別有用，因為您只需提供指向相應屬性的路徑(`/status`)及其值(`ENABLED` 或 `DISABLED`)。

>[!NOTE]
>
>PATCH要求的裝載會遵循JSON修補程式格式。 請參閱 [API基礎指南](../../landing/api-fundamentals.md) 以取得接受語法的詳細資訊。

此 [!DNL Policy Service] API支援JSON修補程式操作 `add`, `remove`，和 `replace`，可讓您將多個更新合併為單一呼叫，如下列範例所示。

**API格式**

```http
PATCH /policies/custom/{POLICY_ID}
```

| 參數 | 說明 |
| --- | --- |
| `{POLICY_ID}` | 此 `id` 要更新其屬性的策略。 |

**要求**

下列要求使用兩個 `replace` 操作，從 `DRAFT` to `ENABLED`，以及更新 `description` 欄位中填入新說明。

>[!IMPORTANT]
>
>在單一請求中傳送多個PATCH作業時，系統會依陣列中的顯示順序加以處理。 請務必視需要以正確順序傳送請求。

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

成功的響應返回更新策略的詳細資訊。


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

您可以刪除自訂原則，方法是將 `id` 在DELETE請求的路徑中。

>[!WARNING]
>
>刪除後，無法恢復策略。 最佳實務是 [執行查閱(GET)請求](#lookup) 首先，查看策略並確認它是您要刪除的正確策略。

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

成功的回應會傳回HTTP狀態200(OK)，並包含空白內文。

您可以嘗試再次查找(GET)原則，以確認刪除。 如果已成功刪除策略，應會收到HTTP 404（找不到）錯誤。

## 擷取已啟用的核心原則清單 {#list-enabled-core}

預設情況下，只有啟用的資料治理策略才參與評估。 您可以向 `/enabledCorePolicies` 端點。

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

成功的回應會傳回 `policyIds` 陣列。

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

預設情況下，只有啟用的資料治理策略才參與評估。 向 `/enabledCorePolicies` 端點，您可以使用單一呼叫來更新貴組織的已啟用核心原則清單。

>[!NOTE]
>
>此端點只能啟用或停用核心原則。 若要啟用或停用自訂原則，請參閱 [更新策略的一部分](#patch).

**API格式**

```http
PUT /enabledCorePolicies
```

**要求**

下列要求會根據裝載中提供的ID更新已啟用核心原則的清單。

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
| `policyIds` | 要啟用的核心策略ID的清單。 未包含的任何核心原則都會設為 `DISABLED` 狀態，不參與評估。 |

**回應**

成功的回應會傳回 `policyIds` 陣列。

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

定義新策略或更新現有策略後，可以使用 [!DNL Policy Service] 針對特定標籤或資料集測試行銷動作，並查看您的原則是否如預期引發違反行為。 請參閱 [策略評估端點](./evaluation.md) 以取得更多資訊。
