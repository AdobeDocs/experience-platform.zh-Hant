---
title: CSV模板到架構轉換API終結點
description: 使用架構註冊表API中的/rpc/csv2schema終結點，可以使用CSV模板自動建立體驗資料模型(XDM)架構。
exl-id: cf08774a-db94-4ea1-a22e-bb06385f8d0e
source-git-commit: b4c186c8c40d1372fb5011f49979523e1201fb0b
workflow-type: tm+mt
source-wordcount: '854'
ht-degree: 5%

---

# CSV模板到架構轉換API終結點

的 `/rpc/csv2schema` 端點 [!DNL Schema Registry] API允許您使用CSV檔案作為模板自動建立體驗資料模型(XDM)架構。 使用此終結點，可以建立模板以批量導入架構欄位並減少手動API或UI工作。

## 快速入門

的 `/rpc/csv2schema` 端點是 [[!DNL Schema Registry] API](https://www.adobe.io/experience-platform-apis/references/schema-registry/)。 在繼續之前，請查看 [入門指南](./getting-started.md) 有關相關文檔的連結、本文檔中讀取示例API調用的指南，以及成功調用任何Adobe Experience PlatformAPI所需的標頭的重要資訊。

的 `/rpc/csv2schema` endpoint是遠程過程調用(RPC)的一部分，該調用由 [!DNL Schema Registry]。 不同於 [!DNL Schema Registry] API、RPC終結點不需要像 `Accept` 或 `Content-Type`，並且不使用 `CONTAINER_ID`。 相反，他們必須使用 `/rpc` 命名空間，如下面的API調用中所示。

## CSV檔案要求

要使用此終結點，必須先建立具有相應列標題和相應值的CSV檔案。 某些列是必需的，而其餘列是可選的。 下表介紹了這些列及其在架構構建中的角色。

| CSV標題位置 | CSV標題名稱 | 必填/選填 | 說明 |
| --- | --- | --- | --- |
| 1 | `isIgnored` | 選填 | 包括時，並設定為 `true`，表示該欄位未準備好進行API上載，應忽略。 |
| 2 | `isCustom` | 必填 | 指示該欄位是否為自定義欄位。 |
| 3 | `fieldGroupId` | 選填 | 自定義欄位應與的欄位組的ID。 |
| 4 | `fieldGroupName` | （請參閱說明） | 要與此欄位關聯的欄位組的名稱。<br><br>對於不擴展現有標準欄位的自定義欄位，可選。 如果留空，系統將自動分配名稱。<br><br>標準欄位或擴展標準欄位組的自定義欄位是必需的，用於查詢 `fieldGroupId`。 |
| 5 | `fieldPath` | 必填 | 欄位的完整XED點符號路徑。 要包括標準欄位組中的所有欄位（如下所示） `fieldGroupName`)，將值設定為 `ALL`。 |
| 6 | `displayName` | 選填 | 欄位的標題或友好顯示名稱。 如果存在別名，也可以是標題的別名。 |
| 7 | `fieldDescription` | 選填 | 欄位的說明。 如果存在，也可以是說明的別名。 |
| 8 | `dataType` | （請參閱說明） | 指示 [基本資料類型](../schema/field-constraints.md#basic-types) 的下界。 所有自定義欄位都是必需的。<br><br>如果 `dataType` 設定為 `object`或 `properties` 或 `$ref` 也需要為同一行定義，但不能同時定義兩行。 |
| 9 | `isRequired` | 選填 | 指示資料接收是否需要該欄位。 |
| 10 | `isArray` | 選填 | 指示欄位是否為其指示的陣列 `dataType`。 |
| 11 | `isIdentity` | 選填 | 指示該欄位是否為標識欄位。 |
| 12 | `identityNamespace` | 如果 `isIdentity` 為真 | 的 [標識命名空間](../../identity-service/namespaces.md) 的子菜單。 |
| 13 | `isPrimaryIdentity` | 選填 | 指示欄位是否是架構的主標識。 |
| 14 | `minimum` | 選填 | （僅適用於數字欄位）欄位的最小值。 |
| 15 | `maximum` | 選填 | （僅適用於數字欄位）欄位的最大值。 |
| 16 | `enum` | 選填 | 欄位的枚舉值清單，表示為陣列(例如， `[value1,value2,value3]`)。 |
| 17 | `stringPattern` | 選填 | （僅適用於字串欄位）規則運算式模式，字串值必須匹配，才能在資料接收期間通過驗證。 |
| 18 | `format` | 選填 | （僅適用於字串欄位）字串欄位的格式。 |
| 19 | `minLength` | 選填 | （僅適用於字串欄位）字串欄位的最小長度。 |
| 20 | `maxLength` | 選填 | （僅適用於字串欄位）字串欄位的最大長度。 |
| 21 | `properties` | （請參閱說明） | 如果 `dataType` 設定為 `object` 和 `$ref` 未定義。 這將對象主體定義為JSON字串(如 `{"myField": {"type": "string"}}`)。 |
| 22 | `$ref` | （請參閱說明） | 如果 `dataType` 設定為 `object` 和 `properties` 未定義。 這定義了 `$id` 對象類型的引用對象(例如 `https://ns.adobe.com/xdm/context/person`)。 |
| 23 | `comment` | 選填 | 當 `isIgnored` 設定為 `true`，此列用於提供架構的標題資訊。 |

{style="table-layout:auto"}

請參閱以下內容 [CSV模板](../assets/sample-csv-template.csv) 確定CSV檔案的格式。

## 從CSV檔案建立導出負載

設定CSV模板後，可以將檔案發送到 `/rpc/csv2schema` 並將其轉換為導出負載。

**API格式**

```http
POST /rpc/csv2schema
```

**要求**

請求負載必須使用表單資料作為其格式。 下面顯示了必需的表單欄位。

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/rpc/csv2schema \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -F 'csv-file=@"/Users/userName/Documents/sample-csv-template.csv"' \
  -F 'schema-class-id="https://ns.adobe.com/xdm/context/profile"' \
  -F 'schema-name="Example Schema"' \
  -F 'schema-description="Example schema description."'
```

| 屬性 | 說明 |
| --- | --- |
| `csv-file` | 儲存在本地電腦上的CSV模板的路徑。 |
| `schema-class-id` | 的 `$id` XDM [類](../schema/composition.md#class) 此架構將採用的。 |
| `schema-name` | 架構的顯示名稱。 |
| `schema-description` | 架構的說明。 |

**回應**

成功的響應返回從CSV檔案生成的導出負載。 負載採用陣列的形式，並且每個陣列項都是表示模式的從屬XDM元件的對象。 選擇下面的部分以查看從CSV檔案生成的導出負載的完整示例。

+++ 響應負載示例

```json
[
    {
        "$id": "https://ns.adobe.com/ddgxdmint/mixins/68397e9293a6904b3006311fb46c9573a8aaad49780dd65a",
        "$schema": "http://json-schema.org/draft-06/schema#",
        "type": "object",
        "meta:xdmType": "object",
        "meta:resourceType": "mixins",
        "title": "Generated field group 68397e9293a6904b3006311fb46c9573a8aaad49780dd65a",
        "description": "Generated field group 68397e9293a6904b3006311fb46c9573a8aaad49780dd65a",
        "meta:intendedToExtend": [
            "https://ns.adobe.com/xdm/context/profile"
        ],
        "required": [
            "_ddgxdmint"
        ],
        "properties": {
            "_ddgxdmint": {
                "properties": {
                    "customField1": {
                        "type": "string",
                        "title": "my custom field1",
                        "description": "Sample custom field1"
                    },
                    "customField2": {
                        "properties": {
                            "customerField22": {
                                "type": "string",
                                "title": "my custom field22",
                                "description": "Sample custom field22"
                            }
                        },
                        "type": "object",
                        "required": [
                            "customerField22"
                        ]
                    },
                    "customField3": {
                        "type": "number",
                        "title": "my custom field3",
                        "description": "Sample custom field3",
                        "minimum": 0,
                        "maximum": 10
                    },
                    "customField4": {
                        "type": "string",
                        "title": "my custom field4",
                        "description": "Sample custom field4",
                        "enum": [
                            "one",
                            "two",
                            "three"
                        ]
                    },
                    "customField5": {
                        "type": "array",
                        "title": "my custom field5",
                        "description": "Sample custom field5",
                        "items": {
                            "type": "string"
                        }
                    },
                    "customField6": {
                        "type": "string",
                        "title": "my custom field6",
                        "description": "Sample custom field6",
                        "format": "date"
                    }
                },
                "type": "object",
                "required": [
                    "customField1",
                    "customField2"
                ]
            }
        }
    },
    {
        "$id": "https://ns.adobe.com/ddgxdmint/mixins/7d4edf1a4c2b8c97d31f9931a10618e0b7341cefc97edad6",
        "$schema": "http://json-schema.org/draft-06/schema#",
        "type": "object",
        "meta:xdmType": "object",
        "meta:resourceType": "mixins",
        "title": "SampleFieldGroup",
        "description": "Generated field group 7d4edf1a4c2b8c97d31f9931a10618e0b7341cefc97edad6",
        "meta:intendedToExtend": [
            "https://ns.adobe.com/xdm/context/profile"
        ],
        "properties": {
            "_ddgxdmint": {
                "properties": {
                    "customField7": {
                        "type": "object",
                        "title": "my custom field7",
                        "description": "Sample custom field7",
                        "properties": {
                            "myField": {
                                "type": "string"
                            }
                        }
                    },
                    "customField8": {
                        "type": "array",
                        "title": "my custom field8",
                        "description": "Sample custom field8",
                        "items": {
                            "type": "object",
                            "$ref": "https://ns.adobe.com/xdm/context/person"
                        }
                    }
                },
                "type": "object"
            }
        }
    },
    {
        "$id": "https://ns.adobe.com/ddgxdmint/mixins/6420020c79930a4c3aa7c9fd03b218e0e85c9a7d9990ecf",
        "$schema": "http://json-schema.org/draft-06/schema#",
        "type": "object",
        "meta:xdmType": "object",
        "meta:resourceType": "mixins",
        "title": "Demographic Details:Generated field group 6420020c79930a4c3aa7c9fd03b218e0e85c9a7d9990ecf",
        "description": "Generated field group 6420020c79930a4c3aa7c9fd03b218e0e85c9a7d9990ecf",
        "meta:intendedToExtend": [
            "https://ns.adobe.com/xdm/context/profile"
        ],
        "meta:extends": [
            "https://ns.adobe.com/xdm/context/profile-person-details"
        ],
        "allOf": [
            {
                "properties": {
                    "person": {
                        "properties": {
                            "name": {
                                "properties": {
                                    "_ddgxdmint": {
                                        "properties": {
                                            "nickName": {
                                                "type": "string"
                                            }
                                        },
                                        "type": "object",
                                        "required": [
                                            "nickName"
                                        ]
                                    }
                                },
                                "type": "object",
                                "required": [
                                    "_ddgxdmint"
                                ]
                            }
                        },
                        "type": "object",
                        "required": [
                            "name"
                        ]
                    }
                },
                "required": [
                    "person"
                ]
            },
            {
                "$ref": "https://ns.adobe.com/xdm/context/profile-person-details"
            }
        ]
    },
    {
        "$id": "https://ns.adobe.com/ddgxdmint/mixins/39e6bb291e5b9072878c5c80c0ff5a325df79385ed10d241",
        "$schema": "http://json-schema.org/draft-06/schema#",
        "type": "object",
        "meta:xdmType": "object",
        "meta:resourceType": "mixins",
        "title": "Loyalty Details:Generated field group 39e6bb291e5b9072878c5c80c0ff5a325df79385ed10d241",
        "description": "Generated field group 39e6bb291e5b9072878c5c80c0ff5a325df79385ed10d241",
        "meta:intendedToExtend": [
            "https://ns.adobe.com/xdm/context/profile"
        ],
        "meta:extends": [
            "https://ns.adobe.com/xdm/mixins/profile/profile-loyalty-details"
        ],
        "allOf": [
            {
                "properties": {
                    "loyalty": {
                        "properties": {
                            "_ddgxdmint": {
                                "properties": {
                                    "joinDate": {
                                        "type": "string"
                                    }
                                },
                                "type": "object"
                            }
                        },
                        "type": "object"
                    }
                }
            },
            {
                "$ref": "https://ns.adobe.com/xdm/mixins/profile/profile-loyalty-details"
            }
        ]
    },
    {
        "$id": "https://ns.adobe.com/ddgxdmint/schemas/632cb76723ce2fd3876385168c03eb5201c5997f3f367a2f",
        "$schema": "http://json-schema.org/draft-06/schema#",
        "type": "object",
        "meta:xdmType": "object",
        "meta:resourceType": "schemas",
        "title": "My Sample Schema",
        "description": "My Sample Schema",
        "meta:extends": [
            "https://ns.adobe.com/xdm/context/profile"
        ],
        "allOf": [
            {
                "$ref": "https://ns.adobe.com/xdm/context/profile"
            },
            {
                "$ref": "https://ns.adobe.com/ddgxdmint/mixins/68397e9293a6904b3006311fb46c9573a8aaad49780dd65a"
            },
            {
                "$ref": "https://ns.adobe.com/ddgxdmint/mixins/7d4edf1a4c2b8c97d31f9931a10618e0b7341cefc97edad6"
            },
            {
                "$ref": "https://ns.adobe.com/ddgxdmint/mixins/6420020c79930a4c3aa7c9fd03b218e0e85c9a7d9990ecf",
                "meta:refProperty": [
                    "/person/name/firstName",
                    "/person/name/lastName",
                    "/person/name/_ddgxdmint/nickName"
                ]
            },
            {
                "$ref": "https://ns.adobe.com/ddgxdmint/mixins/39e6bb291e5b9072878c5c80c0ff5a325df79385ed10d241"
            }
        ]
    },
    {
        "@type": "xdm:alternateDisplayInfo",
        "meta:resourceType": "descriptors",
        "xdm:sourceSchema": "https://ns.adobe.com/ddgxdmint/schemas/632cb76723ce2fd3876385168c03eb5201c5997f3f367a2f",
        "xdm:sourceVersion": 1,
        "xdm:sourceProperty": "/person/name/firstName",
        "xdm:title": {
            "en_us": "My first name"
        }
    },
    {
        "@type": "xdm:descriptorIdentity",
        "meta:resourceType": "descriptors",
        "xdm:sourceSchema": "https://ns.adobe.com/ddgxdmint/schemas/632cb76723ce2fd3876385168c03eb5201c5997f3f367a2f",
        "xdm:sourceVersion": 1,
        "xdm:sourceProperty": "/_ddgxdmint/customField1",
        "xdm:namespace": "email",
        "xdm:property": "xdm:code",
        "xdm:isPrimary": true
    }
]
```

+++

## 導入架構負載

從CSV檔案生成導出負載後，可以將該負載發送到 `/rpc/import` 終結點以生成架構。

查看 [導入終結點指南](./import.md) 有關如何從導出負載生成架構的詳細資訊。
