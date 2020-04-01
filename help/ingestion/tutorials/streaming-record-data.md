---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 串流記錄資料
topic: tutorial
translation-type: tm+mt
source-git-commit: 79466c78fd78c0f99f198b11a9117c946736f47a

---


# 串流記錄資料至Adobe Experience Platform

本教學課程將協助您開始使用串流擷取API，這是Adobe Experience Platform Data Ingestion Service API的一部分。

## 快速入門

本教學課程需要具備各種Adobe Experience Platform服務的相關知識。 在開始本教學課程之前，請先閱讀下列服務的檔案：

- [體驗資料模型(XDM)](../../xdm/home.md):平台組織體驗資料的標準化架構。
- [即時客戶個人檔案](../../profile/home.md):根據來自多個來源的匯整資料，即時提供統一的消費者個人檔案。
- [架構註冊開發人員指南](../../xdm/api/getting-started.md):完整的指南，涵蓋架構註冊表API的每個可用端點，以及如何對其進行呼叫。 這包括瞭解您 `{TENANT_ID}`的資料集（在本教學課程的呼叫中顯示），以及瞭解如何建立結構描述（用於建立資料集以擷取）。

此外，本教學課程要求您已建立串流連線。 如需建立串流連線的詳細資訊，請閱讀建立串 [流連線教學課程](./create-streaming-connection.md)。

以下章節提供您需要知道的其他資訊，以便成功呼叫串流擷取API。

### 讀取範例API呼叫

