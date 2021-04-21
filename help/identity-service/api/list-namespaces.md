---
keywords: Experience Platform;home；常用主題；namespace list;list namespace
solution: Experience Platform
title: 列出可用身份名稱空間
topic-legacy: API guide
description: 列出所有可用的名稱空間。
exl-id: b65e5f86-143d-4ca5-8b3f-2c0a24433bbf
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '79'
ht-degree: 5%

---

# 列出可用的身份名稱空間

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
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

響應包括對象陣列，每個對象表示可用的命名空間。 「[!UICONTROL custom]」值為「[!UICONTROL false]」的名稱空間是標準名稱空間，而「[!UICONTROL custom]」值為「[!UICONTROL true]」的名稱空間是您的組織已建立的名稱空間。

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

繼續下一個教學課程，以[建立自訂命名空間](./create-custom-namespace.md)
