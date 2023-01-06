---
keywords: Experience Platform；首頁；熱門主題；存取控制權限；存取控制資源類型；存取控制api
solution: Experience Platform
title: 參考API端點
description: 訪問控制API中的引用端點允許您查看可用權限和資源類型的名稱，然後這些權限和資源類型可用於查看當前用戶的有效訪問控制策略。
exl-id: 18d84d54-9258-4451-9aa8-7c647b45a8da
source-git-commit: 7b197f253aa5ce04a682040814cf749407154ebc
workflow-type: tm+mt
source-wordcount: '165'
ht-degree: 1%

---

# 參考端點

您可以向發出GET要求，以列出所有權限和資源類型的名稱 `/acl/reference` 端點。 然後，這些名稱便可用於對 [查看有效的訪問控制策略](./effective-policies.md) 針對目前使用者。

權限是透過Adobe Admin Console管理，並映射至零個或更多資源類型原則的原則。 資源類型是一種策略，它為特定類型的 [!DNL Platform] 資源（例如資料集或結構）。

**API格式**

```http
GET /acl/reference
```

**要求**

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/access-control/acl/reference \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}'
```

**回應**

成功的回應會傳回 `permissions` 物件和 `resource-types` 對象，每個對象分別包含訪問權限或資源類型的完整名稱清單。

```json
{
  "permissions": {
    "export-audience-for-segment": {
      "segments": [
        "read"
      ]
    },
    "manage-datasets": {
      "connection": [
        "read",
        "write",
        "delete"
      ],
      "datasets": [
        "read",
        "write",
        "delete"
      ]
    }
    {"..."}
  },
  "resource-types": {
    "classes": [
      "read",
      "write",
      "delete"
    ],
    "connection": [
      "read",
      "write",
      "delete"
    ],
    "data-types": [
      "read",
      "write",
      "delete"
    ],
    "...": [
      "..."
    ]
  }
}
```
