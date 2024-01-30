---
keywords: Experience Platform；首頁；熱門主題；API；屬性型存取控制；屬性型存取控制
solution: Experience Platform
title: 角色API端點
description: 屬性式存取控制API中的/roles端點可讓您以程式設計方式管理Adobe Experience Platform中的角色。
exl-id: 049f7a18-7d06-437b-8ce9-25d7090ba782
source-git-commit: 01574f37593c707f092a8b4aa03d3d67e8c20780
workflow-type: tm+mt
source-wordcount: '1665'
ht-degree: 4%

---

# 角色端點

>[!NOTE]
>
>如果傳遞的是使用者權杖，則權杖的使用者必須具有請求組織的「組織管理員」角色。

角色定義管理員、專家或一般使用者對貴組織資源的存取權。 在基於角色的存取控制環境中，使用者存取布建是透過共同責任和需求進行分組。 一個角色具有一組給定的權限，您的組織成員可以指派到一個或多個角色，依據他們需要的視圖範圍或寫入權限而定。

此 `/roles` 以屬性為基礎的存取控制API中的端點可讓您以程式設計方式管理組織中的角色。

## 快速入門

本指南中使用的API端點屬於屬性型存取控制API的一部分。 在繼續之前，請檢閱 [快速入門手冊](./getting-started.md) 如需相關檔案的連結，請參閱本檔案範例API呼叫的指南，以及有關成功呼叫任何Experience PlatformAPI所需標題的重要資訊。

## 擷取角色清單 {#list}

您可以透過向以下人員發出GET請求，列出屬於您組織的所有現有角色： `/roles` 端點。

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

成功的回應會傳回組織中的角色清單，包括有關其各自角色型別、許可權集和主體屬性的資訊。

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
| `id` | 與角色相對應的ID。 此ID是自動產生的。 |
| `name` | 您角色的名稱。 |
| `description` | description屬性提供角色的額外資訊。 |
| `roleType` | 角色的指定型別。 角色型別的可能值包括： `user-defined` 和 `system-defined`. |
| `permissionSets` | 許可權集代表管理員可套用至角色的一組許可權。 管理員可以將許可權集指派給角色，而不是指派個別許可權。 這可讓您從包含一組許可權的預定義角色建立自訂角色。 |
| `sandboxes` | 此屬性會顯示貴組織內為特定角色布建的沙箱。 |
| `subjectAttributes` | 指出主旨與其可存取之平台資源之間關聯的屬性。 |
| `subjectAttributes.labels` | 顯示套用至查詢角色的資料使用標籤。 |

## 查詢角色 {#lookup}

您可以透過提出包含對應角色的GET請求來查詢個別角色 `roleId` 在請求路徑中。

**API格式**

```http
GET /roles/{ROLE_ID}
```

| 參數 | 說明 |
| --- | --- |
| {ROLE_ID} | 您要查閱的角色的ID。 |

**要求**

以下請求會擷取以下專案的資訊： `{ROLE_ID}`.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/access-control/administration/roles/3dfa045d-de58-4dfd-8ea9-e4e2c1b6d809 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
```

**回應**

成功的回應會傳回查詢角色ID的詳細資料，包括其角色型別、許可權集和主體屬性的資訊。

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
| `id` | 與角色相對應的ID。 此ID是自動產生的。 |
| `name` | 您角色的名稱。 |
| `description` | description屬性提供角色的額外資訊。 |
| `roleType` | 角色的指定型別。 角色型別的可能值包括： `user-defined` 和 `system-defined`. |
| `permissionSets` | 許可權集代表管理員可套用至角色的一組許可權。 管理員可以將許可權集指派給角色，而不是指派個別許可權。 這可讓您從包含一組許可權的預定義角色建立自訂角色。 |
| `sandboxes` | 此屬性會顯示貴組織內為特定角色布建的沙箱。 |
| `subjectAttributes` | 指出主旨與其可存取之平台資源之間關聯的屬性。 |
| `subjectAttributes.labels` | 顯示套用至查詢角色的資料使用標籤。 |

## 依角色ID查詢主題

您也可以向以下網站發出GET要求來擷取主題： `/roles` 端點並提供 {ROLE_ID}.

**API格式**

```http
GET /roles/{ROLE_ID}/subjects
```

| 參數 | 說明 |
| --- | --- |
| {ROLE_ID} | 與您要查閱的主體相關聯之角色的ID。 |

**要求**

以下請求會擷取與關聯的主體 `3dfa045d-de58-4dfd-8ea9-e4e2c1b6d809`.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/access-control/administration/roles/3dfa045d-de58-4dfd-8ea9-e4e2c1b6d809/subjects \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
```

