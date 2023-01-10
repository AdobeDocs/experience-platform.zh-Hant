---
keywords: Experience Platform；首頁；熱門主題；清單可用沙箱；清單沙箱
solution: Experience Platform
title: 可用沙箱API端點
description: 您可以向可用的沙箱端點提出GET要求，以列出目前使用者可用的沙箱。
exl-id: 9b0719af-c1ca-439a-9c8b-86c7fa26a3b8
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '256'
ht-degree: 2%

---

# 可用沙箱端點

>[!NOTE]
>
>與沙箱API中提供的其他端點不同，此端點可供所有使用者使用，包括沒有沙箱管理存取權限的使用者。

您可以向可用的沙箱端點提出GET要求，以列出目前使用者可用的沙箱。

**API格式**

```http
GET /{QUERY_PARAMS}
```

| 參數 | 說明 |
| --------- | ----------- |
| `{QUERY_PARAMS}` | 可選的查詢參數，以依據篩選結果。 請參閱 [附錄檔案](./appendix.md#query) 以取得可用參數的清單。 |

**要求**

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/sandbox-management/?&limit=3&offset=1 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}'
```

**回應**

成功的回應會傳回目前使用者可用的沙箱清單，包括 `name`, `title`, `state`，和 `type`.

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
        }
    ],
    "_page": {
        "limit": 3,
        "count": 1
    },
    "_links": {
        "page": {
            "href": "https://platform.adobe.io:443/data/foundation/sandbox-management/?limit={limit}&offset={offset}",
            "templated": true
        }
    }
}
```

| 屬性 | 說明 |
| --- | --- |
| `name` | 沙箱的名稱。 用於API呼叫中的查詢用途。 |
| `title` | 沙箱的顯示名稱。 |
| `state` | 沙箱的目前處理狀態。 沙箱的狀態可以是下列任一項： <ul><li>`creating`:沙箱已建立，但系統仍在布建。</li><li>`active`:沙箱已建立且作用中。</li><li>`failed`:由於錯誤，系統無法布建沙箱，且已停用。</li><li>`deleted`:沙箱已手動停用。</li></ul> |
| `type` | 沙箱類型，「開發」或「生產」。 |
| `isDefault` | 此布林值屬性可指出此沙箱是否為組織的預設生產沙箱。 |
| `eTag` | 沙箱特定版本的識別碼。 用於版本控制和快取效率，此值會在每次對沙箱進行變更時更新。 |
