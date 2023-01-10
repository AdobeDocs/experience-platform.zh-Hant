---
keywords: Experience Platform；首頁；熱門主題；來源；連接器；來源連接器；來源sdk;sdk; SDK
title: 配置自助源的源規範(Batch SDK)
description: 本檔案概述使用自助來源（批次SDK）所需準備的設定。
exl-id: f814c883-b529-4ecc-bedd-f638bf0014b5
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '1690'
ht-degree: 1%

---

# 配置自助源的源規範（批SDK）

源規範包含源的特定資訊，包括與源的類別、測試版狀態和目錄表徵圖相關的屬性。 它們也包含有用的資訊，例如URL參數、內容、標題和排程。 源規範還描述了從基本連接建立源連接所需的參數的模式。 要建立源連接，必須使用架構。

請參閱 [附錄](#source-spec) 例如，完全填充的源規範。


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
| `sourceSpec.attributes` | 包含UI或API專用來源的相關資訊。 |
| `sourceSpec.attributes.uiAttributes` | 顯示UI專用來源的資訊。 |
| `sourceSpec.attributes.uiAttributes.isBeta` | 一個布林值屬性，指明源是否需要客戶提供更多反饋才能添加到其功能中。 | <ul><li>`true`</li><li>`false`</li></ul> |
| `sourceSpec.attributes.uiAttributes.category` | 定義源的類別。 | <ul><li>`advertising`</li><li>`crm`</li><li>`customer success`</li><li>`database`</li><li>`ecommerce`</li><li>`marketing automation`</li><li>`payments`</li><li>`protocols`</li></ul> |
| `sourceSpec.attributes.uiAttributes.icon` | 定義在Platform UI中轉譯來源時使用的圖示。 | `mailchimp-icon.svg` |
| `sourceSpec.attributes.uiAttributes.description` | 顯示源的簡短說明。 |
| `sourceSpec.attributes.uiAttributes.label` | 在Platform UI中顯示用於轉譯來源的標籤。 |
| `sourceSpec.attributes.spec.properties.urlParams` | 包含URL資源路徑、方法和支援的查詢參數的相關資訊。 |
| `sourceSpec.attributes.spec.properties.urlParams.properties.path` | 定義從中提取資料的資源路徑。 | `/3.0/reports/${campaignId}/email-activity` |
| `sourceSpec.attributes.spec.properties.urlParams.properties.method` | 定義要用來向資源提出要求以擷取資料的HTTP方法。 | `GET`、`POST` |
| `sourceSpec.attributes.spec.properties.urlParams.properties.queryParams` | 定義支援的查詢參數，當提出擷取資料的要求時，可用來附加來源URL。 **附註**:任何由用戶提供的參數值都必須格式化為佔位符。 例如: `${USER_PARAMETER}`. | `"queryParams" : {"key" : "value", "key1" : "value1"}` 會附加至來源URL，如下所示： `/?key=value&key1=value1` |
| `sourceSpec.attributes.spec.properties.spec.properties.headerParams` | 定義擷取資料時，需在HTTP要求中提供給來源URL的標題。 | `"headerParams" : {"Content-Type" : "application/json", "x-api-key" : "key"}` |
| `sourceSpec.attributes.spec.properties.bodyParams` | 此屬性可設定為透過POST要求傳送HTTP內文。 |
| `sourceSpec.attributes.spec.properties.contentPath` | 定義包含要擷取至Platform所需項目清單的節點。 此屬性應遵循有效的JSON路徑語法，且必須指向特定陣列。 | 檢視 [其他資源科](#content-path) 例如內容路徑中包含的資源範例。 |
| `sourceSpec.attributes.spec.properties.contentPath.path` | 指向要擷取至Platform之收集記錄的路徑。 | `$.emails` |
| `sourceSpec.attributes.spec.properties.contentPath.skipAttributes` | 此屬性可讓您從內容路徑中識別的資源中識別要排除不被擷取的特定項目。 | `[total_items]` |
| `sourceSpec.attributes.spec.properties.contentPath.keepAttributes` | 此屬性可讓您明確指定要保留的個別屬性。 | `[total_items]` |
| `sourceSpec.attributes.spec.properties.contentPath.overrideWrapperAttribute` | 此屬性可讓您覆寫您在 `contentPath`. | `email` |
| `sourceSpec.attributes.spec.properties.explodeEntityPath` | 此屬性可讓您平面化兩個陣列，並將資源資料轉換為Platform資源。 |
| `sourceSpec.attributes.spec.properties.explodeEntityPath.path` | 指向您要平面化之集合記錄的路徑。 | `$.email.activity` |
| `sourceSpec.attributes.spec.properties.explodeEntityPath.skipAttributes` | 此屬性可讓您從實體路徑中識別的資源中識別要排除不被擷取的特定項目。 | `[total_items]` |
| `sourceSpec.attributes.spec.properties.explodeEntityPath.keepAttributes` | 此屬性可讓您明確指定要保留的個別屬性。 | `[total_items]` |
| `sourceSpec.attributes.spec.properties.explodeEntityPath.overrideWrapperAttribute` | 此屬性可讓您覆寫您在 `explodeEntityPath`. | `activity` |
| `sourceSpec.attributes.spec.properties.paginationParams` | 定義必須提供的參數或欄位，以便從使用者目前的頁面回應或建立下一頁URL時取得下一頁的連結。 |
| `sourceSpec.attributes.spec.properties.paginationParams.type` | 顯示來源支援的分頁類型類型。 | <ul><li>`OFFSET`:此分頁類型可讓您透過指定索引來剖析結果，以從何處啟動產生的陣列，並限制傳回的結果數。</li><li>`POINTER`:此分頁類型可讓您使用 `pointer` 變數來指向需要隨請求傳送的特定項目。 指標類型分頁需要裝載中指向下一頁的路徑。</li><li>`CONTINUATION_TOKEN`:此分頁類型可讓您將查詢或標題參數附加至繼續Token，以從來源擷取剩餘的傳回資料，而最初由於預先決定的上限而未傳回。</li><li>`PAGE`:此分頁類型可讓您將查詢參數附加至分頁參數，以依頁面從零開始遍歷傳回的資料。</li><li>`NONE`:此分頁類型可用於不支援任何可用分頁類型的來源。 分頁類型 `NONE` 在請求後傳回整個回應資料。</li></ul> |
| `sourceSpec.attributes.spec.properties.paginationParams.limitName` | API可透過的限制名稱，指定要在頁面中擷取的記錄數。 | `limit` 或 `count` |
| `sourceSpec.attributes.spec.properties.paginationParams.limitValue` | 要在頁面中擷取的記錄數。 | `limit=10` 或 `count=10` |
| `sourceSpec.attributes.spec.properties.paginationParams.offSetName` | 偏移屬性名稱。 如果分頁類型設為，則此為必要項目 `offset`. | `offset` |
| `sourceSpec.attributes.spec.properties.paginationParams.pointerPath` | 指針屬性名稱。 這需要指向下一頁的屬性的json路徑。 如果分頁類型設為，則此為必要項目 `pointer`. | `pointer` |
| `sourceSpec.attributes.spec.properties.scheduleParams` | 包含定義源支援的調度格式的參數。 排程參數包括 `startTime` 和 `endTime`，兩者皆可讓您設定批次執行的特定時間間隔，確保先前批次執行中擷取的記錄不會再次擷取。 |
| `sourceSpec.attributes.spec.properties.scheduleParams.scheduleStartParamName` | 定義開始時間參數名稱 | `since_last_changed` |
| `sourceSpec.attributes.spec.properties.scheduleParams.scheduleEndParamName` | 定義結束時間參數名稱 | `before_last_changed` |
| `sourceSpec.attributes.spec.properties.scheduleParams.scheduleStartParamFormat` | 定義 `scheduleStartParamName`. | `yyyy-MM-ddTHH:mm:ssZ` |
| `sourceSpec.attributes.spec.properties.scheduleParams.scheduleEndParamFormat` | 定義 `scheduleEndParamName`. | `yyyy-MM-ddTHH:mm:ssZ` |
| `sourceSpec.spec.properties` | 定義用戶提供的參數以獲取資源值。 | 請參閱 [其他資源](#user-input) 例如，用戶輸入的參數 `spec.properties`. |

{style=&quot;table-layout:auto&quot;}

## 其他資源 {#appendix}

以下小節提供您可對 `sourceSpec`，包括進階排程和自訂結構。

### 內容路徑範例 {#content-path}

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

### `spec.properties` 使用者輸入範例 {#user-input}

以下是使用者提供的範例 `spec.properties` 使用 [!DNL MailChimp Members] 連接規範。

在此範例中， `listId` 作為 `urlParams.path`. 如果您需要擷取 `listId` 從客戶，則您也必須將其定義為 `spec.properties`.


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

以下是已完成的源規範，使用 [!DNL MailChimp Members]:

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

### 為來源設定不同的分頁類型 {#pagination}

以下是自助來源（批次SDK）支援的其他分頁類型範例：

#### `CONTINUATION_TOKEN`

分頁的持續令牌類型傳回字串令牌，表示由於可在單一回應中傳回的項目數上限，而有更多無法傳回的項目存在。

支援連續代號類型分頁的來源可能具有類似以下的分頁參數：

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
| `type` | 用於傳回資料的分頁類型。 |
| `continuationTokenPath` | 必須附加至查詢參數的值，才能移至傳回結果的下一頁。 |
| `parameterType` | 此 `parameterType` 屬性會定義 `parameterName` 必須新增。 此 `QUERYPARAM` 類型可讓您將查詢附加至 `parameterName`. 此 `HEADERPARAM` 可讓您新增 `parameterName` 填入標題請求。 |
| `parameterName` | 用於併入延續代號的參數名稱。 格式如下： `{PARAMETER_NAME}={CONTINUATION_TOKEN}`. |
| `delayRequestMillis` | 此 `delayRequestMillis` 分頁中的屬性可讓您控制對來源提出的請求率。 某些來源可限制每分鐘可提出的請求數。 例如， [!DNL Zendesk] 每分鐘有100個請求，並定義  `delayRequestMillis` to `850` 可讓您將來源設定為每分鐘大約80個請求進行呼叫，且低於每分鐘100個請求的臨界值。 |

以下是使用分頁的連續Token類型傳回的回應範例：

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

此 `PAGE` 分頁類型可讓您依從零開始的頁數遍歷傳回的資料。 使用時 `PAGE` 類型分頁，您必須提供單一頁面中指定的記錄數。

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
| `type` | 用於傳回資料的分頁類型。 |
| `limitName` | API可透過的限制名稱，指定要在頁面中擷取的記錄數。 |
| `limitValue` | 要在頁面中擷取的記錄數。 |
| `pageParamName` | 必須附加至查詢參數以周遊傳回資料的不同頁面的參數名稱。 例如， `https://abc.com?pageIndex=1` 會傳回API傳回裝載的第二頁。 |
| `maximumRequest` | 源可針對給定增量運行發出的最大請求數。 當前預設限制為10000。 |

#### `NONE`

此 `NONE` 分頁類型可用於不支援任何可用分頁類型的來源。 使用分頁類型的來源 `NONE` 只需在提出GET請求時返回所有可檢索的記錄。

```json
"paginationParams": {
  "type": "NONE"
}
```

### 自助來源的進階排程(Batch SDK)

使用進階排程來設定來源的增量和回填排程。 此 `incremental` 屬性可讓您設定排程，其中您的來源只會擷取新記錄或修改的記錄，而 `backfill` 屬性可讓您建立排程來內嵌歷史資料。

使用進階排程，您可以使用來源專屬的運算式和函式來設定增量和回填排程。 在以下範例中， [!DNL Zendesk] 源需要將增量計畫格式化為 `type:user updated > {START_TIME} updated < {END_TIME}` 回填 `type:user updated < {END_TIME}`.

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
| `scheduleParams.type` | 源將使用的計畫類型。 將此值設為 `ADVANCE` 以使用進階排程類型。 |
| `scheduleParams.paramFormat` | 排程參數的已定義格式。 此值可以與來源的 `scheduleStartParamFormat` 和 `scheduleEndParamFormat` 值。 |
| `scheduleParams.incremental` | 源的增量查詢。 增量是指僅擷取新資料或修改資料的擷取方法。 |
| `scheduleParams.backfill` | 源的回填查詢。 回填是指擷取歷史資料的擷取方法。 |

設定進階排程後，您必須參考 `scheduleParams` 在URL、body或header參數區段中，視您的特定來源支援而定。 在以下範例中， `{SCHEDULE_QUERY}` 是預留位置，用於指定將使用增量和回填排程運算式的位置。 若 [!DNL Zendesk] 來源， `query` 用於 `queryParams` 指定高級計畫。

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

### 新增自訂結構以定義來源的動態屬性

您可以將自訂結構包含在 `sourceSpec` 來定義源所需的所有屬性，包括您可能需要的任何動態屬性。 您可以向發出PUT請求，以更新來源的對應連線規格 `/connectionSpecs` 端點 [!DNL Flow Service] API，同時在 `sourceSpec` 連接規範的部分。

以下是可添加到源的連接規範的自定義架構的示例：

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

填入源規範後，您可以繼續為要整合到Platform的源配置瀏覽規範。 請參閱 [配置瀏覽規範](./explorespec.md) 以取得更多資訊。
