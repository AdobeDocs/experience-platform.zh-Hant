---
keywords: Experience Platform；首頁；熱門主題；源；連接器；源連接器；源sdk;sdk;SDK
title: 配置源SDK的源規範
topic-legacy: overview
description: 本文檔概述了使用源SDK時需要準備的配置。
hide: true
hidefromtoc: true
exl-id: f814c883-b529-4ecc-bedd-f638bf0014b5
source-git-commit: 9727f7b0e8eaae92c85f102e5e7bea018a2ee6de
workflow-type: tm+mt
source-wordcount: '861'
ht-degree: 1%

---

# 配置源SDK的源規範

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
| `sourceSpec.attributes.spec.properties.contentPath` | 定義包含需要接收到平台的項目清單的節點。 此屬性應遵循有效的JSON路徑語法，並必須指向特定陣列。 | 查看 [附錄](#content-path) 例如，內容路徑中包含的資源示例。 |
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
| `sourceSpec.attributes.spec.properties.paginationParams.type` | 顯示源支援的分頁類型的類型。 | <ul><li>`offset`:此分頁類型允許您通過指定從何處啟動結果陣列的索引以及返回結果數量的限制來分析結果。</li><li>`pointer`:此分頁類型允許您使用 `pointer` 變數，指向需要隨請求一起發送的特定項。 指針類型分頁要求負載中指向下一頁的路徑</li></ul> |
| `sourceSpec.attributes.spec.properties.paginationParams.limitName` | API可以指定在頁中讀取的記錄數的限制的名稱。 | `limit` 或 `count` |
| `sourceSpec.attributes.spec.properties.paginationParams.limitValue` | 要在頁面中提取的記錄數。 | `limit=10` 或 `count=10` |
| `sourceSpec.attributes.spec.properties.paginationParams.offSetName` | 偏移屬性名稱。 如果分頁類型設定為，則此為必需欄位 `offset`。 | `offset` |
| `sourceSpec.attributes.spec.properties.paginationParams.pointerPath` | 指針屬性名稱。 這需要指向下一頁的屬性的json路徑。 如果分頁類型設定為，則此為必需欄位 `pointer`。 | `pointer` |
| `sourceSpec.attributes.spec.properties.scheduleParams` | 包含為源定義支援的計畫格式的參數。 計畫參數包括 `startTime` 和 `endTime`，這兩個時間間隔都允許您為批處理運行設定特定時間間隔，這樣可確保不會再次提取在前一批處理運行中提取的記錄。 |
| `sourceSpec.attributes.spec.properties.scheduleParams.scheduleStartParamName` | 定義開始時間參數名稱 | `since_last_changed` |
| `sourceSpec.attributes.spec.properties.scheduleParams.scheduleEndParamName` | 定義結束時間參數名稱 | `before_last_changed` |
| `sourceSpec.attributes.spec.properties.scheduleParams.scheduleStartParamFormat` | 定義支援的格式 `scheduleStartParamName`。 | `yyyy-MM-ddTHH:mm:ssZ` |
| `sourceSpec.attributes.spec.properties.scheduleParams.scheduleEndParamFormat` | 定義支援的格式 `scheduleEndParamName`。 | `yyyy-MM-ddTHH:mm:ssZ` |
| `sourceSpec.spec.properties` | 定義用戶提供的參數以提取資源值。 | 查看 [附錄](#user-input) 例如用戶輸入的參數 `spec.properties`。 |

{style=&quot;table-layout:auto&quot;}

## 附錄 {#appendix}

### 內容路徑示例 {#content-path}

以下是 `contentPath` 屬性 [!DNL MailChimp Campaigns] 連接規範。

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

## 後續步驟

在填充了源規範後，您可以繼續為要整合到平台的源配置瀏覽規範。 查看上的文檔 [配置瀏覽規範](./explorespec.md) 的子菜單。
