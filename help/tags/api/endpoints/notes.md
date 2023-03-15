---
title: Notes端點
description: 了解如何在Reactor API中呼叫/notes端點。
exl-id: fa3bebc0-215e-4515-87b9-d195c9ab76c1
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '515'
ht-degree: 5%

---

# Notes端點

在Reactor API中，附註是可新增至特定資源的文字註解。 附註主要是對各自資源的評論。 附註的內容對資源行為沒有影響，可用於多種使用案例，包括：

* 提供背景資訊
* 運作方式清單
* 傳遞資源使用建議
* 向其他團隊成員提供指示
* 記錄歷史內容

此 `/notes` reactor API中的端點可讓您以程式設計方式管理這些附註。

附註可套用至下列資源：

* [資料元素](./data-elements.md)
* [擴充功能](./extensions.md)
* [程式庫](./libraries.md)
* [屬性](./properties.md)
* [規則元件](./rule-components.md)
* [規則](./rules.md)
* [秘密](./secrets.md)

這六種類型統稱為「顯著」資源。 刪除顯著資源時，也會刪除其相關附註。

>[!NOTE]
>
>對於可以有多個修訂的資源，必須在當前（標題）修訂上建立任何注釋。 它們不得附於其他修訂版本。
>
>不過，修訂版仍可閱讀附註。 在這種情況下，API只會傳回建立修訂版本之前存在的附註。 它們提供注釋的快照，與剪切修訂時的快照一樣。 相反地，從當前(head)修訂中讀取注釋將返回其所有注釋。

## 快速入門

本指南中使用的端點屬於 [Reactor API](https://www.adobe.io/experience-platform-apis/references/reactor/). 繼續之前，請檢閱 [快速入門手冊](../getting-started.md) 以取得如何驗證API的重要資訊。

## 擷取附註清單 {#list}

您可以借由附加 `/notes` 至相關資源的GET請求的路徑。

**API格式**

```http
GET /{RESOURCE_TYPE}/{RESOURCE_ID}/notes
```

| 參數 | 說明 |
| --- | --- |
| `RESOURCE_TYPE` | 您為擷取附註的資源類型。 必須是下列其中一個值： <ul><li>`data_elements`</li><li>`extensions`</li><li>`libraries`</li><li>`properties`</li><li>`rule_components`</li><li>`rules`</li></ul> |
| `RESOURCE_ID` | 此 `id` 要列出其附註的特定資源。 |

{style="table-layout:auto"}

**要求**

下列請求會列出附加至程式庫的附註。

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

## 查找注釋 {#lookup}

您可以在請求的路徑中提供附註ID，以查找附註。

**API格式**

```http
GET /notes/{NOTE_ID}
```

| 參數 | 說明 |
| --- | --- |
| `NOTE_ID` | 此 `id` 你想查的那張紙條。 |

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

成功的回應會傳回附註的詳細資訊。

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
>建立新附註之前，請記住附註不可編輯，刪除附註的唯一方式是刪除其對應的資源。

可通過附加 `/notes` 至相關資源的POST請求的路徑。

**API格式**

```http
POST /{RESOURCE_TYPE}/{RESOURCE_ID}/notes
```

| 參數 | 說明 |
| --- | --- |
| `RESOURCE_TYPE` | 要為建立備注的資源類型。 必須是下列其中一個值： <ul><li>`data_elements`</li><li>`extensions`</li><li>`libraries`</li><li>`properties`</li><li>`rule_components`</li><li>`rules`</li></ul> |
| `RESOURCE_ID` | 此 `id` 要為其建立備注的特定資源。 |

{style="table-layout:auto"}

**要求**

以下請求會為屬性建立新附註。

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
| `type` | **（必要）** 要更新的資源類型。 對於此端點，值必須是 `notes`. |
| `attributes.text` | **（必要）** 包含注釋的文本。 每個注釋最多只能有512個Unicode字元。 |

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
