---
keywords: Experience Platform;home;popular topics;update sandbox
solution: Experience Platform
title: 更新沙盒
topic: developer guide
description: 您可以透過提出PATCH請求來更新沙盒中的一或多個欄位，該請求會在請求路徑中包含沙盒的名稱，並在請求裝載中包含要更新的屬性。
translation-type: tm+mt
source-git-commit: 0af537e965605e6c3e02963889acd85b9d780654
workflow-type: tm+mt
source-wordcount: '120'
ht-degree: 3%

---


# 更新沙盒

您可以透過提出PATCH請求來更新沙盒中的一或多個欄位，該請求會在請求路徑中包含沙盒的 `name` ，並在請求裝載中包含要更新的屬性。

>[!NOTE]
>
>目前只能更新沙盒 `title` 的屬性。

**API格式**

```http
PATCH /sandboxes/{SANDBOX_NAME}
```

| 參數 | 說明 |
| --- | --- |
| `{SANDBOX_NAME}` | 您 `name` 要更新沙盒的屬性。 |

**請求**

下列請求會更新 `title` 名為&quot;dev-2&quot;的沙盒屬性。

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
