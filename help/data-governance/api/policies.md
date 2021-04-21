---
keywords: Experience Platform;home；熱門主題；策略實施；基於API的實施；資料治理
solution: Experience Platform
title: 策略API端點
topic-legacy: developer guide
description: 資料使用原則是貴組織採用的規則，可說明您允許或限制對Experience Platform內資料執行的行銷動作類型。 /policys端點用於與查看、建立、更新或刪除資料使用策略相關的所有API調用。
exl-id: 62a6f15b-4c12-4269-bf90-aaa04c147053
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1817'
ht-degree: 2%

---

# 策略端點

資料使用原則是描述您可對[!DNL Experience Platform]內的資料執行或受限制之行銷動作的類型的規則。 [!DNL Policy Service API]中的`/policies`端點可讓您以程式設計方式管理組織的資料使用政策。

## 快速入門

本指南中使用的API端點是[[!DNL Policy Service] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dule-policy-service.yaml)的一部分。 在繼續之前，請先閱讀[快速入門手冊](getting-started.md)，以取得相關檔案的連結、閱讀本檔案中範例API呼叫的指南，以及成功呼叫任何[!DNL Experience Platform] API所需之必要標題的重要資訊。

## 檢索策略清單{#list}

您可以分別向`/policies/core`或`/policies/custom`發出GET請求，以列出所有`core`或`custom`策略。

**API格式**

```http
GET /policies/core
GET /policies/custom
```

**要求**

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

