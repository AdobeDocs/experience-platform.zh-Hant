---
keywords: Experience Platform；首頁；熱門主題；資料準備；api指南；映射集；
solution: Experience Platform
title: 映射集API終結點
description: 可以使用Adobe Experience PlatformAPI中的「/mappingSets」端點以寫程式方式檢索、建立、更新和驗證映射集。
exl-id: a4e4ddcd-164e-42aa-b7d1-ba59d70da142
source-git-commit: 81f48de908b274d836f551bec5693de13c5edaf1
workflow-type: tm+mt
source-wordcount: '852'
ht-degree: 3%

---

# 映射集端點

映射集可用於定義源模式中的資料如何映射到目標模式的資料。 您可以使用 `/mappingSets` 以寫程式方式檢索、建立、更新和驗證映射集。

## 清單映射集

您可以通過向以下站點發出GET請求來檢索組織的所有映射集的清單 `/mappingSets` 端點。

**API格式**

的 `/mappingSets` 終結點支援多個查詢參數以幫助篩選結果。 雖然這些參數大多是可選的，但強烈建議使用這些參數以幫助降低昂貴的開銷。 但是，必須同時包括 `start` 和 `limit` 參數。 可以包括多個參數，用和符號分隔(`&`)。

```http
GET /mappingSets?limit={LIMIT}&start={START}
GET /mappingSets?limit={LIMIT}&start={START}&name={NAME}
GET /mappingSets?limit={LIMIT}&start={START}&orderBy={ORDER_BY}
GET /mappingSets?limit={LIMIT}&start={START}&expandSchema={EXPAND_SCHEMA}
```

| 參數 | 說明 |
| --------- | ----------- |
| `{LIMIT}` | (**必需**)指定返回的映射集數。 |
| `{START}` | (**必需**)指定結果頁的偏移。 要獲取結果的第一頁，請將值設定為 `start=0`。 |
| `{NAME}` | 按名稱篩選映射集。 |
| `{ORDER_BY}` | 對結果的順序進行排序。 唯一支援的欄位是 `createdDate` 和 `updatedDate`。 您可以用 `+` 或 `-` 按升序或降序排序。 |
| `{EXPAND_SCHEMA}` | 一個布爾值，用於確定是否將完整輸出模式作為響應的一部分返回。 |

**要求**

以下請求將檢索您組織內的最後兩個映射集。

