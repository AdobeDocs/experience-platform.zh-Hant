---
keywords: Experience Platform; home；熱門主題；流處理；提取；時間序列資料；流時間序列資料；
solution: Experience Platform
title: 使用串流擷取API串流時間系列資料
topic-legacy: tutorial
type: Tutorial
description: 本教學課程將協助您開始使用串流擷取API，這是Adobe Experience Platform資料擷取服務API的一部分。
exl-id: 720b15ea-217c-4c13-b68f-41d17b54d500
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1312'
ht-degree: 2%

---

# 使用串流擷取API串流時間系列資料

本教學課程將協助您開始使用串流擷取API，這是Adobe Experience Platform[!DNL Data Ingestion Service] API的一部分。

## 快速入門

本教學課程需要具備Adobe Experience Platform各項服務的相關知識。 在開始本教學課程之前，請先閱讀下列服務的檔案：

- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md):組織體驗資料的 [!DNL Platform] 標準化架構。
- [[!DNL Real-time Customer Profile]](../../profile/home.md):根據來自多個來源的匯整資料，即時提供統一的消費者個人檔案。
- [架構註冊開發人員指南](../../xdm/api/getting-started.md):完整的指南，涵蓋 [!DNL Schema Registry] API的每個可用端點，以及如何呼叫這些端點。這包括瞭解在本教學課程中的呼叫中出現的`{TENANT_ID}`，以及瞭解如何建立結構描述（用於建立資料集以擷取）。

此外，本教學課程要求您已建立串流連線。 有關建立流連接的詳細資訊，請閱讀[建立流連接教程](./create-streaming-connection.md)。

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

## 基於XDM ExperienceEvent類合成模式

若要建立資料集，您必須先建立實作[!DNL XDM ExperienceEvent]類別的新架構。 有關如何建立架構的詳細資訊，請閱讀[Schema Registry API開發人員指南](../../xdm/api/getting-started.md)。

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
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
    "imsOrg": "{IMS_ORG}",
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
    "imsOrg": "{IMS_ORG}",
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
| `{SCHEMA_REF_ID}` | 構建架構時先前收到的`$id`。 它應該看起來像這樣：`"https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}"` |

