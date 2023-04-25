---
keywords: Experience Platform；首頁；熱門主題；流量服務；流量服務API；來源；來源
title: 使用流量服務API篩選來源的列層級資料
description: 本教學課程涵蓋如何使用流量服務API在來源層級篩選資料的步驟
exl-id: 224b454e-a079-4df3-a8b2-1bebfb37d11f
source-git-commit: da6f5a79b1ee16fb0d44a5c2990ed1b8be1f99e2
workflow-type: tm+mt
source-wordcount: '785'
ht-degree: 3%

---

# 使用 [!DNL Flow Service] API

>[!IMPORTANT]
>
>篩選列層級資料的支援目前僅適用於下列來源：
>
>* [Google BigQuery](../../connectors/databases/bigquery.md)
>* [Microsoft Dynamics](../../connectors/crm/ms-dynamics.md)
>* [Salesforce](../../connectors/crm/salesforce.md)
>* [SalesforceMarketing Cloud](../../connectors/marketing-automation/salesforce-marketing-cloud.md)
>* [Snowflake](../../connectors/databases/snowflake.md)


本教學課程提供如何使用 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## 快速入門

本教學課程需要您妥善了解下列Adobe Experience Platform元件：

* [來源](../../home.md): [!DNL Experience Platform] 可讓您從各種來源擷取資料，同時使用來建構、加標籤及增強傳入資料 [!DNL Platform] 服務。
* [沙箱](../../../sandboxes/home.md): [!DNL Experience Platform] 提供可分割單一沙箱的虛擬沙箱 [!DNL Platform] 例項放入個別的虛擬環境，以協助開發及改進數位體驗應用程式。

### 使用平台API

如需如何成功呼叫Platform API的詳細資訊，請參閱 [Platform API快速入門](../../../landing/api-guide.md).

## 篩選源資料

以下概述篩選來源的列層級資料所應採取的步驟。

### 查找連接規格

您必須先檢索源的連接規範詳細資訊，以確定特定源支援的運算子和語言，才能使用API篩選源的行級資料。

要檢索給定源的連接規範，請向 `/connectionSpecs` 端點 [!DNL Flow Service] API，同時提供來源的屬性名稱作為查詢參數的一部分。

**API格式**

```http
GET /connectionSpecs/{QUERY_PARAMS}
```

| 參數 | 說明 |
| --- | --- |
| `{QUERY_PARAMS}` | 要篩選結果的可選查詢參數。 您可以擷取 [!DNL Google BigQuery] 通過應用連接規範 `name` 屬性和指定 `"google-big-query"` 在您的搜尋中。 |

**要求**

下列請求會擷取 [!DNL Google BigQuery].

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/connectionSpecs?property=name=="google-big-query"' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應會傳回 [!DNL Google BigQuery]，包括其支援查詢語言和邏輯運算子的相關資訊。

>[!NOTE]
>
>以下的API回應會因為簡潔而截斷。

```json
"attributes": {
  "filterAtSource": {
    "enabled": true,
    "queryLanguage": "SQL",
    "logicalOperators": [
      "and",
      "or",
      "not"
    ],
    "comparisonOperators": [
      "=",
      "!=",
      "<",
      "<=",
      ">",
      ">=",
      "like",
      "in"
    ],
    "columnNameEscapeChar": "`",
    "valueEscapeChar": "'"
  }
