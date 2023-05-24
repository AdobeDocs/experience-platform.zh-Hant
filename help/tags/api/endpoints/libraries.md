---
title: 庫終結點
description: 瞭解如何調用Repartor API中的/library端點。
exl-id: 0f7bc10f-2e03-43fa-993c-a2635f4d0c64
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '1521'
ht-degree: 5%

---

# 庫終結點

庫是標籤資源的集合([擴展](./extensions.md)。 [規則](./rules.md), [資料元素](./data-elements.md))表示 [屬性](./properties.md)。 的 `/libraries` Reactor API中的端點允許您以寫程式方式管理標籤屬性中的庫。

庫只屬於一個屬性。 一個屬性可以具有多個庫。

## 快速入門

本指南中使用的端點是 [反應堆API](https://www.adobe.io/experience-platform-apis/references/reactor/)。 在繼續之前，請查看 [入門指南](../getting-started.md) 有關如何驗證到API的重要資訊。

在使用Repartor API中的庫之前，瞭解庫狀態和環境在確定可以對特定庫執行哪些操作時所起的作用非常重要。 請參閱 [庫發佈流](../../ui/publishing/publishing-flow.md) 的子菜單。

## 檢索庫清單 {#list}

通過將屬性的ID包括在GET請求的路徑中，可以檢索屬性的庫清單。

**API格式**

```http
GET /properties/{PROPERTY_ID}/libraries
```

| 參數 | 說明 |
| --- | --- |
| `PROPERTY_ID` | 的 `id` 擁有庫的屬性。 |

{style="table-layout:auto"}

>[!NOTE]
>
>使用查詢參數，可以根據以下屬性篩選列出的庫：<ul><li>`created_at`</li><li>`name`</li><li>`published_at`</li><li>`stale`</li><li>`state`</li><li>`updated_at`</li></ul>請參閱上的指南 [過濾響應](../guides/filtering.md) 的子菜單。

**要求**

```shell
curl -X GET \
  https://reactor.adobe.io/properties/PR4bc17fb09ed845b1acfb0f6600a1f3c0/libraries \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**回應**

成功的響應將返回指定屬性的庫清單。

```json
{
  "data": [
    {
      "id": "LBb174d60bdbd34f87a2e9466fadaacae0",
      "type": "libraries",
      "attributes": {
        "created_at": "2020-12-14T17:44:10.776Z",
        "name": "My Library",
        "published_at": null,
        "state": "development",
        "updated_at": "2020-12-14T17:44:10.776Z",
        "build_required": true
      },
      "relationships": {
        "builds": {
          "links": {
            "related": "https://reactor.adobe.io/libraries/LBb174d60bdbd34f87a2e9466fadaacae0/builds"
          }
        },
        "environment": {
          "links": {
            "self": "https://reactor.adobe.io/libraries/LBb174d60bdbd34f87a2e9466fadaacae0/relationships/environment"
          },
          "data": null
        },
        "data_elements": {
          "links": {
            "related": "https://reactor.adobe.io/libraries/LBb174d60bdbd34f87a2e9466fadaacae0/data_elements",
            "self": "https://reactor.adobe.io/libraries/LBb174d60bdbd34f87a2e9466fadaacae0/relationships/data_elements"
          }
        },
        "extensions": {
          "links": {
            "related": "https://reactor.adobe.io/libraries/LBb174d60bdbd34f87a2e9466fadaacae0/extensions",
            "self": "https://reactor.adobe.io/libraries/LBb174d60bdbd34f87a2e9466fadaacae0/relationships/extensions"
          }
        },
        "notes": {
          "links": {
            "related": "https://reactor.adobe.io/libraries/LBb174d60bdbd34f87a2e9466fadaacae0/notes"
          }
        },
        "rules": {
          "links": {
            "related": "https://reactor.adobe.io/libraries/LBb174d60bdbd34f87a2e9466fadaacae0/rules",
            "self": "https://reactor.adobe.io/libraries/LBb174d60bdbd34f87a2e9466fadaacae0/relationships/rules"
          }
        },
        "upstream_library": {
          "data": null
        },
        "property": {
          "links": {
            "related": "https://reactor.adobe.io/libraries/LBb174d60bdbd34f87a2e9466fadaacae0/property"
          },
          "data": {
            "id": "PR4bc17fb09ed845b1acfb0f6600a1f3c0",
            "type": "properties"
          }
        },
        "last_build": {
          "links": {
            "related": "https://reactor.adobe.io/libraries/LBb174d60bdbd34f87a2e9466fadaacae0/last_build"
          },
          "data": null
        }
      },
      "links": {
        "property": "https://reactor.adobe.io/properties/PR4bc17fb09ed845b1acfb0f6600a1f3c0",
        "self": "https://reactor.adobe.io/libraries/LBb174d60bdbd34f87a2e9466fadaacae0"
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

## 查找庫 {#lookup}

您可以通過在GET請求的路徑中提供庫ID來查找庫。

**API格式**

```http
GET /libraries/{LIBRARY_ID}
```

| 參數 | 說明 |
| --- | --- |
| `LIBRARY_ID` | 的 `id` 你想查的圖書館。 |

{style="table-layout:auto"}

**要求**

```shell
curl -X GET \
  https://reactor.adobe.io/libraries/LB5862ee2dc21b4646a5536c8d6edb0c84 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**回應**

成功的響應返回庫的詳細資訊。

```json
{
  "data": {
    "id": "LB5862ee2dc21b4646a5536c8d6edb0c84",
    "type": "libraries",
    "attributes": {
      "created_at": "2020-12-14T17:44:00.476Z",
      "name": "My Library",
      "published_at": null,
      "state": "development",
      "updated_at": "2020-12-14T17:44:00.476Z",
      "build_required": true
    },
    "relationships": {
      "builds": {
        "links": {
          "related": "https://reactor.adobe.io/libraries/LB5862ee2dc21b4646a5536c8d6edb0c84/builds"
        }
      },
      "environment": {
        "links": {
          "self": "https://reactor.adobe.io/libraries/LB5862ee2dc21b4646a5536c8d6edb0c84/relationships/environment"
        },
        "data": null
      },
      "data_elements": {
        "links": {
          "related": "https://reactor.adobe.io/libraries/LB5862ee2dc21b4646a5536c8d6edb0c84/data_elements",
          "self": "https://reactor.adobe.io/libraries/LB5862ee2dc21b4646a5536c8d6edb0c84/relationships/data_elements"
        }
      },
      "extensions": {
        "links": {
          "related": "https://reactor.adobe.io/libraries/LB5862ee2dc21b4646a5536c8d6edb0c84/extensions",
          "self": "https://reactor.adobe.io/libraries/LB5862ee2dc21b4646a5536c8d6edb0c84/relationships/extensions"
        }
      },
      "notes": {
        "links": {
          "related": "https://reactor.adobe.io/libraries/LB5862ee2dc21b4646a5536c8d6edb0c84/notes"
        }
      },
      "rules": {
        "links": {
          "related": "https://reactor.adobe.io/libraries/LB5862ee2dc21b4646a5536c8d6edb0c84/rules",
          "self": "https://reactor.adobe.io/libraries/LB5862ee2dc21b4646a5536c8d6edb0c84/relationships/rules"
        }
      },
      "upstream_library": {
        "data": null
      },
      "property": {
        "links": {
          "related": "https://reactor.adobe.io/libraries/LB5862ee2dc21b4646a5536c8d6edb0c84/property"
        },
        "data": {
          "id": "PRc90084c615844db58201d4e70d47b8bf",
          "type": "properties"
        }
      },
      "last_build": {
        "links": {
          "related": "https://reactor.adobe.io/libraries/LB5862ee2dc21b4646a5536c8d6edb0c84/last_build"
        },
        "data": null
      }
    },
    "links": {
      "property": "https://reactor.adobe.io/properties/PRc90084c615844db58201d4e70d47b8bf",
      "self": "https://reactor.adobe.io/libraries/LB5862ee2dc21b4646a5536c8d6edb0c84"
    },
    "meta": {
      "build_status": null,
      "build_required_detail": "No build found since last state change"
    }
  }
}
```

## 建立程式庫 {#create}

可以通過發出POST請求建立新庫。

**API格式**

```http
POST /properties/{PROPERTY_ID}/libraries
```

| 參數 | 說明 |
| --- | --- |
| `PROPERTY_ID` | 的 `id` 的 [屬性](./properties.md) 定義下的庫。 |

{style="table-layout:auto"}

**要求**

以下請求為指定的屬性建立新庫。 首次建立庫時，僅 `name` 可以配置屬性。 要向庫添加資料元素、擴展和規則，必須建立關係。 請參閱 [管理庫資源](#resources) 的子菜單。

```shell
curl -X POST \
  https://reactor.adobe.io/properties/PR97d92a379a5f48758947cdf44f607a0d/libraries \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Content-Type: application/json' \
  -d '{
        "data": {
          "attributes": {
            "name": "My Library"
          },
          "type": "libraries"
        }
      }'
```

| 屬性 | 說明 |
| --- | --- |
| `attributes.name` | **（必需）** 庫的可讀名稱。 |
| `type` | 要更新的資源類型。 對於此終結點，值必須為 `libraries`。 |

{style="table-layout:auto"}

**回應**

成功的響應將返回新建立的庫的詳細資訊。

```json
{
  "data": {
    "id": "DE8667bc64ceba4b599e8458ea4ab58b8f",
    "type": "libraries",
    "attributes": {
      "created_at": "2020-12-14T17:33:21.774Z",
      "deleted_at": null,
      "dirty": true,
      "enabled": true,
      "name": "My library 2020-12-14 17:33:21 +0000",
      "published": false,
      "published_at": null,
      "revision_number": 0,
      "updated_at": "2020-12-14T17:33:21.774Z",
      "clean_text": false,
      "default_value": null,
      "delegate_descriptor_id": "kessel-test::dataElements::dom-attribute",
      "force_lower_case": false,
      "review_status": "unsubmitted",
      "storage_duration": null,
      "settings": "{\"elementSelector\":\".target-element\",\"elementProperty\":\"html\"}"
    },
    "relationships": {
      "libraries": {
        "links": {
          "related": "https://reactor.adobe.io/libraries/DE8667bc64ceba4b599e8458ea4ab58b8f/libraries"
        }
      },
      "revisions": {
        "links": {
          "related": "https://reactor.adobe.io/libraries/DE8667bc64ceba4b599e8458ea4ab58b8f/revisions"
        }
      },
      "notes": {
        "links": {
          "related": "https://reactor.adobe.io/libraries/DE8667bc64ceba4b599e8458ea4ab58b8f/notes"
        }
      },
      "property": {
        "links": {
          "related": "https://reactor.adobe.io/libraries/DE8667bc64ceba4b599e8458ea4ab58b8f/property"
        },
        "data": {
          "id": "PR05ad70a8078f44c1a229ecf0da2802f2",
          "type": "properties"
        }
      },
      "origin": {
        "links": {
          "related": "https://reactor.adobe.io/libraries/DE8667bc64ceba4b599e8458ea4ab58b8f/origin"
        },
        "data": {
          "id": "DE8667bc64ceba4b599e8458ea4ab58b8f",
          "type": "libraries"
        }
      },
      "extension": {
        "links": {
          "related": "https://reactor.adobe.io/libraries/DE8667bc64ceba4b599e8458ea4ab58b8f/extension"
        },
        "data": {
          "id": "EX28788723a8e24a2f927fce1b55eb7ffc",
          "type": "extensions"
        }
      },
      "updated_with_extension_package": {
        "links": {
          "related": "https://reactor.adobe.io/libraries/DE8667bc64ceba4b599e8458ea4ab58b8f/updated_with_extension_package"
        },
        "data": {
          "id": "EP75db2452065b44e2b8a38ca883ce369a",
          "type": "extension_packages"
        }
      },
      "updated_with_extension": {
        "links": {
          "related": "https://reactor.adobe.io/libraries/DE8667bc64ceba4b599e8458ea4ab58b8f/updated_with_extension"
        },
        "data": {
          "id": "EXd6bf04b143e64fe0ae7efe55a6655fa9",
          "type": "extensions"
        }
      }
    },
    "links": {
      "property": "https://reactor.adobe.io/properties/PR05ad70a8078f44c1a229ecf0da2802f2",
      "origin": "https://reactor.adobe.io/libraries/DE8667bc64ceba4b599e8458ea4ab58b8f",
      "self": "https://reactor.adobe.io/libraries/DE8667bc64ceba4b599e8458ea4ab58b8f",
      "extension": "https://reactor.adobe.io/extensions/EX28788723a8e24a2f927fce1b55eb7ffc"
    },
    "meta": {
      "latest_revision_number": 0
    }
  }
}
```

## 管理庫的資源 {#resources}

通過關係建立與庫關聯的資料元素、擴展、規則和環境。 以下各節介紹如何通過API調用管理這些關係。

### 將資源添加到庫 {#add-resources}

可以通過附加將資源添加到庫 `/relationships` 到POST請求的路徑，然後是資源類型。

**API格式**

```http
POST /libraries/{LIBRARY_ID}/relationships/{RESOURCE_TYPE}
```

| 參數 | 說明 |
| --- | --- |
| `{LIBRARY_ID}` | 要添加資源的庫的ID。 |
| `{RESOURCE_TYPE}` | 要添加到庫的資源類型。 接受以下值： <ul><li>`data_elements`</li><li>`extensions`</li><li>`rules`</li></ul> |

{style="table-layout:auto"}

**要求**

以下請求將兩個資料元素添加到庫中。

```shell
curl -X POST \
  https://reactor.adobe.io/libraries/LBdd2f55e9c3bb4ce0a582a0b0c586a6f5/relationships/data_elements \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Accept: application/vnd.api+json;revision=1' \
  -H 'Content-Type: application/json' \
  -d '{
        "data": [
          {
            "id": "DEce7fdee2afe44efeb4d974247d1e8dbe",
            "type": "data_elements"
          },
          {
            "id": "DE8097636264104451ac3a18c95d5ff833",
            "type": "data_elements"
          }
        ]
      }'
```

| 屬性 | 說明 |
| --- | --- |
| `id` | 要添加到庫的資源的ID。 |
| `type` | 要添加到庫的資源類型。 |

{style="table-layout:auto"}

**回應**

成功的響應將返回所添加關係的詳細資訊。 執行 [查找請求](#lookup) 的 `relationships` 屬性。

```json
{
  "data": [
    {
      "type": "data_elements",
      "id": "DEce7fdee2afe44efeb4d974247d1e8dbe"
    },
    {
      "id": "DE8097636264104451ac3a18c95d5ff833",
      "type": "data_elements"
    }
  ],
  "links": {
    "related": "https://reactor.adobe.io/libraries/LB09eca17e012842b49466506f419283a7/data_elements",
    "self": "https://reactor.adobe.io/libraries/LB09eca17e012842b49466506f419283a7/relationships/data_elements"
  }
}
```

### 替換庫的資源 {#replace-resources}

可通過附加來替換庫的特定類型的所有現有資源 `/relationships` 到PATCH請求的路徑，然後是要替換的資源類型。

**API格式**

```http
PATCH /libraries/{LIBRARY_ID}/relationships/{RESOURCE_TYPE}
```

| 參數 | 說明 |
| --- | --- |
| `{LIBRARY_ID}` | 要替換其關係的庫的ID。 |
| `{RESOURCE_TYPE}` | 要替換的資源類型。 接受以下值： <ul><li>`data_elements`</li><li>`extensions`</li><li>`rules`</li></ul> |

{style="table-layout:auto"}

**要求**

以下請求將庫的擴展替換為中提供的擴展 `data` 陣列。

```shell
curl -X PATCH \
  https://reactor.adobe.io/libraries/LBdd2f55e9c3bb4ce0a582a0b0c586a6f5/relationships/environment \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Accept: application/vnd.api+json;revision=1' \
  -H 'Content-Type: application/json' \
  -d '{
        "data": [
          {
            "id": "EX58312732fd0f43f98037d765ef96c4cd",
            "type": "extensions"
          }
        ]
      }'
```

| 屬性 | 說明 |
| --- | --- |
| `id` | 要添加到庫的資源的ID。 |
| `type` | 要添加到庫的資源類型。 |

{style="table-layout:auto"}

**回應**

成功的響應將返回更新關係的詳細資訊。 執行 [查找請求](#lookup) 顯示 `relationships` 屬性。

```json
{
  "data": [
    {
      "type": "extensions",
      "id": "EX58312732fd0f43f98037d765ef96c4cd"
    }
  ],
  "links": {
    "related": "https://reactor.adobe.io/libraries/LBdbc7c49ac8f040bc9576db26b127444d/extensions",
    "self": "https://reactor.adobe.io/libraries/LBdbc7c49ac8f040bc9576db26b127444d/relationships/extensions"
  }
}
```

### 刪除庫的資源 {#remove-resources}

可通過附加來從庫中刪除現有資源 `/relationships` 到DELETE請求的路徑，然後是要刪除的資源類型。

**API格式**

```http
DELETE /libraries/{LIBRARY_ID}/relationships/{RESOURCE_TYPE}
```

| 參數 | 說明 |
| --- | --- |
| `{LIBRARY_ID}` | 要刪除其資源的庫的ID。 |
| `{RESOURCE_TYPE}` | 要刪除的資源類型。 接受以下值： <ul><li>`data_elements`</li><li>`extensions`</li><li>`rules`</li></ul> |

{style="table-layout:auto"}

**要求**

以下請求從庫中刪除規則。 未包含於 `data` 陣列未刪除。

```shell
curl -X DELETE \
  https://reactor.adobe.io/libraries/LBdd2f55e9c3bb4ce0a582a0b0c586a6f5/relationships/environment \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Accept: application/vnd.api+json;revision=1' \
  -H 'Content-Type: application/json' \
  -d '{
        "data": [
          {
            "id": "RLa16f7859c7404239940c2cf2ec02b03c",
            "type": "rules"
          }
        ]
      }'
```

| 屬性 | 說明 |
| --- | --- |
| `id` | 從庫中刪除的資源的ID。 |
| `type` | 從庫中刪除的資源類型。 |

{style="table-layout:auto"}

**回應**

成功的響應將返回資源類型的更新關係的詳細資訊。 如果此資源類型不存在關係，則 `data` 屬性作為空陣列返回。 執行 [查找請求](#lookup) 顯示 `relationships` 屬性。

```json
{
  "data": [

  ],
  "links": {
    "related": "https://reactor.adobe.io/libraries/LBbde5759742844fe59458ca0c988ecd61/rules",
    "self": "https://reactor.adobe.io/libraries/LBbde5759742844fe59458ca0c988ecd61/relationships/rules"
  }
}
```

## 將庫分配給環境 {#environment}

可以將庫分配給環境  `/relationships/environment` 到POST請求的路徑。

**API格式**

```http
POST /libraries/{LIBRARY_ID}/relationships/environment
```

| 參數 | 說明 |
| --- | --- |
| `{LIBRARY_ID}` | 要分配的庫的ID。 |

{style="table-layout:auto"}

**要求**

```shell
curl -X POST \
  https://reactor.adobe.io/libraries/LBdd2f55e9c3bb4ce0a582a0b0c586a6f5/relationships/environment \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Accept: application/vnd.api+json;revision=1' \
  -H 'Content-Type: application/json' \
  -d '{
        "data": {
          "id": "EN867c480dc5ea4158be3ea68e5543bd85",
          "type": "environments"
        }
      }'
