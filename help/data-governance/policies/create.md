---
keywords: Experience Platform；首頁；熱門主題；資料控管；資料使用原則
solution: Experience Platform
title: 在API中建立資料控管原則
type: Tutorial
description: 了解如何使用Policy Service API建立資料控管原則。
exl-id: 8483f8a1-efe8-4ebb-b074-e0577e5a81a4
source-git-commit: 7b15166ae12d90cbcceb9f5a71730bf91d4560e6
workflow-type: tm+mt
source-wordcount: '1200'
ht-degree: 2%

---

# 在API中建立資料控管原則

此 [策略服務API](https://www.adobe.io/experience-platform-apis/references/policy-service/) 可讓您建立和管理資料控管原則，以決定對包含特定資料使用標籤的資料採取哪些行銷動作。

本檔案提供使用 [!DNL Policy Service] API。

>[!NOTE]
>
>有關如何建立訪問控制策略的步驟，請參見 `/policies` 端點指南 [存取控制API](../../access-control/abac/api/policies.md). 若要了解如何建立同意政策，請參閱 [原則UI指南](./user-guide.md#consent-policy).

## 快速入門

本教學課程需要妥善了解建立和評估原則時涉及的下列重要概念：

* [Adobe Experience Platform資料控管](../home.md):框架 [!DNL Platform] 強制資料使用合規性。
   * [資料使用量標籤](../labels/overview.md):資料使用量標籤會套用至XDM資料欄位，指定存取該資料的方式限制。
* [[!DNL Experience Data Model (XDM)]](../../xdm/home.md):標準化框架 [!DNL Platform] 組織客戶體驗資料。
* [沙箱](../../sandboxes/home.md): [!DNL Experience Platform] 提供可分割單一沙箱的虛擬沙箱 [!DNL Platform] 例項放入個別的虛擬環境，以協助開發及改進數位體驗應用程式。

開始本教學課程之前，請檢閱 [開發人員指南](../api/getting-started.md) 以取得您需要知道的重要資訊，以便成功對 [!DNL Policy Service] API，包括必要的標題，以及如何讀取範例API呼叫。

## 定義行銷動作 {#define-action}

在資料控管架構中，行銷動作是指 [!DNL Experience Platform] 資料使用者採用，需要檢查是否有違反資料使用原則的情況。

建立資料使用原則的第一步是決定原則將評估的行銷動作。 您可以使用下列其中一個選項來完成此作業：

* [查找現有的行銷動作](#look-up)
* [建立新的行銷動作](#create-new)

### 查找現有的行銷動作 {#look-up}

您可以向以下任一變數發出GET請求，以查找由政策評估的現有行銷動作： `/marketingActions` 端點。

**API格式**

視您是否查詢提供的行銷動作而定 [!DNL Experience Platform] 或由您的組織建立的自訂行銷動作，請使用 `marketingActions/core` 或 `marketingActions/custom` 端點。

```http
GET /marketingActions/core
GET /marketingActions/custom
```

**要求**

下列請求會使用 `marketingActions/custom` 端點，會擷取您IMS組織所定義之所有行銷動作的清單。

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應會傳回找到的行銷動作總數(`count`)，並列出行銷動作本身的詳細資訊(位於 `children` 陣列。

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
| `_links.self.href` | 內的每個項目 `children` 陣列包含所列行銷動作的URI ID。 |

當您找到要使用的行銷動作時，請記錄其值 `href` 屬性。 此值會用於 [建立原則](#create-policy).

### 建立新的行銷動作 {#create-new}

您可以向 `/marketingActions/custom/` 端點，並在請求路徑的結尾提供行銷動作的名稱。

**API格式**

```http
PUT /marketingActions/custom/{MARKETING_ACTION_NAME}
```

| 參數 | 說明 |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | 您要建立的新行銷動作名稱。 此名稱可作為行銷動作的主要識別碼，因此必須是唯一的。 最佳實務是為行銷動作命名描述性但簡明。 |

**要求**

下列請求會建立名為「exportToThirdParty」的新自訂行銷動作。 請注意， `name` 在要求裝載中，與要求路徑中提供的名稱相同。

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
| `name` | 您要建立的行銷動作名稱。 此名稱必須符合請求路徑中提供的名稱，否則將會發生400(Bad Request)錯誤。 |
| `description` | 人類看得懂的行銷動作說明。 |

**回應**

成功的回應會傳回HTTP狀態201（已建立），以及新建立行銷動作的詳細資訊。

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
| `_links.self.href` | 行銷動作的URI ID。 |

記錄新建立的行銷操作的URI ID，因為它將用於建立策略的下一個步驟。

## 建立原則 {#create-policy}

建立新策略需要您提供行銷操作的URI ID，以及禁止該行銷操作的使用標籤的表達式。

此表達式稱為策略表達式，是包含(A)標籤或(B)運算子和操作數（但不包括兩者）的對象。 反過來，每個操作數也是策略表達式對象。 例如，若 `C1 OR (C3 AND C7)` 標籤存在。 此運算式將指定為：

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

下列要求會在要求裝載中提供行銷動作和原則運算式，以建立名為「匯出資料至第三方」的原則。

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
| `marketingActionRefs` | 包含 `href` 行銷動作的值，取自 [上一步](#define-action). 雖然上述範例僅列出一個行銷動作，但也可提供多個動作。 |
| `deny` | 策略表達式對象。 定義會導致原則拒絕中參考之行銷動作的使用標籤和條件 `marketingActionRefs`. |

**回應**

成功的響應返回HTTP狀態201（已建立）以及新建立策略的詳細資訊。

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
| `id` | 唯讀、系統生成的值，用於唯一標識策略。 |

記錄新建立策略的URI ID，如下一步中用於啟用策略。

## 啟用策略

>[!NOTE]
>
>如果您想將原則保留在 `DRAFT` 狀態，請注意，依預設，策略的狀態必須設定為 `ENABLED` 以參與評價。 請參閱 [政策執行](../enforcement/api-enforcement.md) 有關如何為 `DRAFT` 狀態。

預設情況下，具有 `status` 屬性設定為 `DRAFT` 不參與評估。 您可以向 `/policies/custom/` 端點，並在請求路徑的末尾提供策略的唯一標識符。

**API格式**

```http
PATCH /policies/custom/{POLICY_ID}
```

| 參數 | 說明 |
| --- | --- |
| `{POLICY_ID}` | 此 `id` 要啟用的策略的值。 |

**要求**

下列請求會對 `status` 屬性，將其值從 `DRAFT` to `ENABLED`.

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
| `op` | 要執行的PATCH操作類型。 此請求會執行「取代」操作。 |
| `path` | 要更新的欄位路徑。 啟用策略時，必須將值設定為「/status」。 |
| `value` | 要指派給 `path`. 此請求會設定政策的 `status` 屬性變更為「已啟用」。 |

**回應**

成功的響應返回HTTP狀態200(OK)，以及更新策略的詳細資訊，及其 `status` 現在設為 `ENABLED`.

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

依照本教學課程，您已成功建立行銷動作的資料使用原則。 您現在可以繼續進行 [強制執行資料使用策略](../enforcement/api-enforcement.md) 了解如何檢查是否違反原則，以及在您的體驗應用程式中處理這些規則。

有關 [!DNL Policy Service] API，請參閱 [策略服務開發人員指南](../api/getting-started.md). 有關如何強制執行 [!DNL Real-Time Customer Profile] 資料，請參閱 [強制遵循對象區段的資料使用方式](../../segmentation/tutorials/governance.md).

若要了解如何在 [!DNL Experience Platform] 使用者介面，請參閱 [原則使用手冊](user-guide.md).
