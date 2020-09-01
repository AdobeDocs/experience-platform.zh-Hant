---
keywords: Experience Platform;home;popular topics;api;API;XDM;XDM system;;experience data model;Experience data model;Experience Data Model;data model;Data Model;schema registry;Schema Registry;datatype;Datatype;data type;Data type;create
solution: Experience Platform
title: 建立資料類型
topic: developer guide
description: '當您的組織希望以多種方式使用常見的資料結構時，您可能希望定義資料類型。 資料類型允許一致地使用多欄位結構，其靈活性比混合要大，因為通過將它們添加為欄位的「類型」，它們可以包含在模式中的任意位置。 '
translation-type: tm+mt
source-git-commit: ed1f2fdac0f9c977d11c867327c084353c1bcd0f
workflow-type: tm+mt
source-wordcount: '256'
ht-degree: 0%

---


# 建立資料類型

當您的組織希望以多種方式使用常見的資料結構時，您可能希望定義資料類型。 資料類型允許一致地使用多欄位結構，其靈活性比混合要大，因為可以通過將它們作為欄位添加到模式中的任意 `type` 位置。

換言之，資料類型允許您定義對象層次一次，並以與任何其他標量類型相同的方式在欄位中引用它。

**API格式**

```http
POST /tenant/datatypes
```

**請求**

定義資料類型不需要 `meta:extends` 或欄 `meta:intendedToExtend` 位，也不需要巢狀化欄位以避免衝突。

```SHELL
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/datatypes \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "title":"Property Construction",
        "description":"Information related to the property construction",
        "type":"object",
        "properties": {
          "yearBuilt": {
            "type":"integer",
            "title": "Year Built",
            "description": "The year the property was constructed."
          },
          "propertyType": {
            "type":"string",
            "title": "Property Type",
            "description": "Type of building or structure in which the property exists.",
            "enum": [
              "freeStanding",
              "mall",
              "shoppingCenter"
            ],
            "meta:enum": {
              "freeStanding": "Free Standing Building",
              "mall": "Mall Space",
              "shoppingCentre": "Shopping Center"
            }
          }
        } 
      }'
```

**回應**

成功的回應會傳回HTTP狀態201（已建立）和包含新建立資料類型詳細資訊的裝載，包括 `$id`、 `meta:altId`和 `version`。 這三個值是唯讀的，由指定 [!DNL Schema Registry]。

```JSON
{
    "title": "Property Construction",
    "description": "Information related to the property construction",
    "type": "object",
    "properties": {
        "yearBuilt": {
            "type": "integer",
            "title": "Year Built",
            "description": "The year the property was constructed.",
            "meta:xdmType": "int"
        },
        "constructionType": {
            "type": "string",
            "title": "Construction Type",
            "description": "Type of building or structure in which the property exists.",
            "enum": [
                "freeStanding",
                "mall",
                "shoppingCenter"
            ],
            "meta:enum": {
                "freeStanding": "Free Standing Building",
                "mall": "Mall Space",
                "shoppingCentre": "Shopping Center"
            },
            "meta:xdmType": "string"
        }
    },
    "meta:abstract": true,
    "meta:extensible": true,
    "meta:containerId": "tenant",
    "imsOrg": "{IMS_ORG}",
    "meta:altId": "_{TENANT_ID}.datatypes.24c643f618647344606222c494bd0102",
    "meta:xdmType": "object",
    "$id": "https://ns.adobe.com/{TENANT_ID}/datatypes/24c643f618647344606222c494bd0102",
    "version": "1.0",
    "meta:resourceType": "datatypes",
    "meta:registryMetadata": {
        "repo:createDate": 1552087079285,
        "repo:lastModifiedDate": 1552087079285,
        "xdm:createdClientId": "{CREATED_CLIENT}",
        "xdm:repositoryCreatedBy": "{CREATED_BY}"
    }
}
```

執行GET請求以列出租用戶容器中的所有資料類型，現在會包含「屬性建構」資料類型。 您也可以使用URL編碼的 `$id` URI來執行查閱(GET)請求，以直接檢視新的資料類型。 請務必在查閱請 `version` 求的「接受」標題中加入。
