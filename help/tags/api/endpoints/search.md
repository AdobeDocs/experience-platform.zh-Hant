---
title: 搜索終結點
description: 瞭解如何調用Repartor API中的/search端點。
exl-id: 14eb8d8a-3b42-42f3-be87-f39e16d616f4
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '655'
ht-degree: 1%

---

# 搜索終結點

的 `/search` Reactor API中的端點提供了一種查找符合所需條件的資源的方法，以查詢形式表示。

以下API資源類型是可搜索的，使用與跨API返回的基於資源的文檔相同的資料結構：

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

所有查詢的範圍都限於當前公司和可訪問屬性。

>[!IMPORTANT]
>
>搜索功能具有以下警告和例外：
>* meta不可搜索，在搜索結果中不返回。
>* 擴展包委派的架構欄位（操作、條件等） 可搜索為文本，而不是嵌套的資料結構。
>* 範圍查詢當前僅支援整數。


有關如何使用此功能的更深入資訊，請參閱 [搜索指南](../guides/search.md)。

## 快速入門

本指南中使用的端點是 [反應堆API](https://www.adobe.io/experience-platform-apis/references/reactor/)。 在繼續之前，請查看 [入門指南](../getting-started.md) 有關如何驗證到API的重要資訊。

## 執行搜索 {#perform}

您可以通過發出POST請求來執行搜索。

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1' \
  -d '{
        "data": {
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
| `from` | 要將響應偏移的結果數。 |
| `size` | 要返回的最大結果量。 結果不能超過100項。 |
| `query` | 表示搜索查詢的對象。 對於此對象中的每個屬性，鍵必須表示要查詢的欄位路徑，並且值必須是其子屬性決定查詢內容的對象。<br><br>對於每個欄位路徑，可以使用以下子屬性：<ul><li>`exists`:如果資源中存在該欄位，則返回true。</li><li>`value`:如果欄位的值與此屬性的值匹配，則返回true。</li><li>`value_operator`:用於確定 `value` 應處理查詢。 允許的值為 `AND` 和 `OR`。 排除後， `AND` 假定邏輯。 請參閱 [值運算子邏輯](#value-operator) 的子菜單。</li><li>`range` 如果欄位的值在特定數值範圍內，則返回true。 範圍本身由以下子屬性確定：<ul><li>`gt`:大於提供的值，不包括。</li><li>`gte`:大於或等於提供的值。</li><li>`lt`:小於提供的值，不包括。</li><li>`lte`:小於或等於提供的值。</li></ul></li></ul> |
| `sort` | 對象陣列，指示對結果排序的順序。 每個對象必須包含一個屬性：鍵表示要排序依據的欄位路徑，值表示排序順序(`asc` 升序， `desc` )。 |
| `resource_types` | 字串陣列，指示要搜索的特定資源類型。 |

{style="table-layout:auto"}

**回應**

成功的響應返回查詢的匹配資源清單。 有關API如何確定特定值的匹配項的詳細資訊，請參閱附錄部分。 [匹配約定](#conventions)。

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

以下部分包含有關使用 `/search` 端點。

### 值運算子邏輯 {#value-operator}

將搜索查詢值拆分為與索引文檔相匹配的術語。 在每個術語之間， `AND` 假定關係。

使用時 `AND` 的 `value_operator`，查詢值 `My Rule Holiday Sale` 被解釋為包含 `My AND Rule AND Holiday AND Sale`。

使用時 `OR` 的 `value_operator`，查詢值 `My Rule Holiday Sale` 被解釋為包含 `My OR Rule OR Holiday OR Sale`。 匹配項越多，匹配項越高 `match_score`。 由於部分項匹配的性質，當沒有與所需值緊密匹配的項時，您可以獲得一個結果集，其中該值僅在非常基本的級別上匹配，如文本的幾個字元。

### 匹配約定 {#conventions}

搜索涉及回答文檔與提供的查詢的相關性。 文檔資料的分析和索引方式直接影響著這一點。

下表分解了常用欄位類型的匹配約定：

| 欄位類型 | 匹配約定 |
| --- | --- |
| 字串 | 帶有部分術語分析的文本，不區分大小寫 |
| 枚舉值 | 完全匹配，區分大小寫 |
| 整數 | 完全匹配 |
| 浮點 | 完全匹配 |
| 時間戳 | 完全匹配（DateTime格式） |
| 顯示名稱 | 帶有部分術語分析的文本，不區分大小寫 |

API中顯示的特定欄位有其他約定：

| 欄位 | 匹配約定 |
| --- | --- |
| `id` | 完全匹配，區分大小寫 |
| `delegate_descriptor_id` | 完全匹配，區分大小寫，並且術語拆分於 `::` |
| `name` | 完全匹配，區分大小寫 |
| `settings` | 帶有部分術語分析的文本，不區分大小寫 |
| `type` | 完全匹配，區分大小寫 |