```

| 屬性 | 說明 |
| --- | --- |
| `id` | 將庫分配給的環境的ID。 |
| `type` | 必須設定為 `environments`。 |

{style="table-layout:auto"}

**回應**

成功的響應將返回關係的詳細資訊。 執行 [查找請求](#lookup) 在 `relationships` 屬性。

```json
{
  "data": {
    "id": "EN867c480dc5ea4158be3ea68e5543bd85",
    "type": "environments"
  },
  "links": {
    "related": "https://reactor.adobe.io/libraries/LBdd2f55e9c3bb4ce0a582a0b0c586a6f5/environment",
    "self": "https://reactor.adobe.io/libraries/LBdd2f55e9c3bb4ce0a582a0b0c586a6f5/relationships/environment"
  }
}
```

## 轉換庫 {#transition}

通過將庫的ID包括在PATCH請求的路徑中，並提供適當的發佈狀態，可以將庫轉換到其他發佈狀態 `meta.action` 值。

**API格式**

```http
PATCH /libraries/{LIBRARY_ID}
```

| 參數 | 說明 |
| --- | --- |
| `LIBRARY_ID` | 的 `id` 要轉換的庫。 |

{style="table-layout:auto"}

**要求**

以下請求將根據 `meta.action` 在有效載荷中提供。 庫的可用操作取決於其當前發佈狀態，如 [發佈流](../../ui/publishing/publishing-flow.md#state)。

```shell
curl -X PATCH \
  https://reactor.adobe.io/libraries/LB5862ee2dc21b4646a5536c8d6edb0c84 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Content-Type: application/json' \
  -d '{
        "data": {
          "id": "LB80c337c956804738b2db2ea2f69fcdf0",
          "type": "libraries",
          "meta": {
            "action": "submit"
          }
        }
      }'
