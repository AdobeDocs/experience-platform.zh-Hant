---
keywords: Experience Platform；首頁；熱門主題；原則執行；API型執行；資料控管
solution: Experience Platform
title: 策略API端點
topic-legacy: developer guide
description: 資料使用原則是貴組織採用的規則，可說明您可對Experience Platform內的資料執行或限制的行銷動作類型。 /policies端點用於與檢視、建立、更新或刪除資料使用原則相關的所有API呼叫。
exl-id: 62a6f15b-4c12-4269-bf90-aaa04c147053
source-git-commit: 8133804076b1c0adf2eae5b748e86a35f3186d14
workflow-type: tm+mt
source-wordcount: '1813'
ht-degree: 2%

---

# 策略端點

資料使用原則是描述您可對[!DNL Experience Platform]內的資料執行或限制執行之行銷動作類型的規則。 [!DNL Policy Service API]中的`/policies`端點可讓您以程式設計方式管理組織的資料使用原則。

## 快速入門

本指南中使用的API端點是[[!DNL Policy Service] API](https://www.adobe.io/experience-platform-apis/references/policy-service/)的一部分。 繼續之前，請檢閱[快速入門手冊](getting-started.md)，取得相關檔案的連結、閱讀本檔案中範例API呼叫的指南，以及成功呼叫任何[!DNL Experience Platform] API所需的重要標題資訊。

## 檢索策略清單 {#list}

您可以分別向`/policies/core`或`/policies/custom`發出GET請求，以列出所有`core`或`custom`策略。

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
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的響應包括`children`陣列，該陣列列出每個檢索策略的詳細資訊，包括其`id`值。 您可以使用特定策略的`id`欄位來執行該策略的[lookup](#lookup)、[update](#update)和[delete](#delete)請求。

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
| `name` | 策略的顯示名稱。 |
| `status` | 策略的當前狀態。 有三種可能的狀態：`DRAFT`、`ENABLED`或`DISABLED`。 預設情況下，只有`ENABLED`策略參與評估。 有關詳細資訊，請參見[策略評估](../enforcement/overview.md)上的概述。 |
| `marketingActionRefs` | 一個陣列，列出策略的所有適用市場營銷操作的URI。 |
| `description` | 提供策略使用案例的進一步上下文的可選說明。 |
| `deny` | 描述特定資料使用標籤的對象，策略的相關市場營銷操作被限制不執行。 有關此屬性的詳細資訊，請參閱關於[建立策略](#create-policy)的部分。 |

## 查找策略 {#look-up}

您可以在GET請求的路徑中包含該策略的`id`屬性，以查找特定策略。

**API格式**

```http
GET /policies/core/{POLICY_ID}
GET /policies/custom/{POLICY_ID}
```

| 參數 | 說明 |
| --- | --- |
| `{POLICY_ID}` | 要查找的策略的`id`。 |

**要求**

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/dulepolicy/policies/custom/5c6dacdf685a4913dc48937c \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
| `name` | 策略的顯示名稱。 |
| `status` | 策略的當前狀態。 有三種可能的狀態：`DRAFT`、`ENABLED`或`DISABLED`。 預設情況下，只有`ENABLED`策略參與評估。 有關詳細資訊，請參見[策略評估](../enforcement/overview.md)上的概述。 |
| `marketingActionRefs` | 一個陣列，列出策略的所有適用市場營銷操作的URI。 |
| `description` | 提供策略使用案例的進一步上下文的可選說明。 |
| `deny` | 描述特定資料使用標籤的對象，策略的關聯市場營銷操作被限制不執行。 有關此屬性的詳細資訊，請參閱關於[建立策略](#create-policy)的部分。 |

## 建立自訂原則 {#create-policy}

在[!DNL Policy Service] API中，策略由以下項定義：

* 特定行銷動作的參考
* 描述資料使用標籤的運算式，限制對其執行行銷動作

為了滿足後一要求，策略定義必須包括有關資料使用標籤的布爾表達式。 此表達式稱為策略表達式。

策略表達式以每個策略定義內`deny`屬性的形式提供。 簡單`deny`物件的範例若僅檢查單一標籤是否存在，如下所示：

```json
"deny": {
    "label": "C1"
}
```

但是，許多策略都指定了與資料使用標籤是否存在相關的更複雜的條件。 要支援這些使用案例，您還可以包含布爾運算，以描述策略表達式。 策略表達式對象必須包含標籤或運算子和操作數，但不能同時包含這兩者。 反過來，每個操作數也是策略表達式對象。

例如，為了定義一個策略，該策略禁止對`C1 OR (C3 AND C7)`標籤存在的資料執行行銷操作，策略的`deny`屬性將指定為：

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
| `operator` | 指示同級`operands`陣列中提供的標籤之間的條件關係。 接受的值為： <ul><li>`OR`:如果陣列中有任何標籤存在，則運算式會解 `operands` 析為true。</li><li>`AND`:只有在陣列中所有標籤都存在時，運算式才會解 `operands` 析為true。</li></ul> |
| `operands` | 對象陣列，每個對象表示單個標籤或`operator`和`operands`屬性的附加對。 `operands`陣列中是否存在標籤和/或操作根據其同級`operator`屬性的值解析為true或false。 |
| `label` | 應用於策略的單個資料使用情況標籤的名稱。 |

您可以向`/policies/custom`端點發出POST請求，以建立新的自定義策略。

**API格式**

```http
POST /policies/custom
```

**要求**

下列請求會建立新的原則，限制對包含標籤`C1 OR (C3 AND C7)`的資料執行行銷動作`exportToThirdParty`。

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
| `name` | 策略的顯示名稱。 |
| `status` | 策略的當前狀態。 有三種可能的狀態：`DRAFT`、`ENABLED`或`DISABLED`。 預設情況下，只有`ENABLED`策略參與評估。 有關詳細資訊，請參見[策略評估](../enforcement/overview.md)上的概述。 |
| `marketingActionRefs` | 一個陣列，列出策略的所有適用市場營銷操作的URI。 行銷動作的URI在[查詢行銷動作的回應](./marketing-actions.md#look-up)下提供。`_links.self.href` |
| `description` | 提供策略使用案例的進一步上下文的可選說明。 |
| `deny` | 描述特定資料使用情況標籤的策略表達式限制在上執行策略的關聯市場營銷操作。 |

**回應**

成功的響應返回新建立策略的詳細資訊，包括其`id`。 此值為只讀值，在建立策略時自動分配。

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
>您只能更新自訂原則。 如果要啟用或禁用核心策略，請參閱[上更新已啟用的核心策略清單的部分](#update-enabled-core)。

您可以在PUT請求的路徑中提供現有自定義策略的ID，該路徑中包含包含已更新策略整體形式的有效負載。 換句話說，PUT請求實際上會重寫策略。

>[!NOTE]
>
>如果您只想更新策略的一個或多個欄位，而不是覆蓋策略，請參閱[更新自定義策略的一部分的部分。](#patch)

**API格式**

```http
PUT /policies/custom/{POLICY_ID}
```

| 參數 | 說明 |
| --- | --- |
| `{POLICY_ID}` | 要更新的策略的`id`。 |

**要求**

在此示例中，將資料導出到第三方的條件已更改，現在，如果`C1 AND C5`資料標籤存在，則需要您建立的策略以拒絕此市場營銷操作。

以下請求將更新現有策略以包括新策略表達式。 請注意，由於此要求實際上會重新寫入原則，因此即使部分欄位值未更新，所有欄位也必須包含在裝載中。

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
| `name` | 策略的顯示名稱。 |
| `status` | 策略的當前狀態。 有三種可能的狀態：`DRAFT`、`ENABLED`或`DISABLED`。 預設情況下，只有`ENABLED`策略參與評估。 有關詳細資訊，請參見[策略評估](../enforcement/overview.md)上的概述。 |
| `marketingActionRefs` | 一個陣列，列出策略的所有適用市場營銷操作的URI。 行銷動作的URI在[查詢行銷動作的回應](./marketing-actions.md#look-up)下提供。`_links.self.href` |
| `description` | 提供策略使用案例的進一步上下文的可選說明。 |
| `deny` | 描述特定資料使用情況標籤的策略表達式限制在上執行策略的關聯市場營銷操作。 有關此屬性的詳細資訊，請參閱關於[建立策略](#create-policy)的部分。 |

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
>您只能更新自訂原則。 如果要啟用或禁用核心策略，請參閱[上更新已啟用的核心策略清單的部分](#update-enabled-core)。

策略的特定部分可以使用PATCH請求進行更新。 與重寫策略的PUT請求不同，PATCH請求只更新請求正文中指定的屬性。 當要啟用或禁用策略時，這特別有用，因為您只需提供指向相應屬性(`/status`)及其值（`ENABLED`或`DISABLED`）的路徑。

>[!NOTE]
>
>PATCH要求的裝載會遵循JSON修補程式格式。 如需接受語法的詳細資訊，請參閱[API基本指南](../../landing/api-fundamentals.md) 。

[!DNL Policy Service] API支援JSON修補程式操作`add`、`remove`和`replace`，並可讓您將多個更新合併為單一呼叫，如下列範例所示。

**API格式**

```http
PATCH /policies/custom/{POLICY_ID}
```

| 參數 | 說明 |
| --- | --- |
| `{POLICY_ID}` | 要更新其屬性的策略的`id`。 |

**要求**

以下請求使用兩個`replace`操作將策略狀態從`DRAFT`更改為`ENABLED`，並使用新說明更新`description`欄位。

>[!IMPORTANT]
>
>在單一請求中傳送多個PATCH作業時，系統會依陣列中的顯示順序加以處理。 請務必視需要以正確順序傳送請求。

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

## 刪除自定義策略 {#delete}

您可以在DELETE請求的路徑中加入自訂原則的`id`以刪除自訂原則。

>[!WARNING]
>
>刪除後，無法恢復策略。 最佳做法是先[執行查找(GET)請求](#lookup)以查看策略並確認它是您要刪除的正確策略。

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
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應會傳回HTTP狀態200(OK)，並包含空白內文。

您可以嘗試再次查找(GET)原則，以確認刪除。 如果已成功刪除策略，應會收到HTTP 404（找不到）錯誤。

## 擷取已啟用的核心原則清單 {#list-enabled-core}

預設情況下，僅啟用的資料使用策略參與評估。 您可以向`/enabledCorePolicies`端點提出GET請求，以擷取組織目前啟用的核心原則清單。

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
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的響應返回`policyIds`陣列下啟用的核心策略清單。

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

## 更新已啟用的核心原則清單 {#update-enabled-core}

預設情況下，僅啟用的資料使用策略參與評估。 通過向`/enabledCorePolicies`端點發出PUT請求，您可以使用單個呼叫來更新組織已啟用的核心策略清單。

>[!NOTE]
>
>此端點只能啟用或停用核心原則。 要啟用或禁用自定義策略，請參閱[更新策略](#patch)的部分。

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
| `policyIds` | 要啟用的核心策略ID的清單。 未包括的任何核心策略均設為`DISABLED`狀態，且不參與評估。 |

**回應**

成功的響應返回`policyIds`陣列下啟用的核心策略的更新清單。

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

定義新原則或更新現有原則後，您可以使用[!DNL Policy Service] API來測試針對特定標籤或資料集的行銷動作，並查看您的原則是否如預期引發違規。 有關詳細資訊，請參閱[策略評估終結點](./evaluation.md)上的指南。
