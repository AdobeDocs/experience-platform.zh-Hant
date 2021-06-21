---
keywords: Experience Platform；首頁；熱門主題；資料來源連線
solution: Experience Platform
title: 使用Flow Service API從第三方雲儲存系統內嵌鑲木資料
topic-legacy: overview
type: Tutorial
description: 本教學課程使用流量服務API，逐步引導您完成從協力廠商雲端儲存系統內嵌Apache Parquet資料的步驟。
exl-id: fb1b19d6-16bb-4a5f-9e81-f537bac95041
source-git-commit: d3e1bc9bc075117dcc96c85b8b9c81d6ee617d29
workflow-type: tm+mt
source-wordcount: '1099'
ht-degree: 2%

---

# 使用[!DNL Flow Service] API從第三方雲儲存系統內嵌Parquet資料

[!DNL Flow Service] 可用來收集和集中Adobe Experience Platform中各種不同來源的客戶資料。該服務提供用戶介面和RESTful API，所有受支援的源都可從中連接。

本教學課程使用[!DNL Flow Service] API來引導您完成從協力廠商雲端儲存系統擷取Parquet資料的步驟。

## 快速入門

本指南需要妥善了解下列Adobe Experience Platform元件：

- [來源](../../home.md): [!DNL Experience Platform] 可讓您從各種來源擷取資料，同時使用服務來建構、加標籤及增強傳入 [!DNL Platform] 資料。
- [沙箱](../../../sandboxes/home.md): [!DNL Experience Platform] 提供可將單一執行個體分割成個 [!DNL Platform] 別虛擬環境的虛擬沙箱，以協助開發及改進數位體驗應用程式。

以下各節提供您需要了解的其他資訊，以便使用[!DNL Flow Service] API成功從第三方雲端儲存體內嵌Parquet資料。

### 讀取範例API呼叫

