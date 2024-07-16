---
title: 回呼端點
description: 瞭解如何在Reactor API中呼叫/callbacks端點。
exl-id: dd980f91-89e3-4ba0-a6fc-64d66b288a22
source-git-commit: 7f3b9ef9270b7748bc3366c8c39f503e1aee2100
workflow-type: tm+mt
source-wordcount: '606'
ht-degree: 6%

---

# 回呼端點

回呼是Reactor API傳送至特定URL （通常是您的組織託管的網址）的訊息。

回呼旨在與[稽核事件](./audit-events.md)搭配使用，以追蹤Reactor API中的活動。 每次產生特定型別的稽核事件時，回呼都會傳送符合訊息至指定的URL。

在回撥中指定的URL之後的服務必須以HTTP狀態碼200 （確定）或201 （已建立）回應。 如果服務未回應任一狀態代碼，則會依下列時間間隔重試訊息傳送：

* 1分鐘
* 5 分鐘
* 30 分鐘
* 1 小時
* 12 小時
* 1 天
* 3 天

>[!NOTE]
>
>重試間隔與上一個間隔有關。 例如，如果一分鐘重試失敗，則下次嘗試會排程在1分鐘嘗試失敗後的5分鐘（產生訊息後的6分鐘）。

如果所有傳送嘗試均失敗，則會捨棄訊息。

回呼只屬於一個[屬性](./properties.md)。 屬性可以有許多回呼。

## 快速入門

