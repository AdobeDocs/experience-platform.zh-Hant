---
keywords: Experience Platform；首頁；熱門主題；API；屬性型存取控制；屬性型存取控制
solution: Experience Platform
title: 存取控制原則API端點
description: 屬性型存取控制API中的/policys端點可讓您以程式設計方式管理Adobe Experience Platform中的原則。
exl-id: 07690f43-fdd9-4254-9324-84e6bd226743
source-git-commit: 38447348bc96b2f3f330ca363369eb423efea1c8
workflow-type: tm+mt
source-wordcount: '1412'
ht-degree: 2%

---

# 訪問控制策略終結點

訪問控制策略是將屬性集合在一起以建立允許和不允許的操作的語句。 這些策略可以是本地策略或全局策略，也可以覆蓋其他策略。 此 `/policies` 屬性型存取控制API中的端點可讓您以程式設計方式管理原則，包括規範原則的規則及其各自主旨條件的相關資訊。

>[!IMPORTANT]
>
>此端點不應與 `/policies` 端點 [策略服務API](../../../data-governance/api/policies.md)，用於管理資料使用原則。

## 快速入門

本指南中使用的API端點是屬性型存取控制API的一部分。 繼續之前，請檢閱 [快速入門手冊](./getting-started.md) 如需相關檔案的連結，請參閱本檔案中讀取範例API呼叫的指南，以及成功呼叫任何Experience PlatformAPI所需的必要標頭重要資訊。

## 檢索策略清單 {#list}

向發出GET要求 `/policies` 端點，列出貴組織中的所有現有原則。

**API格式**

```http
GET /policies
```

**要求**