```shell
curl -X GET https://platform.adobe.io/data/foundation/conversion/mappingSets?limit=2&start=0 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \ 
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

```json
{
    "data": [
        {
            "id": "428beb15b4864daaaa9dc3f005448005",
            "version": 1,
            "createdDate": 1582250953000,
            "modifiedDate": 1582251156000,
            "createdBy": "acp_xql_gateway",
            "modifiedBy": "acp_ui_platform",
            "supportVersion": "1.1",
            "inputSchema": {
                "id": "e660142cab8e438382abc5691b364b30",
                "version": 0,
                "sampleId": "f9e83882e3e34c1f8b873a3b8113c01e"
            },
            "outputSchema": {
                "id": "1956affc28be468aa452e5e47c680c6b",
                "version": 0,
                "schemaRef": {
                    "id": "https://ns.adobe.com/xdm/context/profile__union",
                    "contentType": "1.0"
                }
            },
            "mappings": [
                {
                    "id": "af809223484341009ce0db13d4b32a3a",
                    "version": 0,
                    "createdDate": 1582250953000,
                    "modifiedDate": 1582250953000,
                    "createdBy": "acp_xql_gateway",
                    "modifiedBy": "acp_xql_gateway",
                    "sourceType": "text/x.schema-path",
                    "source": "id",
                    "destination": "person.name.firstName",
                    "identity": false,
                    "primaryIdentity": false,
                    "matchScore": 0.0,
                    "functionVersion": 1,
                    "sourceAttribute": "id",
                    "destinationXdmPath": "person.name.firstName"
                }
            ],
            "status": "PUBLISHED",
            "strictMapping": false,
            "allowNullValues": false,
            "xdmVersion": "1.0",
            "schemaRef": {
                "id": "https://ns.adobe.com/xdm/context/profile__union",
                "contentType": "1.0"
            },
            "xdmSchema": "https://ns.adobe.com/xdm/context/profile__union"
        },
        {
            "id": "8afb1351833a4a4692ea61074b60813b",
            "version": 0,
            "createdDate": 1582250893000,
            "modifiedDate": 1582250893000,
            "createdBy": "acp_xql_gateway",
            "modifiedBy": "acp_xql_gateway",
            "supportVersion": "1.1",
            "inputSchema": {
                "id": "97fe2ecf4faa400bb66dd6be88a53fe4",
                "version": 0,
                "sampleId": "0248bfb352214f908bdd6cf9c19447e1"
            },
            "outputSchema": {
                "id": "e9c3696715d94905bb4e9bfc2c508e66",
                "version": 0,
                "schemaRef": {
                    "id": "https://ns.adobe.com/xdm/context/profile__union",
                    "contentType": "1.0"
                }
            },
            "mappings": [
                {
                    "id": "74647d8bf3b742f289534bee2fdeb732",
                    "version": 0,
                    "createdDate": 1582250893000,
                    "modifiedDate": 1582250893000,
                    "createdBy": "acp_xql_gateway",
                    "modifiedBy": "acp_xql_gateway",
                    "sourceType": "text/x.schema-path",
                    "source": "last_name",
                    "destination": "person.name.lastName",
                    "identity": false,
                    "primaryIdentity": false,
                    "matchScore": 0.0,
                    "functionVersion": 1,
                    "sourceAttribute": "last_name",
                    "destinationXdmPath": "person.name.lastName"
                }
            ],
            "status": "DRAFT",
            "strictMapping": false,
            "allowNullValues": false,
            "xdmVersion": "1.0",
            "schemaRef": {
                "id": "https://ns.adobe.com/xdm/context/profile__union",
                "contentType": "1.0"
            },
            "xdmSchema": "https://ns.adobe.com/xdm/context/profile__union"
        }
    ],
    "_page": {
        "count": 0,
        "limit": 2
    }
}
```

## 建立映射集

可通過向POST請求建立新映射集 `/mappingSets` 端點。

**API格式**

```http
POST /mappingSets
```

**要求**

以下請求將建立一個新的映射集，該映射集由負載中提供的參數配置。

```shell
curl -X POST https://platform.adobe.io/data/foundation/conversion/mappingSets \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \ 
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '
  {
    "outputSchema": {
        "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/89abc189258b1cb1a816d8f2b2341a6d98000ed8f4008305",
            "contentType": "application/vnd.adobe.xed-full+json;version=1"
        }
    },
    "mappings": [
        {
            "sourceType": "ATTRIBUTE",
            "source": "id",
            "destination": "_id",
            "name": "id",
            "description": "Identifier field"
        },
        {
            "sourceType": "ATTRIBUTE",
            "source": "firstName",
            "destination": "person.name.firstName"
        },
        {
            "sourceType": "ATTRIBUTE",
            "source": "lastName",
            "destination": "person.name.lastName"
        }
    ]
}
```

| 屬性 | 說明 |
| -------- | ----------- |
| `outputSchema.schemaRef.id` | 您所引用的XDM架構的ID。 |
| `outputSchema.schemaRef.contentType` | 確定引用架構的響應格式。 有關此欄位的詳細資訊，請參閱 [架構註冊表開發人員指南](../../xdm/api/schemas.md#lookup)。 |
| `mappings.sourceType` | 源類型描述如何將值從源提取到目標。 源類型支援兩個可能的值： <ul><li>`ATTRIBUTE`:源類型 `ATTRIBUTE` 當輸入屬性來自源架構時使用。</li><li>`EXPRESSION`:源類型 `EXPRESSION` 在使用計算欄位完成映射時使用。</li></ul> **警告**:錯誤設定源類型值可能會呈現不可編輯的映射集。 |
| `mappings.source` | 要映射資料的位置。 |
| `mappings.destination` | 要映射資料的位置。 |

**回應**

成功的響應返回HTTP狀態200，其中包含有關新建立的映射集的資訊。

```json
{
    "id": "e7c80e4c0d8f4a98a7d400b4e178b635",
    "version": 0,
    "createdDate": 1614901254724,
    "modifiedDate": 1614901254724,
    "createdBy": "{CREATED_BY}",
    "modifiedBy": "{MODIFIED_BY}"
}
```

## 驗證映射

您可以通過向以下站點發出POST請求來驗證映射是否正確工作 `/mappingSets/validate` 端點。

**API格式**

```http
POST /mappingSets/validate
```

**要求**

以下請求驗證負載中提供的映射。

```shell
curl -X POST https://platform.adobe.io/data/foundation/conversion/mappingSets/validate \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \ 
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '
  {
    "outputSchema": {
        "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/89abc189258b1cb1a816d8f2b2341a6d98000ed8f4008305",
            "contentType": "application/vnd.adobe.xed-full+json;version=1"
        }
    },
    "mappings": [
        {
            "sourceType": "ATTRIBUTE",
            "source": "id",
            "destination": "_id",
            "name": "id",
            "description": "Identifier field"
        },
        {
            "sourceType": "ATTRIBUTE",
            "source": "firstName",
            "destination": "person.name.firstName"
        },
        {
            "sourceType": "ATTRIBUTE",
            "source": "lastName",
            "destination": "person.name.lastName"
        }
    ]
}
```

**回應**

成功的響應返回HTTP狀態200，其中包含建議映射的驗證資訊。

```json
{
    "validationResponse": [
        {
            "status": "SUCCESS",
            "errors": null
        },
        {
            "status": "SUCCESS",
            "errors": null
        },
        {
            "status": "SUCCESS",
            "errors": null
        }
    ]
}
```

## 預覽映射的資料

您可以通過向POST發出請求來預覽要映射的資料 `/mappingSets/preview` 端點。

**API格式**

```http
POST /mappingSets/preview
```

**要求**

```shell
curl -X POST https://platform.adobe.io/data/foundation/conversion/mappingSets/preview \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \ 
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '
{
    "data": [
        {
            "id": 1234,
            "firstName": "Jim",
            "lastName": "Seltzer"
        }
    ],
    "mappingSet": {
        "outputSchema": {
            "schemaRef": {
                "id": "https://ns.adobe.com/stardust/schemas/89abc189258b1cb1a816d8f2b2341a6d98000ed8f4008305",
                "contentType": "application/vnd.adobe.xed-full+json;version=1"
            }
        },
        "mappings": [
            {
                "sourceType": "ATTRIBUTE",
                "source": "id",
                "destination": "_id",
                "name": "id",
                "description": "Identifier field"
            },
            {
                "sourceType": "ATTRIBUTE",
                "source": "firstName",
                "destination": "person.name.firstName"
            },
            {
                "sourceType": "ATTRIBUTE",
                "source": "lastName",
                "destination": "person.name.lastName"
            }
        ]
    }
}'
```

**回應**

成功的響應返回HTTP狀態200，並預覽映射的資料。

```json
[
    {
        "data": {
            "person": {
                "name": {
                    "firstName": "Jim",
                    "lastName": "Seltzer"
                }
            },
            "_id": "1234"
        },
        "errors": null
    }
]
```

## 查找映射集

通過在GET請求到的路徑中提供特定映射集的ID，可以檢索特定映射集 `/mappingSets` 端點。 此終結點還支援多個查詢參數，以幫助您檢索有關指定映射集版本的詳細資訊。

**API格式**

```http
GET /mappingSets/{MAPPING_SET_ID}
GET /mappingSets/{MAPPING_SET_ID}?expandSchema={EXPAND_SCHEMA}
GET /mappingSets/{MAPPING_SET_ID}?version={VERSION}
```

| 參數 | 說明 |
| --------- | ----------- |
| `{MAPPING_SET_ID}` | (**必需**)要檢索的映射集的ID。 |
| `{EXPAND_SCHEMA}` | 一個布爾查詢參數，它確定是否將輸出模式作為響應的一部分返回。 |
| `{VERSION}` | 確定要檢索的映射集版本的整數查詢參數。 |

**要求**

以下請求檢索有關指定映射集的詳細資訊。

```shell
curl -X GET https://platform.adobe.io/data/foundation/conversion/mappingSets/e7c80e4c0d8f4a98a7d400b4e178b635 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \ 
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的響應返回HTTP狀態200，其中包含要檢索的映射集的詳細資訊。

