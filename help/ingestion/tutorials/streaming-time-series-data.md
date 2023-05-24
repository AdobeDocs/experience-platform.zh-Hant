---
keywords: Experience Platform；主題；熱門主題；流攝入；接收；時間序列；流時間序列；
solution: Experience Platform
title: 利用流接收APIs流時間序列資料
type: Tutorial
description: 本教程將幫助您開始使用流接收API，這是Adobe Experience Platform資料接收服務API的一部分。
exl-id: 720b15ea-217c-4c13-b68f-41d17b54d500
source-git-commit: 81f48de908b274d836f551bec5693de13c5edaf1
workflow-type: tm+mt
source-wordcount: '1203'
ht-degree: 2%

---

# 使用流接收API流時間序列資料

本教程將幫助您開始使用流接收API，這是Adobe Experience Platform的一部分 [!DNL Data Ingestion Service] API。

## 快速入門

本教程需要瞭解Adobe Experience Platform各項服務的工作知識。 在開始本教程之前，請查看以下服務的文檔：

- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md):標準化框架 [!DNL Platform] 組織經驗資料。
- [[!DNL Real-Time Customer Profile]](../../profile/home.md):根據來自多個源的聚合資料即時提供統一的消費者配置檔案。
- [架構註冊表開發人員指南](../../xdm/api/getting-started.md):一個全面的指南，它涵蓋了 [!DNL Schema Registry] API以及如何調用它們。 這包括瞭解 `{TENANT_ID}`，在本教程的調用中顯示，並瞭解如何建立架構，用於建立用於接收的資料集。

此外，本教程要求您已經建立了流連接。 有關建立流連接的詳細資訊，請閱讀 [建立流連接教程](./create-streaming-connection.md)。

### 使用平台API

有關如何成功調用平台API的資訊，請參見上的指南 [平台API入門](../../landing/api-guide.md)。

## 基於XDM ExperienceEvent類編寫架構

要建立資料集，您首先需要建立一個新架構來實現 [!DNL XDM ExperienceEvent] 類。 有關如何建立架構的詳細資訊，請閱讀 [架構註冊API開發人員指南](../../xdm/api/getting-started.md)。

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
| `{SCHEMA_REF_ID}` | 的 `$id` 構建架構時收到的。 它應該是這樣的： `"https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}"` |

