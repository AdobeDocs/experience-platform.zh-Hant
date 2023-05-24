---
title: 回調終結點
description: 瞭解如何調用Repartor API中的/callbacks端點。
exl-id: dd980f91-89e3-4ba0-a6fc-64d66b288a22
source-git-commit: 7f3b9ef9270b7748bc3366c8c39f503e1aee2100
workflow-type: tm+mt
source-wordcount: '600'
ht-degree: 5%

---

# 回調終結點

回調是Repartor API發送到特定URL（通常由您的組織承載）的消息。

回調將與 [審計事件](./audit-events.md) 跟蹤反應堆API中的活動。 每次生成某種類型的審計事件時，回調可以向指定URL發送匹配消息。

回調中指定的URL後面的服務必須以HTTP狀態代碼200(OK)或201（已建立）響應。 如果服務未使用以下任一狀態代碼響應，則按以下間隔重試消息傳遞：

* 1分鐘
* 5 分鐘
* 30 分鐘
* 1 小時
* 12 小時
* 1 天
* 3 天

>[!NOTE]
>
>重試間隔與上一間隔相對。 例如，如果一分鐘的重試失敗，則在一分鐘的嘗試失敗後（在生成消息後六分鐘）安排下一次嘗試五分鐘。

如果所有傳遞嘗試都未成功，則消息將被丟棄。

回叫正好屬於 [屬性](./properties.md)。 一個屬性可以有許多回調。

## 快速入門

本指南中使用的端點是 [反應堆API](https://www.adobe.io/experience-platform-apis/references/reactor/)。 在繼續之前，請查看 [入門指南](../getting-started.md) 有關如何驗證到API的重要資訊。

## 清單回調 {#list}

通過發出GET請求，可以列出屬性下的所有回調。

**API格式**

```http
GET  /properties/{PROPERTY_ID}/callbacks
```

| 參數 | 說明 |
| --- | --- |
| `{PROPERTY_ID}` | 的 `id` 的子目錄。 |

{style="table-layout:auto"}

>[!NOTE]
>
>使用查詢參數，可以根據以下屬性篩選列出的回調：<ul><li>`created_at`</li><li>`updated_at`</li></ul>請參閱上的指南 [過濾響應](../guides/filtering.md) 的子菜單。

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

成功的響應將返回指定屬性的回調清單。

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

## 查找回調 {#lookup}

您可以通過在GET請求的路徑中提供回調的ID來查找回調。

**API格式**

```http
GET /callbacks/{CALLBACK_ID}
```

| 參數 | 說明 |
| --- | --- |
| `CALLBACK_ID` | 的 `id` 你想查的回電。 |

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

成功的響應返回回調的詳細資訊。

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

## 建立回調 {#create}

可以通過發出POST請求建立新回調。

**API格式**

```http
POST /properties/{PROPERTY_ID}/callbacks
```

| 參數 | 說明 |
| --- | --- |
| `PROPERTY_ID` | 的 `id` 的 [屬性](./properties.md) 定義回叫。 |

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
| `url` | 回調消息的URL目標。 URL必須使用HTTPS協定擴展。 |
| `subscriptions` | 字串陣列，指示將觸發回調的審計事件類型。 查看 [審計事件終結點指南](./audit-events.md) 清單。 |

{style="table-layout:auto"}

**回應**

成功的響應將返回新建立的回調的詳細資訊。

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

## 更新回調

可以通過在回調請求的路徑中包含回調的ID來更新回調。

**API格式**

```http
PATCH /callbacks/{CALLBACK_ID}
```

| 參數 | 說明 |
| --- | --- |
| `CALLBACK_ID` | 的 `id` 要更新的回調。 |

{style="table-layout:auto"}

**要求**

以下請求更新 `subscriptions` 用於現有回調的陣列。

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
| `attributes` | 其屬性表示要為回調更新的屬性的對象。 每個鍵都表示要更新的特定回調屬性以及應更新到的相應值。<br><br>可以更新以下屬性以進行回調：<ul><li>`subscriptions`</li><li>`url`</li></ul> |
| `id` | 的 `id` 要更新的回調。 這應與 `{CALLBACK_ID}` 請求路徑中提供的值。 |
| `type` | 要更新的資源類型。 對於此終結點，值必須為 `callbacks`。 |

{style="table-layout:auto"}

**回應**

成功的響應返回更新的回調的詳細資訊。

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

## 刪除回調

通過將回調ID包含在DELETE請求的路徑中，可以刪除它。

**API格式**

```http
DELETE /callbacks/{CALLBACK_ID}
```

| 參數 | 說明 |
| --- | --- |
| `CALLBACK_ID` | 的 `id` 刪除的回調。 |

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

成功的響應返回HTTP狀態204（無內容），沒有響應正文，表示回調已被刪除。