>[!NOTE]
>
>以下響應已被截斷為空間。

```json
{
    "id": "e7c80e4c0d8f4a98a7d400b4e178b635",
    "version": 0,
    "createdDate": 1614901255000,
    "modifiedDate": 1614901255000,
    "createdBy": "CAEB5DE75E6FBFAC0A494110@techacct.adobe.com",
    "modifiedBy": "CAEB5DE75E6FBFAC0A494110@techacct.adobe.com",
    "supportVersion": "1.1",
    "outputSchema": {
        "id": "cf0a57df22354cfdb5f32a747b63a456",
        "version": 0,
        "jsonSchema": {
            "title": "A sample schema",
            "description": "My sample schema",
            "type": "object",
            "properties": {
                "_id": {
                    "title": "Identifier",
                    "description": "A unique identifier for the record.",
                    "type": "string"
                },
                "_repo": {
                    "type": "object",
                    "properties": {
                        "createDate": {
                            "type": "string",
                            "format": "date-time"
                        },
                        "modifyDate": {
                            "type": "string",
                            "format": "date-time"
                        }
                    }
                },
                "createdByBatchID": {
                    "type": "string",
                    "format": "uri-reference"
                },
                "modifiedByBatchID": {
                    "type": "string",
                    "format": "uri-reference"
                },
                "person": {
                    "type": "object",
                    "properties": {
                        "birthDate": {
                            "type": "string",
                            "format": "date"
                        },
                        "birthDayAndMonth": {
                            "type": "string",
                            "pattern": "[0-1][0-9]-[0-9][0-9]"
                        },
                        "birthYear": {
                            "type": "integer",
                            "minimum": 1,
                            "maximum": 32767
                        },
                        "gender": {
                            "type": "string",
                            "default": "not_specified",
                            "enum": [
                                "non_specific",
                                "not_specified",
                                "female",
                                "male"
                            ]
                        },
                        "name": {
                            "title": "Full name",
                            "description": "The person's full name.",
                            "type": "object",
                            "properties": {
                                "firstName": {
                                    "title": "First name",
                                    "type": "string"
                                },
                                "fullName": {
                                    "title": "Full name",
                                    "type": "string"
                                },
                                "lastName": {
                                    "title": "Last name",
                                    "type": "string"
                                },
                                "middleName": {
                                    "title": "Middle name",
                                    "type": "string"
                                }
                            }
                        }
                    }
                },
                "personID": {
                    "title": "Person ID",
                    "type": "string"
                },
                "repositoryCreatedBy": {
                    "title": "Created by user identifier",
                    "type": "string"
                },
                "repositoryLastModifiedBy": {
                    "title": "Modified by user identifier",
                    "type": "string"
                }
            },
            "version": "1.0",
            "imsOrg": "{ORG_ID}",
            "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/89abc189258b1cb1a816d8f2b2341a6d98000ed8f4008305"
        },
        "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/89abc189258b1cb1a816d8f2b2341a6d98000ed8f4008305",
            "contentType": "application/vnd.adobe.xed-full+json;version=1"
        }
    },
    "mappings": [
        {
            "id": "a11f44b0214d4fdcb79cbb5e1d93e638",
            "version": 0,
            "sourceType": "text/x.schema-path",
            "source": "id",
            "destination": "_id",
            "name": "id",
            "description": "Identifier field"
        },
        {
            "id": "b9bf7873451f4b7ba767ca3ba9327750",
            "version": 0,
            "sourceType": "text/x.schema-path",
            "source": "firstName",
            "destination": "person.name.firstName",
        },
        {
            "id": "bab961fc18f54789b9268ec04c6f6f9b",
            "version": 0,
            "sourceType": "text/x.schema-path",
            "source": "lastName",
            "destination": "person.name.lastName",
        }
    ],
    "status": "DRAFT",
    "strictMapping": false,
    "allowNullValues": false,
    "xdmVersion": "application/vnd.adobe.xed-full+json;version=1",
    "schemaRef": {
        "id": "https://ns.adobe.com/{TENANT_ID}/schemas/89abc189258b1cb1a816d8f2b2341a6d98000ed8f4008305",
        "contentType": "application/vnd.adobe.xed-full+json;version=1"
    },
    "xdmSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/89abc189258b1cb1a816d8f2b2341a6d98000ed8f4008305"
}
```

