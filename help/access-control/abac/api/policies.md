---
keywords: Experience Platform；首頁；熱門主題；api；基於屬性的訪問控制；基於屬性的訪問控制
solution: Experience Platform
title: 訪問控制策略API終結點
description: 基於屬性的訪問控制API中的/policys端點允許您以寫程式方式管理Adobe Experience Platform的策略。
exl-id: 07690f43-fdd9-4254-9324-84e6bd226743
source-git-commit: 05e63064dc8eb3f070a383f508cc4a86d4f5e9cc
workflow-type: tm+mt
source-wordcount: '1443'
ht-degree: 2%

---

# 訪問控制策略終結點

>[!IMPORTANT]
>
>基於屬性的訪問控制目前在面向美國醫療保健客戶的有限版本中提供。 這一功能一旦完全發佈，將可供所有Real-time Customer Data Platform客戶使用。

訪問控制策略是將屬性集合在一起以建立允許和不允許的操作的語句。 這些策略可以是本地策略或全局策略，並且可以覆蓋其他策略。 的 `/policies` 基於屬性的訪問控制API中的端點允許您以寫程式方式管理策略，包括有關管理策略的規則及其各自的主題條件的資訊。

>[!IMPORTANT]
>
>不要將此終結點與 `/policies` 端點 [資料治理API](../../../data-governance/api/policies.md)，用於管理資料使用策略。

## 快速入門

本指南中使用的API終結點是基於屬性的訪問控制API的一部分。 在繼續之前，請查看 [入門指南](./getting-started.md) 有關相關文檔的連結、閱讀本文檔中示例API調用的指南，以及有關成功調用任何Experience PlatformAPI所需標頭的重要資訊。

## 檢索策略清單 {#list}

向 `/policies` 終結點：列出組織中的所有現有策略。

**API格式**

```http
GET /policies
```

**要求**

