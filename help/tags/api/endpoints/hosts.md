---
title: 主機端點
description: 了解如何在Reactor API中呼叫/hosts端點。
source-git-commit: 8133804076b1c0adf2eae5b748e86a35f3186d14
workflow-type: tm+mt
source-wordcount: '765'
ht-degree: 7%

---

# 主機端點

>[!NOTE]
>
>本檔案說明如何在Reactor API中管理主機。 如需標籤之主機的詳細一般資訊，請參閱發佈檔案中[hosts overview](../../ui/publishing/hosts/hosts-overview.md)的指南。

在Reactor API中，主機定義可傳送[build](./builds.md)的目的地。

當Adobe Experience Platform中的標籤使用者要求建立時，系統會檢查程式庫，以判斷應建置程式庫的[environment](./environments.md)。 每個環境都與主機有關係，指出要傳送組建的位置。

主機只屬於一個[屬性](./properties.md)，而一個屬性可以有許多主機。 屬性至少必須有一個主機，您才能發佈。

一個屬性內的多個環境可以使用主機。 在屬性上常有單一主機，且該屬性上的所有環境都使用相同主機。

## 快速入門

本指南中使用的端點是[Reactor API](https://www.adobe.io/experience-platform-apis/references/reactor/)的一部分。 繼續操作之前，請參閱[快速入門手冊](../getting-started.md)，了解如何驗證API的重要資訊。

## 擷取主機清單 {#list}

您可以在GET請求的路徑中加入屬性的ID，以擷取屬性的主機清單。

**API格式**

```http
GET /properties/{PROPERTY_ID}/hosts
```

| 參數 | 說明 |
| --- | --- |
| `PROPERTY_ID` | 擁有主機的屬性的`id`。 |

{style=&quot;table-layout:auto&quot;}

>[!NOTE]
>
>您可以使用查詢參數，根據下列屬性來篩選列出的主機：<ul><li>`created_at`</li><li>`name`</li><li>`type_of`</li><li>`updated_at`</li></ul>如需詳細資訊，請參閱[篩選回應](../guides/filtering.md)的指南。

**要求**

```shell
curl -X GET \
  https://reactor.adobe.io/properties/PRd428c2a25caa4b32af61495f5809b737/hosts \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**回應**

成功的響應返回指定屬性的主機清單。

```json
{
  "data": [
    {
      "id": "HT405b8d9306004eb38106e66c8a4afc09",
      "type": "hosts",
      "attributes": {
        "created_at": "2020-12-14T17:42:35.239Z",
        "server": null,
        "name": "Example Akamai Host",
        "path": null,
        "port": null,
        "status": "succeeded",
        "type_of": "akamai",
        "updated_at": "2020-12-14T17:42:35.239Z",
        "username": null
      },
      "relationships": {
        "property": {
          "links": {
            "related": "https://reactor.adobe.io/hosts/HT405b8d9306004eb38106e66c8a4afc09/property"
          },
          "data": {
            "id": "PRd428c2a25caa4b32af61495f5809b737",
            "type": "properties"
          }
        }
      },
      "links": {
        "property": "https://reactor.adobe.io/properties/PRd428c2a25caa4b32af61495f5809b737",
        "self": "https://reactor.adobe.io/hosts/HT405b8d9306004eb38106e66c8a4afc09"
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

## 查找主機 {#lookup}

您可以在請求的路徑中提供主機ID，以便查詢GET。

**API格式**

```http
GET /hosts/{HOST_ID}
```

| 參數 | 說明 |
| --- | --- |
| `HOST_ID` | 要查找的主機的`id`。 |

{style=&quot;table-layout:auto&quot;}

**要求**

```shell
curl -X GET \
  https://reactor.adobe.io/hosts/HT5d90148e72224224aac9bc0b01498b84 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**回應**

成功的回應會傳回主機的詳細資訊。

```json
{
  "data": {
    "id": "HT5d90148e72224224aac9bc0b01498b84",
    "type": "hosts",
    "attributes": {
      "created_at": "2020-12-14T17:42:25.353Z",
      "server": "https://server.example.com",
      "name": "Example Akamai Host",
      "path": "/akamai",
      "port": 8000,
      "status": "succeeded",
      "type_of": "akamai",
      "updated_at": "2020-12-14T17:42:25.353Z",
      "username": null
    },
    "relationships": {
      "property": {
        "links": {
          "related": "https://reactor.adobe.io/hosts/HT5d90148e72224224aac9bc0b01498b84/property"
        },
        "data": {
          "id": "PRd7cf174259f34057b5c435ef873a79bf",
          "type": "properties"
        }
      }
    },
    "links": {
      "property": "https://reactor.adobe.io/properties/PRd7cf174259f34057b5c435ef873a79bf",
      "self": "https://reactor.adobe.io/hosts/HT5d90148e72224224aac9bc0b01498b84"
    }
  }
}
```

## 建立主機 {#create}

您可以提出POST要求來建立新主機。

**API格式**

```http
POST /properties/{PROPERTY_ID}/hosts
```

| 參數 | 說明 |
| --- | --- |
| `PROPERTY_ID` | 要在下定義主機的[property](./properties.md)的`id`。 |

{style=&quot;table-layout:auto&quot;}

**要求**

下列請求會為指定的屬性建立新主機。 呼叫也會透過`relationships`屬性將主機與現有擴充功能建立關聯。 有關詳細資訊，請參閱[relationships](../guides/relationships.md)上的指南。

```shell
curl -X POST \
  https://reactor.adobe.io/properties/PRb25a704c0b7c4562835ccdf96d3afd31/hosts \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'Content-Type: application/json' \
  -d '{
        "data": {
          "attributes": {
            "name": "Example SFTP Host",
            "type_of": "sftp",
            "username": "John Doe",
            "encrypted_private_key": "{PRIVATE_KEY}",
            "server": "https://example.com",
            "path": "assets",
            "port": 22
          },
          "type": "hosts"
        }
      }'
```

| 屬性 | 說明 |
| --- | --- |
| `attributes.name` | **（必要）** 主機的人類看得懂的名稱。 |
| `attributes.type_of` | **（必要）** 主機的類型。可以是下列兩個選項之一： <ul><li>`akamai` 針對 [Adobe管理主機](../../ui/publishing/hosts/managed-by-adobe-host.md)</li><li>`sftp` (適 [用於SFTP主機)](../../ui/publishing/hosts/sftp-host.md)</li></ul> |
| `attributes.encrypted_private_key` | 用於主機驗證的可選私鑰。 |
| `attributes.path` | 附加至`server` URL的路徑。 |
| `attributes.port` | 一個整數，用於指示要使用的特定伺服器埠。 |
| `attributes.server` | 伺服器的主機URL。 |
| `attributes.username` | 驗證的選用使用者名稱。 |
| `type` | 要更新的資源類型。 對於此端點，值必須為`hosts`。 |

{style=&quot;table-layout:auto&quot;}

**回應**

成功的回應會傳回新建立之主機的詳細資訊。

```json
{
  "data": {
    "id": "HT69bfe634dead4a9a8c659f5d4d94cecd",
    "type": "hosts",
    "attributes": {
      "created_at": "2020-12-14T17:42:07.033Z",
      "server": "//example.com",
      "name": "Example SFTP Host",
      "path": "assets",
      "port": 22,
      "status": "pending",
      "type_of": "sftp",
      "updated_at": "2020-12-14T17:42:07.033Z",
      "username": "John Doe"
    },
    "relationships": {
      "property": {
        "links": {
          "related": "https://reactor.adobe.io/hosts/HT69bfe634dead4a9a8c659f5d4d94cecd/property"
        },
        "data": {
          "id": "PRb25a704c0b7c4562835ccdf96d3afd31",
          "type": "properties"
        }
      }
    },
    "links": {
      "property": "https://reactor.adobe.io/properties/PRb25a704c0b7c4562835ccdf96d3afd31",
      "self": "https://reactor.adobe.io/hosts/HT69bfe634dead4a9a8c659f5d4d94cecd"
    }
  }
}
```

## 更新主機 {#update}

>[!NOTE]
>
>只能更新SFTP主機。

您可以在PATCH請求的路徑中加入主機ID，以更新主機。

**API格式**

```http
PATCH /hosts/{HOST_ID}
```

| 參數 | 說明 |
| --- | --- |
| `HOST_ID` | 要更新的主機的`id`。 |

{style=&quot;table-layout:auto&quot;}

**要求**

下列請求會更新現有主機的`name`。

```shell
curl -X PATCH \
  https://reactor.adobe.io/hosts/HT5d90148e72224224aac9bc0b01498b84 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'Content-Type: application/json' \
  -d '{
        "data": {
          "attributes": {
            "name": "New host Name"
          },
          "id": "HT5d90148e72224224aac9bc0b01498b84",
          "type": "hosts"
        }
      }'
```

| 屬性 | 說明 |
| --- | --- |
| `attributes` | 一個對象，其屬性表示要為主機更新的屬性。 可針對主機更新下列屬性： <ul><li>`encrypted_private_key`</li><li>`name`</li><li>`path`</li><li>`port`</li><li>`server`</li><li>`type_of`</li><li>`username`</li></ul> |
| `id` | 要更新的主機的`id`。 這應符合要求路徑中提供的`{HOST_ID}`值。 |
| `type` | 要更新的資源類型。 對於此端點，值必須為`hosts`。 |

{style=&quot;table-layout:auto&quot;}

**回應**

成功的回應會傳回更新主機的詳細資訊。

```json
{
  "data": {
    "id": "HTb14e136a6fe147459b298a4645d2a6f5",
    "type": "hosts",
    "attributes": {
      "created_at": "2020-12-14T17:42:45.087Z",
      "server": null,
      "name": "My SFTP host",
      "path": null,
      "port": null,
      "status": "succeeded",
      "type_of": "sftp",
      "updated_at": "2020-12-14T17:42:45.696Z",
      "username": null
    },
    "relationships": {
      "property": {
        "links": {
          "related": "https://reactor.adobe.io/hosts/HTb14e136a6fe147459b298a4645d2a6f5/property"
        },
        "data": {
          "id": "PR8f240526f7b54a4dbd46965e79519fde",
          "type": "properties"
        }
      }
    },
    "links": {
      "property": "https://reactor.adobe.io/properties/PR8f240526f7b54a4dbd46965e79519fde",
      "self": "https://reactor.adobe.io/hosts/HTb14e136a6fe147459b298a4645d2a6f5"
    }
  }
}
```

## 刪除主機

您可以在DELETE請求的路徑中加入主機ID，以刪除該主機。

**API格式**

```http
DELETE /hosts/{HOST_ID}
```

| 參數 | 說明 |
| --- | --- |
| `HOST_ID` | 要刪除的主機的`id`。 |

{style=&quot;table-layout:auto&quot;}

**要求**

```shell
curl -X DELETE \
  https://reactor.adobe.io/hosts/HT5d90148e72224224aac9bc0b01498b84 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}'
```

**回應**

成功的回應會傳回HTTP狀態204（無內容），但沒有回應內文，指出主機已遭刪除。

## 為主機擷取相關資源 {#related}

下列呼叫示範如何擷取主機的相關資源。 當[查找主機](#lookup)時，這些關係將列在`relationships`屬性下。

有關Reactor API中關係的詳細資訊，請參閱[關係指南](../guides/relationships.md)。

### 查找主機的相關屬性 {#property}

您可以將`/property`附加至查詢請求的路徑，以尋找擁有主機的屬性。

**API格式**

```http
GET /hosts/{HOST_ID}/property
```

| 參數 | 說明 |
| --- | --- |
| `{HOST_ID}` | 您要查找其屬性的主機的`id`。 |

{style=&quot;table-layout:auto&quot;}

**要求**

```shell
curl -X GET \
  https://reactor.adobe.io/hosts/HT5d90148e72224224aac9bc0b01498b84/property \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**回應**

成功的回應會傳回指定主機屬性的詳細資訊。

```json
{
  "data": {
    "id": "PRbdfaffb7bf374b87be50e672f0cf9309",
    "type": "properties",
    "attributes": {
      "created_at": "2020-12-14T17:52:05.900Z",
      "enabled": true,
      "name": "Kessel Example Property",
      "updated_at": "2020-12-14T17:52:05.900Z",
      "platform": "web",
      "development": false,
      "token": "47d65c7c98db",
      "domains": [
        "example.com"
      ],
      "undefined_vars_return_empty": false,
      "rule_component_sequencing_enabled": false
    },
    "relationships": {
      "company": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PRbdfaffb7bf374b87be50e672f0cf9309/company"
        },
        "data": {
          "id": "CO2bf094214ffd4785bb4bcf88c952a7c1",
          "type": "companies"
        }
      },
      "callbacks": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PRbdfaffb7bf374b87be50e672f0cf9309/callbacks"
        }
      },
      "hosts": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PRbdfaffb7bf374b87be50e672f0cf9309/hosts"
        }
      },
      "environments": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PRbdfaffb7bf374b87be50e672f0cf9309/environments"
        }
      },
      "libraries": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PRbdfaffb7bf374b87be50e672f0cf9309/libraries"
        }
      },
      "data_elements": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PRbdfaffb7bf374b87be50e672f0cf9309/data_elements"
        }
      },
      "extensions": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PRbdfaffb7bf374b87be50e672f0cf9309/extensions"
        }
      },
      "rules": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PRbdfaffb7bf374b87be50e672f0cf9309/rules"
        }
      },
      "notes": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PRbdfaffb7bf374b87be50e672f0cf9309/notes"
        }
      }
    },
    "links": {
      "company": "https://reactor.adobe.io/companies/CO2bf094214ffd4785bb4bcf88c952a7c1",
      "data_elements": "https://reactor.adobe.io/properties/PRbdfaffb7bf374b87be50e672f0cf9309/data_elements",
      "environments": "https://reactor.adobe.io/properties/PRbdfaffb7bf374b87be50e672f0cf9309/environments",
      "extensions": "https://reactor.adobe.io/properties/PRbdfaffb7bf374b87be50e672f0cf9309/extensions",
      "rules": "https://reactor.adobe.io/properties/PRbdfaffb7bf374b87be50e672f0cf9309/rules",
      "self": "https://reactor.adobe.io/properties/PRbdfaffb7bf374b87be50e672f0cf9309"
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
