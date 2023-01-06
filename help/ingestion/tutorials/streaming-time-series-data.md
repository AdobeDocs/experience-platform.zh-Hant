---
keywords: Experience Platform；首頁；熱門主題；串流內嵌；內嵌；時間序列資料；串流時間序列資料；
solution: Experience Platform
title: 使用串流獲取API串流時間序列資料
type: Tutorial
description: 本教學課程將協助您開始使用Adobe Experience Platform資料擷取服務API中的串流擷取API。
exl-id: 720b15ea-217c-4c13-b68f-41d17b54d500
source-git-commit: e802932dea38ebbca8de012a4d285eab691231be
workflow-type: tm+mt
source-wordcount: '1204'
ht-degree: 2%

---

# 使用串流獲取API串流時間序列資料

本教學課程將協助您開始使用Adobe Experience Platform中的串流獲取API [!DNL Data Ingestion Service] API。

## 快速入門

本教學課程需具備各種Adobe Experience Platform服務的工作知識。 開始本教學課程之前，請先檢閱下列服務的檔案：

- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md):標準化框架 [!DNL Platform] 組織體驗資料。
- [[!DNL Real-Time Customer Profile]](../../profile/home.md):根據來自多個來源的匯總資料，即時提供統一的消費者設定檔。
- [Schema Registry開發人員指南](../../xdm/api/getting-started.md):涵蓋以下各個可用端點的完整指南 [!DNL Schema Registry] API及如何對其進行呼叫。 這包括了解您的 `{TENANT_ID}`，且會了解如何建立結構描述（用於建立資料集以擷取），此功能會顯示於本教學課程的呼叫中。

此外，本教學課程需要您已建立串流連線。 如需建立串流連線的詳細資訊，請參閱 [建立串流連線教學課程](./create-streaming-connection.md).

### 使用平台API

如需如何成功呼叫Platform API的詳細資訊，請參閱 [Platform API快速入門](../../landing/api-guide.md).

## 根據XDM ExperienceEvent類別撰寫結構

若要建立資料集，您必須先建立實作的新結構 [!DNL XDM ExperienceEvent] 類別。 如需如何建立結構的詳細資訊，請參閱 [Schema Registry API開發人員指南](../../xdm/api/getting-started.md).

**API格式**

```http
POST /schemaregistry/tenant/schemas
```

**要求**

```shell
curl -X POST https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "type": "object",
    "title": "{SCHEMA_NAME}",
    "description": "{SCHEMA_DESCRIPTION}",
    "allOf": [
        {
            "$ref": "https://ns.adobe.com/xdm/context/experienceevent"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/experienceevent-environment-details"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/experienceevent-commerce"
        },
        {  
         "$ref":"https://ns.adobe.com/experience/campaign/experienceevent-profile-work-details"
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
    "version": "1",
    "type": "object",
    "title": "{SCHEMA_NAME}",
    "description": "{SCHEMA_DESCRIPTION}",
    "allOf": [
        {
            "$ref": "https://ns.adobe.com/xdm/context/experienceevent",
            "type": "object",
            "meta:xdmType": "object"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/experienceevent-environment-details",
            "type": "object",
            "meta:xdmType": "object"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/experienceevent-commerce",
            "type": "object",
            "meta:xdmType": "object"
        },
        {
            "$ref": "https://ns.adobe.com/experience/campaign/experienceevent-profile-work-details",
            "type": "object",
            "meta:xdmType": "object"
        }
    ],
    "refs": [
        "https://ns.adobe.com/xdm/context/experienceevent-commerce",
        "https://ns.adobe.com/experience/campaign/experienceevent-profile-work-details",
        "https://ns.adobe.com/xdm/context/experienceevent-environment-details",
        "https://ns.adobe.com/xdm/context/experienceevent"
    ],
    "imsOrg": "{ORG_ID}",
    "meta:immutableTags": [
        "union"
    ],
    "meta:class": "https://ns.adobe.com/xdm/context/experienceevent",
    "required": [
        "@id",
        "xdm:timestamp"
    ],
    "meta:abstract": false,
    "meta:extensible": false,
    "meta:extends": [
        "https://ns.adobe.com/xdm/context/experienceevent",
        "https://ns.adobe.com/xdm/data/time-series",
        "https://ns.adobe.com/xdm/context/identitymap",
        "https://ns.adobe.com/xdm/context/experienceevent-environment-details",
        "https://ns.adobe.com/xdm/context/experienceevent-commerce",
        "https://ns.adobe.com/experience/campaign/experienceevent-profile-work-details"
    ],
    "meta:containerId": "tenant",
    "imsOrg": "{ORG_ID}",
    "meta:xdmType": "object",
    "meta:class": "https://ns.adobe.com/xdm/context/experienceevent",
    "meta:registryMetadata": {
        "repo:createDate": 1551229957987,
        "repo:lastModifiedDate": 1551229957987,
        "xdm:createdClientId": "{CLIENT_ID}",
        "xdm:repositoryCreatedBy": "{CREATED_BY}"
    },
    "meta:tenantNamespace": "{NAMESPACE}"
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
    "xdm:sourceProperty":"/_experience/campaign/message/profileSnapshot/workEmail/address",
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
>&#x200B;**身分命名空間代碼**
>
> 請確定程式碼有效 — 上述範例使用「電子郵件」（標準身分命名空間）。 您可在 [Identity Service常見問題集](../../identity-service/troubleshooting-guide.md#what-are-the-standard-identity-namespaces-provided-by-experience-platform).
>
> 如果您想要建立自訂命名空間，請依照 [身分命名空間概述](../../identity-service/home.md).

**回應**

成功的回應會傳回HTTP狀態201，其中包含新建立之架構主要身分命名空間的相關資訊。

```json
{
    "xdm:property": "xdm:code",
    "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
    "xdm:namespace": "Email",
    "@type": "xdm:descriptorIdentity",
    "xdm:sourceVersion": 1,
    "xdm:isPrimary": true,
    "xdm:sourceProperty": "/_experience/campaign/message/profileSnapshot/workEmail/address",
    "@id": "ec31c09e0906561861be5a71fcd964e29ebe7923b8eb0d1e",
    "meta:containerId": "tenant",
    "version": "1",
    "imsOrg": "{ORG_ID}"
}
```

## 為時間序列資料建立資料集

建立結構後，您需要建立資料集以內嵌記錄資料。

>[!NOTE]
>
>此資料集將啟用 **[!DNL Real-Time Customer Profile]** 和 **[!DNL Identity]** 來設定適當的標籤。

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
  -d '{
    "name": "{DATASET_NAME}",
    "description": "{DATASET_DESCRIPTION}",
    "schemaRef": {
        "id": "{SCHEMA_REF_ID}",
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
    "@/dataSets/5e72608b10f6e318ad2dee0f"
]
```