>[!NOTE]
>
>&#x200B;**Identity Namespace代碼**
>
> 請確定代碼有效——上述範例使用「電子郵件」，此為標準身分命名空間。 其他常用的標準身分名稱空間可在[Identity Service常見問答集](../../identity-service/troubleshooting-guide.md#what-are-the-standard-identity-namespaces-provided-by-experience-platform)中找到。
>
> 如果您想要建立自訂命名空間，請依照[identity namespace overview](../../identity-service/home.md)中所述的步驟進行。

**回應**

成功的回應會傳回HTTP狀態201，其中包含新建立之架構主要身分名稱空間的相關資訊。

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
    "imsOrg": "{IMS_ORG}"
}
```

## 為時間序列資料建立資料集

建立結構後，您需要建立資料集來收錄記錄資料。

>[!NOTE]
>
>透過設定適當的標籤，此資料集將會啟用&#x200B;**[!DNL Real-time Customer Profile]**&#x200B;和&#x200B;**[!DNL Identity]**。

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

成功的回應會傳回HTTP狀態201，並傳回包含以`@/dataSets/{DATASET_ID}`格式新建立資料集ID的陣列。

```json
[
    "@/dataSets/5e72608b10f6e318ad2dee0f"
]
```

## 將時間系列資料收錄至串流連線

有了資料集和串流連線，您就可以內嵌XDM格式的JSON記錄，以內嵌[!DNL Platform]內的時間系列資料。

**API格式**

```http
POST /collection/{CONNECTION_ID}?synchronousValidation=true
```

| 參數 | 說明 |
| --------- | ----------- |
| `{CONNECTION_ID}` | 您新建立的串流連線的`id`值。 |
| `synchronousValidation` | 可選的查詢參數，用於開發用途。 如果設為`true`，則可用於立即回饋，以判斷請求是否成功傳送。 依預設，此值會設為`false`。 |

**要求**

將時間序列資料引入流連接可以使用或不使用源名稱。

以下的範例請求將遺失來源名稱的時間系列資料擷取至平台。 如果資料遺失來源名稱，則會從串流連線定義新增來源ID。

>[!IMPORTANT]
>
>您需要產生自己的`xdmEntity._id`和`xdmEntity.timestamp`。 產生ID的好方法是在「資料準備」中使用UUID函式。 有關UUID函式的詳細資訊，請參閱[資料準備函式指南](../../data-prep/functions.md)。 `xdmEntity._id`屬性代表記錄本身的唯一識別碼，**not**&#x200B;是記錄所在人或裝置的唯一ID。 人員或裝置ID將在指派為架構之人員或裝置識別碼的任何屬性中指定。
>
>`xdmEntity._id`和`xdmEntity.timestamp`都是時間序列資料的唯一必需欄位。 此外，下列API呼叫不需要任何驗證標題。****

```shell
curl -X POST https://dcs.adobedc.net/collection/{CONNECTION_ID}?synchronousValidation=true \
  -H "Content-Type: application/json" \
  -d '{
    "header": {
        "schemaRef": {
            "id": "{SCHEMA_REF_ID}",
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
| `receivedTimeMs`:時間戳記（以毫秒為單位），顯示收到請求的時間。 |
| `synchronousValidation.status` | 由於已添加查詢參數`synchronousValidation=true`，因此將顯示此值。 如果驗證成功，狀態將為`pass`。 |

## 擷取新擷取的時間序列資料

要驗證以前提取的記錄，可以使用[[!DNL Profile Access API]](../../profile/api/entities.md)來檢索時間序列資料。 這可以使用對`/access/entities`端點的GET請求和可選的查詢參數來完成。 可以使用多個參數，由&amp;符號(&amp;)分隔。&quot;

>[!NOTE]
>
>如果未定義合併策略ID且`schema.name`或`relatedSchema.name`為`_xdm.context.profile`,[!DNL Profile Access]將獲取&#x200B;**所有**&#x200B;相關身份。

**API格式**

```http
GET /access/entities
GET /access/entities?{QUERY_PARAMETERS}
GET /access/entities?schema.name=_xdm.context.experienceevent&relatedSchema.name=_xdm.context.profile&relatedEntityId=janedoe@example.com&relatedEntityIdNS=email
```

| 參數 | 說明 |
| --------- | ----------- |
| `schema.name` | **必填。** 您正在訪問的架構的名稱。 |
| `relatedSchema.name` | **必填。** 由於您正在訪問 `_xdm.context.experienceevent`某個，因此此值指定了與時間系列事件相關的概要檔案實體的方案。 |
| `relatedEntityId` | 相關實體的ID。 如果提供，您也必須提供實體名稱空間。 |
| `relatedEntityIdNS` | 您嘗試擷取之ID的命名空間。 |

**要求**

```shell
curl -X GET \
  https://platform-stage.adobe.io/data/core/ups/access/entities?schema.name=_xdm.context.experienceevent&relatedSchema.name=_xdm.context.profile&relatedEntityId=janedoe@example.com&relatedEntityIdNS=email \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "x-sandbox-name: {SANDBOX_NAME}"
```

**回應**

成功的回應會傳回HTTP狀態200，並包含所請求之實體的詳細資訊。 如您所見，這是先前擷取的相同時間系列資料。

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

閱讀本檔案，您現在就瞭解如何使用串流連線將記錄資料內嵌至[!DNL Platform]。 您可以嘗試使用不同值進行更多呼叫並擷取更新的值。 此外，您還可以透過[!DNL Platform] UI開始監控所擷取的資料。 如需詳細資訊，請閱讀[監控資料擷取](../quality/monitor-data-ingestion.md)指南。

有關串流擷取的詳細資訊，請閱讀[串流擷取概觀](../streaming-ingestion/overview.md)。
