---
title: 回呼端點
description: 了解如何在Reactor API中呼叫/callbacks端點。
exl-id: dd980f91-89e3-4ba0-a6fc-64d66b288a22
source-git-commit: 7f3b9ef9270b7748bc3366c8c39f503e1aee2100
workflow-type: tm+mt
source-wordcount: '600'
ht-degree: 5%

---

# 回呼端點

回呼是Reactor API傳送至特定URL（通常是由您的組織托管的URL）的訊息。

回呼可與 [稽核事件](./audit-events.md) 來追蹤Reactor API中的活動。 每次產生特定類型的稽核事件時，回呼都可傳送相符訊息至指定的URL。

回撥中指定之URL後面的服務必須以HTTP狀態代碼200(OK)或201（已建立）回應。 如果服務未以下列任一狀態代碼回應，則會依下列時間間隔重試訊息傳送：

* 1分鐘
* 5 分鐘
* 30 分鐘
* 1 小時
* 12 小時
* 1 天
* 3 天

>[!NOTE]
>
>重試間隔是與前一個間隔相對的。 例如，如果一分鐘內的重試失敗，則在一分鐘的嘗試失敗後（產生訊息後六分鐘），將下次嘗試排程五分鐘。

如果所有傳送嘗試均失敗，則會捨棄訊息。

回呼只屬於一個 [屬性](./properties.md). 屬性可以有許多回呼。

## 快速入門

本指南中使用的端點屬於 [Reactor API](https://www.adobe.io/experience-platform-apis/references/reactor/). 繼續之前，請檢閱 [快速入門手冊](../getting-started.md) 以取得如何驗證API的重要資訊。

## 清單回呼 {#list}

您可以透過提出GET要求，列出屬性下的所有回呼。

**API格式**

```http
GET  /properties/{PROPERTY_ID}/callbacks
```

| 參數 | 說明 |
| --- | --- |
| `{PROPERTY_ID}` | 此 `id` 屬性的，您要列出其回呼。 |

{style="table-layout:auto"}

>[!NOTE]
>
>您可以使用查詢參數，根據下列屬性來篩選列出的回呼：<ul><li>`created_at`</li><li>`updated_at`</li></ul>請參閱 [篩選回應](../guides/filtering.md) 以取得更多資訊。

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

成功的響應返回指定屬性的回呼清單。

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

您可以在要求的路徑中提供回呼的ID，以查詢GET。

**API格式**

```http
GET /callbacks/{CALLBACK_ID}
```

| 參數 | 說明 |
| --- | --- |
| `CALLBACK_ID` | 此 `id` 您要查詢的回呼。 |

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

成功的回應會傳回回回撥的詳細資訊。

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

## 建立回呼 {#create}

您可以提出POST要求，以建立新回呼。

**API格式**

```http
POST /properties/{PROPERTY_ID}/callbacks
```

| 參數 | 說明 |
| --- | --- |
| `PROPERTY_ID` | 此 `id` 的 [屬性](./properties.md) 定義回呼時所使用之URL區段。 |

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
| `url` | 回撥訊息的URL目的地。 URL必須使用HTTPS通訊協定擴充功能。 |
| `subscriptions` | 字串的陣列，指出將觸發回撥的稽核事件類型。 請參閱 [稽核事件端點指南](./audit-events.md) ，以取得可能的事件類型清單。 |

{style="table-layout:auto"}

**回應**

成功的回應會傳回新建立之回呼的詳細資料。

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

您可以在回呼要求的路徑中加入其ID，以更新回呼。

**API格式**

```http
PATCH /callbacks/{CALLBACK_ID}
```

| 參數 | 說明 |
| --- | --- |
| `CALLBACK_ID` | 此 `id` 的回呼。 |

{style="table-layout:auto"}

**要求**

下列請求會更新 `subscriptions` 陣列（適用於現有回呼）。

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
| `attributes` | 一個物件，其屬性代表要針對回撥更新的屬性。 每個索引鍵代表要更新的特定回呼屬性，以及應更新的對應值。<br><br>可針對回呼更新下列屬性：<ul><li>`subscriptions`</li><li>`url`</li></ul> |
| `id` | 此 `id` 的回呼。 這應符合 `{CALLBACK_ID}` 值。 |
| `type` | 要更新的資源類型。 對於此端點，值必須是 `callbacks`. |

{style="table-layout:auto"}

**回應**

成功的回應會傳回更新回呼的詳細資料。

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

## 刪除回呼

您可以在回呼請求的路徑中加入其ID，以刪除回呼。

**API格式**

```http
DELETE /callbacks/{CALLBACK_ID}
```

| 參數 | 說明 |
| --- | --- |
| `CALLBACK_ID` | 此 `id` 刪除的回呼。 |

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

成功的回應會傳回HTTP狀態204（無內容），但沒有回應內文，指出已刪除回呼。
