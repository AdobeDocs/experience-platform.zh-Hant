---
keywords: Experience Platform；首頁；熱門主題；源；連接器；源連接器；源sdk;sdk;SDK
title: 配置自助源源的源規範（批處理SDK）
topic-legacy: overview
description: 本文檔概述了使用自助源（批處理SDK）所需準備的配置。
exl-id: f814c883-b529-4ecc-bedd-f638bf0014b5
source-git-commit: adaa0e1a63536bc1fdf751eec477e5cda9fd20ae
workflow-type: tm+mt
source-wordcount: '1690'
ht-degree: 1%

---

# 配置自助源源的源規範（批處理SDK）

源規範包含特定於源的資訊，包括與源的類別、測試狀態和目錄表徵圖相關的屬性。 它們還包含URL參數、內容、標題和時間表等有用資訊。 源規範還描述了從基本連接建立源連接所需參數的模式。 建立源連接時必須使用架構。

查看 [附錄](#source-spec) 例如，完全填充的源規範。


```json
"sourceSpec": {
  "attributes": {
    "uiAttributes": {
      "isSource": true,
      "isPreview": true,
      "isBeta": true,
      "category": {
        "key": "protocols"
      },
      "icon": {
        "key": "genericRestIcon"
      },
      "description": {
        "key": "genericRestDescription"
      },
      "label": {
        "key": "genericRestLabel"
      }
    },
    "spec": {
      "$schema": "http://json-schema.org/draft-07/schema#",
      "type": "object",
      "description": "Defines static and user input parameters to fetch resource values.",
      "properties": {
        "urlParams": {
          "type": "object",
          "properties": {
            "host": {
              "type": "string",
              "description": "Enter resource url host path.",
              "example": "https://{domain}.api.mailchimp.com"
            },
            "path": {
              "type": "string",
              "description": "Enter resource path",
              "example": "/3.0/reports/campaignId/email-activity"
            },
            "method": {
              "type": "string",
              "description": "HTTP method type.",
              "enum": [
                "GET",
                "POST"
              ]
            },
            "queryParams": {
              "type": "object",
              "description": "The query parameters in json format",
            }
          },
          "required": [
            "host",
            "path",
            "method"
          ]
        },
        "headerParams": {
          "type": "object",
          "description": "The header parameters in json format",
        },
        "contentPath": {
          "type": "object",
          "description": "The parameters required for main collection content.",
          "properties": {
            "path": {
              "description": "The path to the main content.",
              "type": "string",
              "example": "$.emails"
            },
            "skipAttributes": {
              "type": "array",
              "description": "The list of attributes that needs to be skipped while fattening the array.",
              "example": "[total_items]",
              "items": {
                "type": "string"
              }
            },
            "keepAttributes": {
              "type": "array",
              "description": "The list of attributes that needs to be kept while fattening the array.",
              "example": "[total_items]",
              "items": {
                "type": "string"
              }
            },
            "overrideWrapperAttribute": {
              "type": "string",
              "description": "The new name to be used for the root content path node.",
              "example": "email"
            }
          },
          "required": [
            "path"
          ]
        },
        "explodeEntityPath": {
          "type": "object",
          "description": "The parameters required for the sub-array content.",
          "properties": {
            "path": {
              "description": "The path to the sub-array content.",
              "type": "string",
              "example": "$.email.activity"
            },
            "skipAttributes": {
              "type": "array",
              "description": "The list of attributes that needs to be skipped while fattening sub-array.",
              "example": "[total_items]",
              "items": {
                "type": "string"
              }
            },
            "keepAttributes": {
              "type": "array",
              "description": "The list of attributes that needs to be kept while fattening the sub-array.",
              "example": "[total_items]",
              "items": {
                "type": "string"
              }
            },
            "overrideWrapperAttribute": {
              "type": "string",
              "description": "The new name to be used for the  root content path node.",
              "example": "activity"
            }
          },
          "required": [
            "path"
          ]
        },
        "paginationParams": {
          "type": "object",
          "description": "The parameters required to fetch data using pagination.",
          "properties": {
            "type": {
              "description": "The pagination fetch type.",
              "type": "string",
              "enum": [
                "OFFSET",
                "POINTER"
              ]
            },
            "limitName": {
              "type": "string",
              "description": "The limit property name",
              "example": "limit or count"
            },
            "limitValue": {
              "type": "integer",
              "description": "The number of records to fetch per page.",
              "example": "limit=10 or count=10"
            },
            "offsetName": {
              "type": "string",
              "description": "The offset property name",
              "example": "offset"
            },
            "pointerPath": {
              "type": "string",
              "description": "The path to pointer property",
              "example": "$.paging.next"
            }
          },
          "required": [
            "type",
            "limitName",
            "limitValue"
          ]
        },
        "scheduleParams": {
          "type": "object",
          "description": "The parameters required to fetch data for batch schedule.",
          "properties": {
            "scheduleStartParamName": {
              "type": "string",
              "description": "The order property name to get the order by date."
            },
            "scheduleEndParamName": {
              "type": "string",
              "description": "The order property name to get the order by date."
            },
            "scheduleStartParamFormat": {
              "type": "string",
              "description": "The order property name to get the order by date.",
              "example": "yyyy-MM-ddTHH:mm:ssZ"
            },
            "scheduleEndParamFormat": {
              "type": "string",
              "description": "The order property name to get the order by date.",
              "example": "yyyy-MM-ddTHH:mm:ssZ"
            }
          },
          "required": [
            "scheduleStartParamName",
            "scheduleEndParamName"
          ]
        }
      },
      "required": [
        "urlParams",
        "contentPath",
        "paginationParams",
        "scheduleParams"
      ]
    }
  },
}
```

| 屬性 | 說明 | 範例 |
| --- | --- | --- |
| `sourceSpec.attributes` | 包含有關特定於UI或API的源的資訊。 |
| `sourceSpec.attributes.uiAttributes` | 顯示特定於UI的源的資訊。 |
| `sourceSpec.attributes.uiAttributes.isBeta` | 一個布爾屬性，指明源是否需要客戶提供更多反饋才能添加到其功能中。 | <ul><li>`true`</li><li>`false`</li></ul> |
| `sourceSpec.attributes.uiAttributes.category` | 定義源的類別。 | <ul><li>`advertising`</li><li>`crm`</li><li>`customer success`</li><li>`database`</li><li>`ecommerce`</li><li>`marketing automation`</li><li>`payments`</li><li>`protocols`</li></ul> |
| `sourceSpec.attributes.uiAttributes.icon` | 定義用於在平台UI中呈現源的表徵圖。 | `mailchimp-icon.svg` |
| `sourceSpec.attributes.uiAttributes.description` | 顯示源的簡要說明。 |
| `sourceSpec.attributes.uiAttributes.label` | 在平台UI中顯示用於呈現源的標籤。 |
| `sourceSpec.attributes.spec.properties.urlParams` | 包含有關URL資源路徑、方法和支援的查詢參數的資訊。 |
| `sourceSpec.attributes.spec.properties.urlParams.properties.path` | 定義從何處獲取資料的資源路徑。 | `/3.0/reports/${campaignId}/email-activity` |
| `sourceSpec.attributes.spec.properties.urlParams.properties.method` | 定義用於向資源請求讀取資料的HTTP方法。 | `GET`、`POST` |
| `sourceSpec.attributes.spec.properties.urlParams.properties.queryParams` | 定義支援的查詢參數，當請求提取資料時，這些參數可用於追加源URL。 **注釋**:任何用戶提供的參數值必須格式化為佔位符。 例如: `${USER_PARAMETER}`。 | `"queryParams" : {"key" : "value", "key1" : "value1"}` 將作為以下內容附加到源URL: `/?key=value&key1=value1` |
| `sourceSpec.attributes.spec.properties.spec.properties.headerParams` | 定義在讀取資料時需要在HTTP請求中提供到源URL的標頭。 | `"headerParams" : {"Content-Type" : "application/json", "x-api-key" : "key"}` |
| `sourceSpec.attributes.spec.properties.bodyParams` | 此屬性可配置為通過POST請求發送HTTP正文。 |
| `sourceSpec.attributes.spec.properties.contentPath` | 定義包含需要接收到平台的項目清單的節點。 此屬性應遵循有效的JSON路徑語法，並必須指向特定陣列。 | 查看 [附加資源科](#content-path) 例如，內容路徑中包含的資源示例。 |
| `sourceSpec.attributes.spec.properties.contentPath.path` | 指向要接收到平台的集合記錄的路徑。 | `$.emails` |
| `sourceSpec.attributes.spec.properties.contentPath.skipAttributes` | 此屬性允許您從內容路徑中標識的資源中標識要排除的、不被攝入的特定項。 | `[total_items]` |
| `sourceSpec.attributes.spec.properties.contentPath.keepAttributes` | 此屬性允許您顯式指定要保留的單個屬性。 | `[total_items]` |
| `sourceSpec.attributes.spec.properties.contentPath.overrideWrapperAttribute` | 此屬性允許您覆蓋在中指定的屬性名稱的值 `contentPath`。 | `email` |
| `sourceSpec.attributes.spec.properties.explodeEntityPath` | 此屬性允許您拼合兩個陣列並將資源資料轉換為平台資源。 |
| `sourceSpec.attributes.spec.properties.explodeEntityPath.path` | 指向要拼合的集合記錄的路徑。 | `$.email.activity` |
| `sourceSpec.attributes.spec.properties.explodeEntityPath.skipAttributes` | 此屬性允許您從實體路徑中標識的資源中標識要排除的、不被攝入的特定項。 | `[total_items]` |
| `sourceSpec.attributes.spec.properties.explodeEntityPath.keepAttributes` | 此屬性允許您顯式指定要保留的單個屬性。 | `[total_items]` |
| `sourceSpec.attributes.spec.properties.explodeEntityPath.overrideWrapperAttribute` | 此屬性允許您覆蓋在中指定的屬性名稱的值 `explodeEntityPath`。 | `activity` |
| `sourceSpec.attributes.spec.properties.paginationParams` | 定義必須提供的參數或欄位，以便從用戶的當前頁面響應或在建立下一頁URL時獲取到下一頁的連結。 |
| `sourceSpec.attributes.spec.properties.paginationParams.type` | 顯示源支援的分頁類型的類型。 | <ul><li>`OFFSET`:此分頁類型允許您通過指定從何處啟動結果陣列的索引以及返回結果數量的限制來分析結果。</li><li>`POINTER`:此分頁類型允許您使用 `pointer` 變數，指向需要隨請求一起發送的特定項。 指針類型分頁要求負載中指向下一頁的路徑。</li><li>`CONTINUATION_TOKEN`:此分頁類型允許您將查詢或標頭參數附加為連續標籤，以從源中檢索剩餘的返回資料，由於預先確定的最大值，最初未返回這些資料。</li><li>`PAGE`:此分頁類型允許您將查詢參數與分頁參數一起追加，以便從零頁開始按頁遍歷返回資料。</li><li>`NONE`:此分頁類型可用於不支援任何可用分頁類型的源。 分頁類型 `NONE` 在請求後返回整個響應資料。</li></ul> |
| `sourceSpec.attributes.spec.properties.paginationParams.limitName` | API可以指定在頁中讀取的記錄數的限制的名稱。 | `limit` 或 `count` |
| `sourceSpec.attributes.spec.properties.paginationParams.limitValue` | 要在頁面中提取的記錄數。 | `limit=10` 或 `count=10` |
| `sourceSpec.attributes.spec.properties.paginationParams.offSetName` | 偏移屬性名稱。 如果分頁類型設定為，則此為必需欄位 `offset`。 | `offset` |
| `sourceSpec.attributes.spec.properties.paginationParams.pointerPath` | 指針屬性名稱。 這需要指向下一頁的屬性的json路徑。 如果分頁類型設定為，則此為必需欄位 `pointer`。 | `pointer` |
| `sourceSpec.attributes.spec.properties.scheduleParams` | 包含為源定義支援的計畫格式的參數。 計畫參數包括 `startTime` 和 `endTime`，這兩個時間間隔都允許您為批處理運行設定特定時間間隔，這樣可確保不會再次提取在前一批處理運行中提取的記錄。 |
| `sourceSpec.attributes.spec.properties.scheduleParams.scheduleStartParamName` | 定義開始時間參數名稱 | `since_last_changed` |
| `sourceSpec.attributes.spec.properties.scheduleParams.scheduleEndParamName` | 定義結束時間參數名稱 | `before_last_changed` |
| `sourceSpec.attributes.spec.properties.scheduleParams.scheduleStartParamFormat` | 定義支援的格式 `scheduleStartParamName`。 | `yyyy-MM-ddTHH:mm:ssZ` |
| `sourceSpec.attributes.spec.properties.scheduleParams.scheduleEndParamFormat` | 定義支援的格式 `scheduleEndParamName`。 | `yyyy-MM-ddTHH:mm:ssZ` |
| `sourceSpec.spec.properties` | 定義用戶提供的參數以提取資源值。 | 查看 [額外資源](#user-input) 例如用戶輸入的參數 `spec.properties`。 |

{style=&quot;table-layout:auto&quot;}

## 其他資源 {#appendix}

以下各節提供了有關您可以對 `sourceSpec`包括高級計畫和自定義架構。

### 內容路徑示例 {#content-path}

以下是 `contentPath` 屬性 [!DNL MailChimp Members] 連接規範。

```json
"contentPath": {
  "path": "$.members",
  "skipAttributes": [
    "_links",
    "total_items",
    "list_id"
  ],
  "overrideWrapperAttribute": "member"
}
```

### `spec.properties` 用戶輸入示例 {#user-input}

以下是用戶提供的示例 `spec.properties` 使用 [!DNL MailChimp Members] 連接規範。

在本例中， `listId` 作為 `urlParams.path`。 如果需要檢索 `listId` 從客戶那裡，您還必須將其定義為 `spec.properties`。


```json
"urlParams": {
        "path": "/3.0/lists/${listId}/members",
        "method": "GET"
      }
"spec": {
      "$schema": "http://json-schema.org/draft-07/schema#",
      "type": "object",
      "description": "Define user input parameters to fetch resource values.",
      "properties": {
        "listId": {
          "type": "string",
          "description": "listId for which members need to fetch."
        }
      }
    }
```

### 源規格示例 {#source-spec}

以下是使用 [!DNL MailChimp Members]:

```json
  "sourceSpec": {
    "attributes": {
      "uiAttributes": {
        "isSource": true,
        "isPreview": true,
        "isBeta": true,
        "category": {
          "key": "marketingAutomation"
        },
        "icon": {
          "key": "mailchimpMembersIcon"
        },
        "description": {
          "key": "mailchimpMembersDescription"
        },
        "label": {
          "key": "mailchimpMembersLabel"
        }
      },
      "urlParams": {
        "host": "https://{domain}.api.mailchimp.com",
        "path": "/3.0/lists/${listId}/members",
        "method": "GET"
      },
      "contentPath": {
        "path": "$.members",
        "skipAttributes": [
          "_links",
          "total_items",
          "list_id"
        ],
        "overrideWrapperAttribute": "member"
      },
      "paginationParams": {
        "type": "OFFSET",
        "limitName": "count",
        "limitValue": "100",
        "offSetName": "offset"
      },
      "scheduleParams": {
        "scheduleStartParamName": "since_last_changed",
        "scheduleEndParamName": "before_last_changed",
        "scheduleStartParamFormat": "yyyy-MM-ddTHH:mm:ss:fffffffK",
        "scheduleEndParamFormat": "yyyy-MM-ddTHH:mm:ss:fffffffK"
      }
    },
    "spec": {
      "$schema": "http://json-schema.org/draft-07/schema#",
      "type": "object",
      "description": "Define user input parameters to fetch resource values.",
      "properties": {
        "listId": {
          "type": "string",
          "description": "listId for which members need to fetch."
        }
      }
    }
  }
```

### 為源配置不同的分頁類型 {#pagination}

以下是自助源（批處理SDK）支援的其他分頁類型的示例：

#### `CONTINUATION_TOKEN`

分頁的連續標籤類型返回字串標籤，該字串標籤表示由於在單個響應中可以返回的預定最大項目數而無法返回的項目數。

支援連續標籤類型分頁的源可能具有類似於：

```json
"paginationParams": {
  "type": "CONTINUATION_TOKEN",
  "continuationTokenPath": "$.meta.after_cursor",
  "parameterType": "QUERYPARAM",
  "parameterName": "page[after]",
  "delayRequestMillis": "850"
}
```

| 屬性 | 說明 |
| --- | --- |
| `type` | 用於返回資料的分頁類型。 |
| `continuationTokenPath` | 必須附加到查詢參數以移動到返回結果的下一頁的值。 |
| `parameterType` | 的 `parameterType` 屬性定義位置 `parameterName` 。 的 `QUERYPARAM` 類型允許您將查詢附加到 `parameterName`。 的 `HEADERPARAM` 允許您添加 `parameterName` 你的報頭請求。 |
| `parameterName` | 用於合併連續標籤的參數的名稱。 格式如下： `{PARAMETER_NAME}={CONTINUATION_TOKEN}`。 |
| `delayRequestMillis` | 的 `delayRequestMillis` 分頁中的屬性允許您控制向源發出請求的速率。 某些源可以限制每分鐘可發出的請求數。 比如說， [!DNL Zendesk] 每分鐘限制100個請求，並定義  `delayRequestMillis` 至 `850` 允許您將源配置為每分鐘大約80次請求進行呼叫，這一點低於每分鐘100次請求的閾值。 |

下面是使用連續標籤類型分頁返回的響應的示例：

```json
{
  "results": [
    {
      "id": 5624716025745,
      "url": "https://dev.zendesk.com/api/v2/users/5624716025745.json",
      "name": "newinctest@zenaep.com",
      "email": "newinctest@zenaep.com",
      "created_at": "2022-04-22T10:27:30Z",
      
    }
  ],
  "facets": null,
  "meta": {
    "has_more": false,
    "after_cursor": "eyJmaWVsZCI6ImNyZWF0ZWRfYXQiLCJk",
    "before_cursor": null
  },
  "links": {
    "prev": null,
    "next": "https://dev.zendesk.com/api/v2/search/export.json?filter%5Btype%5D=user&page%5Bafter%5D=eyJmaWVsZCI6"
  }
}
```

#### `PAGE`

的 `PAGE` 分頁類型允許您按從零開始的頁數遍歷返回資料。 使用時 `PAGE` 類型分頁，必須提供單頁中給定的記錄數。

```json
"paginationParams": {
  "type": "PAGE",
  "limitName": "records",
  "limitValue": "100",
  "pageParamName": "pageIndex",
  "maximumRequest": 10000
}
```

| 屬性 | 說明 |
| --- | --- |
| `type` | 用於返回資料的分頁類型。 |
| `limitName` | API可以指定在頁中讀取的記錄數的限制的名稱。 |
| `limitValue` | 要在頁面中提取的記錄數。 |
| `pageParamName` | 要遍歷返回資料的不同頁，必須追加到查詢參數的參數的名稱。 比如說， `https://abc.com?pageIndex=1` 將返回API返回負載的第二頁。 |
| `maximumRequest` | 源可為給定增量運行發出的最大請求數。 當前預設限制為10000。 |

#### `NONE`

的 `NONE` 分頁類型可用於不支援任何可用分頁類型的源。 使用分頁類型的源 `NONE` 只需在發出GET請求時返回所有可檢索的記錄。

```json
"paginationParams": {
  "type": "NONE"
}
```

### 自助源的高級計畫（批處理SDK）

使用高級計畫配置源的增量和回填計畫。 的 `incremental` 屬性允許您配置計畫，其中源將只接收新記錄或修改的記錄，而 `backfill` 屬性允許您建立接收歷史資料的計畫。

使用高級計畫，您可以使用特定於源的表達式和函式來配置增量和回填計畫。 在下面的示例中， [!DNL Zendesk] 源要求將增量計畫格式化為 `type:user updated > {START_TIME} updated < {END_TIME}` 和回填 `type:user updated < {END_TIME}`。

```json
"scheduleParams": {
        "type": "ADVANCE",
        "paramFormat": "yyyy-MM-ddTHH:mm:ssK",
        "incremental": "type:user updated > {START_TIME} updated < {END_TIME}",
        "backfill": "type:user updated < {END_TIME}"
      }
```

| 屬性 | 說明 |
| --- | --- |
| `scheduleParams.type` | 源將使用的計畫類型。 將此值設定為 `ADVANCE` 的子菜單。 |
| `scheduleParams.paramFormat` | 計畫參數的定義格式。 此值可以與源的 `scheduleStartParamFormat` 和 `scheduleEndParamFormat` 值。 |
| `scheduleParams.incremental` | 源的增量查詢。 增量是指只接收新資料或已修改資料的接收方法。 |
| `scheduleParams.backfill` | 源的回填查詢。 回填是指接收歷史資料的接收方法。 |

配置高級計畫後，必須參考 `scheduleParams` 的子菜單。 在下面的示例中， `{SCHEDULE_QUERY}` 是用於指定將使用增量和回填計畫表達式的位置的佔位符。 對於 [!DNL Zendesk] 源， `query` 在 `queryParams` 指定高級計畫。

```json
"urlParams": {
        "path": "/api/v2/search/export@{if(empty(coalesce(pipeline()?.parameters?.ingestionStart,'')),'?query=type:user&filter[type]=user&','')}",
        "method": "GET",
        "queryParams": {
          "query": "{SCHEDULE_QUERY}",
          "filter[type]": "user"
        }
      }
```

### 添加自定義架構以定義源的動態屬性

可以將自定義架構包含到 `sourceSpec` 定義源所需的所有屬性，包括可能需要的任何動態屬性。 您可以通過向PUT請求更新源的相應連接規範 `/connectionSpecs` 端點 [!DNL Flow Service] API，同時在 `sourceSpec` 連接規範的部分。

以下是可添加到源連接規範的自定義架構示例：

```json
      "schema": {
        "type": "object",
        "properties": {
          "results": {
            "type": "array",
            "items": {
              "type": "object",
              "properties": {
                "organization_id": {
                  "type": "integer",
                  "minimum": -9007199254740992,
                  "maximum": 9007199254740991
                }
                "active": {
                  "type": "boolean"
                },
                "created_at": {
                  "type": "string"
                },
                "email": {
                  "type": "string"
                },
                "iana_time_zone": {
                  "type": "string"
                },
                "id": {
                  "type": "integer"
                },
                "locale": {
                  "type": "string"
                },
                "locale_id": {
                  "type": "integer"
                },
                "moderator": {
                  "type": "boolean"
                },
                "name": {
                  "type": "string"
                },
                "only_private_comments": {
                  "type": "boolean"
                },
                "report_csv": {
                  "type": "boolean"
                },
                "restricted_agent": {
                  "type": "boolean"
                },
                "result_type": {
                  "type": "string"
                },
                "role": {
                  "type": "integer"
                },
                "shared": {
                  "type": "boolean"
                },
                "shared_agent": {
                  "type": "boolean"
                },
                "suspended": {
                  "type": "boolean"
                },
                "ticket_restriction": {
                  "type": "string"
                },
                "time_zone": {
                  "type": "string"
                },
                "two_factor_auth_enabled": {
                  "type": "boolean"
                },
                "updated_at": {
                  "type": "string"
                },
                "url": {
                  "type": "string"
                },
                "verified": {
                  "type": "boolean"
                },
                "tags": {
                  "type": "array",
                  "items": {
                    "type": "string"
                  }
                }
              }
            }
          }
        }
      }
```


## 後續步驟

在填充了源規範後，您可以繼續為要整合到平台的源配置瀏覽規範。 查看上的文檔 [配置瀏覽規範](./explorespec.md) 的子菜單。