```

| 屬性 | 說明 |
| --- | --- |
| `attributes.filterAtSource.enabled` | 確定查詢的源是否支援篩選行級資料。 |
| `attributes.filterAtSource.queryLanguage` | 確定查詢源支援的查詢語言。 |
| `attributes.filterAtSource.logicalOperators` | 確定可用於篩選源行級資料的邏輯運算子。 |
| `attributes.filterAtSource.comparisonOperators` | 決定可用來篩選來源之列層級資料的比較運算子。 如需比較運算子的詳細資訊，請參閱下表。 |
| `attributes.filterAtSource.columnNameEscapeChar` | 確定用於轉義列的字元。 |
| `attributes.filterAtSource.valueEscapeChar` | 確定在寫入SQL查詢時如何包圍值。 |

{style="table-layout:auto"}

#### 比較運算子

| 運算子 | 說明 |
| --- | --- |
| `==` | 依屬性是否等於提供的值進行篩選。 |
| `!=` | 依屬性是否不等於提供的值進行篩選。 |
| `<` | 依屬性是否小於提供的值進行篩選。 |
| `>` | 依屬性是否大於提供的值進行篩選。 |
| `<=` | 依屬性是否小於或等於提供的值進行篩選。 |
| `>=` | 依屬性是否大於或等於提供的值進行篩選。 |
| `like` | 在中使用以篩選 `WHERE` 子句來搜索指定的模式。 |
| `in` | 依屬性是否在指定範圍內進行篩選。 |

{style="table-layout:auto"}

### 指定擷取的篩選條件

在確定源支援的邏輯運算子和查詢語言後，可以使用配置檔案查詢語言(PQL)指定要應用於源資料的篩選條件。

在以下範例中，僅套用條件，以選取與列為參數的節點類型所提供值相等的資料。

```json
{
  "type": "PQL",
  "format": "pql/json",
  "value": {
    "nodeType": "fnApply",
    "fnName": "=",
    "params": [
      {
        "nodeType": "fieldLookup",
        "fieldName": "city"
      },
      {
        "nodeType": "literal",
        "value": "DDN"
      }
    ]
  }
}
```

### 預覽您的資料

您可以向 `/explore` 端點 [!DNL Flow Service] API，同時提供 `filters` 作為查詢參數的一部分，並指定PQL輸入條件， [!DNL Base64].

**API格式**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=table&object={TABLE_PATH}&preview=true&filters={FILTERS}
```

| 參數 | 說明 |
| --- | --- |
| `{BASE_CONNECTION_ID}` | 源的基本連接ID。 |
| `{TABLE_PATH}` | 要檢查的表的路徑屬性。 |
| `{FILTERS}` | 以編碼的PQL篩選條件 [!DNL Base64]. |

**要求**

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/connections/89d1459e-3cd0-4069-acb3-68f240db4eeb/explore?objectType=table&object=TESTFAS.FASTABLE&preview=true&filters=ewogICJ0eXBlIjogIlBRTCIsCiAgImZvcm1hdCI6ICJwcWwvanNvbiIsCiAgInZhbHVlIjogewogICAgIm5vZGVUeXBlIjogImZuQXBwbHkiLAogICAgImZuTmFtZSI6ICJhbmQiLAogICAgInBhcmFtcyI6IFsKICAgICAgewogICAgICAgICJub2RlVHlwZSI6ICJmbkFwcGx5IiwKICAgICAgICAiZm5OYW1lIjogImxpa2UiLAogICAgICAgICJwYXJhbXMiOiBbCiAgICAgICAgICB7CiAgICAgICAgICAgICJub2RlVHlwZSI6ICJmaWVsZExvb2t1cCIsCiAgICAgICAgICAgICJmaWVsZE5hbWUiOiAiY2l0eSIKICAgICAgICAgIH0sCiAgICAgICAgICB7CiAgICAgICAgICAgICJub2RlVHlwZSI6ICJsaXRlcmFsIiwKICAgICAgICAgICAgInZhbHVlIjogIk0lIgogICAgICAgICAgfQogICAgICAgIF0KICAgICAgfQogICAgXQogIH0KfQ==\' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的要求會傳回下列回應。

