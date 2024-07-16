---
keywords: Experience Platform；首頁；熱門主題；串流擷取；擷取；記錄資料；串流記錄資料；
solution: Experience Platform
title: 使用串流擷取API串流記錄資料
type: Tutorial
description: 本教學課程將協助您開始使用串流獲取API，這是Adobe Experience Platform資料獲取服務API的一部分。
exl-id: 097dfd5a-4e74-430d-8a12-cac11b1603aa
source-git-commit: 81f48de908b274d836f551bec5693de13c5edaf1
workflow-type: tm+mt
source-wordcount: '1032'
ht-degree: 2%

---


# 使用串流擷取API串流記錄資料

本教學課程將協助您開始使用串流獲取API (屬於Adobe Experience Platform [!DNL Data Ingestion Service] API的一部分)。

## 快速入門

本教學課程需要各種Adobe Experience Platform服務的實際操作知識。 在開始本教學課程之前，請先檢閱下列服務的檔案：

- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md)： [!DNL Platform]用來組織體驗資料的標準化架構。
   - [結構描述登入開發人員指南](../../xdm/api/getting-started.md)：涵蓋[!DNL Schema Registry] API每個可用端點的完整指南，以及如何對其發出呼叫。 這包括瞭解您在本教學課程呼叫中顯示的`{TENANT_ID}`，以及瞭解如何建立結構描述（用於建立要擷取的資料集）。
- [[!DNL Real-Time Customer Profile]](../../profile/home.md)：根據來自多個來源的彙總資料，即時提供統一的消費者設定檔。

### 使用平台API

如需如何成功呼叫Platform API的詳細資訊，請參閱[Platform API快速入門](../../landing/api-guide.md)的指南。

## 根據[!DNL XDM Individual Profile]類別來撰寫結構描述

若要建立資料集，您必須先建立實作[!DNL XDM Individual Profile]類別的新結構描述。 如需有關如何建立結構描述的詳細資訊，請參閱[結構描述登入API開發人員指南](../../xdm/api/getting-started.md)。

**API格式**

```http
POST /schemaregistry/tenant/schemas
```

**要求**

```shell
curl -X POST https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "type": "object",
    "title": "Sample schema",
    "description": "Sample description",
    "allOf": [
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile-person-details"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile-work-details"
        }
    ],
    "meta:immutableTags": [
        "union"
    ]
  }'
```

| 屬性 | 說明 |
| -------- | ----------- |
| `title` | 您要用於結構描述的名稱。 此名稱必須是唯一的。 |
| `description` | 有關您建立之綱要的有意義說明。 |
| `meta:immutableTags` | 在此範例中，`union`標籤用於將您的資料儲存到[[!DNL Real-Time Customer Profile]](../../profile/home.md)中。 |

**回應**

成功的回應會傳回HTTP狀態201以及您新建立之結構描述的詳細資料。

```json
{
    "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
    "meta:altId": "_{TENANT_ID}.schemas.{SCHEMA_ID}",
    "meta:resourceType": "schemas",
    "version": "1.0",
    "type": "object",
    "title": "Sample schema",
    "description": "Sample description",
    "allOf": [
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile-person-details"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile-work-details"
        }
    ],
    "meta:class": "https://ns.adobe.com/xdm/context/profile",
    "meta:abstract": false,
    "meta:extensible": false,
    "meta:extends": [
        "https://ns.adobe.com/xdm/context/profile",
        "https://ns.adobe.com/xdm/data/record",
        "https://ns.adobe.com/xdm/cpmtext/identitymap",
        "https://ns.adobe.com/xdm/common/extensible",
        "https://ns.adobe.com/xdm/common/auditable",
        "https://ns.adobe.com/xdm/context/profile-person-details",
        "https://ns.adobe.com/xdm/context/profile-work-details"
    ],
    "meta:immutableTags": [
        "union"
    ],
    "meta:containerId": "tenant",
    "imsOrg": "{ORG_ID}",
    "meta:xdmType": "object",
    "meta:registryMetadata": {
        "repo:createDate": 1551376506996,
        "repo:lastModifiedDate": 1551376506996,
        "xdm:createdClientId": "{CLIENT_ID}",
        "xdm:repositoryCreatedBy": "{CREATED_BY}"
    }
}
```

