---
keywords: Experience Platform；首頁；熱門主題；API；屬性型存取控制；屬性型存取控制
solution: Experience Platform
title: 角色API端點
description: 屬性型存取控制API中的/roles端點可讓您以程式設計方式管理Adobe Experience Platform中的角色。
exl-id: 049f7a18-7d06-437b-8ce9-25d7090ba782
source-git-commit: 16d85a2a4ee8967fc701a3fe631c9daaba9c9d70
workflow-type: tm+mt
source-wordcount: '1606'
ht-degree: 3%

---

# 角色端點

>[!NOTE]
>
>如果傳遞了使用者Token，則Token的使用者必須對請求的組織具有「組織管理員」角色。

角色定義管理員、專家或一般使用者對您組織中資源的存取權。 在基於角色的訪問控制環境中，用戶訪問配置是通過共同的責任和需求進行分組的。 角色具有一組指定的權限，而您組織的成員可以根據其所需的檢視或寫入存取範圍，指派給一或多個角色。

此 `/roles` 屬性型存取控制API中的端點可讓您以程式設計方式管理組織中的角色。

## 快速入門

本指南中使用的API端點是屬性型存取控制API的一部分。 繼續之前，請檢閱 [快速入門手冊](./getting-started.md) 如需相關檔案的連結，請參閱本檔案中讀取範例API呼叫的指南，以及成功呼叫任何Experience PlatformAPI所需的必要標頭重要資訊。

## 檢索角色清單 {#list}

您可以向以下對象提出GET請求，以列出屬於您組織的所有現有角色： `/roles` 端點。

**API格式**

```http
GET /roles/
```

**要求**

下列請求會擷取屬於您組織的角色清單。

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/access-control/administration/roles \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
```

**回應**

成功的回應會傳回組織中的角色清單，包括其各自角色類型、權限集和主體屬性的相關資訊。

```json
{
  "roles": [
    {
      "id": "3dfa045d-de58-4dfd-8ea9-e4e2c1b6d809",
      "name": "Administrator Role",
      "description": "Role for administrator type of responsibilities and access",
      "roleType": "user-defined",
      "permissionSets": [
        "manage-datasets",
        "manage-schemas"
      ],
      "sandboxes": [
        "prod"
      ],
      "subjectAttributes": {
        "labels": [
          "core/S1"
        ]
      },
      "createdBy": "{CREATED_BY}",
      "createdAt": 1648153201825,
      "modifiedBy": "{MODIFIED_BY}",
      "modifiedAt": 1648153201825,
      "etag": null
    }
  ],
  "_page": {
    "limit": 1,
    "count": 1
  },
  "_links": {
    "next": {
      "href": "https://platform.adobe.io:443/data/foundation/access-control/administration/roles/3dfa045d-de58-4dfd-8ea9-e4e2c1b6d809",
      "templated": true
    },
    "page": {
      "href": "https://platform.adobe.io:443/data/foundation/access-control/administration/roles/3dfa045d-de58-4dfd-8ea9-e4e2c1b6d809",
      "templated": true
    },
    "subjects": {
      "href": "https://platform.adobe.io:443/data/foundation/access-control/administration/roles/3dfa045d-de58-4dfd-8ea9-e4e2c1b6d809",
      "templated": true
    }
  }
}
```

| 屬性 | 說明 |
| --- | --- |
| `id` | 與角色對應的ID。 此ID會自動產生。 |
| `name` | 角色的名稱。 |
| `description` | 說明屬性提供您角色的其他資訊。 |
| `roleType` | 角色的指定類型。 角色類型的可能值為： `user-defined` 和 `system-defined`. |
| `permissionSets` | 權限集表示管理員可以應用到角色的一組權限。 管理員可以將權限集指派給角色，而不是指派個別權限。 這可讓您從包含一組權限的預先定義角色中建立自訂角色。 |
| `sandboxes` | 此屬性會顯示您組織內針對特定角色布建的沙箱。 |
| `subjectAttributes` | 指出主體與其有權存取的平台資源之間關聯的屬性。 |
| `subjectAttributes.labels` | 顯示套用至查詢角色的資料使用量標籤。 |

## 查找角色 {#lookup}

您可以提出包含對應之 `roleId` 在請求路徑中。

**API格式**

```http
GET /roles/{ROLE_ID}
```

| 參數 | 說明 |
| --- | --- |
| {ROLE_ID} | 您要查詢的角色ID。 |

**要求**

下列請求會擷取 `{ROLE_ID}`.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/access-control/administration/roles/3dfa045d-de58-4dfd-8ea9-e4e2c1b6d809 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
```

