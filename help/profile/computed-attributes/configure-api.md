---
keywords: Experience Platform；配置檔案；即時客戶配置檔案；故障排除；API
title: 如何配置計算屬性欄位
topic-legacy: guide
type: Documentation
description: 計算屬性是用於將事件級別資料聚合到配置檔案級別屬性的函式。 為了配置計算屬性，首先需要標識將保存計算屬性值的欄位。 可以使用方案註冊表API建立此欄位，以定義將保存計算屬性欄位的方案和自定義欄位組。
exl-id: 91c5d125-8ab5-4291-a974-48dd44c68a13
translation-type: tm+mt
source-git-commit: 3985ba8f46a62e8d9ea8b1f084198b245318a24f
workflow-type: tm+mt
source-wordcount: '736'
ht-degree: 2%

---

# (Alpha)使用方案註冊表API配置計算屬性欄位

>[!IMPORTANT]
>
>計算屬性功能目前位於alpha值中，並非所有使用者都能使用。 文件和功能可能會有所變更。

為了配置計算屬性，首先需要標識將保存計算屬性值的欄位。 可以使用方案註冊表API建立此欄位，以定義將保存計算屬性欄位的方案和自定義方案欄位組。 建議您最好建立單獨的「計算屬性」方案和欄位組，您的組織可以在其中添加任何用作計算屬性的屬性。 這可讓您的組織將計算的屬性架構與用於資料擷取的其他架構完全分開。

本文檔中的工作流概述了如何使用方案註冊表API建立引用自定義欄位組的啟用概要檔案的「計算屬性」架構。 本文檔包含特定於計算屬性的示例代碼，但有關使用API定義欄位組和方案的詳細資訊，請參閱[方案註冊表API指南](../../xdm/api/overview.md)。

## 建立計算屬性欄位組

要使用方案註冊表API建立欄位組，首先向`/tenant/fieldgroups`端點發出POST請求，並提供請求主體中欄位組的詳細資訊。 有關使用方案註冊表API使用欄位組的詳細資訊，請參閱[欄位組API端點指南](../../xdm/api/field-groups.md)。

**API格式**

```http
POST /tenant/fieldgroups
```

**要求**

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/fieldgroups\
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'content-type: application/json' \
  -d '{
        "title":"Computed Attributes Field Group",
        "description":"Description of the field group.",
        "type":"object",
        "meta:extensible": true,
        "meta:abstract": true,
        "meta:intendedToExtend": [
          "https://ns.adobe.com/xdm/context/profile"
        ],
        "definitions": {
          "computedAttributesFieldGroup": {
            "type": "object",
            "meta:xdmType": "object",
            "properties": {
              "_{TENANT_ID}": {
                "type": "object",
                "meta:xdmType": "object",
                "properties": {
                  "birthdayCurrentMonth": {
                    "type": "boolean",
                    "meta:xdmType": "boolean"
                  }
                }
              }
            }
          }
        },
        "allOf": [
          {
            "$ref": "#/definitions/computedAttributesFieldGroup"
          }
        ]
      }'
