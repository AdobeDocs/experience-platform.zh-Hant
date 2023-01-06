---
keywords: Experience Platform；首頁；熱門主題；命名空間清單；清單命名空間
solution: Experience Platform
title: 列出可用的身分識別命名空間
description: 列出所有可用的命名空間。
exl-id: b65e5f86-143d-4ca5-8b3f-2c0a24433bbf
source-git-commit: 6d01bb4c5212ed1bb69b9a04c6bfafaad4b108f9
workflow-type: tm+mt
source-wordcount: '83'
ht-degree: 4%

---

# 列出可用的身分識別命名空間

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

回應包含一個物件陣列，每個物件代表可用的命名空間。 含有「[!UICONTROL 自訂]&quot;值&quot;[!UICONTROL false]「是標準命名空間，而具有「[!UICONTROL 自訂]&quot;值&quot;[!UICONTROL true]「 」是貴組織已建立的命名空間。

>[!NOTE]
>
>此回應已因空間而截斷。

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

繼續下一個教學課程，前往 [建立自訂命名空間](./create-custom-namespace.md)