**回應**

成功的回應會傳回查詢之角色ID的詳細資訊，包括其角色類型、權限集和主體屬性的相關資訊。

```json
{
  "id": "3dfa045d-de58-4dfd-8ea9-e4e2c1b6d809",
  "name": "Administrator Role",
  "description": "Role for administrator type of responsibilities and access",
  "roleType": "user-defined",
  "permissionSets": [
    "manage-datasets",
    "manage-schemas"
  ],
  "sandboxes": [
    "prod"
  ],
  "subjectAttributes": {
    "labels": [
      "core/S1"
    ]
  },
  "createdBy": "{CREATED_BY}",
  "createdAt": 1648153201825,
  "modifiedBy": "{MODIFIED_BY}",
  "modifiedAt": 1648153201825,
  "etag": null
}
```

| 屬性 | 說明 |
| --- | --- |
| `id` | 與角色對應的ID。 此ID會自動產生。 |
| `name` | 角色的名稱。 |
| `description` | 說明屬性提供您角色的其他資訊。 |
| `roleType` | 角色的指定類型。 角色類型的可能值為： `user-defined` 和 `system-defined`. |
| `permissionSets` | 權限集表示管理員可以應用到角色的一組權限。 管理員可以將權限集指派給角色，而不是指派個別權限。 這可讓您從包含一組權限的預先定義角色中建立自訂角色。 |
| `sandboxes` | 此屬性會顯示您組織內針對特定角色布建的沙箱。 |
| `subjectAttributes` | 指出主體與其有權存取的平台資源之間關聯的屬性。 |
| `subjectAttributes.labels` | 顯示套用至查詢角色的資料使用量標籤。 |

## 按角色ID查找主題

您也可以向 `/roles` 提供{ROLE_ID}時的端點。

**API格式**

```http
GET /roles/{ROLE_ID}/subjects
```

| 參數 | 說明 |
| --- | --- |
| {ROLE_ID} | 與您要查詢的主題相關聯的角色ID。 |

**要求**

以下請求會擷取與 `3dfa045d-de58-4dfd-8ea9-e4e2c1b6d809`.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/access-control/administration/roles/3dfa045d-de58-4dfd-8ea9-e4e2c1b6d809/subjects \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
```

**回應**

成功的回應會傳回與查詢的角色ID相關聯的主體，包括對應的主體ID和主體類型。

```json
{
  "items": [
      {
          "roleId": "3dfa045d-de58-4dfd-8ea9-e4e2c1b6d809",
          "subjectType": "user",
          "subjectId": "03Z07HFQCCUF3TUHAX274206@AdobeID"
      },
      {
          "roleId": "3dfa045d-de58-4dfd-8ea9-e4e2c1b6d809",
          "subjectType": "user",
          "subjectId": "PIRJ7WE5T3QT9Z4TCLVH86DE@AdobeID"
      },
      {
          "roleId": "3dfa045d-de58-4dfd-8ea9-e4e2c1b6d809",
          "subjectType": "user",
          "subjectId": "WHPWE00MC26SHZ7AKBFG403D@AdobeID"
      },
  ]
  "_page": {
    "limit": 0,
    "count": 0
  },
  "_links": {
      "self": {
          "href": "/roles/{ROLE_ID}/subjects",
          "templated": false,
          "type": null,
          "method": null
      },
      "page": {
          "href": "/roles/{ROLE_ID}/subjects?limit={limit}&start={start}&orderBy={orderBy}&property={property}",
          "templated": true,
          "type": null,
          "method": null
      }
  }
}
```

| 屬性 | 說明 |
| --- | --- |
| `roleId` | 與查詢的主體相關聯的角色ID。 |
| `subjectType` | 查詢主題的類型。 |
| `subjectId` | 與查詢的主題對應的ID。 |

## 建立角色 {#create}

若要建立新角色，請向 `/roles` 端點，同時提供角色名稱、說明和角色類型的值。

**API格式**

```http
POST /roles/
```

**要求**

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/access-control/administration/roles \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}'
  -d'{
    "name": "Administrator Role",
    "description": "Role for administrator type of responsibilities and access",
    "roleType": "user-defined"
  }'
```

