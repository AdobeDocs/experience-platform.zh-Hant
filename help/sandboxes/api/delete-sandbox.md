---
keywords: Experience Platform;home；熱門主題；刪除沙盒
solution: Experience Platform
title: 刪除API中的沙盒
topic-legacy: developer guide
description: 您可以透過提出DELETE請求來刪除沙盒，請求路徑中包含沙盒的名稱。
exl-id: c900325e-bc28-42f1-bc9a-eecb33fa9be4
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '116'
ht-degree: 3%

---

# 刪除API中的沙盒

您可以透過提出DELETE請求，將沙盒的`name`包含在請求路徑中，以刪除沙盒。

>[!NOTE]
>
>讓此API呼叫將沙盒的`status`屬性更新為&quot;deleted&quot;，並停用它。 GET請求在刪除後仍可擷取沙盒的詳細資訊。

**API格式**

```http
DELETE /sandboxes/{SANDBOX_NAME}
```

| 參數 | 說明 |
| --- | --- |
| `{SANDBOX_NAME}` | 您要刪除的沙盒的`name`。 |

**要求**

下列請求會刪除名為&quot;dev-2&quot;的沙盒。

```shell
curl -X DELETE \
  https://platform.adobe.io/data/foundation/sandbox-management/sandboxes/dev-2 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應會傳回沙盒的更新詳細資訊，顯示其`state`已「刪除」。

```json
{
    "name": "dev-2",
    "title": "Development 2",
    "state": "deleted",
    "type": "development",
    "region": "VA7"
}
```
