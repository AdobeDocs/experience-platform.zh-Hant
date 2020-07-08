---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 列出可用的名稱空間
topic: API guide
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '68'
ht-degree: 5%

---


# 列出可用的名稱空間

**API格式**

```http
GET /idnamespace/identities
```

**請求**

```shell
curl -X GET \
  'https://platform-va7.adobe.io/data/core/idnamespace/identities' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

響應包括對象陣列，每個對象表示可用的命名空間。 具有&quot;[!UICONTROL custom]&quot;值&quot;[!UICONTROL false]&quot;的名稱空間是標準名稱空間，而具有&quot;[!UICONTROL custom]&quot;值&quot;true&quot;值的名稱空間是貴組織已建立的名稱空間。

>[!NOTE]
>
>此回應已針對空間截斷。

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

繼續下一個教學課程，以建 [立自訂命名空間](./create-custom-namespace.md)