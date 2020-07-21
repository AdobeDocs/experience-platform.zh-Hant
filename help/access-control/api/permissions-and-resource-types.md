---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 權限和資源類型的清單名稱
topic: developer guide
translation-type: tm+mt
source-git-commit: 73a492ba887ddfe651e0a29aac376d82a7a1dcc4
workflow-type: tm+mt
source-wordcount: '123'
ht-degree: 1%

---


# 權限和資源類型的清單名稱

通過向端點發出GET請求，可以列出所有權限和資源類型的 `/acl/reference` 名稱。 然後，這些名稱可用於API呼叫中，以 [檢視目前使用者的](./effective-policies.md) 有效原則。

權 **限** 是透過Adobe Admin Console管理的原則，並對應至零或多個資源類型原則。 資 **源類型** ，是一種策略，可為特定資源類型（如資料集或方案）啟用讀、寫和/ [!DNL Platform] 或刪除功能。

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

成功的響應返回 `permissions` 對象和對 `resource-types` 像，每個對象分別包含訪問權限或資源類型的完整名稱清單。

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
