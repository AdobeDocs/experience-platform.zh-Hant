---
keywords: Experience Platform;home;popular topics;list sandboxes
solution: Experience Platform
title: 列出所有沙盒
topic: developer guide
description: 若要列出屬於您IMS組織（活動或其他）的所有沙盒，請向/sandbox端點提出GET要求。
translation-type: tm+mt
source-git-commit: 0af537e965605e6c3e02963889acd85b9d780654
workflow-type: tm+mt
source-wordcount: '205'
ht-degree: 1%

---


# 列出所有沙盒

若要列出屬於您IMS組織（活動或其他）的所有沙盒，請向端點提出GET請 `/sandboxes` 求。

**API格式**

```http
GET /sandboxes
```

**請求**

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/sandbox-management/sandboxes \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應會傳回屬於您組織的沙盒清單，包括諸如、 `name`、 `title``state`和等詳細資訊 `type`。

```json
{
    "sandboxes": [
        {
            "name": "prod",
            "title": "Production",
            "state": "active",
            "type": "production",
            "region": "VA7",
            "isDefault": true,
            "eTag": 2,
            "createdDate": "2019-09-04 04:57:24",
            "lastModifiedDate": "2019-09-04 04:57:24",
            "createdBy": "{USER_ID}",
            "modifiedBy": "{USER_ID}"
        },
        {
            "name": "dev",
            "title": "Development",
            "state": "active",
            "type": "development",
            "region": "VA7",
            "isDefault": false,
            "eTag": 1,
            "createdDate": "2019-09-03 22:27:48",
            "lastModifiedDate": "2019-09-03 22:27:48",
            "createdBy": "{USER_ID}",
            "modifiedBy": "{USER_ID}"
        },
        {
            "name": "stage",
            "title": "Staging",
            "state": "active",
            "type": "development",
            "region": "VA7",
            "isDefault": false,
            "eTag": 1,
            "createdDate": "2019-09-03 22:27:48",
            "lastModifiedDate": "2019-09-03 22:27:48",
            "createdBy": "{USER_ID}",
            "modifiedBy": "{USER_ID}"
        },
        {
            "name": "dev-2",
            "title": "Development 2",
            "state": "creating",
            "type": "development",
            "region": "VA7",
            "isDefault": false,
            "eTag": 1,
            "createdDate": "2019-09-07 10:16:02",
            "lastModifiedDate": "2019-09-07 10:16:02",
            "createdBy": "{USER_ID}",
            "modifiedBy": "{USER_ID}"
        }
    ]
}
```

| 屬性 | 說明 |
| --- | --- |
| `name` | 沙盒的名稱。 用於API呼叫中的查閱用途。 |
| `title` | 沙盒的顯示名稱。 |
| `state` | 沙盒的目前處理狀態。 沙盒的狀態可以是下列任一項： <br/><ul><li>**建立**:沙盒已建立，但系統仍在布建中。</li><li>**作用中**:沙盒會建立並啟用。</li><li>**失敗**:由於發生錯誤，系統無法布建沙盒並停用沙盒。</li><li>**已刪除**:沙盒已手動停用。</li></ul> |
| `type` | 沙盒類型，「開發」或「生產」。 |
| `isDefault` | 布林屬性，指出此沙盒是否為組織的預設沙盒。 通常這是生產沙盒。 |
| `eTag` | 沙盒特定版本的識別碼。 用於版本控制和快取效率，此值會在每次對沙盒進行變更時更新。 |
