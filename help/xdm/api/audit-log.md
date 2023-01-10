---
keywords: Experience Platform；首頁；熱門主題；API; XDM; XDM系統；體驗資料模型；體驗資料模型；資料模型；資料模型；稽核；稽核記錄；變更記錄；變更記錄；rpc;
solution: Experience Platform
title: 稽核記錄API端點
description: 架構註冊表API中的/auditlog端點可讓您擷取已對現有XDM資源進行之變更的時間順序清單。
exl-id: 8d33ae7c-0aa4-4f38-a183-a2ff1801e291
source-git-commit: 983682489e2c0e70069dbf495ab90fc9555aae2d
workflow-type: tm+mt
source-wordcount: '407'
ht-degree: 3%

---

# 審核日誌端點

對於每個Experience Data Model(XDM)資源， [!DNL Schema Registry] 維護在不同更新之間發生的所有更改的日誌。 此 `/auditlog` 端點 [!DNL Schema Registry] API可讓您擷取ID所指定之任何類別、結構欄位群組、資料類型或結構的稽核記錄。

## 快速入門

本指南中使用的端點屬於 [[!DNL Schema Registry] API](https://www.adobe.io/experience-platform-apis/references/schema-registry/). 繼續之前，請檢閱 [快速入門手冊](./getting-started.md) 如需相關檔案的連結，請參閱本檔案中讀取範例API呼叫的指南，以及成功呼叫任何Experience PlatformAPI所需的必要標頭重要資訊。

此 `/auditlog` 端點是遠端程式呼叫(RPC)的一部分，這些呼叫由 [!DNL Schema Registry]. 不同於 [!DNL Schema Registry] API、RPC端點不需要其他標題，例如 `Accept` 或 `Content-Type`，且不使用 `CONTAINER_ID`. 而是必須使用 `/rpc` 命名空間，如下方API呼叫所示。

## 檢索資源的審核日誌

您可以在方案庫內的任何類、欄位組、資料類型或方案中檢索審核日誌，方法是在GET請求的路徑中指定資源的ID `/auditlog` 端點。

**API格式**

```http
GET /rpc/auditlog/{RESOURCE_ID}
```

| 參數 | 說明 |
| --- | --- |
| `{RESOURCE_ID}` | 此 `meta:altId` 或URL編碼 `$id` 要檢索其審核日誌的資源。 |

{style=&quot;table-layout:auto&quot;}

**要求**

下列請求會擷取結構的稽核記錄。

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/rpc/auditlog/_{TENANT_ID}.schemas.50649eb1b040bf042d6400a0335901cd2a97d31a4eac4330 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應會傳回對資源所做變更（從最近到最近）的時間順序清單。

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
| `updates` | 對象的陣列，每個對象表示對指定資源或其一個相關資源所做的更改。 |
| `id` | 此 `$id` 已變更的資源。 此值通常代表請求路徑中指定的資源，但如果是變更的來源，則可能代表相依資源。 |
| `xdmType` | 已變更的資源類型。 |
| `action` | 已進行的變更類型。 |
| `path` | A [JSON指標](../../landing/api-fundamentals.md#json-pointer) 字串，指出已變更或新增之特定欄位的路徑。 |
| `value` | 指派給新欄位或更新欄位的值。 |

{style=&quot;table-layout:auto&quot;}
