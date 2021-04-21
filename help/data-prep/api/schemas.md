---
keywords: Experience Platform;home；熱門主題；資料準備；api指南；方案；
solution: Experience Platform
title: 方案API端點
topic-legacy: schemas
description: '您可以使用Adobe Experience PlatformAPI中的「/方案」端點，以寫程式方式檢索、建立和更新方案，以便與平台中的映射器一起使用。 '
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '613'
ht-degree: 3%

---



# 方案端點

方案可與映射器一起使用，以確保您已收錄到Adobe Experience Platform的資料與要收錄的資料匹配。 您可以使用`/schemas`端點，以寫程式方式建立、列出和獲取自定義結構，以便與平台中的映射器一起使用。

>[!NOTE]
>
>使用此端點建立的方案只與映射器和映射集一起使用。 要建立可由其他平台服務訪問的架構，請閱讀[架構註冊表開發人員指南](../../xdm/api/schemas.md)。

## 取得所有結構描述

通過向`/schemas`端點發出GET請求，可以檢索IMS組織的所有可用映射程式方案的清單。

**API格式**

`/schemas`端點支援數個查詢參數，可協助您篩選結果。 雖然這些參數大部分都是選擇性的，但強烈建議使用它們，以協助降低昂貴的開銷。 不過，您必須同時包含`start`和`limit`參數，做為請求的一部分。 可以包括多個參數，用&amp;符號(`&`)分隔。

```http
GET /schemas?limit={LIMIT}&start={START}
GET /schemas?limit={LIMIT}&start={START}&name={NAME}
GET /schemas?limit={LIMIT}&start={START}&orderBy={ORDER_BY}
```

| 參數 | 說明 |
| --------- | ----------- |
| `{LIMIT}` | **必填**. 指定返回的方案數。 |
| `{START}` | **必填**. 指定結果頁的偏移。 若要取得第一頁的結果，請將值設定為`start=0`。 |
| `{NAME}` | 根據名稱篩選架構。 |
| `{ORDER_BY}` | 對結果的順序進行排序。 支援的欄位有`modifiedDate`和`createdDate`。 您可以在屬性前加上`+`或`-`，分別依遞增或遞減順序來排序。 |

**要求**

下列請求會擷取您IMS組織的最後兩個已建立結構。

```shell
curl -X GET https://platform.adobe.io/data/foundation/conversion/schemas&start=0&limit=2 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

以下響應返回HTTP狀態200，並返回請求的結構描述的清單。

>[!NOTE]
>
>下列回應已截斷空格。

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

## 建立架構

通過向`/schemas`端點發出POST請求，可以建立要驗證的方案。 建立架構有三種方法：使用範例資料傳送[JSON結構描述](https://json-schema.org/)，或參考現有的XDM結構描述。

```http
POST /schemas
```

### 使用JSON結構描述

**要求**

下列請求可讓您傳送[JSON結構描述](https://json-schema.org/)來建立結構描述。

```shell
curl -X POST https://platform.adobe.io/data/foundation/conversion/schemas \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
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

成功的回應會傳回HTTP狀態200，其中包含您新建立之架構的相關資訊。

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

### 使用樣本資料

**要求**

下列請求可讓您使用先前上傳的範例資料來建立結構。

```shell
curl -X POST https://platform.adobe.io/data/foundation/conversion/schemas \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '
 {
     "sampleId": "45439a93d48d47d098d26e0f0840cc02"  
 }'
```

| 屬性 | 說明 |
| -------- | ----------- |
| `sampleId` | 您將模式設定為of的示例資料的ID。 |

**回應**

成功的回應會傳回HTTP狀態200，其中包含您新建立之架構的相關資訊。

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

### 請參閱XDM架構

**要求**

以下請求可讓您參考現有的XDM架構來建立架構。

```shell
curl -X POST https://platform.adobe.io/data/foundation/conversion/schemas \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
| `name` | 要建立的方案的名稱。 |
| `schemaRef.id` | 您所參照之架構的ID。 |
| `schemaRef.contentType` | 確定引用方案的響應格式。 有關此欄位的詳細資訊，請參閱[方案註冊表開發人員指南](../../xdm/api/schemas.md#lookup) |

**回應**

成功的回應會傳回HTTP狀態200，其中包含您新建立之架構的相關資訊。

>[!NOTE]
>
>下列回應已截斷空格。

```json
{
    "id": "4b64daa51b774cb2ac21b61d80125ed0",
    "version": 0,
    "name": "schemaName",
    "jsonSchema": "{\"id\":null,\"schema\":null,\"_refId\":null,\"title\":\"SimpleUser\",...,\"imsOrg\":\"{IMS_ORG}\",\"$id\":\"https://ns.adobe.com/{TENANT_ID}/schemas/901c44cc5b2748488574f4e2824c5f96\"}",
    "schemaRef": {
        "id": "https://ns.adobe.com/{TENANT_ID}/schemas/901c44cc5b2748488574f4e2824c5f96",
        "contentType": "application/vnd.adobe.xed+json;version=1.0"
    }
}
```

## 使用檔案上載建立架構

您可以上傳JSON檔案，以便從中轉換，以建立結構描述。

**API格式**

```http
POST /schemas/upload
```

**要求**

下列請求可讓您從已上傳的JSON檔案建立結構描述。

```shell
curl -X POST https://platform.adobe.io/data/foundation/conversion/schemas/upload \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: multipart/form-data' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -F 'file=@{PATH_TO_FILE}.json'
```

**回應**

成功的回應會傳回HTTP狀態200，其中包含您新建立之架構的相關資訊。

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

## 檢索特定模式

通過向`/schemas`端點發出GET請求，並在請求路徑中提供要檢索的方案的ID，可以檢索有關特定方案的資訊。

**API格式**

```http
GET /schemas/{SCHEMA_ID}
```

| 屬性 | 說明 |
| -------- | ----------- |
| `{SCHEMA_ID}` | 您正在查找的架構的ID。 |

**要求**

以下請求將檢索有關指定方案的資訊。

```shell
curl -X GET https://platform.adobe.io/data/foundation/conversion/schemas/0f868d3a1b804fb0abf738306290ae79 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的響應返回HTTP狀態200，並返回有關指定模式的資訊。

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
