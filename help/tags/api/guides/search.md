---
title: 在Reactor API中搜尋資源
description: 了解如何在Reactor API中搜尋資源。
source-git-commit: 59592154eeb8592fa171b5488ecb0385e0e59f39
workflow-type: tm+mt
source-wordcount: '260'
ht-degree: 0%

---

# 在Reactor API中搜尋資源

Reactor API中的`/search`端點可讓您對儲存的資源進行結構化查詢。 本檔案針對各種常見使用案例提供不同搜尋查詢的範例。

>[!NOTE]
>
>閱讀本指南之前，請參閱[search endpoint guide](../endpoints/search.md) ，了解接受的查詢語法和其他使用指南。

## 基本查詢策略

下列範例示範使用API搜尋功能的一些基本概念。

### 跨多個欄位搜尋

在欄位名稱中使用萬用字元，即可在多個欄位間執行搜尋。 例如，要跨多個屬性欄位進行搜索，請使用`attributes.*`作為欄位名稱。

```json
{
  "data" : {
    "query": {
      "attributes.*": {
        "value": "evar7"
      }
    }
  }
}
```

>[!IMPORTANT]
>
>通常，搜尋值必須符合要搜尋的資料類型。 例如，針對整數欄位的查詢值`evar7`將會失敗。 在多個欄位間搜尋時，查詢類型要求會較寬，以避免錯誤，但可能會產生不適當的結果。

### 對特定資源類型的作用域查詢

您可以在請求中提供`resource_types`，將搜索範圍限定為特定資源類型。 例如，要跨`data_elements`和`rule_components`進行搜索：

```json
{
  "data" : {
    "from": 0,
    "size": 25,
    "query": {
      "attributes.display_name": {
        "value": "Performance"
      }
    },
    "resource_types": [
      "data_elements",
      "rule_components"
    ]
  }
}
```

### 排序回應

`sort`屬性可用於排序回應。 例如，若要依`created_at`排序，請以最新優先：

```json
{
  "data" : {
    "from": 0,
    "size": 25,
    "query": {
      "attributes.display_name": {
        "value": "Performance"
      }
    },
    "sort": [
      {
        "attributes.created_at": "desc"
      }
    ],
    "resource_types": [
      "data_elements",
      "rule_components"
    ]
  }
}
```

## 常見搜尋範例

下列範例示範其他常見的搜尋模式。

### 具有特定名稱的任何資源

```shell
curl -X POST \
  https://reactor.adobe.io/search \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1' \
  -d '{
        "data" : {
          "query": {
            "attributes.name": {
              "value": "Adobe"
            }
          }
        }
      }'
```

### 參考「evar7」的任何資源

```shell
curl -X POST \
  https://reactor.adobe.io/search \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1' \
  -d '{
        "data" : {
          "query": {
            "attributes.*": {
              "value": "evar7"
            }
          }
        }
      }'
```

### 「自訂程式碼」委派類型的資料元素

```shell
curl -X POST \
  https://reactor.adobe.io/search \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1' \
  -d '{
        "data" : {
          "query": {
            "attributes.delegate_descriptor_id": {
              "value": "custom-code"
            }
          },
          "resource_types": ["data_elements"]
        }
      }'
```

### 參考特定資料元素的規則元件

```shell
curl -X POST \
  https://reactor.adobe.io/search \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1' \
  -d '{
        "data" : {
          "query": {
            "attributes.settings": {
              "value": "myDataElement8"
            }
          },
          "resource_types": ["rule_components"]
        }
      }'
```

### 特定屬性中的規則

```shell
curl -X POST \
  https://reactor.adobe.io/search \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1' \
  -d '{
        "data" : {
          "query": {
            "relationships.property.data.id": {
              "value": "PR3cab070a9eb3423894e4a3038ef0e7b7"
            }
          },
          "resource_types": ["rules"]
        }
      }'
```

### 依ID尋找資源

```shell
curl -X POST \
  https://reactor.adobe.io/search \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1' \
  -d '{
        "data" : {
          "query": {
            "id": {
              "value": "PR3cab070a9eb3423894e4a3038ef0e7b7"
            }
          }
        }
      }'
```

### 使用&quot;OR&quot;詞語邏輯執行搜尋

```shell
curl -X POST \
  https://reactor.adobe.io/search \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1' \
  -d '{
        "data" : {
          "query": {
            "attributes.display_name": {
              "value": "My Rule Holiday Sale",
              "value_operator: "OR"
            }
          }
        }
      }'
```
