---
keywords: Experience Platform；首頁；熱門主題；訪問控制權限；訪問控制資源類型；訪問控制API
solution: Experience Platform
title: 引用API終結點
description: 訪問控制API中的引用終結點允許您查看可用權限和資源類型的名稱，然後這些名稱可用於查看當前用戶的有效訪問控制策略。
exl-id: 18d84d54-9258-4451-9aa8-7c647b45a8da
source-git-commit: 16d85a2a4ee8967fc701a3fe631c9daaba9c9d70
workflow-type: tm+mt
source-wordcount: '188'
ht-degree: 1%

---

# 引用端點

>[!NOTE]
>
>如果傳遞用戶令牌，則令牌的用戶必須對所請求的組織具有「組織管理員」角色。

可以通過向以下對象發出GET請求來列出所有權限和資源類型的名稱： `/acl/reference` 端點。 然後，這些名稱可用於API調用 [查看有效的訪問控制策略](./effective-policies.md) 為當前用戶。

權限是通過Adobe Admin Console管理的策略，並映射到零個或更多資源類型的策略。 資源類型是一種策略，它為特定類型的 [!DNL Platform] 資源（如資料集或架構）。

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

成功的響應返回 `permissions` 對象和 `resource-types` 對象，每個對象分別包含訪問權限或資源類型的完整名稱清單。

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
