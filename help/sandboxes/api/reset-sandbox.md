---
keywords: Experience Platform;home；熱門主題；重置沙箱
solution: Experience Platform
title: 在API中重設沙盒
topic: 開發人員指南
description: 開發沙盒具有「工廠重設」功能，可從沙盒中刪除所有非預設資源。 您可以重設沙盒，方法是提出PUT請求，請求路徑中包含沙盒的名稱。
translation-type: tm+mt
source-git-commit: 62ce5ac92d03a6e85589fc92e8d953f7fc1d8f31
workflow-type: tm+mt
source-wordcount: '171'
ht-degree: 3%

---


# 在API中重設沙盒

開發沙盒具有「工廠重設」功能，可從沙盒中刪除所有非預設資源。 您可以重設沙盒，方法是提出PUT請求，請求路徑中包含沙盒的`name`。

**API格式**

```http
PUT /sandboxes/{SANDBOX_NAME}
```

| 參數 | 說明 |
| --- | --- |
| `{SANDBOX_NAME}` | 您要重設沙盒的`name`屬性。 |

**請求**

下列請求會重設名為&quot;dev-2&quot;的沙盒。

```shell
curl -X PUT \
  https://platform.adobe.io/data/foundation/sandbox-management/sandboxes/dev-2 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
    "action": "reset"
  }'
```

| 屬性 | 說明 |
| --- | --- |
| `action` | 此參數必須在請求裝載中提供值為&quot;reset&quot;，才能重設沙盒。 |

**回應**

成功的回應會傳回更新沙盒的詳細資料，顯示其`state`是「重設」。

```json
{
    "id": "d8184350-dbf5-11e9-875f-6bf1873fec16",
    "name": "dev-2",
    "title": "Development 2",
    "state": "resetting",
    "type": "development",
    "region": "VA7"
}
```

>[!NOTE]
>
>重設沙盒後，系統大約需要15分鐘才能布建。 布建後，沙盒的`state`會變成「作用中」或「失敗」。