成功的響應包括`children`陣列，該陣列列出了每個檢索到的策略的詳細資訊，包括其`id`值。 您可以使用特定原則的`id`欄位來執行[查閱](#lookup)、[update](#update)和[delete](#delete)要求。

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
| `status` | 策略的當前狀態。 有三種可能的狀態：`DRAFT`、`ENABLED`或`DISABLED`。 預設情況下，只有`ENABLED`策略參與評估。 有關詳細資訊，請參閱[策略評估](../enforcement/overview.md)的概述。 |
| `marketingActionRefs` | 列出策略所有適用行銷動作的URI的陣列。 |
| `description` | 可選說明，提供策略使用案例的進一步上下文。 |
| `deny` | 一種對象，它描述了策略的關聯行銷操作無法對其執行的特定資料使用標籤。 有關此屬性的詳細資訊，請參閱[建立策略](#create-policy)一節。 |

## 查找策略{#look-up}

您可以在請求路徑中加入該策略的`id`屬性，以查找特定策略。

**API格式**

```http
GET /policies/core/{POLICY_ID}
GET /policies/custom/{POLICY_ID}
```

| 參數 | 說明 |
| --- | --- |
| `{POLICY_ID}` | 您要查找的策略的`id`。 |

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
| `status` | 策略的當前狀態。 有三種可能的狀態：`DRAFT`、`ENABLED`或`DISABLED`。 預設情況下，只有`ENABLED`策略參與評估。 有關詳細資訊，請參閱[策略評估](../enforcement/overview.md)的概述。 |
| `marketingActionRefs` | 列出策略所有適用行銷操作的URI的陣列。 |
| `description` | 可選說明，提供策略使用案例的進一步上下文。 |
| `deny` | 一種對象，它描述了策略的關聯行銷操作無法對其執行的特定資料使用標籤。 有關此屬性的詳細資訊，請參閱[建立策略](#create-policy)一節。 |

## 建立自訂原則{#create-policy}

在[!DNL Policy Service] API中，策略由以下內容定義：

* 特定行銷動作的參考
* 描述限制行銷動作執行之資料使用標籤的運算式

為滿足後一個要求，策略定義必須包含關於資料使用標籤存在的布爾表達式。 此表達式稱為策略表達式。

在每個策略定義中以`deny`屬性的形式提供策略表達式。 簡單`deny`物件的範例（僅檢查單一標籤是否存在）如下所示：

```json
"deny": {
    "label": "C1"
}
```

但是，許多策略會針對資料使用標籤的存在指定更複雜的條件。 若要支援這些使用案例，您也可以包含布林運算，以說明原則運算式。 策略表達式對象必須包含標籤或運算子和操作數，但不能同時包含兩者。 反過來，每個操作數也是策略表達式對象。

例如，為了定義禁止對`C1 OR (C3 AND C7)`標籤存在的資料執行行銷動作的策略，策略的`deny`屬性將指定為：

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
| `operator` | 指示在同級`operands`陣列中提供的標籤之間的條件關係。 接受的值為： <ul><li>`OR`:如果陣列中有任何標籤存在，表達式會解 `operands` 析為true。</li><li>`AND`:運算式只會在陣列中所有標籤都存在時解 `operands` 析為true。</li></ul> |
| `operands` | 對象陣列，每個對象代表單個標籤或`operator`和`operands`屬性的另一對。 `operands`陣列中標籤和／或操作的存在根據其同級`operator`屬性的值解析為true或false。 |
| `label` | 套用至原則的單一資料使用標籤的名稱。 |

您可以通過向`/policies/custom`端點發出POST請求來建立新的自定義策略。

**API格式**

```http
POST /policies/custom
```

**要求**

下列請求會建立新原則，限制對包含標籤`C1 OR (C3 AND C7)`的資料執行行銷動作`exportToThirdParty`。

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
| `status` | 策略的當前狀態。 有三種可能的狀態：`DRAFT`、`ENABLED`或`DISABLED`。 預設情況下，只有`ENABLED`策略參與評估。 有關詳細資訊，請參閱[策略評估](../enforcement/overview.md)的概述。 |
| `marketingActionRefs` | 列出策略所有適用行銷操作的URI的陣列。 在[查詢行銷動作](./marketing-actions.md#look-up)的回應中，在`_links.self.href`下提供行銷動作的URI。 |
| `description` | 可選說明，提供策略使用案例的進一步上下文。 |
| `deny` | 描述策略相關行銷動作之特定資料使用標籤的原則運算式，會限制其無法執行。 |

**回應**

成功的響應返回新建策略的詳細資訊，包括其`id`。 此值是唯讀的，在建立原則時會自動指派。

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

## 更新自訂原則{#update}

>[!IMPORTANT]
>
>您只能更新自訂原則。 如果要啟用或禁用核心策略，請參閱[中有關更新已啟用核心策略清單的章節](#update-enabled-core)。

您可以在PUT請求的路徑中提供現有自訂原則的ID，以更新包含完整原則更新形式的裝載。 換言之，PUT請求實質上會改寫策略。

>[!NOTE]
>
>如果您只想更新策略的一個或多個欄位，而不是覆寫策略，請參閱[更新自定義策略的部分部分。](#patch)

**API格式**

```http
PUT /policies/custom/{POLICY_ID}
```

| 參數 | 說明 |
| --- | --- |
| `{POLICY_ID}` | 您要更新的策略的`id`。 |

**要求**

在此範例中，將資料匯出至第三方的條件已經變更，而且，如果`C1 AND C5`資料標籤存在，您現在需要建立的原則才能拒絕此行銷動作。

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
| `status` | 策略的當前狀態。 有三種可能的狀態：`DRAFT`、`ENABLED`或`DISABLED`。 預設情況下，只有`ENABLED`策略參與評估。 有關詳細資訊，請參閱[策略評估](../enforcement/overview.md)的概述。 |
| `marketingActionRefs` | 列出策略所有適用行銷操作的URI的陣列。 在[查詢行銷動作](./marketing-actions.md#look-up)的回應中，在`_links.self.href`下提供行銷動作的URI。 |
| `description` | 可選說明，提供策略使用案例的進一步上下文。 |
| `deny` | 描述策略相關行銷動作之特定資料使用標籤的原則運算式，會限制其無法執行。 有關此屬性的詳細資訊，請參閱[建立策略](#create-policy)一節。 |

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

## 更新自訂原則的一部分{#patch}

>[!IMPORTANT]
>
>您只能更新自訂原則。 如果要啟用或禁用核心策略，請參閱[中有關更新已啟用核心策略清單的章節](#update-enabled-core)。

策略的特定部分可以使用PATCH請求進行更新。 與重寫策略的PUT請求不同，PATCH請求只更新請求主體中指定的屬性。 當您想要啟用或停用原則時，這特別有用，因為您只需要提供適當屬性(`/status`)及其值（`ENABLED`或`DISABLED`）的路徑。

>[!NOTE]
>
>PATCH請求的裝載會遵循JSON修補程式格式。 如需已接受語法的詳細資訊，請參閱[API基礎指南](../../landing/api-fundamentals.md)。

[!DNL Policy Service] API支援JSON修補程式作業`add`、`remove`和`replace`，並可讓您將數個更新合併為單一呼叫，如下例所示。

**API格式**

```http
PATCH /policies/custom/{POLICY_ID}
```

| 參數 | 說明 |
| --- | --- |
| `{POLICY_ID}` | 要更新其屬性的策略的`id`。 |

**要求**

以下請求使用兩個`replace`操作將策略狀態從`DRAFT`更改為`ENABLED` ，並使用新說明更新`description`欄位。

>[!IMPORTANT]
>
>在單一請求中傳送多個PATCH作業時，會依其在陣列中的顯示順序加以處理。 請務必視需要以正確順序傳送請求。

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

## 刪除自訂原則{#delete}

您可以刪除自訂原則，方法是將其`id`納入DELETE請求的路徑。

>[!WARNING]
>
>刪除後，將無法恢復策略。 最好先執行查閱(GET)請求](#lookup)，以檢視原則並確認這是您要移除的正確原則。[

**API格式**

```http
DELETE /policies/custom/{POLICY_ID}
```

| 參數 | 說明 |
| --- | --- |
| `{POLICY_ID}` | 您要刪除之原則的ID。 |

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

成功的回應會傳回HTTP狀態200（確定），但會傳回空白的內文。

您可以嘗試再次查找(GET)原則，以確認刪除。 如果策略已成功刪除，您應該會收到HTTP 404（找不到）錯誤。

## 檢索已啟用核心策略的清單{#list-enabled-core}

依預設，只有啟用的資料使用政策才會參與評估。 通過向`/enabledCorePolicies`端點發出GET請求，可以檢索組織當前啟用的核心策略清單。

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

## 更新已啟用的核心策略清單{#update-enabled-core}

依預設，只有啟用的資料使用政策才會參與評估。 通過向`/enabledCorePolicies`端點發出PUT請求，您可以使用單次調用更新組織的已啟用核心策略清單。

>[!NOTE]
>
>此端點只能啟用或禁用核心策略。 要啟用或禁用自定義策略，請參閱[更新策略的一部分。](#patch)

**API格式**

```http
PUT /enabledCorePolicies
```

**要求**

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
| `policyIds` | 要啟用的核心原則ID清單。 未包含的任何核心策略都設定為`DISABLED`狀態，不參與評估。 |

**回應**

成功的響應返回`policyIds`陣列下已啟用核心策略的更新清單。

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

定義新策略或更新現有策略後，可以使用[!DNL Policy Service] API來測試針對特定標籤或資料集的行銷動作，並查看您的策略是否如預期引發違規。 有關詳細資訊，請參見[策略評估端點](./evaluation.md)上的指南。