本指南提供範例API呼叫，以示範如何格式化您的請求。 這些包括路徑、必要標題和正確格式化的請求負載。 也提供API回應中傳回的範例JSON。 如需範例API呼叫檔案中所用慣例的詳細資訊，請參閱「Experience Platform疑難排解指 [南」中有關如何讀取範例API呼叫的章節](../../landing/troubleshooting.md#how-do-i-format-an-api-request) 。

### 收集必要標題的值

若要呼叫平台API，您必須先完成驗證教 [學課程](../../tutorials/authentication.md)。 完成驗證教學課程後，所有Experience Platform API呼叫中每個必要標題的值都會顯示在下方：

- 授權：生產者 `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Experience Platform中的所有資源都隔離至特定的虛擬沙盒。 所有對平台API的請求都需要一個標題，該標題會指定要在中執行的操作的沙盒名稱：

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE] 如需平台中沙盒的詳細資訊，請參閱沙盒 [概觀檔案](../../sandboxes/home.md)。

所有包含裝載(POST、PUT、PATCH)的請求都需要額外的標題：

- 內容類型：application/json

## 基於XDM單個配置檔案類合成方案

若要建立資料集，您首先需要建立新的架構，以實作XDM個別描述檔類別。 如需如何建立結構描述的詳細資訊，請閱讀「結構描述注 [冊表API開發人員指南」](../../xdm/api/getting-started.md)。

**API格式**

```http
POST /schemaregistry/tenant/schemas
```

**請求**

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
| `meta:immutableTags` | 在此範例中，標 `union` 記會用來將您的資料保存 [在即時客戶個人檔案中](../../profile/home.md)。 |

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
| `{TENANT_ID}` | 此ID可用來確保您建立的資源已正確命名並包含在IMS組織中。 如需租用戶ID的詳細資訊，請閱讀架 [構註冊指南](../../xdm/api/getting-started.md#know-your-tenant-id)。 |

請注意屬性 `$id` 和屬性，因 `version` 為在建立資料集時，會使用這兩個屬性。

## 為方案設定主標識描述符

接著，使用工 [作電子郵件地址屬性作為主要標識符](../../xdm/api/descriptors.md) ，將身份描述符添加到上面建立的架構中。 這樣做會產生兩項變更：

1. 工作電子郵件地址將成為必填欄位。 這表示未使用此欄位傳送的訊息將無法驗證，且不會被收錄。

2. 即時客戶個人檔案會使用工作電子郵件地址做為識別碼，協助拼湊更多有關該個人的資訊。

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
| `{SCHEMA_REF_ID}` | 構 `$id` 成架構時先前收到的。 它應該看起來像這樣： `"https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}"` |

>[!NOTE] 識&#x200B;&#x200B;別名稱空間代碼&#x200B;****
>
> 請確定代碼有效——上述範例使用「電子郵件」，此為標準身分命名空間。 其他常用的標準身分名稱空間可在 [Identity Service常見問答集中找到](../../identity-service/troubleshooting-guide.md#what-are-the-standard-identity-namespaces-provided-by-experience-platform)。
>
> 如果您想要建立自訂命名空間，請依照識別命名空間概述中 [的步驟](../../identity-service/home.md)。

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

>[!NOTE] 此資料集將啟用「即 **時客戶設定檔** 」 **和「身分服務」**。

**API格式**

```http
POST /catalog/dataSets
```

**請求**

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
        "contentType": "application/vnd.adobe.xed-full+json;version=1.0"
    },
    "tags": {
        "unifiedIdentity": ["enabled:true"],
        "unifiedProfile": ["enabled:true"]
    }
}'
```

**回應**

成功的回應會傳回HTTP狀態201，並傳回包含新建立之資料集ID的格式陣列 `@/dataSets/{DATASET_ID}`。

```json
[
    "@/dataSets/5e30d7986c0cc218a85cee65
]
```

## 將記錄資料內嵌至串流連線

有了資料集和串流連線，您就可以內嵌XDM格式的JSON記錄，以便將記錄資料內嵌至平台。

**API格式**

```http
POST /collection/{CONNECTION_ID}?synchronousValidation=true
```

| 參數 | 說明 |
| --------- | ----------- |
| `{CONNECTION_ID}` | 先前 `id` 建立的串流連線值。 |
| `synchronousValidation` | 可選的查詢參數，用於開發用途。 如果設為 `true`，則可用來立即回饋，以判斷請求是否成功傳送。 依預設，此值會設為 `false`。 |

**請求**

>[!NOTE] 下列API呼叫不需 **要** 任何驗證標題。

```shell
curl -X POST https://dcs.adobedc.net/collection/{CONNECTION_ID}?synchronousValidation=true \
  -H "Cache-Control: no-cache" \
  -H "Content-Type: application/json" \
  -d '{
    "header": {
        "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
            "contentType": "application/vnd.adobe.xed-full+json;version={SCHEMA_VERSION}"
        },
        "imsOrgId": "{IMS_ORG}",
        "source": {
            "name": "GettingStarted"
        },
        "datasetId": "{DATASET_ID}"
    },
    "body": {
        "xdmMeta": {
            "schemaRef": {
                "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
                "contentType": "application/vnd.adobe.xed-full+json;version={SCHEMA_VERSION}"
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

**回應**

成功的回應會傳回HTTP狀態200，並包含新串流描述檔的詳細資訊。

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
| `xactionId` | 唯一識別碼是您剛傳送之記錄的伺服器端產生。 此ID可協助Adobe透過各種系統及除錯來追蹤此記錄的生命週期。 |
| `receivedTimeMs` | 時間戳記（以毫秒為單位），顯示收到請求的時間。 |
| `synchronousValidation.status` | 由於已新增查 `synchronousValidation=true` 詢參數，因此會顯示此值。 如果驗證成功，則狀態為 `pass`。 |

## 擷取新收錄的記錄資料

若要驗證先前擷取的記錄，您可以使用描述檔 [存取API](../../profile/api/entities.md) ，擷取記錄資料。

>[!NOTE] 如果未定義合併策略ID和架構。</span>name或relatedSchema</span>.name為 `_xdm.context.profile`，描述檔存取會擷取所 **有相關** 的身分。

**API格式**

```http
GET /access/entities
GET /access/entities?{QUERY_PARAMETERS}
GET /access/entities?schema.name=_xdm.context.profile&entityId=janedoe@example.com&entityIdNS=email
```

| 參數 | 說明 |
| --------- | ----------- |
| `schema.name` | **必填.** 您正在訪問的架構的名稱。 |
| `entityId` | 實體的ID。 如果提供，您也必須提供實體名稱空間。 |
| `entityIdNS` | 您嘗試擷取之ID的命名空間。 |

**請求**

您可以使用下列GET請求來檢閱先前擷取的記錄資料。

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

閱讀本檔案，您現在就瞭解如何使用串流連線將錄制資料內嵌至平台。 您可以嘗試使用不同值進行更多呼叫並擷取更新的值。 此外，您還可以透過平台UI開始監控所擷取的資料。 如需詳細資訊，請閱讀監控資 [料擷取指南](../quality/monitor-data-flows.md) 。

如需串流擷取的詳細資訊，請閱讀串流擷取 [概觀](../streaming-ingestion/overview.md)。