以下請求檢索現有策略的清單。

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/access-control/administration/policies \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
```

**回應**

成功的響應返回現有策略的清單。

```json
{
  {
      "id": "7019068e-a3a0-48ce-b56b-008109470592",
      "imsOrgId": "{IMS_ORG}",
      "createdBy": "{CREATED_BY}",
      "createdAt": 1652892767559,
      "modifiedBy": "{MODIFIED_BY}",
      "modifiedAt": 1652895736367,
      "name": "schema-field",
      "description": "schema-field",
      "status": "inactive",
      "subjectCondition": null,
      "rules": [
          {
              "effect": "Deny",
              "resource": "/orgs/{IMS_ORG}/sandboxes/xql/schemas/*/schema-fields/*",
              "condition": "{\"adobe.match_all_labels_by_prefix\":[{\"var\":\"subject.roles.labels\"},\"core/\",{\"var\":\"resource.labels\"}]}",
              "actions": [
                  "com.adobe.action.read",
                  "com.adobe.action.write",
                  "com.adobe.action.view"
              ]
          },
          {
              "effect": "Permit",
              "resource": "/orgs/{IMS_ORG}/sandboxes/*/schemas/*/schema-fields/*",
              "condition": "{\"adobe.match_all_labels_by_prefix\":[{\"var\":\"subject.roles.labels\"},\"core/\",{\"var\":\"resource.labels\"}]}",
              "actions": [
                  "com.adobe.action.delete"
              ]
          },
          {
              "effect": "Deny",
              "resource": "/orgs/{IMS_ORG}/sandboxes/delete-sandbox-adfengine-test-8/segments/*",
              "condition": "{\"!\":[{\"adobe.match_any_labels_by_prefix\":[{\"var\":\"subject.roles.labels\"},\"custom/\",{\"var\":\"resource.labels\"}]}]}",
              "actions": [
                  "com.adobe.action.write"
              ]
          }
      ],
      "_etag": "\"0300593f-0000-0200-0000-62852ff80000\""
  },
  {
      "id": "13138ef6-c007-495d-837f-0a248867e219",
      "imsOrgId": "{IMS_ORG}",
      "createdBy": "{CREATED_BY}",
      "createdAt": 1652859368555,
      "modifiedBy": "{MODIFIED_BY}",
      "modifiedAt": 1652890780206,
      "name": "Documentation-Copy",
      "description": "xyz",
      "status": "active",
      "subjectCondition": null,
      "rules": [
          {
              "effect": "Permit",
              "resource": "orgs/{IMS_ORG}/sandboxes/ro-sand/schemas/*/schema-fields/*",
              "condition": "{\"!\":[{\"or\":[{\"adobe.match_all_labels_by_prefix\":[{\"var\":\"subject.roles.labels\"},\"core/\",{\"var\":\"resource.labels\"}]},{\"!\":[{\"and\":[{\"adobe.match_any_labels_by_prefix\":[{\"var\":\"subject.roles.labels\"},\"core/\",{\"var\":\"resource.labels\"}]},{\"adobe.match_all_labels_by_prefix\":[{\"var\":\"subject.roles.labels\"},\"core/\",{\"var\":\"resource.labels\"}]}]}]}]}]}",
              "actions": [
                  "com.adobe.action.read"
              ]
          },
          {
              "effect": "Deny",
              "resource": "orgs/{IMS_ORG}/sandboxes/*/segments/*",
              "condition": "{\"!\":[{\"or\":[{\"adobe.match_any_labels_by_prefix\":[{\"var\":\"subject.roles.labels\"},\"core/\",{\"var\":\"resource.labels\"}]},{\"adobe.match_all_labels_by_prefix\":[{\"var\":\"subject.roles.labels\"},\"custom/\",{\"var\":\"resource.labels\"}]}]}]}",
              "actions": [
                  "com.adobe.action.read"
              ]
          }
      ],
      "_etag": "\"0300d43c-0000-0200-0000-62851c9c0000\""
  },
}
```

| 屬性 | 說明 |
| --- | --- |
| `id` | 與策略對應的ID。 此標識符是自動生成的，可用於查找、更新和刪除策略。 |
| `imsOrgId` | 可訪問查詢策略的組織。 |
| `createdBy` | 建立策略的用戶的ID。 |
| `createdAt` | 建立策略的時間。 的 `createdAt` 屬性在unix劃分時間戳中顯示。 |
| `modifiedBy` | 上次更新策略的用戶的ID。 |
| `modifiedAt` | 上次更新策略的時間。 的 `modifiedAt` 屬性在unix劃分時間戳中顯示。 |
| `name` | 策略的名稱。 |
| `description` | （可選）可添加以提供有關特定策略的詳細資訊的屬性。 |
| `status` | 策略的當前狀態。 此屬性定義策略當前是否 `active` 或 `inactive`。 |
| `subjectCondition` | 適用於對象的條件。 主題是具有請求訪問資源以執行操作的特定屬性的用戶。 在這個例子中， `subjectCondition` 是應用於主題屬性的類似查詢的條件。 |
| `rules` | 定義策略的規則集。 規則定義哪些屬性組合已授權，以便使用者成功對資源執行操作。 |
| `rules.effect` | 在考慮值後產生的效果 `action`。 `condition` 和 `resource`。 可能的值包括： `permit`。 `deny`或 `indeterminate`。 |
| `rules.resource` | 主題可以訪問或無法訪問的資產或對象。  資源可以是檔案、應用程式、伺服器，甚至是API。 |
| `rules.condition` | 應用於資源的條件。 例如，如果資源是架構，則架構可以應用某些標籤，這些標籤有助於針對該架構的操作是允許的還是不允許的。 |
| `rules.action` | 允許主體對查詢的資源執行的操作。 可能的值包括： `read`。 `create`。 `edit`, `delete`。 |

## 按ID查找策略詳細資訊 {#lookup}

向 `/policies` 終結點，同時在請求路徑中提供策略ID以檢索有關該單個策略的資訊。

**API格式**

```http
GET /policies/{POLICY_ID}
```

| 參數 | 說明 |
| --- | --- |
| {POLICY_ID} | 要檢索的策略的ID。 |

**要求**

以下請求檢索有關單個策略的資訊。

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/access-control/administration/policies/13138ef6-c007-495d-837f-0a248867e219 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
```

**回應**

成功的請求返回有關查詢的策略ID的資訊。

