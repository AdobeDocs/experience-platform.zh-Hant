---
keywords: Experience Platform；首頁；熱門主題；串流內嵌；內嵌；記錄資料；串流記錄資料；
solution: Experience Platform
title: 使用串流獲取API的串流記錄資料
type: Tutorial
description: 本教學課程將協助您開始使用Adobe Experience Platform資料擷取服務API中的串流擷取API。
exl-id: 097dfd5a-4e74-430d-8a12-cac11b1603aa
source-git-commit: e802932dea38ebbca8de012a4d285eab691231be
workflow-type: tm+mt
source-wordcount: '1025'
ht-degree: 2%

---


# 使用串流獲取API的串流記錄資料

本教學課程將協助您開始使用Adobe Experience Platform中的串流獲取API [!DNL Data Ingestion Service] API。

## 快速入門

本教學課程需具備各種Adobe Experience Platform服務的工作知識。 開始本教學課程之前，請先檢閱下列服務的檔案：

- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md):標準化框架 [!DNL Platform] 組織體驗資料。
   - [Schema Registry開發人員指南](../../xdm/api/getting-started.md):涵蓋以下各個可用端點的完整指南 [!DNL Schema Registry] API及如何對其進行呼叫。 這包括了解您的 `{TENANT_ID}`，且會了解如何建立結構描述（用於建立資料集以擷取），此功能會顯示於本教學課程的呼叫中。
- [[!DNL Real-Time Customer Profile]](../../profile/home.md):根據來自多個來源的匯總資料，即時提供統一的消費者設定檔。

### 使用平台API

如需如何成功呼叫Platform API的詳細資訊，請參閱 [Platform API快速入門](../../landing/api-guide.md).

## 根據 [!DNL XDM Individual Profile] 類

若要建立資料集，您必須先建立實作的新結構 [!DNL XDM Individual Profile] 類別。 如需如何建立結構的詳細資訊，請參閱 [Schema Registry API開發人員指南](../../xdm/api/getting-started.md).

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
| `title` | 要用於架構的名稱。 此名稱必須是唯一的。 |
| `description` | 您正在建立之結構的有意義說明。 |
| `meta:immutableTags` | 在此範例中， `union` 標籤可用來將資料保留至 [[!DNL Real-Time Customer Profile]](../../profile/home.md). |

**回應**

