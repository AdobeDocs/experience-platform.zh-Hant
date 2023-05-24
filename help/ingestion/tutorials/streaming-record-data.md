---
keywords: Experience Platform；主題；熱門主題；流攝入；接收；記錄資料；流記錄資料；
solution: Experience Platform
title: 使用流接收API的流記錄資料
type: Tutorial
description: 本教程將幫助您開始使用流接收API，這是Adobe Experience Platform資料接收服務API的一部分。
exl-id: 097dfd5a-4e74-430d-8a12-cac11b1603aa
source-git-commit: 81f48de908b274d836f551bec5693de13c5edaf1
workflow-type: tm+mt
source-wordcount: '1024'
ht-degree: 2%

---


# 使用流接收API的流記錄資料

本教程將幫助您開始使用流接收API，這是Adobe Experience Platform的一部分 [!DNL Data Ingestion Service] API。

## 快速入門

本教程需要瞭解Adobe Experience Platform各項服務的工作知識。 在開始本教程之前，請查看以下服務的文檔：

- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md):標準化框架 [!DNL Platform] 組織經驗資料。
   - [架構註冊表開發人員指南](../../xdm/api/getting-started.md):一個全面的指南，它涵蓋了 [!DNL Schema Registry] API以及如何調用它們。 這包括瞭解 `{TENANT_ID}`，在本教程的調用中顯示，並瞭解如何建立架構，用於建立用於接收的資料集。
- [[!DNL Real-Time Customer Profile]](../../profile/home.md):根據來自多個源的聚合資料即時提供統一的消費者配置檔案。

### 使用平台API

有關如何成功調用平台API的資訊，請參見上的指南 [平台API入門](../../landing/api-guide.md)。

## 基於 [!DNL XDM Individual Profile] 類

要建立資料集，您首先需要建立一個新架構來實現 [!DNL XDM Individual Profile] 類。 有關如何建立架構的詳細資訊，請閱讀 [架構註冊API開發人員指南](../../xdm/api/getting-started.md)。

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
| `title` | 要用於架構的名稱。 此名稱必須唯一。 |
| `description` | 正在建立的架構的有意義說明。 |
| `meta:immutableTags` | 在此示例中， `union` 標籤用於將資料保留到 [[!DNL Real-Time Customer Profile]](../../profile/home.md)。 |

**回應**