```

| 屬性 | 說明 |
| --- | --- |
| `meta.action` | 要對庫執行的特定轉換操作。 根據庫的當前發佈狀態，可以執行以下操作： <ul><li>`develop`</li><li>`submit`</li><li>`approve`</li><li>`reject`</li></ul> |
| `id` | 的 `id` 的子菜單。 這應與 `{LIBRARY_ID}` 請求路徑中提供的值。 |
| `type` | 要更新的資源類型。 對於此終結點，值必須為 `libraries`。 |

{style="table-layout:auto"}

**回應**

成功的響應將返回更新的庫的詳細資訊。

```json
{
  "data": {
    "id": "LB80c337c956804738b2db2ea2f69fcdf0",
    "type": "libraries",
    "attributes": {
      "created_at": "2020-12-14T17:47:57.783Z",
      "name": "My Library",
      "published_at": null,
      "state": "submitted",
      "updated_at": "2020-12-14T17:48:06.431Z",
      "build_required": true
    },
    "relationships": {
      "builds": {
        "links": {
          "related": "https://reactor.adobe.io/libraries/LB80c337c956804738b2db2ea2f69fcdf0/builds"
        }
      },
      "environment": {
        "links": {
          "self": "https://reactor.adobe.io/libraries/LB80c337c956804738b2db2ea2f69fcdf0/relationships/environment"
        },
        "data": null
      },
      "data_elements": {
        "links": {
          "related": "https://reactor.adobe.io/libraries/LB80c337c956804738b2db2ea2f69fcdf0/data_elements",
          "self": "https://reactor.adobe.io/libraries/LB80c337c956804738b2db2ea2f69fcdf0/relationships/data_elements"
        }
      },
      "extensions": {
        "links": {
          "related": "https://reactor.adobe.io/libraries/LB80c337c956804738b2db2ea2f69fcdf0/extensions",
          "self": "https://reactor.adobe.io/libraries/LB80c337c956804738b2db2ea2f69fcdf0/relationships/extensions"
        }
      },
      "notes": {
        "links": {
          "related": "https://reactor.adobe.io/libraries/LB80c337c956804738b2db2ea2f69fcdf0/notes"
        }
      },
      "rules": {
        "links": {
          "related": "https://reactor.adobe.io/libraries/LB80c337c956804738b2db2ea2f69fcdf0/rules",
          "self": "https://reactor.adobe.io/libraries/LB80c337c956804738b2db2ea2f69fcdf0/relationships/rules"
        }
      },
      "upstream_library": {
        "data": null
      },
      "property": {
        "links": {
          "related": "https://reactor.adobe.io/libraries/LB80c337c956804738b2db2ea2f69fcdf0/property"
        },
        "data": {
          "id": "PRbc84c93c1c9f48c9836ade5ea4199006",
          "type": "properties"
        }
      },
      "last_build": {
        "links": {
          "related": "https://reactor.adobe.io/libraries/LB80c337c956804738b2db2ea2f69fcdf0/last_build"
        },
        "data": {
          "id": "BL8d6e931f2f6d48ea96d6730122f13bcc",
          "type": "builds"
        }
      }
    },
    "links": {
      "property": "https://reactor.adobe.io/properties/PRbc84c93c1c9f48c9836ade5ea4199006",
      "self": "https://reactor.adobe.io/libraries/LB80c337c956804738b2db2ea2f69fcdf0"
    },
    "meta": {
      "build_status": null,
      "build_required_detail": "No build found since last state change"
    }
  }
}
```

## 發佈庫 {#publish}

>[!NOTE]
>
>只能將已批准的庫發佈到生產環境中。

要將庫發佈到生產，請確保已將生產環境添加到庫中，然後建立生成。

**API格式**

```http
POST /libraries/{LIBRARY_ID}/builds
```

| 參數 | 說明 |
| --- | --- |
| `LIBRARY_ID` | 的 `id` 你想發佈的庫。 |

{style="table-layout:auto"}

**要求**

此請求不需要負載。

```shell
curl -X POST \
  https://reactor.adobe.io/libraries/LB80c337c956804738b2db2ea2f69fcdf0/builds \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Content-Type: application/json'
