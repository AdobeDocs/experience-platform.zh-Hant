---
keywords: Experience Platform；首頁；熱門主題；資料治理；資料使用策略
solution: Experience Platform
title: 在API中建立資料使用原則
topic-legacy: policies
type: Tutorial
description: 「原則服務API」可讓您建立和管理資料使用原則，以決定對包含特定資料使用標籤的資料可採取哪些行銷動作。 本檔案提供使用Policy Service API建立原則的逐步教學課程。
exl-id: 8483f8a1-efe8-4ebb-b074-e0577e5a81a4
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1219'
ht-degree: 2%

---

# 在API中建立資料使用原則

[原則服務API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dule-policy-service.yaml)可讓您建立和管理資料使用原則，以決定可針對包含特定資料使用標籤的資料採取哪些行銷動作。

本檔案提供使用[!DNL Policy Service] API建立原則的逐步教學課程。 如需API中可用之不同作業的更完整指南，請參閱[政策服務開發人員指南](../api/getting-started.md)。

## 快速入門

本教學課程需要對以下在建立和評估策略時涉及的主要概念有充分的瞭解：

* [Adobe Experience Platform資料治理](../home.md):強制執行資料使 [!DNL Platform] 用合規性的框架。
   * [資料使用標籤](../labels/overview.md):資料使用標籤會套用至XDM資料欄位，指定資料存取限制。
* [[!DNL Experience Data Model (XDM)]](../../xdm/home.md):組織客戶體驗資 [!DNL Platform] 料的標準化架構。
* [沙盒](../../sandboxes/home.md): [!DNL Experience Platform] 提供虛擬沙盒，可將單一執行個體分 [!DNL Platform] 割為不同的虛擬環境，以協助開發和發展數位體驗應用程式。

在開始本教學課程之前，請先閱讀[開發人員指南](../api/getting-started.md)，以取得成功呼叫[!DNL Policy Service] API所需的重要資訊，包括必要的標題和如何讀取範例API呼叫。

## 定義行銷動作{#define-action}

在[!DNL Data Governance]架構中，行銷動作是[!DNL Experience Platform]資料使用者採取的動作，需要檢查資料使用政策是否違規。

建立資料使用原則的第一步是決定該原則將評估的行銷動作。 您可以使用下列其中一個選項來完成此作業：

* [尋找現有的行銷動作](#look-up)
* [建立新的行銷動作](#create-new)

### 尋找現有的行銷動作{#look-up}

您可以向`/marketingActions`端點之一提出GET請求，以尋找由策略評估的現有行銷動作。

**API格式**

視您要尋找由[!DNL Experience Platform]提供的行銷動作或由您的組織建立的自訂行銷動作而定，請分別使用`marketingActions/core`或`marketingActions/custom`端點。

```http
GET /marketingActions/core
GET /marketingActions/custom
```

**要求**

下列請求使用`marketingActions/custom`端點，此端點會擷取IMS組織所定義之所有行銷動作的清單。

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應會傳回找到的行銷動作總數(`count`)，並列出`children`陣列中行銷動作本身的詳細資訊。

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
| `_links.self.href` | `children`陣列中的每個項目都包含列出的行銷動作的URI ID。 |

當您找到要使用的行銷動作時，請記錄其`href`屬性的值。 此值用於[建立策略](#create-policy)的下一步。

### 建立新的行銷動作{#create-new}

您可以透過向`/marketingActions/custom/`端點提出PUT請求，並在請求路徑結尾提供行銷動作的名稱，來建立新的行銷動作。

**API格式**

```http
PUT /marketingActions/custom/{MARKETING_ACTION_NAME}
```

| 參數 | 說明 |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | 您要建立之新行銷動作的名稱。 此名稱會當做行銷動作的主要識別碼，因此必須是唯一的。 最佳實務是為行銷動作指定描述性但簡明的名稱。 |

**要求**

下列請求會建立新的自訂行銷動作，稱為「exportToThirdParty」。 請注意，請求裝載中的`name`與請求路徑中提供的名稱相同。

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
| `name` | 您要建立之行銷動作的名稱。 此名稱必須符合請求路徑中提供的名稱，否則將會發生400（錯誤請求）錯誤。 |
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

記錄新建立之行銷動作的URI ID，因為它將用於建立原則的下一步驟。

## 建立策略{#create-policy}

建立新原則時，您必須提供行銷動作的URI ID，以及禁止該行銷動作的使用標籤的運算式。

此表達式稱為策略表達式，是包含(A)標籤或(B)運算子和操作數（但不同時包含兩者）的對象。 反過來，每個操作數也是策略表達式對象。 例如，如果`C1 OR (C3 AND C7)`標籤存在，則可能禁止將資料匯出至第三方的政策。 此表達式將指定為：

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

配置策略表達式後，可以通過向`/policies/custom`端點發出POST請求來建立新策略。

**API格式**

```http
POST /policies/custom
```

**要求**

下列請求會在請求裝載中提供行銷動作和原則運算式，以建立稱為「將資料匯出至第三方」的原則。

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
| `marketingActionRefs` | 包含[上一步驟](#define-action)中獲得的行銷動作`href`值的陣列。 雖然上述範例僅列出一個行銷動作，但也可提供多個動作。 |
| `deny` | 策略表達式對象。 定義會導致原則拒絕`marketingActionRefs`中參考之行銷動作的使用標籤和條件。 |

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
| `id` | 唯讀、系統生成的值，可唯一標識策略。 |

記錄新建立策略的URI ID，因為它用於下一步以啟用策略。

## 啟用原則

>[!NOTE]
>
>如果您希望將策略保留為`DRAFT`狀態，則此步驟是可選的，但請注意，預設情況下，策略的狀態必須設定為`ENABLED`，才能參與評估。 有關如何對`DRAFT`狀態的策略進行例外的資訊，請參閱[策略實施](../enforcement/api-enforcement.md)指南。

預設情況下，其`status`屬性設定為`DRAFT`的策略不參與評估。 您可以通過向`/policies/custom/`端點發出PATCH請求並在請求路徑末尾提供策略的唯一標識符來啟用策略以進行評估。

**API格式**

```http
PATCH /policies/custom/{POLICY_ID}
```

| 參數 | 說明 |
| --- | --- |
| `{POLICY_ID}` | 要啟用的策略的`id`值。 |

**要求**

以下請求對策略的`status`屬性執行PATCH操作，將其值從`DRAFT`更改為`ENABLED`。

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
| `op` | 要執行的PATCH操作類型。 此請求會執行「取代」操作。 |
| `path` | 要更新的欄位的路徑。 啟用策略時，值必須設定為「/status」。 |
| `value` | 要分配給`path`中指定屬性的新值。 此請求將策略的`status`屬性設定為「ENABLED」。 |

**回應**

成功的響應返回HTTP狀態200(OK)和更新策略的詳細資訊，其`status`現在設定為`ENABLED`。

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

遵循本教學課程，您已成功建立行銷動作的資料使用原則。 您現在可以繼續[實施資料使用原則的教學課程，學習如何檢查是否有違反原則的情況，並在體驗應用程式中處理這些情況。](../enforcement/api-enforcement.md)

有關[!DNL Policy Service] API中不同可用操作的詳細資訊，請參閱[策略服務開發人員指南](../api/getting-started.md)。 如需如何對[!DNL Real-time Customer Profile]資料實施原則的詳細資訊，請參閱[對讀者區段實施資料使用規範的教學課程](../../segmentation/tutorials/governance.md)。

要瞭解如何在[!DNL Experience Platform]用戶介面中管理使用策略，請參閱[策略使用手冊](user-guide.md)。
