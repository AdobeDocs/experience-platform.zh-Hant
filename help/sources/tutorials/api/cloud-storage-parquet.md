---
keywords: Experience Platform；首頁；熱門主題；資料來源連線
solution: Experience Platform
title: 使用流量服務API從第三方雲端儲存系統擷取Parquet資料
type: Tutorial
description: 本教學課程使用流程服務API來逐步引導您完成從協力廠商雲端儲存系統中擷取Apache Parquet資料的步驟。
exl-id: fb1b19d6-16bb-4a5f-9e81-f537bac95041
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '1088'
ht-degree: 9%

---

# 使用[!DNL Flow Service] API從協力廠商雲端儲存系統擷取Parquet資料

[!DNL Flow Service]用於收集及集中來自Adobe Experience Platform內各種不同來源的客戶資料。 此服務提供使用者介面和RESTful API，所有支援的來源都可從此API連線。

本教學課程使用[!DNL Flow Service] API逐步引導您完成從協力廠商雲端儲存系統擷取Parquet資料的步驟。

## 快速入門

本指南需要您深入了解下列 Adobe Experience Platform 元件：

- [來源](../../home.md)： [!DNL Experience Platform]允許從各種來源擷取資料，同時讓您能夠使用[!DNL Platform]服務來建構、加標籤以及增強傳入的資料。
- [沙箱](../../../sandboxes/home.md)： [!DNL Experience Platform]提供可將單一[!DNL Platform]執行個體分割成個別虛擬環境的虛擬沙箱，以利開發及改進數位體驗應用程式。

下列章節提供您需瞭解的其他資訊，才能使用[!DNL Flow Service] API從協力廠商雲端儲存空間成功擷取Parquet資料。

### 讀取範例 API 呼叫

