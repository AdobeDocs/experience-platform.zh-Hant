---
title: 規則端點
description: 瞭解如何在Reactor API中呼叫/rules端點。
exl-id: 79ef4389-e4b7-461e-8579-16a1a78cdd43
source-git-commit: b66a50e40aaac8df312a2c9a977fb8d4f1fb0c80
workflow-type: tm+mt
source-wordcount: '893'
ht-degree: 5%

---

# 規則端點

在資料收集標籤的內容中，規則會控制已部署程式庫中資源的行為。 規則是由一或多個[規則元件](./rule-components.md)組成，以邏輯方式將這些規則元件連結在一起。 Reactor API中的`/rules`端點可讓您以程式設計方式管理標籤規則。

>[!NOTE]
>
>本文介紹如何管理Reactor API中的規則。 如需有關如何與UI中的規則互動的資訊，請參閱[UI指南](../../ui/managing-resources/rules.md)。

規則只屬於一個[屬性](./properties.md)。 屬性可以有許多規則。

## 快速入門

此指南中使用的端點是[Reactor API](https://www.adobe.io/experience-platform-apis/references/reactor/)的一部分。 在繼續之前，請檢閱[快速入門手冊](../getting-started.md)，以取得有關如何向API驗證的重要資訊。

## 擷取規則清單 {#list}

您可以透過包含提出GET要求來擷取屬於某個屬性的規則清單。

**API格式**

```http
GET /properties/{PROPERTY_ID}/rules
```

| 參數 | 說明 |
| --- | --- |
| `PROPERTY_ID` | 您要列出其元件的屬性之`id`。 |

{style="table-layout:auto"}

>[!NOTE]
>
>使用查詢引數，可以根據以下屬性篩選列出的規則：<ul><li>`created_at`</li><li>`dirty`</li><li>`enabled`</li><li>`name`</li><li>`origin_id`</li><li>`published`</li><li>`published_at`</li><li>`revision_number`</li><li>`updated_at`</li></ul>如需詳細資訊，請參閱[篩選回應](../guides/filtering.md)的指南。

**要求**

```shell
curl -X GET \
  https://reactor.adobe.io/properties/PR41f64d2a9d9b4862b0582c5ff6a07504/rules \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**回應**

成功的回應會傳回指定屬性的規則清單。

```json
{
  "data": [
    {
      "id": "RL8429f3fee98b44c68f7a538e68e21747",
      "type": "rules",
      "attributes": {
        "created_at": "2020-12-14T17:56:44.109Z",
        "deleted_at": null,
        "dirty": true,
        "enabled": true,
        "name": "Example Rule",
        "published": false,
        "published_at": null,
        "revision_number": 0,
        "updated_at": "2020-12-14T17:56:44.109Z",
        "review_status": "unsubmitted"
      },
      "relationships": {
        "libraries": {
          "links": {
            "related": "https://reactor.adobe.io/rules/RL8429f3fee98b44c68f7a538e68e21747/libraries"
          }
        },
        "revisions": {
          "links": {
            "related": "https://reactor.adobe.io/rules/RL8429f3fee98b44c68f7a538e68e21747/revisions"
          }
        },
        "notes": {
          "links": {
            "related": "https://reactor.adobe.io/rules/RL8429f3fee98b44c68f7a538e68e21747/notes"
          }
        },
        "property": {
          "links": {
            "related": "https://reactor.adobe.io/rules/RL8429f3fee98b44c68f7a538e68e21747/property"
          },
          "data": {
            "id": "PR41f64d2a9d9b4862b0582c5ff6a07504",
            "type": "properties"
          }
        },
        "origin": {
          "links": {
            "related": "https://reactor.adobe.io/rules/RL8429f3fee98b44c68f7a538e68e21747/origin"
          },
          "data": {
            "id": "RL8429f3fee98b44c68f7a538e68e21747",
            "type": "rules"
          }
        },
        "rule_components": {
          "links": {
            "related": "https://reactor.adobe.io/rules/RL8429f3fee98b44c68f7a538e68e21747/rule_components"
          }
        }
      },
      "links": {
        "property": "https://reactor.adobe.io/properties/PR41f64d2a9d9b4862b0582c5ff6a07504",
        "origin": "https://reactor.adobe.io/rules/RL8429f3fee98b44c68f7a538e68e21747",
        "self": "https://reactor.adobe.io/rules/RL8429f3fee98b44c68f7a538e68e21747",
        "rule_components": "https://reactor.adobe.io/rules/RL8429f3fee98b44c68f7a538e68e21747/rule_components"
      },
      "meta": {
        "latest_revision_number": 0
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

## 查詢規則 {#lookup}

您可以在GET請求的路徑中提供規則ID以查詢規則。

>[!NOTE]
>
>刪除規則時，這些規則會標籤為已刪除，但實際上並不會從系統中移除。 因此，可以擷取已刪除的規則。 刪除的規則可由`meta.deleted_at`屬性的存在來識別。

**API格式**

```http
GET /rules/{RULE_ID}
```

| 參數 | 說明 |
| --- | --- |
| `RULE_ID` | 您要查閱之規則的`id`。 |

{style="table-layout:auto"}

**要求**

```shell
curl -X GET \
  https://reactor.adobe.io/rules/RL14dc6a8c37b14b619ddb2b3ba489a1f5 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**回應**

成功的回應會傳回規則的詳細資料。

```json
{
  "data": {
    "id": "RL14dc6a8c37b14b619ddb2b3ba489a1f5",
    "type": "rules",
    "attributes": {
      "created_at": "2020-12-14T17:56:33.188Z",
      "deleted_at": null,
      "dirty": true,
      "enabled": true,
      "name": "Example Rule",
      "published": false,
      "published_at": null,
      "revision_number": 0,
      "updated_at": "2020-12-14T17:56:33.188Z",
      "review_status": "unsubmitted"
    },
    "relationships": {
      "libraries": {
        "links": {
          "related": "https://reactor.adobe.io/rules/RL14dc6a8c37b14b619ddb2b3ba489a1f5/libraries"
        }
      },
      "revisions": {
        "links": {
          "related": "https://reactor.adobe.io/rules/RL14dc6a8c37b14b619ddb2b3ba489a1f5/revisions"
        }
      },
      "notes": {
        "links": {
          "related": "https://reactor.adobe.io/rules/RL14dc6a8c37b14b619ddb2b3ba489a1f5/notes"
        }
      },
      "property": {
        "links": {
          "related": "https://reactor.adobe.io/rules/RL14dc6a8c37b14b619ddb2b3ba489a1f5/property"
        },
        "data": {
          "id": "PRfa164e39b0d74eb5b093ab963b1f1200",
          "type": "properties"
        }
      },
      "origin": {
        "links": {
          "related": "https://reactor.adobe.io/rules/RL14dc6a8c37b14b619ddb2b3ba489a1f5/origin"
        },
        "data": {
          "id": "RL14dc6a8c37b14b619ddb2b3ba489a1f5",
          "type": "rules"
        }
      },
      "rule_components": {
        "links": {
          "related": "https://reactor.adobe.io/rules/RL14dc6a8c37b14b619ddb2b3ba489a1f5/rule_components"
        }
      }
    },
    "links": {
      "property": "https://reactor.adobe.io/properties/PRfa164e39b0d74eb5b093ab963b1f1200",
      "origin": "https://reactor.adobe.io/rules/RL14dc6a8c37b14b619ddb2b3ba489a1f5",
      "self": "https://reactor.adobe.io/rules/RL14dc6a8c37b14b619ddb2b3ba489a1f5",
      "rule_components": "https://reactor.adobe.io/rules/RL14dc6a8c37b14b619ddb2b3ba489a1f5/rule_components"
    },
    "meta": {
      "latest_revision_number": 0
    }
  }
}
```

## 建立規則 {#create}

您可以發出POST要求來建立新規則。

**API格式**

```http
POST /properties/{PROPERTY_ID}/rules
```

| 參數 | 說明 |
| --- | --- |
| `PROPERTY_ID` | 您正在定義規則之屬性的`id`。 |

{style="table-layout:auto"}

**要求**

```shell
curl -X POST \
  https://reactor.adobe.io/properties/PR03cc61073ef74fd2af21e4cfb6ed97a7/rules \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Content-Type: application/json' \
  -d '{
        "data": {
          "attributes": {
            "name": "Example Rule",
            "enabled": true,
          },
          "type": "rules"
        }
      }'
```

| 屬性 | 說明 |
| --- | --- |
| `attributes.name` | **（必要）**&#x200B;規則的可讀取名稱。 |
| `attributes.enabled` | 表示規則是否已啟用的布林值。 |
| `type` | 正在建立的資源型別。 此端點的值必須是`rules`。 |

{style="table-layout:auto"}

**回應**

成功的回應會傳回新建立規則的詳細資料。

```json
{
  "data": {
    "id": "RL52d156a9074844b89ca20c987dbafd3b",
    "type": "rules",
    "attributes": {
      "created_at": "2020-12-14T17:31:46.883Z",
      "deleted_at": null,
      "dirty": true,
      "enabled": true,
      "name": "Example Rule",
      "published": false,
      "published_at": null,
      "revision_number": 0,
      "updated_at": "2020-12-14T17:31:46.883Z",
      "review_status": "unsubmitted"
    },
    "relationships": {
      "libraries": {
        "links": {
          "related": "https://reactor.adobe.io/rules/RL52d156a9074844b89ca20c987dbafd3b/libraries"
        }
      },
      "revisions": {
        "links": {
          "related": "https://reactor.adobe.io/rules/RL52d156a9074844b89ca20c987dbafd3b/revisions"
        }
      },
      "notes": {
        "links": {
          "related": "https://reactor.adobe.io/rules/RL52d156a9074844b89ca20c987dbafd3b/notes"
        }
      },
      "property": {
        "links": {
          "related": "https://reactor.adobe.io/rules/RL52d156a9074844b89ca20c987dbafd3b/property"
        },
        "data": {
          "id": "PR03cc61073ef74fd2af21e4cfb6ed97a7",
          "type": "properties"
        }
      },
      "origin": {
        "links": {
          "related": "https://reactor.adobe.io/rules/RL52d156a9074844b89ca20c987dbafd3b/origin"
        },
        "data": {
          "id": "RL52d156a9074844b89ca20c987dbafd3b",
          "type": "rules"
        }
      },
      "rule_components": {
        "links": {
          "related": "https://reactor.adobe.io/rules/RL52d156a9074844b89ca20c987dbafd3b/rule_components"
        }
      }
    },
    "links": {
      "property": "https://reactor.adobe.io/properties/PR03cc61073ef74fd2af21e4cfb6ed97a7",
      "origin": "https://reactor.adobe.io/rules/RL52d156a9074844b89ca20c987dbafd3b",
      "self": "https://reactor.adobe.io/rules/RL52d156a9074844b89ca20c987dbafd3b",
      "rule_components": "https://reactor.adobe.io/rules/RL52d156a9074844b89ca20c987dbafd3b/rule_components"
    },
    "meta": {
      "latest_revision_number": 0
    }
  }
}
```

## 將事件、條件和動作新增至規則 {#components}

建立規則[&#128279;](#create)之後，您就可以新增事件、條件和動作（統稱為規則元件）來開始建立其邏輯。 請參閱`/rule_components`端點指南中有關[建立規則元件](./rule-components.md#create)的章節，以瞭解如何在Reactor API中執行此作業。

## 更新規則 {#update}

您可以在PATCH請求的路徑中包含規則的ID，以更新規則的屬性。

**API格式**

```http
PATCH /rules/{RULE_ID}
```

| 參數 | 說明 |
| --- | --- |
| `RULE_ID` | 您要更新的規則`id`。 |

{style="table-layout:auto"}

**要求**

下列要求會更新現有規則的`name`。

```shell
curl -X PATCH \
  https://reactor.adobe.io/rules/RLd2528a53c21a468f93cfd85244f16fdd \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Content-Type: application/json' \
  -d '{
  "data": {
    "attributes": {
      "name": "Test Rule"
    },
    "id": "RLd2528a53c21a468f93cfd85244f16fdd",
    "type": "rules"
  }
}'
```

| 屬性 | 說明 |
| --- | --- |
| `attributes` | 物件，其規則代表要針對規則更新的屬性。 您可以為規則更新下列屬性： <ul><li>`name`</li><li>`enabled`</li></ul> |
| `id` | 您要更新的規則`id`。 這應該符合請求路徑中提供的`{RULE_ID}`值。 |
| `type` | 正在更新的資源型別。 此端點的值必須是`rules`。 |

{style="table-layout:auto"}

**回應**

成功的回應會傳回已更新規則的詳細資料。

```json
{
  "data": {
    "id": "RLd2528a53c21a468f93cfd85244f16fdd",
    "type": "rules",
    "attributes": {
      "created_at": "2020-12-14T17:56:55.026Z",
      "deleted_at": null,
      "dirty": true,
      "enabled": true,
      "name": "Test Rule",
      "published": false,
      "published_at": null,
      "revision_number": 0,
      "updated_at": "2020-12-14T17:56:55.717Z",
      "review_status": "unsubmitted"
    },
    "relationships": {
      "libraries": {
        "links": {
          "related": "https://reactor.adobe.io/rules/RLd2528a53c21a468f93cfd85244f16fdd/libraries"
        }
      },
      "revisions": {
        "links": {
          "related": "https://reactor.adobe.io/rules/RLd2528a53c21a468f93cfd85244f16fdd/revisions"
        }
      },
      "notes": {
        "links": {
          "related": "https://reactor.adobe.io/rules/RLd2528a53c21a468f93cfd85244f16fdd/notes"
        }
      },
      "property": {
        "links": {
          "related": "https://reactor.adobe.io/rules/RLd2528a53c21a468f93cfd85244f16fdd/property"
        },
        "data": {
          "id": "PR7e37a33354cc4aa7880f2a550c4f844f",
          "type": "properties"
        }
      },
      "origin": {
        "links": {
          "related": "https://reactor.adobe.io/rules/RLd2528a53c21a468f93cfd85244f16fdd/origin"
        },
        "data": {
          "id": "RLd2528a53c21a468f93cfd85244f16fdd",
          "type": "rules"
        }
      },
      "rule_components": {
        "links": {
          "related": "https://reactor.adobe.io/rules/RLd2528a53c21a468f93cfd85244f16fdd/rule_components"
        }
      }
    },
    "links": {
      "property": "https://reactor.adobe.io/properties/PR7e37a33354cc4aa7880f2a550c4f844f",
      "origin": "https://reactor.adobe.io/rules/RLd2528a53c21a468f93cfd85244f16fdd",
      "self": "https://reactor.adobe.io/rules/RLd2528a53c21a468f93cfd85244f16fdd",
      "rule_components": "https://reactor.adobe.io/rules/RLd2528a53c21a468f93cfd85244f16fdd/rule_components"
    },
    "meta": {
      "latest_revision_number": 0
    }
  }
}
```

## 刪除規則

您可以在DELETE請求的路徑中包含規則ID以刪除規則。

**API格式**

```http
DELETE /rules/{RULE_ID}
```

| 參數 | 說明 |
| --- | --- |
| `RULE_ID` | 您要刪除之規則的`id`。 |

{style="table-layout:auto"}

**要求**

```shell
curl -X DELETE \
  https://reactor.adobe.io/rules/RLd2528a53c21a468f93cfd85244f16fdd \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}'
```

**回應**

成功的回應會傳回HTTP狀態204 （無內容），沒有回應內文，表示規則已刪除。

## 管理規則的附註 {#notes}

規則是「重要」資源，這表示您可以在每個個別資源上建立和擷取文字型附註。 如需有關如何管理規則和其他相容資源的附註的詳細資訊，請參閱[附註端點指南](./notes.md)。

## 擷取規則的相關資源 {#related}

下列呼叫示範如何擷取規則的相關資源。 當[查詢規則](#lookup)時，這些關係會列在`relationships`規則下。

請參閱[關係指南](../guides/relationships.md)，以取得有關Reactor API中關係的詳細資訊。

### 列出規則的相關程式庫 {#libraries}

您可以將`/libraries`附加至查閱要求的路徑，以列出使用特定規則的資料庫。

**API格式**

```http
GET  /rules/{RULE_ID}/libraries
```

| 參數 | 說明 |
| --- | --- |
| `{RULE_ID}` | 您要列出其程式庫的規則`id`。 |

{style="table-layout:auto"}

**要求**

```shell
curl -X GET \
  https://reactor.adobe.io/rules/RLd2528a53c21a468f93cfd85244f16fdd/libraries \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**回應**

成功的回應會傳回使用指定規則的程式庫清單。

```json
{
  "data": [
    {
      "id": "LB62d20ad807a949e6b13b0a2c7299eb65",
      "type": "libraries",
      "attributes": {
        "created_at": "2020-12-14T17:50:19.589Z",
        "name": "My Library",
        "published_at": null,
        "state": "development",
        "updated_at": "2020-12-14T17:50:19.589Z",
        "build_required": true
      },
      "relationships": {
        "builds": {
          "links": {
            "related": "https://reactor.adobe.io/libraries/LB62d20ad807a949e6b13b0a2c7299eb65/builds"
          }
        },
        "environment": {
          "links": {
            "self": "https://reactor.adobe.io/libraries/LB62d20ad807a949e6b13b0a2c7299eb65/relationships/environment"
          },
          "data": null
        },
        "data_elements": {
          "links": {
            "related": "https://reactor.adobe.io/libraries/LB62d20ad807a949e6b13b0a2c7299eb65/data_elements",
            "self": "https://reactor.adobe.io/libraries/LB62d20ad807a949e6b13b0a2c7299eb65/relationships/data_elements"
          }
        },
        "extensions": {
          "links": {
            "related": "https://reactor.adobe.io/libraries/LB62d20ad807a949e6b13b0a2c7299eb65/extensions",
            "self": "https://reactor.adobe.io/libraries/LB62d20ad807a949e6b13b0a2c7299eb65/relationships/extensions"
          }
        },
        "notes": {
          "links": {
            "related": "https://reactor.adobe.io/libraries/LB62d20ad807a949e6b13b0a2c7299eb65/notes"
          }
        },
        "rules": {
          "links": {
            "related": "https://reactor.adobe.io/libraries/LB62d20ad807a949e6b13b0a2c7299eb65/rules",
            "self": "https://reactor.adobe.io/libraries/LB62d20ad807a949e6b13b0a2c7299eb65/relationships/rules"
          }
        },
        "upstream_library": {
          "data": null
        },
        "property": {
          "links": {
            "related": "https://reactor.adobe.io/libraries/LB62d20ad807a949e6b13b0a2c7299eb65/property"
          },
          "data": {
            "id": "PR241ba9cd56324ac192de68d658f20cb0",
            "type": "properties"
          }
        },
        "last_build": {
          "links": {
            "related": "https://reactor.adobe.io/libraries/LB62d20ad807a949e6b13b0a2c7299eb65/last_build"
          },
          "data": null
        }
      },
      "links": {
        "property": "https://reactor.adobe.io/properties/PR241ba9cd56324ac192de68d658f20cb0",
        "self": "https://reactor.adobe.io/libraries/LB62d20ad807a949e6b13b0a2c7299eb65"
      },
      "meta": {
        "build_status": null,
        "build_required_detail": "No build found since last state change"
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

### 列出規則的相關修訂版本 {#revisions}

您可以將`/revisions`附加至查閱要求的路徑，以列出規則的修訂版本。

**API格式**

```http
GET  /rules/{RULE_ID}/revisions
```

| 參數 | 說明 |
| --- | --- |
| `{RULE_ID}` | 您要列出其修訂版本的規則的`id`。 |

{style="table-layout:auto"}

**要求**

```shell
curl -X GET \
  https://reactor.adobe.io/rules/RL67de76e5bff9413aa8ad14e55172d8dc/revisions \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**回應**

成功的回應會傳回使用指定規則的修訂清單。

```json
{
  "data": [
    {
      "id": "RL67de76e5bff9413aa8ad14e55172d8dc",
      "type": "rules",
      "attributes": {
        "created_at": "2020-12-14T17:57:29.835Z",
        "deleted_at": null,
        "dirty": false,
        "enabled": true,
        "name": "Example Rule",
        "published": false,
        "published_at": null,
        "revision_number": 0,
        "updated_at": "2020-12-14T17:57:29.835Z",
        "review_status": "unsubmitted"
      },
      "relationships": {
        "libraries": {
          "links": {
            "related": "https://reactor.adobe.io/rules/RL67de76e5bff9413aa8ad14e55172d8dc/libraries"
          }
        },
        "revisions": {
          "links": {
            "related": "https://reactor.adobe.io/rules/RL67de76e5bff9413aa8ad14e55172d8dc/revisions"
          }
        },
        "notes": {
          "links": {
            "related": "https://reactor.adobe.io/rules/RL67de76e5bff9413aa8ad14e55172d8dc/notes"
          }
        },
        "property": {
          "links": {
            "related": "https://reactor.adobe.io/rules/RL67de76e5bff9413aa8ad14e55172d8dc/property"
          },
          "data": {
            "id": "PR391208e5ea96442ea7903fe3f33f50e7",
            "type": "properties"
          }
        },
        "origin": {
          "links": {
            "related": "https://reactor.adobe.io/rules/RL67de76e5bff9413aa8ad14e55172d8dc/origin"
          },
          "data": {
            "id": "RL67de76e5bff9413aa8ad14e55172d8dc",
            "type": "rules"
          }
        },
        "rule_components": {
          "links": {
            "related": "https://reactor.adobe.io/rules/RL67de76e5bff9413aa8ad14e55172d8dc/rule_components"
          }
        }
      },
      "links": {
        "property": "https://reactor.adobe.io/properties/PR391208e5ea96442ea7903fe3f33f50e7",
        "origin": "https://reactor.adobe.io/rules/RL67de76e5bff9413aa8ad14e55172d8dc",
        "self": "https://reactor.adobe.io/rules/RL67de76e5bff9413aa8ad14e55172d8dc",
        "rule_components": "https://reactor.adobe.io/rules/RL67de76e5bff9413aa8ad14e55172d8dc/rule_components"
      },
      "meta": {
        "latest_revision_number": 1
      }
    },
    {
      "id": "RL6e5cb0d1c74542d6a3d04d08c6bb97ae",
      "type": "rules",
      "attributes": {
        "created_at": "2020-12-14T17:57:30.528Z",
        "deleted_at": null,
        "dirty": false,
        "enabled": true,
        "name": "Example Rule",
        "published": false,
        "published_at": null,
        "revision_number": 1,
        "updated_at": "2020-12-14T17:57:30.528Z",
        "review_status": "unsubmitted"
      },
      "relationships": {
        "libraries": {
          "links": {
            "related": "https://reactor.adobe.io/rules/RL6e5cb0d1c74542d6a3d04d08c6bb97ae/libraries"
          }
        },
        "revisions": {
          "links": {
            "related": "https://reactor.adobe.io/rules/RL6e5cb0d1c74542d6a3d04d08c6bb97ae/revisions"
          }
        },
        "notes": {
          "links": {
            "related": "https://reactor.adobe.io/rules/RL6e5cb0d1c74542d6a3d04d08c6bb97ae/notes"
          }
        },
        "property": {
          "links": {
            "related": "https://reactor.adobe.io/rules/RL6e5cb0d1c74542d6a3d04d08c6bb97ae/property"
          },
          "data": {
            "id": "PR391208e5ea96442ea7903fe3f33f50e7",
            "type": "properties"
          }
        },
        "origin": {
          "links": {
            "related": "https://reactor.adobe.io/rules/RL6e5cb0d1c74542d6a3d04d08c6bb97ae/origin"
          },
          "data": {
            "id": "RL67de76e5bff9413aa8ad14e55172d8dc",
            "type": "rules"
          }
        },
        "rule_components": {
          "links": {
            "related": "https://reactor.adobe.io/rules/RL6e5cb0d1c74542d6a3d04d08c6bb97ae/rule_components"
          }
        }
      },
      "links": {
        "property": "https://reactor.adobe.io/properties/PR391208e5ea96442ea7903fe3f33f50e7",
        "origin": "https://reactor.adobe.io/rules/RL67de76e5bff9413aa8ad14e55172d8dc",
        "self": "https://reactor.adobe.io/rules/RL6e5cb0d1c74542d6a3d04d08c6bb97ae",
        "rule_components": "https://reactor.adobe.io/rules/RL6e5cb0d1c74542d6a3d04d08c6bb97ae/rule_components"
      },
      "meta": {
        "latest_revision_number": 1
      }
    }
  ],
  "meta": {
    "pagination": {
      "current_page": 1,
      "next_page": null,
      "prev_page": null,
      "total_pages": 1,
      "total_count": 2
    }
  }
}
```

### 查詢規則的相關來源 {#origin}

您可以將`/origin`附加至查閱要求的路徑，以查閱規則的來源（舊版）。

**API格式**

```http
GET /rules/{RULE_ID}/origin
```

| 參數 | 說明 |
| --- | --- |
| `{RULE_ID}` | 您要查詢其來源的規則的`id`。 |

{style="table-layout:auto"}

**要求**

```shell
curl -X GET \
  https://reactor.adobe.io/rules/RLb83ed2278dc045628c069ab7eb9bb866/origin \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**回應**

成功的回應會傳回指定規則擴充功能的詳細資料。

```json
{
  "data": {
    "id": "RLb83ed2278dc045628c069ab7eb9bb866",
    "type": "rules",
    "attributes": {
      "created_at": "2020-12-14T17:57:41.517Z",
      "deleted_at": null,
      "dirty": false,
      "enabled": true,
      "name": "Example Rule",
      "published": false,
      "published_at": null,
      "revision_number": 0,
      "updated_at": "2020-12-14T17:57:41.517Z",
      "review_status": "unsubmitted"
    },
    "relationships": {
      "libraries": {
        "links": {
          "related": "https://reactor.adobe.io/rules/RLb83ed2278dc045628c069ab7eb9bb866/libraries"
        }
      },
      "revisions": {
        "links": {
          "related": "https://reactor.adobe.io/rules/RLb83ed2278dc045628c069ab7eb9bb866/revisions"
        }
      },
      "notes": {
        "links": {
          "related": "https://reactor.adobe.io/rules/RLb83ed2278dc045628c069ab7eb9bb866/notes"
        }
      },
      "property": {
        "links": {
          "related": "https://reactor.adobe.io/rules/RLb83ed2278dc045628c069ab7eb9bb866/property"
        },
        "data": {
          "id": "PR169d832d20ea4243b5a5db0ccc5aae9c",
          "type": "properties"
        }
      },
      "origin": {
        "links": {
          "related": "https://reactor.adobe.io/rules/RLb83ed2278dc045628c069ab7eb9bb866/origin"
        },
        "data": {
          "id": "RLb83ed2278dc045628c069ab7eb9bb866",
          "type": "rules"
        }
      },
      "rule_components": {
        "links": {
          "related": "https://reactor.adobe.io/rules/RLb83ed2278dc045628c069ab7eb9bb866/rule_components"
        }
      }
    },
    "links": {
      "property": "https://reactor.adobe.io/properties/PR169d832d20ea4243b5a5db0ccc5aae9c",
      "origin": "https://reactor.adobe.io/rules/RLb83ed2278dc045628c069ab7eb9bb866",
      "self": "https://reactor.adobe.io/rules/RLb83ed2278dc045628c069ab7eb9bb866",
      "rule_components": "https://reactor.adobe.io/rules/RLb83ed2278dc045628c069ab7eb9bb866/rule_components"
    },
    "meta": {
      "latest_revision_number": 1
    }
  }
}
```

### 查詢規則的相關屬性 {#property}

您可以將`/property`附加至查閱要求的路徑，以查閱擁有規則的屬性。

**API格式**

```http
GET /rules/{RULE_ID}/property
```

| 參數 | 說明 |
| --- | --- |
| `{RULE_ID}` | 您要查詢其屬性的規則`id`。 |

{style="table-layout:auto"}

**要求**

```shell
curl -X GET \
  https://reactor.adobe.io/rules/RC3d0805fde85d42db8988090bc074bb44/property \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**回應**

成功的回應會傳回指定規則屬性的詳細資料。

```json
{
  "data": {
    "id": "PR8ac25b57d5c24ebab68ffe5c630fc690",
    "type": "properties",
    "attributes": {
      "created_at": "2020-12-14T17:53:19.088Z",
      "enabled": true,
      "name": "Kessel Example Property",
      "updated_at": "2020-12-14T17:53:19.088Z",
      "platform": "web",
      "development": false,
      "token": "97b2cb1177df",
      "domains": [
        "example.com"
      ],
      "undefined_vars_return_empty": false,
      "rule_component_sequencing_enabled": false
    },
    "relationships": {
      "company": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR8ac25b57d5c24ebab68ffe5c630fc690/company"
        },
        "data": {
          "id": "CO2bf094214ffd4785bb4bcf88c952a7c1",
          "type": "companies"
        }
      },
      "callbacks": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR8ac25b57d5c24ebab68ffe5c630fc690/callbacks"
        }
      },
      "hosts": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR8ac25b57d5c24ebab68ffe5c630fc690/hosts"
        }
      },
      "environments": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR8ac25b57d5c24ebab68ffe5c630fc690/environments"
        }
      },
      "libraries": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR8ac25b57d5c24ebab68ffe5c630fc690/libraries"
        }
      },
      "data_elements": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR8ac25b57d5c24ebab68ffe5c630fc690/data_elements"
        }
      },
      "extensions": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR8ac25b57d5c24ebab68ffe5c630fc690/extensions"
        }
      },
      "rules": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR8ac25b57d5c24ebab68ffe5c630fc690/rules"
        }
      },
      "notes": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR8ac25b57d5c24ebab68ffe5c630fc690/notes"
        }
      }
    },
    "links": {
      "company": "https://reactor.adobe.io/companies/CO2bf094214ffd4785bb4bcf88c952a7c1",
      "data_elements": "https://reactor.adobe.io/properties/PR8ac25b57d5c24ebab68ffe5c630fc690/data_elements",
      "environments": "https://reactor.adobe.io/properties/PR8ac25b57d5c24ebab68ffe5c630fc690/environments",
      "extensions": "https://reactor.adobe.io/properties/PR8ac25b57d5c24ebab68ffe5c630fc690/extensions",
      "rules": "https://reactor.adobe.io/properties/PR8ac25b57d5c24ebab68ffe5c630fc690/rules",
      "self": "https://reactor.adobe.io/properties/PR8ac25b57d5c24ebab68ffe5c630fc690"
    },
    "meta": {
      "rights": [
        "approve",
        "develop",
        "manage_environments",
        "manage_extensions",
        "publish"
      ]
    }
  }
}
```
