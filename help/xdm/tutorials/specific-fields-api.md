---
title: 使用結構註冊表API將特定欄位新增至結構
description: 了解如何使用Schema Registry API，將預先存在的欄位群組中的個別欄位新增至Experience Data Model(XDM)架構。
source-git-commit: 4bcd949e901c11bb933000f7ae76f17134dda496
workflow-type: tm+mt
source-wordcount: '629'
ht-degree: 2%

---

# 使用Schema Registry API將特定欄位新增至結構

Adobe資料模型(XDM)結構由基本類別組成，其他欄位可透過使用由組織定義的標準欄位群組和自訂欄位群組所包含。

建置架構時，您可能會想使用指定欄位群組中的某些欄位，同時將其他欄位排除在您不需要的相同群組中。 本教學課程說明如何使用Schema Registry API將欄位群組中的個別欄位新增至架構。

>[!NOTE]
>
>如需如何新增和移除Adobe Experience Platform UI中個別結構欄位的資訊，請參閱 [欄位型工作流程](../ui/field-based-workflows.md) （目前為測試版）。

## 先決條件

本教學課程包含呼叫 [結構註冊表API](https://developer.adobe.com/experience-platform-apis/references/schema-registry/). 開始之前，請檢閱 [開發人員指南](../api/getting-started.md) 以取得您需要知道的重要資訊，以便成功呼叫API，包括您的 `{TENANT_ID}`、容器的概念，以及提出要求所需的標題。

## 了解 `meta:refProperty` 欄位

對於任何給定架構，組成其結構的類和欄位組在其下被引用 `allOf` 陣列。 每個元件都以包含 `$ref` 引用元件URI的屬性 `$id`.

下列JSON代表使用單一類別(`experienceevent`)和欄位群組(`experienceevent-all`):

```json
{
  "title": "My Sample Schema",
  "description": "My Sample Description",
  "type": "object",
  "allOf": [
    {
      "$ref": "https://ns.adobe.com/xdm/context/experienceevent"
    },
    {
      "$ref": "https://ns.adobe.com/experience/campaign/experienceevent-all"
    }
  ]
}
```

針對 `allOf` 引用欄位組的陣列，可以添加同級 `meta:refProperty` 欄位，指定應將群組中的哪些欄位納入架構中。

>[!NOTE]
>
>每個欄位都使用JSON指標字串指定，代表其個別欄位群組中欄位的路徑。 字串必須以前導斜線(`/`)，不應包含任何 `properties` 命名空間。 例如: `/_experience/campaign/message/id`.

當包含為字串時， `meta:refProperty` 可以參照群組中的單一欄位。 可使用相同的 `$ref` 值 `meta:refProperty` 值。

```json
{
  "title": "My Sample Schema",
  "description": "An example schema that uses the XDM ExperienceEvent class.",
  "type": "object",
  "allOf": [
    {
      "$ref": "https://ns.adobe.com/xdm/context/experienceevent"
    },
    {
      "$ref": "https://ns.adobe.com/experience/campaign/experienceevent-all",
      "meta:refProperty": "/_experience/campaign/message/id"
    },
    {
      "$ref": "https://ns.adobe.com/experience/campaign/experienceevent-all",
      "meta:refProperty": "/_experience/campaign/message/size"
    }
  ]
}
```

或者， `meta:refProperty` 可作為陣列提供，讓您指定多個欄位以納入單一內指定群組的多個欄位 `allOf` 清單項目：

```json
{
  "title": "My Sample Schema",
  "description": "An example schema that uses the XDM ExperienceEvent class.",
  "type": "object",
  "allOf": [
    {
      "$ref": "https://ns.adobe.com/xdm/context/experienceevent"
    },
    {
      "$ref": "https://ns.adobe.com/experience/campaign/experienceevent-all",
      "meta:refProperty": [
        "/_experience/campaign/message/id",
        "/_experience/campaign/message/size",
        "/_experience/campaign/message/variant"
      ]
    }
  ]
}
```

## 使用PUT操作添加欄位

您可以使用PUT請求來重寫整個架構，並設定要在下加入的欄位 `allOf`.

**API格式**

```http
PUT /tenant/schemas/{SCHEMA_ID}
```

| 參數 | 說明 |
| --- | --- |
| `{SCHEMA_ID}` | 此 `meta:altId` 或URL編碼 `$id` 要重寫的結構。 |

**要求**

下列請求會更新下方欄位群組中包含的特定欄位 `allOf` 陣列。

```shell
curl -X PUT \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.d5cc04eb8d50190001287e4c869ebe67 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
        "title": "My Sample Schema",
        "description": "My Sample Description",
        "type": "object",
        "allOf": [
          {
            "$ref": "https://ns.adobe.com/xdm/context/experienceevent"
          },
          {
            "$ref": "https://ns.adobe.com/experience/campaign/experienceevent-all",
            "meta:refProperty": [
              "/_experience/campaign/message/id",
              "/_experience/campaign/message/size",
              "/_experience/campaign/message/variant"
            ]
          }
        ]
      }'
```

**回應**

成功的回應會傳回更新架構的詳細資訊。

```json
{
  "title": "My Sample Schema",
  "description": "My Sample Description",
  "type": "object",
  "allOf": [
    {
      "$ref": "https://ns.adobe.com/xdm/context/experienceevent"
    },
    {
      "$ref": "https://ns.adobe.com/experience/campaign/experienceevent-all",
      "meta:refProperty": [
        "/_experience/campaign/message/id",
        "/_experience/campaign/message/size",
        "/_experience/campaign/message/variant"
      ]
    }
  ],
  "meta:class": "https://ns.adobe.com/xdm/context/experienceevent",
  "meta:abstract": false,
  "meta:extensible": false,
  "meta:extends": [
      "https://ns.adobe.com/xdm/context/experienceevent",
      "https://ns.adobe.com/xdm/data/time-series"
  ],
  "meta:containerId": "tenant",
  "imsOrg": "{ORG_ID}",
  "meta:altId": "_{TENANT_ID}.schemas.d5cc04eb8d50190001287e4c869ebe67",
  "meta:xdmType": "object",
  "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/d5cc04eb8d50190001287e4c869ebe67",
  "version": "1.0",
  "meta:resourceType": "schemas",
  "meta:registryMetadata": {
      "repo:createDate": 1552088461236,
      "repo:lastModifiedDate": 1552088470592,
      "xdm:createdClientId": "{CREATED_CLIENT}",
      "xdm:repositoryCreatedBy": "{CREATED_BY}"
  }
}
```

>[!NOTE]
>
>如需結構PUT請求的詳細資訊，請參閱 [schemas endpoint指南](../api/schemas.md#put).

## 使用PATCH操作添加欄位

您可以使用PATCH請求將個別欄位新增至架構，而不會覆寫其他欄位。 結構註冊表支援所有標準JSON修補程式操作，包括 `add`, `remove`，和 `replace`. 如需JSON修補程式的詳細資訊，請參閱 [API基礎指南](../../landing/api-fundamentals.md#json-patch).

**API格式**

```http
PATCH /tenant/schemas/{SCHEMA_ID}
```

| 參數 | 說明 |
| --- | --- |
| `{SCHEMA_ID}` | 此 `meta:altId` 或URL編碼 `$id` 要重寫的結構。 |

**要求**

下列要求會將新物件新增至結構的 `allOf` 陣列，指定要新增的欄位。

```shell
curl -X PATCH \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.d5cc04eb8d50190001287e4c869ebe67 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '[
        {
          "op": "add",
          "path": "/allOf/-",
          "value":  {
            "$ref": "https://ns.adobe.com/experience/campaign/experienceevent-all",
            "meta:refProperty": [
              "/_experience/campaign/message/id",
              "/_experience/campaign/message/size",
              "/_experience/campaign/message/variant"
            ]
          }
        }
      ]'
```

**回應**

成功的回應會傳回更新架構的詳細資訊。

```json
{
  "title": "My Sample Schema",
  "description": "My Sample Description",
  "type": "object",
  "allOf": [
    {
      "$ref": "https://ns.adobe.com/xdm/context/experienceevent"
    },
    {
      "$ref": "https://ns.adobe.com/experience/campaign/experienceevent-all",
      "meta:refProperty": [
        "/_experience/campaign/message/id",
        "/_experience/campaign/message/size",
        "/_experience/campaign/message/variant"
      ]
    }
  ],
  "meta:class": "https://ns.adobe.com/xdm/context/experienceevent",
  "meta:abstract": false,
  "meta:extensible": false,
  "meta:extends": [
      "https://ns.adobe.com/xdm/context/experienceevent",
      "https://ns.adobe.com/xdm/data/time-series"
  ],
  "meta:containerId": "tenant",
  "imsOrg": "{ORG_ID}",
  "meta:altId": "_{TENANT_ID}.schemas.d5cc04eb8d50190001287e4c869ebe67",
  "meta:xdmType": "object",
  "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/d5cc04eb8d50190001287e4c869ebe67",
  "version": "1.0",
  "meta:resourceType": "schemas",
  "meta:registryMetadata": {
      "repo:createDate": 1552088461236,
      "repo:lastModifiedDate": 1552088470592,
      "xdm:createdClientId": "{CREATED_CLIENT}",
      "xdm:repositoryCreatedBy": "{CREATED_BY}"
  }
}
```

>[!NOTE]
>
>如需結構PATCH請求的詳細資訊，請參閱 [schemas endpoint指南](../api/schemas.md#patch).

## 後續步驟

本指南說明如何使用API呼叫，將現有欄位群組中的個別欄位新增至結構。 如需如何在Platform UI中執行類似欄位式工作的詳細資訊，請參閱 [欄位型工作流程](../ui/field-based-workflows.md).

如需Schema Registry API功能的詳細資訊，請參閱 [API概述](../api/overview.md) 以取得端點和程式的完整清單。