```

**回應**

```json
{
  "data": {
    "id": "BL162b63703eb74c6bb3c12471e0062c05",
    "type": "builds",
    "attributes": {
      "created_at": "2020-12-14T17:48:18.731Z",
      "status": "pending",
      "updated_at": "2020-12-14T17:48:18.731Z",
      "token": "b223fc55df1c"
    },
    "relationships": {
      "data_elements": {
        "links": {
          "related": "https://reactor.adobe.io/builds/BL162b63703eb74c6bb3c12471e0062c05/data_elements"
        }
      },
      "extensions": {
        "links": {
          "related": "https://reactor.adobe.io/builds/BL162b63703eb74c6bb3c12471e0062c05/extensions"
        }
      },
      "rules": {
        "links": {
          "related": "https://reactor.adobe.io/builds/BL162b63703eb74c6bb3c12471e0062c05/rules"
        }
      },
      "environment": {
        "links": {
          "related": "https://reactor.adobe.io/builds/BL162b63703eb74c6bb3c12471e0062c05/environment"
        },
        "data": {
          "id": "EN5428335fff304c749f06a241db137a60",
          "type": "environments"
        }
      },
      "library": {
        "links": {
          "related": "https://reactor.adobe.io/builds/BL162b63703eb74c6bb3c12471e0062c05/library"
        },
        "data": {
          "id": "LBa937e62887e94d85b77cbe703f5dfc56",
          "type": "libraries"
        }
      },
      "property": {
        "links": {
          "related": "https://reactor.adobe.io/builds/BL162b63703eb74c6bb3c12471e0062c05/property"
        },
        "data": {
          "id": "PR7e2b7aaaffcb499398010ba964603415",
          "type": "properties"
        }
      }
    },
    "links": {
      "environment": "https://reactor.adobe.io/environments/EN5428335fff304c749f06a241db137a60",
      "library": "https://reactor.adobe.io/libraries/LBa937e62887e94d85b77cbe703f5dfc56",
      "self": "https://reactor.adobe.io/builds/BL162b63703eb74c6bb3c12471e0062c05"
    },
    "meta": {
      "artifact_url": "https://assets.adobedtm.com/staging/f9fd106ab399/8b659dd115cf/launch-5986a1b644a4-development.min.js",
      "direct_artifact_url": "https://assets.adobedtm.com/staging/f9fd106ab399/8b659dd115cf/b223fc55df1c/launch-5986a1b644a4-development.min.js",
      "archive": false,
      "host_type_of": "akamai"
    }
  }
}
```

## 管理庫的注釋 {#notes}

庫是「顯著」資源，這意味著您可以建立和檢索每個資源上基於文本的注釋。 查看 [notes endpoint guide（注釋終結點指南）](./notes.md) 的子菜單。

## 檢索庫的相關資源 {#related}

以下調用演示如何檢索庫的相關資源。 當 [查圖書館](#lookup)，這些關係列在 `relationships` 屬性。

查看 [關係指南](../guides/relationships.md) 的子菜單。

### 列出庫的相關資料元素 {#data-elements}

可以通過附加列出庫使用的資料元素 `/data_elements` 查找請求的路徑。

**API格式**

```http
GET  /libraries/{LIBRARY_ID}/data_elements
```

| 參數 | 說明 |
| --- | --- |
| `{LIBRARY_ID}` | 的 `id` 列出其資料元素的庫。 |

{style="table-layout:auto"}

**要求**

```shell
curl -X GET \
  https://reactor.adobe.io/libraries/LB5862ee2dc21b4646a5536c8d6edb0c84/data_elements \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**回應**

