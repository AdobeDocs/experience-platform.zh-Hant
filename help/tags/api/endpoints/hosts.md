---
title: 主機端點
description: 瞭解如何在Reactor API中呼叫/hosts端點。
exl-id: 9d0d2a65-49e9-429c-a665-754b59a11cf1
source-git-commit: b66a50e40aaac8df312a2c9a977fb8d4f1fb0c80
workflow-type: tm+mt
source-wordcount: '793'
ht-degree: 3%

---

# 主機端點

>[!NOTE]
>
>本文介紹如何在Reactor API中管理主機。 如需標籤主機的一般詳細資訊，請參閱發佈檔案中有關[主機概觀](../../ui/publishing/hosts/hosts-overview.md)的指南。

在Reactor API中，主機會定義可傳送[組建](./builds.md)的目的地。

當Adobe Experience Platform中的標籤使用者要求組建時，系統會檢查程式庫以決定程式庫應建置到的[環境](./environments.md)。 每個環境都與主機有關聯，以指示傳遞組建的位置。

主機只屬於一個[屬性](./properties.md)，而屬性可以有許多主機。 屬性必須至少有一個主機，您才能發佈。

一個主機可由一個屬性中的多個環境使用。 通常屬性上會有一個主機，且該屬性上的所有環境都會使用相同的主機。

## 快速入門