```json
{
    "id": "13138ef6-c007-495d-837f-0a248867e219",
    "imsOrgId": "{IMS_ORG}",
    "createdBy": "{CREATED_BY}",
    "createdAt": 1652859368555,
    "modifiedBy": "{MODIFIED_BY}",
    "modifiedAt": 1652890780206,
    "name": "Documentation-Copy",
    "description": "xyz",
    "status": "active",
    "subjectCondition": null,
    "rules": [
        {
            "effect": "Permit",
            "resource": "orgs/{IMS_ORG}/sandboxes/ro-sand/schemas/*/schema-fields/*",
            "condition": "{\"!\":[{\"or\":[{\"adobe.match_all_labels_by_prefix\":[{\"var\":\"subject.roles.labels\"},\"core/\",{\"var\":\"resource.labels\"}]},{\"!\":[{\"and\":[{\"adobe.match_any_labels_by_prefix\":[{\"var\":\"subject.roles.labels\"},\"core/\",{\"var\":\"resource.labels\"}]},{\"adobe.match_all_labels_by_prefix\":[{\"var\":\"subject.roles.labels\"},\"core/\",{\"var\":\"resource.labels\"}]}]}]}]}]}",
            "actions": [
                "com.adobe.action.read"
            ]
        },
        {
            "effect": "Deny",
            "resource": "orgs/{IMS_ORG}/sandboxes/*/segments/*",
            "condition": "{\"!\":[{\"or\":[{\"adobe.match_any_labels_by_prefix\":[{\"var\":\"subject.roles.labels\"},\"core/\",{\"var\":\"resource.labels\"}]},{\"adobe.match_all_labels_by_prefix\":[{\"var\":\"subject.roles.labels\"},\"custom/\",{\"var\":\"resource.labels\"}]}]}]}",
            "actions": [
                "com.adobe.action.read"
            ]
        }
    ],
    "_etag": "\"0300d43c-0000-0200-0000-62851c9c0000\""
}
```

| 屬性 | 說明 |
| --- | --- |
| `id` | 與策略對應的ID。 此標識符是自動生成的，可用於查找、更新和刪除策略。 |
| `imsOrgId` | 可訪問查詢策略的組織。 |
| `createdBy` | 建立策略的用戶的ID。 |
| `createdAt` | 建立策略的時間。 的 `createdAt` 屬性在unix劃分時間戳中顯示。 |
| `modifiedBy` | 上次更新策略的用戶的ID。 |
| `modifiedAt` | 上次更新策略的時間。 的 `modifiedAt` 屬性在unix劃分時間戳中顯示。 |
| `name` | 策略的名稱。 |
| `description` | （可選）可添加以提供有關特定策略的詳細資訊的屬性。 |
| `status` | 策略的當前狀態。 此屬性定義策略當前是否 `active` 或 `inactive`。 |
| `subjectCondition` | 適用於對象的條件。 主題是具有請求訪問資源以執行操作的特定屬性的用戶。 在這個例子中， `subjectCondition` 是應用於主題屬性的類似查詢的條件。 |
| `rules` | 定義策略的規則集。 規則定義哪些屬性組合已授權，以便使用者成功對資源執行操作。 |
| `rules.effect` | 在考慮值後產生的效果 `action`。 `condition` 和 `resource`。 可能的值包括： `permit`。 `deny`或 `indeterminate`。 |
| `rules.resource` | 主題可以訪問或無法訪問的資產或對象。  資源可以是檔案、應用程式、伺服器，甚至是API。 |
| `rules.condition` | 應用於資源的條件。 例如，如果資源是架構，則架構可以應用某些標籤，這些標籤有助於針對該架構的操作是允許的還是不允許的。 |
| `rules.action` | 允許主體對查詢的資源執行的操作。 可能的值包括： `read`。 `create`。 `edit`, `delete`。 |


## 建立策略 {#create}

要建立新策略，請向 `/policies` 端點。

**API格式**

```http
POST /policies
```

**要求**

以下請求將建立名為的新策略： `acme-integration-policy`。

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/access-control/administration/policies \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}'
  -d'{
      "name": "acme-integration-policy",
      "description": "Policy for ACME",
      "imsOrgId": "{IMS_ORG}",
      "rules": [
        {
          "effect": "Permit",
          "resource": "/orgs/{IMS_ORG}/sandboxes/*",
          "condition": "{\"or\":[{\"adobe.match_any_labels_by_prefix\":[{\"var\":\"subject.roles.labels\"},\"core/\",{\"var\":\"resource.labels\"}]},{\"!\":[{\"adobe.match_all_labels_by_prefix\":[{\"var\":\"subject.roles.labels\"},\"core/\",{\"var\":\"resource.labels\"}]}]}]}",
          "actions": [
            "read"
          ]
        }
      ]
    }'
