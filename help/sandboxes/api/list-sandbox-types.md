---
keywords: Experience Platform;home;popular topics;list sandboxes
solution: Experience Platform
title: 列出支援的沙盒類型
topic: developer guide
description: 您可以向/sandboxTypes端點提出GET請求，以擷取組織支援的沙盒類型清單。
translation-type: tm+mt
source-git-commit: 0af537e965605e6c3e02963889acd85b9d780654
workflow-type: tm+mt
source-wordcount: '68'
ht-degree: 2%

---


# 列出支援的沙盒類型

您可以向端點提出GET請求，以擷取組織支援的沙盒類型清 `/sandboxTypes` 單。

**API格式**

```http
GET /sandboxTypes
```

**請求**

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/sandbox-management/sandboxTypes \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應會傳回組織支援的沙盒類型清單。

```json
{
    "sandboxTypes": [
        "production",
        "development"
    ]
}
```
