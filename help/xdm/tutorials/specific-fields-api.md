---
title: 使用架構註冊表API將特定欄位添加到架構
description: 瞭解如何使用架構註冊表API將預先存在的欄位組中的各個欄位添加到體驗資料模型(XDM)架構中。
exl-id: 696cce2b-bbde-416a-9f52-12ab4da9c2c6
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '629'
ht-degree: 2%

---

# 使用架構註冊表API將特定欄位添加到架構

體驗資料模型(XDM)方案由基類組成，通過使用由Adobe定義的標準欄位組和由組織定義的自定義欄位組包括附加欄位。

在構建架構時，您可能希望使用給定欄位組中的某些欄位，而將其他欄位排除在不需要的同一組中。 本教程介紹如何使用架構註冊表API將欄位組中的各個欄位添加到架構。

>[!NOTE]
>
>有關如何在Adobe Experience PlatformUI中添加和刪除單個架構欄位的資訊，請參見上的指南 [基於欄位的工作流](../ui/field-based-workflows.md) （當前為beta）。

## 先決條件

本教程涉及調用 [架構註冊表API](https://developer.adobe.com/experience-platform-apis/references/schema-registry/)。 開始前，請查看 [開發者指南](../api/getting-started.md) 要成功調用API，包括 `{TENANT_ID}`、容器的概念以及發出請求所需的標頭。

## 瞭解 `meta:refProperty` 場

對於任何給定架構，組成其結構的類和欄位組在其下面被引用 `allOf` 陣列。 每個元件被表示為包含 `$ref` 引用元件URI的屬性 `$id`。

以下JSON表示使用單個類的簡化架構(`experienceevent`)和欄位組(`experienceevent-all`):

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

對於中的任何對象 `allOf` 引用欄位組的陣列，您可以添加同級 `meta:refProperty` 欄位，以指定在架構中應包括組中的哪些欄位。

>[!NOTE]
>
>每個欄位都使用JSON指針字串指定，該字串表示各個欄位組中欄位的路徑。 字串必須以前導斜槓(`/`)，不應包括 `properties` 命名空間。 例如: `/_experience/campaign/message/id`.

當包含為字串時， `meta:refProperty` 可以引用組中的單個欄位。 使用同一組可以包括來自同一組的其他欄位 `$ref` 另一個對象中的值 `meta:refProperty` 值。

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

或者， `meta:refProperty` 可以作為陣列提供，允許您指定單個組中要包含的多個欄位 `allOf` 清單項：

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

您可以使用PUT請求重寫整個架構並配置要包含在下的欄位 `allOf`。

**API格式**

```http
PUT /tenant/schemas/{SCHEMA_ID}
```

| 參數 | 說明 |
| --- | --- |
| `{SCHEMA_ID}` | 的 `meta:altId` 或URL編碼 `$id` 的下界。 |

**要求**

以下請求將更新包含在 `allOf` 陣列。

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

成功的響應返回更新的架構的詳細資訊。

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
>有關架構的PUT請求的詳細資訊，請參閱 [架構終結點指南](../api/schemas.md#put)。

## 使用PATCH操作添加欄位

您可以使用PATCH請求將單個欄位添加到方案而不覆蓋其他欄位。 架構註冊表支援所有標準JSON修補程式操作，包括 `add`。 `remove`, `replace`。 有關JSON修補程式的詳細資訊，請參見 [API基礎指南](../../landing/api-fundamentals.md#json-patch)。

**API格式**

```http
PATCH /tenant/schemas/{SCHEMA_ID}
```

| 參數 | 說明 |
| --- | --- |
| `{SCHEMA_ID}` | 的 `meta:altId` 或URL編碼 `$id` 的下界。 |

**要求**

以下請求將新對象添加到架構 `allOf` 陣列，指定要添加的欄位。

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

成功的響應返回更新的架構的詳細資訊。

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
>有關架構的PATCH請求的詳細資訊，請參閱 [架構終結點指南](../api/schemas.md#patch)。

## 後續步驟

本指南介紹了如何使用API調用將現有欄位組中的各個欄位添加到架構。 有關如何在平台UI中執行類似基於欄位的任務的詳細資訊，請參閱上的指南 [基於欄位的工作流](../ui/field-based-workflows.md)。

有關架構註冊表API功能的詳細資訊，請參閱 [API概述](../api/overview.md) 的子菜單。