成功的響應返回使用指定庫的資料元素清單。

```json
{
  "data": [
    {
      "id": "DE4956628e8baa4b358cc592337049b37b",
      "type": "data_elements",
      "attributes": {
        "created_at": "2020-12-14T17:45:11.694Z",
        "deleted_at": null,
        "dirty": false,
        "enabled": true,
        "name": "My Data Element 2020-12-14 17:45:10 +0000",
        "published": false,
        "published_at": null,
        "revision_number": 1,
        "updated_at": "2020-12-14T17:45:11.694Z",
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
            "related": "https://reactor.adobe.io/data_elements/DE4956628e8baa4b358cc592337049b37b/libraries"
          }
        },
        "revisions": {
          "links": {
            "related": "https://reactor.adobe.io/data_elements/DE4956628e8baa4b358cc592337049b37b/revisions"
          }
        },
        "notes": {
          "links": {
            "related": "https://reactor.adobe.io/data_elements/DE4956628e8baa4b358cc592337049b37b/notes"
          }
        },
        "property": {
          "links": {
            "related": "https://reactor.adobe.io/data_elements/DE4956628e8baa4b358cc592337049b37b/property"
          },
          "data": {
            "id": "PR245ca5e560784249b2a88ef82f2851b6",
            "type": "properties"
          }
        },
        "origin": {
          "links": {
            "related": "https://reactor.adobe.io/data_elements/DE4956628e8baa4b358cc592337049b37b/origin"
          },
          "data": {
            "id": "DE4c027939f2004fdcb15e3b4099e70974",
            "type": "data_elements"
          }
        },
        "extension": {
          "links": {
            "related": "https://reactor.adobe.io/data_elements/DE4956628e8baa4b358cc592337049b37b/extension"
          },
          "data": {
            "id": "EX5942ffd7fac94428875bd664e397bd47",
            "type": "extensions"
          }
        },
        "updated_with_extension_package": {
          "links": {
            "related": "https://reactor.adobe.io/data_elements/DE4956628e8baa4b358cc592337049b37b/updated_with_extension_package"
          },
          "data": {
            "id": "EP75db2452065b44e2b8a38ca883ce369a",
            "type": "extension_packages"
          }
        },
        "updated_with_extension": {
          "links": {
            "related": "https://reactor.adobe.io/data_elements/DE4956628e8baa4b358cc592337049b37b/updated_with_extension"
          },
          "data": {
            "id": "EXbf411638b90843c486254b5ca0fe47d6",
            "type": "extensions"
          }
        }
      },
      "links": {
        "property": "https://reactor.adobe.io/properties/PR245ca5e560784249b2a88ef82f2851b6",
        "origin": "https://reactor.adobe.io/data_elements/DE4c027939f2004fdcb15e3b4099e70974",
        "self": "https://reactor.adobe.io/data_elements/DE4956628e8baa4b358cc592337049b37b",
        "extension": "https://reactor.adobe.io/extensions/EX5942ffd7fac94428875bd664e397bd47"
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

### 列出庫的相關擴展 {#extensions}

可通過附加列出庫使用的擴展 `/extensions` 查找請求的路徑。

**API格式**

```http
GET  /libraries/{LIBRARY_ID}/extensions
```

| 參數 | 說明 |
| --- | --- |
| `{LIBRARY_ID}` | 的 `id` 的子目錄。 |

{style="table-layout:auto"}

**要求**

```shell
curl -X GET \
  https://reactor.adobe.io/libraries/LB5862ee2dc21b4646a5536c8d6edb0c84/extensions \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**回應**

