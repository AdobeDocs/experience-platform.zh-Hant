---
title: 使用流量服務API更新串流SDK的流量規格
description: 以下檔案提供如何使用Flow Service API for Self-Serve Sources (Streaming SDK)擷取和更新流程規格的步驟。
exl-id: cc9dab7a-08fa-4c6c-bbac-cb658a6376fb
badge: Beta
source-git-commit: 256857103b4037b2cd7b5b52d6c5385121af5a9f
workflow-type: tm+mt
source-wordcount: '423'
ht-degree: 2%

---

# 使用[!DNL Flow Service] API更新流程規格

>[!NOTE]
>
>自助來源串流SDK為測試版。 如需使用Beta版標籤來源的相關資訊，請參閱[來源概觀](../../home.md#terms-and-conditions)。

產生新的連線規格ID後，您必須將此ID新增至流程規格，才能建立資料流。

流程規格包含定義流程的資訊，包括它支援的來源與目標連線ID、需要套用至資料的轉換規格，以及產生流程所需的排程引數。 您可以使用`/flowSpecs`端點來編輯流程規格。

以下檔案提供如何使用[!DNL Flow Service] API for Self-Serve Sources (Streaming SDK)擷取和更新流程規格的步驟。

## 快速入門

繼續之前，請先檢閱[快速入門手冊](./getting-started.md)，以取得相關檔案的連結、閱讀本檔案中範例API呼叫的手冊，以及有關成功呼叫任何Experience PlatformAPI所需必要標題的重要資訊。

## 查詢流程規格 {#lookup}

以`generic-streaming`範本建立的來源都使用`GenericStreamingAEP`流程規格。 您可以對`/flowSpecs/`端點發出GET要求，並提供`e77fde5a-22a8-11ed-861d-0242ac120002`的`flowSpec.id`，以擷取此流量規格。

**API格式**

```http
GET /flowSpecs/e77fde5a-22a8-11ed-861d-0242ac120002
```

**要求**

下列要求會擷取`e77fde5a-22a8-11ed-861d-0242ac120002`流程規格。

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/flowSpecs/e77fde5a-22a8-11ed-861d-0242ac120002' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' 
```

**回應**

成功的回應會傳回查詢流程規格的詳細資料。

```json
{
  "items": [
    {
      "id": "e77fde5a-22a8-11ed-861d-0242ac120002",
      "name": "GenericStreamingAEP",
      "providerId": "521eee4d-8cbe-4906-bb48-fb6bd4450033",
      "version": "1.0",
      "sourceConnectionSpecIds": [
        "e77fd9d2-22a8-11ed-861d-0242ac120002"
      ],
      "targetConnectionSpecIds": [
        "c604ff05-7f1a-43c0-8e18-33bf874cb11c"
      ],
      "optionSpec": {
        "name": "OptionSpec",
        "spec": {
          "$schema": "http://json-schema.org/draft-07/schema#",
          "type": "object",
          "properties": {
            "errorDiagnosticsEnabled": {
              "title": "Error diagnostics.",
              "description": "Flag to enable detailed and sample error diagnostics summary.",
              "type": "boolean",
              "default": false
            },
            "partialIngestionPercent": {
              "title": "Partial ingestion threshold.",
              "description": "Percentage which defines the threshold of errors allowed before the run is marked as failed.",
              "type": "number",
              "exclusiveMinimum": 0
            },
            "inletUrl": {
              "title": "Inlet Url.",
              "description": "Inlet Url which defines the streaming endpoint.",
              "type": "string"
            }
          }
        }
      },
      "transformationSpecs": [
        {
          "name": "Mapping",
          "spec": {
            "$schema": "http://json-schema.org/draft-07/schema#",
            "type": "object",
            "description": "defines various params required for different mapping from source to target",
            "properties": {
              "mappingId": {
                "type": "string"
              },
              "mappingVersion": {
                "type": "string"
              }
            }
          }
        }
      ],
      "attributes": {
        "isSourceFlow": true,
        "flacValidationSupported": true,
        "frequency": "streaming",
        "uiAttributes": {
          "apiFeatures": {
            "updateSupported": true,
            "flowRunsSupported": true
          }
        }
      },
      "permissionsInfo": {
        "manage": [
          {
            "@type": "lowLevel",
            "name": "StreamingSource",
            "permissions": [
              "write"
            ]
          }
        ],
        "view": [
          {
            "@type": "lowLevel",
            "name": "StreamingSource",
            "permissions": [
              "read"
            ]
          }
        ]
      }
    }
  ]
}
```

## 更新流程規格 {#update}

您可以透過PUT作業更新流程規格的欄位。 透過PUT請求更新流量規格時，本文必須包含在POST請求中建立新流量規格時所需的所有欄位。

>[!IMPORTANT]
>
>當您為新來源建立連線規格時，必須將其規格ID新增至與您的來源對應的流程規格`sourceConnectionSpecIds`陣列。 這可確保現有流程規格支援您的新來源，從而允許您使用新來源完成資料流程建立流程。

**API格式**

```http
PUT /flowSpecs/e77fde5a-22a8-11ed-861d-0242ac120002
```

**要求**

下列要求會更新`e77fde5a-22a8-11ed-861d-0242ac120002`的流程規格，以包含連線規格識別碼`bdb5b792-451b-42de-acf8-15f3195821de`。

```shell
PUT -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/connectionSpecs/e77fde5a-22a8-11ed-861d-0242ac120002' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
  -d '{
      "id": "e77fde5a-22a8-11ed-861d-0242ac120002",
      "name": "GenericStreamingAEP",
      "providerId": "521eee4d-8cbe-4906-bb48-fb6bd4450033",
      "version": "1.0",
      "sourceConnectionSpecIds": [
          "e77fd9d2-22a8-11ed-861d-0242ac120002",
          "bdb5b792-451b-42de-acf8-15f3195821de"
      ],
      "targetConnectionSpecIds": [
          "c604ff05-7f1a-43c0-8e18-33bf874cb11c"
      ],
      "optionSpec": {
          "name": "OptionSpec",
          "spec": {
              "$schema": "http://json-schema.org/draft-07/schema#",
              "type": "object",
              "properties": {
                  "errorDiagnosticsEnabled": {
                      "title": "Error diagnostics.",
                      "description": "Flag to enable detailed and sample error diagnostics summary.",
                      "type": "boolean",
                      "default": false
                  },
                  "partialIngestionPercent": {
                      "title": "Partial ingestion threshold.",
                      "description": "Percentage which defines the threshold of errors allowed before the run is marked as failed.",
                      "type": "number",
                      "exclusiveMinimum": 0
                  },
                  "inletUrl": {
                      "title": "Inlet Url.",
                      "description": "Inlet Url which defines the streaming endpoint.",
                      "type": "string"
                  }
              }
          }
      },
      "transformationSpecs": [
          {
              "name": "Mapping",
              "spec": {
                  "$schema": "http://json-schema.org/draft-07/schema#",
                  "type": "object",
                  "description": "defines various params required for different mapping from source to target",
                  "properties": {
                      "mappingId": {
                          "type": "string"
                      },
                      "mappingVersion": {
                          "type": "string"
                      }
                  }
              }
          }
      ],
      "attributes": {
          "isSourceFlow": true,
          "flacValidationSupported": true,
          "frequency": "streaming",
          "uiAttributes": {
              "apiFeatures": {
                  "updateSupported": true,
                  "flowRunsSupported": true
              }
          }
      },
      "permissionsInfo": {
          "view": [
              {
                  "@type": "lowLevel",
                  "name": "StreamingSource",
                  "permissions": [
                      "read"
                  ]
              }
          ],
          "manage": [
              {
                  "@type": "lowLevel",
                  "name": "StreamingSource",
                  "permissions": [
                      "write"
                  ]
              }
          ]
      }
  }'
