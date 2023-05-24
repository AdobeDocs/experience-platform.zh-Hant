---
keywords: Experience Platform；主題；熱門主題；api;API;XDM;XDM系統；體驗資料模型；體驗資料模型；資料模型；資料模型；資料模型；審計；審計日誌；更改日誌；rpc;
solution: Experience Platform
title: 審核日誌API終結點
description: 通過架構註冊表API中的/auditlog終結點，可以檢索對現有XDM資源所做更改的按時間順序排列的清單。
exl-id: 8d33ae7c-0aa4-4f38-a183-a2ff1801e291
source-git-commit: 983682489e2c0e70069dbf495ab90fc9555aae2d
workflow-type: tm+mt
source-wordcount: '401'
ht-degree: 1%

---

# 審核日誌終結點

對於每個體驗資料模型(XDM)資源， [!DNL Schema Registry] 維護不同更新之間發生的所有更改的日誌。 的 `/auditlog` 端點 [!DNL Schema Registry] API允許您檢索由ID指定的任何類、架構欄位組、資料類型或架構的審核日誌。

## 快速入門

本指南中使用的端點是 [[!DNL Schema Registry] API](https://www.adobe.io/experience-platform-apis/references/schema-registry/)。 在繼續之前，請查看 [入門指南](./getting-started.md) 有關相關文檔的連結、閱讀本文檔中示例API調用的指南，以及有關成功調用任何Experience PlatformAPI所需標頭的重要資訊。

的 `/auditlog` endpoint是遠程過程調用(RPC)的一部分，該調用由 [!DNL Schema Registry]。 不同於 [!DNL Schema Registry] API、RPC終結點不需要像 `Accept` 或 `Content-Type`，並且不使用 `CONTAINER_ID`。 相反，他們必須使用 `/rpc` 命名空間，如下面的API調用所示。

## 檢索資源的審計日誌

通過在GET請求到的路徑中指定資源的ID，可以檢索架構庫中任何類、欄位組、資料類型或架構的審核日誌 `/auditlog` 端點。

**API格式**

```http
GET /rpc/auditlog/{RESOURCE_ID}
```

| 參數 | 說明 |
| --- | --- |
| `{RESOURCE_ID}` | 的 `meta:altId` 或URL編碼 `$id` 要檢索其審核日誌的資源。 |

{style="table-layout:auto"}

**要求**

以下請求檢索架構的審計日誌。

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/rpc/auditlog/_{TENANT_ID}.schemas.50649eb1b040bf042d6400a0335901cd2a97d31a4eac4330 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的響應返回對資源從最近到最近所做更改的按時間順序排列的清單。

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
| `updates` | 對象陣列，其中每個對象表示對指定資源或其從屬資源之一所做的更改。 |
| `id` | 的 `$id` 已更改的資源。 此值通常表示在請求路徑中指定的資源，但如果是更改的源，則可能表示從屬資源。 |
| `xdmType` | 已更改的資源類型。 |
| `action` | 所做更改的類型。 |
| `path` | A [JSON指針](../../landing/api-fundamentals.md#json-pointer) 字串，指示已更改或添加的特定欄位的路徑。 |
| `value` | 分配給新欄位或更新欄位的值。 |

{style="table-layout:auto"}
