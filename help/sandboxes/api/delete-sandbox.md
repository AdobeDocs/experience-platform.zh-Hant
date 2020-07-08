---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 刪除沙盒
topic: developer guide
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '84'
ht-degree: 4%

---


# 刪除沙盒

您可以透過提出DELETE請求來刪除沙盒，請求路徑中包含沙 `name` 盒的請求。

>[!NOTE]
>
>使用此API呼叫會將沙盒的屬性 `status` 更新為「已刪除」並停用它。 刪除沙盒後，GET請求仍可擷取其詳細資訊。

**API格式**

```http
DELETE /sandboxes/{SANDBOX_NAME}
```

| 參數 | 說明 |
| --- | --- |
| `{SANDBOX_NAME}` | 您 `name` 要刪除的沙盒。 |

**請求**

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

成功的回應會傳回沙盒的更新詳細資訊，顯示其 `state` 已「刪除」。

```json
{
    "name": "dev-2",
    "title": "Development 2",
    "state": "deleted",
    "type": "development",
    "region": "VA7"
}
```
