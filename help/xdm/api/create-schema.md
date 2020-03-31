---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 建立架構
topic: developer guide
translation-type: tm+mt
source-git-commit: 162316c3b908ffa87d8df4dff72e26ba237993db

---


# 建立架構

架構可視為您要匯入Experience Platform之資料的藍圖。 每個模式由類和零個或多個混合組成。 換言之，您不必新增混音來定義結構，但在大多數情況下，至少會使用一個混音。

架構構成過程從分配類開始。 該類定義資料的關鍵行為方面（記錄或時間序列），以及描述將接收的資料所需的最小欄位。

**API格式**

```http
POST /tenant/schemas
```

**請求**

請求必須包含 `allOf` 引用類的 `$id` 屬性。 此屬性定義了方案將實施的「基本類」。 在此範例中，基本類別是先前建立的「屬性資訊」類別。

```SHELL
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas \
  -H 'Authorization: Bearer {ACCESS_TOKEN' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "title":"Property Information",
        "description": "Property-related information.",
        "type": "object",
        "allOf": [ 
          { 
            "$ref": "https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590" 
          } 
        ]
      }'
```

| 屬性 | 說明 |
| --- | --- |
| `allOf > $ref` | 新 `$id` 架構將實施的類的值。 |

**回應**

成功的回應會傳回HTTP狀態201（已建立）和包含新建架構詳細資訊的裝載，包括 `$id`、 `meta:altId`和 `version`。 這些值是只讀的，由方案註冊表指定。

```JSON
{
    "title": "Property Information",
    "description": "Property-related information.",
    "type": "object",
    "allOf": [
        {
            "$ref": "https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590"
        }
    ],
    "meta:class": "https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590",
    "meta:abstract": false,
    "meta:extensible": false,
    "meta:extends": [
        "https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590",
        "https://ns.adobe.com/xdm/data/record"
    ],
    "meta:containerId": "tenant",
    "imsOrg": "{IMS_ORG}",
    "meta:altId": "_{TENANT_ID}.schemas.d5cc04eb8d50190001287e4c869ebe67",
    "meta:xdmType": "object",
    "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/d5cc04eb8d50190001287e4c869ebe67",
    "version": "1.0",
    "meta:resourceType": "schemas",
    "meta:registryMetadata": {
        "repo:createDate": 1552088461236,
        "repo:lastModifiedDate": 1552088461236,
        "xdm:createdClientId": "{CREATED_CLIENT}",
        "xdm:repositoryCreatedBy": "{CREATED_BY}"
    }
}
```

執行GET請求以列出租用戶容器中的所有結構，現在會包含屬性資訊結構，或者您可以使用URL編碼 `$id` URI執行查閱(GET)請求，以直接檢視新結構。 請記得在「接 `version` 受」標題中包含所有查閱請求。