>[!NOTE]
>
>&#x200B;**標識名稱空間代碼**
>
> 請確保代碼有效 — 上面的示例使用「email」，它是標準標識命名空間。 在 [Identity Service常見問題](../../identity-service/troubleshooting-guide.md#what-are-the-standard-identity-namespaces-provided-by-experience-platform)。
>
> 如果要建立自定義命名空間，請執行中介紹的步驟 [標識命名空間概述](../../identity-service/home.md)。

**回應**

成功的響應返回HTTP狀態201，其中包含有關新建立的架構主標識命名空間的資訊。

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

建立架構後，需要建立資料集以接收記錄資料。

>[!NOTE]
>
>將為 **[!DNL Real-Time Customer Profile]** 和 **[!DNL Identity]** 設定相應的標籤。

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

成功的響應返回HTTP狀態201和包含以格式新建立的資料集ID的陣列 `@/dataSets/{DATASET_ID}`。

```json
[
    "@/dataSets/5e72608b10f6e318ad2dee0f"
]
```


## 建立流連接

在建立模式和資料集後，您需要建立流連接以接收資料。

有關建立流連接的詳細資訊，請閱讀 [建立流連接教程](./create-streaming-connection.md)。

## 將時間序列資料接收到流連接

建立資料集、流連接和資料流後，您可以接收XDM格式的JSON記錄，以接收內的時間序列資料 [!DNL Platform]。

**API格式**

```http
POST /collection/{CONNECTION_ID}?syncValidation=true
```

| 參數 | 說明 |
| --------- | ----------- |
| `{CONNECTION_ID}` | 的 `id` 新建立的流連接的值。 |
| `syncValidation` | 用於開發目的的可選查詢參數。 如果設定為 `true`，它可用於立即反饋以確定請求是否成功發送。 預設情況下，此值設定為 `false`。 請注意，如果將此查詢參數設定為 `true` 請求的速率將限制為每分鐘60次 `CONNECTION_ID`。 |

**要求**

將時間序列資料插入流連接可以使用或不使用源名稱。

下面的示例請求將缺少源名稱的時間序列資料接收到平台。 如果資料缺少源名稱，它將從流連接定義中添加源ID。

兩者 `xdmEntity._id` 和 `xdmEntity.timestamp` 是時間系列資料的必填欄位。 的 `xdmEntity._id` 屬性表示記錄本身的唯一標識符， **不** 記錄其的個人或設備的唯一ID。

您需要生成自己的 `xdmEntity._id` 和 `xdmEntity.timestamp` 如果記錄需要重新攝入，則記錄將保持一致。 理想情況下，源系統將包含這些值。 如果ID不可用，請考慮將記錄中其他欄位的值連接起來，以建立一個唯一值，該值可以在重新攝取時從記錄中一致地重新生成。

>[!NOTE]
>
>以下API調用 **不** 需要任何身份驗證標頭。

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

成功的響應返回HTTP狀態200，其中包含新流式傳輸的詳細資訊 [!DNL Profile]。

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
| `{CONNECTION_ID}` | 的 `inletId` 以前建立的流連接。 |
| `xactionId` | 為您剛發送的記錄生成的唯一標識符伺服器端。 此ID有助於Adobe通過各種系統和調試跟蹤此記錄的生命週期。 |
| `receivedTimeMs`:顯示接收請求的時間的時間戳（以毫秒為單位）。 |
| `syncValidation.status` | 自查詢參數 `syncValidation=true` 添加後，此值將出現。 如果驗證成功，則狀態將為 `pass`。 |

## 檢索新攝取的時間序列資料

要驗證以前攝取的記錄，可以使用 [[!DNL Profile Access API]](../../profile/api/entities.md) 的子菜單。 可以使用GET請求 `/access/entities` 終結點和使用可選查詢參數。 可以使用多個參數，用和符號(&amp;)分隔。&quot;

>[!NOTE]
>
>如果未定義合併策略ID, `schema.name` 或 `relatedSchema.name` 是 `_xdm.context.profile`。 [!DNL Profile Access] 將 **全部** 相關身份。

**API格式**

```http
GET /access/entities
GET /access/entities?{QUERY_PARAMETERS}
GET /access/entities?schema.name=_xdm.context.experienceevent&relatedSchema.name=_xdm.context.profile&relatedEntityId=janedoe@example.com&relatedEntityIdNS=email
```

| 參數 | 說明 |
| --------- | ----------- |
| `schema.name` | **必填。** 正在訪問的架構的名稱。 |
| `relatedSchema.name` | **必填。** 因為您訪問 `_xdm.context.experienceevent`，此值指定與時間系列事件相關的配置檔案實體的架構。 |
| `relatedEntityId` | 相關實體的ID。 如果提供，則還必須提供實體命名空間。 |
| `relatedEntityIdNS` | 您嘗試檢索的ID的命名空間。 |

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

成功響應返回HTTP狀態200，並返回所請求實體的詳細資訊。 正如您所看到的，這是以前攝取的相同時間序列資料。

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

通過閱讀此文檔，您現在瞭解如何將記錄資料 [!DNL Platform] 使用流連接。 您可以嘗試使用不同的值進行更多調用並檢索更新的值。 此外，您還可以通過 [!DNL Platform] UI。 有關詳細資訊，請閱讀 [監控資料接收](../quality/monitor-data-ingestion.md) 的子菜單。

有關流式接收的詳細資訊，請閱讀 [流式處理概述](../streaming-ingestion/overview.md)。
