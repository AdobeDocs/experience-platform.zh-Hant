---
keywords: Experience Platform; home；熱門主題；訪問控制權限；訪問控制資源類型；訪問控制api
solution: Experience Platform
title: 參考API端點
topic: developer guide
description: Adobe Experience Platform中的存取控制功能可讓您使用Adobe Admin Console管理各種平台功能的角色和權限。 通過向訪問控制API中的/acl/reference端點發出GET請求，可以列出所有權限和資源類型的名稱。 然後，這些名稱可用於API呼叫，以檢視目前使用者的有效原則。
translation-type: tm+mt
source-git-commit: 698639d6c2f7897f0eb4cce2a1f265a0f7bb57c9
workflow-type: tm+mt
source-wordcount: '195'
ht-degree: 1%

---


# 參照端點

通過向`/acl/reference`端點發出GET請求，可以列出所有權限和資源類型的名稱。 然後，這些名稱可用於[檢視目前使用者之有效原則](./effective-policies.md)的API呼叫。

權限是透過Adobe Admin Console管理的原則，並對應至零或多個資源類型原則。 資源類型是一種策略，可為特定類型的[!DNL Platform]資源（如資料集或方案）啟用讀、寫和／或刪除功能。

**API格式**

```http
GET /acl/reference
```

**請求**

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/access-control/acl/reference \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}'
```

**回應**

成功的響應返回`permissions`對象和`resource-types`對象，每個對象分別包含訪問權限或資源類型的完整名稱清單。

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
