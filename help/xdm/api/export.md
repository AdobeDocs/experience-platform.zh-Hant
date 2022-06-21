---
title: 導出API終結點
description: 架構註冊表API中的/export終結點允許您在沙箱之間共用XDM資源。
source-git-commit: 2a58236031834bbe298576e2fcab54b04ec16ac3
workflow-type: tm+mt
source-wordcount: '414'
ht-degree: 2%

---

# 導出終結點

所有資源 [!DNL Schema Library] 都在Adobe Experience Platform的一個沙箱裡。 在某些情況下，您可能希望在沙箱和組織之間共用經驗資料模型(XDM)資源。 的 `/rpc/export` 端點 [!DNL Schema Registry] API允許您為中的任何架構、架構欄位組或資料類型生成導出負載 [!DNL Schema Library]，然後使用該負載通過目標沙箱和組織將該資源（以及所有從屬資源）導入到目標沙箱和組織 [`/rpc/import` 端點](./import.md)。

## 快速入門

的 `/rpc/export` 端點是 [[!DNL Schema Registry] API](https://www.adobe.io/experience-platform-apis/references/schema-registry/)。 在繼續之前，請查看 [入門指南](./getting-started.md) 有關相關文檔的連結、閱讀本文檔中示例API調用的指南，以及有關成功調用任何Experience PlatformAPI所需標頭的重要資訊。

的 `/rpc/export` endpoint是遠程過程調用(RPC)的一部分，該調用由 [!DNL Schema Registry]。 不同於 [!DNL Schema Registry] API、RPC終結點不需要像 `Accept` 或 `Content-Type`，並且不使用 `CONTAINER_ID`。 相反，他們必須使用 `/rpc` 命名空間，如下面的API調用中所示。

## 為資源生成導出負載 {#export}

對於中的任何現有架構、欄位組或資料類型 [!DNL Schema Library]，可通過向GET請求生成導出負載 `/export` 終結點，提供路徑中資源的ID。

**API格式**

```http
GET /rpc/export/{RESOURCE_ID}
```

| 參數 | 說明 |
| --- | --- |
| `{RESOURCE_ID}` | 的 `meta:altId` 或URL編碼 `$id` 要導出的XDM資源。 |

{style=&quot;table-layout:auto&quot;}

**要求**

以下請求檢索的導出負載 `Restaurant` 欄位組。

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/rpc/export/_{TENANT_ID}.mixins.922a56b58c6b4e4aeb49e577ec82752106ffe8971b23b4d9 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Accept: application/vnd.adobe.xdm-link+json'
```

**回應**

成功的響應返回一組對象，這些對象表示目標XDM資源及其所有相關資源。 在此示例中，陣列中的第一個對象是租戶建立的 `Property` 資料類型 `Restaurant` 欄位組雇用，而第二個對象是 `Restaurant` 欄位組本身。 然後，此負載可用於 [導入資源](#import) 進入另一個沙箱或IMS組織。

請注意，資源的租戶ID的所有實例都替換為 `<XDM_TENANTID_PLACEHOLDER>`。 這允許架構註冊表根據資源在後續導入調用中的發送位置自動將正確的租戶ID應用到資源。

```json
[
    {
        "$id": "https://ns.adobe.com/<XDM_TENANTID_PLACEHOLDER>/datatypes/fc07162ee7ca8d18e074a3bb50c3938c76160bf6040e8495",
        "meta:altId": "_<XDM_TENANTID_PLACEHOLDER>.datatypes.fc07162ee7ca8d18e074a3bb50c3938c76160bf6040e8495",
        "meta:resourceType": "datatypes",
        "version": "1.0",
        "title": "Property",
        "type": "object",
        "description": "",
        "definitions": {
            "customFields": {
                "properties": {
                    "propertyId": {
                        "title": "Property ID",
                        "description": "ID for a company-owned property.",
                        "type": "string",
                        "isRequired": false,
                        "meta:ui": {
                            "ref": [
                                "schema://5fbc29ec292534000055dd55",
                                "#/definitions/customFields"
                            ],
                            "path": "{}._<XDM_TENANTID_PLACEHOLDER>{}.property{}.propertyId",
                            "editable": true,
                            "generateDate": 1606168175975
                        },
                        "meta:xdmType": "string"
                    },
                    "jurisdiction": {
                        "title": "Jurisdiction",
                        "description": "",
                        "type": "string",
                        "isRequired": false,
                        "enum": [
                            "NA",
                            "UK",
                            "EU"
                        ],
                        "meta:enum": {
                            "NA": "North America",
                            "UK": "United Kingdom",
                            "EU": "European Union"
                        },
                        "meta:ui": {
                            "ref": [
                                "schema://5fbc29ec292534000055dd55",
                                "#/definitions/customFields"
                            ],
                            "path": "{}._<XDM_TENANTID_PLACEHOLDER>{}.property{}.jurisdiction",
                            "editable": true,
                            "generateDate": 1606168175975
                        },
                        "meta:xdmType": "string"
                    }
                }
            }
        },
        "allOf": [
            {
                "$ref": "#/definitions/customFields",
                "type": "object",
                "meta:xdmType": "object"
            }
        ],
        "meta:extensible": true,
        "meta:abstract": true,
        "meta:xdmType": "object",
        "meta:sandboxId": "ff0f6870-c46d-11e9-8ca3-036939a64204",
        "meta:sandboxType": "production"
    },
    {
        "$id": "https://ns.adobe.com/<XDM_TENANTID_PLACEHOLDER>/mixins/922a56b58c6b4e4aeb49e577ec82752106ffe8971b23b4d9",
        "meta:altId": "_<XDM_TENANTID_PLACEHOLDER>.mixins.922a56b58c6b4e4aeb49e577ec82752106ffe8971b23b4d9",
        "meta:resourceType": "mixins",
        "version": "1.0",
        "title": "Restaurant",
        "type": "object",
        "description": "",
        "definitions": {
            "customFields": {
                "type": "object",
                "properties": {
                    "_<XDM_TENANTID_PLACEHOLDER>": {
                        "type": "object",
                        "properties": {
                            "capacity": {
                                "title": "Capacity",
                                "description": "Restaurant capacity",
                                "type": "string",
                                "isRequired": false,
                                "meta:xdmType": "string"
                            },
                            "kitchen": {
                                "title": "Kitchen Style",
                                "description": "Style of kitchen",
                                "type": "string",
                                "isRequired": false,
                                "meta:xdmType": "string"
                            },
                            "rating": {
                                "title": "Rating",
                                "description": "",
                                "type": "integer",
                                "isRequired": false,
                                "meta:xdmType": "int"
                            },
                            "property": {
                                "title": "Property",
                                "description": "",
                                "$ref": "https://ns.adobe.com/<XDM_TENANTID_PLACEHOLDER>/datatypes/fc07162ee7ca8d18e074a3bb50c3938c76160bf6040e8495",
                                "type": "object",
                                "meta:xdmType": "object"
                            }
                        },
                        "meta:xdmType": "object"
                    }
                },
                "meta:xdmType": "object"
            }
        },
        "allOf": [
            {
                "$ref": "#/definitions/customFields",
                "type": "object",
                "meta:xdmType": "object"
            }
        ],
        "meta:extensible": true,
        "meta:abstract": true,
        "meta:intendedToExtend": [],
        "meta:xdmType": "object",
        "meta:sandboxId": "ff0f6870-c46d-11e9-8ca3-036939a64204",
        "meta:sandboxType": "production"
    }
]
```

## 導入資源 {#import}

從CSV檔案生成導出負載後，可以將該負載發送到 `/rpc/import` 終結點以生成架構。

查看 [導入終結點指南](./import.md) 有關如何從導出負載生成架構的詳細資訊。