成功的響應返回使用指定庫的擴展的清單。

```json
{
  "data": [
    {
      "id": "EXac1e55883e5b47eb9a3589b311960677",
      "type": "extensions",
      "attributes": {
        "created_at": "2020-12-14T17:45:23.759Z",
        "deleted_at": null,
        "dirty": false,
        "enabled": true,
        "name": "kessel-test",
        "published": false,
        "published_at": null,
        "revision_number": 1,
        "updated_at": "2020-12-14T17:45:23.759Z",
        "delegate_descriptor_id": null,
        "display_name": "Kessel Test",
        "review_status": "unsubmitted",
        "version": "1.2.0",
        "settings": "{}"
      },
      "relationships": {
        "libraries": {
          "links": {
            "related": "https://reactor.adobe.io/extensions/EXac1e55883e5b47eb9a3589b311960677/libraries"
          }
        },
        "revisions": {
          "links": {
            "related": "https://reactor.adobe.io/extensions/EXac1e55883e5b47eb9a3589b311960677/revisions"
          }
        },
        "notes": {
          "links": {
            "related": "https://reactor.adobe.io/extensions/EXac1e55883e5b47eb9a3589b311960677/notes"
          }
        },
        "property": {
          "links": {
            "related": "https://reactor.adobe.io/extensions/EXac1e55883e5b47eb9a3589b311960677/property"
          },
          "data": {
            "id": "PR2d1f3ba867204dc7a4c17614d23bbab0",
            "type": "properties"
          }
        },
        "origin": {
          "links": {
            "related": "https://reactor.adobe.io/extensions/EXac1e55883e5b47eb9a3589b311960677/origin"
          },
          "data": {
            "id": "EX63cf3b91ec8146889759bbacb15627c3",
            "type": "extensions"
          }
        },
        "updated_with_extension_package": {
          "links": {
            "related": "https://reactor.adobe.io/extensions/EXac1e55883e5b47eb9a3589b311960677/updated_with_extension_package"
          },
          "data": {
            "id": "EP75db2452065b44e2b8a38ca883ce369a",
            "type": "extension_packages"
          }
        },
        "extension_package": {
          "links": {
            "related": "https://reactor.adobe.io/extensions/EXac1e55883e5b47eb9a3589b311960677/extension_package"
          },
          "data": {
            "id": "EP75db2452065b44e2b8a38ca883ce369a",
            "type": "extension_packages"
          }
        }
      },
      "links": {
        "property": "https://reactor.adobe.io/properties/PR2d1f3ba867204dc7a4c17614d23bbab0",
        "origin": "https://reactor.adobe.io/extensions/EX63cf3b91ec8146889759bbacb15627c3",
        "self": "https://reactor.adobe.io/extensions/EXac1e55883e5b47eb9a3589b311960677",
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

### 列出庫的相關規則 {#rules}

可通過附加列出庫使用的規則 `/rules` 查找請求的路徑。

**API格式**

```http
GET  /libraries/{LIBRARY_ID}/rules
```

| 參數 | 說明 |
| --- | --- |
| `{LIBRARY_ID}` | 的 `id` 列出其規則的庫。 |

{style="table-layout:auto"}

**要求**

```shell
curl -X GET \
  https://reactor.adobe.io/libraries/LB5862ee2dc21b4646a5536c8d6edb0c84/rules \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**回應**

成功的響應返回使用指定庫的規則清單。

