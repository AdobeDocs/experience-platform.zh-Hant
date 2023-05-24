---
title: 環境終結點
description: 瞭解如何調用Reactor API中的/environments端點。
exl-id: 4c22f799-8338-4cf0-980a-3900d725ab5d
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '1002'
ht-degree: 4%

---

# 環境終結點

當 [庫](./libraries.md) 編譯成 [構建](./builds.md) 在Reactor API中，生成的確切內容取決於環境設定和庫中包含的資源。 具體來說，環境確定了以下內容：

1. **目標**:要部署生成的位置。 通過選擇 [主機](./hosts.md) 供環境使用。
1. **存檔**:您可以選擇將生成作為可部署的檔案集進行檢索，或者將其壓縮為存檔格式。 此項由 `archive` 的下界。

環境配置的目標和存檔格式會更改您引用應用程式中生成的方式(該引用是 [嵌入代碼](../../ui/publishing/environments.md#embed-code))。 如果對目標或檔案格式進行了任何更改，則必須對應用程式進行匹配更新才能使用新引用。

環境分為三種類型（或階段），每種類型對您可以擁有的總數量有不同的限制：

| 環境類型 | 允許的編號 |
| --- | --- |
| 開發 | （無限制） |
| 預備 | 一 |
| 生產 | 一 |

{style="table-layout:auto"}

這些環境類型具有相似的行為，但在 [標籤發佈工作流](../../ui/publishing/publishing-flow.md)。

環境正好屬於 [屬性](./properties.md)。

有關環境的更多一般資訊，請參見 [環境](../../ui/publishing/environments.md) 在發佈文檔中。

## 快速入門

本指南中使用的端點是 [反應堆API](https://www.adobe.io/experience-platform-apis/references/reactor/)。 在繼續之前，請查看 [入門指南](../getting-started.md) 有關如何驗證到API的重要資訊。

## 檢索環境清單 {#list}

通過將屬性的ID包括在GET請求的路徑中，可以檢索屬性的環境清單。

**API格式**

```http
GET /properties/{PROPERTY_ID}/environments
```

| 參數 | 說明 |
| --- | --- |
| `PROPERTY_ID` | 的 `id` 擁有環境的財產。 |

{style="table-layout:auto"}

>[!NOTE]
>
>使用查詢參數，可以根據以下屬性篩選列出的環境：<ul><li>`archive`</li><li>`created_at`</li><li>`name`</li><li>`stage`</li><li>`token`</li><li>`updated_at`</li></ul>請參閱上的指南 [過濾響應](../guides/filtering.md) 的子菜單。

**要求**

```shell
curl -X GET \
  https://reactor.adobe.io/properties/PR97d92a379a5f48758947cdf44f607a0d/environments \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**回應**

成功的響應將返回指定屬性的環境清單。

```json
{
  "data": [
    {
      "id": "ENbe322acb4fc64dfdb603254ffe98b5d3",
      "type": "environments",
      "attributes": {
        "archive": false,
        "created_at": "2020-12-14T17:38:51.047Z",
        "library_path": "f9fd106ab399/cb29d726b35e",
        "library_name": "launch-c0331746ae03-development.min.js",
        "library_entry_points": [
          {
            "library_name": "launch-c0331746ae03-development.min.js",
            "minified": true,
            "references": [
              "f9fd106ab399/cb29d726b35e/launch-c0331746ae03-development.min.js"
            ],
            "license_path": "f9fd106ab399/cb29d726b35e/launch-c0331746ae03-development.js"
          },
          {
            "library_name": "launch-c0331746ae03-development.js",
            "minified": false,
            "references": [
              "f9fd106ab399/cb29d726b35e/launch-c0331746ae03-development.js"
            ]
          }
        ],
        "name": "Development Environment A",
        "path": "https://assets.adobedtm.com/staging",
        "stage": "development",
        "updated_at": "2020-12-14T17:38:51.047Z",
        "status": "succeeded",
        "token": "c0331746ae03"
      },
      "relationships": {
        "library": {
          "links": {
            "related": "https://reactor.adobe.io/environments/ENbe322acb4fc64dfdb603254ffe98b5d3/library"
          },
          "data": null
        },
        "builds": {
          "links": {
            "related": "https://reactor.adobe.io/environments/ENbe322acb4fc64dfdb603254ffe98b5d3/builds"
          }
        },
        "host": {
          "links": {
            "related": "https://reactor.adobe.io/environments/ENbe322acb4fc64dfdb603254ffe98b5d3/host",
            "self": "https://reactor.adobe.io/environments/ENbe322acb4fc64dfdb603254ffe98b5d3/relationships/host"
          },
          "data": {
            "id": "HTc5cae9ce1e3943aab185bdba939f98bd",
            "type": "hosts"
          }
        },
        "property": {
          "links": {
            "related": "https://reactor.adobe.io/environments/ENbe322acb4fc64dfdb603254ffe98b5d3/property"
          },
          "data": {
            "id": "PR06c9196bc57048dd8ff169c27baeeca8",
            "type": "properties"
          }
        }
      },
      "links": {
        "property": "https://reactor.adobe.io/properties/PR06c9196bc57048dd8ff169c27baeeca8",
        "self": "https://reactor.adobe.io/environments/ENbe322acb4fc64dfdb603254ffe98b5d3"
      },
      "meta": {
        "archive_encrypted": false
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

## 查找環境 {#lookup}

您可以通過在GET請求的路徑中提供其ID來查找環境。

**API格式**

```http
GET /environments/{ENVIRONMENT_ID}
```

| 參數 | 說明 |
| --- | --- |
| `ENVIRONMENT_ID` | 的 `id` 你想查的環境。 |

{style="table-layout:auto"}

**要求**

```shell
curl -X GET \
  https://reactor.adobe.io/environments/ENb0c1fbfdc1fd4b8593bfd269f827b3e6 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**回應**

成功的響應將返回環境的詳細資訊。

```json
{
  "data": {
    "id": "ENb0c1fbfdc1fd4b8593bfd269f827b3e6",
    "type": "environments",
    "attributes": {
      "archive": false,
      "created_at": "2020-12-14T17:38:30.378Z",
      "library_path": "f9fd106ab399/2f67fccade5e",
      "library_name": "launch-4436c89f6839-development.min.js",
      "library_entry_points": [
        {
          "library_name": "launch-4436c89f6839-development.min.js",
          "minified": true,
          "references": [
            "f9fd106ab399/2f67fccade5e/launch-4436c89f6839-development.min.js"
          ],
          "license_path": "f9fd106ab399/2f67fccade5e/launch-4436c89f6839-development.js"
        },
        {
          "library_name": "launch-4436c89f6839-development.js",
          "minified": false,
          "references": [
            "f9fd106ab399/2f67fccade5e/launch-4436c89f6839-development.js"
          ]
        }
      ],
      "name": "Development Environment A",
      "path": "https://assets.adobedtm.com/staging",
      "stage": "development",
      "updated_at": "2020-12-14T17:38:30.378Z",
      "status": "succeeded",
      "token": "4436c89f6839"
    },
    "relationships": {
      "library": {
        "links": {
          "related": "https://reactor.adobe.io/environments/ENb0c1fbfdc1fd4b8593bfd269f827b3e6/library"
        },
        "data": null
      },
      "builds": {
        "links": {
          "related": "https://reactor.adobe.io/environments/ENb0c1fbfdc1fd4b8593bfd269f827b3e6/builds"
        }
      },
      "host": {
        "links": {
          "related": "https://reactor.adobe.io/environments/ENb0c1fbfdc1fd4b8593bfd269f827b3e6/host",
          "self": "https://reactor.adobe.io/environments/ENb0c1fbfdc1fd4b8593bfd269f827b3e6/relationships/host"
        },
        "data": {
          "id": "HTecb76453c8284f84a3c55fe981b5e6c9",
          "type": "hosts"
        }
      },
      "property": {
        "links": {
          "related": "https://reactor.adobe.io/environments/ENb0c1fbfdc1fd4b8593bfd269f827b3e6/property"
        },
        "data": {
          "id": "PRadbee4fb64754081a945ed2a5b66627a",
          "type": "properties"
        }
      }
    },
    "links": {
      "property": "https://reactor.adobe.io/properties/PRadbee4fb64754081a945ed2a5b66627a",
      "self": "https://reactor.adobe.io/environments/ENb0c1fbfdc1fd4b8593bfd269f827b3e6"
    },
    "meta": {
      "archive_encrypted": false
    }
  }
}
```

## 建立環境 {#create}

可以通過發出POST請求來建立新環境。

**API格式**

```http
POST /properties/{PROPERTY_ID}/environments
```

| 參數 | 說明 |
| --- | --- |
| `PROPERTY_ID` | 的 `id` 的 [屬性](./properties.md) 定義環境。 |

{style="table-layout:auto"}

**要求**

以下請求為指定的屬性建立新環境。 此調用還通過以下方式將環境與現有主機關聯： `relationships` 屬性。 請參閱上的指南 [關係](../guides/relationships.md) 的子菜單。

```shell
curl -X POST \
  https://reactor.adobe.io/properties/PR97d92a379a5f48758947cdf44f607a0d/environments \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Content-Type: application/json' \
  -d '{
        "data": {
          "attributes": {
            "name": "Development Environment A",
            "archive": true,
            "archive_passphrase": "pass12345",
            "path": "/development-a",
            "stage": "development"
          },
          "relationships": {
            "host": {
              "data": {
                "id": "HT5d3fbe7bd34d4f65a46fad4598aefd4e",
                "type": "hosts"
              }
            }
          },
          "type": "environments"
        }
      }'
```

| 屬性 | 說明 |
| --- | --- |
| `attributes.name` | **（必需）** 環境的可讀名稱。 |
| `attributes.archive` | 一個布爾值，指示該生成是否為存檔格式。 |
| `attributes.archive_passphrase` | 可用於解鎖存檔檔案的字串密碼。 |
| `attributes.path` | 來自環境的主機URL的路徑。 |
| `attributes.stage` | 環境的階段（開發、試運行或生產）。 |
| `id` | 的 `id` 的下界。 這應與 `{ENVIRONMENT_ID}` 請求路徑中提供的值。 |
| `type` | 要更新的資源類型。 對於此終結點，值必須為 `environments`。 |

{style="table-layout:auto"}

**回應**

成功的響應將返回新建立環境的詳細資訊。

```json
{
  "data": {
    "id": "EN867c480dc5ea4158be3ea68e5543bd85",
    "type": "environments",
    "attributes": {
      "archive": false,
      "created_at": "2020-12-14T17:31:57.857Z",
      "library_path": "f9fd106ab399/bd007122e3e3",
      "library_name": "launch-4d5a31f6ca53-development.min.js",
      "library_entry_points": [
        {
          "library_name": "launch-4d5a31f6ca53-development.min.js",
          "minified": true,
          "references": [
            "f9fd106ab399/bd007122e3e3/launch-4d5a31f6ca53-development.min.js"
          ],
          "license_path": "f9fd106ab399/bd007122e3e3/launch-4d5a31f6ca53-development.js"
        },
        {
          "library_name": "launch-4d5a31f6ca53-development.js",
          "minified": false,
          "references": [
            "f9fd106ab399/bd007122e3e3/launch-4d5a31f6ca53-development.js"
          ]
        }
      ],
      "name": "Development Environment A",
      "path": "https://assets.adobedtm.com/staging",
      "stage": "development",
      "updated_at": "2020-12-14T17:31:57.857Z",
      "status": "succeeded",
      "token": "4d5a31f6ca53"
    },
    "relationships": {
      "library": {
        "links": {
          "related": "https://reactor.adobe.io/environments/EN867c480dc5ea4158be3ea68e5543bd85/library"
        },
        "data": null
      },
      "builds": {
        "links": {
          "related": "https://reactor.adobe.io/environments/EN867c480dc5ea4158be3ea68e5543bd85/builds"
        }
      },
      "host": {
        "links": {
          "related": "https://reactor.adobe.io/environments/EN867c480dc5ea4158be3ea68e5543bd85/host",
          "self": "https://reactor.adobe.io/environments/EN867c480dc5ea4158be3ea68e5543bd85/relationships/host"
        },
        "data": {
          "id": "HT5d3fbe7bd34d4f65a46fad4598aefd4e",
          "type": "hosts"
        }
      },
      "property": {
        "links": {
          "related": "https://reactor.adobe.io/environments/EN867c480dc5ea4158be3ea68e5543bd85/property"
        },
        "data": {
          "id": "PRa41874e4d1604efd9c3c67d7a123f4c6",
          "type": "properties"
        }
      }
    },
    "links": {
      "property": "https://reactor.adobe.io/properties/PRa41874e4d1604efd9c3c67d7a123f4c6",
      "self": "https://reactor.adobe.io/environments/EN867c480dc5ea4158be3ea68e5543bd85"
    },
    "meta": {
      "archive_encrypted": false
    }
  }
}
```

## 更新環境 {#update}

您可以通過將環境ID包含在PATCH請求的路徑中來更新環境。

**API格式**

```http
PATCH /environments/{ENVIRONMENT_ID}
```

| 參數 | 說明 |
| --- | --- |
| `ENVIRONMENT_ID` | 的 `id` 要更新的環境。 |

{style="table-layout:auto"}

**要求**

以下請求更新 `name` 的下界。

```shell
curl -X PATCH \
  https://reactor.adobe.io/environments/DE3fab176ccf8641838b3da59f716fc42b \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Content-Type: application/json' \
  -d '{
        "data": {
          "attributes": {
            "name": "New Environment Name"
          },
          "id": "ENeb00d8f62d244732bd27765301b1410f",
          "type": "environments"
        }
      }'
```

| 屬性 | 說明 |
| --- | --- |
| `attributes` | 其屬性表示要為環境更新的屬性的對象。 可以更新以下環境屬性： <ul><li>`archive`</li><li>`archive_passphrase`</li><li>`include_debug_library`</li><li>`name`</li><li>`path`</li></ul> 請參閱的示例調用 [建立環境](#create) 的子菜單。 |
| `id` | 的 `id` 的下界。 這應與 `{ENVIRONMENT_ID}` 請求路徑中提供的值。 |
| `type` | 要更新的資源類型。 對於此終結點，值必須為 `environments`。 |

{style="table-layout:auto"}

**回應**

成功的響應將返回更新環境的詳細資訊。

```json
{
  "data": {
    "id": "ENeb00d8f62d244732bd27765301b1410f",
    "type": "environments",
    "attributes": {
      "archive": false,
      "created_at": "2020-12-14T17:38:40.608Z",
      "library_path": "f9fd106ab399/1eb59e88f015",
      "library_name": "launch-caa955ee58ff-development.min.js",
      "library_entry_points": [
        {
          "library_name": "launch-caa955ee58ff-development.min.js",
          "minified": true,
          "references": [
            "f9fd106ab399/1eb59e88f015/launch-caa955ee58ff-development.min.js"
          ],
          "license_path": "f9fd106ab399/1eb59e88f015/launch-caa955ee58ff-development.js"
        },
        {
          "library_name": "launch-caa955ee58ff-development.js",
          "minified": false,
          "references": [
            "f9fd106ab399/1eb59e88f015/launch-caa955ee58ff-development.js"
          ]
        }
      ],
      "name": "New environment name",
      "path": "https://assets.adobedtm.com/staging",
      "stage": "development",
      "updated_at": "2020-12-14T17:38:41.210Z",
      "status": "succeeded",
      "token": "caa955ee58ff"
    },
    "relationships": {
      "library": {
        "links": {
          "related": "https://reactor.adobe.io/environments/ENeb00d8f62d244732bd27765301b1410f/library"
        },
        "data": null
      },
      "builds": {
        "links": {
          "related": "https://reactor.adobe.io/environments/ENeb00d8f62d244732bd27765301b1410f/builds"
        }
      },
      "host": {
        "links": {
          "related": "https://reactor.adobe.io/environments/ENeb00d8f62d244732bd27765301b1410f/host",
          "self": "https://reactor.adobe.io/environments/ENeb00d8f62d244732bd27765301b1410f/relationships/host"
        },
        "data": {
          "id": "HT7ea0b7c5c556476bafae8240da2d657d",
          "type": "hosts"
        }
      },
      "property": {
        "links": {
          "related": "https://reactor.adobe.io/environments/ENeb00d8f62d244732bd27765301b1410f/property"
        },
        "data": {
          "id": "PR558b6514e529409fa740a34e5f974dd8",
          "type": "properties"
        }
      }
    },
    "links": {
      "property": "https://reactor.adobe.io/properties/PR558b6514e529409fa740a34e5f974dd8",
      "self": "https://reactor.adobe.io/environments/ENeb00d8f62d244732bd27765301b1410f"
    },
    "meta": {
      "archive_encrypted": false
    }
  }
}
```

## 刪除環境

可以通過將環境ID包含在DELETE請求的路徑中來刪除環境。

**API格式**

```http
DELETE /environments/{ENVIRONMENT_ID}
```

| 參數 | 說明 |
| --- | --- |
| `ENVIRONMENT_ID` | 的 `id` 的子菜單。 |

{style="table-layout:auto"}

**要求**

```shell
curl -X DELETE \
  https://reactor.adobe.io/environments/ENeb00d8f62d244732bd27765301b1410f \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}'
```

**回應**

成功的響應返回沒有響應正文的HTTP狀態204（無內容），表示該環境已被刪除。

## 檢索環境的相關資源 {#related}

以下調用演示如何檢索環境的相關資源。 當 [查找環境](#lookup)，這些關係列在 `relationships` 屬性。

查看 [關係指南](../guides/relationships.md) 的子菜單。

### 列出環境的相關生成 {#builds}

可通過附加來列出使用環境的生成 `/builds` 查找請求的路徑。

**API格式**

```http
GET  /environments/{ENVIRONMENT_ID}/builds
```

| 參數 | 說明 |
| --- | --- |
| `{ENVIRONMENT_ID}` | 的 `id` 要列出其生成的環境。 |

{style="table-layout:auto"}

**要求**

```shell
curl -X GET \
  https://reactor.adobe.io/environments/ENeb00d8f62d244732bd27765301b1410f/builds \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**回應**

成功的響應返回使用指定環境的生成清單。

```json
{
  "data": [
    {
      "id": "BL775f919553aa4c6c8116cbf1da8baec8",
      "type": "builds",
      "attributes": {
        "created_at": "2020-12-14T17:32:43.113Z",
        "status": "pending",
        "updated_at": "2020-12-14T17:32:43.113Z",
        "token": "983989bcdad4"
      },
      "relationships": {
        "data_elements": {
          "links": {
            "related": "https://reactor.adobe.io/builds/BL775f919553aa4c6c8116cbf1da8baec8/data_elements"
          }
        },
        "extensions": {
          "links": {
            "related": "https://reactor.adobe.io/builds/BL775f919553aa4c6c8116cbf1da8baec8/extensions"
          }
        },
        "rules": {
          "links": {
            "related": "https://reactor.adobe.io/builds/BL775f919553aa4c6c8116cbf1da8baec8/rules"
          }
        },
        "environment": {
          "links": {
            "related": "https://reactor.adobe.io/builds/BL775f919553aa4c6c8116cbf1da8baec8/environment"
          },
          "data": {
            "id": "ENd8b1aee9d1674e7aa6135752ce839f82",
            "type": "environments"
          }
        },
        "library": {
          "links": {
            "related": "https://reactor.adobe.io/builds/BL775f919553aa4c6c8116cbf1da8baec8/library"
          },
          "data": {
            "id": "LB9bca25483e0849a089524c5ca655f2fe",
            "type": "libraries"
          }
        },
        "property": {
          "links": {
            "related": "https://reactor.adobe.io/builds/BL775f919553aa4c6c8116cbf1da8baec8/property"
          },
          "data": {
            "id": "PRbe32d7f41b2741ecae1c06f6fd2d3906",
            "type": "properties"
          }
        }
      },
      "links": {
        "environment": "https://reactor.adobe.io/environments/ENd8b1aee9d1674e7aa6135752ce839f82",
        "library": "https://reactor.adobe.io/libraries/LB9bca25483e0849a089524c5ca655f2fe",
        "self": "https://reactor.adobe.io/builds/BL775f919553aa4c6c8116cbf1da8baec8"
      },
      "meta": {
        "artifact_url": "https://assets.adobedtm.com/staging/f9fd106ab399/70ee12a3f313/launch-d481f2d29bd0-development.min.js",
        "direct_artifact_url": "https://assets.adobedtm.com/staging/f9fd106ab399/70ee12a3f313/983989bcdad4/launch-d481f2d29bd0-development.min.js",
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

### 查找環境的相關主機 {#host}

可以通過附加 `/host` 到GET請求的路徑。

>[!NOTE]
>
>您可以通過 [單獨呼叫](#host-relationship)。

**API格式**

```http
GET  /environments/{ENVIRONMENT_ID}/host
```

| 參數 | 說明 |
| --- | --- |
| `{ENVIRONMENT_ID}` | 的 `id` 要查找其主機的環境。 |

{style="table-layout:auto"}

**要求**

```shell
curl -X GET \
  https://reactor.adobe.io/environments/ENeb00d8f62d244732bd27765301b1410f/host \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**回應**

成功的響應返回使用指定環境的主機的詳細資訊。

```json
{
  "data": {
    "id": "HT621241cf4fbb4f7da5b6415ee1b15ac0",
    "type": "hosts",
    "attributes": {
      "created_at": "2020-12-14T17:43:05.382Z",
      "server": null,
      "name": "Example Akamai Host",
      "path": null,
      "port": null,
      "status": "succeeded",
      "type_of": "akamai",
      "updated_at": "2020-12-14T17:43:05.382Z",
      "username": null
    },
    "relationships": {
      "property": {
        "links": {
          "related": "https://reactor.adobe.io/hosts/HT621241cf4fbb4f7da5b6415ee1b15ac0/property"
        },
        "data": {
          "id": "PR50586546f7764fc59997342b8ff7647c",
          "type": "properties"
        }
      }
    },
    "links": {
      "property": "https://reactor.adobe.io/properties/PR50586546f7764fc59997342b8ff7647c",
      "self": "https://reactor.adobe.io/hosts/HT621241cf4fbb4f7da5b6415ee1b15ac0"
    }
  }
}
```

### 查找環境的相關庫 {#library}

可通過附加 `/library` 到GET請求的路徑。

**API格式**

```http
GET  /environments/{ENVIRONMENT_ID}/library
```

| 參數 | 說明 |
| --- | --- |
| `{ENVIRONMENT_ID}` | 的 `id` 你要查找的環境。 |

{style="table-layout:auto"}

**要求**

```shell
curl -X GET \
  https://reactor.adobe.io/environments/ENeb00d8f62d244732bd27765301b1410f/library \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**回應**

成功的響應返回使用指定環境的庫的詳細資訊。

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

### 查找環境的相關屬性 {#property}

可通過附加 `/property` 到GET請求的路徑。

**API格式**

```http
GET  /environments/{ENVIRONMENT_ID}/property
```

| 參數 | 說明 |
| --- | --- |
| `{ENVIRONMENT_ID}` | 的 `id` 你想查的環境。 |

{style="table-layout:auto"}

**要求**

```shell
curl -X GET \
  https://reactor.adobe.io/environments/ENeb00d8f62d244732bd27765301b1410f/property \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**回應**

成功的響應將返回擁有指定環境的屬性的詳細資訊。

```json
{
  "data": {
    "id": "PR7688dba9f1384507bbd20f10947536f2",
    "type": "properties",
    "attributes": {
      "created_at": "2020-12-14T17:52:55.254Z",
      "enabled": true,
      "name": "Kessel Example Property",
      "updated_at": "2020-12-14T17:52:55.254Z",
      "platform": "web",
      "development": false,
      "token": "9611419d84a4",
      "domains": [
        "example.com"
      ],
      "undefined_vars_return_empty": false,
      "rule_component_sequencing_enabled": false
    },
    "relationships": {
      "company": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR7688dba9f1384507bbd20f10947536f2/company"
        },
        "data": {
          "id": "CO2bf094214ffd4785bb4bcf88c952a7c1",
          "type": "companies"
        }
      },
      "callbacks": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR7688dba9f1384507bbd20f10947536f2/callbacks"
        }
      },
      "hosts": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR7688dba9f1384507bbd20f10947536f2/hosts"
        }
      },
      "environments": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR7688dba9f1384507bbd20f10947536f2/environments"
        }
      },
      "libraries": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR7688dba9f1384507bbd20f10947536f2/libraries"
        }
      },
      "data_elements": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR7688dba9f1384507bbd20f10947536f2/data_elements"
        }
      },
      "extensions": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR7688dba9f1384507bbd20f10947536f2/extensions"
        }
      },
      "rules": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR7688dba9f1384507bbd20f10947536f2/rules"
        }
      },
      "notes": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR7688dba9f1384507bbd20f10947536f2/notes"
        }
      }
    },
    "links": {
      "company": "https://reactor.adobe.io/companies/CO2bf094214ffd4785bb4bcf88c952a7c1",
      "data_elements": "https://reactor.adobe.io/properties/PR7688dba9f1384507bbd20f10947536f2/data_elements",
      "environments": "https://reactor.adobe.io/properties/PR7688dba9f1384507bbd20f10947536f2/environments",
      "extensions": "https://reactor.adobe.io/properties/PR7688dba9f1384507bbd20f10947536f2/extensions",
      "rules": "https://reactor.adobe.io/properties/PR7688dba9f1384507bbd20f10947536f2/rules",
      "self": "https://reactor.adobe.io/properties/PR7688dba9f1384507bbd20f10947536f2"
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