```json
{
  "format": "flat",
  "schema": {
    "columns": [
      {
        "name": "FIRSTNAME",
        "type": "string",
        "xdm": {
          "type": "string"
        }
      },
      {
        "name": "LASTNAME",
        "type": "string",
        "xdm": {
          "type": "string"
        }
      },
      {
        "name": "CITY",
        "type": "string",
        "xdm": {
          "type": "string"
        }
      },
      {
        "name": "AGE",
        "type": "string",
        "xdm": {
          "type": "string"
        }
      },
      {
        "name": "HEIGHT",
        "type": "string",
        "xdm": {
          "type": "string"
        }
      },
      {
        "name": "ISEMPLOYED",
        "type": "boolean",
        "xdm": {
          "type": "boolean"
        }
      },
      {
        "name": "POSTG",
        "type": "boolean",
        "xdm": {
          "type": "boolean"
        }
      },
      {
        "name": "LATITUDE",
        "type": "double",
        "xdm": {
          "type": "number"
        }
      },
      {
        "name": "LONGITUDE",
        "type": "double",
        "xdm": {
          "type": "number"
        }
      },
      {
        "name": "JOINEDDATE",
        "type": "string",
        "meta:xdmType": "date-time",
        "xdm": {
          "type": "string",
          "format": "date-time"
        }
      },
      {
        "name": "CREATEDAT",
        "type": "string",
        "meta:xdmType": "date-time",
        "xdm": {
          "type": "string",
          "format": "date-time"
        }
      },
      {
        "name": "CREATEDATTS",
        "type": "string",
        "meta:xdmType": "date-time",
        "xdm": {
          "type": "string",
          "format": "date-time"
        }
      }
    ]
  },
 "data": [
    {
        "CITY": "MZN",
        "LASTNAME": "Jain",
        "JOINEDDATE": "2022-06-22T00:00:00",
        "LONGITUDE": 1000.222,
        "CREATEDAT": "2022-06-22T17:19:33",
        "FIRSTNAME": "Shivam",
        "POSTG": true,
        "HEIGHT": "169",
        "CREATEDATTS": "2022-06-22T17:19:33",
        "ISEMPLOYED": true,
        "LATITUDE": 2000.89,
        "AGE": "25"
    },
    {
        "CITY": "MUM",
        "LASTNAME": "Kreet",
        "JOINEDDATE": "2022-09-07T00:00:00",
        "LONGITUDE": 10500.01,
        "CREATEDAT": "2022-09-07T17:19:33",
        "FIRSTNAME": "Rakul",
        "POSTG": true,
        "HEIGHT": "155",
        "CREATEDATTS": "2022-09-07T17:19:33",
        "ISEMPLOYED": false,
        "LATITUDE": 2500.89,
        "AGE": "42"
    },
    {
        "CITY": "MAN",
        "LASTNAME": "Lee",
        "JOINEDDATE": "2022-09-14T00:00:00",
        "LONGITUDE": 1000.222,
        "CREATEDAT": "2022-09-14T05:02:33",
        "FIRSTNAME": "Denzel",
        "POSTG": true,
        "HEIGHT": "185",
        "CREATEDATTS": "2022-09-14T05:02:33",
        "ISEMPLOYED": true,
        "LATITUDE": 123.89,
        "AGE": "16"
    }
  ]
}
```

### 為篩選的資料建立源連接

若要建立來源連線並擷取篩選的資料，請向 `/sourceConnections` 端點，同時提供篩選條件作為內文參數的一部分。

**API格式**

```http
POST /sourceConnections
```

**要求**

下列請求會建立來源連線，以從 `test1.fasTestTable` where `city` = `DDN`.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "BigQuery Source Connection",
      "description": "Source Connection for Filter test",
      "baseConnectionId": "89d1459e-3cd0-4069-acb3-68f240db4eeb",
      "data": {
        "format": "tabular"
      },
      "params": {
        "tableName": "test1.fasTestTable",
        "filters": {
          "type": "PQL",
          "format": "pql/json",
          "value": {
            "nodeType": "fnApply",
            "fnName": "=",
            "params": [
              {
                "nodeType": "fieldLookup",
                "fieldName": "city"
              },
              {
                "nodeType": "literal",
                "value": "DDN"
              }
            ]
          }
        }
      },
      "connectionSpec": {
        "id": "3c9b37f8-13a6-43d8-bad3-b863b941fedd",
        "version": "1.0"
      }
    }'