## 更新映射集

可以通過在路徑中提供映射集的ID來更新映射集 `PUT` 請求 `mappingSets` 端點。

**API格式**

```http
PUT /mappingSets/{MAPPING_SET_ID}
```

| 參數 | 說明 |
| --------- | ----------- |
| `{MAPPING_SET_ID}` | 要更新的映射集的ID。 |

**要求**

```shell
curl -X PUT https://platform.adobe.io/data/foundation/conversion/mappingSets/e7c80e4c0d8f4a98a7d400b4e178b635 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \ 
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '
  {
    "outputSchema": {
        "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/89abc189258b1cb1a816d8f2b2341a6d98000ed8f4008305",
            "contentType": "application/vnd.adobe.xed-full+json;version=1"
        }
    },
    "mappings": [
        {
            "sourceType": "ATTRIBUTE",
            "source": "id",
            "destination": "_id",
            "name": "id",
            "description": "Identifier field"
        },
        {
            "sourceType": "ATTRIBUTE",
            "source": "firstName",
            "destination": "person.name.firstName"
        },
        {
            "sourceType": "ATTRIBUTE",
            "source": "lastName",
            "destination": "person.name.lastName"
        },
        {
            "sourceType": "ATTRIBUTE",
            "source": "nationality",
            "destination": "person.nationality"           
        }
    ]
}
```

