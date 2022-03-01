---
keywords: Experience Platform；首頁；熱門主題；雲儲存資料
solution: Experience Platform
title: 使用流服務API為雲儲存源建立資料流
topic-legacy: overview
type: Tutorial
description: 本教程介紹了使用源連接器和API從第三方雲儲存中檢索資料並將其引入平台的步驟。
exl-id: 95373c25-24f6-4905-ae6c-5000bf493e6f
source-git-commit: 67e6de74ea8f2f4868a39ec1907ee1cac335c9f0
workflow-type: tm+mt
source-wordcount: '1575'
ht-degree: 1%

---

# 使用 [!DNL Flow Service] API

本教程介紹從雲儲存源檢索資料並將資料帶入平台的步驟 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/)。

>[!NOTE]
>
>為了建立資料流，您必須已具有與平台上以下任何雲儲存源的有效基本連接ID:<ul><li>[[!DNL Amazon S3]](../create/cloud-storage/s3.md)</li><li>[[!DNL Apache HDFS]](../create/cloud-storage/hdfs.md)</li><li>[[!DNL Azure Blob]](../create/cloud-storage/blob.md)</li><li>[[!DNL Azure Data Lake Storage Gen2]](../create/cloud-storage/adls-gen2.md)</li><li>[[!DNL Azure File Storage]](../create/cloud-storage/azure-file-storage.md)</li><li>[[!DNL FTP]](../create/cloud-storage/ftp.md)</li><li>[[!DNL Google Cloud Storage]](../create/cloud-storage/google.md)</li><li>[[!DNL Oracle Object Storage]](../create/cloud-storage/oracle-object-storage.md)</li><li>[[!DNL SFTP]](../create/cloud-storage/sftp.md)</li></ul>

## 快速入門

本教程要求您對以下Adobe Experience Platform元件有一定的瞭解：

- [[!DNL Experience Data Model (XDM) System]](../../../../xdm/home.md):Experience Platform組織客戶體驗資料的標準化框架。
   - [架構組合的基礎](../../../../xdm/schema/composition.md):瞭解XDM架構的基本構建基塊，包括架構組成中的關鍵原則和最佳做法。
   - [架構註冊表開發人員指南](../../../../xdm/api/getting-started.md):包括成功執行對架構註冊表API的調用所需要瞭解的重要資訊。 這包括您 `{TENANT_ID}`、「容器」的概念和發出請求所需的標頭（特別要注意「接受」標頭及其可能值）。
- [[!DNL Catalog Service]](../../../../catalog/home.md):目錄是記錄Experience Platform中資料位置和沿襲的系統。
- [[!DNL Batch ingestion]](../../../../ingestion/batch-ingestion/overview.md):批處理接收API允許您將資料作為批處理檔案接收到Experience Platform中。
- [沙箱](../../../../sandboxes/home.md):Experience Platform提供虛擬沙箱，將單個平台實例分區為獨立的虛擬環境，以幫助開發和發展數字型驗應用程式。

### 使用平台API

有關如何成功調用平台API的資訊，請參見上的指南 [平台API入門](../../../../landing/api-guide.md)。

## 建立源連接 {#source}

您可以通過向POST請求建立源連接 [!DNL Flow Service] API。 源連接由連接ID、源資料檔案的路徑和連接規範ID組成。

要建立源連接，還必須為資料格式屬性定義枚舉值。

對基於檔案的源使用以下枚舉值：

| 資料格式 | 枚舉值 |
| ----------- | ---------- |
| 分隔 | `delimited` |
| JSON | `json` |
| 鑲木 | `parquet` |

對於所有基於表的源，將值設定為 `tabular`。