## 建立串流連線

建立結構和資料集後，您需要建立串流連線才能內嵌資料。

如需建立串流連線的詳細資訊，請參閱 [建立串流連線教學課程](./create-streaming-connection.md).

## 將時間序列資料內嵌至串流連線

建立資料集、串流連線和資料流後，您可以內嵌XDM格式的JSON記錄，以內嵌時間序列資料 [!DNL Platform].

**API格式**

```http
POST /collection/{CONNECTION_ID}?syncValidation=true
```

| 參數 | 說明 |
| --------- | ----------- |
| `{CONNECTION_ID}` | 此 `id` 新建立串流連線的值。 |
| `syncValidation` | 供開發使用的選用查詢參數。 若設為 `true`，可用於立即回饋，以判斷要求是否成功傳送。 此值預設為 `false`. 請注意，若您將此查詢參數設為 `true` 要求的費率限制為每分鐘60次 `CONNECTION_ID`. |

**要求**

使用或不使用來源名稱，即可將時間序列資料擷取至串流連線。

以下範例要求將缺少來源名稱的時間序列資料內嵌至Platform。 如果資料缺少來源名稱，則會從串流連線定義新增來源ID。

兩者 `xdmEntity._id` 和 `xdmEntity.timestamp` 是時間序列資料的必填欄位。 此 `xdmEntity._id` 屬性表示記錄本身的唯一標識符， **not** 記錄所在之人員或裝置的唯一ID。

您需要自行產生 `xdmEntity._id` 和 `xdmEntity.timestamp` 如果需要重新獲取記錄，記錄將保持一致。 理想情況下，源系統將包含這些值。 如果ID不可用，請考慮串連記錄中其他欄位的值，以建立唯一值，該唯一值可在重新擷取時從記錄一致地重新產生。

>[!NOTE]
>
>下列API呼叫會執行 **not** 需要任何驗證標題。

