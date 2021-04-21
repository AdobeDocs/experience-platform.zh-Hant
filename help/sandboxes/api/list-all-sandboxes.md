---
keywords: Experience Platform；首頁；熱門主題；清單沙箱
solution: Experience Platform
title: 在API中列出沙盒
topic-legacy: developer guide
description: 若要列出屬於您IMS組織（活動或其他）的所有沙盒，請向/sandbox端點提出GET要求。
exl-id: 5e7dc6e7-cb9c-41e0-a3ad-025b625f14ec
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '320'
ht-degree: 2%

---

# 列出API中的沙盒

若要列出屬於您IMS組織（活動或其他）的所有沙盒，請向`/sandboxes`端點提出GET要求。

**API格式**

```http
GET /sandboxes?{QUERY_PARAMS}
```

| 參數 | 說明 |
| --------- | ----------- |
| `{QUERY_PARAMS}` | 可選查詢參數，以篩選結果。 如需詳細資訊，請參閱[查詢參數](#query)一節。 |

**要求**

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/sandbox-management/sandboxes?&limit=4&offset=1 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應會傳回屬於您組織的沙盒清單，包括`name`、`title`、`state`和`type`等詳細資訊。

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
    ],
    "_page": {
        "limit": 4,
        "count": 4
    },
    "_links": {
        "next": {
            "href": "https://platform.adobe.io:443/data/foundation/sandbox-management/sandboxes/?limit={limit}&offset={offset}",
            "templated": true
        },
        "prev": {
            "href": "https://platform.adobe.io:443/data/foundation/sandbox-management/sandboxes?offset=0&limit=1",
            "templated": null
        },
        "page": {
            "href": "https://platform-int.adobe.io:443/data/foundation/sandbox-management/sandboxes?offset=1&limit=1",
            "templated": null
        }
    }
}
```

| 屬性 | 說明 |
| --- | --- |
| `name` | 沙盒的名稱。 用於API呼叫中的查閱用途。 |
| `title` | 沙盒的顯示名稱。 |
| `state` | 沙盒的目前處理狀態。 沙盒的狀態可以是下列任一項：<br/><ul><li>**建立**:沙盒已建立，但系統仍在布建中。</li><li>**作用中**:沙盒會建立並啟用。</li><li>**失敗**:由於發生錯誤，系統無法布建沙盒並停用沙盒。</li><li>**已刪除**:沙盒已手動停用。</li></ul> |
| `type` | 沙盒類型，「開發」或「生產」。 |
| `isDefault` | 布林屬性，指出此沙盒是否為組織的預設沙盒。 通常這是生產沙盒。 |
| `eTag` | 沙盒特定版本的識別碼。 用於版本控制和快取效率，此值會在每次對沙盒進行變更時更新。 |

## 使用查詢參數{#query}

[[!DNL Sandbox]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sandbox-api.yaml) API支援在列出沙盒時，對頁面使用查詢參數並篩選結果。

>[!NOTE]
>
>必須同時指定`limit`和`offset`查詢參數。 如果您只指定一個，API將會傳回錯誤。 如果指定無，則預設限制為50，偏移為0。

| 參數 | 說明 |
| --------- | ----------- |
| `limit` | 響應中要返回的最大記錄數。 |
| `offset` | 從第一個記錄開始（偏移）響應清單的實體數。 |
