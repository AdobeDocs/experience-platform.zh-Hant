---
title: 搜尋端點
description: 了解如何在Reactor API中呼叫/search端點。
source-git-commit: 53612919dc040a8a3ad35a3c5c0991554ffbea7c
workflow-type: tm+mt
source-wordcount: '662'
ht-degree: 1%

---

# 搜尋端點

Reactor API中的`/search`端點提供尋找符合所需條件的資源的方式，以查詢的形式表示。

下列API資源類型可供搜尋，其資料結構與API中傳回的資源型檔案相同：

* `audit_events`
* `builds`
* `callbacks`
* `data_elements`
* `environments`
* `extension_packages`
* `extensions`
* `hosts`
* `libraries`
* `properties`
* `rule_components`
* `rules`

所有查詢都限定在您目前公司的範圍和可存取的屬性。

>[!IMPORTANT]
>
>搜尋功能有下列警告和例外：
>* meta不可搜尋，也不會在搜尋結果中傳回。
>* 擴充功能套件委派的結構欄位（動作、條件等） 可搜尋為文字，而非巢狀資料結構。
>* 範圍查詢目前僅支援整數。


有關如何使用此功能的更深入資訊，請參閱[搜索指南](../guides/search.md)。

## 快速入門

本指南中使用的端點是[Reactor API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/reactor.yaml)的一部分。 繼續操作之前，請參閱[快速入門手冊](../getting-started.md)，了解如何驗證API的重要資訊。

## 執行搜尋 {#perform}

您可以提出POST請求來執行搜尋。

**API格式**

```http
POST /search
```

**要求**

```shell
curl -X POST \
  https://reactor.adobe.io/search \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1' \
  -d '{
        "data" : {
          "from": 0,
          "size": 25,
          "query": {
            "attributes.name": {
              "value": "Performance"
            },
            "attributes.revision_number": {
              "range": {
                "lte": "2",
                "gt": "0"
              }
            }
          },
          "sort": [
            {
              "attributes.revision_number": "desc"
            }
          ],
          "resource_types": [
            "data_elements",
            "rule_components"
          ]
        }
      }'
```

