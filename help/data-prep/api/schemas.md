---
keywords: Experience Platform；首頁；熱門主題；資料準備；api指南；架構；
solution: Experience Platform
title: 架構API終結點
description: 可以使用Adobe Experience PlatformAPI中的「/schemas」端點以寫程式方式檢索、建立和更新架構，以便與平台中的映射器一起使用。
source-git-commit: 81f48de908b274d836f551bec5693de13c5edaf1
workflow-type: tm+mt
source-wordcount: '611'
ht-degree: 4%

---



# 架構終結點

架構可與映射器一起使用，以確保您在Adobe Experience Platform攝取的資料與您要攝取的資料相匹配。 您可以使用 `/schemas` 終結點，以寫程式方式建立、列出和獲取自定義架構，以便與平台中的映射器一起使用。

>[!NOTE]
>
>使用此終結點建立的架構專用於映射器和映射集。 要建立其他平台服務可訪問的架構，請閱讀 [架構註冊表開發人員指南](../../xdm/api/schemas.md)。

## 獲取所有架構

您可以通過向以下組織發出GET請求來檢索組織的所有可用映射器架構的清單： `/schemas` 端點。

**API格式**

的 `/schemas` 終結點支援多個查詢參數，以幫助您篩選結果。 雖然這些參數大多是可選的，但強烈建議使用這些參數以幫助降低昂貴的開銷。 但是，必須同時包括 `start` 和 `limit` 參數。 可以包括多個參數，用和符號分隔(`&`)。

```http
GET /schemas?limit={LIMIT}&start={START}
GET /schemas?limit={LIMIT}&start={START}&name={NAME}
GET /schemas?limit={LIMIT}&start={START}&orderBy={ORDER_BY}
```

| 參數 | 說明 |
| --------- | ----------- |
| `{LIMIT}` | **必填**. 指定返回的架構數。 |
| `{START}` | **必填**. 指定結果頁的偏移。 要獲取結果的第一頁，請將值設定為 `start=0`。 |
| `{NAME}` | 根據名稱篩選架構。 |
| `{ORDER_BY}` | 對結果的順序進行排序。 支援的欄位為 `modifiedDate` 和 `createdDate`。 您可以用 `+` 或 `-` 按升序或降序排序。 |

**要求**

以下請求將檢索組織的最後兩個建立的方案。

```shell
curl -X GET https://platform.adobe.io/data/foundation/conversion/schemas&start=0&limit=2 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

以下響應返回HTTP狀態200，其中包含請求的架構的清單。

>[!NOTE]
>
>以下響應已被截斷為空間。

```json
{
    "data": [
        {
            "id": "823ac494f35e4e84bcb2f061378fcca6",
            "version": 0,
            "jsonSchema": {
                "title": "Sample schema",
                "type": "object",
                "properties": {
                    "_id": {
                        "title": "Identifier",
                        "description": "A unique identifier for the record.",
                        "type": "string",
                        "format": "uri-reference",
                        "meta:xdmField": "@id",
                        "meta:xdmType": "string"
                    },
                    "city": {
                        "title": "City",
                        "description": "The name of the city.",
                        "type": "string",
                        "meta:xdmField": "xdm:city",
                        "meta:xdmType": "string"
                    }
                }
            },
            "schemaRef": {
                "id": "https://ns.adobe.com/{TENANT_ID}/schemas/833b1d8a749943d49fe7e925ea19b5dc",
                "contentType": "1.0"
            }
        },
        {
            "id": "0f868d3a1b804fb0abf738306290ae79",
            "version": 0,
            "jsonSchema": {
                "title": "Sample schema 2",
                "type": "object",
                "properties": {
                    "_id": {
                        "title": "Identifier",
                        "description": "A unique identifier for the record.",
                        "type": "string",
                        "format": "uri-reference",
                        "meta:xdmField": "@id",
                        "meta:xdmType": "string"
                    },
                    "city": {
                        "title": "City",
                        "description": "The name of the city.",
                        "type": "string",
                        "meta:xdmField": "xdm:city",
                        "meta:xdmType": "string"
                    }
                }
            },
            "schemaRef": {
                "id": "https://ns.adobe.com/{TENANT_ID}/schemas/0f868d3a1b804fb0abf738306290ae79",
                "contentType": "1.0"
            }
        }
    ],
    "_page": {
        "count": 2,
        "limit": 2
    }
}
```

## 建立方案

您可以通過向Web站點發出POST請求來建立要驗證的架構 `/schemas` 端點。 建立架構有三種方法：發送 [JSON架構](https://json-schema.org/)、使用示例資料或引用現有XDM架構。

```http
POST /schemas
```

### 使用JSON架構

**要求**

以下請求允許您通過發送 [JSON架構](https://json-schema.org/)。

```shell
curl -X POST https://platform.adobe.io/data/foundation/conversion/schemas \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '
{
    "jsonSchema": {
        "id": "string",
        "firstName": "string",
        "lastName": "string"
    }
}'
```

**回應**

成功的響應返回HTTP狀態200，其中包含有關新建立的架構的資訊。

```json
{
    "id": "6daffabf14b1425292add3719afc8fab",
    "version": 0,
    "jsonSchema": {
        "id": "string",
        "firstName": "string",
        "lastName": "string"
    }
}
```

### 使用示例資料

**要求**

以下請求允許您使用先前上載的示例資料建立方案。

```shell
curl -X POST https://platform.adobe.io/data/foundation/conversion/schemas \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '
 {
     "sampleId": "45439a93d48d47d098d26e0f0840cc02"  
 }'
