---
keywords: Experience Platform;home;popular topics;api;API;XDM;XDM system;;experience data model;Experience data model;Experience Data Model;data model;Data Model;schema registry;Schema Registry;lookup;Lookup;get;GET
solution: Experience Platform
title: 查找資源
description: 您可以在方案註冊表API中尋找特定資源，方法是提出GET請求，該請求在請求路徑中包含資源的$id（URL編碼URI）。
topic: developer guide
translation-type: tm+mt
source-git-commit: 74a4a3cc713cc068be30379e8ee11572f8bb0c63
workflow-type: tm+mt
source-wordcount: '203'
ht-degree: 2%

---


# 查找資源

您可以透過提出GET請求，在請求路徑中包含資 `$id` 源的（URL編碼URI），來尋找特定資源。

**API格式**

```http
GET /{CONTAINER_ID}/{RESOURCE_TYPE}/{RESOURCE_ID} 
```

| 參數 | 說明 |
| --- | --- |
| `{CONTAINER_ID}` | 資源所在的容器（「全域」或「租用戶」）。 |
| `{RESOURCE_TYPE}` | 要從中檢索的資源類型 [!DNL Schema Library]。 有效類 `datatypes`型有 `mixins`、 `schemas`和 `classes`。 |
| `{RESOURCE_ID}` | URL編碼的 `$id` URI或 `meta:altId` 資源。 |

**請求**

```SHELL
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/global/mixins/https%3A%2F%2Fns.adobe.com%2Fxdm%2Fcontext%2Fprofile-person-details \
  -H 'Accept: application/vnd.adobe.xed+json; version=1' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

資源查閱請求需 `version` 要包含在「接受」標題中。 以下「接受」題頭可用於查找：

| 接受 | 說明 |
| ------- | ------------ |
| `application/vnd.adobe.xed+json; version={MAJOR_VERSION}` | Raw含 `$ref` 和 `allOf`，有標題和說明。 |
| `application/vnd.adobe.xed-full+json; version={MAJOR_VERSION}` | `$ref` 而且 `allOf` 有標題和說明。 |
| `application/vnd.adobe.xed-notext+json; version={MAJOR_VERSION}` | Raw含 `$ref` 和 `allOf`，無標題或說明。 |
| `application/vnd.adobe.xed-full-notext+json; version={MAJOR_VERSION}` | `$ref` 並解 `allOf` 決，沒有標題或說明。 |
| `application/vnd.adobe.xed-full-desc+json; version={MAJOR_VERSION}` | `$ref` 和已解 `allOf` 析的包含描述符。 |

>[!NOTE]
>
>如果僅提 `major` 供版本（1、2、3等），註冊表將自動返回最 `minor` 新版本（.1、.2、.3等）。

**回應**

成功的響應返回資源的詳細資訊。 傳回的欄位取決於請求中傳送的「接受」標題。 嘗試不同的「接受」標題，以比較回應，並判斷哪個標題最適合您的使用案例。

```JSON
{
    "$id": "https://ns.adobe.com/xdm/context/profile-person-details",
    "title": "Profile Person Details",
    "type": "object",
    "meta:extensible": true,
    "meta:abstract": true,
    "meta:intendedToExtend": [
        "https://ns.adobe.com/xdm/context/profile"
    ],
    "description": "Profile person details including naming, gender etc.",
    "definitions": {
        "profile-person-details": {
            "properties": {
                "person": {
                    "title": "Person",
                    "$ref": "https://ns.adobe.com/xdm/context/person",
                    "description": "An individual actor, contact, or owner.",
                    "meta:xdmField": "xdm:person"
                }
            }
        }
    },
    "allOf": [
        {
            "$ref": "https://ns.adobe.com/xdm/common/extensible#/definitions/@context"
        },
        {
            "$ref": "#/definitions/profile-person-details"
        }
    ],
    "meta:xdmId": "https://ns.adobe.com/xdm/context/profile-person-details",
    "meta:altId": "_xdm.context.profile-person-details",
    "meta:xdmType": "object",
    "meta:status": "experimental",
    "version": "1",
    "$schema": "http://json-schema.org/draft-06/schema#",
    "meta:resourceType": "mixins",
    "meta:registryMetadata": {
        "repo:createDate": 1551745787442,
        "repo:lastModifiedDate": 1551745787442
    }
}
```