本教學課程提供範例API呼叫，示範如何格式化您的請求。 這些包括路徑、必要的標頭和正確格式化的請求承載。 此外，也提供 API 回應中傳回的範例 JSON。 如需檔案中所使用範例API呼叫慣例的詳細資訊，請參閱[!DNL Experience Platform]疑難排解指南中[如何讀取範例API呼叫](../../../landing/troubleshooting.md#how-do-i-format-an-api-request)一節。

### 收集所需標頭的值

若要呼叫[!DNL Platform] API，您必須先完成[驗證教學課程](https://www.adobe.com/go/platform-api-authentication-en)。 完成驗證教學課程會提供所有 [!DNL Experience Platform] API 呼叫中每個必要標頭的值，如下所示：

- `Authorization: Bearer {ACCESS_TOKEN}`
- `x-api-key: {API_KEY}`
- `x-gw-ims-org-id: {ORG_ID}`

[!DNL Experience Platform]中的所有資源（包括屬於[!DNL Flow Service]的資源）都與特定的虛擬沙箱隔離。 對[!DNL Platform] API的所有請求都需要標頭，以指定將在其中執行作業的沙箱名稱：

- `x-sandbox-name: {SANDBOX_NAME}`

包含裝載(POST、PUT、PATCH)的所有請求都需要額外的媒體型別標頭：

- `Content-Type: application/json`

## 建立連線

若要使用[!DNL Platform] API擷取Parquet資料，您必須對要存取的第三方雲端儲存空間來源擁有有效的連線。 如果您尚未建立要使用的儲存裝置連線，您可以透過下列教學課程建立連線：

- [Amazon S3](./create/cloud-storage/s3.md)
- [Azure Blob](./create/cloud-storage/blob.md)
- [Azure Data Lake Storage Gen2](./create/cloud-storage/adls-gen2.md)
- [Google雲端商店](./create/cloud-storage/google.md)
- [SFTP](./create/cloud-storage/sftp.md)

取得並儲存連線的唯一識別碼(`$id`)，然後繼續本教學課程的下一個步驟。

## 建立目標結構描述

為了在[!DNL Platform]中使用來源資料，也必須建立目標結構描述，以根據您的需求建構來源資料。 然後使用目標結構描述來建立包含來源資料的[!DNL Platform]資料集。

如果您偏好在[!DNL Experience Platform]中使用使用者介面，[結構描述編輯器教學課程](../../../xdm/tutorials/create-schema-ui.md)會提供在結構描述編輯器中執行類似動作的逐步指示。

**API格式**

```http
POST /schemaregistry/tenant/schemas
```

**要求**

以下範例請求會建立擴充XDM [!DNL Individual Profile]類別的XDM結構描述。

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
    "type": "object",
    "title": "Sample Demo Profile XDM {{$guid}}",
    "description": "",
    "allOf": [
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile-person-details"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile-personal-details"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile-work-details"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile-subscriptions"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/identitymap"
        }
    ],
    "meta:containerId": "tenant",
    "meta:resourceType": "schemas",
    "meta:xdmType": "object",
    "meta:class": "https://ns.adobe.com/xdm/context/profile"
}'
```

**回應**

成功的回應會傳回新建立之結構描述的詳細資料，包括其唯一識別碼(`$id`)。 建立來源連線的下一個步驟需要此ID。

```json
{
    "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/e15530faf88aeb52d9ca5c5671a059f44f1a42ea7f5fdb80",
    "meta:altId": "_{TENANT_ID}.schemas.e15530faf88aeb52d9ca5c5671a059f44f1a42ea7f5fdb80",
    "meta:resourceType": "schemas",
    "version": "1.0",
    "title": "Sample Demo Profile XDM 8d96a964-aad8-43c5-a73a-c8b9b1ccbfb1",
    "type": "object",
    "description": "",
    "allOf": [
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile",
            "type": "object",
            "meta:xdmType": "object"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile-person-details",
            "type": "object",
            "meta:xdmType": "object"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile-personal-details",
            "type": "object",
            "meta:xdmType": "object"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile-work-details",
            "type": "object",
            "meta:xdmType": "object"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile-subscriptions",
            "type": "object",
            "meta:xdmType": "object"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/identitymap",
            "type": "object",
            "meta:xdmType": "object"
        }
    ],
    "refs": [
        "https://ns.adobe.com/xdm/context/profile-person-details",
        "https://ns.adobe.com/xdm/context/profile-personal-details",
        "https://ns.adobe.com/xdm/context/profile",
        "https://ns.adobe.com/xdm/context/profile-subscriptions",
        "https://ns.adobe.com/xdm/context/identitymap",
        "https://ns.adobe.com/xdm/context/profile-work-details"
    ],
    "imsOrg": "{ORG_ID}",
    "meta:extensible": false,
    "meta:abstract": false,
    "meta:extends": [
        "https://ns.adobe.com/xdm/context/profile-person-details",
        "https://ns.adobe.com/xdm/context/profile-personal-details",
        "https://ns.adobe.com/xdm/common/auditable",
        "https://ns.adobe.com/xdm/data/record",
        "https://ns.adobe.com/xdm/context/profile",
        "https://ns.adobe.com/xdm/context/profile-subscriptions",
        "https://ns.adobe.com/xdm/context/identitymap",
        "https://ns.adobe.com/xdm/context/profile-work-details"
    ],
    "meta:xdmType": "object",
    "meta:registryMetadata": {
        "repo:createdDate": 1584673864341,
        "repo:lastModifiedDate": 1584673864341,
        "xdm:createdClientId": "{CREATED_CLIENT_ID}",
        "xdm:lastModifiedClientId": "{MODIFIED_CLIENT_ID}",
        "xdm:createdUserId": "{CREATED_USER_ID}",
        "xdm:lastModifiedUserId": "{MODIFIED_USER_ID}",
        "eTag": "fa704f80da907c8f0f66f453ffcac3e52958687edbf55d71231dc5e1522193c4"
    },
    "meta:class": "https://ns.adobe.com/xdm/context/profile",
    "meta:containerId": "tenant",
    "meta:tenantNamespace": "_{TENANT_ID}"
}
```

## 建立來源連線 {#source}

建立目標XDM結構描述後，現在即可使用對[!DNL Flow Service] API的POST要求來建立來源連線。 來源連線包含API的連線、來源資料格式，以及對上一步驟中擷取的目標XDM架構的參照。

**API格式**

```http
POST /sourceConnections
```

**要求**

```shell
curl -X POST \
    'http://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Source Connection S3 {{$guid}}",
        "baseConnectionId": "5831c52c-c261-4945-b1c5-2cc261d945b2",
        "connectionSpec": {
            "id": "ecadc60c-7455-4d87-84dc-2a0e293d997b",
            "version": 1
        },
        "data": {
            "format": "parquet_xdm",
            "schema": {
                "id": "https://ns.adobe.com/{TENANT_ID}/schemas/e15530faf88aeb52d9ca5c5671a059f44f1a42ea7f5fdb80",
                "id": "",
                "version": "application/vnd.adobe.xed-full+json;version=1"
            }
        },
        "params": {
            "path": "partners-demo/samples",
            "recursive": "true"
        }
    }'
```

| 屬性 | 說明 |
| -------- | ----------- |
| `baseConnectionId` | 代表您雲端儲存空間的API連線。 |
| `data.schema.id` | (`$id`)，如果目標xdm結構描述已在上一步中擷取。 |
| `params.path` | 來源檔案的路徑。 |

**回應**

成功的回應會傳回新建立的來源連線的唯一識別碼(`id`)。 將此值儲存為稍後建立目標連線時所需的值。

```json
{
    "id": "73bc8911-505a-4e46-bc89-11505a6e466f",
    "etag": "\"c4004435-0000-0200-0000-5e7437d90000\""
}
```

## 建立資料集基礎連線

若要將外部資料擷取到[!DNL Platform]，必須先取得[!DNL Experience Platform]資料集基礎連線。

若要建立資料集基礎連線，請依照[資料集基礎連線教學課程](./create-dataset-base-connection.md)中概述的步驟操作。

繼續依照開發人員指南中概述的步驟進行，直到您建立資料集基礎連線為止。 取得並儲存唯一識別碼(`$id`)，然後繼續將它當做建立目標連線的下一個步驟中的基礎連線ID。

## 建立目標資料集

可以透過對[目錄服務API](https://www.adobe.io/experience-platform-apis/references/catalog/)執行POST要求，在承載中提供目標結構描述的ID來建立目標資料集。

**API格式**

```http
POST /catalog/dataSets
```

**要求**

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/catalog/dataSets?requestDataSource=true' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Leads Dataset {{$guid}}",
        "schemaRef": {
            "id": ""https://ns.adobe.com/{TENANT_ID}/schemas/e15530faf88aeb52d9ca5c5671a059f44f1a42ea7f5fdb80"",
            "contentType": "application/vnd.adobe.xed-full-notext+json; version=1"
        }
    }'
```