**回應**

成功回應會傳回與查詢的角色ID相關聯的主題，包括對應的主題ID和主題型別。

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
| `roleId` | 與查詢主體相關聯的角色ID。 |
| `subjectType` | 查詢的主旨型別。 |
| `subjectId` | 與查詢主體相對應的ID。 |

## 建立角色 {#create}

POST若要建立新角色，請向 `/roles` 端點，同時提供角色名稱、說明和角色型別的值。

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
| `name` | 您角色的名稱。 確保您角色的名稱是描述性的，因為您可以使用此名稱來查閱有關您角色的資訊。 |
| `description` | （選擇性）您可納入的描述性值，以提供角色的相關詳細資訊。 |
| `roleType` | 角色的指定型別。 角色型別的可能值包括： `user-defined` 和 `system-defined`. |

**回應**

成功的回應會傳回您新建立的角色，以及其對應的角色ID，以及其角色型別、許可權集和主體屬性的資訊。

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
| `id` | 與角色相對應的ID。 此ID是自動產生的。 |
| `name` | 您角色的名稱。 |
| `description` | description屬性提供角色的額外資訊。 |
| `roleType` | 角色的指定型別。 角色型別的可能值包括： `user-defined` 和 `system-defined`. |
| `permissionSets` | 許可權集代表管理員可套用至角色的一組許可權。 管理員可以將許可權集指派給角色，而不是指派個別許可權。 這可讓您從包含一組許可權的預定義角色建立自訂角色。 |
| `sandboxes` | 此屬性會顯示貴組織內為特定角色布建的沙箱。 |
| `subjectAttributes` | 指出主旨與其可存取之平台資源之間關聯的屬性。 |
| `subjectAttributes.labels` | 顯示套用至查詢角色的資料使用標籤。 |

## 更新角色 {#patch}

您可以透過向以下專案發出PATCH請求來更新角色的屬性： `/roles` 端點，並為您要套用的作業提供對應的角色ID和值。

**API格式**

```http
PATCH /roles/{ROLE_ID}
```

| 參數 | 說明 |
| --- | --- |
| {ROLE_ID} | 您要更新之角色的ID。 |

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
| `op` | 用於定義更新角色所需動作的操作呼叫。 操作包括： `add`， `replace`、和 `remove`. |
| `path` | 要更新之引數的路徑。 |
| `value` | 您想要用來更新引數的新值。 |

**回應**

成功的回應會傳回更新的角色，包括您選擇更新的屬性的新值。

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
| `id` | 與角色相對應的ID。 此ID是自動產生的。 |
| `name` | 您角色的名稱。 |
| `description` | description屬性提供角色的額外資訊。 |
| `roleType` | 角色的指定型別。 角色型別的可能值包括： `user-defined` 和 `system-defined`. |
| `permissionSets` | 許可權集代表管理員可套用至角色的一組許可權。 管理員可以將許可權集指派給角色，而不是指派個別許可權。 這可讓您從包含一組許可權的預定義角色建立自訂角色。 |
| `sandboxes` | 此屬性會顯示貴組織內為特定角色布建的沙箱。 |
| `subjectAttributes` | 指出主旨與其可存取之平台資源之間關聯的屬性。 |
| `subjectAttributes.labels` | 顯示套用至查詢角色的資料使用標籤。 |

## 依角色ID更新角色 {#put}

您可以透過向以下專案發出PUT請求來更新角色： `/roles` 端點，並指定與您要更新的角色對應的角色ID。

**API格式**

```http
PUT /roles/{ROLE_ID}
```

**要求**

以下請求會更新角色ID的名稱、說明和角色型別： `3dfa045d-de58-4dfd-8ea9-e4e2c1b6d809`.

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
| `roleType` | 角色的指定型別。 角色型別的可能值包括： `user-defined` 和 `system-defined`. |

**回應**

成功的回應會傳回您更新的角色，包括其名稱、說明和角色型別的新值。

