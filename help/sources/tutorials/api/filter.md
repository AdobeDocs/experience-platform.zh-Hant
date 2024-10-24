---
title: 使用流量服務API篩選Source的列層級資料
description: 本教學課程涵蓋如何使用Flow Service API在來源層級篩選資料的步驟
exl-id: 224b454e-a079-4df3-a8b2-1bebfb37d11f
source-git-commit: e8e8914c41d7a083395b0bf53aaac8021fcf9e9a
workflow-type: tm+mt
source-wordcount: '1820'
ht-degree: 4%

---

# 使用[!DNL Flow Service] API篩選來源的資料列層級資料

>[!AVAILABILITY]
>
>篩選列層級資料的支援目前僅適用於下列來源：
>
>* [[!DNL Google BigQuery]](../../connectors/databases/bigquery.md)
>* [[!DNL Microsoft Dynamics]](../../connectors/crm/ms-dynamics.md)
>* [[!DNL Salesforce]](../../connectors/crm/salesforce.md)
>* [[!DNL Snowflake]](../../connectors/databases/snowflake.md)
>* [[!DNL Marketo Engage] 標準活動](../../connectors/adobe-applications/marketo/marketo.md)

閱讀本指南，瞭解如何使用[[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/)來篩選來源之資料列層級資料的步驟。

## 快速入門

本教學課程需要您實際瞭解下列Adobe Experience Platform元件：

* [來源](../../home.md)： [!DNL Experience Platform]允許從各種來源擷取資料，同時讓您能夠使用[!DNL Platform]服務來建構、加標籤以及增強傳入的資料。
* [沙箱](../../../sandboxes/home.md)： [!DNL Experience Platform]提供可將單一[!DNL Platform]執行個體分割成個別虛擬環境的虛擬沙箱，以利開發及改進數位體驗應用程式。

### 使用平台API

如需如何成功呼叫Platform API的詳細資訊，請參閱[Platform API快速入門](../../../landing/api-guide.md)的指南。

## 篩選來源資料 {#filter-source-data}

以下概述篩選來源之列層級資料時應採取的步驟。

### 擷取您的連線規格 {#retrieve-your-connection-specs}

篩選來源的列層級資料的第一步是擷取來源的連線規格，並判斷來源支援的運運算元和語言。

若要擷取指定來源的連線規格，請向[!DNL Flow Service] API的`/connectionSpecs`端點提出GET要求，並提供您來源的屬性名稱做為查詢引數的一部分。

**API格式**

```http
GET /connectionSpecs/{QUERY_PARAMS}
```

| 參數 | 說明 |
| --- | --- |
| `{QUERY_PARAMS}` | 篩選結果的選用查詢引數。 您可以套用`name`屬性並在搜尋中指定`"google-big-query"`來擷取[!DNL Google BigQuery]連線規格。 |

+++要求

下列要求會擷取[!DNL Google BigQuery]的連線規格。

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/connectionSpecs?property=name=="google-big-query"' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

+++回應

成功的回應會傳回狀態碼200和[!DNL Google BigQuery]的連線規格，包括其支援的查詢語言和邏輯運運算元的資訊。

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
| `attributes.filterAtSource.enabled` | 決定查詢的來源是否支援資料列層級資料的篩選。 |
| `attributes.filterAtSource.queryLanguage` | 決定查詢來源支援的查詢語言。 |
| `attributes.filterAtSource.logicalOperators` | 決定可用來篩選來源之資料列層級資料的邏輯運運算元。 |
| `attributes.filterAtSource.comparisonOperators` | 決定可用來篩選來源之列層級資料的比較運運算元。 請參閱下表，以取得比較運運算元的詳細資訊。 |
| `attributes.filterAtSource.columnNameEscapeChar` | 決定用於逸出欄的字元。 |
| `attributes.filterAtSource.valueEscapeChar` | 決定寫入SQL查詢時如何包圍值。 |

{style="table-layout:auto"}

+++

#### 比較運運算元 {#comparison-operators}

| 運算子 | 說明 |
| --- | --- |
| `==` | 依屬性是否等於提供的值篩選。 |
| `!=` | 依據屬性是否不等於提供的值來篩選。 |
| `<` | 依據屬性是否小於提供的值篩選。 |
| `>` | 依據屬性是否大於提供的值篩選。 |
| `<=` | 依據屬性是否小於或等於提供的值來篩選。 |
| `>=` | 依據屬性是否大於或等於提供的值來篩選。 |
| `like` | 在`WHERE`子句中使用來搜尋指定模式的篩選器。 |
| `in` | 依據屬性是否在指定範圍內進行篩選。 |

{style="table-layout:auto"}

### 指定內嵌的篩選條件 {#specify-filtering-conditions-for-ingestion}

在識別來源支援的邏輯運運算元和查詢語言後，您就可以使用Profile Query Language (PQL)來指定要套用至來源資料的篩選條件。

在下列範例中，條件僅會套用至與作為引數列出的節點型別所提供的值相等的選取資料。

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

### 預覽您的資料 {#preview-your-data}

您可以預覽資料，方法是向[!DNL Flow Service] API的`/explore`端點發出GET要求，同時提供`filters`作為查詢引數的一部分，並在[!DNL Base64]中指定PQL輸入條件。

**API格式**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=table&object={TABLE_PATH}&preview=true&filters={FILTERS}
```

| 參數 | 說明 |
| --- | --- |
| `{BASE_CONNECTION_ID}` | 來源的基本連線ID。 |
| `{TABLE_PATH}` | 您要檢查之資料表的路徑屬性。 |
| `{FILTERS}` | 您的PQL篩選條件以[!DNL Base64]編碼。 |

+++要求

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/connections/89d1459e-3cd0-4069-acb3-68f240db4eeb/explore?objectType=table&object=TESTFAS.FASTABLE&preview=true&filters=ewogICJ0eXBlIjogIlBRTCIsCiAgImZvcm1hdCI6ICJwcWwvanNvbiIsCiAgInZhbHVlIjogewogICAgIm5vZGVUeXBlIjogImZuQXBwbHkiLAogICAgImZuTmFtZSI6ICJhbmQiLAogICAgInBhcmFtcyI6IFsKICAgICAgewogICAgICAgICJub2RlVHlwZSI6ICJmbkFwcGx5IiwKICAgICAgICAiZm5OYW1lIjogImxpa2UiLAogICAgICAgICJwYXJhbXMiOiBbCiAgICAgICAgICB7CiAgICAgICAgICAgICJub2RlVHlwZSI6ICJmaWVsZExvb2t1cCIsCiAgICAgICAgICAgICJmaWVsZE5hbWUiOiAiY2l0eSIKICAgICAgICAgIH0sCiAgICAgICAgICB7CiAgICAgICAgICAgICJub2RlVHlwZSI6ICJsaXRlcmFsIiwKICAgICAgICAgICAgInZhbHVlIjogIk0lIgogICAgICAgICAgfQogICAgICAgIF0KICAgICAgfQogICAgXQogIH0KfQ==\' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

+++回應

成功的回應會傳回資料的內容和結構。

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

+++

### 建立篩選資料的來源連線

若要建立來源連線並擷取經過篩選的資料，請對`/sourceConnections`端點提出POST要求，並在要求內文引數中提供您的篩選條件。

**API格式**

```http
POST /sourceConnections
```

+++要求

下列要求會建立來源連線，以從`test1.fasTestTable`擷取資料，其中`city` = `DDN`。

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

+++

+++回應

成功的回應會傳回新建立的來源連線的唯一識別碼(`id`)。

```json
{
    "id": "b7581b59-c603-4df1-a689-d23d7ac440f3",
    "etag": "\"ef05d265-0000-0200-0000-6019e0080000\""
}
```

+++

## 篩選[!DNL Marketo Engage]的活動實體 {#filter-for-marketo}

使用[[!DNL Marketo Engage] 來源聯結器](../../connectors/adobe-applications/marketo/marketo.md)時，您可以使用列層級篩選來篩選活動實體。 目前，您只能篩選活動實體和標準活動型別。 自訂活動仍在[[!DNL Marketo] 欄位對應](../../connectors/adobe-applications/mapping/marketo.md)之下受管理。

### [!DNL Marketo]標準活動型別 {#marketo-standard-activity-types}

下表概述[!DNL Marketo]的標準活動型別。 使用此表格作為篩選條件的參考。

| 活動型別ID | 活動型別名稱 |
| --- | --- |
| 1 | 造訪網頁 |
| 2 | 填寫表格 |
| 3 | 按一下連結 |
| 6 | 傳送電子郵件 |
| 7 | 電子郵件已發送 |
| 8 | 電子郵件已退回 |
| 9 | 取消訂閱電子郵件 |
| 10 | 開啟電子郵件 |
| 11 | 按一下電子郵件 |
| 12 | 新的潛在客戶 |
| 21 | 轉換潛在客戶 |
| 22 | 變更分數 |
| 24 | 新增至清單 |
| 25 | 從清單移除 |
| 27 | 電子郵件已退回 (軟彈) |
| 32 | 合併潛在客戶 |
| 34 | 新增至商機 |
| 35 | 從機會移除 |
| 36 | 更新機會 |
| 46 | 有趣的時刻 |
| 101 | 變更收入階段 |
| 104 | 進度中的變更狀態 |
| 110 | 調用 Webhook |
| 113 | 新增至Nurture |
| 114 | 變更培養軌跡 |
| 115 | 變更Nurture步調 |

{style="table-layout:auto"}

使用[!DNL Marketo]來源聯結器時，請依照下列步驟篩選標準活動實體。

### 建立草稿資料流

首先，建立[[!DNL Marketo] 資料流](../ui/create/adobe-applications/marketo.md)並將其儲存為草稿。 請參閱下列檔案，以取得有關如何建立草稿資料流的詳細步驟：

* [使用UI將資料流儲存為草稿](../ui/draft.md)
* [使用API將資料流儲存為草稿](../api/draft.md)

### 擷取您的資料流ID

草擬資料流後，您必須擷取其對應的ID。

在UI中，導覽至來源目錄，然後從頂端標題中選取&#x200B;**[!UICONTROL 資料流程]**。 使用狀態列來識別所有以草稿模式儲存的資料流，然後選取資料流的名稱。 接下來，使用右側的&#x200B;**[!UICONTROL 屬性]**&#x200B;面板來尋找您的資料流ID。

### 擷取您的資料流詳細資料

接下來，您必須擷取資料流詳細資料，尤其是與資料流相關聯的來源連線ID。 若要擷取您的資料流詳細資料，請向`/flows`端點提出GET要求，並提供您的資料流ID作為路徑引數。

**API格式**

```http
GET /flows/{FLOW_ID}
```

| 參數 | 說明 |
| --- | --- |
| `{FLOW_ID}` | 您要擷取的資料流ID。 |

+++要求

下列要求會擷取資料流ID的資訊： `a7e88a01-40f9-4ebf-80b2-0fc838ff82ef`。

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/flows/a7e88a01-40f9-4ebf-80b2-0fc838ff82ef' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

+++回應

成功的回應會傳回資料流詳細資料，包括其對應來源和目標連線的資訊。 您必須記下來源和目標連線ID，因為稍後需要這些值，才能發佈資料流。

```json {line-numbers="true" start-line="1" highlight="23, 26"}
{
    "items": [
        {
            "id": "a7e88a01-40f9-4ebf-80b2-0fc838ff82ef",
            "createdAt": 1728592929650,
            "updatedAt": 1728597187444,
            "createdBy": "acme@AdobeID",
            "updatedBy": "acme@AdobeID",
            "createdClient": "exc_app",
            "updatedClient": "acme",
            "sandboxId": "7f3419ce-53e2-476b-b419-ce53e2376b02",
            "sandboxName": "prod",
            "imsOrgId": "acme@AdobeOrg",
            "name": "Marketo Engage Standard Activities ACME",
            "description": "",
            "flowSpec": {
                "id": "15f8402c-ba66-4626-b54c-9f8e54244d61",
                "version": "1.0"
            },
            "state": "enabled",
            "version": "\"600290fc-0000-0200-0000-67084cc30000\"",
            "etag": "\"600290fc-0000-0200-0000-67084cc30000\"",
            "sourceConnectionIds": [
                "56f7eb3a-b544-4eaa-b167-ef1711044c7a"
            ],
            "targetConnectionIds": [
                "7e53e6e8-b432-4134-bb29-21fc6e8532e5"
            ],
            "inheritedAttributes": {
                "properties": {
                    "isSourceFlow": true
                },
                "sourceConnections": [
                    {
                        "id": "56f7eb3a-b544-4eaa-b167-ef1711044c7a",
                        "connectionSpec": {
                            "id": "bf1f4218-73ce-4ff0-b744-48d78ffae2e4",
                            "version": "1.0"
                        },
                        "baseConnection": {
                            "id": "0137118b-373a-4c4e-847c-13a0abf73b33",
                            "connectionSpec": {
                                "id": "bf1f4218-73ce-4ff0-b744-48d78ffae2e4",
                                "version": "1.0"
                            }
                        }
                    }
                ],
                "targetConnections": [
                    {
                        "id": "7e53e6e8-b432-4134-bb29-21fc6e8532e5",
                        "connectionSpec": {
                            "id": "c604ff05-7f1a-43c0-8e18-33bf874cb11c",
                            "version": "1.0"
                        }
                    }
                ]
            },
            "options": {
                "isSampleDataflow": false,
                "errorDiagnosticsEnabled": true
            },
            "transformations": [
                {
                    "name": "Mapping",
                    "params": {
                        "mappingVersion": 0,
                        "mappingId": "f6447514ef95482889fac1818972e285"
                    }
                }
            ],
            "runs": "/runs?property=flowId==a7e88a01-40f9-4ebf-80b2-0fc838ff82ef",
            "lastOperation": {
                "started": 1728592929650,
                "updated": 0,
                "operation": "create"
            },
            "lastRunDetails": {
                "id": "2d7863d5-ca4d-4313-ac52-2603eaf2cdbe",
                "state": "success",
                "startedAtUTC": 1728594713537,
                "completedAtUTC": 1728597183080
            },
            "labels": [],
            "recordTypes": [
                {
                    "type": "experienceevent",
                    "extensions": {}
                }
            ]
        }
    ]
}
```

+++

### 擷取您的來源連線詳細資料

接下來，使用您的來源連線ID並向`/sourceConnections`端點發出GET要求，以擷取您的來源連線詳細資料。

**API格式**

```http
GET /sourceConnections/{SOURCE_CONNECTION_ID}
```

| 參數 | 說明 |
| --- | --- |
| `{SOURCE_CONNECTION_ID}` | 您要擷取之來源連線的ID。 |

+++要求

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/sourceConnections/56f7eb3a-b544-4eaa-b167-ef1711044c7a' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

+++回應

成功的回應會傳回來源連線的詳細資料。 記下版本，因為您需要在下一個步驟中使用此值來更新來源連線。

```json {line-numbers="true" start-line="1" highlight="30"}
{
    "items": [
        {
            "id": "b85b895f-a289-42e9-8fe1-ae448ccc7e53",
            "createdAt": 1729634331185,
            "updatedAt": 1729634331185,
            "createdBy": "acme@AdobeID",
            "updatedBy": "acme@AdobeID",
            "createdClient": "exc_app",
            "updatedClient": "acme",
            "sandboxId": "7f3419ce-53e2-476b-b419-ce53e2376b02",
            "sandboxName": "prod",
            "imsOrgId": "acme@AdobeOrg",
            "name": "New Source Connection - 2024-10-23T03:28:50+05:30",
            "description": "Source connection created from the workflow",
            "baseConnectionId": "fd9f7455-1e23-4831-9283-7717e20bee40",
            "state": "draft",
            "data": {
                "format": "tabular",
                "schema": null,
                "properties": null
            },
            "connectionSpec": {
                "id": "2d31dfd1-df1a-456b-948f-226e040ba102",
                "version": "1.0"
            },
            "params": {
                "columns": [],
                "tableName": "Activity"
            },
            "version": "\"210068a6-0000-0200-0000-6718201b0000\"",
            "etag": "\"210068a6-0000-0200-0000-6718201b0000\"",
            "inheritedAttributes": {
                "baseConnection": {
                    "id": "fd9f7455-1e23-4831-9283-7717e20bee40",
                    "connectionSpec": {
                        "id": "2d31dfd1-df1a-456b-948f-226e040ba102",
                        "version": "1.0"
                    }
                }
            },
            "lastOperation": {
                "started": 1729634331185,
                "updated": 0,
                "operation": "draft_create"
            }
        }
    ]
}
```

+++

### 使用篩選條件更新您的來源連線

現在您已擁有來源連線ID及其對應版本，現在可以使用指定標準活動型別的篩選條件來發出PATCH請求。

若要更新您的來源連線，請對`/sourceConnections`端點提出PATCH要求，並提供您的來源連線ID作為查詢引數。 此外，您必須提供`If-Match`標頭引數，以及您來源連線的對應版本。

>[!TIP]
>
>發出PATCH要求時需要`If-Match`標頭。 此標題的值是您要更新之資料流的唯一版本/etag。 每次成功更新資料流時，版本/etag值都會更新。

**API格式**

```http
PATCH /sourceConnections/{SOURCE_CONNECTION_ID}
```

| 參數 | 說明 |
| --- | --- |
| `{SOURCE_CONNECTION_ID}` | 您要更新的來源連線識別碼 |

+++要求

```shell
curl -X PATCH \
  'https://platform.adobe.io/data/foundation/flowservice/sourceConnections/56f7eb3a-b544-4eaa-b167-ef1711044c7a' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'If-Match: {VERSION_HERE}'
  -d '
      {
        "op": "add",
        "path": "/params/filters",
        "value": {
            "type": "PQL",
            "format": "pql/json",
            "value": {
                "nodeType": "fnApply",
                "fnName": "in",
                "params": [
                    {
                        "nodeType": "fieldLookup",
                        "fieldName": "activityType"
                    },
                    {
                        "nodeType": "literal",
                        "value": [
                            "Change Status in Progression",
                            "Fill Out Form"
                        ]
                    }
                ]
            }
        }
    }'
```

+++

+++回應

成功的回應會傳回來源連線ID和etag （版本）。

```json
{
    "id": "56f7eb3a-b544-4eaa-b167-ef1711044c7a",
    "etag": "\"210068a6-0000-0200-0000-6718201b0000\""
}
```

+++

### Publish您的來源連線

您的來源連線已隨著篩選條件而更新，您現在可以從草稿狀態繼續並發佈您的來源連線。 若要這麼做，請向`/sourceConnections`端點提出POST要求，並提供草稿來源連線的識別碼，以及發佈的動作操作。

**API格式**

```http
POST /sourceConnections/{SOURCE_CONNECTION_ID}/action?op=publish
```

| 參數 | 說明 |
| --- | --- |
| `{SOURCE_CONNECTION_ID}` | 您要發佈的來源連線ID。 |
| `op` | 更新查詢來源連線狀態的動作操作。 若要發佈草稿來源連線，請將`op`設為`publish`。 |

+++要求

下列要求會發佈草擬的來源連線。

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/sourceConnections/56f7eb3a-b544-4eaa-b167-ef1711044c7a/action?op=publish' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

+++

+++回應

成功的回應會傳回來源連線ID和etag （版本）。

```json
{
    "id": "56f7eb3a-b544-4eaa-b167-ef1711044c7a",
    "etag": "\"9f007f7b-0000-0200-0000-670ef1150000\""
}
```

+++

### Publish您的目標連線

與上一個步驟類似，您也必須發佈目標連線，才能繼續並發佈草稿資料流。 向`/targetConnections`端點發出POST要求，並提供您要發佈的草稿目標連線識別碼，以及發佈的動作操作。

**API格式**

```http
POST /targetConnections/{TARGET_CONNECTION_ID}/action?op=publish
```

| 參數 | 說明 |
| --- | --- |
| `{TARGET_CONNECTION_ID}` | 您要發佈的目標連線ID。 |
| `op` | 更新查詢之目標連線狀態的動作操作。 若要發佈草稿目標連線，請將`op`設為`publish`。 |

+++要求

下列要求發佈識別碼為`7e53e6e8-b432-4134-bb29-21fc6e8532e5`的目標連線。

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections/7e53e6e8-b432-4134-bb29-21fc6e8532e5/action?op=publish' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

+++

+++回應

成功的回應會傳回已發佈目標連線的ID和對應標籤。

```json
{
    "id": "7e53e6e8-b432-4134-bb29-21fc6e8532e5",
    "etag": "\"8e000533-0000-0200-0000-5f3c40fd0000\""
}
```

+++


### Publish您的資料流

您的來源和目標連線均已發佈後，您現在可以繼續進行最後步驟並發佈資料流。 若要發佈您的資料流，請向`/flows`端點提出POST要求，並提供您的資料流ID和用於發佈的動作操作。

**API格式**

```http
POST /flows/{FLOW_ID}/action?op=publish
```

| 參數 | 說明 |
| --- | --- |
| `{FLOW_ID}` | 您要發佈的資料流ID。 |
| `op` | 更新查詢資料流狀態的動作操作。 若要發佈草稿資料流，請將`op`設為`publish`。 |

+++要求

以下請求會發佈您的草稿資料流。

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/flows/a7e88a01-40f9-4ebf-80b2-0fc838ff82ef/action?op=publish' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

+++

+++回應

成功的回應會傳回您的資料流的ID和對應的`etag`。

```json
{
  "id": "a7e88a01-40f9-4ebf-80b2-0fc838ff82ef",
  "etag": "\"4b0354b7-0000-0200-0000-6716ce1f0000\""
}
```

+++

您可以使用Experience PlatformUI來確認草稿資料流已發佈。 導覽至來源目錄中的資料流頁面，並參考您的資料流的&#x200B;**[!UICONTROL 狀態]**。 如果成功，狀態現在應該設定為&#x200B;**已啟用**。

>[!TIP]
>
>* 已啟用篩選的資料流將只會回填一次。 您在篩選條件中所做的任何變更（無論是新增或移除）都只能對增量資料生效。
>* 如果您需要擷取任何新活動型別的歷史資料，建議您建立新的資料流，並在篩選條件中使用適當的活動型別定義篩選條件。
>* 您無法篩選自訂活動型別。
>* 您無法預覽篩選的資料。

## 附錄

本節提供不同裝載的更多範例以供篩選。

### 奇異條件

對於只需要一個條件的案例，您可以省略初始`fnApply`。

+++選取以檢視範例

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

+++

### 使用`in`運運算元

如需運運算元`in`的範例，請參閱下列裝載範例。

+++選取以檢視範例

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

+++

### 使用`isNull`運運算元

+++選取以檢視範例

如需運運算元`isNull`的範例，請參閱下列裝載範例。

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

+++

### 使用`NOT`運運算元

如需運運算元`NOT`的範例，請參閱下列裝載範例。


+++選取以檢視範例

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

+++

### 巢狀條件的範例

如需複雜巢狀條件的範例，請參閱以下的裝載範例。

+++選取以檢視範例

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

+++