| 屬性 | 說明 |
| -------- | ----------- |
| `{TENANT_ID}` | 此ID可用來確保您建立的資源能正確進行名稱空間，並包含在您的組織內。 如需租使用者ID的詳細資訊，請參閱[結構描述登入指南](../../xdm/api/getting-started.md#know-your-tenant-id)。 |

請記下`$id`以及`version`屬性，因為建立資料集時會同時使用這兩個屬性。

## 設定結構描述的主要身分描述項

接著，將[身分描述項](../../xdm/api/descriptors.md)新增至上述建立的結構描述，使用工作電子郵件地址屬性做為主要識別碼。 這麼做將造成兩項變更：

1. 工作電子郵件地址將成為必填欄位。 這表示沒有此欄位傳送的訊息將無法通過驗證，且不會擷取。

2. [!DNL Real-Time Customer Profile]將使用工作電子郵件地址做為識別碼，以協助彙整該個人的更多資訊。

### 請求

```shell
curl -X POST https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "@type":"xdm:descriptorIdentity",
    "xdm:sourceProperty":"/workEmail/address",
    "xdm:property":"xdm:code",
    "xdm:isPrimary":true,
    "xdm:namespace":"Email",
    "xdm:sourceSchema":"{SCHEMA_REF_ID}",
    "xdm:sourceVersion":1
}
```

| 屬性 | 說明 |
| -------- | ----------- |
| `{SCHEMA_REF_ID}` | 您先前撰寫結構描述時收到的`$id`。 它應該看起來像這樣： `"https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}"` |

>[!NOTE]
>
>{&#x200B;0}身&#x200B;分名稱空間程式碼&#x200B;****
>
> 請確定程式碼有效 — 上述範例使用「電子郵件」，這是標準身分名稱空間。 在[Identity Service常見問題集](../../identity-service/troubleshooting-guide.md#what-are-the-standard-identity-namespaces-provided-by-experience-platform)中可找到其他常用的標準身分名稱空間。
>
> 如果要建立自訂名稱空間，請依照[身分名稱空間概觀](../../identity-service/home.md)中概述的步驟操作。

**回應**

成功的回應會傳回HTTP狀態201，其中包含有關結構描述新建立的主要身分描述項的資訊。

```json
{
    "xdm:property": "xdm:code",
    "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
    "xdm:namespace": "Email",
    "@type": "xdm:descriptorIdentity",
    "xdm:sourceVersion": 1,
    "xdm:isPrimary": true,
    "xdm:sourceProperty": "/workEmail/address",
    "@id": "17aaebfa382ce8fc0a40d3e43870b6470aab894e1c368d16",
    "meta:containerId": "tenant",
    "version": "1",
    "imsOrg": "{ORG_ID}"
}
```

## 建立記錄資料的資料集

建立結構描述後，您需要建立資料集以擷取記錄資料。

>[!NOTE]
>
>此資料集將針對&#x200B;**[!DNL Real-Time Customer Profile]**&#x200B;和&#x200B;**[!DNL Identity Service]**&#x200B;啟用。

**API格式**

```http
POST /catalog/dataSets
```

**要求**

```shell
curl -X POST https://platform.adobe.io/data/foundation/catalog/dataSets \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d ' {
    "name": "Dataset name",
    "description": "Dataset description",
    "schemaRef": {
        "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID},
        "contentType": "application/vnd.adobe.xed-full+json;version=1"
    },
    "tags": {
        "unifiedIdentity": ["enabled:true"],
        "unifiedProfile": ["enabled:true"]
    }
}'
```

**回應**

成功的回應會傳回HTTP狀態201以及包含新建立資料集識別碼（格式為`@/dataSets/{DATASET_ID}`）的陣列。

```json
[
    "@/dataSets/5e30d7986c0cc218a85cee65
]
```

## 建立串流連線

建立結構描述和資料集後，您可以建立串流連線

如需建立串流連線的詳細資訊，請參閱[建立串流連線教學課程](./create-streaming-connection.md)。

## 將記錄資料擷取至串流連線 {#ingest-data}

資料集和串流連線就緒後，您就可以內嵌XDM格式的JSON記錄，將記錄資料內嵌至[!DNL Platform]。

**API格式**

```http
POST /collection/{CONNECTION_ID}?syncValidation=true
```

| 參數 | 說明 |
| --------- | ----------- |
| `{CONNECTION_ID}` | 先前建立的串流連線的`inletId`值。 |
| `syncValidation` | 供開發使用的選用查詢引數。 如果設為`true`，則可將其用於立即回饋，以判斷要求是否已成功傳送。 預設情況下，此值設定為`false`。 請注意，如果您將此查詢引數設為`true`，則每`CONNECTION_ID`的請求速率限製為每分鐘60次。 |

**要求**

您可以將記錄資料擷取至串流連線，無論是否使用來源名稱皆可。

以下範例請求會將缺少來源名稱的記錄擷取至Platform。 如果記錄缺少來源名稱，則會從串流連線定義新增來源ID。

>[!NOTE]
>
>下列API呼叫&#x200B;**不**&#x200B;需要任何驗證標頭。

```shell
curl -X POST https://dcs.adobedc.net/collection/{CONNECTION_ID}?syncValidation=true \
  -H "Cache-Control: no-cache" \
  -H "Content-Type: application/json" \
  -d '{
    "header": {
        "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
            "contentType": "application/vnd.adobe.xed-full+json;version=1"
        },
        "imsOrgId": "{ORG_ID}",
        "datasetId": "{DATASET_ID}",
        "flowId": "{FLOW_ID}",
    },
    "body": {
        "xdmMeta": {
            "schemaRef": {
                "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
                "contentType": "application/vnd.adobe.xed-full+json;version=1"
            }
        },
        "xdmEntity": {
            "person": {
                "name": {
                    "firstName": "Jane",
                    "middleName": "F",
                    "lastName": "Doe"
                },
                "birthDate": "1969-03-14",
                "gender": "female"
            },
            "workEmail": {
                "primary": true,
                "address": "janedoe@example.com",
                "type": "work",
                "status": "active"
            }
        }
    }
}'
```

如果要包含來源名稱，下列範例顯示如何包含它。

```json
    "header": {
        "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
            "contentType": "application/vnd.adobe.xed-full+json;version=1"
        },
        "imsOrgId": "{ORG_ID}",
        "datasetId": "{DATASET_ID}",
        "source": {
            "name": "Sample source name"
        }
    }
```

**回應**

成功的回應傳回HTTP狀態200，其中包含新串流[!DNL Profile]的詳細資料。

```json
{
    "inletId": "{CONNECTION_ID}",
    "xactionId": "1584479347507:2153:240",
    "receivedTimeMs": 1584479347507,
    "syncValidation": {
        "status": "pass"
    }
}
```

| 屬性 | 說明 |
| -------- | ----------- |
| `{CONNECTION_ID}` | 先前建立串流連線的ID。 |
| `xactionId` | 在伺服器端為您剛傳送的記錄產生的唯一識別碼。 此ID可協助Adobe透過各種系統和偵錯追蹤此記錄的生命週期。 |
| `receivedTimeMs` | 顯示收到要求的時間戳記（紀元單位：毫秒）。 |
| `syncValidation.status` | 由於已新增查詢引數`syncValidation=true`，因此會顯示這個值。 如果驗證成功，狀態將會是`pass`。 |

## 擷取新擷取的記錄資料

若要驗證先前擷取的記錄，您可以使用[[!DNL Profile Access API]](../../profile/api/entities.md)來擷取記錄資料。

>[!NOTE]
>
>如果未定義合併原則ID，且`schema.name`或`relatedSchema.name`為`_xdm.context.profile`，則[!DNL Profile Access]將會擷取&#x200B;**所有**&#x200B;相關的身分。

**API格式**

```http
GET /access/entities
GET /access/entities?{QUERY_PARAMETERS}
GET /access/entities?schema.name=_xdm.context.profile&entityId=janedoe@example.com&entityIdNS=email
```

| 參數 | 說明 |
| --------- | ----------- |
| `schema.name` | **必要。**&#x200B;您正在存取的結構描述名稱。 |
| `entityId` | 實體的識別碼。 如果提供，您也必須提供實體名稱空間。 |
| `entityIdNS` | 您嘗試擷取的ID名稱空間。 |

**要求**

您可以使用以下GET請求來檢閱先前擷取的記錄資料。

```shell
curl -X GET 'https://platform.adobe.io/data/core/ups/access/entities?schema.name=_xdm.context.profile&entityId=janedoe@example.com&entityIdNS=email'\
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應會傳回HTTP狀態200以及要求實體的詳細資訊。 如您所見，這是與先前成功擷取的記錄相同。

```json
{
    "BVrqzwVv7o2p3naHvnsWpqZXv3KJgA": {
        "entityId": "BVrqzwVv7o2p3naHvnsWpqZXv3KJgA",
        "mergePolicy": {
            "id": "e161dae9-52f0-4c7f-b264-dc43dd903d56"
        },
        "sources": [
            "5e30d7986c0cc218a85cee65"
        ],
        "tags": [
            "1580346827274:2478:215"
        ],
        "identityGraph": [
            "BVrqzwVv7o2p3naHvnsWpqZXv3KJgA"
        ],
        "entity": {
            "person": {
                "name": {
                    "lastName": "Doe",
                    "middleName": "F",
                    "firstName": "Jane"
                },
                "gender": "female",
                "birthDate": "1969-03-14"
            },
            "workEmail": {
                "type": "work",
                "address": "janedoe@example.com",
                "status": "active",
                "primary": true
            },
            "identityMap": {
                "email": [
                    {
                        "id": "janedoe@example.com"
                    }
                ]
            }
        },
        "lastModifiedAt": "2020-01-30T01:13:59Z"
    }
}
```

## 後續步驟

閱讀本檔案後，您現在瞭解如何使用串流連線將記錄資料擷取到[!DNL Platform]。 您可以嘗試使用不同的值發出更多呼叫並擷取更新的值。 此外，您可以透過[!DNL Platform] UI開始監視您擷取的資料。 如需詳細資訊，請參閱[監視資料擷取](../quality/monitor-data-ingestion.md)指南。

如需一般串流擷取的詳細資訊，請閱讀[串流擷取總覽](../streaming-ingestion/overview.md)。