**回應**

成功的響應返回HTTP狀態200，其中包含有關新更新的映射集的詳細資訊。

>[!NOTE]
>
>以下響應已被截斷為空間。

```json
{
    "id": "e7c80e4c0d8f4a98a7d400b4e178b635",
    "version": 1,
    "createdDate": 1614901255000,
    "modifiedDate": 1614909614227,
    "createdBy": "CAEB5DE75E6FBFAC0A494110@techacct.adobe.com",
    "modifiedBy": "CAEB5DE75E6FBFAC0A494110@techacct.adobe.com",
    "supportVersion": "1.1",
    "outputSchema": {
        "id": "cf0a57df22354cfdb5f32a747b63a456",
        "version": 0,
        "jsonSchema": {
            "title": "A sample schema",
            "description": "My sample schema",
            "type": "object",
            "properties": {
                "_id": {
                    "title": "Identifier",
                    "description": "A unique identifier for the record.",
                    "type": "string",
                },
                "_repo": {
                    "type": "object",
                    "properties": {
                        "createDate": {
                            "type": "string",
                            "format": "date-time"
                        },
                        "modifyDate": {
                            "type": "string",
                            "format": "date-time"
                        }
                    }
                },
                "createdByBatchID": {
                    "type": "string",
                    "format": "uri-reference"
                },
                "modifiedByBatchID": {
                    "type": "string",
                    "format": "uri-reference"
                },
                "person": {
                    "type": "object",
                    "properties": {
                        "birthDate": {
                            "type": "string",
                            "format": "date"
                        },
                        "birthDayAndMonth": {
                            "type": "string",
                            "pattern": "[0-1][0-9]-[0-9][0-9]"
                        },
                        "birthYear": {
                            "type": "integer",
                            "minimum": 1,
                            "maximum": 32767
                        },
                        "gender": {
                            "type": "string",
                            "default": "not_specified",
                            "enum": [
                                "non_specific",
                                "not_specified",
                                "female",
                                "male"
                            ]
                        },
                        "name": {
                            "title": "Full name",
                            "description": "The person's full name.",
                            "type": "object",
                            "properties": {
                                "firstName": {
                                    "title": "First name",
                                    "type": "string"
                                },
                                "fullName": {
                                    "title": "Full name",
                                    "type": "string"
                                },
                                "lastName": {
                                    "title": "Last name",
                                    "type": "string"
                                },
                                "middleName": {
                                    "title": "Middle name",
                                    "type": "string"
                                },
                                "suffix": {
                                    "title": "Suffix",
                                    "type": "string"
                                }
                            }
                        }
                },
                "personID": {
                    "title": "Person ID",
                    "type": "string"
                },
                "repositoryCreatedBy": {
                    "title": "Created by user identifier",
                    "type": "string"
                },
                "repositoryLastModifiedBy": {
                    "title": "Modified by user identifier",
                    "type": "string"
                }
            },
            "version": "1.0",
            "imsOrg": "6A29340459CA8D350A49413A@AdobeOrg",
            "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/89abc189258b1cb1a816d8f2b2341a6d98000ed8f4008305"
        },
        "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/89abc189258b1cb1a816d8f2b2341a6d98000ed8f4008305",
            "contentType": "application/vnd.adobe.xed-full+json;version=1"
        }
    },
    "mappings": [
        {
            "id": "1bb13ec5929f4847a8ea0f1d9e60d3e6",
            "version": 0,
            "sourceType": "text/x.schema-path",
            "source": "id",
            "destination": "_id",
            "name": "id"
        },
        {
            "id": "394bec970d54410b98e1d4c55a3843ca",
            "version": 0,
            "sourceType": "text/x.schema-path",
            "source": "firstName",
            "destination": "person.name.firstName"
        },
        {
            "id": "a78729629b22418998b528755b3e0fb1",
            "version": 0,
            "sourceType": "text/x.schema-path",
            "source": "lastName",
            "destination": "person.name.lastName"
        },
        {
            "id": "c5211e1e295f48018c125c24a04e925a",
            "version": 0,
            "sourceType": "text/x.schema-path",
            "source": "nationality",
            "destination": "person.nationality"
        }
    ],
    "strictMapping": false,
    "allowNullValues": false,
    "xdmVersion": "application/vnd.adobe.xed-full+json;version=1",
    "schemaRef": {
        "id": "https://ns.adobe.com/{TENANT_ID}/schemas/89abc189258b1cb1a816d8f2b2341a6d98000ed8f4008305",
        "contentType": "application/vnd.adobe.xed-full+json;version=1"
    },
    "xdmSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/89abc189258b1cb1a816d8f2b2341a6d98000ed8f4008305"
}
```