```shell
curl -X POST https://dcs.adobedc.net/collection/{CONNECTION_ID}?syncValidation=true \
  -H "Content-Type: application/json" \
  -d '{
    "header": {
        "schemaRef": {
            "id": "{SCHEMA_REF_ID}",
            "contentType": "application/vnd.adobe.xed-full+json;version=1"
        },
        "flowId": "{FLOW_ID}",
        "datasetId": "{DATASET_ID}"
    },
    "body": {
        "xdmMeta": {
            "schemaRef": {
                "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
                "contentType": "application/vnd.adobe.xed-full+json;version=1"
            },
        "identityMap": {
                "Email": [
                  {
                    "id": "acme_user@gmail.com",
                    "primary": true
                  }
                ]
              },
        },
        "xdmEntity":{
            "_id": "9af5adcc-db9c-4692-b826-65d3abe68c22",
            "timestamp": "2019-02-23T22:07:01Z",
            "environment": {
                "browserDetails": {
                    "userAgent": "Mozilla\/5.0 (Windows NT 5.1) AppleWebKit\/537.36 (KHTML, like Gecko) Chrome\/29.0.1547.57 Safari\/537.36 OPR\/16.0.1196.62",
                    "acceptLanguage": "en-US",
                    "cookiesEnabled": true,
                    "javaScriptVersion": "1.6",
                    "javaEnabled": true
                },
                "colorDepth": 32,
                "viewportHeight": 799,
                "viewportWidth": 414
            },
            "productListItems": [
                {
                    "SKU": "CC",
                    "name": "Fernie Snow",
                    "quantity": 30,
                    "priceTotal": 7.8
                }
            ],
            "commerce": {
                "productViews": {
                    "value": 1
                }
            },
            "_experience": {
                "campaign": {
                    "message": {
                        "profileSnapshot": {
                            "workEmail":{
                                "address": "janedoe@example.com"
                            }
                        }
                    }
                }
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
| `{CONNECTION_ID}` | 此 `inletId` 之前建立的串流連線。 |
| `xactionId` | 在伺服器端為您剛傳送的記錄產生唯一識別碼。 此ID有助於Adobe通過各種系統和調試跟蹤此記錄的生命週期。 |
| `receivedTimeMs`:顯示接收請求的時間的時間戳記（以毫秒為單位）。 |
| `syncValidation.status` | 由於查詢參數 `syncValidation=true` 新增後，此值就會出現。 如果驗證成功，狀態將為 `pass`. |

## 擷取新擷取的時間序列資料

若要驗證先前擷取的記錄，您可以使用 [[!DNL Profile Access API]](../../profile/api/entities.md) 來擷取時間序列資料。 您可以使用GET要求來完成 `/access/entities` 端點和使用選用的查詢參數。 可使用多個參數，以&amp;符號分隔。&quot;

>[!NOTE]
>
>如果未定義合併策略ID，則 `schema.name` 或 `relatedSchema.name` is `_xdm.context.profile`, [!DNL Profile Access] 將擷取 **all** 相關身分。

**API格式**

```http
GET /access/entities
GET /access/entities?{QUERY_PARAMETERS}
GET /access/entities?schema.name=_xdm.context.experienceevent&relatedSchema.name=_xdm.context.profile&relatedEntityId=janedoe@example.com&relatedEntityIdNS=email
```

| 參數 | 說明 |
| --------- | ----------- |
| `schema.name` | **必填。** 您正在存取的架構的名稱。 |
| `relatedSchema.name` | **必填。** 由於您要存取 `_xdm.context.experienceevent`，此值會指定與時間序列事件相關的設定檔實體的架構。 |
| `relatedEntityId` | 相關實體的ID。 若有提供，您也必須提供實體命名空間。 |
| `relatedEntityIdNS` | 您嘗試擷取之ID的命名空間。 |

**要求**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/access/entities?schema.name=_xdm.context.experienceevent&relatedSchema.name=_xdm.context.profile&relatedEntityId=janedoe@example.com&relatedEntityIdNS=email \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "x-sandbox-name: {SANDBOX_NAME}"
```

**回應**

成功的回應會傳回HTTP狀態200，並包含所請求實體的詳細資訊。 如您所見，這與先前擷取的時間序列資料相同。

```json
{
    "_page": {
        "orderby": "timestamp",
        "start": "9af5adcc-db9c-4692-b826-65d3abe68c22",
        "count": 1,
        "next": ""
    },
    "children": [
        {
            "relatedEntityId": "BVrqzwVv7o2p3naHvnsWpqZXv3KJgA",
            "entityId": "9af5adcc-db9c-4692-b826-65d3abe68c22",
            "timestamp": 1582495621000,
            "entity": {
                "environment": {
                    "browserDetails": {
                        "javaScriptVersion": "1.6",
                        "cookiesEnabled": true,
                        "userAgent": "Mozilla/5.0 (Windows NT 5.1) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/29.0.1547.57 Safari/537.36 OPR/16.0.1196.62",
                        "acceptLanguage": "en-US",
                        "javaEnabled": true
                    },
                    "colorDepth": 32,
                    "viewportHeight": 799,
                    "viewportWidth": 414
                },
                "_id": "9af5adcc-db9c-4692-b826-65d3abe68c22",
                "commerce": {
                    "productViews": {
                        "value": 1
                    }
                },
                "productListItems": [
                    {
                        "name": "Fernie Snow",
                        "quantity": 30,
                        "SKU": "CC",
                        "priceTotal": 7.8
                    }
                ],
                "_experience": {
                    "campaign": {
                        "message": {
                            "profileSnapshot": {
                                "workEmail": {
                                    "address": "janedoe@example.com"
                                }
                            }
                        }
                    }
                },
                "timestamp": "2020-02-23T22:07:01Z"
            },
            "lastModifiedAt": "2020-03-18T18:51:19Z"
        }
    ],
    "_links": {
        "next": {
            "href": ""
        }
    }
}
```

## 後續步驟

閱讀本檔案後，您現在就能了解如何將記錄資料內嵌至 [!DNL Platform] 使用串流連線。 您可以嘗試使用不同值進行更多呼叫並擷取更新的值。 此外，您也可以透過 [!DNL Platform] UI。 欲知更多資訊，請閱讀 [監控資料擷取](../quality/monitor-data-ingestion.md) 指南。

如需串流獲取的詳細資訊，請參閱 [串流獲取概觀](../streaming-ingestion/overview.md).
