---
keywords: Experience Platform；首頁；熱門主題；api；基於屬性的訪問控制；基於屬性的訪問控制
solution: Experience Platform
title: 產品API終結點
description: 基於屬性的訪問控制API中的/products端點允許您以寫程式方式管理Adobe Experience Platform的產品。
exl-id: 44ee9a9d-7a13-4d59-a1a9-97764dbd3763
source-git-commit: 16d85a2a4ee8967fc701a3fe631c9daaba9c9d70
workflow-type: tm+mt
source-wordcount: '515'
ht-degree: 3%

---

# 產品終結點

>[!NOTE]
>
>如果傳遞用戶令牌，則令牌的用戶必須對所請求的組織具有「組織管理員」角色。

的 `/products` 通過基於屬性的訪問控制API中的端點，您可以以寫程式方式管理產品以及與組織中的產品相關聯的權限類別和權限集。

## 快速入門

本指南中使用的API終結點是基於屬性的訪問控制API的一部分。 在繼續之前，請查看 [入門指南](./getting-started.md) 有關相關文檔的連結、閱讀本文檔中示例API調用的指南，以及有關成功調用任何Experience PlatformAPI所需標頭的重要資訊。

## 檢索已授權產品的清單 {#list}

您可以通過向以下站點發出GET請求來檢索已授權產品的清單 `/products` 端點。

**API格式**

```http
GET /products/
```

**要求**

以下請求將檢索屬於您組織的有權產品清單。

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/access-control/administration/products \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
```

**回應**

成功的響應將返回屬於您組織的有權產品清單。

```json
{
  "products": [
    {
      "id": "{ID}",
      "name": "Adobe Experience Platform",
      "serviceCode": "{SERVICE_CODE}"
    }
  ]
}
```

| 屬性 | 說明 |
| --- | --- |
| `id` | 查詢產品的相應ID。 |
| `name` | 查詢的產品的名稱。 |
| `serviceCode` | 查詢產品的相應服務代碼。 |

## 按產品ID查找權限類別

您可以通過向以下對象發出GET請求來查找給定產品的權限類別 `/products/{PRODUCT_ID}/categories` 指定產品ID時的終結點。

**API格式**

```http
GET /products/{PRODUCT_ID}/categories
```

| 參數 | 說明 |
| --- | --- |
| {PRODUCT_ID} | 與要查找的權限類別關聯的產品的ID。 |

**要求**

以下請求檢索與關聯的權限類別 `{PRODUCT_ID}`。

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/access-control/administration/products/{PRODUCT_ID}/categories \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
```

**回應**

成功的響應將返回與您查詢的產品ID關聯的權限類別。

```json
{
  "categories": [
    {
        "name": "Profile Management"
    },
    {
        "name": "Data Ingestion"
    },
    {
        "name": "Sandbox Administration"
    },
    {
        "name": "Query Service"
    },
    {
        "name": "Data Management"
    },
    {
        "name": "Identity Management"
    },
    {
        "name": "Data Modeling"
    },
    {
        "name": "Data Science Workspace"
    },
    {
        "name": "Dashboards"
    },
    {
        "name": "Alerts"
    },
    {
        "name": "Data Governance"
    }
  ]
}
```

| 屬性 | 說明 |
| --- | --- |
| `category` | 查詢的產品ID中可用的權限類別。 |
| `name` | 權限類別的名稱。 |

## 按產品ID查找權限集

您可以通過向Web站點發出GET請求來查找給定產品的權限集 `/products/{PRODUCT_ID}/permission-sets` 指定產品ID時的終結點。

**API格式**

```http
GET /products/{PRODUCT_ID}/permission-sets
```

| 參數 | 說明 |
| --- | --- |
| {PRODUCT_ID} | 與要查找的權限集關聯的產品的ID。 |

**要求**

以下請求檢索與關聯的權限集 `{PRODUCT_ID}`。

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/access-control/administration/products/{PRODUCT_ID}/permission-sets \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
```

**回應**

成功的響應將返回與您查詢的產品ID關聯的權限集。

```json
{
  "permission-sets": [
      {
          "id": "manage-schemas",
          "name": "Manage Schemas",
          "category": "Data Modeling",
          "permissions": [
              {
                  "resource": "schemas",
                  "actions": [
                      "read",
                      "write",
                      "delete"
                  ]
              },
              {
                  "resource": "schema-fields",
                  "actions": [
                      "read",
                      "write",
                      "delete"
                  ]
              },
              {
                  "resource": "sandboxes",
                  "actions": [
                      "view"
                  ]
              }
          ]
      },
      {
          "id": "view-schemas",
          "name": "View Schemas",
          "category": "Data Modeling",
          "permissions": [
              {
                  "resource": "schemas",
                  "actions": [
                      "read"
                  ]
              },
              {
                  "resource": "schema-fields",
                  "actions": [
                      "read"
                  ]
              },
              {
                  "resource": "sandboxes",
                  "actions": [
                      "view"
                  ]
              }
          ]
      },
  ]
}
```

| 屬性 | 說明 |
| --- | --- |
| `permission-sets` | 權限集表示管理員可以應用於角色的一組權限。 管理員可以將權限集分配給角色，而不是分配單個權限。 這允許您從包含一組權限的預定義角色建立自定義角色。 |
| `id` | 查詢的權限集的相應ID。 |
| `name` | 查詢的權限集的對應名稱。 |
| `category` | 可用權限類別。 |
| `permissions` | 權限包括查看和/或使用平台功能（如建立沙箱、定義架構和管理資料集）的能力。 |
| `permissions.resource` | 主題可以訪問或無法訪問的資產或對象。 資源可以是檔案、應用程式、伺服器，甚至是API。 |
| `permissions.actions` | 允許主體對查詢的資源執行的操作。 可能的值包括： `view`。 `read`。 `create`。 `edit`, `delete` |
