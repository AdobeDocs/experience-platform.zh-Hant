---
title: 主機終結點
description: 瞭解如何調用Repartor API中的/hosts端點。
exl-id: 9d0d2a65-49e9-429c-a665-754b59a11cf1
source-git-commit: 905384b3190cd55e7caa9c4560d6b2774280eee7
workflow-type: tm+mt
source-wordcount: '821'
ht-degree: 6%

---

# 主機終結點

>[!NOTE]
>
>本文檔介紹如何管理Reactor API中的主機。 有關標籤的主機的更多一般資訊，請參見上的指南 [主機概述](../../ui/publishing/hosts/hosts-overview.md) 的下界。

在Reactor API中，主機定義目標 [構建](./builds.md) 可以交付。

當Adobe Experience Platform的標籤用戶請求生成時，系統會檢查庫以確定 [環境](./environments.md) 圖書館應該建成。 每個環境都與主機有關係，指明在何處交付生成。

主機恰好屬於 [屬性](./properties.md)，而屬性可以具有多個主機。 在可以發佈之前，屬性必須至少有一個主機。

一個屬性中的多個環境可以使用主機。 在屬性上有單個主機，並且該屬性上的所有環境都使用同一台主機是常見的。

## 快速入門

本指南中使用的端點是 [反應堆API](https://www.adobe.io/experience-platform-apis/references/reactor/)。 在繼續之前，請查看 [入門指南](../getting-started.md) 有關如何驗證到API的重要資訊。

## 檢索主機清單 {#list}

通過將屬性的ID包含在GET請求的路徑中，可以檢索屬性的主機清單。

**API格式**

```http
GET /properties/{PROPERTY_ID}/hosts
```

| 參數 | 說明 |
| --- | --- |
| `PROPERTY_ID` | 的 `id` 擁有主機的財產。 |

{style=&quot;table-layout:auto&quot;}

>[!NOTE]
>
>使用查詢參數，可以根據以下屬性篩選列出的主機：<ul><li>`created_at`</li><li>`name`</li><li>`type_of`</li><li>`updated_at`</li></ul>請參閱上的指南 [過濾響應](../guides/filtering.md) 的子菜單。

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

成功的響應將返回指定屬性的主機清單。

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

通過在GET請求的路徑中提供主機ID，可以查找主機。

**API格式**

```http
GET /hosts/{HOST_ID}
```

| 參數 | 說明 |
| --- | --- |
| `HOST_ID` | 的 `id` 你想查的主人。 |

{style=&quot;table-layout:auto&quot;&quot;

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

成功的響應將返回主機的詳細資訊。

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

通過發出POST請求，可以建立新主機。

**API格式**

```http
POST /properties/{PROPERTY_ID}/hosts
```

| 參數 | 說明 |
| --- | --- |
| `PROPERTY_ID` | 的 `id` 的 [屬性](./properties.md) 定義主機。 |

{style=&quot;table-layout:auto&quot;&quot;

**要求**

以下請求為指定的屬性建立新主機。 該呼叫還將主機與通過 `relationships` 屬性。 請參閱上的指南 [關係](../guides/relationships.md) 的子菜單。

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
| `attributes.name` | **（必需）** 主機的可讀名稱。 |
| `attributes.type_of` | **（必需）** 主機類型。 可以是兩種選項之一： <ul><li>`akamai` 為 [Adobe管理的主機](../../ui/publishing/hosts/managed-by-adobe-host.md)</li><li>`sftp` 為 [SFTP主機](../../ui/publishing/hosts/sftp-host.md)</li></ul> |
| `attributes.encrypted_private_key` | 用於主機身份驗證的可選私鑰。 |
| `attributes.path` | 附加到的路徑 `server` URL。 |
| `attributes.port` | 一個整數，指示要使用的特定伺服器埠。 |
| `attributes.server` | 伺服器的主機URL。 |
| `attributes.skip_symlinks`<br><br>（僅適用於SFTP主機） | 預設情況下，所有SFTP主機都使用符號連結（符號連結）來引用保存到伺服器的庫生成。 但是，並非所有伺服器都支援使用符號連結。 當包含此屬性並設定為 `true`，主機使用複製操作直接更新生成資產，而不是使用symlinks。 |
| `attributes.username` | 驗證的可選用戶名。 |
| `type` | 要更新的資源類型。 對於此終結點，值必須為 `hosts`。 |

{style=&quot;table-layout:auto&quot;&quot;

**回應**

成功的響應將返回新建立的主機的詳細資訊。

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

您可以通過將主機ID包含在PATCH請求的路徑中來更新主機。

**API格式**

```http
PATCH /hosts/{HOST_ID}
```

| 參數 | 說明 |
| --- | --- |
| `HOST_ID` | 的 `id` 要更新的主機。 |

{style=&quot;table-layout:auto&quot;&quot;

**要求**

以下請求更新 `name` 的下界。

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
| `attributes` | 其屬性表示要為主機更新的屬性的對象。 可以為主機更新以下屬性： <ul><li>`encrypted_private_key`</li><li>`name`</li><li>`path`</li><li>`port`</li><li>`server`</li><li>`type_of`</li><li>`username`</li></ul> |
| `id` | 的 `id` 要更新的主機。 這應與 `{HOST_ID}` 請求路徑中提供的值。 |
| `type` | 要更新的資源類型。 對於此終結點，值必須為 `hosts`。 |

{style=&quot;table-layout:auto&quot;&quot;

**回應**

成功的響應將返回更新主機的詳細資訊。

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

通過將主機ID包含在DELETE請求的路徑中，可以刪除該主機。

**API格式**

```http
DELETE /hosts/{HOST_ID}
```

| 參數 | 說明 |
| --- | --- |
| `HOST_ID` | 的 `id` 刪除的主機。 |

{style=&quot;table-layout:auto&quot;&quot;

**要求**

```shell
curl -X DELETE \
  https://reactor.adobe.io/hosts/HT5d90148e72224224aac9bc0b01498b84 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}'
```

**回應**

成功的響應返回HTTP狀態204（無內容），沒有響應正文，表示主機已被刪除。

## 檢索主機的相關資源 {#related}

以下調用演示如何檢索主機的相關資源。 當 [查找主機](#lookup)，這些關係列在 `relationships` 屬性。

查看 [關係指南](../guides/relationships.md) 的子菜單。

### 查找主機的相關屬性 {#property}

可以通過附加 `/property` 查找請求的路徑。

**API格式**

```http
GET /hosts/{HOST_ID}/property
```

| 參數 | 說明 |
| --- | --- |
| `{HOST_ID}` | 的 `id` 要查找其財產的主人。 |

{style=&quot;table-layout:auto&quot;&quot;

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

成功的響應將返回指定主機屬性的詳細資訊。

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