| 屬性 | 說明 |
| --- | --- |
| `name` | 角色的名稱。 請確定角色的名稱是描述性的，因為您可以使用此名稱來查詢角色的相關資訊。 |
| `description` | （選用）可包含的描述性值，可提供角色的詳細資訊。 |
| `roleType` | 角色的指定類型。 角色類型的可能值為： `user-defined` 和 `system-defined`. |

**回應**

成功的回應會傳回您新建立的角色、其對應的角色ID，以及其角色類型、權限集和主體屬性的相關資訊。

```json
{
  "id": "3dfa045d-de58-4dfd-8ea9-e4e2c1b6d809",
  "name": "Administrator Role",
  "description": "Role for administrator type of responsibilities and access",
  "roleType": "user-defined",
  "permissionSets": [
    "manage-datasets",
    "manage-schemas"
  ],
  "sandboxes": [
    "prod"
  ],
  "subjectAttributes": {
    "labels": [
      "core/S1"
    ]
  },
  "createdBy": "{CREATED_BY}",
  "createdAt": 1648153201825,
  "modifiedBy": "{MODIFIED_BY}",
  "modifiedAt": 1648153201825,
  "etag": null
}
```

| 屬性 | 說明 |
| --- | --- |
| `id` | 與角色對應的ID。 此ID會自動產生。 |
| `name` | 角色的名稱。 |
| `description` | 說明屬性提供您角色的其他資訊。 |
| `roleType` | 角色的指定類型。 角色類型的可能值為： `user-defined` 和 `system-defined`. |
| `permissionSets` | 權限集表示管理員可以應用到角色的一組權限。 管理員可以將權限集指派給角色，而不是指派個別權限。 這可讓您從包含一組權限的預先定義角色中建立自訂角色。 |
| `sandboxes` | 此屬性會顯示您組織內針對特定角色布建的沙箱。 |
| `subjectAttributes` | 指出主體與其有權存取的平台資源之間關聯的屬性。 |
| `subjectAttributes.labels` | 顯示套用至查詢角色的資料使用量標籤。 |

## 更新角色 {#patch}

您可以向 `/roles` 端點，同時為您要套用的操作提供對應的角色ID和值。

**API格式**

```http
PATCH /roles/{ROLE_ID}
```

| 參數 | 說明 |
| --- | --- |
| {ROLE_ID} | 要更新的角色ID。 |

**要求**

```shell
curl -X PATCH \
  https://platform.adobe.io/data/foundation/access-control/administration/roles/{ROLE_ID} \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}'
  -d'{
    "operations": [
      {
        "op": "add",
        "path": "/description",
        "value": "Role with permission sets for admin type of access"
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

成功的回應會傳回更新的角色，包括您所選要更新之屬性的新值。

```json
{
  "id": "3dfa045d-de58-4dfd-8ea9-e4e2c1b6d809",
  "name": "Administrator Role",
  "description": "Role with permission sets for admin type of access",
  "roleType": "user-defined",
  "permissionSets": [
    "manage-datasets",
    "manage-schemas"
  ],
  "sandboxes": [
    "prod"
  ],
  "subjectAttributes": {
    "labels": [
      "core/S1"
    ]
  },
  "createdBy": "{CREATED_BY}",
  "createdAt": 1648153201825,
  "modifiedBy": "{MODIFIED_BY}",
  "modifiedAt": 1648153201825,
  "etag": null
}
```

| 屬性 | 說明 |
| --- | --- |
| `id` | 與角色對應的ID。 此ID會自動產生。 |
| `name` | 角色的名稱。 |
| `description` | 說明屬性提供您角色的其他資訊。 |
| `roleType` | 角色的指定類型。 角色類型的可能值為： `user-defined` 和 `system-defined`. |
| `permissionSets` | 權限集表示管理員可以應用到角色的一組權限。 管理員可以將權限集指派給角色，而不是指派個別權限。 這可讓您從包含一組權限的預先定義角色中建立自訂角色。 |
| `sandboxes` | 此屬性會顯示您組織內針對特定角色布建的沙箱。 |
| `subjectAttributes` | 指出主體與其有權存取的平台資源之間關聯的屬性。 |
| `subjectAttributes.labels` | 顯示套用至查詢角色的資料使用量標籤。 |

## 按角色ID更新角色 {#put}

您可以透過向 `/roles` 端點，並指定與要更新的角色對應的角色ID。

**API格式**

```http
PUT /roles/{ROLE_ID}
```

**要求**

以下請求會更新角色ID的名稱、說明和角色類型： `3dfa045d-de58-4dfd-8ea9-e4e2c1b6d809`.

```shell
curl -X PUT \
  https://platform.adobe.io/data/foundation/access-control/administration/roles/3dfa045d-de58-4dfd-8ea9-e4e2c1b6d809 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}'
  -d'{
    "name": "Administrator role for ACME",
    "description": "New administrator role for ACME",
    "roleType": "user-defined"
  }'
