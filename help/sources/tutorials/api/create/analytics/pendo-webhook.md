---
title: 使用流服務API為Pendo建立源連接和資料流
description: 了解如何使用Flow Service API將Adobe Experience Platform連線至Pendo。
badge: "Beta"
source-git-commit: c35daa60db315f1ed04ed6424464f1ae7bfb4243
workflow-type: tm+mt
source-wordcount: '1459'
ht-degree: 1%

---

# 為建立源連接和資料流 [!DNL Pendo] 使用流量服務API

>[!NOTE]
>
>此 [!DNL Pendo] 來源為測試版。 請閱讀 [來源概觀](../../../../home.md#terms-and-conditions) 以取得使用測試版標籤來源的詳細資訊。

以下教程將逐步引導您完成建立源連接和資料流的步驟 [[!DNL Pendo]](https://Pendo.com/) 事件資料傳送至Adobe Experience Platform，使用 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## 快速入門 {#getting-started}

本指南需要妥善了解下列Experience Platform元件：

* [來源](../../../../home.md):Experience Platform可讓您從各種來源擷取資料，同時使用來建構、加標籤及增強傳入資料 [!DNL Platform] 服務。
* [沙箱](../../../../../sandboxes/home.md):Experience Platform提供可將單一Platform執行個體分割成個別虛擬環境的虛擬沙箱，以協助開發及改進數位體驗應用程式。

## Connect [!DNL Pendo] 到使用 [!DNL Flow Service] API {#connect-platform-to-flow-api}

以下概述建立源連接和資料流以帶來您 [!DNL Pendo] 事件資料Experience Platform。

### 建立源連接 {#source-connection}

向發出POST請求以建立來源連線 [!DNL Flow Service] API，在提供來源的連線規格ID時，會提供名稱和說明等詳細資訊，以及資料的格式。

**API格式**

```https
POST /sourceConnections
```

**要求**

以下請求將建立源連接 [!DNL Pendo]:

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Streaming Source Connection for Pendo",
      "providerId": "521eee4d-8cbe-4906-bb48-fb6bd4450033",
      "description": "Streaming Source Connection for Pendo",
      "connectionSpec": {
          "id": "6ff5654f-19d5-427d-bd3e-c0ebc802389a",
          "version": "1.0"
      },
      "data": {
          "format": "json"
      }
    }'
```

| 屬性 | 說明 |
| --- | --- |
| `name` | 源連接的名稱。 請確保源連接的名稱是描述性的，因為您可以使用此名稱查找有關源連接的資訊。 |
| `description` | 可包含的選用值，用於提供來源連線的詳細資訊。 |
| `connectionSpec.id` | 與源對應的連接規範ID。 |
| `data.format` | 格式 [!DNL Pendo] 您要擷取的資料。 目前，唯一支援的資料格式是 `json`. |

**回應**

成功的回應會傳回唯一識別碼(`id`)。 在後續步驟中需要此ID才能建立資料流。

```json
{
    "id": "76b968ff-3ff0-4e98-98bb-f3205d4d370c",
    "etag": "\"0301c198-0000-0200-0000-63f32ba50000\""
}
```

### 建立目標XDM結構 {#target-schema}

為了在Platform中使用來源資料，必須建立目標架構，以根據您的需求來建構來源資料。 然後，目標架構會用來建立包含來源資料的Platform資料集。

您可以透過執行POST要求來建立目標XDM結構 [結構註冊表API](https://developer.adobe.com/experience-platform-apis/references/schema-registry/).

如需建立Target XDM結構的詳細步驟，請參閱 [使用API建立結構](https://experienceleague.adobe.com/docs/experience-platform/xdm/api/schemas.html?lang=en#create).

### 建立目標資料集 {#target-dataset}

目標資料集的建立方式，是透過對 [目錄服務API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml)，提供裝載中目標架構的ID。

如需如何建立目標資料集的詳細步驟，請參閱 [使用API建立資料集](https://experienceleague.adobe.com/docs/experience-platform/catalog/api/create-dataset.html?lang=en).

### 建立目標連線 {#target-connection}

目標連線代表要儲存所擷取資料的目的地連線。 要建立目標連接，必須提供與資料庫對應的固定連接規範ID。 此ID為： `c604ff05-7f1a-43c0-8e18-33bf874cb11c`.

您現在擁有目標架構、目標資料集以及資料湖的連線規格ID的唯一識別碼。 使用這些識別碼，您可以使用 [!DNL Flow Service] API，指定包含傳入來源資料的資料集。

**API格式**

```https
POST /targetConnections
```

**要求**

下列請求會為 [!DNL Pendo]:

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/targetConnections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Streaming Target Connection for Pendo",
      "description": "Streaming Target Connection for Pendo",
      "connectionSpec": {
          "id": "c604ff05-7f1a-43c0-8e18-33bf874cb11c",
          "version": "1.0"
      },
      "data": {
          "format": "json",
          "schema": {
              "id": "https://ns.adobe.com/extconndev/schemas/b48de0b204046e65a4c50232e7946401946b4c519fd7c172",
              "version": "application/vnd.adobe.xed-full+json;version=1"
          }
      },
      "params": {
          "dataSetId": "63dca52231a6031c07280614"
      }
  }'
```

| 屬性 | 說明 |
| -------- | ----------- |
| `name` | 目標連接的名稱。 請確定目標連線的名稱是描述性的，因為您可以使用此名稱來查詢目標連線的資訊。 |
| `description` | 可包含的選用值，用於提供目標連線的詳細資訊。 |
| `connectionSpec.id` | 與資料湖對應的連接規範ID。 此固定ID為： `c604ff05-7f1a-43c0-8e18-33bf874cb11c`. |
| `data.format` | 格式 [!DNL Pendo] 您要擷取的資料。 |
| `params.dataSetId` | 上一步驟中擷取的目標資料集ID。 |

**回應**

成功的回應會傳回新目標連線的唯一識別碼(`id`)。 後續步驟需要此ID。

```json
{
    "id": "c63978c1-df7e-4611-aa32-3657eab5704b",
    "etag": "\"7f0045f1-0000-0200-0000-63f32c9d0000\""
}
```

### 建立對應 {#mapping}

若要將來源資料內嵌至目標資料集，必須先將其對應至目標資料集所遵守的目標架構。 這是透過執行POST要求來達成 [[!DNL Data Prep] API](https://www.adobe.io/experience-platform-apis/references/data-prep/) 在要求裝載中定義的資料對應。

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "outputSchema": {
          "schemaRef": {
              "id": "https://ns.adobe.com/{TENANT_ID}/schemas/945546112b746524bfd9f1264b26c2b7d8e7f5b7fadb953a",
              "contentType": "application/vnd.adobe.xed-full+json;version=1"
          }
      },
    "mappings": [
        {
            "destinationXdmPath": "_extconndev.accountid",
            "sourceAttribute": "accountId",
            "identity": false,
            "version": 0
        },
        {
            "destinationXdmPath": "_extconndev.uniqueid",
            "sourceAttribute": "uniqueId",
            "identity": false,
            "version": 0
        },
        {
            "destinationXdmPath": "_extconndev.name1",
            "sourceAttribute": "properties.guideProperties.name",
            "identity": false,
            "version": 0
        },
        {
            "destinationXdmPath": "_extconndev.timestamp1",
            "sourceAttribute": "timestamp",
            "identity": false,
            "version": 0
        },
        {
            "destinationXdmPath": "_extconndev.visitorid",
            "sourceAttribute": "visitorId",
            "identity": false,
            "version": 0
        }
    ]
  }'
```

| 屬性 | 說明 |
| --- | --- |
| `outputSchema.schemaRef.id` | 的ID [target XDM結構](#target-schema) 在先前的步驟中產生。 |
| `mappings.sourceType` | 要映射的源屬性類型。 |
| `mappings.source` | 需要對應至目標XDM路徑的來源屬性。 |
| `mappings.destination` | 要映射源屬性的目標XDM路徑。 |

**回應**

成功的回應會傳回新建立之對應的詳細資訊，包括其唯一識別碼(`id`)。 在以後的步驟中需要此值才能建立資料流。

```json
{
    "id": "a126ae1a1d134c4b82bd00c2d01a039e",
    "version": 0,
    "createdDate": 1676881164541,
    "modifiedDate": 1676881164541,
    "createdBy": "{CREATED_BY}",
    "modifiedBy": "{MODIFIED_BY}"
}
```

### 建立流程 {#flow}

將資料從 [!DNL Pendo] 到平台是建立資料流。 您現在已準備下列必要值：

* [源連接ID](#source-connection)
* [Target連線ID](#target-connection)
* [對應ID](#mapping)

資料流負責從源中調度和收集資料。 您可以在裝載中提供先前提及的值時，執行POST要求來建立資料流。

**API格式**

```http
POST /flows
```

**要求**

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/flows' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Streaming Dataflow for Pendo",
      "description": "Streaming Dataflow for Pendo",
      "flowSpec": {
          "id": "e77fde5a-22a8-11ed-861d-0242ac120002",
          "version": "1.0"
      },
      "sourceConnectionIds": [
          "339d60a5-9ff6-4eba-8197-e8887eeb3c08"
      ],
      "targetConnectionIds": [
          "df7c660e-3484-463b-b01a-1835e9b04ac9"
      ],
      "transformations": [
      {
        "name": "Mapping",
        "params": {
          "mappingId": "bae11501021646e58cecc1182451af22",
          "mappingVersion": 0
        }
      }
    ]
  }'
```

| 屬性 | 說明 |
| --- | --- |
| `name` | 資料流的名稱。 請確保資料流的名稱具有描述性，因為您可以使用此名稱查找資料流的資訊。 |
| `description` | 一個可選值，可以包括該值以提供有關資料流的詳細資訊。 |
| `flowSpec.id` | 建立資料流所需的流規範ID。 此固定ID為： `e77fde5a-22a8-11ed-861d-0242ac120002`. |
| `flowSpec.version` | 流規範ID的相應版本。 此值預設為 `1.0`. |
| `sourceConnectionIds` | 此 [源連接ID](#source-connection) 在先前的步驟中產生。 |
| `targetConnectionIds` | 此 [目標連線ID](#target-connection) 在先前的步驟中產生。 |
| `transformations` | 此屬性包含需要套用至資料的各種轉換。 將不符合XDM的資料帶入Platform時，此屬性為必要屬性。 |
| `transformations.name` | 指派給轉換的名稱。 |
| `transformations.params.mappingId` | 此 [對應ID](#mapping) 在先前的步驟中產生。 |
| `transformations.params.mappingVersion` | 對應ID的對應版本。 此值預設為 `0`. |

**回應**

成功的回應會傳回ID(`id`)。 您可以使用此ID監視、更新或刪除資料流。

```json
{
    "id": "c341617b-e143-43d5-aff1-da02b3e028b6",
    "etag": "\"9c01173c-0000-0200-0000-63f32d7c0000\""
}
```

### 取得您的串流端點URL {#get-streaming-url}

建立資料流後，您現在可以檢索流終結點URL。 您將使用此端點URL將源訂閱到Webhook，從而允許源與Experience Platform通信。

若要擷取串流端點URL，請向 `/flows` 端點，並提供資料流的ID。

**API格式**

```http
GET /flows/{FLOW_ID}
```

**要求**

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/flows/4982698b-e6b3-48c2-8dcf-040e20121fd2' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的響應返回有關資料流的資訊，包括終結點URL，標籤為 `inletUrl`. 請參閱 [設定Webhook](../../../ui/create/analytics/pendo-webhook.md#get-streaming-endpoint-url) 頁面，以取得必要值。

```json
{
    "items": [
        {
            "id": "d947e6a9-ea53-42c4-985c-c9379265491f",
            "createdAt": 1676875325841,
            "updatedAt": 1676875331938,
            "createdBy": "acme@AdobeID",
            "updatedBy": "acme@AdobeID",
            "createdClient": "{CREATED_CLIENT}",
            "updatedClient": "{UPDATED_CLIENT}",
            "sandboxId": "{SANDBOX_ID}",
            "sandboxName": "{SANDBOX_NAME}",
            "imsOrgId": "{ORG_ID}",
            "name": "Streaming Dataflow for Pendo",
            "description": "Streaming Dataflow for Pendo",
            "flowSpec": {
                "id": "e77fde5a-22a8-11ed-861d-0242ac120002",
                "version": "1.0"
            },
            "state": "enabled",
            "version": "\"9801a366-0000-0200-0000-63f2f92c0000\"",
            "etag": "\"9801a366-0000-0200-0000-63f2f92c0000\"",
            "sourceConnectionIds": [
                "339d60a5-9ff6-4eba-8197-e8887eeb3c08"
            ],
            "targetConnectionIds": [
                "df7c660e-3484-463b-b01a-1835e9b04ac9"
            ],
            "inheritedAttributes": {
                "properties": {
                    "isSourceFlow": true
                },
                "sourceConnections": [
                    {
                        "id": "339d60a5-9ff6-4eba-8197-e8887eeb3c08",
                        "connectionSpec": {
                            "id": "6ff5654f-19d5-427d-bd3e-c0ebc802389a",
                            "version": "1.0"
                        }
                    }
                ],
                "targetConnections": [
                    {
                        "id": "df7c660e-3484-463b-b01a-1835e9b04ac9",
                        "connectionSpec": {
                            "id": "c604ff05-7f1a-43c0-8e18-33bf874cb11c",
                            "version": "1.0"
                        }
                    }
                ]
            },
            "options": {
                "inletUrl": "https://dcs.adobedc.net/collection/e389c18dbc7f5de8b95df07b1b89d76ddd9b1e88d5423abc71b6ac9161491373"
            },
            "transformations": [
                {
                    "name": "Mapping",
                    "params": {
                        "mappingId": "bae11501021646e58cecc1182451af22",
                        "mappingVersion": 0
                    }
                }
            ],
            "runs": "/runs?property=flowId==4d90b316-1c9b-469d-935f-5a27d5deefdf",
            "providerRefId": "19d9fb14-9cb9-42a5-bb8b-23dc545e766a",
            "lastOperation": {
                "started": 0,
                "updated": 0,
                "operation": "enable"
            },
            "lastRunDetails": {
                "id": "d6972216-2332-41f6-8ed3-2ac82e6550b7",
                "state": "partialSuccess",
                "startedAtUTC": 1676862000000,
                "completedAtUTC": 1676867880000
            }
        }
    ]
}
```

## 附錄 {#appendix}

以下部分提供了可以監視、更新和刪除資料流的步驟資訊。

### 監視資料流 {#monitor-dataflow}

建立資料流後，您可以監視正在通過資料流進行內嵌的資料，以查看有關流運行、完成狀態和錯誤的資訊。 如需完整的API範例，請參閱 [使用API監控來源資料流](https://experienceleague.adobe.com/docs/experience-platform/sources/api-tutorials/monitor.html).

### 更新資料流 {#update-dataflow}

通過向發出PATCH請求，更新資料流的詳細資訊（如其名稱和說明），以及其運行計畫和關聯的映射集 `/flows` 端點 [!DNL Flow Service] API，同時提供資料流的ID。 發出PATCH請求時，必須提供資料流的唯一 `etag` 在 `If-Match` 頁首。 如需完整的API範例，請參閱 [使用API更新源資料流](https://experienceleague.adobe.com/docs/experience-platform/sources/api-tutorials/update-dataflows.html)

### 更新您的帳戶 {#update-account}

通過向執行PATCH請求，更新源帳戶的名稱、說明和憑據 [!DNL Flow Service] API，同時將基本連線ID設為查詢參數。 提出PATCH請求時，您必須提供來源帳戶的唯一 `etag` 在 `If-Match` 頁首。 如需完整的API範例，請參閱 [使用API更新您的來源帳戶](https://experienceleague.adobe.com/docs/experience-platform/sources/api-tutorials/update.html).

### 刪除資料流 {#delete-dataflow}

通過執行DELETE請求以刪除資料流 [!DNL Flow Service] API，同時提供您要在查詢參數中刪除之資料流的ID。 如需完整的API範例，請參閱 [使用API刪除資料流](https://experienceleague.adobe.com/docs/experience-platform/sources/api-tutorials/delete-dataflows.html).

### 刪除您的帳戶 {#delete-account}

對執行DELETE請求以刪除帳戶 [!DNL Flow Service] API，同時提供您要刪除之帳戶的基本連線ID。 如需完整的API範例，請參閱 [使用API刪除您的來源帳戶](https://experienceleague.adobe.com/docs/experience-platform/sources/api-tutorials/delete.html).