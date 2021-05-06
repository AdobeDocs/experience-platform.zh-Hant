---
keywords: Experience Platform; home；熱門主題；流處理；攝取；記錄資料；流記錄資料；
solution: Experience Platform
title: 使用串流擷取API來串流記錄資料
topic-legacy: tutorial
type: Tutorial
description: 本教學課程將協助您開始使用串流擷取API，這是Adobe Experience Platform資料擷取服務API的一部分。
exl-id: 097dfd5a-4e74-430d-8a12-cac11b1603aa
translation-type: tm+mt
source-git-commit: 544eeb3a27d0b218885e3000deb214f21c8e9fcd
workflow-type: tm+mt
source-wordcount: '1168'
ht-degree: 2%

---


# 使用串流擷取API來串流記錄資料

本教學課程將協助您開始使用串流擷取API，這是Adobe Experience Platform[!DNL Data Ingestion Service] API的一部分。

## 快速入門

本教學課程需要具備Adobe Experience Platform各項服務的相關知識。 在開始本教學課程之前，請先閱讀下列服務的檔案：

- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md):組織體驗資料的 [!DNL Platform] 標準化架構。
   - [架構註冊開發人員指南](../../xdm/api/getting-started.md):完整的指南，涵蓋 [!DNL Schema Registry] API的每個可用端點，以及如何呼叫這些端點。這包括瞭解在本教學課程中的呼叫中出現的`{TENANT_ID}`，以及瞭解如何建立結構描述（用於建立資料集以擷取）。
- [[!DNL Real-time Customer Profile]](../../profile/home.md):根據來自多個來源的匯整資料，即時提供統一的消費者個人檔案。

以下章節提供您需要知道的其他資訊，以便成功呼叫串流擷取API。

### 讀取範例API呼叫

