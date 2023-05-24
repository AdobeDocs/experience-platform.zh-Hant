---
title: 使用流服務API為Pendo建立源連接和資料流
description: 瞭解如何使用流服務API將Adobe Experience Platform連接到Pendo。
badge: β
exl-id: 12b0295d-4b26-4eb7-a02a-a01d825d2a1e
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '1459'
ht-degree: 1%

---

# 建立源連接和資料流 [!DNL Pendo] 使用流服務API

>[!NOTE]
>
>的 [!DNL Pendo] 源為beta。 請閱讀 [源概述](../../../../home.md#terms-and-conditions) 的子菜單。

以下教程將指導您完成建立源連接和資料流的步驟，以便 [[!DNL Pendo]](https://Pendo.com/) 事件資料到Adobe Experience Platform [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/)。

## 快速入門 {#getting-started}

本指南要求對以下Experience Platform元件進行工作理解：

* [源](../../../../home.md):Experience Platform允許從各種源接收資料，同時讓您能夠使用 [!DNL Platform] 服務。
* [沙箱](../../../../../sandboxes/home.md):Experience Platform提供虛擬沙箱，將單個平台實例分區為獨立的虛擬環境，以幫助開發和發展數字型驗應用程式。

## 連接 [!DNL Pendo] 到使用 [!DNL Flow Service] API {#connect-platform-to-flow-api}

下面概述了建立源連接和資料流以使用 [!DNL Pendo] 事件資料到Experience Platform。

### 建立源連接 {#source-connection}

通過向Oracle提供POST請求建立源連接 [!DNL Flow Service] API，在提供源的連接規範ID時，提供名稱和說明等詳細資訊以及資料格式。

**API格式**

```https
POST /sourceConnections
```

**要求**

以下請求為 [!DNL Pendo]:

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
| `name` | 源連接的名稱。 確保源連接的名稱是描述性的，因為您可以使用它來查找有關源連接的資訊。 |
| `description` | 可以包括的可選值，用於提供有關源連接的詳細資訊。 |
| `connectionSpec.id` | 與源對應的連接規範ID。 |
| `data.format` | 格式 [!DNL Pendo] 要攝取的資料。 目前，唯一支援的資料格式是 `json`。 |

**回應**

成功的響應返回唯一標識符(`id`)。 在後續步驟中建立資料流時需要此ID。

```json
{
    "id": "76b968ff-3ff0-4e98-98bb-f3205d4d370c",
    "etag": "\"0301c198-0000-0200-0000-63f32ba50000\""
}
```

### 建立目標XDM架構 {#target-schema}

為了在平台中使用源資料，必須建立目標架構以根據您的需要來構造源資料。 然後使用目標模式建立包含源資料的平台資料集。

通過執行對目標XDM的POST請求，可以建立目標XDM模式 [架構註冊表API](https://developer.adobe.com/experience-platform-apis/references/schema-registry/)。

有關如何建立目標XDM架構的詳細步驟，請參見上的教程 [使用API建立架構](https://experienceleague.adobe.com/docs/experience-platform/xdm/api/schemas.html?lang=en#create)。

### 建立目標資料集 {#target-dataset}

通過對目標資料集執行POST請求，可以建立目標資料集 [目錄服務API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml)，提供負載內目標架構的ID。

有關如何建立目標資料集的詳細步驟，請參見上的教程 [使用API建立資料集](https://experienceleague.adobe.com/docs/experience-platform/catalog/api/create-dataset.html?lang=en)。

### 建立目標連接 {#target-connection}

目標連接表示到要儲存所攝取資料的目的地的連接。 要建立目標連接，必須提供與資料湖相對應的固定連接規範ID。 此ID為： `c604ff05-7f1a-43c0-8e18-33bf874cb11c`。

您現在將唯一標識符作為目標模式、目標資料集和到資料湖的連接規範ID。 使用這些標識符，可以使用 [!DNL Flow Service] API，用於指定將包含入站源資料的資料集。

**API格式**

```https
POST /targetConnections
```

**要求**

以下請求為 [!DNL Pendo]:

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
| `name` | 目標連接的名稱。 確保目標連接的名稱是描述性的，因為您可以使用此名稱查找有關目標連接的資訊。 |
| `description` | 可以包括的可選值，用於提供有關目標連接的詳細資訊。 |
| `connectionSpec.id` | 與資料湖對應的連接規範ID。 此固定ID為： `c604ff05-7f1a-43c0-8e18-33bf874cb11c`。 |
| `data.format` | 格式 [!DNL Pendo] 要攝取的資料。 |
| `params.dataSetId` | 在上一步中檢索到的目標資料集ID。 |

**回應**

成功的響應返回新目標連接的唯一標識符(`id`)。 後續步驟中需要此ID。

```json
{
    "id": "c63978c1-df7e-4611-aa32-3657eab5704b",
    "etag": "\"7f0045f1-0000-0200-0000-63f32c9d0000\""
}
```

### 建立映射 {#mapping}

為了將源資料攝取到目標資料集中，必須首先將其映射到目標資料集所遵循的目標模式。 這通過執行POST請求來實現 [[!DNL Data Prep] API](https://www.adobe.io/experience-platform-apis/references/data-prep/) 在請求負載中定義資料映射。

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
| `outputSchema.schemaRef.id` | 的ID [目標XDM架構](#target-schema) 生成。 |
| `mappings.sourceType` | 正在映射的源屬性類型。 |
| `mappings.source` | 需要映射到目標XDM路徑的源屬性。 |
| `mappings.destination` | 要映射源屬性的目標XDM路徑。 |

**回應**

成功的響應返回新建立的映射的詳細資訊，包括其唯一標識符(`id`)。 在後續步驟中建立資料流時需要此值。

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

### 建立流 {#flow}

向從 [!DNL Pendo] 平台是建立資料流。 現在，您準備了以下必需值：

* [源連接ID](#source-connection)
* [目標連接ID](#target-connection)
* [對應 ID](#mapping)

資料流負責從源調度和收集資料。 通過在負載中提供先前提到的值的同時執行POST請求，可以建立資料流。

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
| `name` | 資料流的名稱。 確保資料流的名稱是描述性的，因為您可以使用此名稱查找有關資料流的資訊。 |
| `description` | 可以包括的可選值，用於提供有關資料流的詳細資訊。 |
| `flowSpec.id` | 建立資料流所需的流規範ID。 此固定ID為： `e77fde5a-22a8-11ed-861d-0242ac120002`。 |
| `flowSpec.version` | 流規範ID的相應版本。 此值預設為 `1.0`。 |
| `sourceConnectionIds` | 的 [源連接ID](#source-connection) 生成。 |
| `targetConnectionIds` | 的 [目標連接ID](#target-connection) 生成。 |
| `transformations` | 此屬性包含需要應用於資料的各種轉換。 將不符合XDM的資料帶入平台時需要此屬性。 |
| `transformations.name` | 分配給轉換的名稱。 |
| `transformations.params.mappingId` | 的 [映射ID](#mapping) 生成。 |
| `transformations.params.mappingVersion` | 映射ID的相應版本。 此值預設為 `0`。 |

**回應**

成功的響應返回ID(`id`)。 您可以使用此ID監視、更新或刪除資料流。

```json
{
    "id": "c341617b-e143-43d5-aff1-da02b3e028b6",
    "etag": "\"9c01173c-0000-0200-0000-63f32d7c0000\""
}
```

### 獲取流終結點URL {#get-streaming-url}

建立資料流後，現在可以檢索流終結點URL。 您將使用此終結點URL將源訂閱到webhook，從而允許源與Experience Platform通信。

要檢索流終結點URL，請向 `/flows` 並提供資料流的ID。

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

成功的響應將返回有關資料流的資訊，包括標籤為的終結點URL `inletUrl`。 請參閱 [設定網頁掛接](../../../ui/create/analytics/pendo-webhook.md#get-streaming-endpoint-url) 的子菜單。

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

以下部分提供了有關可以監視、更新和刪除資料流的步驟的資訊。

### 監視資料流 {#monitor-dataflow}

建立資料流後，您可以監視正在通過其接收的資料，以查看有關流運行、完成狀態和錯誤的資訊。 有關完整的API示例，請閱讀上的指南 [使用API監視源資料流](https://experienceleague.adobe.com/docs/experience-platform/sources/api-tutorials/monitor.html)。

### 更新資料流 {#update-dataflow}

通過向發出PATCH請求來更新資料流的詳細資訊，如其名稱和說明，以及其運行計畫和關聯映射集 `/flows` 端點 [!DNL Flow Service] API，同時提供資料流的ID。 發出PATCH請求時，必須提供資料流的唯一性 `etag` 的 `If-Match` 標題。 有關完整的API示例，請閱讀上的指南 [使用API更新源資料流](https://experienceleague.adobe.com/docs/experience-platform/sources/api-tutorials/update-dataflows.html)

### 更新帳戶 {#update-account}

通過執行對的PATCH請求，更新源帳戶的名稱、說明和憑據 [!DNL Flow Service] API，同時將基本連接ID作為查詢參數提供。 發出PATCH請求時，必須提供源帳戶的唯一 `etag` 的 `If-Match` 標題。 有關完整的API示例，請閱讀上的指南 [使用API更新源帳戶](https://experienceleague.adobe.com/docs/experience-platform/sources/api-tutorials/update.html)。

### 刪除資料流 {#delete-dataflow}

通過執行DELETE請求刪除資料流 [!DNL Flow Service] API，同時提供要作為查詢參數一部分刪除的資料流的ID。 有關完整的API示例，請閱讀上的指南 [使用API刪除資料流](https://experienceleague.adobe.com/docs/experience-platform/sources/api-tutorials/delete-dataflows.html)。

### 刪除帳戶 {#delete-account}

通過執行DELETE請求刪除帳戶 [!DNL Flow Service] API，同時提供要刪除的帳戶的基本連接ID。 有關完整的API示例，請閱讀上的指南 [使用API刪除源帳戶](https://experienceleague.adobe.com/docs/experience-platform/sources/api-tutorials/delete.html)。