成功的回應會傳回HTTP狀態201，並包含新建立結構的詳細資訊。

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
| `{TENANT_ID}` | 此ID可確保您建立的資源與IMS組織中的資源命名正確，且完整無缺。 如需租用戶ID的詳細資訊，請閱讀 [方案註冊表指南](../../xdm/api/getting-started.md#know-your-tenant-id). |

請注意 `$id` 以及 `version` 屬性，因為建立資料集時，會同時使用這些屬性。

## 為架構設定主標識描述符

接下來，新增 [標識符](../../xdm/api/descriptors.md) 使用工作電子郵件地址屬性作為主要識別碼，重新命名為上述建立的架構。 執行此動作會產生兩個變更：

1. 工作電子郵件地址將成為必填欄位。 這表示未使用此欄位傳送的訊息將無法驗證，且不會擷取。

2. [!DNL Real-Time Customer Profile] 會使用工作電子郵件地址做為識別碼，協助匯整該個人的詳細資訊。

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
| `{SCHEMA_REF_ID}` | 此 `$id` 構建架構時先前收到的。 看起來應該像這樣： `"https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}"` |

>[!NOTE]
>
>&#x200B; &#x200B;**身分命名空間代碼**
>
> 請確定程式碼有效 — 上述範例使用「電子郵件」（標準身分命名空間）。 您可在 [Identity Service常見問題集](../../identity-service/troubleshooting-guide.md#what-are-the-standard-identity-namespaces-provided-by-experience-platform).
>
> 如果您想要建立自訂命名空間，請依照 [身分命名空間概述](../../identity-service/home.md).

**回應**

成功的響應返回HTTP狀態201，其中包含有關新建立的架構的主標識描述符的資訊。

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

建立結構後，您需要建立資料集以內嵌記錄資料。

>[!NOTE]
>
>此資料集將啟用 **[!DNL Real-Time Customer Profile]** 和 **[!DNL Identity Service]**.

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

成功的回應會傳回HTTP狀態201，而陣列會以格式包含新建立資料集的ID `@/dataSets/{DATASET_ID}`.

```json
[
    "@/dataSets/5e30d7986c0cc218a85cee65
]
```

## 建立串流連線

建立結構和資料集後，您可以建立串流連線

如需建立串流連線的詳細資訊，請參閱 [建立串流連線教學課程](./create-streaming-connection.md).

## 將記錄資料內嵌至串流連線 {#ingest-data}

有了資料集和串流連線，您就可以內嵌XDM格式的JSON記錄，將記錄資料內嵌至 [!DNL Platform].

**API格式**

```http
POST /collection/{CONNECTION_ID}?syncValidation=true
```

| 參數 | 說明 |
| --------- | ----------- |
| `{CONNECTION_ID}` | 此 `inletId` 串流連線的值。 |
| `syncValidation` | 供開發使用的選用查詢參數。 若設為 `true`，可用於立即回饋，以判斷要求是否成功傳送。 此值預設為 `false`. 請注意，若您將此查詢參數設為 `true` 要求的費率限制為每分鐘60次 `CONNECTION_ID`. |

**要求**

使用或不使用來源名稱，即可將記錄資料擷取至串流連線。

以下範例請求會將來源名稱遺失的記錄內嵌至Platform。 如果記錄缺少來源名稱，則會從串流連線定義新增來源ID。

>[!NOTE]
>
>下列API呼叫會執行 **not** 需要任何驗證標題。

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

如果要包括源名稱，以下示例將說明如何包括它。

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

成功的回應會傳回HTTP狀態200，並包含新串流的詳細資訊 [!DNL Profile].

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
| `{CONNECTION_ID}` | 先前建立的串流連線ID。 |
| `xactionId` | 在伺服器端為您剛傳送的記錄產生唯一識別碼。 此ID有助於Adobe通過各種系統和調試跟蹤此記錄的生命週期。 |
| `receivedTimeMs` | 顯示接收請求的時間的時間戳記（以毫秒為單位）。 |
| `syncValidation.status` | 由於查詢參數 `syncValidation=true` 新增後，此值就會出現。 如果驗證成功，狀態將為 `pass`. |

## 擷取新擷取的記錄資料

若要驗證先前擷取的記錄，您可以使用 [[!DNL Profile Access API]](../../profile/api/entities.md) 來擷取記錄資料。

>[!NOTE]
>
>如果未定義合併策略ID，則 `schema.name` 或 `relatedSchema.name` is `_xdm.context.profile`, [!DNL Profile Access] 將擷取 **all** 相關身分。

**API格式**

```http
GET /access/entities
GET /access/entities?{QUERY_PARAMETERS}
GET /access/entities?schema.name=_xdm.context.profile&entityId=janedoe@example.com&entityIdNS=email
```

| 參數 | 說明 |
| --------- | ----------- |
| `schema.name` | **必填。** 您正在存取的架構的名稱。 |
| `entityId` | 實體的ID。 若有提供，您也必須提供實體命名空間。 |
| `entityIdNS` | 您嘗試擷取之ID的命名空間。 |

**要求**

您可以透過下列請求檢閱先前擷取的記錄資料。

```shell
curl -X GET 'https://platform.adobe.io/data/core/ups/access/entities?schema.name=_xdm.context.profile&entityId=janedoe@example.com&entityIdNS=email'\
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應會傳回HTTP狀態200，並包含所請求實體的詳細資訊。 如您所見，這與先前成功擷取的記錄相同。

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

閱讀本檔案後，您現在就能了解如何將記錄資料內嵌至 [!DNL Platform] 使用串流連線。 您可以嘗試使用不同值進行更多呼叫並擷取更新的值。 此外，您也可以透過 [!DNL Platform] UI。 欲知更多資訊，請閱讀 [監控資料擷取](../quality/monitor-data-ingestion.md) 指南。

如需串流獲取的詳細資訊，請參閱 [串流獲取概觀](../streaming-ingestion/overview.md).
