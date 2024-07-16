---
title: 附註端點
description: 瞭解如何在Reactor API中呼叫/notes端點。
exl-id: fa3bebc0-215e-4515-87b9-d195c9ab76c1
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '512'
ht-degree: 5%

---

# 附註端點

在Reactor API中，附註是可新增至特定資源的文字註釋。 附註基本上是對各自資源的評論。 附註的內容對資源行為沒有影響，可用於各種使用案例，包括：

* 提供背景資訊
* 作為待辦事項清單使用
* 傳遞資源使用建議
* 向其他團隊成員提供指示
* 記錄歷史內容

Reactor API中的`/notes`端點可讓您以程式設計方式管理這些備註。

附註可套用下列資源：

* [資料元素](./data-elements.md)
* [擴充功能](./extensions.md)
* [程式庫](./libraries.md)
* [屬性](./properties.md)
* [規則元件](./rule-components.md)
* [規則](./rules.md)
* [秘密](./secrets.md)

這六種型別統稱為「重要」資源。 刪除重要資源時，也會刪除其相關的附註。

>[!NOTE]
>
>對於可以有多個修訂版本的資源，必須在目前（標題）修訂版本上建立任何附註。 它們不能附加到其他修訂版本。
>
>不過，您仍可從修訂版本讀取附註。 在這種情況下，API只會傳回修訂版本建立前存在的附註。 它們會提供與剪下修訂版本時相同的註釋快照。 相反地，從目前（標題）修訂版本讀取註記會傳回其所有註記。

## 快速入門

此指南中使用的端點是[Reactor API](https://www.adobe.io/experience-platform-apis/references/reactor/)的一部分。 在繼續之前，請檢閱[快速入門手冊](../getting-started.md)，以取得有關如何向API驗證的重要資訊。

## 擷取附註清單 {#list}

您可以將`/notes`附加至相關資源的GET要求路徑，以擷取資源的附註清單。

**API格式**

```http
GET /{RESOURCE_TYPE}/{RESOURCE_ID}/notes
```

| 參數 | 說明 |
| --- | --- |
| `RESOURCE_TYPE` | 您要擷取備註的資源型別。 必須為下列其中一個值： <ul><li>`data_elements`</li><li>`extensions`</li><li>`libraries`</li><li>`properties`</li><li>`rule_components`</li><li>`rules`</li></ul> |
| `RESOURCE_ID` | 您要列出其筆記的特定資源的`id`。 |

{style="table-layout:auto"}

**要求**

下列請求列出附加至程式庫的附註。

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

成功的回應會傳回附加至指定資源的附註清單。

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

## 查詢附註 {#lookup}

您可以在GET請求的路徑中提供其ID來查詢附註。

**API格式**

```http
GET /notes/{NOTE_ID}
```

| 參數 | 說明 |
| --- | --- |
| `NOTE_ID` | 您要查閱之筆記的`id`。 |

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

成功的回應會傳回附註的詳細資料。

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
>建立新註記之前，請記住，註記不可編輯，刪除註記的唯一方法是刪除其對應的資源。

您可以將`/notes`附加至相關資源之POST要求的路徑，以建立新附註。

**API格式**

```http
POST /{RESOURCE_TYPE}/{RESOURCE_ID}/notes
```

| 參數 | 說明 |
| --- | --- |
| `RESOURCE_TYPE` | 您正在建立附註的資源型別。 必須為下列其中一個值： <ul><li>`data_elements`</li><li>`extensions`</li><li>`libraries`</li><li>`properties`</li><li>`rule_components`</li><li>`rules`</li></ul> |
| `RESOURCE_ID` | 您要為其建立附註的特定資源的`id`。 |

{style="table-layout:auto"}

**要求**

以下請求會為屬性建立新的附註。

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
| `type` | **（必要）**&#x200B;正在更新的資源型別。 此端點的值必須是`notes`。 |
| `attributes.text` | **（必要）**&#x200B;包含附註的文字。 每個附註限定為512個Unicode字元。 |

{style="table-layout:auto"}

**回應**

成功的回應會傳回新建立附註的詳細資訊。

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
