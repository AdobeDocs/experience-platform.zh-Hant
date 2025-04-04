---
title: 使用結構描述登入API新增特定欄位到結構描述
description: 瞭解如何使用結構描述登入API，將現有欄位群組中的個別欄位新增到體驗資料模型(XDM)結構描述。
exl-id: 696cce2b-bbde-416a-9f52-12ab4da9c2c6
source-git-commit: fded2f25f76e396cd49702431fa40e8e4521ebf8
workflow-type: tm+mt
source-wordcount: '626'
ht-degree: 1%

---

# 使用結構描述登入API將特定欄位新增到結構描述

Experience Data Model (XDM)結構描述由基底類別組成，並使用由Adobe定義的標準欄位群組和由您的組織定義的自訂欄位群組來包含其他欄位。

建立結構描述時，您可能會想要使用指定欄位群組中的某些欄位，同時排除相同群組中您不需要的其他欄位。 本教學課程說明如何使用Schema Registry API將欄位群組中的個別欄位新增至結構描述。

>[!NOTE]
>
>如需如何在Adobe Experience Platform UI中新增及移除個別結構描述欄位的詳細資訊，請參閱[欄位式工作流程](../ui/field-based-workflows.md)的指南（目前為測試版）。

## 先決條件

此教學課程涉及呼叫[結構描述登入API](https://developer.adobe.com/experience-platform-apis/references/schema-registry/)。 開始之前，請檢閱[開發人員指南](../api/getting-started.md)以取得重要資訊，您必須瞭解這些資訊才能成功呼叫API，包括您的`{TENANT_ID}`、容器的概念以及發出要求的必要標頭。

## 瞭解`meta:refProperty`欄位

對於任何指定的結構描述，構成其結構的類別和欄位群組在其`allOf`陣列下參考。 每個元件都表示為一個物件，其中包含參考元件URI `$id`的`$ref`屬性。

下列JSON代表使用單一類別(`experienceevent`)和欄位群組(`experienceevent-all`)的簡化結構描述：

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

對於`allOf`陣列中參考欄位群組的任何物件，您可以新增同層級`meta:refProperty`欄位，以指定群組中應包含於結構描述中的欄位。

>[!NOTE]
>
>每個欄位都使用JSON指標字串來指定，該字串代表其各自欄位群組中的欄位路徑。 字串必須以前導斜線(`/`)開頭，且不應包含任何`properties`名稱空間。 例如： `/_experience/campaign/message/id`。

當以字串形式包含時，`meta:refProperty`可以參照群組中的單一欄位。 使用具有不同`meta:refProperty`值的另一個物件中的相同`$ref`值，可以包含相同群組中的其他欄位。

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

或者，也可以將`meta:refProperty`提供為陣列，讓您從單一`allOf`清單專案中指定要包含之指定群組中的多個欄位：

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

## 使用PUT作業新增欄位

您可以使用PUT要求重寫整個結構描述，並設定您要包含在`allOf`下的欄位。

**API格式**

```http
PUT /tenant/schemas/{SCHEMA_ID}
```

| 參數 | 說明 |
| --- | --- |
| `{SCHEMA_ID}` | 您要重寫之結構描述的`meta:altId`或URL編碼的`$id`。 |

**要求**

下列要求會更新`allOf`陣列下之欄位群組所包含的特定欄位。

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

成功的回應會傳回已更新結構的詳細資料。

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
>如需結構描述的PUT要求的詳細資訊，請參閱[結構描述端點指南](../api/schemas.md#put)。

## 使用PATCH作業新增欄位

您可以使用PATCH要求將個別欄位新增至結構描述，而不覆寫其他欄位。 結構描述登入支援所有標準JSON修補程式作業，包括`add`、`remove`和`replace`。 如需JSON修補程式的詳細資訊，請參閱[API基礎指南](../../landing/api-fundamentals.md#json-patch)。

**API格式**

```http
PATCH /tenant/schemas/{SCHEMA_ID}
```

| 參數 | 說明 |
| --- | --- |
| `{SCHEMA_ID}` | 您要重寫之結構描述的`meta:altId`或URL編碼的`$id`。 |

**要求**

下列要求會將新物件加入結構描述的`allOf`陣列，指定要加入的欄位。

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

成功的回應會傳回已更新結構的詳細資料。

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
>如需結構描述的PATCH要求的詳細資訊，請參閱[結構描述端點指南](../api/schemas.md#patch)。

## 後續步驟

本指南說明如何使用API呼叫，將現有欄位群組中的個別欄位新增至結構描述。 如需有關如何在Experience Platform UI中執行類似的欄位型工作的詳細資訊，請參閱[欄位型工作流程](../ui/field-based-workflows.md)的指南。

如需Schema Registry API功能的詳細資訊，請參閱[API總覽](../api/overview.md)，以取得完整的端點與程式清單。