```

**回應**

成功的回應會傳回查詢流程規格的詳細資料，包括其更新的`sourceConnectionSpecIds`清單。

```json
{
    "id": "e77fde5a-22a8-11ed-861d-0242ac120002",
    "updatedAt": 1633393222979,
    "updatedBy": "1633393222979",
    "updatedClient": "{UPDATED_CLIENT}",
    "sandboxId": "{SANDBOX_ID}",
    "sandboxName": "{SANDBOX_NAME}",
    "imsOrgId": "{ORG_ID}",
    "name": "GenericStreamingAEP",
    "providerId": "521eee4d-8cbe-4906-bb48-fb6bd4450033",
    "version": "1.0",
      "sourceConnectionSpecIds": [
        "e77fd9d2-22a8-11ed-861d-0242ac120002"
      ],
      "targetConnectionSpecIds": [
        "c604ff05-7f1a-43c0-8e18-33bf874cb11c"
      ],
      "optionSpec": {
        "name": "OptionSpec",
        "spec": {
          "$schema": "http://json-schema.org/draft-07/schema#",
          "type": "object",
          "properties": {
            "errorDiagnosticsEnabled": {
              "title": "Error diagnostics.",
              "description": "Flag to enable detailed and sample error diagnostics summary.",
              "type": "boolean",
              "default": false
            },
            "partialIngestionPercent": {
              "title": "Partial ingestion threshold.",
              "description": "Percentage which defines the threshold of errors allowed before the run is marked as failed.",
              "type": "number",
              "exclusiveMinimum": 0
            },
            "inletUrl": {
              "title": "Inlet Url.",
              "description": "Inlet Url which defines the streaming endpoint.",
              "type": "string"
            }
          }
        }
      },
      "transformationSpecs": [
        {
          "name": "Mapping",
          "spec": {
            "$schema": "http://json-schema.org/draft-07/schema#",
            "type": "object",
            "description": "defines various params required for different mapping from source to target",
            "properties": {
              "mappingId": {
                "type": "string"
              },
              "mappingVersion": {
                "type": "string"
              }
            }
          }
        }
      ],
      "attributes": {
        "isSourceFlow": true,
        "flacValidationSupported": true,
        "frequency": "streaming",
        "uiAttributes": {
          "apiFeatures": {
            "updateSupported": true,
            "flowRunsSupported": true
          }
        }
      },
      "permissionsInfo": {
        "manage": [
          {
            "@type": "lowLevel",
            "name": "StreamingSource",
            "permissions": [
              "write"
            ]
          }
        ],
        "view": [
          {
            "@type": "lowLevel",
            "name": "StreamingSource",
            "permissions": [
              "read"
            ]
          }
        ]
      }
    }
  ]
}
```

## 後續步驟

將新的連線規格新增至適當的流量規格後，您現在可以繼續測試並提交新的來源。 如需詳細資訊，請參閱[測試和提交新來源](./submit.md)的指南。
