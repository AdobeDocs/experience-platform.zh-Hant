---
title: 組建端點
description: 了解如何在Reactor API中呼叫/builds端點。
source-git-commit: 8133804076b1c0adf2eae5b748e86a35f3186d14
workflow-type: tm+mt
source-wordcount: '833'
ht-degree: 8%

---

# 組建端點

擴充功能、規則和資料元素是Adobe Experience Platform中標籤的基礎要素。 當您想讓應用程式執行某項作業時，這些建置區塊會新增至[library](./libraries.md)。 若要在您的體驗應用程式上部署程式庫，程式庫會編譯到組建中。 Reactor API中的`/builds`端點可讓您以程式設計方式管理體驗應用程式中的組建。

組建是在網頁和行動應用程式中載入的實際檔案（或檔案）。 每個組建的內容會因下列因素而異：

* 程式庫中包含的資源
* 建置程式庫所在的[environment](./environments.md)的配置
* 組建所屬[屬性](./properties.md)的平台

組建只屬於一個程式庫。 程式庫可以有許多組建。

如需關於組建以及組建與標籤發佈工作流程的配合情形的詳細資訊，請參閱[發佈概述](../../ui/publishing/overview.md)。

## 快速入門

本指南中使用的端點是[Reactor API](https://www.adobe.io/experience-platform-apis/references/reactor/)的一部分。 繼續操作之前，請參閱[快速入門手冊](../getting-started.md)，了解如何驗證API的重要資訊。

## 擷取組建清單 {#list}

您可以將程式庫的ID加入特定程式庫的請求路徑中，以列出特定程式庫的組建。

**API格式**

```http
GET /libraries/{LIBRARY_ID}/builds
```

| 參數 | 說明 |
| --- | --- |
| `LIBRARY_ID` | 您要列出其組建的程式庫的`id`。 |

{style=&quot;table-layout:auto&quot;}

>[!NOTE]
>
>您可以使用查詢參數，根據下列屬性來篩選列出的組建：<ul><li>`created_at`</li><li>`status`</li><li>`token`</li><li>`updated_at`</li></ul>如需詳細資訊，請參閱[篩選回應](../guides/filtering.md)的指南。

**要求**

```shell
curl -X GET \
  https://reactor.adobe.io/libraries/LBad32d71feff844b7b5a11dd0bf030964/builds \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**回應**

成功的回應會傳回指定程式庫的組建清單。

```json
{
  "data": [
    {
      "id": "BL654195b78ac84f00b633a0ef4cdde484",
      "type": "builds",
      "attributes": {
        "created_at": "2020-12-14T17:32:29.002Z",
        "status": "pending",
        "updated_at": "2020-12-14T17:32:29.002Z",
        "token": "83407e650dbf"
      },
      "relationships": {
        "data_elements": {
          "links": {
            "related": "https://reactor.adobe.io/builds/BL654195b78ac84f00b633a0ef4cdde484/data_elements"
          }
        },
        "extensions": {
          "links": {
            "related": "https://reactor.adobe.io/builds/BL654195b78ac84f00b633a0ef4cdde484/extensions"
          }
        },
        "rules": {
          "links": {
            "related": "https://reactor.adobe.io/builds/BL654195b78ac84f00b633a0ef4cdde484/rules"
          }
        },
        "environment": {
          "links": {
            "related": "https://reactor.adobe.io/builds/BL654195b78ac84f00b633a0ef4cdde484/environment"
          },
          "data": {
            "id": "EN7d73baa7b287421685a3ba5a447754df",
            "type": "environments"
          }
        },
        "library": {
          "links": {
            "related": "https://reactor.adobe.io/builds/BL654195b78ac84f00b633a0ef4cdde484/library"
          },
          "data": {
            "id": "LBad32d71feff844b7b5a11dd0bf030964",
            "type": "libraries"
          }
        },
        "property": {
          "links": {
            "related": "https://reactor.adobe.io/builds/BL654195b78ac84f00b633a0ef4cdde484/property"
          },
          "data": {
            "id": "PR7dbf185ba81f4698811f6e650c862492",
            "type": "properties"
          }
        }
      },
      "links": {
        "environment": "https://reactor.adobe.io/environments/EN7d73baa7b287421685a3ba5a447754df",
        "library": "https://reactor.adobe.io/libraries/LBad32d71feff844b7b5a11dd0bf030964",
        "self": "https://reactor.adobe.io/builds/BL654195b78ac84f00b633a0ef4cdde484"
      },
      "meta": {
        "artifact_url": "https://assets.adobedtm.com/staging/f9fd106ab399/bf45601a3b3d/launch-678767d5a218-development.min.js",
        "direct_artifact_url": "https://assets.adobedtm.com/staging/f9fd106ab399/bf45601a3b3d/83407e650dbf/launch-678767d5a218-development.min.js",
        "archive": false,
        "host_type_of": "akamai"
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

## 查找組建 {#lookup}

您可以在請求的路徑中提供組建ID，以便查詢GET。

**API格式**

```http
GET /builds/{BUILD_ID}
```

| 參數 | 說明 |
| --- | --- |
| `BUILD_ID` | 您要查詢之組建的`id`。 |

{style=&quot;table-layout:auto&quot;}

**要求**

```shell
curl -X GET \
  https://reactor.adobe.io/builds/BL8238895201d548718bda2d0bf2b83467 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**回應**

成功的回應會傳回組建的詳細資訊。

```json
{
  "data": {
    "id": "BL8238895201d548718bda2d0bf2b83467",
    "type": "builds",
    "attributes": {
      "created_at": "2020-12-14T17:32:14.671Z",
      "status": "pending",
      "updated_at": "2020-12-14T17:32:14.671Z",
      "token": "ae8c9574e8d4"
    },
    "relationships": {
      "data_elements": {
        "links": {
          "related": "https://reactor.adobe.io/builds/BL8238895201d548718bda2d0bf2b83467/data_elements"
        }
      },
      "extensions": {
        "links": {
          "related": "https://reactor.adobe.io/builds/BL8238895201d548718bda2d0bf2b83467/extensions"
        }
      },
      "rules": {
        "links": {
          "related": "https://reactor.adobe.io/builds/BL8238895201d548718bda2d0bf2b83467/rules"
        }
      },
      "environment": {
        "links": {
          "related": "https://reactor.adobe.io/builds/BL8238895201d548718bda2d0bf2b83467/environment"
        },
        "data": {
          "id": "EN2fe1274add61492a983ad7322d1b3010",
          "type": "environments"
        }
      },
      "library": {
        "links": {
          "related": "https://reactor.adobe.io/builds/BL8238895201d548718bda2d0bf2b83467/library"
        },
        "data": {
          "id": "LBd8eaef8283fe40738348db65a8984475",
          "type": "libraries"
        }
      },
      "property": {
        "links": {
          "related": "https://reactor.adobe.io/builds/BL8238895201d548718bda2d0bf2b83467/property"
        },
        "data": {
          "id": "PRb75b4216130e469abf1eb1795da8048b",
          "type": "properties"
        }
      }
    },
    "links": {
      "environment": "https://reactor.adobe.io/environments/EN2fe1274add61492a983ad7322d1b3010",
      "library": "https://reactor.adobe.io/libraries/LBd8eaef8283fe40738348db65a8984475",
      "self": "https://reactor.adobe.io/builds/BL8238895201d548718bda2d0bf2b83467"
    },
    "meta": {
      "artifact_url": "https://assets.adobedtm.com/staging/f9fd106ab399/5fc05b7c8e8f/launch-32129df48f5b-development.min.js",
      "direct_artifact_url": "https://assets.adobedtm.com/staging/f9fd106ab399/5fc05b7c8e8f/ae8c9574e8d4/launch-32129df48f5b-development.min.js",
      "archive": false,
      "host_type_of": "akamai"
    }
  }
}
```

## 建立組建 {#create}

您可以為程式庫建立組建，包括程式庫ID在POST請求的路徑中。

**API格式**

```http
POST /libraries/{LIBRARY_ID}/builds
```

| 參數 | 說明 |
| --- | --- |
| `LIBRARY_ID` | 您要定義下組建的程式庫的`id`。 |

{style=&quot;table-layout:auto&quot;}

**要求**

下列請求會為請求路徑中指定的程式庫建立新的組建。 不需要要求裝載。

```shell
curl -X POST \
  https://reactor.adobe.io/libraries/LBd8eaef8283fe40738348db65a8984475/builds \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}'
```

**回應**

成功的回應會傳回新建立之組建的詳細資訊。

```json
{
  "data": {
    "id": "BL5b3fbb0dfd66480abb55a376005ec3f7",
    "type": "builds",
    "attributes": {
      "created_at": "2020-12-14T17:32:00.021Z",
      "status": "pending",
      "updated_at": "2020-12-14T17:32:00.021Z",
      "token": "65bbda194025"
    },
    "relationships": {
      "data_elements": {
        "links": {
          "related": "https://reactor.adobe.io/builds/BL5b3fbb0dfd66480abb55a376005ec3f7/data_elements"
        }
      },
      "extensions": {
        "links": {
          "related": "https://reactor.adobe.io/builds/BL5b3fbb0dfd66480abb55a376005ec3f7/extensions"
        }
      },
      "rules": {
        "links": {
          "related": "https://reactor.adobe.io/builds/BL5b3fbb0dfd66480abb55a376005ec3f7/rules"
        }
      },
      "environment": {
        "links": {
          "related": "https://reactor.adobe.io/builds/BL5b3fbb0dfd66480abb55a376005ec3f7/environment"
        },
        "data": {
          "id": "EN867c480dc5ea4158be3ea68e5543bd85",
          "type": "environments"
        }
      },
      "library": {
        "links": {
          "related": "https://reactor.adobe.io/builds/BL5b3fbb0dfd66480abb55a376005ec3f7/library"
        },
        "data": {
          "id": "LBdd2f55e9c3bb4ce0a582a0b0c586a6f5",
          "type": "libraries"
        }
      },
      "property": {
        "links": {
          "related": "https://reactor.adobe.io/builds/BL5b3fbb0dfd66480abb55a376005ec3f7/property"
        },
        "data": {
          "id": "PRa41874e4d1604efd9c3c67d7a123f4c6",
          "type": "properties"
        }
      }
    },
    "links": {
      "environment": "https://reactor.adobe.io/environments/EN867c480dc5ea4158be3ea68e5543bd85",
      "library": "https://reactor.adobe.io/libraries/LBdd2f55e9c3bb4ce0a582a0b0c586a6f5",
      "self": "https://reactor.adobe.io/builds/BL5b3fbb0dfd66480abb55a376005ec3f7"
    },
    "meta": {
      "artifact_url": "https://assets.adobedtm.com/staging/f9fd106ab399/bd007122e3e3/launch-4d5a31f6ca53-development.min.js",
      "direct_artifact_url": "https://assets.adobedtm.com/staging/f9fd106ab399/bd007122e3e3/65bbda194025/launch-4d5a31f6ca53-development.min.js",
      "archive": false,
      "host_type_of": "akamai"
    }
  }
}
```

## 重新發佈組建 {#republish}

您可以從[已發佈的程式庫](./libraries.md#publish)重新發佈組建，方法是將其ID納入PATCH請求的路徑。

**API格式**

```http
PATCH /builds/{BUILD_ID}
```

| 參數 | 說明 |
| --- | --- |
| `BUILD_ID` | 您要重新發佈之組建的`id`。 |

{style=&quot;table-layout:auto&quot;}

**要求**

下列請求會更新現有應用程式設定的`app_id`。

```shell
curl -X PATCH \
  https://reactor.adobe.io/builds/BLb408c04c20ba4a82b6df496969a99781 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'Content-Type: application/json' \
  -d '{
        "data": {
          "id": "BLb408c04c20ba4a82b6df496969a99781",
          "type": "builds",
          "meta": {
            "action": "republish"
          }
        }
      }'
```

| 屬性 | 說明 |
| --- | --- |
| `id` | 您要更新之組建的`id`。 這應符合要求路徑中提供的`{BUILD_ID}`值。 |
| `type` | 要更新的資源類型。 對於此端點，值必須為`builds`。 |
| `meta.action` | 要執行的PATCH動作類型。 必須設為`republish`。 |

{style=&quot;table-layout:auto&quot;}

**回應**

成功的回應會傳回重新發佈之組建的詳細資訊。

```json
{
  "data": {
    "id": "BLb408c04c20ba4a82b6df496969a99781",
    "type": "builds",
    "attributes": {
      "created_at": "2020-12-14T17:34:08.558Z",
      "status": "succeeded",
      "updated_at": "2020-12-14T17:34:16.190Z",
      "token": "951e1b7911e8"
    },
    "relationships": {
      "data_elements": {
        "links": {
          "related": "https://reactor.adobe.io/builds/BLb408c04c20ba4a82b6df496969a99781/data_elements"
        }
      },
      "extensions": {
        "links": {
          "related": "https://reactor.adobe.io/builds/BLb408c04c20ba4a82b6df496969a99781/extensions"
        }
      },
      "rules": {
        "links": {
          "related": "https://reactor.adobe.io/builds/BLb408c04c20ba4a82b6df496969a99781/rules"
        }
      },
      "environment": {
        "links": {
          "related": "https://reactor.adobe.io/builds/BLb408c04c20ba4a82b6df496969a99781/environment"
        },
        "data": {
          "id": "EN51a1b47d737341b1b742cbd62504bb5a",
          "type": "environments"
        }
      },
      "library": {
        "links": {
          "related": "https://reactor.adobe.io/builds/BLb408c04c20ba4a82b6df496969a99781/library"
        },
        "data": {
          "id": "LBa503843ac6e64df0ad18604adad78600",
          "type": "libraries"
        }
      },
      "property": {
        "links": {
          "related": "https://reactor.adobe.io/builds/BLb408c04c20ba4a82b6df496969a99781/property"
        },
        "data": {
          "id": "PR00abebfe39f84dc2a0ca13410e0a1751",
          "type": "properties"
        }
      }
    },
    "links": {
      "environment": "https://reactor.adobe.io/environments/EN51a1b47d737341b1b742cbd62504bb5a",
      "library": "https://reactor.adobe.io/libraries/LBa503843ac6e64df0ad18604adad78600",
      "self": "https://reactor.adobe.io/builds/BLb408c04c20ba4a82b6df496969a99781"
    },
    "meta": {
      "artifact_url": "https://assets.adobedtm.com/staging/f9fd106ab399/f812fa6d64df/launch-9b1b8e461782.min.js",
      "direct_artifact_url": "https://assets.adobedtm.com/staging/f9fd106ab399/f812fa6d64df/951e1b7911e8/launch-9b1b8e461782.min.js",
      "archive": false,
      "republish_status": "pending",
      "host_type_of": "akamai"
    }
  }
}
```

## 擷取組建的相關資源 {#related}

下列呼叫示範如何擷取組建的相關資源。 當[查詢組建](#lookup)時，這些關係會列在`relationships`屬性下。

有關Reactor API中關係的詳細資訊，請參閱[關係指南](../guides/relationships.md)。

### 列出組建的相關資料元素 {#data-elements}

您可以將`/data_elements`附加至查詢請求的路徑，以列出組建的相關資料元素。

**API格式**

```http
GET  /builds/{BUILD_ID}/data_elements
```

| 參數 | 說明 |
| --- | --- |
| `{BUILD_ID}` | 您要列出其資料元素之組建的`id`。 |

{style=&quot;table-layout:auto&quot;}

**要求**

```shell
curl -X GET \
  https://reactor.adobe.io/builds/BLb408c04c20ba4a82b6df496969a99781/data_elements \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**回應**

成功的回應會傳回與組建相關的資料元素清單。

```json
{
  "data": [
    {
      "id": "DE4139bfd5c2194254b5c1af254d421262",
      "type": "data_elements",
      "attributes": {
        "created_at": "2020-12-14T17:33:22.668Z",
        "deleted_at": null,
        "dirty": false,
        "enabled": true,
        "name": "My Data Element 2020-12-14 17:33:21 +0000",
        "published": false,
        "published_at": null,
        "revision_number": 1,
        "updated_at": "2020-12-14T17:33:22.668Z",
        "clean_text": false,
        "default_value": null,
        "delegate_descriptor_id": "kessel-test::dataElements::dom-attribute",
        "force_lower_case": false,
        "review_status": "unsubmitted",
        "storage_duration": null,
        "settings": "{\"elementProperty\":\"html\",\"elementSelector\":\".target-element\"}"
      },
      "relationships": {
        "libraries": {
          "links": {
            "related": "https://reactor.adobe.io/data_elements/DE4139bfd5c2194254b5c1af254d421262/libraries"
          }
        },
        "revisions": {
          "links": {
            "related": "https://reactor.adobe.io/data_elements/DE4139bfd5c2194254b5c1af254d421262/revisions"
          }
        },
        "notes": {
          "links": {
            "related": "https://reactor.adobe.io/data_elements/DE4139bfd5c2194254b5c1af254d421262/notes"
          }
        },
        "property": {
          "links": {
            "related": "https://reactor.adobe.io/data_elements/DE4139bfd5c2194254b5c1af254d421262/property"
          },
          "data": {
            "id": "PR05ad70a8078f44c1a229ecf0da2802f2",
            "type": "properties"
          }
        },
        "origin": {
          "links": {
            "related": "https://reactor.adobe.io/data_elements/DE4139bfd5c2194254b5c1af254d421262/origin"
          },
          "data": {
            "id": "DE8667bc64ceba4b599e8458ea4ab58b8f",
            "type": "data_elements"
          }
        },
        "extension": {
          "links": {
            "related": "https://reactor.adobe.io/data_elements/DE4139bfd5c2194254b5c1af254d421262/extension"
          },
          "data": {
            "id": "EX28788723a8e24a2f927fce1b55eb7ffc",
            "type": "extensions"
          }
        },
        "updated_with_extension_package": {
          "links": {
            "related": "https://reactor.adobe.io/data_elements/DE4139bfd5c2194254b5c1af254d421262/updated_with_extension_package"
          },
          "data": {
            "id": "EP75db2452065b44e2b8a38ca883ce369a",
            "type": "extension_packages"
          }
        },
        "updated_with_extension": {
          "links": {
            "related": "https://reactor.adobe.io/data_elements/DE4139bfd5c2194254b5c1af254d421262/updated_with_extension"
          },
          "data": {
            "id": "EXd6bf04b143e64fe0ae7efe55a6655fa9",
            "type": "extensions"
          }
        }
      },
      "links": {
        "property": "https://reactor.adobe.io/properties/PR05ad70a8078f44c1a229ecf0da2802f2",
        "origin": "https://reactor.adobe.io/data_elements/DE8667bc64ceba4b599e8458ea4ab58b8f",
        "self": "https://reactor.adobe.io/data_elements/DE4139bfd5c2194254b5c1af254d421262",
        "extension": "https://reactor.adobe.io/extensions/EX28788723a8e24a2f927fce1b55eb7ffc"
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
      "total_count": 1
    }
  }
}
```

### 列出組建的相關擴充功能 {#extensions}

您可以將`/extensions`附加至查詢請求的路徑，以列出組建的相關擴充功能。

**API格式**

```http
GET  /builds/{BUILD_ID}/extensions
```

| 參數 | 說明 |
| --- | --- |
| `{BUILD_ID}` | 您要列出其擴充功能之組建的`id`。 |

{style=&quot;table-layout:auto&quot;}

**要求**

```shell
curl -X GET \
  https://reactor.adobe.io/builds/BLb408c04c20ba4a82b6df496969a99781/extensions \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**回應**

成功的回應會傳回與組建相關的擴充功能清單。

```json
{
  "data": [
    {
      "id": "EXf6242ef93c1c47e6971ed6ea85912b11",
      "type": "extensions",
      "attributes": {
        "created_at": "2020-12-14T17:32:56.163Z",
        "deleted_at": null,
        "dirty": false,
        "enabled": true,
        "name": "kessel-test",
        "published": false,
        "published_at": null,
        "revision_number": 1,
        "updated_at": "2020-12-14T17:32:56.163Z",
        "delegate_descriptor_id": null,
        "display_name": "Kessel Test",
        "review_status": "unsubmitted",
        "version": "1.2.0",
        "settings": "{}"
      },
      "relationships": {
        "libraries": {
          "links": {
            "related": "https://reactor.adobe.io/extensions/EXf6242ef93c1c47e6971ed6ea85912b11/libraries"
          }
        },
        "revisions": {
          "links": {
            "related": "https://reactor.adobe.io/extensions/EXf6242ef93c1c47e6971ed6ea85912b11/revisions"
          }
        },
        "notes": {
          "links": {
            "related": "https://reactor.adobe.io/extensions/EXf6242ef93c1c47e6971ed6ea85912b11/notes"
          }
        },
        "property": {
          "links": {
            "related": "https://reactor.adobe.io/extensions/EXf6242ef93c1c47e6971ed6ea85912b11/property"
          },
          "data": {
            "id": "PRcf1f3e4c218b4caab8191fab003a8355",
            "type": "properties"
          }
        },
        "origin": {
          "links": {
            "related": "https://reactor.adobe.io/extensions/EXf6242ef93c1c47e6971ed6ea85912b11/origin"
          },
          "data": {
            "id": "EX8ce7ced633f34bd48d33089ff8fad082",
            "type": "extensions"
          }
        },
        "updated_with_extension_package": {
          "links": {
            "related": "https://reactor.adobe.io/extensions/EXf6242ef93c1c47e6971ed6ea85912b11/updated_with_extension_package"
          },
          "data": {
            "id": "EP75db2452065b44e2b8a38ca883ce369a",
            "type": "extension_packages"
          }
        },
        "extension_package": {
          "links": {
            "related": "https://reactor.adobe.io/extensions/EXf6242ef93c1c47e6971ed6ea85912b11/extension_package"
          },
          "data": {
            "id": "EP75db2452065b44e2b8a38ca883ce369a",
            "type": "extension_packages"
          }
        }
      },
      "links": {
        "property": "https://reactor.adobe.io/properties/PRcf1f3e4c218b4caab8191fab003a8355",
        "origin": "https://reactor.adobe.io/extensions/EX8ce7ced633f34bd48d33089ff8fad082",
        "self": "https://reactor.adobe.io/extensions/EXf6242ef93c1c47e6971ed6ea85912b11",
        "extension_package": "https://reactor.adobe.io/extension_packages/EP75db2452065b44e2b8a38ca883ce369a",
        "latest_extension_package": "https://reactor.adobe.io/extension_packages/EP75db2452065b44e2b8a38ca883ce369a"
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
      "total_count": 1
    }
  }
}
```

### 列出組建的相關規則 {#rules}

您可以將`/rules`附加至查詢請求的路徑，借此列出組建的相關規則。

**API格式**

```http
GET  /builds/{BUILD_ID}/rules
```

| 參數 | 說明 |
| --- | --- |
| `{BUILD_ID}` | 要列出其規則的組建的`id`。 |

{style=&quot;table-layout:auto&quot;}

**要求**

```shell
curl -X GET \
  https://reactor.adobe.io/builds/BLb408c04c20ba4a82b6df496969a99781/rules \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**回應**

成功的回應會傳回與組建相關的規則清單。

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

### 尋找組建的相關程式庫 {#library}

您可以將`/library`附加至查詢請求的路徑，借此擷取組建的相關程式庫。

**API格式**

```http
GET  /builds/{BUILD_ID}/library
```

| 參數 | 說明 |
| --- | --- |
| `{BUILD_ID}` | 您要查詢其程式庫的組建的`id`。 |

{style=&quot;table-layout:auto&quot;}

**要求**

```shell
curl -X GET \
  https://reactor.adobe.io/builds/BLb408c04c20ba4a82b6df496969a99781/library \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**回應**

```json
{
  "data": {
    "id": "LB6ce27064ebe04ceab3d6942e9de563db",
    "type": "libraries",
    "attributes": {
      "created_at": "2020-12-14T17:50:06.695Z",
      "name": "My Library",
      "published_at": null,
      "state": "development",
      "updated_at": "2020-12-14T17:50:06.695Z",
      "build_required": true
    },
    "relationships": {
      "builds": {
        "links": {
          "related": "https://reactor.adobe.io/libraries/LB6ce27064ebe04ceab3d6942e9de563db/builds"
        }
      },
      "environment": {
        "links": {
          "related": "https://reactor.adobe.io/libraries/LB6ce27064ebe04ceab3d6942e9de563db/environment",
          "self": "https://reactor.adobe.io/libraries/LB6ce27064ebe04ceab3d6942e9de563db/relationships/environment"
        },
        "data": {
          "id": "EN3287da6fafa143c289afd2f578b4d33d",
          "type": "environments"
        }
      },
      "data_elements": {
        "links": {
          "related": "https://reactor.adobe.io/libraries/LB6ce27064ebe04ceab3d6942e9de563db/data_elements",
          "self": "https://reactor.adobe.io/libraries/LB6ce27064ebe04ceab3d6942e9de563db/relationships/data_elements"
        }
      },
      "extensions": {
        "links": {
          "related": "https://reactor.adobe.io/libraries/LB6ce27064ebe04ceab3d6942e9de563db/extensions",
          "self": "https://reactor.adobe.io/libraries/LB6ce27064ebe04ceab3d6942e9de563db/relationships/extensions"
        }
      },
      "notes": {
        "links": {
          "related": "https://reactor.adobe.io/libraries/LB6ce27064ebe04ceab3d6942e9de563db/notes"
        }
      },
      "rules": {
        "links": {
          "related": "https://reactor.adobe.io/libraries/LB6ce27064ebe04ceab3d6942e9de563db/rules",
          "self": "https://reactor.adobe.io/libraries/LB6ce27064ebe04ceab3d6942e9de563db/relationships/rules"
        }
      },
      "upstream_library": {
        "data": null
      },
      "property": {
        "links": {
          "related": "https://reactor.adobe.io/libraries/LB6ce27064ebe04ceab3d6942e9de563db/property"
        },
        "data": {
          "id": "PR95eaa16990c745a78f5bee8439fe4c34",
          "type": "properties"
        }
      },
      "last_build": {
        "links": {
          "related": "https://reactor.adobe.io/libraries/LB6ce27064ebe04ceab3d6942e9de563db/last_build"
        },
        "data": null
      }
    },
    "links": {
      "property": "https://reactor.adobe.io/properties/PR95eaa16990c745a78f5bee8439fe4c34",
      "self": "https://reactor.adobe.io/libraries/LB6ce27064ebe04ceab3d6942e9de563db"
    },
    "meta": {
      "build_status": null,
      "build_required_detail": "No build found since last state change"
    }
  }
}
```

### 查找組建的相關環境 {#environment}

您可以將`/environment`附加至查詢請求的路徑，借此擷取組建的相關環境。

**API格式**

```http
GET  /builds/{BUILD_ID}/environment
```

| 參數 | 說明 |
| --- | --- |
| `{BUILD_ID}` | 您要查詢其環境的組建的`id`。 |

{style=&quot;table-layout:auto&quot;}

**要求**

```shell
curl -X GET \
  https://reactor.adobe.io/builds/BLb408c04c20ba4a82b6df496969a99781/environment \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**回應**

```json
{
  "data": {
    "id": "EN11e6b85c0af14f0fb99f0c192a22e5e2",
    "type": "environments",
    "attributes": {
      "archive": false,
      "created_at": "2020-12-14T17:39:25.179Z",
      "library_path": "f9fd106ab399/5a1ebaf3db58",
      "library_name": "launch-f0e3e49544fe-development.min.js",
      "library_entry_points": [
        {
          "library_name": "launch-f0e3e49544fe-development.min.js",
          "minified": true,
          "references": [
            "f9fd106ab399/5a1ebaf3db58/launch-f0e3e49544fe-development.min.js"
          ],
          "license_path": "f9fd106ab399/5a1ebaf3db58/launch-f0e3e49544fe-development.js"
        },
        {
          "library_name": "launch-f0e3e49544fe-development.js",
          "minified": false,
          "references": [
            "f9fd106ab399/5a1ebaf3db58/launch-f0e3e49544fe-development.js"
          ]
        }
      ],
      "name": "Development Environment A",
      "path": "https://assets.adobedtm.com/staging",
      "stage": "development",
      "updated_at": "2020-12-14T17:39:26.221Z",
      "status": "succeeded",
      "token": "f0e3e49544fe"
    },
    "relationships": {
      "library": {
        "links": {
          "related": "https://reactor.adobe.io/environments/EN11e6b85c0af14f0fb99f0c192a22e5e2/library"
        },
        "data": {
          "id": "LB6e0f7904575f489497b959fd6b81dce8",
          "type": "libraries"
        }
      },
      "builds": {
        "links": {
          "related": "https://reactor.adobe.io/environments/EN11e6b85c0af14f0fb99f0c192a22e5e2/builds"
        }
      },
      "host": {
        "links": {
          "related": "https://reactor.adobe.io/environments/EN11e6b85c0af14f0fb99f0c192a22e5e2/host",
          "self": "https://reactor.adobe.io/environments/EN11e6b85c0af14f0fb99f0c192a22e5e2/relationships/host"
        },
        "data": {
          "id": "HT33afd835e6da4533a4b07d39e916d3be",
          "type": "hosts"
        }
      },
      "property": {
        "links": {
          "related": "https://reactor.adobe.io/environments/EN11e6b85c0af14f0fb99f0c192a22e5e2/property"
        },
        "data": {
          "id": "PRe686c8ac90b343f98bbd14e990952605",
          "type": "properties"
        }
      }
    },
    "links": {
      "property": "https://reactor.adobe.io/properties/PRe686c8ac90b343f98bbd14e990952605",
      "self": "https://reactor.adobe.io/environments/EN11e6b85c0af14f0fb99f0c192a22e5e2"
    },
    "meta": {
      "archive_encrypted": false
    }
  }
}
```
