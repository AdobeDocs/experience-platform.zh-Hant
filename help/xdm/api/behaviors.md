---
keywords: Experience Platform；首頁；熱門主題；API; XDM; XDM系統；體驗資料模型；體驗資料模型；資料模型；資料模型；結構註冊表；結構註冊表；行為；行為；行為；行為；行為；
solution: Experience Platform
title: 行為API端點
description: 架構註冊表API中的/behaviors端點可讓您擷取全域容器中所有可用的行為。
exl-id: 3b45431f-1d55-4279-8b62-9b27863885ec
source-git-commit: 983682489e2c0e70069dbf495ab90fc9555aae2d
workflow-type: tm+mt
source-wordcount: '425'
ht-degree: 2%

---

# 行為端點

在Experience Data Model(XDM)中，行為會定義結構描述的資料性質。 每個XDM類別都必須參考特定行為，採用該類別的所有結構都將繼承該行為。 在Platform的幾乎所有使用案例中，有兩種可用的行為：

* **[!UICONTROL 記錄]**:提供主題屬性的相關資訊。 主題可以是組織或個人。
* **[!UICONTROL 時間序列]**:提供記錄主體直接或間接執行操作時系統的快照。

>[!NOTE]
>
>在Platform中，有些使用案例需要使用結構，而不採用上述任一行為。 針對這些情況，提供第三種「臨機」行為。 請參閱 [建立臨機結構](../tutorials/ad-hoc.md) 以取得更多資訊。
>
>有關資料行為如何影響架構構成的更一般資訊，請參閱 [綱要構成基本知識](../schema/composition.md).

此 `/behaviors` 端點 [!DNL Schema Registry] API可讓您檢視 `global` 容器。

## 快速入門

本指南中使用的端點屬於 [[!DNL Schema Registry] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/behavior-registry.yaml). 繼續之前，請檢閱 [快速入門手冊](./getting-started.md) 如需相關檔案的連結，請參閱本檔案中讀取範例API呼叫的指南，以及成功呼叫任何Experience PlatformAPI所需的必要標頭重要資訊。

## 擷取行為清單 {#list}

您可以向提出GET要求，以擷取所有可用行為的清單 `/behaviors` 端點。

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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

## 查找行為 {#lookup}

您可以在GET要求的路徑中提供ID給 `/behaviors` 端點。

**API格式**

```http
GET /global/behaviors/{BEHAVIOR_ID}
```

| 參數 | 說明 |
| --- | --- |
| `{BEHAVIOR_ID}` | 此 `meta:altId` 或URL編碼 `$id` 你想查的行為。 |

{style="table-layout:auto"}

**要求**

下列請求會提供記錄行為的 `meta:altId` 在請求路徑中。

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/global/behaviors/_xdm.data.record \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Accept: application/vnd.adobe.xed+json;version=1'
```

**回應**

成功的響應返回行為的詳細資訊，包括其版本、說明以及行為提供給採用它的類的屬性。

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

本指南說明如何使用 `/behaviors` 端點 [!DNL Schema Registry] API。 若要了解如何使用API將行為指派給類別，請參閱 [classes endpoint guide](./classes.md).