```

| 屬性 | 說明 |
|---|---|
| `title` | 您正在建立的欄位群組名稱。 |
| `meta:intendedToExtend` | 可使用欄位組的XDM類。 |

**回應**

成功的請求返回HTTP響應狀態201（已建立），其響應主體包含新建欄位組的詳細資訊，包括`$id`、`meta:altIt`和`version`。 這些值是只讀的，由方案註冊表指定。

```json
{
  "$id": "https://ns.adobe.com/{TENANT_ID}/fieldgroups/860ad1b1b35e0a88ecf6df92ebce08335c180313d5805352",
  "meta:altId": "_{TENANT_ID}.fieldgroups.860ad1b1b35e0a88ecf6df92ebce08335c180313d5805352",
  "meta:resourceType": "fieldgroups",
  "version": "1.0",
  "title": "Computed Attributes Field Group",
  "type": "object",
  "description": "Description of the field group.",
  "definitions": {
    "computedAttributesFieldGroup": {
      "type": "object",
      "meta:xdmType": "object",
      "properties": {
        "_{TENANT_ID}": {
          "type": "object",
          "meta:xdmType": "object",
          "properties": {
            "birthdayCurrentMonth": {
              "type": "boolean",
              "meta:xdmType": "boolean"
            }
          }
        }
      }
    }
  },
  "allOf": [
    {
      "$ref": "#/definitions/computedAttributesFieldGroup",
      "type": "object",
      "meta:xdmType": "object"
    }
  ],
  "imsOrg": "{IMS_ORG}",
  "meta:extensible": true,
  "meta:abstract": true,
  "meta:intendedToExtend": [
    "https://ns.adobe.com/xdm/context/profile"
  ],
  "meta:xdmType": "object",
  "meta:registryMetadata": {
    "repo:createdDate": 1612861108205,
    "repo:lastModifiedDate": 1612861108205,
    "xdm:createdClientId": "{CLIENT_ID}",
    "xdm:lastModifiedClientId": "{CLIENT_ID}",
    "xdm:createdUserId": "{USER_ID}",
    "xdm:lastModifiedUserId": "{USER_ID}",
    "eTag": "627faa3346d3004aef2010e9bd2b7e721b19ae7857b276f3ef733e6e732d495f",
    "meta:globalLibVersion": "1.19.4"
  },
  "meta:containerId": "tenant",
  "meta:sandboxId": "{SANDBOX_ID}",
  "meta:sandboxType": "production",
  "meta:tenantNamespace": "_{TENANT_ID}"
}
```

## 使用其他計算屬性更新欄位組

由於需要更多計算屬性，因此可以通過向`/tenant/fieldgroups`端點發出PUT請求，以附加屬性更新計算屬性欄位組。 此請求要求您必須包含路徑中建立之欄位群組的唯一ID，以及您要新增至內文的所有新欄位。

有關使用方案註冊表API更新欄位組的詳細資訊，請參閱[欄位組API端點指南](../../xdm/api/field-groups.md)。

**API格式**

```http
PUT /tenant/fieldgroups/{FIELD_GROUP_ID}
```

**要求**

此請求會新增與`purchaseSummary`資訊相關的欄位。

>[!NOTE]
>
>在通過PUT請求更新欄位組時，主體必須包括在POST請求中建立新欄位組時需要的所有欄位。

```shell
curl -X PUT \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/fieldgroups/_{TENANT_ID}.fieldgroups.8779fd45d6e4eb074300023a439862bbba359b60d451627a \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "type": "object",
        "title": "Computed Attributes Field Group",
        "meta:extensible": true,
        "meta:abstract": true,
        "meta:intendedToExtend": [
          "https://ns.adobe.com/xdm/context/profile"
        ],
        "description": "Description of field group.",
        "definitions": {
          "computedAttributesFieldGroup": {
            "type": "object",
            "meta:xdmType": "object",
            "properties": {
              "_{TENANT_ID}": {
                "type": "object",
                "meta:xdmType": "object",
                "properties": {
                  "birthdayCurrentMonth": {
                    "type": "boolean",
                    "meta:xdmType": "boolean"
                  },
                  "purchaseSummary": {
                    "type": "object",
                    "meta:xdmType": "object",
                    "properties": {
                      "totalSpend": {
                        "type": "number",
                        "meta:xdmType": "number"
                      },
                      "countPurchases": {
                        "meta:xdmType": "int",
                        "type": "integer",
                        "minimum": -2147483648,
                        "maximum": 2147483647
                      },
                      "averageSpend": {
                        "type": "number",
                        "meta:xdmType": "number"
                      }
                    }
                  }
                }
              }
            }
          }
        },
        "allOf": [
          {
            "$ref": "#/definitions/computedAttributesFieldGroup"
          }
        ]
      }'
