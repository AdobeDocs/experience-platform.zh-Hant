---
keywords: Experience Platform；首頁；熱門主題；API；屬性型存取控制；屬性型存取控制
solution: Experience Platform
title: 產品API端點
description: 以屬性為基礎的存取控制API中的/products端點可讓您以程式設計方式管理Adobe Experience Platform中的產品。
role: Developer
exl-id: 44ee9a9d-7a13-4d59-a1a9-97764dbd3763
source-git-commit: fded2f25f76e396cd49702431fa40e8e4521ebf8
workflow-type: tm+mt
source-wordcount: '514'
ht-degree: 3%

---

# 產品端點

>[!NOTE]
>
>如果傳遞的是使用者權杖，則權杖的使用者必須具有請求組織的「組織管理員」角色。

以屬性為基礎的存取控制API中的`/products`端點可讓您以程式設計方式管理產品，以及與您組織中的產品相關聯的許可權類別和許可權集。

## 快速入門

本指南中使用的API端點屬於屬性型存取控制API的一部分。 在繼續之前，請先檢閱[快速入門手冊](./getting-started.md)，以取得相關檔案的連結、閱讀本檔案中範例API呼叫的手冊，以及有關成功呼叫任何Experience Platform API所需必要標題的重要資訊。

## 擷取已授權產品的清單 {#list}

您可以向`/products`端點發出GET要求，以擷取已授權產品的清單。

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
| `name` | 查詢產品的名稱。 |
| `serviceCode` | 查詢產品的對應服務代碼。 |

## 依產品ID查詢許可權類別

您可以在指定產品ID時，向`/products/{PRODUCT_ID}/categories`端點發出GET要求，藉此查詢指定產品的許可權類別。

**API格式**

```http
GET /products/{PRODUCT_ID}/categories
```

| 參數 | 說明 |
| --- | --- |
| {PRODUCT_ID} | 與您要查閱的許可權類別相關聯的產品識別碼。 |

**要求**

下列要求會擷取與`{PRODUCT_ID}`關聯的許可權類別。

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/access-control/administration/products/{PRODUCT_ID}/categories \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
```

**回應**

成功的回應會傳回與您查詢的產品ID相關聯的許可權類別。

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
| `category` | 查詢的產品ID中可用的許可權類別。 |
| `name` | 許可權類別的名稱。 |

## 依產品ID查詢許可權集

您可以在指定產品ID時，向`/products/{PRODUCT_ID}/permission-sets`端點發出GET要求，藉此查詢指定產品的許可權集。

**API格式**

```http
GET /products/{PRODUCT_ID}/permission-sets
```

| 參數 | 說明 |
| --- | --- |
| {PRODUCT_ID} | 與您要查閱的許可權集相關聯的產品識別碼。 |

**要求**

下列要求會擷取與`{PRODUCT_ID}`關聯的許可權集。

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/access-control/administration/products/{PRODUCT_ID}/permission-sets \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
```

**回應**

成功的回應會傳回與您查詢的產品ID相關聯的許可權集。

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
| `permission-sets` | 許可權集代表管理員可套用至角色的一組許可權。 管理員可以將許可權集指派給角色，而不是指派個別許可權。 這可讓您從包含一組許可權的預定義角色建立自訂角色。 |
| `id` | 查詢許可權集的對應ID。 |
| `name` | 查詢許可權集的對應名稱。 |
| `category` | 可用的許可權類別。 |
| `permissions` | 許可權包括檢視和/或使用Experience Platform功能，例如建立沙箱、定義結構以及管理資料集的能力。 |
| `permissions.resource` | 主體可以或無法存取的資產或物件。 資源可以是檔案、應用程式、伺服器或甚至API。 |
| `permissions.actions` | 允許主體對查詢的資源執行的動作。 可能的值包括： `view`、`read`、`create`、`edit`和`delete` |
