---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 列出支援的沙盒類型
topic: developer guide
translation-type: tm+mt
source-git-commit: b4741cdfd065bbaed7f2feeafe8619191e4b8f6c
workflow-type: tm+mt
source-wordcount: '47'
ht-degree: 4%

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