本指南提供範例API呼叫，以示範如何格式化您的請求。 這些包括路徑、必要標題和正確格式化的請求負載。 也提供API回應中傳回的範例JSON。 如需範例API呼叫檔案中所用慣例的詳細資訊，請參閱[!DNL Experience Platform]疑難排解指南中[如何讀取範例API呼叫](../../landing/troubleshooting.md#how-do-i-format-an-api-request)一節。

### 收集必要標題的值

若要呼叫[!DNL Platform] API，您必須先完成[驗證教學課程](https://www.adobe.com/go/platform-api-authentication-en)。 完成驗證教學課程後，所有[!DNL Experience Platform] API呼叫中每個所需標題的值都會顯示在下面：

- 授權：載體`{ACCESS_TOKEN}`
- x-api-key:`{API_KEY}`
- x-gw-ims-org-id:`{IMS_ORG}`

[!DNL Experience Platform]中的所有資源都隔離到特定的虛擬沙盒。 對[!DNL Platform] API的所有請求都需要一個標題，該標題指定要在中執行操作的沙盒的名稱：

- x-sandbox-name:`{SANDBOX_NAME}`

>[!NOTE]
>
>如需[!DNL Platform]中沙盒的詳細資訊，請參閱[沙盒概述檔案](../../sandboxes/home.md)。

所有包含裝載(POST、PUT、PATCH)的請求都需要額外的標題：

- 內容類型：application/json

## 基於[!DNL XDM Individual Profile]類合成方案

若要建立資料集，您必須先建立實作[!DNL XDM Individual Profile]類別的新架構。 有關如何建立架構的詳細資訊，請閱讀[Schema Registry API開發人員指南](../../xdm/api/getting-started.md)。

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
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
| `title` | 您要用於架構的名稱。 此名稱必須是唯一的。 |
| `description` | 正在建立的方案的有意義說明。 |
| `meta:immutableTags` | 在此範例中，`union`標籤可用來將資料保存至[[!DNL Real-time Customer Profile]](../../profile/home.md)。 |

**回應**

成功的回應會傳回HTTP狀態201，並包含您新建立之架構的詳細資訊。

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
    "imsOrg": "{IMS_ORG}",
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
| `{TENANT_ID}` | 此ID可用來確保您建立的資源已正確命名並包含在IMS組織中。 如需租用戶ID的詳細資訊，請閱讀[架構註冊表指南](../../xdm/api/getting-started.md#know-your-tenant-id)。 |

請注意`$id`和`version`屬性，因為在建立資料集時將使用這兩種屬性。

## 為方案設定主標識描述符

接著，將[標識描述符](../../xdm/api/descriptors.md)添加到上述建立的模式中，使用工作電子郵件地址屬性作為主標識符。 這樣做會產生兩項變更：

1. 工作電子郵件地址將成為必填欄位。 這表示未使用此欄位傳送的訊息將無法驗證，且不會被收錄。

2. [!DNL Real-time Customer Profile] 將會使用工作電子郵件地址做為識別碼，協助拼湊出更多有關該個人的資訊。

### 請求

```shell
curl -X POST https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
| `{SCHEMA_REF_ID}` | 構建架構時先前收到的`$id`。 它應該看起來像這樣：`"https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}"` |

>[!NOTE]
>
>&#x200B;&#x200B;**識別名稱空間代碼**
>
> 請確定代碼有效——上述範例使用「電子郵件」，此為標準身分命名空間。 其他常用的標準身分名稱空間可在[Identity Service常見問答集](../../identity-service/troubleshooting-guide.md#what-are-the-standard-identity-namespaces-provided-by-experience-platform)中找到。
>
> 如果您想要建立自訂命名空間，請依照[identity namespace overview](../../identity-service/home.md)中所述的步驟進行。

**回應**

成功的響應返回HTTP狀態201，其中包含有關新建立的架構主標識描述符的資訊。

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
    "imsOrg": "{IMS_ORG}"
}
```

## 建立記錄資料的資料集

建立結構後，您需要建立資料集來收錄記錄資料。

>[!NOTE]
>
>此資料集將啟用&#x200B;**[!DNL Real-time Customer Profile]**&#x200B;和&#x200B;**[!DNL Identity Service]**。

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
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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

成功的回應會傳回HTTP狀態201，並傳回包含以`@/dataSets/{DATASET_ID}`格式新建立資料集ID的陣列。

```json
[
    "@/dataSets/5e30d7986c0cc218a85cee65
]
```

## 建立串流連線

在建立架構和資料集後，您可以建立串流連線

有關建立流連接的詳細資訊，請閱讀[建立流連接教程](./create-streaming-connection.md)。

## 將記錄資料收錄到流連接{#ingest-data}

有了資料集和串流連線，您就可以內嵌XDM格式的JSON記錄，將記錄資料內嵌至[!DNL Platform]。

**API格式**

```http
POST /collection/{CONNECTION_ID}?synchronousValidation=true
```

| 參數 | 說明 |
| --------- | ----------- |
| `{CONNECTION_ID}` | 先前建立的串流連接的`inletId`值。 |
| `synchronousValidation` | 可選的查詢參數，用於開發用途。 如果設為`true`，則可用於立即回饋，以判斷請求是否成功傳送。 依預設，此值會設為`false`。 |

**要求**

將記錄資料收錄到串流連接可以使用或不使用源名稱。

下面的範例請求會將遺失來源名稱的記錄擷取至平台。 如果記錄缺少源名稱，它將從流連接定義中添加源ID。

>[!NOTE]
>
>下列API呼叫&#x200B;**not**&#x200B;需要任何驗證標題。

```shell
curl -X POST https://dcs.adobedc.net/collection/{CONNECTION_ID}?synchronousValidation=true \
  -H "Cache-Control: no-cache" \
  -H "Content-Type: application/json" \
  -d '{
    "header": {
        "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
            "contentType": "application/vnd.adobe.xed-full+json;version=1"
        },
        "imsOrgId": "{IMS_ORG}",
        "datasetId": "{DATASET_ID}"
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

如果要包含源名稱，以下示例將說明如何包括該名稱。

```json
    "header": {
        "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
            "contentType": "application/vnd.adobe.xed-full+json;version=1"
        },
        "imsOrgId": "{IMS_ORG}",
        "datasetId": "{DATASET_ID}",
        "source": {
            "name": "Sample source name"
        }
    }
```

**回應**

成功的回應會傳回HTTP狀態200，並包含新串流[!DNL Profile]的詳細資訊。

```json
{
    "inletId": "{CONNECTION_ID}",
    "xactionId": "1584479347507:2153:240",
    "receivedTimeMs": 1584479347507,
    "synchronousValidation": {
        "status": "pass"
    }
}
```

| 屬性 | 說明 |
| -------- | ----------- |
| `{CONNECTION_ID}` | 先前建立之串流連線的ID。 |
| `xactionId` | 唯一識別碼是您剛傳送之記錄的伺服器端產生。 此ID有助於Adobe通過各種系統和調試跟蹤此記錄的生命週期。 |
| `receivedTimeMs` | 時間戳記（以毫秒為單位），顯示收到請求的時間。 |
| `synchronousValidation.status` | 由於已添加查詢參數`synchronousValidation=true`，因此將顯示此值。 如果驗證成功，狀態將為`pass`。 |

## 擷取新收錄的記錄資料

要驗證以前提取的記錄，可以使用[[!DNL Profile Access API]](../../profile/api/entities.md)檢索記錄資料。

>[!NOTE]
>
>如果未定義合併策略ID且`schema.name`或`relatedSchema.name`為`_xdm.context.profile`,[!DNL Profile Access]將獲取&#x200B;**所有**&#x200B;相關身份。

**API格式**

```http
GET /access/entities
GET /access/entities?{QUERY_PARAMETERS}
GET /access/entities?schema.name=_xdm.context.profile&entityId=janedoe@example.com&entityIdNS=email
```

| 參數 | 說明 |
| --------- | ----------- |
| `schema.name` | **必填。** 您正在訪問的架構的名稱。 |
| `entityId` | 實體的ID。 如果提供，您也必須提供實體名稱空間。 |
| `entityIdNS` | 您嘗試擷取之ID的命名空間。 |

**要求**

您可以使用下列GET請求來檢閱先前收錄的記錄資料。

```shell
curl -X GET 'https://platform.adobe.io/data/core/ups/access/entities?schema.name=_xdm.context.profile&entityId=janedoe@example.com&entityIdNS=email'\
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應會傳回HTTP狀態200，並包含所請求之實體的詳細資訊。 如您所見，這是先前成功攝取的相同記錄。

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

閱讀本檔案，您現在就瞭解如何使用串流連線將記錄資料內嵌至[!DNL Platform]。 您可以嘗試使用不同值進行更多呼叫並擷取更新的值。 此外，您還可以透過[!DNL Platform] UI開始監控所擷取的資料。 如需詳細資訊，請閱讀[監控資料擷取](../quality/monitor-data-ingestion.md)指南。

有關串流擷取的詳細資訊，請閱讀[串流擷取概觀](../streaming-ingestion/overview.md)。