此指南中使用的端點是[Reactor API](https://www.adobe.io/experience-platform-apis/references/reactor/)的一部分。 在繼續之前，請檢閱[快速入門手冊](../getting-started.md)，以取得有關如何向API驗證的重要資訊。

## 清單回呼 {#list}

您可以發出GET要求，列出屬性下的所有回呼。

**API格式**

```http
GET  /properties/{PROPERTY_ID}/callbacks
```

| 參數 | 說明 |
| --- | --- |
| `{PROPERTY_ID}` | 您要列出其回呼的屬性`id`。 |

{style="table-layout:auto"}

>[!NOTE]
>
>您可以使用查詢引數，根據下列屬性篩選列出的回呼：<ul><li>`created_at`</li><li>`updated_at`</li></ul>如需詳細資訊，請參閱[篩選回應](../guides/filtering.md)的指南。

**要求**

```shell
curl -X GET \
  https://reactor.adobe.io/properties/PR66a3356c73fc4aabb67ee22caae53d70/callbacks \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**回應**

成功的回應會傳回指定屬性的回呼清單。

```json
{
  "data": [
    {
      "id": "CB26edef8d709243579589107bcda034da",
      "type": "callbacks",
      "attributes": {
        "created_at": "2020-12-14T17:34:47.082Z",
        "subscriptions": [
          "rule.created"
        ],
        "updated_at": "2020-12-14T17:34:47.082Z",
        "url": "https://www.example.com"
      },
      "relationships": {
        "property": {
          "links": {
            "related": "https://reactor.adobe.io/callbacks/CB26edef8d709243579589107bcda034da/property"
          },
          "data": {
            "id": "PR66a3356c73fc4aabb67ee22caae53d70",
            "type": "properties"
          }
        }
      },
      "links": {
        "property": "https://reactor.adobe.io/properties/PR66a3356c73fc4aabb67ee22caae53d70",
        "self": "https://reactor.adobe.io/callbacks/CB26edef8d709243579589107bcda034da"
      }
    }
  ],
  "meta": {
    "pagination": {
      "current_page": 1,
      "next_page": null,
      "prev_page": null,
      "total_pages": 1,
      "total_count": 1
    }
  }
}
```

## 查詢回呼 {#lookup}

您可以在GET請求的路徑中提供回呼的ID以查詢它。

**API格式**

```http
GET /callbacks/{CALLBACK_ID}
```

| 參數 | 說明 |
| --- | --- |
| `CALLBACK_ID` | 您要查閱之回呼的`id`。 |

{style="table-layout:auto"}

**要求**

```shell
curl -X GET \
  https://reactor.adobe.io/callbacks/CBeef389cee8d84e69acef8665e4dcbef6 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**回應**

成功的回應會傳回回回撥的詳細資料。

```json
{
  "data": {
    "id": "CBeef389cee8d84e69acef8665e4dcbef6",
    "type": "callbacks",
    "attributes": {
      "created_at": "2020-12-14T17:34:36.872Z",
      "subscriptions": [
        "rule.created"
      ],
      "updated_at": "2020-12-14T17:34:36.872Z",
      "url": "https://www.example.com"
    },
    "relationships": {
      "property": {
        "links": {
          "related": "https://reactor.adobe.io/callbacks/CBeef389cee8d84e69acef8665e4dcbef6/property"
        },
        "data": {
          "id": "PRb513bbab52114573ac87f9848eea6ead",
          "type": "properties"
        }
      }
    },
    "links": {
      "property": "https://reactor.adobe.io/properties/PRb513bbab52114573ac87f9848eea6ead",
      "self": "https://reactor.adobe.io/callbacks/CBeef389cee8d84e69acef8665e4dcbef6"
    }
  }
}
```

## 建立回撥 {#create}

您可以發出POST要求來建立新的回呼。

**API格式**

```http
POST /properties/{PROPERTY_ID}/callbacks
```

| 參數 | 說明 |
| --- | --- |
| `PROPERTY_ID` | 您正在定義回呼的[屬性](./properties.md)的`id`。 |

{style="table-layout:auto"}

**要求**

```shell
curl -X POST \
  https://reactor.adobe.io/properties/PR5e22de986a7c4070965e7546b2bb108d/callbacks \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/vnd.api+json;revision=1' \
  -d '{
        "data": {
          "attributes": {
            "url": "https://www.example.com",
            "subscriptions": [
              "rule.created"
            ]
          }
        }
      }'
```

| 屬性 | 說明 |
| --- | --- |
| `url` | 回撥訊息的URL目的地。 URL必須使用HTTPS通訊協定副檔名。 |
| `subscriptions` | 字串陣列，指出將觸發回撥的稽核事件型別。 如需可能的事件型別清單，請參閱[稽核事件端點指南](./audit-events.md)。 |

{style="table-layout:auto"}

**回應**

成功的回應會傳回新建立回撥的詳細資料。

```json
{
  "data": {
    "id": "CB32d8f23d5ee548278d32076af4c442a0",
    "type": "callbacks",
    "attributes": {
      "created_at": "2020-12-14T17:34:27.059Z",
      "subscriptions": [
        "rule.created"
      ],
      "updated_at": "2020-12-14T17:34:27.059Z",
      "url": "https://www.example.com"
    },
    "relationships": {
      "property": {
        "links": {
          "related": "https://reactor.adobe.io/callbacks/CB32d8f23d5ee548278d32076af4c442a0/property"
        },
        "data": {
          "id": "PR5e22de986a7c4070965e7546b2bb108d",
          "type": "properties"
        }
      }
    },
    "links": {
      "property": "https://reactor.adobe.io/properties/PR5e22de986a7c4070965e7546b2bb108d",
      "self": "https://reactor.adobe.io/callbacks/CB32d8f23d5ee548278d32076af4c442a0"
    }
  }
}
```

## 更新回呼

您可以在PATCH請求的路徑中包含回呼的ID以更新回呼。

**API格式**

```http
PATCH /callbacks/{CALLBACK_ID}
```

| 參數 | 說明 |
| --- | --- |
| `CALLBACK_ID` | 您要更新的回呼的`id`。 |

{style="table-layout:auto"}

**要求**

下列要求會更新現有回呼的`subscriptions`陣列。

```shell
curl -X PATCH \
  https://reactor.adobe.io/callbacks/CB4310904d415549888cc9e31ebe1e1e45 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/vnd.api+json;revision=1' \
  -d '{
        "data": {
          "attributes": {
            "url": "https://www.example.net",
            "subscriptions": [
              "rule.created",
              "build.created"
            ]
          },
          "type": "callbacks",
          "id": "CB4310904d415549888cc9e31ebe1e1e45"
        }
      }'
```

| 屬性 | 說明 |
| --- | --- |
| `attributes` | 物件，其屬性代表要針對回呼更新的屬性。 每個索引鍵代表要更新的特定回呼屬性，以及應更新到的對應值。<br><br>可以更新回呼的下列屬性：<ul><li>`subscriptions`</li><li>`url`</li></ul> |
| `id` | 您要更新的回呼`id`。 這應該符合請求路徑中提供的`{CALLBACK_ID}`值。 |
| `type` | 正在更新的資源型別。 此端點的值必須是`callbacks`。 |

{style="table-layout:auto"}

**回應**

成功的回應會傳回已更新回撥的詳細資料。

```json
{
  "data": {
    "id": "CB4310904d415549888cc9e31ebe1e1e45",
    "type": "callbacks",
    "attributes": {
      "created_at": "2020-12-14T17:34:56.884Z",
      "subscriptions": [
        "rule.created",
        "build.created"
      ],
      "updated_at": "2020-12-14T17:34:57.614Z",
      "url": "https://www.example.net"
    },
    "relationships": {
      "property": {
        "links": {
          "related": "https://reactor.adobe.io/callbacks/CB4310904d415549888cc9e31ebe1e1e45/property"
        },
        "data": {
          "id": "PR0a8ef3ca31dc456a8566e9288960bd79",
          "type": "properties"
        }
      }
    },
    "links": {
      "property": "https://reactor.adobe.io/properties/PR0a8ef3ca31dc456a8566e9288960bd79",
      "self": "https://reactor.adobe.io/callbacks/CB4310904d415549888cc9e31ebe1e1e45"
    }
  }
}
```

## 刪除回撥

您可以在DELETE請求的路徑中包含回呼ID以刪除回呼。

**API格式**

```http
DELETE /callbacks/{CALLBACK_ID}
```

| 參數 | 說明 |
| --- | --- |
| `CALLBACK_ID` | 您要刪除之回呼的`id`。 |

{style="table-layout:auto"}

**要求**

```shell
curl -X DELETE \
  https://reactor.adobe.io/callbacks/CB4310904d415549888cc9e31ebe1e1e45 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**回應**

成功的回應會傳回HTTP狀態204 （無內容），且沒有回應內文，這表示回呼已刪除。
