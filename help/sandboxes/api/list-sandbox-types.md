---
keywords: Experience Platform；首頁；熱門主題；清單沙箱
solution: Experience Platform
title: 在API中列出支援的沙盒類型
topic: 開發人員指南
description: 您可以向/sandboxTypes端點提出GET請求，以擷取組織支援的沙盒類型清單。
translation-type: tm+mt
source-git-commit: 62ce5ac92d03a6e85589fc92e8d953f7fc1d8f31
workflow-type: tm+mt
source-wordcount: '83'
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
