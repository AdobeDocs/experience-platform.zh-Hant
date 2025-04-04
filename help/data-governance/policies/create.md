---
keywords: Experience Platform；首頁；熱門主題；資料控管；資料使用原則
solution: Experience Platform
title: 在API中建立資料控管原則
type: Tutorial
description: 瞭解如何使用原則服務API建立資料治理原則。
exl-id: 8483f8a1-efe8-4ebb-b074-e0577e5a81a4
source-git-commit: b48c24ac032cbf785a26a86b50a669d7fcae5d97
workflow-type: tm+mt
source-wordcount: '1199'
ht-degree: 2%

---

# 在API中建立資料治理原則

[原則服務API](https://www.adobe.io/experience-platform-apis/references/policy-service/)可讓您建立和管理資料治理原則，以決定可以對包含特定資料使用標籤的資料採取哪些行銷動作。

本檔案逐步說明如何使用[!DNL Policy Service] API建立治理原則。

>[!NOTE]
>
>如需如何建立存取控制原則的步驟，請參閱[存取控制API](../../access-control/abac/api/policies.md)的`/policies`端點指南。 若要瞭解如何建立同意原則，請參閱[原則UI指南](./user-guide.md#consent-policy)。

## 快速入門

本教學課程需要您實際瞭解下列與建立和評估原則有關的主要概念：

* [Adobe Experience Platform資料控管](../home.md)： [!DNL Experience Platform]用來強制資料使用方式法規遵循的架構。
   * [資料使用標籤](../labels/overview.md)：資料使用標籤套用至XDM資料欄位，指定存取該資料方式的限制。
* [[!DNL Experience Data Model (XDM)]](../../xdm/home.md)： [!DNL Experience Platform]用來組織客戶體驗資料的標準化架構。
* [沙箱](../../sandboxes/home.md)： [!DNL Experience Platform]提供可將單一[!DNL Experience Platform]執行個體分割成個別虛擬環境的虛擬沙箱，以利開發及改進數位體驗應用程式。

開始進行此教學課程之前，請檢閱[開發人員指南](../api/getting-started.md)以取得重要資訊，您必須瞭解這些資訊才能成功呼叫[!DNL Policy Service] API，包括必要的標頭以及如何讀取範例API呼叫。

## 定義行銷動作 {#define-action}

在資料控管架構中，行銷動作是[!DNL Experience Platform]資料消費者採取的動作，需要檢查其是否違反資料使用原則。

建立資料使用原則的第一步，是決定該原則將評估哪些行銷動作。 您可使用下列其中一個選項來達成此目的：

* [查詢現有的行銷動作](#look-up)
* [建立新的行銷動作](#create-new)

### 查詢現有的行銷動作 {#look-up}

您可以透過向其中一個`/marketingActions`端點發出GET請求，查詢要由您的原則評估的現有行銷動作。

**API格式**

視您要查詢[!DNL Experience Platform]提供的行銷動作或貴組織建立的自訂行銷動作而定，請分別使用`marketingActions/core`或`marketingActions/custom`端點。

```http
GET /marketingActions/core
GET /marketingActions/custom
```

**要求**

下列請求使用`marketingActions/custom`端點，它會擷取貴組織定義的所有行銷動作清單。

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應會傳回找到的行銷動作總數(`count`)，並列出`children`陣列中行銷動作本身的詳細資料。

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
| `_links.self.href` | `children`陣列中的每個專案都包含所列行銷動作的URI ID。 |

當您找到要使用的行銷動作時，請記錄其`href`屬性的值。 此值會在[建立原則](#create-policy)的下一個步驟中使用。

### 建立新的行銷動作 {#create-new}

您可以對`/marketingActions/custom/`端點發出PUT要求，並在要求路徑結尾提供行銷動作的名稱，藉此建立新的行銷動作。

**API格式**

```http
PUT /marketingActions/custom/{MARKETING_ACTION_NAME}
```

| 參數 | 說明 |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | 您要建立的新行銷動作的名稱。 此名稱會作為行銷動作的主要識別碼，因此必須是唯一的。 最佳實務建議為行銷動作指定描述清楚但簡潔的名稱。 |

**要求**

下列請求會建立名為「exportToThirdParty」的新自訂行銷動作。 請注意，請求承載中的`name`與請求路徑中提供的名稱相同。

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
| `name` | 您要建立的行銷動作名稱。 此名稱必須符合請求路徑中提供的名稱，否則會發生400 （錯誤請求）錯誤。 |
| `description` | 人類看得懂的行銷動作說明。 |

**回應**

成功的回應會傳回HTTP狀態201 （已建立）和新建立行銷動作的詳細資訊。

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

記錄新建立之行銷動作的URI ID，因為此URI ID將用於建立原則的下一個步驟。

## 建立原則 {#create-policy}

建立新原則需要您提供行銷動作的URI ID，以及禁止該行銷動作的使用標籤運算式。

此運算式稱為原則運算式，而且是包含(A)標籤或(B)運運算元和運算元的物件，但不能同時包含兩者。 反過來，每個運算元也是原則運算式物件。 例如，如果有`C1 OR (C3 AND C7)`標籤，可能會禁止將資料匯出至協力廠商的原則。 此運算式將指定為：

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
>僅支援OR和AND運運算元。

設定原則運算式後，您可以對`/policies/custom`端點發出POST要求，以建立新原則。

**API格式**

```http
POST /policies/custom
```

**要求**

下列請求會建立名為「將資料匯出至第三方」的原則，方法是在請求承載中提供行銷動作和原則運算式。

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
| `marketingActionRefs` | 包含行銷動作`href`值的陣列，取得於[先前的步驟](#define-action)。 雖然上述範例僅列出一個行銷動作，但也可提供多個動作。 |
| `deny` | 原則運算式物件。 定義使用標籤和條件，這些標籤和條件會導致原則拒絕`marketingActionRefs`中參考的行銷動作。 |

**回應**

成功的回應會傳回HTTP狀態201 （已建立）和新建立原則的詳細資訊。

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
| `id` | 唯讀，系統產生的值，可唯一識別原則。 |

記錄新建立之原則的URI ID，以便在下一個步驟中啟用該原則。

## 啟用原則

>[!NOTE]
>
>雖然此步驟是選擇性的，如果您希望讓原則保持在`DRAFT`狀態，請注意，原則預設必須將其狀態設定為`ENABLED`，才能參與評估。 請參閱[原則強制執行](../enforcement/api-enforcement.md)的指南，瞭解如何為處於`DRAFT`狀態的原則制定例外狀況的資訊。

依預設，將`status`屬性設定為`DRAFT`的原則不會參與評估。 您可以透過向`/policies/custom/`端點發出PATCH要求，並在要求路徑結尾提供原則的唯一識別碼，來啟用原則以供評估。

**API格式**

```http
PATCH /policies/custom/{POLICY_ID}
```

| 參數 | 說明 |
| --- | --- |
| `{POLICY_ID}` | 您要啟用之原則的`id`值。 |

**要求**

下列要求會對原則的`status`屬性執行PATCH作業，將其值從`DRAFT`變更為`ENABLED`。

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
| `op` | 要執行的PATCH作業型別。 此請求會執行「取代」操作。 |
| `path` | 要更新之欄位的路徑。 啟用原則時，值必須設為&quot;/status&quot;。 |
| `value` | 要指派給`path`中指定的屬性的新值。 此要求會將原則的`status`屬性設為「ENABLED」。 |

**回應**

成功的回應傳回HTTP狀態200 （確定）和已更新原則的詳細資料，其`status`現在設定為`ENABLED`。

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

依照本教學課程，您已成功建立行銷動作的資料使用原則。 您現在可以繼續有關[強制資料使用原則](../enforcement/api-enforcement.md)的教學課程，以瞭解如何檢查原則違規並在您的體驗應用程式中處理這些違規。

如需[!DNL Policy Service] API中不同可用作業的詳細資訊，請參閱[原則服務開發人員指南](../api/getting-started.md)。 如需如何強制執行[!DNL Real-Time Customer Profile]資料原則的詳細資訊，請參閱有關[強制對象區段遵守資料使用規定的教學課程](../../segmentation/tutorials/governance.md)。

若要瞭解如何在[!DNL Experience Platform]使用者介面中管理使用原則，請參閱[原則使用者指南](user-guide.md)。
