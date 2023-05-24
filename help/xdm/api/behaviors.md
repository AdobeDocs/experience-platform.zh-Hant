---
keywords: Experience Platform；主題；熱門主題；api;API;XDM;XDM系統；經驗資料模型；經驗資料模型；資料模型；資料模型；資料模型；模式註冊；模式註冊；行為；行為；行為；行為；行為；行為；
solution: Experience Platform
title: 行為API終結點
description: 架構註冊表API中的/behaviors終結點允許您檢索全局容器中的所有可用行為。
exl-id: 3b45431f-1d55-4279-8b62-9b27863885ec
source-git-commit: 983682489e2c0e70069dbf495ab90fc9555aae2d
workflow-type: tm+mt
source-wordcount: '425'
ht-degree: 2%

---

# 行為端點

在經驗資料模型(XDM)中，行為定義模式描述的資料的性質。 每個XDM類必須引用特定行為，使用該類的所有架構都將繼承該行為。 對於平台中幾乎所有的使用情形，有兩種可用行為：

* **[!UICONTROL 記錄]**:提供有關主題屬性的資訊。 主題可以是組織或個人。
* **[!UICONTROL 時間序列]**:提供記錄主題直接或間接執行操作時系統的快照。

>[!NOTE]
>
>平台中有一些使用案例要求使用不採用上述任何一種行為的架構。 對於這些情況，有第三種「臨時」行為。 請參閱上的教程 [建立即席模式](../tutorials/ad-hoc.md) 的子菜單。
>
>有關資料行為如何影響模式組合的更一般資訊，請參閱上的指南 [架構組合基礎](../schema/composition.md)。

的 `/behaviors` 端點 [!DNL Schema Registry] API允許您查看 `global` 容器。

## 快速入門

本指南中使用的端點是 [[!DNL Schema Registry] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/behavior-registry.yaml)。 在繼續之前，請查看 [入門指南](./getting-started.md) 有關相關文檔的連結、閱讀本文檔中示例API調用的指南，以及有關成功調用任何Experience PlatformAPI所需標頭的重要資訊。

## 檢索行為清單 {#list}

可通過向以下對象發出GET請求來檢索所有可用行為的清單： `/behaviors` 端點。

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

通過在GET請求路徑中提供特定行為的ID，可以查找特定行為 `/behaviors` 端點。

**API格式**

```http
GET /global/behaviors/{BEHAVIOR_ID}
```

| 參數 | 說明 |
| --- | --- |
| `{BEHAVIOR_ID}` | 的 `meta:altId` 或URL編碼 `$id` 你想查的行為。 |

{style="table-layout:auto"}

**要求**

以下請求通過提供記錄行為的詳細資訊 `meta:altId` 的子菜單。

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

成功的響應將返回行為的詳細資訊，包括其版本、說明以及行為提供給使用它的類的屬性。

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

本指南介紹了 `/behaviors` 端點 [!DNL Schema Registry] API。 要瞭解如何使用API為類分配行為，請參見 [類終結點指南](./classes.md)。
