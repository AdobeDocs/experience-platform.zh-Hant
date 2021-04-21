---
keywords: Experience Platform;home；熱門主題；api;API;XDM;XDM系統；體驗資料模型；體驗資料模型；資料模型；模式註冊；模式註冊；行為；行為；行為；行為；
solution: Experience Platform
title: 行為API端點
description: 架構註冊表API中的/behaviors端點可讓您擷取全域容器中的所有可用行為。
topic-legacy: developer guide
exl-id: 3b45431f-1d55-4279-8b62-9b27863885ec
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '423'
ht-degree: 2%

---

# 行為端點

在Experience Data Model(XDM)中，行為會定義模式所描述的資料性質。 每個XDM類都必須引用特定的行為，使用該類的所有方案都將繼承該行為。 在Platform中，幾乎所有的使用案例中，有兩種可用的行為：

* **[!UICONTROL Record]**:提供主題屬性的相關資訊。主題可以是組織或個人。
* **[!UICONTROL Time-series]**:提供記錄主體直接或間接採取操作時系統的快照。

>[!NOTE]
>
>在Platform中，有些使用案例需要使用不採用上述任一行為的架構。 針對這些情況，提供第三種「臨機」行為。 如需詳細資訊，請參閱[建立臨機架構](../tutorials/ad-hoc.md)的教學課程。
>
>有關資料行為如何影響模式組合的更一般資訊，請參閱[架構組合基礎](../schema/composition.md)的指南。

[!DNL Schema Registry] API中的`/behaviors`端點可讓您在`global`容器中檢視可用行為。

## 快速入門

本指南中使用的端點是[[!DNL Schema Registry] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/behavior-registry.yaml)的一部分。 在繼續之前，請先閱讀[快速入門手冊](./getting-started.md)，以取得相關檔案的連結、閱讀本檔案中範例API呼叫的指南，以及成功呼叫任何Experience PlatformAPI所需之必要標題的重要資訊。

## 擷取行為清單{#list}

通過向`/behaviors`端點發出GET請求，可以檢索所有可用行為的清單。

**API格式**

```http
GET /global/behaviors
```

**要求**

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/global/behaviors \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Accept: application/vnd.adobe.xed-id+json'
```

**回應**

```json
{
    "results": [
        {
            "$id": "https://ns.adobe.com/xdm/data/record",
            "meta:altId": "_xdm.data.record",
            "version": "1.16.4",
            "title": "Record Schema"
        },
        {
            "$id": "https://ns.adobe.com/xdm/data/adhoc",
            "meta:altId": "_xdm.data.adhoc",
            "version": "1.16.4",
            "title": "Ad Hoc Schema"
        },
        {
            "$id": "https://ns.adobe.com/xdm/data/time-series",
            "meta:altId": "_xdm.data.time-series",
            "version": "1.16.4",
            "title": "Time-series Schema"
        }
    ],
    "_page": {
        "orderby": "updated",
        "next": null,
        "count": 3
    },
    "_links": {
        "next": null
    }
}
```

## 查找行為{#lookup}

您可在`/behaviors`端點的GET請求路徑中提供其ID，以查找特定行為。

**API格式**

```http
GET /global/behaviors/{BEHAVIOR_ID}
```

| 參數 | 說明 |
| --- | --- |
| `{BEHAVIOR_ID}` | 您要查看之行為的`meta:altId`或URL編碼`$id`。 |

**要求**

以下請求在請求路徑中提供記錄行為的`meta:altId`，以檢索記錄行為的詳細資訊。

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/global/behaviors/_xdm.data.record \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Accept: application/vnd.adobe.xed+json;version=1'
```

**回應**

成功的響應返回行為的詳細資訊，包括其版本、說明以及行為提供給使用行為的類的屬性。

```json
{
    "$id": "https://ns.adobe.com/xdm/data/record",
    "meta:altId": "_xdm.data.record",
    "meta:resourceType": "behaviors",
    "version": "1.16.4",
    "title": "Record Schema",
    "type": "object",
    "description": "Used to indicate the behavior of record data semantic when composed into data schemas.",
    "definitions": {
        "record": {
            "properties": {
                "_id": {
                    "title": "Identifier",
                    "type": "string",
                    "format": "uri-reference",
                    "description": "A unique identifier for the record.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "@id"
                }
            }
        }
    },
    "allOf": [
        {
            "$ref": "#/definitions/record",
            "type": "object",
            "meta:xdmType": "object"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/common/extensible#/definitions/@context",
            "type": "object",
            "meta:xdmType": "object"
        }
    ],
    "meta:extensible": true,
    "meta:abstract": true,
    "meta:xdmType": "object",
    "meta:status": "stable",
    "$schema": "http://json-schema.org/draft-06/schema#",
    "meta:registryMetadata": {
        "repo:createdDate": 1606266789446,
        "repo:lastModifiedDate": 1606266789446,
        "eTag": "2cc114a54949a9668fe2ad046ccece59192e1bfa28f14e5ac7c893acb7820ba2",
        "meta:globalLibVersion": "1.16.4"
    }
}
```

## 後續步驟

本指南涵蓋[!DNL Schema Registry] API中`/behaviors`端點的使用。 要瞭解如何使用API為類指定行為，請參見[類端點指南](./classes.md)。