```

| 參數 | 說明 |
| --- | --- |
| `name` | 角色的更新名稱。 |
| `description` | 角色的更新說明。 |
| `roleType` | 角色的指定類型。 角色類型的可能值為： `user-defined` 和 `system-defined`. |

**回應**

成功會傳回您更新的角色，包括名稱、說明和角色類型的新值。

```json
{
  "id": "3dfa045d-de58-4dfd-8ea9-e4e2c1b6d809",
  "name": "Administrator Role",
  "description": "Role with permission sets for admin type of access",
  "roleType": "user-defined",
  "permissionSets": [
    "manage-datasets",
    "manage-schemas"
  ],
  "sandboxes": [
    "prod"
  ],
  "subjectAttributes": {
    "labels": [
      "core/S1"
    ]
  },
  "createdBy": "{CREATED_BY}",
  "createdAt": 1648153201825,
  "modifiedBy": "{MODIFIED_BY}",
  "modifiedAt": 1648153201825,
  "etag": null
}
```

| 屬性 | 說明 |
| --- | --- |
| `id` | 與角色對應的ID。 此ID會自動產生。 |
| `name` | 角色的名稱。 |
| `description` | 說明屬性提供您角色的其他資訊。 |
| `roleType` | 角色的指定類型。 角色類型的可能值為： `user-defined` 和 `system-defined`. |
| `permissionSets` | 權限集表示管理員可以應用到角色的一組權限。 管理員可以將權限集指派給角色，而不是指派個別權限。 這可讓您從包含一組權限的預先定義角色中建立自訂角色。 |
| `sandboxes` | 此屬性會顯示您組織內針對特定角色布建的沙箱。 |
| `subjectAttributes` | 指出主體與其有權存取的平台資源之間關聯的屬性。 |
| `subjectAttributes.labels` | 顯示套用至查詢角色的資料使用量標籤。 |

## 按角色ID更新主體

若要更新與角色相關聯的主體，請向 `/roles` 端點，同時提供您要更新之主體的角色ID。

**API格式**

```http
PATCH /roles/{ROLE_ID}
```

| 參數 | 說明 |
| --- | --- |
| {ROLE_ID} | 與您要更新的主題相關聯的角色ID。 |

**要求**

下列請求會更新與 `{ROLE_ID}`.

```shell
curl -X PATCH \
  https://platform.adobe.io/data/foundation/access-control/administration/roles/{ROLE_ID} \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}'
  -d'{
    "operations": [
      {
        "op": "add",
        "path": "/subjects",
        "value": "New subjects"
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

成功的回應會傳回與查詢的角色ID相關聯的更新主體。

```json
{
  "subjects": [
    {
      "subjectId": "string",
      "subjectType": "user"
    }
  ],
  "_page": {
    "limit": 0,
    "count": 0
  },
  "_links": {
    "next": {
      "href": "string",
      "templated": true
    },
    "page": {
      "href": "string",
      "templated": true
    }
  }
}
```

| 屬性 | 說明 |
| --- | --- |
| `subjectId` | 主題的ID。 |
| `subjectType` | 主題的類型。 |

## 刪除角色 {#delete}

若要刪除角色，請向 `/roles` 端點，同時指定您要刪除之角色的ID。

**API格式**

```http
DELETE /roles/{ROLE_ID}
```

| 參數 | 說明 |
| --- | --- |
| {ROLE_ID} | 要刪除的角色的ID。 |

**要求**

以下請求會刪除ID為的角色 `{ROLE_ID}`.

```shell
curl -X DELETE \
  https://platform.adobe.io/data/foundation/access-control/administration/roles/{ROLE_ID} \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
```

**回應**

成功的回應會傳回HTTP狀態204（無內容）和空白內文。

您可以嘗試對角色進行查詢(GET)以確認刪除。 您會收到HTTP狀態404（找不到），因為該角色已從管理中移除。
