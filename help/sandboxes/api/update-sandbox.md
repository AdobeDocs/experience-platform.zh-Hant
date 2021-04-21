---
keywords: Experience Platform;home；熱門主題；更新沙盒
solution: Experience Platform
title: 在API中更新沙盒
topic-legacy: developer guide
description: 您可以更新沙盒中的一或多個欄位，方法是提出PATCH請求，請求路徑中包含沙盒的名稱，請求裝載中包含要更新的屬性。
exl-id: a8ef4305-5e0c-4d8f-8663-1933c957f122
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '133'
ht-degree: 3%

---

# 在API中更新沙盒

您可以更新沙盒中的一或多個欄位，方法是提出PATCH請求，請求中包含沙盒的`name`在請求路徑中，以及要在請求裝載中更新的屬性。

>[!NOTE]
>
>目前只能更新沙盒的`title`屬性。

**API格式**

```http
PATCH /sandboxes/{SANDBOX_NAME}
```

| 參數 | 說明 |
| --- | --- |
| `{SANDBOX_NAME}` | 您要更新沙盒的`name`屬性。 |

**要求**

下列請求會更新名為&quot;dev-2&quot;的沙盒的`title`屬性。

```shell
curl -X PATCH \
  https://platform.adobe.io/data/foundation/sandbox-management/sandboxes/dev-2 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
    "title": "Development B"
  }'
```

**回應**

成功的回應會傳回HTTP狀態200（確定），並包含最新更新沙盒的詳細資訊。

```json
{
    "name": "dev-2",
    "title": "Development B",
    "state": "active",
    "type": "development",
    "region": "VA7"
}
```