```json
{
  "data": [
    {
      "id": "RL460e550125054fffb824cce56c8cb1ac",
      "type": "rules",
      "attributes": {
        "created_at": "2020-12-14T17:45:36.405Z",
        "deleted_at": null,
        "dirty": false,
        "enabled": true,
        "name": "Example Rule",
        "published": false,
        "published_at": null,
        "revision_number": 1,
        "updated_at": "2020-12-14T17:45:36.405Z",
        "review_status": "unsubmitted"
      },
      "relationships": {
        "libraries": {
          "links": {
            "related": "https://reactor.adobe.io/rules/RL460e550125054fffb824cce56c8cb1ac/libraries"
          }
        },
        "revisions": {
          "links": {
            "related": "https://reactor.adobe.io/rules/RL460e550125054fffb824cce56c8cb1ac/revisions"
          }
        },
        "notes": {
          "links": {
            "related": "https://reactor.adobe.io/rules/RL460e550125054fffb824cce56c8cb1ac/notes"
          }
        },
        "property": {
          "links": {
            "related": "https://reactor.adobe.io/rules/RL460e550125054fffb824cce56c8cb1ac/property"
          },
          "data": {
            "id": "PRa68d0d2c6e0a4ae380fb30f17f7c435d",
            "type": "properties"
          }
        },
        "origin": {
          "links": {
            "related": "https://reactor.adobe.io/rules/RL460e550125054fffb824cce56c8cb1ac/origin"
          },
          "data": {
            "id": "RL04911614524d463a9c115bea442bce72",
            "type": "rules"
          }
        },
        "rule_components": {
          "links": {
            "related": "https://reactor.adobe.io/rules/RL460e550125054fffb824cce56c8cb1ac/rule_components"
          }
        }
      },
      "links": {
        "property": "https://reactor.adobe.io/properties/PRa68d0d2c6e0a4ae380fb30f17f7c435d",
        "origin": "https://reactor.adobe.io/rules/RL04911614524d463a9c115bea442bce72",
        "self": "https://reactor.adobe.io/rules/RL460e550125054fffb824cce56c8cb1ac",
        "rule_components": "https://reactor.adobe.io/rules/RL460e550125054fffb824cce56c8cb1ac/rule_components"
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

### 查找庫的相關環境 {#related-environment}

可通過附加來查找庫所分配的環境 `/environment` 到GET請求的路徑。

**API格式**

```http
GET  /libraries/{LIBRARY_ID}/environment
```

| 參數 | 說明 |
| --- | --- |
| `{LIBRARY_ID}` | 的 `id` 你想查的那個圖書館。 |

{style="table-layout:auto"}

**要求**

```shell
curl -X GET \
  https://reactor.adobe.io/libraries/LB5862ee2dc21b4646a5536c8d6edb0c84/environment \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**回應**

成功的響應將返回指定庫所分配到的環境的詳細資訊。

```json
{
  "data": {
    "id": "ENe66122e6793641d8a8453f63c42e4270",
    "type": "environments",
    "attributes": {
      "archive": false,
      "created_at": "2020-12-14T17:39:12.484Z",
      "library_path": "f9fd106ab399/2df53b69e8a2",
      "library_name": "launch-1d2ffee7eef5-development.min.js",
      "library_entry_points": [
        {
          "library_name": "launch-1d2ffee7eef5-development.min.js",
          "minified": true,
          "references": [
            "f9fd106ab399/2df53b69e8a2/launch-1d2ffee7eef5-development.min.js"
          ],
          "license_path": "f9fd106ab399/2df53b69e8a2/launch-1d2ffee7eef5-development.js"
        },
        {
          "library_name": "launch-1d2ffee7eef5-development.js",
          "minified": false,
          "references": [
            "f9fd106ab399/2df53b69e8a2/launch-1d2ffee7eef5-development.js"
          ]
        }
      ],
      "name": "Development Environment A",
      "path": "https://assets.adobedtm.com/staging",
      "stage": "development",
      "updated_at": "2020-12-14T17:39:13.988Z",
      "status": "succeeded",
      "token": "1d2ffee7eef5"
    },
    "relationships": {
      "library": {
        "links": {
          "related": "https://reactor.adobe.io/environments/ENe66122e6793641d8a8453f63c42e4270/library"
        },
        "data": {
          "id": "LB52ccd7f1e99146999f90cb3bca4940a2",
          "type": "libraries"
        }
      },
      "builds": {
        "links": {
          "related": "https://reactor.adobe.io/environments/ENe66122e6793641d8a8453f63c42e4270/builds"
        }
      },
      "host": {
        "links": {
          "related": "https://reactor.adobe.io/environments/ENe66122e6793641d8a8453f63c42e4270/host",
          "self": "https://reactor.adobe.io/environments/ENe66122e6793641d8a8453f63c42e4270/relationships/host"
        },
        "data": {
          "id": "HT53a4ebcb177d431e8fd26929930de0af",
          "type": "hosts"
        }
      },
      "property": {
        "links": {
          "related": "https://reactor.adobe.io/environments/ENe66122e6793641d8a8453f63c42e4270/property"
        },
        "data": {
          "id": "PR79de7e0885a9451786f1bf4b9136a72c",
          "type": "properties"
        }
      }
    },
    "links": {
      "property": "https://reactor.adobe.io/properties/PR79de7e0885a9451786f1bf4b9136a72c",
      "self": "https://reactor.adobe.io/environments/ENe66122e6793641d8a8453f63c42e4270"
    },
    "meta": {
      "archive_encrypted": false
    }
  }
}
```

### 查找庫的相關屬性 {#property}

可以通過附加 `/property` 到GET請求的路徑。

**API格式**

```http
GET  /libraries/{LIBRARY_ID}/property
```

| 參數 | 說明 |
| --- | --- |
| `{LIBRARY_ID}` | 的 `id` 你想查的圖書館。 |

{style="table-layout:auto"}

**要求**

