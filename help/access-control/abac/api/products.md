---
keywords: Experience Platform；首頁；熱門主題；API；屬性型存取控制；屬性型存取控制
solution: Experience Platform
title: 產品API端點
description: 屬性型存取控制API中的/products端點可讓您以程式設計方式管理Adobe Experience Platform中的產品。
exl-id: 44ee9a9d-7a13-4d59-a1a9-97764dbd3763
source-git-commit: 9e44e647e4647a323fa9d1af55266d6f32b5ccb9
workflow-type: tm+mt
source-wordcount: '492'
ht-degree: 3%

---

# 產品端點

此 `/products` 屬性型存取控制API中的端點可讓您以程式設計方式管理產品，以及與貴組織產品相關聯的權限類別和權限集。

## 快速入門

本指南中使用的API端點是屬性型存取控制API的一部分。 繼續之前，請檢閱 [快速入門手冊](./getting-started.md) 如需相關檔案的連結，請參閱本檔案中讀取範例API呼叫的指南，以及成功呼叫任何Experience PlatformAPI所需的必要標頭重要資訊。

## 擷取已授權產品的清單 {#list}

您可以向 `/products` 端點。

**API格式**

```http
GET /products/
```

**要求**

下列請求會擷取屬於您組織的已授權產品清單。

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/access-control/administration/products \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
```

**回應**

成功的回應會傳回屬於您組織的已授權產品清單。

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
| `id` | 查詢產品的對應ID。 |
| `name` | 查詢的產品的名稱。 |
| `serviceCode` | 查詢產品的對應服務代碼。 |

## 依產品ID查詢權限類別

您可以向 `/products/{PRODUCT_ID}/categories` 端點，同時指定您的產品ID。

**API格式**

```http
GET /products/{PRODUCT_ID}/categories
```

| 參數 | 說明 |
| --- | --- |
| {PRODUCT_ID} | 與您要查詢的權限類別相關聯的產品ID。 |

**要求**

下列請求會擷取與 `{PRODUCT_ID}`.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/access-control/administration/products/{PRODUCT_ID}/categories \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
```

**回應**

成功的回應會傳回與您查詢的產品ID相關聯的權限類別。

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

## 依產品ID查詢權限集

您可以向 `/products/{PRODUCT_ID}/permission-sets` 端點，同時指定您的產品ID。

**API格式**

```http
GET /products/{PRODUCT_ID}/permission-sets
```

| 參數 | 說明 |
| --- | --- |
| {PRODUCT_ID} | 與您要查詢的權限集相關聯的產品ID。 |

**要求**

下列請求會擷取與 `{PRODUCT_ID}`.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/access-control/administration/products/{PRODUCT_ID}/permission-sets \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
```

**回應**

成功的回應會傳回與您查詢的產品ID相關聯的權限集。

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
| `permission-sets` | 權限集表示管理員可以應用到角色的一組權限。 管理員可以將權限集指派給角色，而不是指派個別權限。 這可讓您從包含一組權限的預先定義角色中建立自訂角色。 |
| `id` | 查詢的權限集的對應ID。 |
| `name` | 查詢的權限集的對應名稱。 |
| `category` | 可用權限類別。 |
| `permissions` | 權限包括檢視和/或使用Platform功能的功能，例如建立沙箱、定義結構描述及管理資料集。 |
| `permissions.resource` | 主體可以或無法存取的資產或物件。 資源可以是檔案、應用程式、伺服器或甚至API。 |
| `permissions.actions` | 允許主體對查詢的資源執行的操作。 可能的值包括： `view`, `read`, `create`, `edit`，和 `delete` |
