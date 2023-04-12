---
title: 匯出API端點
description: Schema Registry API中的/export端點可讓您在沙箱之間共用XDM資源。
exl-id: 1dcbfa59-af98-4db5-b6f4-f848e5bf5e81
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '410'
ht-degree: 1%

---

# 匯出端點

中的所有資源 [!DNL Schema Library] 包含在Adobe Experience Platform內的特定沙箱中。 在某些情況下，您可能會想在沙箱和組織之間共用Experience Data Model(XDM)資源。 此 `/rpc/export` 端點 [!DNL Schema Registry] API可讓您為中的任何結構、結構欄位群組或資料類型產生匯出裝載 [!DNL Schema Library]，然後使用該裝載，透過目標沙箱和組織將該資源（及所有相依資源）匯入目標沙箱和組織 [`/rpc/import` 端點](./import.md).

## 快速入門

此 `/rpc/export` 端點是 [[!DNL Schema Registry] API](https://www.adobe.io/experience-platform-apis/references/schema-registry/). 繼續之前，請檢閱 [快速入門手冊](./getting-started.md) 如需相關檔案的連結，請參閱本檔案中讀取範例API呼叫的指南，以及成功呼叫任何Experience PlatformAPI所需的必要標頭重要資訊。

此 `/rpc/export` 端點是遠端程式呼叫(RPC)的一部分，這些呼叫由 [!DNL Schema Registry]. 不同於 [!DNL Schema Registry] API、RPC端點不需要其他標題，例如 `Accept` 或 `Content-Type`，且不使用 `CONTAINER_ID`. 而是必須使用 `/rpc` 命名空間，如下方API呼叫所示。

## 為資源產生匯出裝載 {#export}

對於 [!DNL Schema Library]，您可以向 `/export` 端點，在路徑中提供資源的ID。

**API格式**

```http
GET /rpc/export/{RESOURCE_ID}
```

| 參數 | 說明 |
| --- | --- |
| `{RESOURCE_ID}` | 此 `meta:altId` 或URL編碼 `$id` 匯出的XDM資源。 |

{style="table-layout:auto"}

**要求**

下列要求會擷取 `Restaurant` 欄位群組。

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

成功的回應會傳回物件陣列，代表目標XDM資源及其所有相依資源。 在此範例中，陣列中的第一個物件是租用戶建立的 `Property` 資料類型 `Restaurant` 欄位組採用，而第二個物件為 `Restaurant` 欄位群組本身。 然後，此裝載便可用於 [匯入資源](#import) 進入不同的沙箱或組織。

請注意，資源的租用戶ID的所有例項都會取代為 `<XDM_TENANTID_PLACEHOLDER>`. 這可讓架構註冊表根據資源在後續匯入呼叫中的傳送位置，自動將正確的租用戶ID套用至資源。

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

## 匯入資源 {#import}

從CSV檔案產生匯出裝載後，您可以將該裝載傳送至 `/rpc/import` 端點來產生架構。

請參閱 [匯入端點指南](./import.md) 有關如何從匯出裝載產生綱要的詳細資訊。
