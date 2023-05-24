---
keywords: Experience Platform；首頁；熱門主題；api；基於屬性的訪問控制；基於屬性的訪問控制
solution: Experience Platform
title: 角色API終結點
description: 基於屬性的訪問控制API中的/roles終結點允許您以寫程式方式管理Adobe Experience Platform中的角色。
exl-id: 049f7a18-7d06-437b-8ce9-25d7090ba782
source-git-commit: 16d85a2a4ee8967fc701a3fe631c9daaba9c9d70
workflow-type: tm+mt
source-wordcount: '1606'
ht-degree: 5%

---

# 角色終結點

>[!NOTE]
>
>如果傳遞用戶令牌，則令牌的用戶必須對所請求的組織具有「組織管理員」角色。

角色定義管理員、專家或最終用戶對您組織中的資源的訪問權限。 在基於角色的訪問控制環境中，用戶訪問設定是通過共同的責任和需要進行分組的。 一個角色具有一組給定的權限，您的組織成員可以指派到一個或多個角色，依據他們需要的視圖範圍或寫入權限而定。

的 `/roles` 通過基於屬性的訪問控制API中的端點，可以以寫程式方式管理組織中的角色。

## 快速入門

本指南中使用的API終結點是基於屬性的訪問控制API的一部分。 在繼續之前，請查看 [入門指南](./getting-started.md) 有關相關文檔的連結、閱讀本文檔中示例API調用的指南，以及有關成功調用任何Experience PlatformAPI所需標頭的重要資訊。

## 檢索角色清單 {#list}

您可以通過向組織發出GET請求，列出屬於您組織的所有現有角色 `/roles` 端點。

**API格式**

```http
GET /roles/
```

**要求**

以下請求檢索屬於您組織的角色清單。

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/access-control/administration/roles \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
```

**回應**

成功的響應將返回組織中的角色清單，包括有關其各自的角色類型、權限集和主題屬性的資訊。

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
| `id` | 與角色對應的ID。 此ID是自動生成的。 |
| `name` | 角色的名稱。 |
| `description` | description屬性提供有關您角色的其他資訊。 |
| `roleType` | 角色的指定類型。 角色類型的可能值為： `user-defined` 和 `system-defined`。 |
| `permissionSets` | 權限集表示管理員可以應用於角色的一組權限。 管理員可以將權限集分配給角色，而不是分配單個權限。 這允許您從包含一組權限的預定義角色建立自定義角色。 |
| `sandboxes` | 此屬性顯示您組織內為特定角色設定的沙箱。 |
| `subjectAttributes` | 指示主題與他們有權訪問的平台資源之間的關聯的屬性。 |
| `subjectAttributes.labels` | 顯示應用於查詢角色的資料使用標籤。 |

## 查找角色 {#lookup}

您可以通過發出包含相應角色的GET請求來查找單個角色 `roleId` 的子菜單。

**API格式**

```http
GET /roles/{ROLE_ID}
```

| 參數 | 說明 |
| --- | --- |
| {ROLE_ID} | 要查找的角色的ID。 |

**要求**

以下請求檢索資訊 `{ROLE_ID}`。

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/access-control/administration/roles/3dfa045d-de58-4dfd-8ea9-e4e2c1b6d809 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
```

**回應**

成功的響應返回查詢的角色ID的詳細資訊，包括其角色類型、權限集和主題屬性的資訊。

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
| `id` | 與角色對應的ID。 此ID是自動生成的。 |
| `name` | 角色的名稱。 |
| `description` | description屬性提供有關您角色的其他資訊。 |
| `roleType` | 角色的指定類型。 角色類型的可能值為： `user-defined` 和 `system-defined`。 |
| `permissionSets` | 權限集表示管理員可以應用於角色的一組權限。 管理員可以將權限集分配給角色，而不是分配單個權限。 這允許您從包含一組權限的預定義角色建立自定義角色。 |
| `sandboxes` | 此屬性顯示您組織內為特定角色設定的沙箱。 |
| `subjectAttributes` | 指示主題與他們有權訪問的平台資源之間的關聯的屬性。 |
| `subjectAttributes.labels` | 顯示應用於查詢角色的資料使用標籤。 |

## 按角色ID查找主題

您還可以通過向 `/roles` 提供{ROLE_ID}時的終結點。

**API格式**

```http
GET /roles/{ROLE_ID}/subjects
```

| 參數 | 說明 |
| --- | --- |
| {ROLE_ID} | 與要查找的主體關聯的角色的ID。 |

**要求**