```

| 參數 | 說明 |
| --- | --- |
| `name` | 策略的名稱。 |
| `description` | （可選）可添加以提供有關特定策略的詳細資訊的屬性。 |
| `imsOrgId` | 包含策略的組織。 |
| `rules` | 定義策略的規則集。 規則定義哪些屬性組合已授權，以便使用者成功對資源執行操作。 |
| `rules.effect` | 在考慮值後產生的效果 `action`。 `condition` 和 `resource`。 可能的值包括： `permit`。 `deny`或 `indeterminate`。 |
| `rules.resource` | 主題可以訪問或無法訪問的資產或對象。  資源可以是檔案、應用程式、伺服器，甚至是API。 |
| `rules.condition` | 應用於資源的條件。 例如，如果資源是架構，則架構可以應用某些標籤，這些標籤有助於針對該架構的操作是允許的還是不允許的。 |
| `rules.action` | 允許主體對查詢的資源執行的操作。 可能的值包括： `read`。 `create`。 `edit`, `delete`。 |

**回應**

成功的請求將返回新建立的策略，包括其唯一策略ID和關聯規則。

```json
{
    "id": "c3863937-5d40-448d-a7be-416e538f955e",
    "imsOrgId": "{IMS_ORG}",
    "createdBy": "{CREATED_BY}",
    "createdAt": 1652988384458,
    "modifiedBy": "{MODIFIED_BY}",
    "modifiedAt": 1652988384458,
    "name": "acme-integration-policy",
    "description": "Policy for ACME",
    "status": "active",
    "subjectCondition": null,
    "rules": [
        {
            "effect": "Permit",
            "resource": "/orgs/{IMS_ORG}/sandboxes/*",
            "condition": "{\"or\":[{\"adobe.match_any_labels_by_prefix\":[{\"var\":\"subject.roles.labels\"},\"core/\",{\"var\":\"resource.labels\"}]},{\"!\":[{\"adobe.match_all_labels_by_prefix\":[{\"var\":\"subject.roles.labels\"},\"core/\",{\"var\":\"resource.labels\"}]}]}]}",
            "actions": [
                "read"
            ]
        }
    ],
    "_etag": null
}
```

| 屬性 | 說明 |
| --- | --- |
| `id` | 與策略對應的ID。 此標識符是自動生成的，可用於查找、更新和刪除策略。 |
| `name` | 策略的名稱。 |
| `rules` | 定義策略的規則集。 規則定義哪些屬性組合已授權，以便使用者成功對資源執行操作。 |
| `rules.effect` | 在考慮值後產生的效果 `action`。 `condition` 和 `resource`。 可能的值包括： `permit`。 `deny`或 `indeterminate`。 |
| `rules.resource` | 主題可以訪問或無法訪問的資產或對象。  資源可以是檔案、應用程式、伺服器，甚至是API。 |
| `rules.condition` | 應用於資源的條件。 例如，如果資源是架構，則架構可以應用某些標籤，這些標籤有助於針對該架構的操作是允許的還是不允許的。 |
| `rules.action` | 允許主體對查詢的資源執行的操作。 可能的值包括： `read`。 `create`。 `edit`, `delete`。 |


## 按策略ID更新策略 {#put}

要更新單個策略的規則，請向 `/policies` 終結點，同時提供要在請求路徑中更新的策略的ID。

**API格式**

```http
PUT /policies/{POLICY_ID}
```

| 參數 | 說明 |
| --- | --- |
| {POLICY_ID} | 要更新的策略的ID。 |

**要求**

```shell
curl -X PUT \
  https://platform.adobe.io/data/foundation/access-control/administration/policies/8cf487d7-3642-4243-a8ea-213d72f694b9 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}'
  -d'{
      "id": "8cf487d7-3642-4243-a8ea-213d72f694b9",
      "imsOrgId": "{IMS_ORG}",
      "name": "test-2",
      "rules": [
      {
        "effect": "Deny",
        "resource": "/orgs/{IMS_ORG}/sandboxes/*",
        "condition": "{\"or\":[{\"adobe.match_any_labels_by_prefix\":[{\"var\":\"subject.roles.labels\"},\"core/\",{\"var\":\"resource.labels\"}]},{\"!\":[{\"adobe.match_all_labels_by_prefix\":[{\"var\":\"subject.roles.labels\"},\"core/\",{\"var\":\"resource.labels\"}]}]}]}",
        "actions": [
          "read"
        ]
      }
    ]
  }'