| 屬性 | 說明 |
| --- | --- |
| `from` | 要偏移響應的結果數。 |
| `size` | 要返回的最大結果量。 結果不能超過100個項目。 |
| `query` | 表示搜索查詢的對象。 對於此對象中的每個屬性，鍵必須表示要查詢的欄位路徑，且值必須是一個子屬性決定要查詢的對象。<br><br>對於每個欄位路徑，您可以使用下列子屬性：<ul><li>`exists`:如果資源中存在欄位，則傳回true。</li><li>`value`:如果欄位的值符合此屬性的值，則傳回true。</li><li>`value_operator`:用來判斷查詢應如何處理 `value` 的布林邏輯。允許的值為`AND`和`OR`。 排除時，會假設`AND`邏輯。 如需詳細資訊，請參閱[value運算子邏輯](#value-operator)上的區段。</li><li>`range` 如果欄位值落在特定數值範圍內，則傳回true。範圍本身由下列子屬性決定：<ul><li>`gt`:大於提供的值，不包含。</li><li>`gte`:大於或等於提供的值。</li><li>`lt`:小於提供的值，不包含。</li><li>`lte`:小於或等於提供的值。</li></ul></li></ul> |
| `sort` | 對象的陣列，指示對結果進行排序的順序。 每個物件都必須包含單一屬性：索引鍵代表要排序的欄位路徑，值代表排序順序（升序為`asc`，降序為`desc`）。 |
| `resource_types` | 字串的陣列，用於指示要搜索的特定資源類型。 |

{style=&quot;table-layout:auto&quot;}

**回應**

成功的回應會傳回查詢的相符資源清單。 如需API如何為特定值判斷相符項目的詳細資訊，請參閱[符合慣例](#conventions)的附錄一節。

```json
{
  "data": [
    {
      "id": "DE5d11b3ed301d4ce99b530a5121e392b2",
      "type": "data_elements",
      "attributes": {
        "created_at": "2020-12-14T17:36:09.045Z",
        "deleted_at": null,
        "dirty": true,
        "enabled": true,
        "name": "Performance Indicator",
        "published": false,
        "published_at": null,
        "revision_number": 1,
        "updated_at": "2020-12-14T17:36:09.045Z",
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
            "related": "https://reactor.adobe.io/data_elements/DE5d11b3ed301d4ce99b530a5121e392b2/libraries"
          }
        },
        "revisions": {
          "links": {
            "related": "https://reactor.adobe.io/data_elements/DE5d11b3ed301d4ce99b530a5121e392b2/revisions"
          }
        },
        "notes": {
          "links": {
            "related": "https://reactor.adobe.io/data_elements/DE5d11b3ed301d4ce99b530a5121e392b2/notes"
          }
        },
        "property": {
          "links": {
            "related": "https://reactor.adobe.io/data_elements/DE5d11b3ed301d4ce99b530a5121e392b2/property"
          },
          "data": {
            "id": "PR97d92a379a5f48758947cdf44f607a0d",
            "type": "properties"
          }
        },
        "origin": {
          "links": {
            "related": "https://reactor.adobe.io/data_elements/DE5d11b3ed301d4ce99b530a5121e392b2/origin"
          },
          "data": {
            "id": "DE5d11b3ed301d4ce99b530a5121e392b2",
            "type": "data_elements"
          }
        },
        "extension": {
          "links": {
            "related": "https://reactor.adobe.io/data_elements/DE5d11b3ed301d4ce99b530a5121e392b2/extension"
          },
          "data": {
            "id": "EX0348d463358c4c89afe726245576f112",
            "type": "extensions"
          }
        },
        "updated_with_extension_package": {
          "links": {
            "related": "https://reactor.adobe.io/data_elements/DE5d11b3ed301d4ce99b530a5121e392b2/updated_with_extension_package"
          },
          "data": {
            "id": "EP75db2452065b44e2b8a38ca883ce369a",
            "type": "extension_packages"
          }
        },
        "updated_with_extension": {
          "links": {
            "related": "https://reactor.adobe.io/data_elements/DE5d11b3ed301d4ce99b530a5121e392b2/updated_with_extension"
          },
          "data": {
            "id": "EX1cc78b39339242da82a0e0752fa53375",
            "type": "extensions"
          }
        }
      },
      "links": {
        "property": "https://reactor.adobe.io/properties/PR97d92a379a5f48758947cdf44f607a0d",
        "origin": "https://reactor.adobe.io/data_elements/DE5d11b3ed301d4ce99b530a5121e392b2",
        "self": "https://reactor.adobe.io/data_elements/DE5d11b3ed301d4ce99b530a5121e392b2",
        "extension": "https://reactor.adobe.io/extensions/EX0348d463358c4c89afe726245576f112"
      },
      "meta": {
        "latest_revision_number": 1
      }
    }
  ],
  "meta": {
    "total_hits": 1
  }
}
```

## 附錄

下節包含有關使用`/search`端點的其他資訊。

### 值運算子邏輯 {#value-operator}

搜索查詢值被拆分為詞語，以與索引文檔匹配。 在每個詞語之間，假設`AND`關係。

使用`AND`作為`value_operator`時，將`My Rule Holiday Sale`的查詢值解釋為帶有`My AND Rule AND Holiday AND Sale`欄位的文檔。

使用`OR`作為`value_operator`時，將`My Rule Holiday Sale`的查詢值解釋為帶有`My OR Rule OR Holiday OR Sale`欄位的文檔。 符合的詞語越多，`match_score`就越高。 由於部分詞語匹配的性質，當沒有任何內容與所需值緊密匹配時，您可以獲得一個結果集，其中值僅在非常基本的級別上匹配，例如文本的幾個字元。

### 相符的慣例 {#conventions}

搜索與回答文檔與提供的查詢的相關性有關。 分析和索引文檔資料的方式直接影響到這一點。

下表劃分了常見欄位類型的匹配慣例：

| 欄位類型 | 匹配約定 |
| --- | --- |
| 字串 | 具有部分術語分析的文本，不區分大小寫 |
| 列舉值 | 完全匹配，區分大小寫 |
| 整數 | 完全匹配 |
| 浮動 | 完全匹配 |
| 時間戳記 | 完全相符（DateTime格式） |
| 顯示名稱 | 具有部分術語分析的文本，不區分大小寫 |

API中會顯示特定欄位的其他慣例：

| 欄位 | 匹配約定 |
| --- | --- |
| `id` | 完全匹配，區分大小寫 |
| `delegate_descriptor_id` | 完全相符，區分大小寫，詞語在`::`上分割 |
| `name` | 完全匹配，區分大小寫 |
| `settings` | 具有部分術語分析的文本，不區分大小寫 |
| `type` | 完全匹配，區分大小寫 |