本教學課程提供範例API呼叫，以示範如何設定要求格式。 這些功能包括路徑、必要標題和格式正確的請求裝載。 也提供API回應中傳回的範例JSON。 如需範例API呼叫檔案中所使用慣例的資訊，請參閱[!DNL Experience Platform]疑難排解指南中[如何讀取範例API呼叫](../../../landing/troubleshooting.md#how-do-i-format-an-api-request)一節。

### 收集必要標題的值

若要呼叫[!DNL Platform] API，您必須先完成[authentication tutorial](https://www.adobe.com/go/platform-api-authentication-en)。 完成驗證教學課程後，將提供所有[!DNL Experience Platform] API呼叫中每個必要標題的值，如下所示：

- `Authorization: Bearer {ACCESS_TOKEN}`
- `x-api-key: {API_KEY}`
- `x-gw-ims-org-id: {IMS_ORG}`

[!DNL Experience Platform]中的所有資源，包括屬於[!DNL Flow Service]的資源，都與特定虛擬沙箱隔離。 對[!DNL Platform] API的所有請求都需要標題，以指定作業將在下列位置進行的沙箱名稱：

- `x-sandbox-name: {SANDBOX_NAME}`

所有包含裝載(POST、PUT、PATCH)的請求都需要其他媒體類型標題：

- `Content-Type: application/json`

## 建立連線

若要使用[!DNL Platform] API內嵌Parquet資料，您必須擁有您所存取之第三方雲端儲存來源的有效連線。 如果您尚未連接要使用的儲存，則可以通過以下教程建立連接：

- [Amazon S3](./create/cloud-storage/s3.md)
- [Azure Blob](./create/cloud-storage/blob.md)
- [Azure資料湖儲存Gen2](./create/cloud-storage/adls-gen2.md)
- [Google雲端商店](./create/cloud-storage/google.md)
- [SFTP](./create/cloud-storage/sftp.md)

取得並儲存連線的唯一識別碼(`$id`)，然後繼續進行本教學課程的下一個步驟。

## 建立目標結構

為了在[!DNL Platform]中使用源資料，還必須建立目標架構，以根據您的需要構建源資料。 然後，目標架構將用於建立包含源資料的[!DNL Platform]資料集。

如果您希望在[!DNL Experience Platform]中使用用戶介面，[架構編輯器教程](../../../xdm/tutorials/create-schema-ui.md)提供了在架構編輯器中執行類似操作的逐步說明。

**API格式**

```http
POST /schemaregistry/tenant/schemas
```

**要求**

下列範例要求會建立可擴充XDM [!DNL Individual Profile]類別的XDM架構。

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
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

成功的響應返回新建立的架構的詳細資訊，包括其唯一標識符(`$id`)。 在下一步建立源連接時需要此ID。

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
    "imsOrg": "{IMS_ORG}",
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

## 建立源連接 {#source}

建立目標XDM架構後，現在可以使用[!DNL Flow Service] API的POST請求來建立來源連線。 來源連線包含API的連線、來源資料格式，以及上一步驟中擷取之目標XDM架構的參考。

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
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
| `baseConnectionId` | 代表雲端儲存空間之API的連線。 |
| `data.schema.id` | (`$id`)，如果目標xdm架構是在前一個步驟中擷取的。 |
| `params.path` | 源檔案的路徑。 |

**回應**

成功的響應返回新建源連接的唯一標識符(`id`)。 在後續建立目標連線的步驟中，依需要儲存此值。

```json
{
    "id": "73bc8911-505a-4e46-bc89-11505a6e466f",
    "etag": "\"c4004435-0000-0200-0000-5e7437d90000\""
}
```

## 建立資料集基礎連線

若要將外部資料內嵌至[!DNL Platform]，必須先取得[!DNL Experience Platform]資料集基礎連線。

若要建立資料集基礎連線，請依照[資料集基礎連線教學課程](./create-dataset-base-connection.md)中概述的步驟操作。

請依照開發人員指南中概述的步驟操作，直到您建立資料集基底連線為止。 獲取並儲存唯一標識符(`$id`)，然後在下一步中繼續將其用作基本連接ID以建立目標連接。

## 建立目標資料集

目標資料集的建立方式，是對[目錄服務API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml)執行POST請求，提供裝載內目標架構的ID。

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
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
| `schemaRef.id` | 目標XDM結構的ID。 |

**回應**

成功的回應會傳回一個陣列，內含新建立資料集的ID，格式為`"@/datasets/{DATASET_ID}"`。 資料集ID是唯讀、系統產生的字串，用於在API呼叫中參考資料集。 在後續步驟建立目標連線和資料流時，視需要儲存目標資料集ID。

```json
[
    "@/dataSets/5e7439b1ad55a618ad4c5102"
]
```

## 建立目標連線 {#target}

您現在擁有資料集基礎連線、目標結構和目標資料集的唯一識別碼。 使用這些識別碼，您可以使用[!DNL Flow Service] API建立目標連線，以指定將包含傳入來源資料的資料集。

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
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
| `data.schema.id` | 目標XDM架構的`$id`。 |
| `params.dataSetId` | 目標資料集的ID。 |
| `connectionSpec.id` | 雲儲存的連接規範ID。 |

**回應**

成功的響應返回新目標連接的唯一標識符(`id`)。 在後續步驟中，視需要儲存此值。

```json
{
    "id": "9b3abc95-f2e9-47c1-babc-95f2e927c1ec",
    "etag": "\"7501936b-0000-0200-0000-5e743bcc0000\""
}
```

## 建立資料流

從第三方雲儲存中提取Parquet資料的最後一步是建立資料流。 您現在已準備下列必要值：

- [源連接ID](#source)
- [Target連線ID](#target)

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
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
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

成功的響應返回新建立的資料流的ID(`id`)。

```json
{
    "id": "89ff50ef-b082-426e-bf50-efb082d26e78",
    "etag": "\"890070b8-0000-0200-0000-5e743c040000\""
}
```

## 後續步驟

依照本教學課程，您已建立來源連接器，以排程從協力廠商雲端儲存系統收集Parquet資料。 下游[!DNL Platform]服務（如[!DNL Real-time Customer Profile]和[!DNL Data Science Workspace]）現在可以使用傳入資料。 如需詳細資訊，請參閱下列檔案：

- [即時客戶個人檔案概觀](../../../profile/home.md)
- [Data Science Workspace概觀](../../../data-science-workspace/home.md)