```

**回應**

成功的回應會傳回更新欄位群組的詳細資料。

```json
{
  "$id": "https://ns.adobe.com/{TENANT_ID}/fieldgroups/860ad1b1b35e0a88ecf6df92ebce08335c180313d5805352",
  "meta:altId": "_{TENANT_ID}.fieldgroups.860ad1b1b35e0a88ecf6df92ebce08335c180313d5805352",
  "meta:resourceType": "fieldgroups",
  "version": "1.0",
  "title": "Computed Attributes Field Group",
  "type": "object",
  "description": "Description of field group.",
  "definitions": {
    "computedAttributesFieldGroup": {
      "type": "object",
      "meta:xdmType": "object",
      "properties": {
        "_{TENANT_ID}": {
          "type": "object",
          "meta:xdmType": "object",
          "properties": {
            "birthdayCurrentMonth": {
              "type": "boolean",
              "meta:xdmType": "boolean"
            },
            "purchaseSummary": {
              "type": "object",
              "meta:xdmType": "object",
              "properties": {
                "totalSpend": {
                  "type": "number",
                  "meta:xdmType": "number"
                },
                "countPurchases": {
                  "meta:xdmType": "int",
                  "type": "integer",
                  "minimum": -2147483648,
                  "maximum": 2147483647
                },
                "averageSpend": {
                  "type": "number",
                  "meta:xdmType": "number"
                }
              }
            }
          }
        }
      }
    }
  },
  "allOf": [
    {
      "$ref": "#/definitions/computedAttributesFieldGroup",
      "type": "object",
      "meta:xdmType": "object"
    }
  ],
  "imsOrg": "{IMS_ORG}",
  "meta:extensible": true,
  "meta:abstract": true,
  "meta:intendedToExtend": [
    "https://ns.adobe.com/xdm/context/profile"
  ],
  "meta:xdmType": "object",
  "meta:registryMetadata": {
    "repo:createdDate": 1612861108205,
    "repo:lastModifiedDate": 1612861108205,
    "xdm:createdClientId": "{CLIENT_ID}",
    "xdm:lastModifiedClientId": "{CLIENT_ID}",
    "xdm:createdUserId": "{USER_ID}",
    "xdm:lastModifiedUserId": "{USER_ID}",
    "eTag": "627faa3346d3004aef2010e9bd2b7e721b19ae7857b276f3ef733e6e732d495f",
    "meta:globalLibVersion": "1.19.4"
  },
  "meta:containerId": "tenant",
  "meta:sandboxId": "{SANDBOX_ID}",
  "meta:sandboxType": "production",
  "meta:tenantNamespace": "_{TENANT_ID}"
}
```

## 建立啟用配置檔案的架構

要使用方案註冊表API建立方案，首先向`/tenant/schemas`端點發出POST請求，並在請求主體中提供方案的詳細資訊。 [!DNL Profile]還必須啟用架構，並作為架構類的聯合架構的一部分出現。

有關[!DNL Profile]啟用的架構和聯合架構的詳細資訊，請查看[[!DNL Schema Registry] API指南](../../xdm/api/overview.md)和[架構構成基礎文檔](../../xdm/schema/composition.md)。

**API格式**

```http
POST /tenants/schemas
```

**要求**

以下請求將建立一個新模式，該模式引用在本文檔之前建立的`computedAttributesFieldGroup`（使用其唯一ID），並且已為Profile union模式（使用`meta:immutableTags`陣列）啟用。 有關如何使用方案註冊表API建立方案的詳細說明，請參閱[方案API端點指南](../../xdm/api/schemas.md)。

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas \
  -H 'Authorization: Bearer {ACCESS_TOKEN' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "type": "object",
        "title": "Computed Attributes Schema",
        "meta:extensible": false,
        "meta:abstract": false,
        "meta:immutableTags": [
          "union"
        ],
        "meta:extends": [
          "https://ns.adobe.com/xdm/context/profile",
          "https://ns.adobe.com/xdm/context/identitymap",
          "https://ns.adobe.com/{TENANT_ID}/fieldgroups/860ad1b1b35e0a88ecf6df92ebce08335c180313d5805352"
        ],
        "description": "Description of schema.",
        "definitions": {
        },
        "allOf": [
          {
            "$ref": "https://ns.adobe.com/xdm/context/profile"
          },
          {
            "$ref": "https://ns.adobe.com/xdm/context/identitymap"
          },
          {
            "$ref": "https://ns.adobe.com/{TENANT_ID}/fieldgroups/860ad1b1b35e0a88ecf6df92ebce08335c180313d5805352"
          }
        ],
        "meta:class": "https://ns.adobe.com/xdm/context/profile"
      }' 
```