```json
{
  "id": "3dfa045d-de58-4dfd-8ea9-e4e2c1b6d809",
  "name": "Administrator role for ACME",
  "description": "New administrator role for ACME",
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
| `id` | 與角色相對應的ID。 此ID是自動產生的。 |
| `name` | 您角色的名稱。 |
| `description` | description屬性提供角色的額外資訊。 |
| `roleType` | 角色的指定型別。 角色型別的可能值包括： `user-defined` 和 `system-defined`. |
| `permissionSets` | 許可權集代表管理員可套用至角色的一組許可權。 管理員可以將許可權集指派給角色，而不是指派個別許可權。 這可讓您從包含一組許可權的預定義角色建立自訂角色。 |
| `sandboxes` | 此屬性會顯示貴組織內為特定角色布建的沙箱。 |
| `subjectAttributes` | 指出主旨與其可存取之平台資源之間關聯的屬性。 |
| `subjectAttributes.labels` | 顯示套用至查詢角色的資料使用標籤。 |

## 依角色ID更新主旨

PATCH若要更新與角色相關聯的主體，請向 `/roles` 端點，同時提供您要更新之主體的角色ID。

**API格式**

```http
PATCH /roles/{ROLE_ID}/subjects
```

| 參數 | 說明 |
| --- | --- |
| {ROLE_ID} | 與您要更新之主體相關聯之角色的ID。 |

**要求**

以下要求會更新與關聯的主題 `{ROLE_ID}`.

```shell
curl --location --request PATCH 'https://platform.adobe.io/data/foundation/access-control/administration/roles/<ROLE_ID>/subjects' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {IMS_ORG}' \
--header 'Content-Type: application/json' \
--data-raw '[
    {
        "op": "add",
        "path": "/user",
        "value": "{USER ID}"
    }
]' 
```

| 運作 | 說明 |
| --- | --- |
| `op` | 用於定義更新角色所需動作的操作呼叫。 操作包括： `add`， `replace`、和 `remove`. |
| `path` | 要更新之引數的路徑。 |
| `value` | 您想要用來更新引數的新值。 |

**回應**

成功的回應會傳回您更新的角色，包括主題的新值。

```json
{
  "subjects": [
    [
      {
        "subjectId": "03Z07HFQCCUF3TUHAX274206@AdobeID",
        "subjectType": "user"
      }
    ]
  ],
  "_page": {
    "limit": 1,
    "count": 1
  },
  "_links": {
    "self": {
      "href": "https://platform.adobe.io:443/data/foundation/access-control/administration/roles/{ROLE_ID}/subjects",
      "templated": true
    },
    "page": {
      "href": "https://platform.adobe.io:443/data/foundation/access-control/administration/roles/{ROLE_ID}/subjects?limit={limit}&start={start}&orderBy={orderBy}&property={property}",
      "templated": true
    }
  }
}
```

## 刪除角色 {#delete}

DELETE若要刪除角色，請向 `/roles` 端點，並指定您要刪除的角色的ID。

**API格式**

```http
DELETE /roles/{ROLE_ID}
```

| 參數 | 說明 |
| --- | --- |
| {ROLE_ID} | 您要刪除之角色的ID。 |

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

成功的回應會傳回HTTP狀態204 （無內容）和空白內文。

您可以嘗試向角色查詢(GET)請求以確認刪除。 您會收到HTTP狀態404 （找不到），因為角色已從管理中移除。

## 新增API認證 {#apicredential}

若要新增API認證，請發出PATCH請求至 `/roles` 端點並提供主體的角色ID。

**API格式**

```shell
curl --location --request PATCH 'https://platform.adobe.io/data/foundation/access-control/administration/roles/<ROLE_ID>/subjects' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {IMS_ORG}' \
--header 'Content-Type: application/json' \
--data-raw '[
    {
        "op": "add",
        "path": "/api-integration",
        "value": "{TECHNICAL ACCOUNT ID}"
    }
]'   
```

| 運作 | 說明 |
| --- | --- |
| `op` | 用於定義更新角色所需動作的操作呼叫。 操作包括： `add`， `replace`、和 `remove`. |
| `path` | 要新增的引數的路徑。 |
| `value` | 您想要用來新增引數的值。 |

**回應**

成功的回應會傳回HTTP狀態204 （無內容）和空白內文。