```

**回應**

成功的響應將返回更新的策略。

```json
{
    "id": "8cf487d7-3642-4243-a8ea-213d72f694b9",
    "imsOrgId": "{IMS_ORG}",
    "createdBy": "{CREATED_BY}",
    "createdAt": 1652988866647,
    "modifiedBy": "{MODIFIED_BY}",
    "modifiedAt": 1652989297287,
    "name": "test-2",
    "description": null,
    "status": "active",
    "subjectCondition": null,
    "rules": [
        {
            "effect": "Deny",
            "resource": "/orgs/{IMS_ORG}/sandboxes/*",
            "condition": "{\"or\":[{\"adobe.match_any_labels_by_prefix\":[{\"var\":\"subject.roles.labels\"},\"core/\",{\"var\":\"resource.labels\"}]},{\"!\":[{\"adobe.match_all_labels_by_prefix\":[{\"var\":\"subject.roles.labels\"},\"core/\",{\"var\":\"resource.labels\"}]}]}]}",
            "actions": [
                "read"
            ]
        }
    ],
    "_etag": null
}
```

## 更新策略屬性 {#patch}

要更新單個策略的屬性，請向 `/policies` 終結點，同時提供要在請求路徑中更新的策略的ID。

**API格式**

```http
PATCH /policies/{POLICY_ID}
```

| 參數 | 說明 |
| --- | --- |
| {POLICY_ID} | 要更新的策略的ID。 |

**要求**

以下請求將替換 `/description` 在策略ID中 `c3863937-5d40-448d-a7be-416e538f955e`。

```shell
curl -X PATCH \
  https://platform.adobe.io/data/foundation/access-control/administration/policies/c3863937-5d40-448d-a7be-416e538f955e \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}'
  -d'{
    "operations": [
      {
        "op": "replace",
        "path": "/description",
        "value": "Pre-set policy to be applied for ACME"
      }
    ]
  }'
```

| 運作 | 說明 |
| --- | --- |
| `op` | 用於定義更新角色所需操作的操作調用。 操作包括： `add`。 `replace`, `remove`。 |
| `path` | 要更新的參數的路徑。 |
| `value` | 要用更新參數的新值。 |

**回應**

成功的響應將返回查詢的策略ID，其中包含更新的說明。

```json
{
    "id": "c3863937-5d40-448d-a7be-416e538f955e",
    "imsOrgId": "{IMS_ORG}",
    "createdBy": "acp_accessControlService",
    "createdAt": 1652988384458,
    "modifiedBy": "acp_accessControlService",
    "modifiedAt": 1652988384458,
    "name": "acme-integration-policy",
    "description": "Pre-set policy to be applied for ACME",
    "status": "active",
    "subjectCondition": null,
    "rules": [
        {
            "effect": "Permit",
            "resource": "/orgs/{IMS_ORG}/sandboxes/*",
            "condition": "{\"or\":[{\"adobe.match_any_labels_by_prefix\":[{\"var\":\"subject.roles.labels\"},\"core/\",{\"var\":\"resource.labels\"}]},{\"!\":[{\"adobe.match_all_labels_by_prefix\":[{\"var\":\"subject.roles.labels\"},\"core/\",{\"var\":\"resource.labels\"}]}]}]}",
            "actions": [
                "read"
            ]
        }
    ],
    "_etag": null
}
```

## 刪除策略 {#delete}

要刪除策略，請向 `/policies` 提供要刪除的策略的ID時的終結點。

**API格式**

```http
DELETE /policies/{POLICY_ID}
```

| 參數 | 說明 |
| --- | --- |
| {POLICY_ID} | 要刪除的策略的ID。 |

**要求**

以下請求刪除ID為 `c3863937-5d40-448d-a7be-416e538f955e`。

```shell
curl -X DELETE \
  https://platform.adobe.io/data/foundation/access-control/administration/policies/c3863937-5d40-448d-a7be-416e538f955e \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
```

**回應**

成功的響應返回HTTP狀態204（無內容）和空白正文。

您可以通過嘗試對策略進行查找(GET)請求來確認刪除。 您將收到HTTP狀態404（未找到），因為已從管理中刪除了該策略。
