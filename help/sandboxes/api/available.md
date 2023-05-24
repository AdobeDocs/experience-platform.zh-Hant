---
keywords: Experience Platform；首頁；熱門主題；清單可用沙箱；清單沙箱
solution: Experience Platform
title: 可用沙箱API終結點
description: 通過向可用沙箱端點發出GET請求，可以列出當前用戶可用的沙箱。
exl-id: 9b0719af-c1ca-439a-9c8b-86c7fa26a3b8
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '256'
ht-degree: 2%

---

# 可用沙箱端點

>[!NOTE]
>
>與沙盒API中提供的其他終結點不同，此終結點可供所有用戶使用，包括那些沒有沙盒管理訪問權限的用戶。

通過向可用沙箱端點發出GET請求，可以列出當前用戶可用的沙箱。

**API格式**

```http
GET /{QUERY_PARAMS}
```

| 參數 | 說明 |
| --------- | ----------- |
| `{QUERY_PARAMS}` | 用於篩選結果的可選查詢參數。 查看 [附錄文檔](./appendix.md#query) 的子菜單。 |

**要求**

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/sandbox-management/?&limit=3&offset=1 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}'
```

**回應**

成功的響應將返回當前用戶可用的沙盒清單，包括詳細資訊，如 `name`。 `title`。 `state`, `type`。

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
| `name` | 沙盒的名稱。 用於API調用中的查找目的。 |
| `title` | 沙盒的顯示名稱。 |
| `state` | 沙盒的當前處理狀態。 沙盒的狀態可以是下列任何一種： <ul><li>`creating`:沙盒已建立，但系統仍在設定。</li><li>`active`:沙盒已建立並處於活動狀態。</li><li>`failed`:由於錯誤，系統無法設定沙盒並且已禁用。</li><li>`deleted`:已手動禁用沙盒。</li></ul> |
| `type` | 沙盒類型，即「development」或「production」。 |
| `isDefault` | 一個布爾屬性，用於指示此沙盒是否是組織的預設生產沙盒。 |
| `eTag` | 沙盒的特定版本的標識符。 用於版本控制和快取效率，每次更改沙盒時都會更新此值。 |