**回應**

成功的響應返回HTTP狀態201（已建立）和包含新建立模式詳細資訊的裝載，包括`$id`、`meta:altId`和`version`。 這些值是只讀的，由方案註冊表指定。

```json
{
  "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/699c1f16821c51086394fef8233d7fdb61e6f5b574b5a230",
  "meta:altId": "_{TENANT}.schemas.699c1f16821c51086394fef8233d7fdb61e6f5b574b5a230",
  "meta:resourceType": "schemas",
  "version": "1.0",
  "title": "Computed Attributes Schema",
  "type": "object",
  "description": "Description of schema.",
  "definitions": {},
  "allOf": [
    {
      "$ref": "https://ns.adobe.com/xdm/context/profile",
      "type": "object",
      "meta:xdmType": "object"
    },
    {
      "$ref": "https://ns.adobe.com/xdm/context/identitymap",
      "type": "object",
      "meta:xdmType": "object"
    },
    {
      "$ref": "https://ns.adobe.com/{TENANT_ID}/fieldgroups/860ad1b1b35e0a88ecf6df92ebce08335c180313d5805352",
      "type": "object",
      "meta:xdmType": "object"
    }
  ],
  "refs": [
    "https://ns.adobe.com/xdm/context/profile",
    "https://ns.adobe.com/xdm/context/identitymap",
    "https://ns.adobe.com/{TENANT_ID}/fieldgroups/860ad1b1b35e0a88ecf6df92ebce08335c180313d5805352"
  ],
  "imsOrg": "{IMS_ORG}",
  "meta:extensible": false,
  "meta:abstract": false,
  "meta:extends": [
    "https://ns.adobe.com/xdm/common/auditable",
    "https://ns.adobe.com/xdm/data/record",
    "https://ns.adobe.com/xdm/context/profile",
    "https://ns.adobe.com/xdm/context/identitymap",
    "https://ns.adobe.com/{TENANT_ID}/fieldgroups/860ad1b1b35e0a88ecf6df92ebce08335c180313d5805352"
  ],
  "meta:xdmType": "object",
  "meta:registryMetadata": {
    "repo:createdDate": 1612385766411,
    "repo:lastModifiedDate": 1612385766411,
    "xdm:createdClientId": "{CLIENT_ID}",
    "xdm:lastModifiedClientId": "{CLIENT_ID}",
    "xdm:createdUserId": "{USER_ID}",
    "xdm:lastModifiedUserId": "{USER_ID}",
    "eTag": "a9c6b5c25c109970ffa5eaeb3db2b47b59c696e1d9407fb39ccf7e48b74b558e",
    "meta:globalLibVersion": "1.18.4"
  },
  "meta:class": "https://ns.adobe.com/xdm/context/profile",
  "meta:containerId": "tenant",
  "meta:sandboxId": "{SANDBOX_ID}",
  "meta:sandboxType": "production",
  "meta:tenantNamespace": "_{TENANT}",
  "meta:immutableTags": [
    "union"
  ]
}
```

## 後續步驟

現在，您已經建立了模式和欄位組，計算屬性將儲存到其中，您可以使用`/computedattributes` API端點建立計算屬性。 有關在API中建立計算屬性的詳細步驟，請遵循[計算屬性API端點指南](ca-api.md)中提供的步驟。