## 列出映射集的映射

通過在GET請求到以下端點的路徑中提供其ID，可以查看屬於特定映射集的所有映射。

**API格式**

```http
GET /mappingSets/{MAPPING_SET_ID}/mappings
```

| 參數 | 說明 |
| --------- | ----------- |
| `{MAPPING_SET_ID}` | 要檢索映射的映射集的ID。 |

**要求**

以下請求返回指定映射集中的所有映射。

```shell
curl -X GET https://platform.adobe.io/data/foundation/conversion/mappingSets/e7c80e4c0d8f4a98a7d400b4e178b635/mappings \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \ 
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

```json
[
    {
        "id": "1bb13ec5929f4847a8ea0f1d9e60d3e6",
        "version": 0,
        "createdDate": 1614909614000,
        "modifiedDate": 1614909614000,
        "createdBy": "{CREATED_BY}",
        "modifiedBy": "{MODIFIED_BY}",
        "sourceType": "text/x.schema-path",
        "source": "id",
        "destination": "_id",
        "name": "id",
        "description": "Identifier field",
        "identity": false,
        "primaryIdentity": false,
        "matchScore": 0.0,
        "functionVersion": 1,
        "sourceAttribute": "id",
        "destinationXdmPath": "_id"
    },
    {
        "id": "394bec970d54410b98e1d4c55a3843ca",
        "version": 0,
        "createdDate": 1614909614000,
        "modifiedDate": 1614909614000,
        "createdBy": "{CREATED_BY}",
        "modifiedBy": "{MODIFIED_BY}",
        "sourceType": "text/x.schema-path",
        "source": "firstName",
        "destination": "person.name.firstName",
        "identity": false,
        "primaryIdentity": false,
        "matchScore": 0.0,
        "functionVersion": 1,
        "sourceAttribute": "firstName",
        "destinationXdmPath": "person.name.firstName"
    },
    {
        "id": "a78729629b22418998b528755b3e0fb1",
        "version": 0,
        "createdDate": 1614909614000,
        "modifiedDate": 1614909614000,
        "createdBy": "{CREATED_BY}",
        "modifiedBy": "{MODIFIED_BY}",
        "sourceType": "text/x.schema-path",
        "source": "lastName",
        "destination": "person.name.lastName",
        "identity": false,
        "primaryIdentity": false,
        "matchScore": 0.0,
        "functionVersion": 1,
        "sourceAttribute": "lastName",
        "destinationXdmPath": "person.name.lastName"
    },
    {
        "id": "c5211e1e295f48018c125c24a04e925a",
        "version": 0,
        "createdDate": 1614909614000,
        "modifiedDate": 1614909614000,
        "createdBy": "{CREATED_BY}",
        "modifiedBy": "{MODIFIED_BY}",
        "sourceType": "text/x.schema-path",
        "source": "nationality",
        "destination": "person.nationality",
        "identity": false,
        "primaryIdentity": false,
        "matchScore": 0.0,
        "functionVersion": 1,
        "sourceAttribute": "nationality",
        "destinationXdmPath": "person.nationality"
    }
]
```

## 查找映射集內的映射

通過在GET請求路徑中提供映射集的ID到以下端點，可以檢索映射集的特定映射。

**API格式**

```http
GET /mappingSets/{MAPPING_SET_ID}/mappings/{MAPPING_ID}
```

| 參數 | 說明 |
| --------- | ----------- |
| `{MAPPING_SET_ID}` | 要查找有關的映射資訊的映射集的ID。 |
| `{MAPPING_ID}` | 要查找的映射的ID。 |

**要求**

以下請求檢索有關指定映射集中特定映射的資訊。

```shell
curl -X GET https://platform.adobe.io/data/foundation/conversion/mappingSets/e7c80e4c0d8f4a98a7d400b4e178b635/mappings/394bec970d54410b98e1d4c55a3843ca \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \ 
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的響應返回HTTP狀態200，其中包含有關指定映射的詳細資訊。

```json
{
    "id": "394bec970d54410b98e1d4c55a3843ca",
    "version": 0,
    "createdDate": 1614909614000,
    "modifiedDate": 1614909614000,
    "createdBy": "{CREATED_BY}",
    "modifiedBy": "{MODIFIED_BY}",
    "sourceType": "text/x.schema-path",
    "source": "firstName",
    "destination": "person.name.firstName",
    "identity": false,
    "primaryIdentity": false,
    "matchScore": 0.0,
    "functionVersion": 1,
    "sourceAttribute": "firstName",
    "destinationXdmPath": "person.name.firstName"
}
```