```

| 屬性 | 說明 |
| -------- | ----------- |
| `sampleId` | 基於的架構的示例資料的ID。 |

**回應**

成功的響應返回HTTP狀態200，其中包含有關新建立的架構的資訊。

```json
{
    "id": "b2ee78bd55ac45f781a93fb8b90d99b2",
    "version": 0,
    "jsonSchema": {
        "title": "SampleSchema:45439a93d48d47d098d26e0f0840cc02",
        "type": "object",
        "properties": {
            "gender": {
                "title": "gender",
                "type": "string"
            },
            "last_name": {
                "title": "last_name",
                "type": "string"
            },
            "id": {
                "title": "id",
                "type": "string"
            },
            "ip_address": {
                "title": "ip_address",
                "type": "string"
            },
            "first_name": {
                "title": "first_name",
                "type": "string"
            },
            "email": {
                "title": "email",
                "type": "string"
            }
        }
    },
    "sampleId": "45439a93d48d47d098d26e0f0840cc02"
}
```

### 參考XDM架構

**要求**

以下請求允許您通過引用現有XDM架構來建立架構。

```shell
curl -X POST https://platform.adobe.io/data/foundation/conversion/schemas \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '
 {
     "name": "outputSchema1",
     "schemaRef": {
         "id": "https://ns.adobe.com/{TENANT_ID}/schemas/0d555890502224d187b619f23c35c8d1",
         "contentType": "application/vnd.adobe.xed-full+json;version=1"
     }  
 }'
```

| 屬性 | 說明 |
| -------- | ----------- |
| `name` | 要建立的架構的名稱。 |
| `schemaRef.id` | 您引用的架構的ID。 |
| `schemaRef.contentType` | 確定引用架構的響應格式。 有關此欄位的詳細資訊，請參閱 [架構註冊表開發者指南](../../xdm/api/schemas.md#lookup) |

**回應**

成功的響應返回HTTP狀態200，其中包含有關新建立的架構的資訊。

>[!NOTE]
>
>以下響應已被截斷為空間。

```json
{
    "id": "4b64daa51b774cb2ac21b61d80125ed0",
    "version": 0,
    "name": "schemaName",
    "jsonSchema": "{\"id\":null,\"schema\":null,\"_refId\":null,\"title\":\"SimpleUser\",...,\"imsOrg\":\"{ORG_ID}\",\"$id\":\"https://ns.adobe.com/{TENANT_ID}/schemas/901c44cc5b2748488574f4e2824c5f96\"}",
    "schemaRef": {
        "id": "https://ns.adobe.com/{TENANT_ID}/schemas/901c44cc5b2748488574f4e2824c5f96",
        "contentType": "application/vnd.adobe.xed+json;version=1.0"
    }
}
```

## 使用檔案上載建立架構

可以通過上載JSON檔案來建立要從中轉換的架構。

**API格式**

```http
POST /schemas/upload
```

**要求**

以下請求允許您從上載的JSON檔案建立架構。

```shell
curl -X POST https://platform.adobe.io/data/foundation/conversion/schemas/upload \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: multipart/form-data' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -F 'file=@{PATH_TO_FILE}.json'
```

**回應**

成功的響應返回HTTP狀態200，其中包含有關新建立的架構的資訊。

```json
{
    "id": "292add3716daffabf14b14259afc8fab",
    "version": 0,
    "jsonSchema": {
        "id": "string",
        "firstName": "string",
        "lastName": "string"
    }
}
```

## 檢索特定架構

可通過向Web站點發出GET請求來檢索有關特定架構的資訊 `/schemas` 端點，並提供要在請求路徑中檢索的架構的ID。

**API格式**

```http
GET /schemas/{SCHEMA_ID}
```

| 屬性 | 說明 |
| -------- | ----------- |
| `{SCHEMA_ID}` | 您正在查找的架構的ID。 |

**要求**

以下請求檢索有關指定架構的資訊。

```shell
curl -X GET https://platform.adobe.io/data/foundation/conversion/schemas/0f868d3a1b804fb0abf738306290ae79 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的響應返回HTTP狀態200，其中包含有關指定架構的資訊。

```json
{
    "id": "0f868d3a1b804fb0abf738306290ae79",
    "version": 0,
    "jsonSchema": {
        "title": "Sample schema",
        "description": "Sample description",
        "type": "object",
        "properties": {
            "_id": {
                "title": "Identifier",
                "description": "A unique identifier for the record.",
                "type": "string",
                "format": "uri-reference",
                "meta:xdmField": "@id",
                "meta:xdmType": "string"
            },
            "personalEmail": {
                "title": "Personal Email",
                "description": "A personal email address.",
                "type": "object",
                "properties": {
                    "primary": {
                        "title": "Primary",
                        "description": "Primary email indicator.\n\nA Profile can have only one `primary` email address at a given point of time.\n",
                        "type": "boolean",
                        "meta:xdmField": "xdm:primary",
                        "meta:xdmType": "boolean"
                    },
                    "address": {
                        "title": "Address",
                        "description": "The technical address, e.g 'name@domain.com' as commonly defined in RFC2822 and subsequent standards.",
                        "type": "string",
                        "format": "email",
                        "meta:xdmField": "xdm:address",
                        "meta:xdmType": "string"
                    }
                },
                "meta:xdmField": "xdm:personalEmail",
                "meta:referencedFrom": "https://ns.adobe.com/xdm/context/emailaddress",
                "meta:xdmType": "object"
            }
        },
        "imsOrg": "6A29340459CA8D350A49413A@AdobeOrg",
        "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/833b1d8a749943d49fe7e925ea19b5dc"
    },
    "schemaRef": {
        "id": "https://ns.adobe.com/{TENANT_ID}/schemas/833b1d8a749943d49fe7e925ea19b5dc",
        "contentType": "1.0"
    }
}
```
