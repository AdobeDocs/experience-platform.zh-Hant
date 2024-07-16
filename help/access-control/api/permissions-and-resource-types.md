---
keywords: Experience Platform；首頁；熱門主題；存取控制許可權；存取控制資源型別；存取控制api
solution: Experience Platform
title: 參考API端點
description: 存取控制API中的參考端點可讓您檢視可用許可權和資源型別的名稱，然後這些名稱可用來檢視目前使用者的有效存取控制原則。
role: Developer
exl-id: 18d84d54-9258-4451-9aa8-7c647b45a8da
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
workflow-type: tm+mt
source-wordcount: '188'
ht-degree: 1%

---

# 參考端點

>[!NOTE]
>
>如果傳遞的是使用者權杖，則權杖的使用者必須具有請求組織的「組織管理員」角色。

您可以透過向`/acl/reference`端點發出GET要求來列出所有許可權和資源型別的名稱。 然後，這些名稱便可以用在對[檢視目前使用者的有效存取控制原則](./effective-policies.md)的API呼叫中。

許可權是透過Adobe Admin Console管理的原則，並對應到零個或多個資源型別原則。 資源型別是啟用特定型別[!DNL Platform]資源（例如資料集或結構描述）的讀取、寫入和/或刪除功能的原則。

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

成功的回應會傳回`permissions`物件和`resource-types`物件，分別包含存取許可權或資源型別的完整名稱清單。

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
