---
keywords: Experience Platform；首頁；熱門主題；資料管理；資料使用策略
solution: Experience Platform
title: 在API中建立資料治理策略
type: Tutorial
description: 瞭解如何使用策略服務API建立資料治理策略。
exl-id: 8483f8a1-efe8-4ebb-b074-e0577e5a81a4
source-git-commit: 81f48de908b274d836f551bec5693de13c5edaf1
workflow-type: tm+mt
source-wordcount: '1199'
ht-degree: 2%

---

# 在API中建立資料管理策略

的 [策略服務API](https://www.adobe.io/experience-platform-apis/references/policy-service/) 允許您建立和管理資料治理策略，以確定可以針對包含某些資料使用標籤的資料採取哪些市場營銷操作。

本文檔提供使用 [!DNL Policy Service] API。

>[!NOTE]
>
>有關如何建立訪問控制策略的步驟，請參見 `/policies` 端點指南 [訪問控制API](../../access-control/abac/api/policies.md)。 要瞭解如何建立同意策略，請參閱 [策略UI指南](./user-guide.md#consent-policy)。

## 快速入門

本教程要求對建立和評估策略時涉及的以下關鍵概念有深入的瞭解：

* [Adobe Experience Platform資料治理](../home.md):框架 [!DNL Platform] 強制實施資料使用合規性。
   * [資料使用標籤](../labels/overview.md):資料使用標籤將應用到XDM資料欄位，為如何訪問資料指定限制。
* [[!DNL Experience Data Model (XDM)]](../../xdm/home.md):標準化框架 [!DNL Platform] 組織客戶體驗資料。
* [沙箱](../../sandboxes/home.md): [!DNL Experience Platform] 提供虛擬沙箱，將單個沙箱 [!DNL Platform] 實例到獨立的虛擬環境，以幫助開發和發展數字型驗應用程式。

在開始本教程之前，請複習 [開發者指南](../api/getting-started.md) 獲取您需要瞭解的重要資訊，以便成功撥打 [!DNL Policy Service] API，包括所需的標頭以及如何讀取示例API調用。

## 定義市場營銷活動 {#define-action}

在「資料治理」框架中，市場營銷操作是 [!DNL Experience Platform] 資料使用者獲取的資料，需要檢查是否違反了資料使用策略。

建立資料使用策略的第一步是確定策略將評估的市場營銷操作。 可以使用以下選項之一來完成此操作：

* [查找現有市場營銷活動](#look-up)
* [建立新的市場營銷活動](#create-new)

### 查找現有市場營銷活動 {#look-up}

您可以通過向以下任一策略發出GET請求來查找要由策略評估的現有市場營銷活動 `/marketingActions` 端點。

**API格式**

根據您是否查找由 [!DNL Experience Platform] 或由您的組織建立的自定義市場營銷操作 `marketingActions/core` 或 `marketingActions/custom` 端點。

```http
GET /marketingActions/core
GET /marketingActions/custom
```

**要求**

以下請求使用 `marketingActions/custom` 終結點，它將提取由您的組織定義的所有市場營銷操作的清單。

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的響應返回找到的市場活動總數(`count`)，並列出在 `children` 陣列。

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
            "imsOrg": "{ORG_ID}",
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
            "imsOrg": "{ORG_ID}",
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
| `_links.self.href` | 在 `children` 陣列包含列出的市場營銷操作的URI ID。 |

當您找到要使用的市場營銷活動時，記錄其值 `href` 屬性。 此值將在下一步的 [建立策略](#create-policy)。

### 建立新的市場營銷活動 {#create-new}

您可以通過向以下站點發出PUT請求來建立新的市場營銷活動 `/marketingActions/custom/` 在請求路徑的末尾提供市場營銷操作的名稱。

**API格式**

```http
PUT /marketingActions/custom/{MARKETING_ACTION_NAME}
```

| 參數 | 說明 |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | 要建立的新市場營銷操作的名稱。 此名稱用作市場營銷活動的主要標識符，因此必須唯一。 最佳做法是給營銷活動一個描述性但簡潔的名稱。 |

**要求**

以下請求將建立一個名為&quot;exportToThirdParty&quot;的新自定義市場營銷操作。 請注意 `name` 在請求負載中與請求路徑中提供的名稱相同。

```shell
curl -X PUT \  
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/exportToThirdParty \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "exportToThirdParty",
      "description": "Export data to a third party"
    }'
```

| 屬性 | 說明 |
| --- | --- |
| `name` | 要建立的市場營銷操作的名稱。 此名稱必須與請求路徑中提供的名稱匹配，否則將發生400（錯誤請求）錯誤。 |
| `description` | 市場營銷活動的可讀描述。 |

**回應**

成功的響應返回HTTP狀態201（已建立）和新建立的市場營銷操作的詳細資訊。

```json
{
    "name": "exportToThirdParty",
    "description": "Export data to a third party",
    "imsOrg": "{ORG_ID}",
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
| `_links.self.href` | 市場營銷操作的URI ID。 |

記錄新建立的市場營銷操作的URI ID，因為它將用於建立策略的下一步。

## 建立原則 {#create-policy}

建立新策略要求您提供市場營銷操作的URI ID，其中包含禁止該市場營銷操作的用法標籤的表達式。

此表達式稱為策略表達式，是包含(A)標籤或(B)運算子和操作數的對象，但不同時包含兩者。 反過來，每個操作數也是策略表達式對象。 例如，在以下情況下，可能禁止向第三方出口資料的政策 `C1 OR (C3 AND C7)` 標籤存在。 此表達式將指定為：

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

>[!NOTE]
>
>僅支援OR和AND運算子。

配置策略表達式後，可以通過向 `/policies/custom` 端點。

**API格式**

```http
POST /policies/custom
```

**要求**

以下請求通過在請求負載中提供市場營銷操作和策略表達式來建立名為「將資料導出到第三方」的策略。

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
| `marketingActionRefs` | 包含 `href` 在 [上一步](#define-action)。 雖然上面的示例僅列出一個市場營銷活動，但還可以提供多個活動。 |
| `deny` | 策略表達式對象。 定義使策略拒絕中引用的市場營銷操作的使用標籤和條件 `marketingActionRefs`。 |

**回應**

成功的響應返回HTTP狀態201（已建立）和新建立策略的詳細資訊。

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
    "imsOrg": "{ORG_ID}",
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
| `id` | 唯一標識策略的只讀系統生成的值。 |

記錄新建立策略的URI ID，因為在下一步中將其用於啟用策略。

## 啟用策略

>[!NOTE]
>
>如果希望將策略保留在 `DRAFT` 狀態，請注意，預設情況下策略的狀態必須設定為 `ENABLED` 以參與評估。 請參閱上的指南 [策略執行](../enforcement/api-enforcement.md) 有關如何為中的策略設定例外的資訊 `DRAFT` 狀態。

預設情況下，具有 `status` 屬性設定為 `DRAFT` 不參與評估。 您可以通過向以下站點發出PATCH請求來啟用評估策略 `/policies/custom/` 在請求路徑的末尾提供策略的唯一標識符。

**API格式**

```http
PATCH /policies/custom/{POLICY_ID}
```

| 參數 | 說明 |
| --- | --- |
| `{POLICY_ID}` | 的 `id` 要啟用的策略的值。 |

**要求**

以下請求對 `status` 策略的屬性，將其值從 `DRAFT` 至 `ENABLED`。

```shell
curl -X PATCH \
  https://platform.adobe.io/data/foundation/dulepolicy/policies/custom/5d51f322e553c814e67af1a3
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `op` | 要執行的PATCH操作的類型。 此請求執行「替換」操作。 |
| `path` | 要更新的欄位的路徑。 啟用策略時，必須將值設定為「/status」。 |
| `value` | 要分配給在中指定的屬性的新值 `path`。 此請求設定策略 `status` 屬性。 |

**回應**

成功響應返回HTTP狀態200(OK)及更新策略的詳細資訊，其中 `status` 現在設定為 `ENABLED`。

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
    "imsOrg": "{ORG_ID}",
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

按照本教程，您已成功為市場營銷操作建立了資料使用策略。 現在，您可以繼續上的教程 [強制實施資料使用策略](../enforcement/api-enforcement.md) 瞭解如何檢查策略違規並在您的體驗應用程式中處理它們。

有關中不同可用操作的詳細資訊 [!DNL Policy Service] API，請參見 [策略服務開發人員指南](../api/getting-started.md)。 有關如何強制執行策略的資訊 [!DNL Real-Time Customer Profile] 資料，請參見上的教程 [強制對受眾群實施資料使用合規性](../../segmentation/tutorials/governance.md)。

瞭解如何在 [!DNL Experience Platform] 用戶介面，請參閱 [策略使用手冊](user-guide.md)。