此指南中使用的端點是[Reactor API](https://www.adobe.io/experience-platform-apis/references/reactor/)的一部分。 在繼續之前，請檢閱[快速入門手冊](../getting-started.md)，以取得有關如何向API驗證的重要資訊。

## 擷取主機清單 {#list}

您可以在GET要求的路徑中包含屬性的ID，以擷取屬性的主機清單。

**API格式**

```http
GET /properties/{PROPERTY_ID}/hosts
```

| 參數 | 說明 |
| --- | --- |
| `PROPERTY_ID` | 擁有主機的屬性之`id`。 |

{style="table-layout:auto"}

>[!NOTE]
>
>您可以使用查詢引數，根據下列屬性篩選列出的主機：<ul><li>`created_at`</li><li>`name`</li><li>`type_of`</li><li>`updated_at`</li></ul>如需詳細資訊，請參閱[篩選回應](../guides/filtering.md)的指南。

**要求**

```shell
curl -X GET \
  https://reactor.adobe.io/properties/PRd428c2a25caa4b32af61495f5809b737/hosts \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**回應**

成功的回應會傳回指定屬性的主機清單。

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

## 查詢主機 {#lookup}

您可以在GET請求的路徑中提供主機ID以查詢主機。

**API格式**

```http
GET /hosts/{HOST_ID}
```

| 參數 | 說明 |
| --- | --- |
| `HOST_ID` | 您要查閱之主機的`id`。 |

{style="table-layout:auto"}

**要求**

```shell
curl -X GET \
  https://reactor.adobe.io/hosts/HT5d90148e72224224aac9bc0b01498b84 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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

您可以發出POST要求來建立新主機。

**API格式**

```http
POST /properties/{PROPERTY_ID}/hosts
```

| 參數 | 說明 |
| --- | --- |
| `PROPERTY_ID` | 您正在定義主機的[屬性](./properties.md)的`id`。 |

{style="table-layout:auto"}

**要求**

下列要求會為指定的屬性建立新的主機。 呼叫也會透過`relationships`屬性將主機與現有的分機建立關聯。 如需詳細資訊，請參閱[關係](../guides/relationships.md)的指南。

```shell
curl -X POST \
  https://reactor.adobe.io/properties/PRb25a704c0b7c4562835ccdf96d3afd31/hosts \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Content-Type: application/json' \
  -d '{
        "data": {
          "attributes": {
            "name": "Example SFTP Host",
            "type_of": "sftp",
            "username": "John Doe",
            "encrypted_private_key": "{PRIVATE_KEY}",
            "server": "https://example.com",
            "skip_symlinks": true,
            "path": "assets",
            "port": 22
          },
          "type": "hosts"
        }
      }'
```

| 屬性 | 說明 |
| --- | --- |
| `attributes.name` | **（必要）**&#x200B;人類看得懂的主機名稱。 |
| `attributes.type_of` | **（必要）**&#x200B;主機的型別。 可以是下列兩個選項之一： <ul><li>[Adobe管理主機](../../ui/publishing/hosts/managed-by-adobe-host.md)的`akamai`</li><li>[SFTP主機](../../ui/publishing/hosts/sftp-host.md)的`sftp`</li></ul> |
| `attributes.encrypted_private_key` | 用於主機驗證的選用私密金鑰。 |
| `attributes.path` | 要附加至`server` URL的路徑。 |
| `attributes.port` | 整數，表示要使用的特定伺服器連線埠。 |
| `attributes.server` | 伺服器的主機URL。 |
| `attributes.skip_symlinks`<br><br> （僅適用於SFTP主機） | 依預設，所有SFTP主機都使用符號連結(symlink)來參照儲存至伺服器的程式庫組建。 不過，並非所有伺服器都支援使用symlink。 當包含此屬性且設為`true`時，主機會使用復製作業來直接更新組建資產，而不使用符號連結。 |
| `attributes.username` | 用於驗證的選用使用者名稱。 |
| `type` | 正在更新的資源型別。 此端點的值必須是`hosts`。 |

{style="table-layout:auto"}

**回應**

成功的回應會傳回新建立主機的詳細資訊。

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
      "skip_symlinks": true,
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

您可以在PATCH請求的路徑中包含主機ID來更新主機。

**API格式**

```http
PATCH /hosts/{HOST_ID}
```

| 參數 | 說明 |
| --- | --- |
| `HOST_ID` | 您要更新的主機之`id`。 |

{style="table-layout:auto"}

**要求**

下列要求會更新現有主機的`name`。

```shell
curl -X PATCH \
  https://reactor.adobe.io/hosts/HT5d90148e72224224aac9bc0b01498b84 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `attributes` | 物件，其屬性代表主機要更新的屬性。 可以為主機更新下列屬性： <ul><li>`encrypted_private_key`</li><li>`name`</li><li>`path`</li><li>`port`</li><li>`server`</li><li>`type_of`</li><li>`username`</li></ul> |
| `id` | 您要更新的主機`id`。 這應該符合請求路徑中提供的`{HOST_ID}`值。 |
| `type` | 正在更新的資源型別。 此端點的值必須是`hosts`。 |

{style="table-layout:auto"}

**回應**

成功的回應會傳回已更新主機的詳細資訊。

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
      "skip_symlinks": true,
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

您可以在DELETE請求的路徑中包含主機ID以刪除主機。

**API格式**

```http
DELETE /hosts/{HOST_ID}
```

| 參數 | 說明 |
| --- | --- |
| `HOST_ID` | 您要刪除之主機的`id`。 |

{style="table-layout:auto"}

**要求**

```shell
curl -X DELETE \
  https://reactor.adobe.io/hosts/HT5d90148e72224224aac9bc0b01498b84 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}'
```

**回應**

成功的回應會傳回HTTP狀態204 （無內容），但沒有回應內文，這表示主機已被刪除。

## 擷取主機的相關資源 {#related}

下列呼叫示範如何擷取主機的相關資源。 當[查詢主機](#lookup)時，這些關係會列在`relationships`屬性下。

請參閱[關係指南](../guides/relationships.md)，以取得有關Reactor API中關係的詳細資訊。

### 查詢主機的相關屬性 {#property}

您可以將`/property`附加至查閱要求的路徑，以查閱擁有主機的屬性。

**API格式**

```http
GET /hosts/{HOST_ID}/property
```

| 參數 | 說明 |
| --- | --- |
| `{HOST_ID}` | 您要查詢其屬性的主機之`id`。 |

{style="table-layout:auto"}

**要求**

```shell
curl -X GET \
  https://reactor.adobe.io/hosts/HT5d90148e72224224aac9bc0b01498b84/property \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**回應**

成功的回應會傳回指定之主機屬性的詳細資訊。

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
