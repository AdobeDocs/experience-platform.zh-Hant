---
keywords: Experience Platform；首頁；熱門主題；來源；連接器；來源連接器；來源sdk;sdk; SDK
title: 配置源SDK的驗證規範
topic-legacy: overview
description: 本檔案概述使用Sources SDK所需準備的設定。
hide: true
hidefromtoc: true
source-git-commit: d4b5b54be9fa2b430a3b45eded94a523b6bd4ef8
workflow-type: tm+mt
source-wordcount: '876'
ht-degree: 1%

---


# 配置源SDK的源規範

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
        "key": "{CATEGORY}"
      },
      "icon": {
        "key": "{ICON}"
      },
      "description": {
        "key": "{DESCRIPTION}"
      },
      "label": {
        "key": "{LABEL}"
      }
    },
    "urlParams": {
      "path": "{RESOURCE_PATH}",
      "method": "{GET_or_POST}",
      "queryParams": "{QUERY_PARAMS}"
    },
    "headerParams": "{HEADER_VALUES}",
    "bodyParams": "{BODY_PARAMS_USED_IF_METHOD_IS_POST}",
    "contentPath": {
      "path": "{PATH_SHOULD_POINT_TO_COLLECTION_OF_RECORDS}",
      "skipAttributes": [],
      "overrideWrapperAttribute": "{OVERRIDE_ATTRIBUTES}",
      "keepAttributes": ["action", "type", "timestamp"]
    },
    "explodeEntityPath": {
      "path": "{PATH_SHOULD_POINT_TO_COLLECTION_OF_RECORDS}",
      "skipAttributes": [],
      "overrideWrapperAttribute": "{OVERRIDE_ATTRIBUTES}",
      "keepAttributes": ["action", "type", "timestamp"]
    },
    "paginationParams": {
      "type": "{OFFSET_OR_POINTER}",
      "limitName": "{NUMBER_OF_RECORDS_ATTRIBUTE_NAME}",
      "limitValue": "{NUMBER_OF_RECORDS_PER_PAGE}",
      "offSetName": "{OFFSET_ATTRIBUTE_NAME_REQUIRED_IN_CASE_OF_OFFSET BASED_PAGINATION}",
      "pointerName": "{POINTER_PATH_REQUIRED_IN__CASE_OF_POINTER BASED_PAGINATION}"
    },
    "scheduleParams": {
      "scheduleStartParamName": "{START_TIME_PARAMETER_NAME}",
      "scheduleEndParamName": "{END_TIME_PARAMETER_NAME}",
      "scheduleStartParamFormat": "{DATE_TIME_FORMAT_FOR_START_TIME}",
      "scheduleEndParamFormat": "{END_TIME_FORMAT_FOR_START_TIME}"
    }
  },
  "spec": {
    "$schema": "http://json-schema.org/draft-07/schema#",
    "type": "object",
    "description": "Define user input parameters to fetch resource values.",
    "properties": "{USER_INPUT}"
  }
}
```

| 屬性 | 說明 | 範例 |
| --- | --- | --- |
| `sourceSpec.attributes` | 包含UI或API專用來源的相關資訊。 |
| `sourceSpec.attributes.uiAttributes` | 顯示UI專用來源的資訊。 |
| `sourceSpec.attributes.uiAttributes.isBeta` | 一個布林值屬性，指明源是否需要客戶提供更多反饋才能添加到其功能中。 | <ul><li>`true`</li><li>`false`</li></ul> |
| `sourceSpec.attributes.uiAttributes.category` | 定義源的類別。 | <ul><li>`advertising`</li><li>`cloud storage`</li><li>`crm`</li><li>`customer success`</li><li>`database`</li><li>`ecommerce`</li><li>`marketing automation`</li><li>`payments`</li><li>`protocols`</li><li>`streaming`</li></ul> |
| `sourceSpec.attributes.uiAttributes.icon` | 定義在Platform UI中轉譯來源時使用的圖示。 | `mailchimp-icon.svg` |
| `sourceSpec.attributes.uiAttributes.description` | 顯示源的簡短說明。 |
| `sourceSpec.attributes.uiAttributes.label` | 在Platform UI中顯示用於轉譯來源的標籤。 |
| `sourceSpec.attributes.urlParams` | 包含URL資源路徑、方法和支援的查詢參數的相關資訊。 |
| `sourceSpec.attributes.urlParams.path` | 定義從中提取資料的資源路徑。 | `/3.0/reports/${campaignId}/email-activity` |
| `sourceSpec.attributes.urlParams.method` | 定義要用來向資源提出要求以擷取資料的HTTP方法。 | `GET`、`POST` |
| `sourceSpec.attributes.urlParams.queryParams` | 定義支援的查詢參數，當提出擷取資料的要求時，可用來附加來源URL。 查詢參數必須是逗號(`,`)分隔的索引鍵值配對。 **附註**:任何由用戶提供的參數值都必須格式化為佔位符。 例如: `${USER_PARAMETER}`。 | `exclude_fields=emails._links,id=${id}` |
| `sourceSpec.attributes.headerParams` | 定義逗號(`,`)擷取資料時，需要在HTTP要求中提供給來源URL的已分隔標題。 | `Content-Type=application/json,foo=bar&userHeader={{USER_HEADER_VALUE}}` |
| `sourceSpec.attributes.bodyParams` | 定義所需的內文參數。 只有在 `urlParams.method` 設為 `POST`. |
| `sourceSpec.attributes.contentPath` | 定義包含要擷取至Platform所需項目清單的節點。 此屬性應遵循有效的JSON路徑語法，且必須指向特定陣列。 | 請參閱 [附錄](#content-path) 例如內容路徑中包含的資源範例。 |
| `sourceSpec.attributes.contentPath.path` | 指向要擷取至Platform之收集記錄的路徑。 | `$.emails` |
| `sourceSpec.attributes.contentPath.skipAttributes` | 此屬性可讓您從內容路徑中識別的資源中識別要排除不被擷取的特定項目。 |
| `sourceSpec.attributes.contentPath.overrideWrapperAttribute` | 此屬性可讓您覆寫您在 `contentPath`. |
| `sourceSpec.attributes.contentPath.keepAttributes` | 此屬性可讓您明確指定要映射的個別屬性。 |
| `sourceSpec.attributes.explodeEntityPath` | 此屬性可讓您平面化兩個陣列，並將資源資料轉換為Platform資源。 |
| `sourceSpec.attributes.explodeEntityPath.path` | 指向您要平面化之集合記錄的路徑。 | `$.email.activity` |
| `sourceSpec.attributes.explodeEntityPath.skipAttributes` | 此屬性可讓您從實體路徑中識別的資源中識別要排除不被擷取的特定項目。 |
| `sourceSpec.attributes.explodeEntityPath.overrideWrapperAttribute` | 此屬性可讓您覆寫您在 `explodeEntityPath`. |
| `sourceSpec.attributes.explodeEntityPath.keepAttributes` | 此屬性可讓您明確指定要映射的個別屬性。 |
| `sourceSpec.attributes.paginationParams` | 定義必須提供的參數或欄位，以便從使用者目前的頁面回應或建立下一頁URL時取得下一頁的連結。 |
| `sourceSpec.attributes.paginationParams.type` | 顯示來源支援的分頁類型類型。 | <ul><li>`offset`:此分頁類型可讓您透過指定索引來剖析結果，以從何處啟動產生的陣列，並限制傳回的結果數。</li><li>`pointer`:此分頁類型可讓您使用 `pointer` 變數來指向需要隨請求傳送的特定項目。 指標類型分頁需要裝載中指向下一頁的路徑</li></ul> |
| `sourceSpec.attributes.paginationParams.limitName` | API可透過的限制名稱，指定要在頁面中擷取的記錄數。 | `count` |
| `sourceSpec.attributes.paginationParams.limitValue` | 要在頁面中擷取的記錄數。 | `100` |
| `sourceSpec.attributes.paginationParams.offSetName` | 偏移屬性名稱。 如果分頁類型設為，則此為必要項目 `offset`. | `offset` |
| `sourceSpec.attributes.paginationParams.pointerName` | 指針屬性名稱。 這需要指向下一頁的屬性的json路徑。 如果分頁類型設為，則此為必要項目 `pointer`. | `pointer` |
| `sourceSpec.attributes.scheduleParams` | 包含定義源支援的調度格式的參數。 排程參數包括 `startTime` 和 `endTime`，兩者皆可讓您設定批次執行的特定時間間隔，確保先前批次執行中擷取的記錄不會再次擷取。 |
| `sourceSpec.attributes.scheduleParams.scheduleStartParamName` | 定義開始時間參數名稱 | `since_last_changed` |
| `sourceSpec.attributes.scheduleParams.scheduleEndParamName` | 定義結束時間參數名稱 | `before_last_changed` |
| `sourceSpec.attributes.scheduleParams.scheduleStartParamFormat` | 定義 `scheduleStartParamName`. | `yyyy-MM-ddTHH:mm:ssZ` |
| `sourceSpec.attributes.scheduleParams.scheduleEndParamFormat` | 定義 `scheduleEndParamName`. | `yyyy-MM-ddTHH:mm:ssZ` |
| `sourceSpec.spec.properties` | 定義用戶提供的參數以獲取資源值。 | 請參閱 [附錄](#user-input) 例如，用戶輸入的參數 `spec.properties`. |

{style=&quot;table-layout:auto&quot;}

## 附錄 {#appendix}

### 內容路徑範例 {#content-path}

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

填入源規範後，您可以繼續為要整合到Platform的源配置瀏覽規範。 請參閱 [配置瀏覽規範](./explorespec.md) 以取得更多資訊。