| 屬性 | 說明 |
| -------- | ----------- |
| `schemaRef.id` | 目標XDM結構描述的ID。 |

**回應**

成功的回應會傳回陣列，其中包含以`"@/datasets/{DATASET_ID}"`格式建立之新資料集的識別碼。 資料集ID是系統產生的唯讀字串，用來參考API呼叫中的資料集。 儲存目標資料集ID，因為後續步驟需要此ID來建立目標連線和資料流。

```json
[
    "@/dataSets/5e7439b1ad55a618ad4c5102"
]
```

## 建立目標連線 {#target}

您現在有資料集基礎連線、目標結構描述和目標資料集的唯一識別碼。 使用這些識別碼，您可以使用[!DNL Flow Service] API建立目標連線，以指定將包含傳入來源資料的資料集。

**API格式**

```http
POST /targetConnections
```

**要求**

```shell
curl -X POST \
    'http://platform.adobe.io/data/foundation/flowservice/targetConnections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "baseConnectionId": "291257e3-c560-4e07-9257-e3c5606e07d1",
        "connectionSpec": {
            "id":"c604ff05-7f1a-43c0-8e18-33bf874cb11c",
            "version": "1.0"
        },
        "name": "Target Connection {{$guid}}",
        "data": {
            "format": "parquet_xdm",
            "schema": {
                "id": ""https://ns.adobe.com/{TENANT_ID}/schemas/e15530faf88aeb52d9ca5c5671a059f44f1a42ea7f5fdb80"",
                "version": "application/vnd.adobe.xed-full+json;version=1"
            }
        },
        "params": {
            "dataSetId": "5e7439b1ad55a618ad4c5102"
        }
    }'
```

| 屬性 | 說明 |
| -------- | ----------- |
| `baseConnectionId` | 資料集基礎連線的ID。 |
| `data.schema.id` | 目標XDM結構的`$id`。 |
| `params.dataSetId` | 目標資料集的識別碼。 |
| `connectionSpec.id` | 您的雲端儲存空間的連線規格ID。 |

**回應**

成功的回應會傳回新目標連線的唯一識別碼(`id`)。 視需要在後續步驟中儲存此值。

```json
{
    "id": "9b3abc95-f2e9-47c1-babc-95f2e927c1ec",
    "etag": "\"7501936b-0000-0200-0000-5e743bcc0000\""
}
```

## 建立資料流

從第三方雲端儲存空間擷取Parquet資料的最後一步是建立資料流。 到現在為止，您已準備下列必要值：

- [Source連線ID](#source)
- [目標連線ID](#target)

資料流負責從來源排程及收集資料。 您可以執行POST要求，同時在裝載中提供先前提到的值，藉此建立資料流。

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
        "name": "Demo Parquet Ingestion Flow {{$guid}}",
        "flowSpec": {
            "id": "9753525b-82c7-4dce-8a9b-5ccfce2b9876",
            "version": "1.0"
        },
        "sourceConnectionIds": [
            "73bc8911-505a-4e46-bc89-11505a6e466f"
        ],
        "targetConnectionIds": [
            "9b3abc95-f2e9-47c1-babc-95f2e927c1ec"
        ],
        "scheduleParams": {
            "startTime": {{$timestamp}},
            "frequency": "minute",
            "interval": 1000,
            "backfill": true
        }
    }'
```

| 屬性 | 說明 |
| -------- | ----------- |
| `sourceConnectionIds` | 在先前步驟中擷取的來源連線ID。 |
| `targetConnectionIds` | 在先前步驟中擷取的目標連線ID。 |

**回應**

成功的回應會傳回新建立的資料流識別碼(`id`)。

```json
{
    "id": "89ff50ef-b082-426e-bf50-efb082d26e78",
    "etag": "\"890070b8-0000-0200-0000-5e743c040000\""
}
```

## 後續步驟

依照本教學課程所述，您已建立來源聯結器，以依排程從您的協力廠商雲端儲存系統收集Parquet資料。 下游[!DNL Platform]服務（例如[!DNL Real-Time Customer Profile]和[!DNL Data Science Workspace]）現在可以使用內送資料。 如需更多詳細資訊，請參閱下列檔案：

- [即時客戶輪廓概觀](../../../profile/home.md)
- [資料科學工作區總覽](../../../data-science-workspace/home.md)