- [使用自定義分隔檔案建立源連接](#using-custom-delimited-files)
- [使用壓縮檔案建立源連接](#using-compressed-files)

**API格式**

```http
POST /sourceConnections
```

### 使用自定義分隔檔案建立源連接 {#using-custom-delimited-files}

**要求**

通過指定 `columnDelimiter` 作為財產。 任何單個字元值都是允許的列分隔符。 如果未提供，則逗號 `(,)` 值。

以下示例請求使用以制表符分隔的值為分隔的檔案類型建立源連接。

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Cloud storage source connection for delimited files",
        "description": "Cloud storage source connector",
        "baseConnectionId": "9e2541a0-b143-4d23-a541-a0b143dd2301",
        "data": {
            "format": "delimited",
            "columnDelimiter": "\t"
        },
        "params": {
            "path": "/ingestion-demos/leads/tsv_data/*.tsv",
            "recursive": "true"
        },
        "connectionSpec": {
            "id": "4c10e202-c428-4796-9208-5f1f5732b1cf",
            "version": "1.0"
        }
    }'
```

| 屬性 | 說明 |
| --- | --- |
| `baseConnectionId` | 您正在訪問的第三方雲儲存系統的唯一連接ID。 |
| `data.format` | 定義資料格式屬性的枚舉值。 |
| `data.columnDelimiter` | 可以使用任何單個字元列分隔符來收集平面檔案。 僅當插入CSV或TSV檔案時，才需要此屬性。 |
| `params.path` | 要訪問的源檔案的路徑。 |
| `connectionSpec.id` | 與特定第三方雲儲存系統關聯的連接規範ID。 查看 [附錄](#appendix) 連接規範ID清單。 |

**回應**

成功的響應返回唯一標識符(`id`)。 在後續步驟中建立資料流時需要此ID。

```json
{
    "id": "26b53912-1005-49f0-b539-12100559f0e2",
    "etag": "\"11004d97-0000-0200-0000-5f3c3b140000\""
}
```

### 使用壓縮檔案建立源連接 {#using-compressed-files}

**要求**

還可以通過指定壓縮的JSON或分隔的檔案 `compressionType` 作為財產。 支援的壓縮檔案類型清單包括：

- `bzip2`
- `gzip`
- `deflate`
- `zipDeflate`
- `tarGzip`
- `tar`

下面的示例請求使用 `gzip` 檔案類型。

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Cloud storage source connection for compressed files",
        "description": "Cloud storage source connection for compressed files",
        "baseConnectionId": "9e2541a0-b143-4d23-a541-a0b143dd2301",
        "data": {
            "format": "delimited",
            "properties": {
                "compressionType": "gzip"
            }
        },
        "params": {
            "path": "/compressed/files.gzip"
        },
        "connectionSpec": {
            "id": "4c10e202-c428-4796-9208-5f1f5732b1cf",
            "version": "1.0"
        }
     }'
```

| 屬性 | 說明 |
| --- | --- |
| `data.properties.compressionType` | 確定用於接收的壓縮檔案類型。 僅當插入壓縮的JSON或分隔檔案時，才需要此屬性。 |

**回應**

成功的響應返回唯一標識符(`id`)。 在後續步驟中建立資料流時需要此ID。

```json
{
    "id": "26b53912-1005-49f0-b539-12100559f0e2",
    "etag": "\"11004d97-0000-0200-0000-5f3c3b140000\""
}
```

## 建立目標XDM架構 {#target-schema}

為了在平台中使用源資料，必須建立目標架構以根據您的需要來構造源資料。 然後使用目標模式建立包含源資料的平台資料集。

通過執行對目標XDM的POST請求，可以建立目標XDM模式 [架構註冊表API](https://www.adobe.io/experience-platform-apis/references/schema-registry/)。

有關如何建立目標XDM架構的詳細步驟，請參見上的教程 [使用API建立架構](../../../../xdm/api/schemas.md)。

## 建立目標資料集 {#target-dataset}

通過對目標資料集執行POST請求，可以建立目標資料集 [目錄服務API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml)，提供負載內目標架構的ID。

有關如何建立目標資料集的詳細步驟，請參見上的教程 [使用API建立資料集](../../../../catalog/api/create-dataset.md)。

## 建立目標連接 {#target-connection}

目標連接表示到所接收資料所在目的地的連接。 要建立目標連接，必須提供與資料湖關聯的固定連接規範ID。 此連接規範ID為： `c604ff05-7f1a-43c0-8e18-33bf874cb11c`。

您現在將唯一標識符作為目標模式、目標資料集和到資料湖的連接規範ID。 使用這些標識符，可以使用 [!DNL Flow Service] API，用於指定將包含入站源資料的資料集。

**API格式**

```http
POST /targetConnections
```

**要求**

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/targetConnections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Target Connection for a Cloud Storage connector",
        "description": "Target Connection for a Cloud Storage connector",
        "data": {
            "schema": {
                "id": "https://ns.adobe.com/{TENANT_ID}/schemas/995dabbea86d58e346ff91bd8aa741a9f36f29b1019138d4",
                "version": "application/vnd.adobe.xed-full+json;version=1"
            }
        },
        "params": {
            "dataSetId": "5f3c3cedb2805c194ff0b69a"
        },
            "connectionSpec": {
            "id": "c604ff05-7f1a-43c0-8e18-33bf874cb11c",
            "version": "1.0"
        }
    }'
```

| 屬性 | 說明 |
| -------- | ----------- |
| `data.schema.id` | 的 `$id` 目標XDM架構。 |
| `data.schema.version` | 架構的版本。 必須設定此值 `application/vnd.adobe.xed-full+json;version=1`，返回架構的最新次版本。 |
| `params.dataSetId` | 目標資料集的ID。 |
| `connectionSpec.id` | 到資料湖的固定連接規範ID。 此ID為： `c604ff05-7f1a-43c0-8e18-33bf874cb11c`。 |

**回應**

成功的響應返回新目標連接的唯一標識符(`id`)。 後續步驟中需要此ID。

```json
{
    "id": "dbc5c132-bc2a-4625-85c1-32bc2a262558",
    "etag": "\"8e000533-0000-0200-0000-5f3c40fd0000\""
}
```

## 建立映射 {#mapping}

為了將源資料攝取到目標資料集中，必須首先將其映射到目標資料集所遵循的目標模式。

要建立映射集，請向 `mappingSets` 端點 [[!DNL Data Prep] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/data-prep.yaml) 提供目標XDM架構時 `$id` 以及要建立的映射集的詳細資訊。

>[!TIP]
>
>可以使用雲儲存源連接器在JSON檔案中映射複雜資料類型（如陣列）。

**API格式**

```http
POST /conversion/mappingSets
```

**要求**

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/conversion/mappingSets' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "version": 0,
        "xdmSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/995dabbea86d58e346ff91bd8aa741a9f36f29b1019138d4",
        "xdmVersion": "1.0",
        "id": null,
        "mappings": [
            {
                "destinationXdmPath": "_id",
                "sourceAttribute": "Id",
                "identity": false,
                "identityGroup": null,
                "namespaceCode": null,
                "version": 0
            },
            {
                "destinationXdmPath": "person.name.firstName",
                "sourceAttribute": "FirstName",
                "identity": false,
                "identityGroup": null,
                "namespaceCode": null,
                "version": 0
            },
            {
                "destinationXdmPath": "person.name.lastName",
                "sourceAttribute": "LastName",
                "identity": false,
                "identityGroup": null,
                "namespaceCode": null,
                "version": 0
            }
        ]
    }'
```

| 屬性 | 說明 |
| --- | --- |
| `xdmSchema` | 目標XDM架構的ID。 |

**回應**

成功的響應返回新建立的映射的詳細資訊，包括其唯一標識符(`id`)。 在後續步驟中建立資料流時需要此值。

```json
{
    "id": "bf5286a9c1ad4266baca76ba3adc9366",
    "version": 0,
    "createdDate": 1597784069368,
    "modifiedDate": 1597784069368,
    "createdBy": "{CREATED_BY}",
    "modifiedBy": "{MODIFIED_BY}"
}
```

## 檢索資料流規範 {#specs}

資料流負責從源收集資料，並將其引入平台。 要建立資料流，必須首先獲得負責收集雲儲存資料的資料流規範。

**API格式**

```http
GET /flowSpecs?property=name=="CloudStorageToAEP"
```

**要求**

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/flowSpecs?property=name==%22CloudStorageToAEP%22' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的響應將返回負責將資料從源引入平台的資料流規範的詳細資訊。 響應包括唯一流規範 `id` 建立新資料流所需。

```json
{
    "items": [
        {
            "id": "9753525b-82c7-4dce-8a9b-5ccfce2b9876",
            "name": "CloudStorageToAEP",
            "providerId": "0ed90a81-07f4-4586-8190-b40eccef1c5a",
            "version": "1.0",
            "sourceConnectionSpecIds": [
                "b3ba5556-48be-44b7-8b85-ff2b69b46dc4",
                "ecadc60c-7455-4d87-84dc-2a0e293d997b",
                "b7829c2f-2eb0-4f49-a6ee-55e33008b629",
                "4c10e202-c428-4796-9208-5f1f5732b1cf",
                "fb2e94c9-c031-467d-8103-6bd6e0a432f2",
                "32e8f412-cdf7-464c-9885-78184cb113fd",
                "b7bf2577-4520-42c9-bae9-cad01560f7bc",
                "998b8ae3-cec0-43b7-8abe-40b1eb4ee069",
                "be5ec48c-5b78-49d5-b8fa-7c89ec4569b8"
            ],
            "targetConnectionSpecIds": [
                "c604ff05-7f1a-43c0-8e18-33bf874cb11c"
            ],
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
            "scheduleSpec": {
                "name": "PeriodicSchedule",
                "type": "Periodic",
                "spec": {
                    "$schema": "http://json-schema.org/draft-07/schema#",
                    "type": "object",
                    "properties": {
                        "startTime": {
                            "description": "epoch time",
                            "type": "integer"
                        },
                        "endTime": {
                            "description": "epoch time",
                            "type": "integer"
                        },
                        "interval": {
                            "type": "integer"
                        },
                        "frequency": {
                            "type": "string",
                            "enum": [
                                "minute",
                                "hour",
                                "day",
                                "week"
                            ]
                        },
                        "backfill": {
                            "type": "boolean",
                            "default": true
                        }
                    },
                    "required": [
                        "startTime",
                        "frequency",
                        "interval"
                    ],
                    "if": {
                        "properties": {
                            "frequency": {
                                "const": "minute"
                            }
                        }
                    },
                    "then": {
                        "properties": {
                            "interval": {
                                "minimum": 15
                            }
                        }
                    },
                    "else": {
                        "properties": {
                            "interval": {
                                "minimum": 1
                            }
                        }
                    }
                }
            },
            "permissionsInfo": {
                "view": [
                    {
                        "@type": "lowLevel",
                        "name": "EnterpriseSource",
                        "permissions": [
                            "read"
                        ]
                    }
                ],
                "manage": [
                    {
                        "@type": "lowLevel",
                        "name": "EnterpriseSource",
                        "permissions": [
                            "write"
                        ]
                    }
                ]
            }
        }
    ]
}
```

## 建立資料流

收集雲儲存資料的最後一步是建立資料流。 現在，您準備了以下必需值：

- [源連接ID](#source)
- [目標連接ID](#target)
- [映射ID](#mapping)
- [資料流規範ID](#specs)

資料流負責從源調度和收集資料。 通過在負載中提供先前提到的值的同時執行POST請求，可以建立資料流。

>[!NOTE]
>
>對於批處理接收，每個後續資料流都會根據源檔案選擇要從源檔案接收的檔案 **上次修改** 時間戳。 這意味著批處理資料流從源中選擇新檔案或自上次資料流運行以來已修改的檔案。

要計畫攝取，必須首先將開始時間值設定為劃時代（秒）。 然後，必須將頻率值設定為以下五個選項之一： `once`。 `minute`。 `hour`。 `day`或 `week`。 該間隔值指定兩個連續接收之間的期間，並且建立一次性接收不需要設定間隔。 對於所有其它頻率，間隔值必須設定為等於或大於 `15`。

>[!IMPORTANT]
>
>強烈建議在使用 [FTP連接器](../../../connectors/cloud-storage/ftp.md)。

**API格式**

```http
POST /flows
```

**要求**

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/flows' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Cloud Storage flow to Platform",
        "description": "Cloud Storage flow to Platform",
        "flowSpec": {
            "id": "9753525b-82c7-4dce-8a9b-5ccfce2b9876",
            "version": "1.0"
        },
        "sourceConnectionIds": [
            "26b53912-1005-49f0-b539-12100559f0e2"
        ],
        "targetConnectionIds": [
            "f7eb08fa-5f04-4e45-ab08-fa5f046e45ee"
        ],
        "transformations": [
            {
                "name": "Mapping",
                "params": {
                    "mappingId": "bf5286a9c1ad4266baca76ba3adc9366",
                    "mappingVersion": "0"
                }
            }
        ],
        "scheduleParams": {
            "startTime": "1597784298",
            "frequency":"minute",
            "interval":"30"
        }
    }'
```

| 屬性 | 說明 |
| --- | --- |
| `flowSpec.id` | 的 [流規範ID](#specs) 在上一步中檢索。 |
| `sourceConnectionIds` | 的 [源連接ID](#source) 在較早的步驟中檢索。 |
| `targetConnectionIds` | 的 [目標連接ID](#target-connection) 在較早的步驟中檢索。 |
| `transformations.params.mappingId` | 的 [映射ID](#mapping) 在較早的步驟中檢索。 |
| `scheduleParams.startTime` | 資料流在紀元時間中的開始時間。 |
| `scheduleParams.frequency` | 資料流收集資料的頻率。 可接受值包括： `once`。 `minute`。 `hour`。 `day`或 `week`。 |
| `scheduleParams.interval` | 該間隔指定兩個連續流運行之間的期間。 間隔的值應為非零整數。 頻率設定為時不需要間隔 `once` 應大於或等於 `15` 其他頻率值。 |

**回應**

成功的響應返回ID(`id`)。

```json
{
    "id": "dbc5c132-bc2a-4625-85c1-32bc2a262558",
    "etag": "\"8e000533-0000-0200-0000-5f3c40fd0000\""
}
```

## 監視資料流

建立資料流後，您可以監視正在通過其接收的資料，以查看有關流運行、完成狀態和錯誤的資訊。 有關如何監視資料流的詳細資訊，請參見上的教程 [監視API中的資料流](../monitor.md)

## 後續步驟

按照本教程，您建立了源連接器，以按計畫從雲儲存中收集資料。 現在，下游平台服務(如 [!DNL Real-time Customer Profile] 和 [!DNL Data Science Workspace]。 有關詳細資訊，請參閱以下文檔：

- [即時客戶概要資訊概述](../../../../profile/home.md)
- [資料科學工作區概述](../../../../data-science-workspace/home.md)

## 附錄 {#appendix}

以下部分列出了不同的雲儲存源連接器及其連接規範。

### 連接規範

| 連接器名稱 | 連接規範 |
| -------------- | --------------- |
| [!DNL Amazon S3] (S3) | `ecadc60c-7455-4d87-84dc-2a0e293d997b` |
| [!DNL Amazon Kinesis] (Kinesis) | `86043421-563b-46ec-8e6c-e23184711bf6` |
| [!DNL Azure Blob] (Blob) | `4c10e202-c428-4796-9208-5f1f5732b1cf` |
| [!DNL Azure Data Lake Storage Gen2] （ADLS第2代） | `b3ba5556-48be-44b7-8b85-ff2b69b46dc4` |
| [!DNL Azure Event Hubs] （事件中心） | `bf9f5905-92b7-48bf-bf20-455bc6b60a4e` |
| [!DNL Azure File Storage] | `be5ec48c-5b78-49d5-b8fa-7c89ec4569b8` |
| [!DNL Google Cloud Storage] | `32e8f412-cdf7-464c-9885-78184cb113fd` |
| [!DNL HDFS] | `54e221aa-d342-4707-bcff-7a4bceef0001` |
| [!DNL Oracle Object Storage] | `c85f9425-fb21-426c-ad0b-405e9bd8a46c` |
| [!DNL SFTP] | `bf367b0d-3d9b-4060-b67b-0d3d9bd06094` |