```

**回應**

成功的回應會傳回唯一識別碼(`id`)。

```json
{
    "id": "b7581b59-c603-4df1-a689-d23d7ac440f3",
    "etag": "\"ef05d265-0000-0200-0000-6019e0080000\""
}
```

## 附錄

本節提供篩選用不同負載的進一步範例。

### 奇異條件

您可以忽略初始 `fnApply` 僅需一個條件的情況。

```json
{
  "type": "PQL",
  "format": "pql/json",
  "value": {
    "nodeType": "fnApply",
    "fnName": "like",
    "params": [
      {
        "nodeType": "fieldLookup",
        "fieldName": "firstname"
      },
      {
        "nodeType": "literal",
        "value": "%s"
      }
    ]
  }
}
```

### 使用 `in` 運算子

如需運算子的範例，請參閱下方的裝載範例 `in`.

```json
{
  "type": "PQL",
  "format": "pql/json",
  "value": {
    "nodeType": "fnApply",
    "fnName": "and",
    "params": [
      {
        "nodeType": "fnApply",
        "fnName": "in",
        "params": [
          {
            "nodeType": "fieldLookup",
            "fieldName": "firstname"
          },
          {
            "nodeType": "literal",
            "value": [
              "Ramen",
              "John"
            ]
          }
        ]
      }
    ]
  }
}
```

### 使用 `isNull` 運算子

如需運算子的範例，請參閱下方的裝載範例 `isNull`.

```json
{
  "type": "PQL",
  "format": "pql/json",
  "value": {
    "nodeType": "fnApply",
    "fnName": "isNull",
    "params": [
      {
        "nodeType": "fieldLookup",
        "fieldName": "complaint_type"
      }
    ]
  }
}
```

### 使用 `NOT` 運算子

如需運算子的範例，請參閱下方的裝載範例 `NOT`.

```json
{
  "type": "PQL",
  "format": "pql/json",
  "value": {
    "nodeType": "fnApply",
    "fnName": "NOT",
    "params": [
      {
        "nodeType": "fnApply",
        "fnName": "isNull",
        "params": [
          {
            "nodeType": "fieldLookup",
            "fieldName": "complaint_type"
          }
        ]
      }
    ]
  }
}
```

### 含巢狀條件的範例

如需複雜巢狀條件的範例，請參閱下方的裝載範例。

```json
{
  "type": "PQL",
  "format": "pql/json",
  "value": {
    "nodeType": "fnApply",
    "fnName": "and",
    "params": [
      {
        "nodeType": "fnApply",
        "fnName": ">=",
        "params": [
          {
            "nodeType": "fieldLookup",
            "fieldName": "age"
          },
          {
            "nodeType": "literal",
            "value": 20
          }
        ]
      },
      {
        "nodeType": "fnApply",
        "fnName": "<=",
        "params": [
          {
            "nodeType": "fieldLookup",
            "fieldName": "age"
          },
          {
            "nodeType": "literal",
            "value": 30
          }
        ]
      },
      {
        "nodeType": "fnApply",
        "fnName": "or",
        "params": [
          {
            "nodeType": "fnApply",
            "fnName": "!=",
            "params": [
              {
                "nodeType": "fieldLookup",
                "fieldName": "city"
              },
              {
                "nodeType": "literal",
                "value": "PUD"
              }
            ]
          },
          {
            "nodeType": "fnApply",
            "fnName": "=",
            "params": [
              {
                "nodeType": "fieldLookup",
                "fieldName": "joinedDate"
              },
              {
                "nodeType": "literal",
                "value": "2020-04-22"
              }
            ]
          }
        ]
      }
    ]
  }
}
```
