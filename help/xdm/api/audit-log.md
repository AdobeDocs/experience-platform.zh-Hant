---
keywords: Experience Platform；首頁；熱門主題；API；API；XDM；XDM系統；體驗資料模型；體驗資料模型；資料模型；資料模型；稽核；稽核記錄；變更記錄；變更記錄；rpc；
solution: Experience Platform
title: 稽核記錄API端點
description: 結構描述登入API中的/auditlog端點可讓您擷取對現有XDM資源進行的變更的清單（以時間順序排列）。
exl-id: 8d33ae7c-0aa4-4f38-a183-a2ff1801e291
source-git-commit: 983682489e2c0e70069dbf495ab90fc9555aae2d
workflow-type: tm+mt
source-wordcount: '397'
ht-degree: 2%

---

# 稽核記錄端點

針對每個Experience Data Model (XDM)資源，[!DNL Schema Registry]會維護在不同更新之間發生的所有變更記錄。 [!DNL Schema Registry] API中的`/auditlog`端點可讓您擷取任何類別、結構描述欄位群組、資料型別或ID所指定的結構描述的稽核記錄。

## 快速入門

本指南中使用的端點是[[!DNL Schema Registry] API](https://www.adobe.io/experience-platform-apis/references/schema-registry/)的一部分。 繼續之前，請先檢閱[快速入門手冊](./getting-started.md)，以取得相關檔案的連結、閱讀本檔案中範例API呼叫的手冊，以及有關成功呼叫任何Experience PlatformAPI所需必要標題的重要資訊。

`/auditlog`端點是[!DNL Schema Registry]支援的遠端程式呼叫(RPC)的一部分。 與[!DNL Schema Registry] API中的其他端點不同，RPC端點不需要`Accept`或`Content-Type`等其他標頭，也不使用`CONTAINER_ID`。 相反地，他們必須使用`/rpc`名稱空間，如下面的API呼叫所示。

## 擷取資源的稽核記錄

您可以在`/auditlog`端點的GET要求路徑中指定資源的ID，以擷取結構描述資料庫內任何類別、欄位群組、資料型別或結構描述的稽核記錄。

**API格式**

```http
GET /rpc/auditlog/{RESOURCE_ID}
```

| 參數 | 說明 |
| --- | --- |
| `{RESOURCE_ID}` | 您要擷取其稽核記錄檔之資源的`meta:altId`或URL編碼的`$id`。 |

{style="table-layout:auto"}

**要求**

以下請求會擷取結構的稽核記錄。

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/rpc/auditlog/_{TENANT_ID}.schemas.50649eb1b040bf042d6400a0335901cd2a97d31a4eac4330 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應會按時間順序傳回資源變更清單（從最近到最近）。

```json
[
  {
    "id": "https://ns.adobe.com/{TENANT_ID}/schemas/50649eb1b040bf042d6400a0335901cd2a97d31a4eac4330",
    "updatedUser": "{USER_ID}",
    "imsOrg": "{ORG_ID}",
    "updatedTime": "02-19-2021 05:43:56",
    "requestId": "a14NMF0jd6BIfyXaHdTDl4bC4R0r9rht",
    "clientId": "{CLIENT_ID}",
    "sandBoxId": "28e74200-e3de-11e9-8f5d-7f27416c5f0d",
    "updates": [
      {
        "id": "https://ns.adobe.com/{TENANT_ID}/schemas/50649eb1b040bf042d6400a0335901cd2a97d31a4eac4330",
        "xdmType": "schemas",
        "action": "remove",
        "path": "/meta:usageCount",
        "value": 0
      }
    ]
  },
  {
    "id": "https://ns.adobe.com/{TENANT_ID}/schemas/50649eb1b040bf042d6400a0335901cd2a97d31a4eac4330",
    "updatedUser": "{USER_ID}",
    "imsOrg": "{ORG_ID}",
    "updatedTime": "02-19-2021 05:43:56",
    "requestId": "pFQbgmWrdbJrNB9GdxTSGECpXYWspu68",
    "clientId": "{CLIENT_ID}",
    "sandBoxId": "28e74200-e3de-11e9-8f5d-7f27416c5f0d",
    "updates": [
      {
        "id": "https://ns.adobe.com/{TENANT_ID}/classes/11052164b588f0c29584bf6ae1a6663a59aa65426c82389f",
        "xdmType": "classes",
        "action": "remove",
        "path": "/definitions/customFields/properties/_{TENANT_ID}/properties/loyaltySunday_ABC",
        "value": {
          "title": "LoyaltySundayABC",
          "description": "",
          "type": "string",
          "isRequired": false,
          "required": [],
          "meta:xdmType": "string"
        }
      },
      {
        "id": "https://ns.adobe.com/{TENANT_ID}/classes/11052164b588f0c29584bf6ae1a6663a59aa65426c82389f",
        "xdmType": "classes",
        "action": "remove",
        "path": "/definitions/customFields/properties/_{TENANT_ID}/properties/loyaltyMoxee_XYZ",
        "value": {
          "title": "LoyaltyMoxeeXYZ",
          "description": "",
          "type": "string",
          "isRequired": false,
          "required": [],
          "meta:xdmType": "string"
        }
      }
    ]
  }
]
```

| 屬性 | 說明 |
| --- | --- |
| `updates` | 一個物件陣列，每個物件代表對指定資源或其相依資源之一所做的變更。 |
| `id` | 已變更資源的`$id`。 此值通常代表請求路徑中指定的資源，但如果這是變更的來源，則可能代表相依資源。 |
| `xdmType` | 已變更的資源型別。 |
| `action` | 已進行的變更型別。 |
| `path` | [JSON指標](../../landing/api-fundamentals.md#json-pointer)字串，指出已變更或新增之特定欄位的路徑。 |
| `value` | 指派給新欄位或更新欄位的值。 |

{style="table-layout:auto"}