成功的響應返回HTTP狀態201，其中包含新建立架構的詳細資訊。

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
| `{TENANT_ID}` | 此ID用於確保您建立的資源與組織中的資源同名並包含在組織中。 有關租戶ID的詳細資訊，請閱讀 [架構註冊表指南](../../xdm/api/getting-started.md#know-your-tenant-id)。 |

請注意 `$id` 以及 `version` 屬性，因為建立資料集時將使用這兩個屬性。

## 為架構設定主標識描述符

下一步，添加 [標識符](../../xdm/api/descriptors.md) 使用工作電子郵件地址屬性作為主標識符。 這樣做將導致兩項更改：

1. 工作電子郵件地址將成為必填欄位。 這表示未使用此欄位發送的消息將驗證失敗，不會被接收。

2. [!DNL Real-Time Customer Profile] 將使用工作電子郵件地址作為標識符，幫助拼湊有關該個人的更多資訊。

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
| `{SCHEMA_REF_ID}` | 的 `$id` 構建架構時收到的。 它應該是這樣的： `"https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}"` |

>[!NOTE]
>
>&#x200B;&#x200B;**標識名稱空間代碼**
>
> 請確保代碼有效 — 上面的示例使用「email」，它是標準標識命名空間。 在 [Identity Service常見問題](../../identity-service/troubleshooting-guide.md#what-are-the-standard-identity-namespaces-provided-by-experience-platform)。
>
> 如果要建立自定義命名空間，請執行中介紹的步驟 [標識命名空間概述](../../identity-service/home.md)。

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
    "imsOrg": "{ORG_ID}"
}
```

## 為記錄資料建立資料集

建立架構後，需要建立資料集以接收記錄資料。

>[!NOTE]
>
>將為 **[!DNL Real-Time Customer Profile]** 和 **[!DNL Identity Service]**。

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

成功的響應返回HTTP狀態201和包含以格式新建立的資料集ID的陣列 `@/dataSets/{DATASET_ID}`。

```json
[
    "@/dataSets/5e30d7986c0cc218a85cee65
]
```

## 建立流連接

建立架構和資料集後，可以建立流連接

有關建立流連接的詳細資訊，請閱讀 [建立流連接教程](./create-streaming-connection.md)。

## 將記錄資料接收到流連接 {#ingest-data}

在資料集和流連接就位後，您可以將XDM格式的JSON記錄接收到 [!DNL Platform]。

**API格式**

```http
POST /collection/{CONNECTION_ID}?syncValidation=true
```

| 參數 | 說明 |
| --------- | ----------- |
| `{CONNECTION_ID}` | 的 `inletId` 先前建立的流連接的值。 |
| `syncValidation` | 用於開發目的的可選查詢參數。 如果設定為 `true`，它可用於立即反饋以確定請求是否成功發送。 預設情況下，此值設定為 `false`。 請注意，如果將此查詢參數設定為 `true` 請求的速率將限制為每分鐘60次 `CONNECTION_ID`。 |

**要求**

將記錄資料接收到流連接可以使用或不使用源名稱。

下面的示例請求將缺少源名稱的記錄接收到平台。 如果記錄缺少源名稱，它將從流連接定義中添加源ID。

>[!NOTE]
>
>以下API調用 **不** 需要任何身份驗證標頭。

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

成功響應返回HTTP狀態200，並返回新流式傳輸的詳細資訊 [!DNL Profile]。

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
| `{CONNECTION_ID}` | 先前建立的流連接的ID。 |
| `xactionId` | 為您剛發送的記錄生成的唯一標識符伺服器端。 此ID有助於Adobe通過各種系統和調試跟蹤此記錄的生命週期。 |
| `receivedTimeMs` | 顯示接收請求的時間的時間戳（以毫秒為單位）。 |
| `syncValidation.status` | 自查詢參數 `syncValidation=true` 添加後，此值將出現。 如果驗證成功，則狀態將為 `pass`。 |

## 檢索新攝取的記錄資料

要驗證以前攝取的記錄，可以使用 [[!DNL Profile Access API]](../../profile/api/entities.md) 以檢索記錄資料。

>[!NOTE]
>
>如果未定義合併策略ID, `schema.name` 或 `relatedSchema.name` 是 `_xdm.context.profile`。 [!DNL Profile Access] 將 **全部** 相關身份。

**API格式**

```http
GET /access/entities
GET /access/entities?{QUERY_PARAMETERS}
GET /access/entities?schema.name=_xdm.context.profile&entityId=janedoe@example.com&entityIdNS=email
```

| 參數 | 說明 |
| --------- | ----------- |
| `schema.name` | **必填。** 正在訪問的架構的名稱。 |
| `entityId` | 實體的ID。 如果提供，則還必須提供實體命名空間。 |
| `entityIdNS` | 您嘗試檢索的ID的命名空間。 |

**要求**

您可以使用以下請求複查以前接收的記錄資料。

```shell
curl -X GET 'https://platform.adobe.io/data/core/ups/access/entities?schema.name=_xdm.context.profile&entityId=janedoe@example.com&entityIdNS=email'\
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功響應返回HTTP狀態200，並返回所請求實體的詳細資訊。 如您所見，這是之前成功攝取的相同記錄。

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

通過閱讀此文檔，您現在瞭解如何將記錄資料 [!DNL Platform] 使用流連接。 您可以嘗試使用不同的值進行更多調用並檢索更新的值。 此外，您還可以通過 [!DNL Platform] UI。 有關詳細資訊，請閱讀 [監控資料接收](../quality/monitor-data-ingestion.md) 的子菜單。

有關流式接收的詳細資訊，請閱讀 [流式處理概述](../streaming-ingestion/overview.md)。