下列請求會擷取現有原則的清單。

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/access-control/administration/policies \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
```

**回應**

成功的回應會傳回現有原則的清單。

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
| `createdAt` | 建立策略的時間。 此 `createdAt` 屬性會以unix epoch時間戳記顯示。 |
| `modifiedBy` | 上次更新策略的用戶的ID。 |
| `modifiedAt` | 上次更新策略的時間。 此 `modifiedAt` 屬性會以unix epoch時間戳記顯示。 |
| `name` | 策略的名稱。 |
| `description` | （可選）可添加的屬性，以提供有關特定策略的進一步資訊。 |
| `status` | 策略的當前狀態。 此屬性定義策略當前是否為 `active` 或 `inactive`. |
| `subjectCondition` | 適用於主體的條件。 主體是具有特定屬性的使用者，請求存取資源以執行動作。 在這種情況下， `subjectCondition` 是套用至主旨屬性的類似查詢條件。 |
| `rules` | 定義策略的規則集。 規則會定義已授權的屬性組合，以便主體成功對資源執行動作。 |
| `rules.effect` | 考慮 `action`, `condition` 和 `resource`. 可能的值包括： `permit`, `deny`，或 `indeterminate`. |
| `rules.resource` | 主體可以或無法存取的資產或物件。  資源可以是檔案、應用程式、伺服器或甚至API。 |
| `rules.condition` | 套用至資源的條件。 例如，如果資源是架構，則架構可以套用特定標籤，以判斷針對該架構的動作是否允許或不允許。 |
| `rules.action` | 允許主體對查詢的資源執行的操作。 可能的值包括： `read`, `create`, `edit`，和 `delete`. |

## 按ID查找策略詳細資訊 {#lookup}

向發出GET要求 `/policies` 端點，同時在請求路徑中提供策略ID以檢索有關該單個策略的資訊。

**API格式**

```http
GET /policies/{POLICY_ID}
```

| 參數 | 說明 |
| --- | --- |
| {POLICY_ID} | 要檢索的策略的ID。 |

**要求**

以下請求將檢索有關單個策略的資訊。

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
| `createdAt` | 建立策略的時間。 此 `createdAt` 屬性會以unix epoch時間戳記顯示。 |
| `modifiedBy` | 上次更新策略的用戶的ID。 |
| `modifiedAt` | 上次更新策略的時間。 此 `modifiedAt` 屬性會以unix epoch時間戳記顯示。 |
| `name` | 策略的名稱。 |
| `description` | （可選）可添加的屬性，以提供有關特定策略的進一步資訊。 |
| `status` | 策略的當前狀態。 此屬性定義策略當前是否為 `active` 或 `inactive`. |
| `subjectCondition` | 適用於主體的條件。 主體是具有特定屬性的使用者，請求存取資源以執行動作。 在這種情況下， `subjectCondition` 是套用至主旨屬性的類似查詢條件。 |
| `rules` | 定義策略的規則集。 規則會定義已授權的屬性組合，以便主體成功對資源執行動作。 |
| `rules.effect` | 考慮 `action`, `condition` 和 `resource`. 可能的值包括： `permit`, `deny`，或 `indeterminate`. |
| `rules.resource` | 主體可以或無法存取的資產或物件。  資源可以是檔案、應用程式、伺服器或甚至API。 |
| `rules.condition` | 套用至資源的條件。 例如，如果資源是架構，則架構可以套用特定標籤，以判斷針對該架構的動作是否允許或不允許。 |
| `rules.action` | 允許主體對查詢的資源執行的操作。 可能的值包括： `read`, `create`, `edit`，和 `delete`. |


## 建立原則 {#create}

若要建立新原則，請向 `/policies` 端點。

**API格式**

```http
POST /policies
```

**要求**

以下請求將建立一個名為的新策略： `acme-integration-policy`.

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
| `description` | （可選）可添加的屬性，以提供有關特定策略的進一步資訊。 |
| `imsOrgId` | 包含策略的組織。 |
| `rules` | 定義策略的規則集。 規則會定義已授權的屬性組合，以便主體成功對資源執行動作。 |
| `rules.effect` | 考慮 `action`, `condition` 和 `resource`. 可能的值包括： `permit`, `deny`，或 `indeterminate`. |
| `rules.resource` | 主體可以或無法存取的資產或物件。  資源可以是檔案、應用程式、伺服器或甚至API。 |
| `rules.condition` | 套用至資源的條件。 例如，如果資源是架構，則架構可以套用特定標籤，以判斷針對該架構的動作是否允許或不允許。 |
| `rules.action` | 允許主體對查詢的資源執行的操作。 可能的值包括： `read`, `create`, `edit`，和 `delete`. |

**回應**

成功的請求返回新建立的策略，包括其唯一策略ID和相關規則。

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
| `rules` | 定義策略的規則集。 規則會定義已授權的屬性組合，以便主體成功對資源執行動作。 |
| `rules.effect` | 考慮 `action`, `condition` 和 `resource`. 可能的值包括： `permit`, `deny`，或 `indeterminate`. |
| `rules.resource` | 主體可以或無法存取的資產或物件。  資源可以是檔案、應用程式、伺服器或甚至API。 |
| `rules.condition` | 套用至資源的條件。 例如，如果資源是架構，則架構可以套用特定標籤，以判斷針對該架構的動作是否允許或不允許。 |
| `rules.action` | 允許主體對查詢的資源執行的操作。 可能的值包括： `read`, `create`, `edit`，和 `delete`. |


## 按策略ID更新策略 {#put}

若要更新個別政策的規則，請向 `/policies` 端點，同時在請求路徑中提供要更新的策略ID。

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

成功的響應返回更新的策略。

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

要更新單個策略的屬性，請向 `/policies` 端點，同時在請求路徑中提供要更新的策略ID。

**API格式**

```http
PATCH /policies/{POLICY_ID}
```

| 參數 | 說明 |
| --- | --- |
| {POLICY_ID} | 要更新的策略的ID。 |

**要求**

下列請求會取代 `/description` 在原則ID中 `c3863937-5d40-448d-a7be-416e538f955e`.

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
| `op` | 用於定義更新角色所需操作的操作調用。 操作包括： `add`, `replace`，和 `remove`. |
| `path` | 要更新的參數的路徑。 |
| `value` | 您要用更新參數的新值。 |

**回應**

成功的響應返回查詢的策略ID，其說明已更新。

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

若要刪除原則，請向 `/policies` 端點，同時提供要刪除的策略的ID。

**API格式**

```http
DELETE /policies/{POLICY_ID}
```

| 參數 | 說明 |
| --- | --- |
| {POLICY_ID} | 要刪除的策略的ID。 |

**要求**

以下請求將刪除ID為的策略 `c3863937-5d40-448d-a7be-416e538f955e`.

```shell
curl -X DELETE \
  https://platform.adobe.io/data/foundation/access-control/administration/policies/c3863937-5d40-448d-a7be-416e538f955e \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
```

**回應**

成功的回應會傳回HTTP狀態204（無內容）和空白內文。

您可以嘗試對原則進行查詢(GET)以確認刪除。 您會收到HTTP狀態404（找不到），因為已從管理中移除該原則。
