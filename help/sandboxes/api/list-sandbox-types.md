---
keywords: Experience Platform;home；熱門主題；清單沙箱
solution: Experience Platform
title: 在API中列出支援的沙盒類型
topic: developer guide
description: 您可以向/sandboxTypes端點提出GET請求，以擷取組織支援的沙盒類型清單。
translation-type: tm+mt
source-git-commit: 36f63cecd49e6a6b39367359d50252612ea16d7a
workflow-type: tm+mt
source-wordcount: '81'
ht-degree: 2%

---


# 在API中列出支援的沙盒類型

您可以向`/sandboxTypes`端點提出GET請求，以擷取組織支援的沙盒類型清單。

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
