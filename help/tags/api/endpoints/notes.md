---
title: Notes終結點
description: 瞭解如何調用Repartor API中的/notes端點。
exl-id: fa3bebc0-215e-4515-87b9-d195c9ab76c1
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '515'
ht-degree: 5%

---

# Notes終結點

在Reactor API中，注釋是可添加到某些資源的文本注釋。 注釋實質上是對各自資源的評論。 注釋的內容對資源行為沒有影響，可用於包括以下內容在內的各種使用情形：

* 提供背景資訊
* 作為待辦事項清單
* 傳遞資源使用建議
* 向其他團隊成員提供說明
* 記錄歷史上下文

的 `/notes` Reactor API中的端點允許您以寫程式方式管理這些注釋。

注釋可應用於以下資源：

* [資料元素](./data-elements.md)
* [擴充功能](./extensions.md)
* [程式庫](./libraries.md)
* [屬性](./properties.md)
* [規則元件](./rule-components.md)
* [規則](./rules.md)
* [秘密](./secrets.md)

這六種資源統稱為&quot;顯著&quot;資源。 刪除顯著資源時，其關聯注釋也會被刪除。

>[!NOTE]
>
>對於可以具有多個修訂的資源，必須在當前（頭）修訂上建立任何注釋。 它們可能不附於其他修訂。
>
>但是，注釋仍可從修訂中閱讀。 在這種情況下， API只返回在建立修訂之前存在的注釋。 它們提供了注釋的快照，與剪切修訂時的快照一樣。 相反，從當前(head)修訂中讀取注釋將返回其所有注釋。

## 快速入門

本指南中使用的端點是 [反應堆API](https://www.adobe.io/experience-platform-apis/references/reactor/)。 在繼續之前，請查看 [入門指南](../getting-started.md) 有關如何驗證到API的重要資訊。

## 檢索注釋清單 {#list}

可通過附加來檢索資源的注釋清單 `/notes` 到有關資源的GET請求的路徑。

**API格式**

```http
GET /{RESOURCE_TYPE}/{RESOURCE_ID}/notes
```

| 參數 | 說明 |
| --- | --- |
| `RESOURCE_TYPE` | 您為其提取注釋的資源類型。 必須是以下值之一： <ul><li>`data_elements`</li><li>`extensions`</li><li>`libraries`</li><li>`properties`</li><li>`rule_components`</li><li>`rules`</li></ul> |
| `RESOURCE_ID` | 的 `id` 要列出其注釋的特定資源。 |

{style="table-layout:auto"}

**要求**

以下請求列出了附加到庫的注釋。

```shell
curl -X GET \
  https://reactor.adobe.io/libraries/LBcffea1a38c52408cae2398868625a12d/notes \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**回應**

成功的響應返回附加到指定資源的注釋清單。

```json
{
  "data": [
    {
      "id": "NTa40de8d76bfd4e40835830900ce83b7b",
      "type": "notes",
      "attributes": {
        "author_display_name": "John Smith",
        "author_email": "jsmith@example.com",
        "created_at": "2020-12-14T17:51:00.411Z",
        "text": "this is a note on a library"
      },
      "relationships": {
        "resource": {
          "links": {
            "related": "https://reactor.adobe.io/libraries/LBcffea1a38c52408cae2398868625a12d"
          },
          "data": {
            "id": "LBcffea1a38c52408cae2398868625a12d",
            "type": "libraries"
          }
        }
      },
      "links": {
        "resource": "https://reactor.adobe.io/libraries/LBcffea1a38c52408cae2398868625a12d",
        "self": "https://reactor.adobe.io/notes/NTa40de8d76bfd4e40835830900ce83b7b"
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

## 查找便箋 {#lookup}

可以通過在GET請求的路徑中提供注釋ID來查找注釋。

**API格式**

```http
GET /notes/{NOTE_ID}
```

| 參數 | 說明 |
| --- | --- |
| `NOTE_ID` | 的 `id` 你想查的便條。 |

{style="table-layout:auto"}

**要求**

```shell
curl -X GET \
  https://reactor.adobe.io/notes/NT550b7a17ab304d49ba289a2978d673e5 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**回應**

成功的響應將返回注釋的詳細資訊。

```json
{
  "data": {
    "id": "NT550b7a17ab304d49ba289a2978d673e5",
    "type": "notes",
    "attributes": {
      "author_display_name": "John Smith",
      "author_email": "jsmith@example.com",
      "created_at": "2020-12-14T17:51:10.316Z",
      "text": "this is a note on a property"
    },
    "relationships": {
      "resource": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR4537ac6f1f204ffd864ec47c4b27c2e8"
        },
        "data": {
          "id": "PR4537ac6f1f204ffd864ec47c4b27c2e8",
          "type": "properties"
        }
      }
    },
    "links": {
      "resource": "https://reactor.adobe.io/properties/PR4537ac6f1f204ffd864ec47c4b27c2e8",
      "self": "https://reactor.adobe.io/notes/NT550b7a17ab304d49ba289a2978d673e5"
    }
  }
}
```

## 建立附註 {#create}

>[!WARNING]
>
>在建立新注釋之前，請記住注釋不可編輯，刪除它們的唯一方法是刪除它們的相應資源。

可通過附加建立新注釋 `/notes` 到有關資源的POST請求的路徑。

**API格式**

```http
POST /{RESOURCE_TYPE}/{RESOURCE_ID}/notes
```

| 參數 | 說明 |
| --- | --- |
| `RESOURCE_TYPE` | 要為其建立注釋的資源類型。 必須是以下值之一： <ul><li>`data_elements`</li><li>`extensions`</li><li>`libraries`</li><li>`properties`</li><li>`rule_components`</li><li>`rules`</li></ul> |
| `RESOURCE_ID` | 的 `id` 要為其建立注釋的特定資源。 |

{style="table-layout:auto"}

**要求**

以下請求將為屬性建立新附註。

```shell
curl -X POST \
  https://reactor.adobe.io/properties/PRb25a704c0b7c4562835ccdf96d3afd31/notes \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Content-Type: application/json' \
  -d '{
        "data": {
          "type": "notes",
          "attributes": {
            "text": "this is a note on a property"
          }
        }
      }'
```

| 屬性 | 說明 |
| --- | --- |
| `type` | **（必需）** 要更新的資源類型。 對於此終結點，值必須為 `notes`。 |
| `attributes.text` | **（必需）** 包含注釋的文本。 每個注釋限制為512個Unicode字元。 |

{style="table-layout:auto"}

**回應**

成功的響應將返回新建立的注釋的詳細資訊。

```json
{
  "data": {
    "id": "NT550b7a17ab304d49ba289a2978d673e5",
    "type": "notes",
    "attributes": {
      "author_display_name": "John Smith",
      "author_email": "jsmith@example.com",
      "created_at": "2020-12-14T17:51:10.316Z",
      "text": "This is a note on a property"
    },
    "relationships": {
      "resource": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR4537ac6f1f204ffd864ec47c4b27c2e8"
        },
        "data": {
          "id": "PR4537ac6f1f204ffd864ec47c4b27c2e8",
          "type": "properties"
        }
      }
    },
    "links": {
      "resource": "https://reactor.adobe.io/properties/PR4537ac6f1f204ffd864ec47c4b27c2e8",
      "self": "https://reactor.adobe.io/notes/NT550b7a17ab304d49ba289a2978d673e5"
    }
  }
}
```