```shell
curl -X GET \
  https://reactor.adobe.io/libraries/LB5862ee2dc21b4646a5536c8d6edb0c84/property \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**回應**

成功的響應將返回擁有指定庫的屬性的詳細資訊。

```json
{
  "data": {
    "id": "PRb18ac8f8b69d4f99af43870e91c17543",
    "type": "properties",
    "attributes": {
      "created_at": "2020-12-14T17:51:56.180Z",
      "enabled": true,
      "name": "Kessel Example Property",
      "updated_at": "2020-12-14T17:51:56.180Z",
      "platform": "web",
      "development": false,
      "token": "9d97006b0f9b",
      "domains": [
        "example.com"
      ],
      "undefined_vars_return_empty": false,
      "rule_component_sequencing_enabled": false
    },
    "relationships": {
      "company": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PRb18ac8f8b69d4f99af43870e91c17543/company"
        },
        "data": {
          "id": "CO2bf094214ffd4785bb4bcf88c952a7c1",
          "type": "companies"
        }
      },
      "callbacks": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PRb18ac8f8b69d4f99af43870e91c17543/callbacks"
        }
      },
      "hosts": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PRb18ac8f8b69d4f99af43870e91c17543/hosts"
        }
      },
      "environments": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PRb18ac8f8b69d4f99af43870e91c17543/environments"
        }
      },
      "libraries": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PRb18ac8f8b69d4f99af43870e91c17543/libraries"
        }
      },
      "data_elements": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PRb18ac8f8b69d4f99af43870e91c17543/data_elements"
        }
      },
      "extensions": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PRb18ac8f8b69d4f99af43870e91c17543/extensions"
        }
      },
      "rules": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PRb18ac8f8b69d4f99af43870e91c17543/rules"
        }
      },
      "notes": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PRb18ac8f8b69d4f99af43870e91c17543/notes"
        }
      }
    },
    "links": {
      "company": "https://reactor.adobe.io/companies/CO2bf094214ffd4785bb4bcf88c952a7c1",
      "data_elements": "https://reactor.adobe.io/properties/PRb18ac8f8b69d4f99af43870e91c17543/data_elements",
      "environments": "https://reactor.adobe.io/properties/PRb18ac8f8b69d4f99af43870e91c17543/environments",
      "extensions": "https://reactor.adobe.io/properties/PRb18ac8f8b69d4f99af43870e91c17543/extensions",
      "rules": "https://reactor.adobe.io/properties/PRb18ac8f8b69d4f99af43870e91c17543/rules",
      "self": "https://reactor.adobe.io/properties/PRb18ac8f8b69d4f99af43870e91c17543"
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

### 在上游查找庫 {#upstream}

可通過附加從庫上游查找下一個庫 `/upstream_library` 到GET請求的路徑。

**API格式**

```http
GET  /libraries/{LIBRARY_ID}/upstream_library
```

| 參數 | 說明 |
| --- | --- |
| `{LIBRARY_ID}` | 的 `id` 你要查的上游圖書館。 |

{style="table-layout:auto"}

**要求**

```shell
curl -X GET \
  https://reactor.adobe.io/libraries/LB5862ee2dc21b4646a5536c8d6edb0c84/upstream_library \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**回應**

成功的響應返回上游庫的詳細資訊。

```json
{
  "data": {
    "id": "LB29cc2f86b3684e00a10d196a60f4b0c0",
    "type": "libraries",
    "attributes": {
      "created_at": "2020-12-14T17:49:32.459Z",
      "name": "My Library",
      "published_at": null,
      "state": "submitted",
      "updated_at": "2020-12-14T17:49:41.070Z",
      "build_required": true
    },
    "relationships": {
      "builds": {
        "links": {
          "related": "https://reactor.adobe.io/libraries/LB29cc2f86b3684e00a10d196a60f4b0c0/builds"
        }
      },
      "environment": {
        "links": {
          "self": "https://reactor.adobe.io/libraries/LB29cc2f86b3684e00a10d196a60f4b0c0/relationships/environment"
        },
        "data": null
      },
      "data_elements": {
        "links": {
          "related": "https://reactor.adobe.io/libraries/LB29cc2f86b3684e00a10d196a60f4b0c0/data_elements",
          "self": "https://reactor.adobe.io/libraries/LB29cc2f86b3684e00a10d196a60f4b0c0/relationships/data_elements"
        }
      },
      "extensions": {
        "links": {
          "related": "https://reactor.adobe.io/libraries/LB29cc2f86b3684e00a10d196a60f4b0c0/extensions",
          "self": "https://reactor.adobe.io/libraries/LB29cc2f86b3684e00a10d196a60f4b0c0/relationships/extensions"
        }
      },
      "notes": {
        "links": {
          "related": "https://reactor.adobe.io/libraries/LB29cc2f86b3684e00a10d196a60f4b0c0/notes"
        }
      },
      "rules": {
        "links": {
          "related": "https://reactor.adobe.io/libraries/LB29cc2f86b3684e00a10d196a60f4b0c0/rules",
          "self": "https://reactor.adobe.io/libraries/LB29cc2f86b3684e00a10d196a60f4b0c0/relationships/rules"
        }
      },
      "upstream_library": {
        "data": null
      },
      "property": {
        "links": {
          "related": "https://reactor.adobe.io/libraries/LB29cc2f86b3684e00a10d196a60f4b0c0/property"
        },
        "data": {
          "id": "PR7c206ed399644222aef329488cee7fa7",
          "type": "properties"
        }
      },
      "last_build": {
        "links": {
          "related": "https://reactor.adobe.io/libraries/LB29cc2f86b3684e00a10d196a60f4b0c0/last_build"
        },
        "data": {
          "id": "BL87cde018ecd44ac7a20b0271ab06d04b",
          "type": "builds"
        }
      }
    },
    "links": {
      "property": "https://reactor.adobe.io/properties/PR7c206ed399644222aef329488cee7fa7",
      "self": "https://reactor.adobe.io/libraries/LB29cc2f86b3684e00a10d196a60f4b0c0"
    },
    "meta": {
      "build_status": null,
      "build_required_detail": "No build found since last state change"
    }
  }
}
```
