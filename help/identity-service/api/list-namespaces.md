---
keywords: Experience Platform；首頁；熱門主題；命名空間清單；list namespace
solution: Experience Platform
title: 列出可用標識命名空間
description: 列出所有可用命名空間。
exl-id: b65e5f86-143d-4ca5-8b3f-2c0a24433bbf
source-git-commit: 6d01bb4c5212ed1bb69b9a04c6bfafaad4b108f9
workflow-type: tm+mt
source-wordcount: '83'
ht-degree: 4%

---

# 列出可用標識命名空間

**API格式**

```http
GET /idnamespace/identities
```

**要求**

```shell
curl -X GET \
  'https://platform-va7.adobe.io/data/core/idnamespace/identities' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

響應包括對象陣列，每個對象表示可用的命名空間。 具有「」的命名空間[!UICONTROL 自定義]&quot;值&quot;[!UICONTROL 假]&#39;&#39;是標準命名空間，而&#39;&#39;[!UICONTROL 自定義]&quot;值&quot;[!UICONTROL 真]&#39;&#39;是您的組織建立的命名空間。

>[!NOTE]
>
>此響應已被截斷為空間。

```json
[
  {
        "updateTime": 1441122419000,
        "code": "CORE",
        "status": "ACTIVE",
        "description": "CORE Namespace",
        "id": 0,
        "createTime": 1441122419000,
        "idType": "COOKIE",
        "name": "CORE",
        "custom": false
    },
    {
        "updateTime": 1495153678000,
        "code": "ECID",
        "status": "ACTIVE",
        "description": "ECID Namespace",
        "id": 4,
        "createTime": 1495153678000,
        "idType": "COOKIE",
        "name": "ECID",
        "custom": false
    },
    {
        "updateTime": 1522783145000,
        "code": "AdCloud",
        "status": "ACTIVE",
        "description": "Adobe AdCloud - ID Syncing Partner",
        "id": 411,
        "createTime": 1522783145000,
        "idType": "COOKIE",
        "name": "AdCloud",
        "custom": false
    }
]
```

## 後續步驟

繼續下一教程， [建立自定義命名空間](./create-custom-namespace.md)
