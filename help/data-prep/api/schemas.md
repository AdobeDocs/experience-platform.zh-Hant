---
keywords: Experience Platform；首頁；熱門主題；資料準備；api指南；方案；
solution: Experience Platform
title: 結構描述API端點
description: 您可以在Adobe Experience Platform API中使用「/schemas」端點，以程式設計方式擷取、建立及更新綱要，以便與Experience Platform中的對應程式搭配使用。
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '619'
ht-degree: 3%

---



# 結構描述端點

結構描述可與對應程式搭配使用，以確保您擷取到Adobe Experience Platform的資料與您想要擷取的資料相符。 您可以使用`/schemas`端點以程式設計方式建立、列出和取得自訂結構描述，以便與Experience Platform中的對應程式搭配使用。

>[!NOTE]
>
>使用此端點建立的結構描述只會搭配對應程式和對應集使用。 若要建立其他Experience Platform服務可存取的結構描述，請參閱[結構描述登入開發人員指南](../../xdm/api/schemas.md)。

## 取得所有結構描述

您可以向`/schemas`端點發出GET要求，以擷取貴組織所有可用對應程式結構描述的清單。

**API格式**

`/schemas`端點支援數個查詢引數，可協助您篩選結果。 雖然這些引數大多為選用引數，但強烈建議使用這些引數來協助減少昂貴的額外負荷。 不過，您必須在要求中同時包含`start`和`limit`引數。 可以包含多個引數，以&amp;符號(`&`)分隔。

```http
GET /schemas?limit={LIMIT}&start={START}
GET /schemas?limit={LIMIT}&start={START}&name={NAME}
GET /schemas?limit={LIMIT}&start={START}&orderBy={ORDER_BY}
```

| 參數 | 說明 |
| --------- | ----------- |
| `{LIMIT}` | **必要**。 指定傳回的結構描述數目。 |
| `{START}` | **必要**。 指定結果頁面的位移。 若要取得結果的第一頁，請將值設為`start=0`。 |
| `{NAME}` | 根據名稱篩選結構。 |
| `{ORDER_BY}` | 排序結果的順序。 支援的欄位是`modifiedDate`和`createdDate`。 您可以在屬性前面加上`+`或`-`，以分別依遞增或遞減順序排序。 |

**要求**

以下請求會擷取您組織最後兩個建立的結構描述。

```shell
curl -X GET https://platform.adobe.io/data/foundation/conversion/schemas&start=0&limit=2 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

以下回應會傳回HTTP狀態200，其中包含請求的結構描述清單。

>[!NOTE]
>
>下列回應已因空間而截斷。

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

## 建立結構描述

您可以透過向`/schemas`端點發出POST要求，建立要驗證的結構描述。 建立結構描述有三個方法：傳送[JSON結構描述](https://json-schema.org/)、使用範例資料，或參考現有的XDM結構描述。

```http
POST /schemas
```

### 使用JSON結構描述

**要求**

下列要求可讓您透過傳送[JSON結構描述](https://json-schema.org/)來建立結構描述。

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

成功的回應會傳回HTTP狀態200以及有關您新建立之結構描述的資訊。

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

### 使用範例資料

**要求**

下列請求可讓您使用先前上傳的範例資料建立結構描述。

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
| `sampleId` | 架構所依據之範例資料的ID。 |

**回應**

成功的回應會傳回HTTP狀態200以及有關您新建立之結構描述的資訊。

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

### 參考XDM結構描述

**要求**

以下請求可讓您參照現有的XDM結構描述來建立結構描述。

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
| `name` | 您要建立的結構描述名稱。 |
| `schemaRef.id` | 您參考的結構描述ID。 |
| `schemaRef.contentType` | 決定參考之結構描述的回應格式。 您可以在[結構描述登入開發人員指南](../../xdm/api/schemas.md#lookup)中找到此欄位的詳細資訊 |

**回應**

成功的回應會傳回HTTP狀態200以及有關您新建立之結構描述的資訊。

>[!NOTE]
>
>下列回應已因空間而截斷。

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

## 使用檔案上傳建立結構描述

您可以上傳要轉換的JSON檔案來建立結構描述。

**API格式**

```http
POST /schemas/upload
```

**要求**

以下請求可讓您從上傳的JSON檔案建立結構描述。

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

成功的回應會傳回HTTP狀態200以及有關您新建立之結構描述的資訊。

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

## 擷取特定結構描述

您可以向`/schemas`端點發出GET要求，並在要求路徑中提供您要擷取之結構描述的識別碼，以擷取特定結構描述的資訊。

**API格式**

```http
GET /schemas/{SCHEMA_ID}
```

| 屬性 | 說明 |
| -------- | ----------- |
| `{SCHEMA_ID}` | 您要查詢之結構描述的ID。 |

**要求**

以下請求會擷取指定之結構描述的相關資訊。

```shell
curl -X GET https://platform.adobe.io/data/foundation/conversion/schemas/0f868d3a1b804fb0abf738306290ae79 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應會傳回HTTP狀態200，其中包含指定之結構描述的相關資訊。

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
