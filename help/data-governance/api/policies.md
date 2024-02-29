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

資料治理原則是描述允許或限制您對中的資料執行何種行銷動作的規則 [!DNL Experience Platform]. 此 `/policies` 中的端點 [!DNL Policy Service API] 可讓您以程式設計方式管理組織的資料控管原則。

>[!IMPORTANT]
>
>治理原則不應與存取控制原則混淆，存取控制原則會決定貴組織中特定Platform使用者可存取的特定資料屬性。 請參閱 `/policies` 的端點指南 [存取控制API](../../access-control/abac/api/policies.md) 以取得有關如何以程式設計方式管理存取控制原則的詳細資料。

## 快速入門

本指南中使用的API端點屬於 [[!DNL Policy Service] API](https://www.adobe.io/experience-platform-apis/references/policy-service/). 在繼續之前，請檢閱 [快速入門手冊](getting-started.md) 如需相關檔案的連結，請參閱本檔案範例API呼叫的指南，以及有關成功呼叫任何專案所需標題的重要資訊 [!DNL Experience Platform] API。

## 擷取原則清單 {#list}

您可以列出所有 `core` 或 `custom` 向發出GET請求以制定原則 `/policies/core` 或 `/policies/custom`，依序輸入。

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

成功的回應包括 `children` 列出每個擷取原則的詳細資訊的陣列，包括其 `id` 值。 您可以使用 `id` 要執行的特定原則的欄位 [查詢](#lookup)， [更新](#update)、和 [刪除](#delete) 該原則的要求。

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
| `status` | 原則的目前狀態。 可能的狀態有三種： `DRAFT`， `ENABLED`，或 `DISABLED`. 根據預設，僅限 `ENABLED` 原則會參與評估。 請參閱以下主題的概觀： [原則評估](../enforcement/overview.md) 以取得詳細資訊。 |
| `marketingActionRefs` | 列出原則之所有適用行銷動作的URI的陣列。 |
| `description` | 選擇性說明，提供原則使用案例的後續內容。 |
| `deny` | 說明原則的相關行銷動作限制執行的特定資料使用標籤的物件。 請參閱以下小節： [建立原則](#create-policy) 以取得此屬性的詳細資訊。 |

## 查詢原則 {#look-up}

您可以包含特定原則，以查詢該原則 `id` 屬性位於GET請求的路徑中。

**API格式**

```http
GET /policies/core/{POLICY_ID}
GET /policies/custom/{POLICY_ID}
```

| 參數 | 說明 |
| --- | --- |
| `{POLICY_ID}` | 此 `id` 要查閱的原則的摘要。 |

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
| `status` | 原則的目前狀態。 可能的狀態有三種： `DRAFT`， `ENABLED`，或 `DISABLED`. 根據預設，僅限 `ENABLED` 原則會參與評估。 請參閱以下主題的概觀： [原則評估](../enforcement/overview.md) 以取得詳細資訊。 |
| `marketingActionRefs` | 此陣列會列出原則所有適用行銷動作的URI。 |
| `description` | 選擇性說明，提供原則使用案例的後續內容。 |
| `deny` | 說明原則相關行銷動作限制執行的特定資料使用標籤的物件。 請參閱以下小節： [建立原則](#create-policy) 以取得此屬性的詳細資訊。 |

## 建立自訂原則 {#create-policy}

在 [!DNL Policy Service] API，原則由以下定義：

* 特定行銷動作的參考
* 描述行銷動作被限制執行的資料使用標籤的運算式

為了滿足後一要求，原則定義必須包括關於資料使用標籤存在的布林運算式。 此運算式稱為原則運算式。

原則運算式的提供形式為 `deny` 屬性。 簡單範例 `deny` 只檢查單一標籤是否存在的物件如下所示：

```json
"deny": {
    "label": "C1"
}
```

不過，許多原則會針對資料使用標籤的出現指定更複雜的條件。 若要支援這些使用案例，您也可以包含布林運算來說明您的原則運算式。 原則運算式物件必須包含標籤或運運算元與運算元，但不能同時包含兩者。 反過來，每個運算元也是原則運算式物件。

例如，為了定義禁止對資料執行行銷動作的原則， `C1 OR (C3 AND C7)` 標籤存在，原則的 `deny` 屬性將指定為：

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
| `operator` | 表示同層級中提供的標籤之間的條件關係 `operands` 陣列。 接受的值包括： <ul><li>`OR`：如果有任何標籤，運算式會解析為true `operands` 陣列存在。</li><li>`AND`：只有在 `operands` 陣列存在。</li></ul> |
| `operands` | 一個物件陣列，每個物件分別代表單一標籤或額外的一對 `operator` 和 `operands` 屬性。 標籤和/或作業是否存在 `operands` 陣列會根據其同層級的值解析為true或false `operator` 屬性。 |
| `label` | 套用至原則的單一資料使用標籤的名稱。 |

您可以透過向以下發出POST請求來建立新的自訂原則： `/policies/custom` 端點。

**API格式**

```http
POST /policies/custom
```

**要求**

以下請求會建立限制行銷動作的新原則 `exportToThirdParty` 不在包含標籤的資料上執行 `C1 OR (C3 AND C7)`.

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
| `status` | 原則的目前狀態。 可能的狀態有三種： `DRAFT`， `ENABLED`，或 `DISABLED`. 根據預設，僅限 `ENABLED` 原則會參與評估。 請參閱以下主題的概觀： [原則評估](../enforcement/overview.md) 以取得詳細資訊。 |
| `marketingActionRefs` | 此陣列會列出原則所有適用行銷動作的URI。 行銷動作的URI提供於 `_links.self.href` 在的回應中 [查詢行銷動作](./marketing-actions.md#look-up). |
| `description` | 選擇性說明，提供原則使用案例的後續內容。 |
| `deny` | 說明特定資料使用標籤的原則運算式，其會限制對其執行原則的相關行銷動作。 |

**回應**

成功的回應會傳回新建立原則的詳細資訊，包括其 `id`. 此值是唯讀的，會在建立原則時自動指定。

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
>您只能更新自訂原則。 如果要啟用或停用核心原則，請參閱以下章節： [更新已啟用的核心原則清單](#update-enabled-core).

您可以在PUT請求的路徑中提供其ID，並使用包含完整原則更新形式的裝載，以更新現有的自訂原則。 換言之，PUT要求基本上會重寫原則。

>[!NOTE]
>
>請參閱以下小節： [更新部分自訂原則](#patch) 如果您只想更新原則的一或多個欄位，不要覆寫原則。

**API格式**

```http
PUT /policies/custom/{POLICY_ID}
```

| 參數 | 說明 |
| --- | --- |
| `{POLICY_ID}` | 此 `id` 要更新的原則。 |

**要求**

在此範例中，將資料匯出至協力廠商的條件已變更，現在您需要建立的原則來拒絕此行銷動作，如果 `C1 AND C5` 出現資料標籤。

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
| `status` | 原則的目前狀態。 可能的狀態有三種： `DRAFT`， `ENABLED`，或 `DISABLED`. 根據預設，僅限 `ENABLED` 原則會參與評估。 請參閱以下主題的概觀： [原則評估](../enforcement/overview.md) 以取得詳細資訊。 |
| `marketingActionRefs` | 此陣列會列出原則所有適用行銷動作的URI。 行銷動作的URI提供於 `_links.self.href` 在的回應中 [查詢行銷動作](./marketing-actions.md#look-up). |
| `description` | 選擇性說明，提供原則使用案例的後續內容。 |
| `deny` | 說明特定資料使用標籤的原則運算式，其會限制對其執行原則的相關行銷動作。 請參閱以下小節： [建立原則](#create-policy) 以取得此屬性的詳細資訊。 |

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
>您只能更新自訂原則。 如果要啟用或停用核心原則，請參閱以下章節： [更新已啟用的核心原則清單](#update-enabled-core).

可以使用PATCH請求更新原則的特定部分。 不同於重寫原則的PUT要求，PATCH要求只更新要求內文中指定的屬性。 當您想要啟用或停用原則時，此功能特別實用，因為您只需要提供適當屬性的路徑(`/status`)及其值(`ENABLED` 或 `DISABLED`)。

>[!NOTE]
>
>PATCH請求的裝載遵循JSON修補程式格式。 請參閱 [API基礎指南](../../landing/api-fundamentals.md) 以取得接受的語法的詳細資訊。

此 [!DNL Policy Service] API支援JSON修補程式操作 `add`， `remove`、和 `replace`，並可讓您將數個更新一起合併為單一呼叫，如下列範例所示。

**API格式**

```http
PATCH /policies/custom/{POLICY_ID}
```

| 參數 | 說明 |
| --- | --- |
| `{POLICY_ID}` | 此 `id` 要更新其屬性的原則的。 |

**要求**

以下請求使用兩個 `replace` 變更原則狀態的作業 `DRAFT` 至 `ENABLED`，並更新 `description` 欄位及新的說明。

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

您可以包含自訂原則，刪除自訂原則 `id` 在DELETE請求的路徑中。

>[!WARNING]
>
>一旦刪除，原則就無法復原。 最佳實務是 [執行查詢(GET)請求](#lookup) 首先檢視原則，並確認它是您要移除的正確原則。

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

依預設，只有已啟用的資料治理原則會參與評估。 您可以透過向以下網站發出GET請求，擷取貴組織目前啟用的核心原則清單： `/enabledCorePolicies` 端點。

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

成功的回應會傳回底下啟用的核心原則清單 `policyIds` 陣列。

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

依預設，只有已啟用的資料治理原則會參與評估。 PUT藉由向 `/enabledCorePolicies` 端點，您可使用單一呼叫更新組織的已啟用核心原則清單。

>[!NOTE]
>
>此端點只能啟用或停用核心原則。 若要啟用或停用自訂原則，請參閱以下章節： [更新原則的一部分](#patch).

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
| `policyIds` | 要啟用的核心原則ID清單。 任何未包含的核心原則都會設為 `DISABLED` 狀態，將不參與評估。 |

**回應**

成功的回應會傳回底下啟用的核心原則更新清單 `policyIds` 陣列。

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

定義新原則或更新現有原則後，您可以使用 [!DNL Policy Service] API可針對特定標籤或資料集測試行銷動作，並檢視您的原則是否如預期引發違規。 請參閱 [原則評估端點](./evaluation.md) 以取得詳細資訊。