以下請求檢索與 `3dfa045d-de58-4dfd-8ea9-e4e2c1b6d809`。

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/access-control/administration/roles/3dfa045d-de58-4dfd-8ea9-e4e2c1b6d809/subjects \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
```

**回應**

成功的響應返回與查詢的角色ID相關聯的主題，包括相應的主題ID和主題類型。

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
| `roleId` | 與查詢主題關聯的角色ID。 |
| `subjectType` | 查詢主題的類型。 |
| `subjectId` | 與查詢主題對應的ID。 |

## 建立角色 {#create}

要建立新角色，請向 `/roles` 終結點，同時為角色的名稱、說明和角色類型提供值。

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
| `name` | 角色的名稱。 確保角色的名稱是描述性的，因為您可以使用此名稱查找有關角色的資訊。 |
| `description` | （可選）可包括的說明性值，以提供有關職責的詳細資訊。 |
| `roleType` | 角色的指定類型。 角色類型的可能值為： `user-defined` 和 `system-defined`。 |

**回應**

成功的響應將返回您新建立的角色及其相應的角色ID，以及有關其角色類型、權限集和主題屬性的資訊。

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
| `id` | 與角色對應的ID。 此ID是自動生成的。 |
| `name` | 角色的名稱。 |
| `description` | description屬性提供有關您角色的其他資訊。 |
| `roleType` | 角色的指定類型。 角色類型的可能值為： `user-defined` 和 `system-defined`。 |
| `permissionSets` | 權限集表示管理員可以應用於角色的一組權限。 管理員可以將權限集分配給角色，而不是分配單個權限。 這允許您從包含一組權限的預定義角色建立自定義角色。 |
| `sandboxes` | 此屬性顯示您組織內為特定角色設定的沙箱。 |
| `subjectAttributes` | 指示主題與他們有權訪問的平台資源之間的關聯的屬性。 |
| `subjectAttributes.labels` | 顯示應用於查詢角色的資料使用標籤。 |

## 更新角色 {#patch}

您可以通過向以下對象發出PATCH請求來更新角色的屬性 `/roles` 端點，同時為要應用的操作提供相應的角色ID和值。

**API格式**

```http
PATCH /roles/{ROLE_ID}
```

| 參數 | 說明 |
| --- | --- |
| {ROLE_ID} | 要更新的角色的ID。 |

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
| `op` | 用於定義更新角色所需操作的操作調用。 操作包括： `add`。 `replace`, `remove`。 |
| `path` | 要更新的參數的路徑。 |
| `value` | 要用更新參數的新值。 |

**回應**

成功的響應將返回更新的角色，包括您選擇更新的屬性的新值。

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
| `id` | 與角色對應的ID。 此ID是自動生成的。 |
| `name` | 角色的名稱。 |
| `description` | description屬性提供有關您角色的其他資訊。 |
| `roleType` | 角色的指定類型。 角色類型的可能值為： `user-defined` 和 `system-defined`。 |
| `permissionSets` | 權限集表示管理員可以應用於角色的一組權限。 管理員可以將權限集分配給角色，而不是分配單個權限。 這允許您從包含一組權限的預定義角色建立自定義角色。 |
| `sandboxes` | 此屬性顯示您組織內為特定角色設定的沙箱。 |
| `subjectAttributes` | 指示主題與他們有權訪問的平台資源之間的關聯的屬性。 |
| `subjectAttributes.labels` | 顯示應用於查詢角色的資料使用標籤。 |

## 按角色ID更新角色 {#put}

您可以通過向 `/roles` 終結點並指定與要更新的角色對應的角色ID。

**API格式**

```http
PUT /roles/{ROLE_ID}
```

**要求**

以下請求更新角色ID的名稱、說明和角色類型： `3dfa045d-de58-4dfd-8ea9-e4e2c1b6d809`。

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
| `roleType` | 角色的指定類型。 角色類型的可能值為： `user-defined` 和 `system-defined`。 |

**回應**

成功返回更新的角色，包括名稱、說明和角色類型的新值。

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
| `id` | 與角色對應的ID。 此ID是自動生成的。 |
| `name` | 角色的名稱。 |
| `description` | description屬性提供有關您角色的其他資訊。 |
| `roleType` | 角色的指定類型。 角色類型的可能值為： `user-defined` 和 `system-defined`。 |
| `permissionSets` | 權限集表示管理員可以應用於角色的一組權限。 管理員可以將權限集分配給角色，而不是分配單個權限。 這允許您從包含一組權限的預定義角色建立自定義角色。 |
| `sandboxes` | 此屬性顯示您組織內為特定角色設定的沙箱。 |
| `subjectAttributes` | 指示主題與他們有權訪問的平台資源之間的關聯的屬性。 |
| `subjectAttributes.labels` | 顯示應用於查詢角色的資料使用標籤。 |

## 按角色ID更新主題

要更新與角色關聯的主題，請向 `/roles` 終結點，同時提供要更新的主題的角色ID。

**API格式**

```http
PATCH /roles/{ROLE_ID}
```

| 參數 | 說明 |
| --- | --- |
| {ROLE_ID} | 與要更新的主題關聯的角色的ID。 |

**要求**

以下請求更新與 `{ROLE_ID}`。

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
| `op` | 用於定義更新角色所需操作的操作調用。 操作包括： `add`。 `replace`, `remove`。 |
| `path` | 要更新的參數的路徑。 |
| `value` | 要用更新參數的新值。 |

**回應**

成功的響應返回與查詢的角色ID關聯的更新主題。

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

要刪除角色，請向 `/roles` 指定要刪除的角色的ID時執行端點。

**API格式**

```http
DELETE /roles/{ROLE_ID}
```

| 參數 | 說明 |
| --- | --- |
| {ROLE_ID} | 要刪除的角色的ID。 |

**要求**

以下請求刪除ID為 `{ROLE_ID}`。

```shell
curl -X DELETE \
  https://platform.adobe.io/data/foundation/access-control/administration/roles/{ROLE_ID} \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
```

**回應**

成功的響應返回HTTP狀態204（無內容）和空白正文。

您可以通過嘗試查找(GET)角色來確認刪除。 您將收到HTTP狀態404（未找到），因為該角色已從管理中刪除。
