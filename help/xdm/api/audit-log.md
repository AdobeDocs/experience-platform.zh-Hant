---
keywords: Experience Platform;home；熱門主題；api;API;XDM;XDM系統；體驗資料模型；體驗資料模型；資料模型；資料模型；審計；審計；更改日誌；rpc;
solution: Experience Platform
title: 審核日誌API端點
description: 方案註冊表API中的/auditlog端點允許您檢索對現有XDM資源所做更改的時間順序清單。
topic-legacy: developer guide
exl-id: 8d33ae7c-0aa4-4f38-a183-a2ff1801e291
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '396'
ht-degree: 2%

---

# 審計日誌端點

對於每個體驗資料模型(XDM)資源，[!DNL Schema Registry]會維護不同更新之間發生的所有變更記錄。 [!DNL Schema Registry] API中的`/auditlog`端點允許您檢索由ID指定的任何類、混音、資料類型或方案的審計日誌。

## 快速入門

本指南中使用的端點是[[!DNL Schema Registry] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/schema-registry.yaml)的一部分。 在繼續之前，請先閱讀[快速入門手冊](./getting-started.md)，以取得相關檔案的連結、閱讀本檔案中範例API呼叫的指南，以及成功呼叫任何Experience PlatformAPI所需之必要標題的重要資訊。

`/auditlog`端點是[!DNL Schema Registry]所支援的遠程過程調用(RPC)的一部分。 與[!DNL Schema Registry] API中的其他端點不同，RPC端點不需要額外的標題，如`Accept`或`Content-Type`，也不使用`CONTAINER_ID`。 而必須改用`/rpc`命名空間，如下列API呼叫所示。

## 檢索資源的審計日誌

通過在`/auditlog`端點的GET請求路徑中指定資源的ID，可以檢索方案庫中任何類、混合、資料類型或方案的審計日誌。

**API格式**

```http
GET /rpc/auditlog/{RESOURCE_ID}
```

| 參數 | 說明 |
| --- | --- |
| `{RESOURCE_ID}` | 要檢索其審計日誌的資源的`meta:altId`或URL編碼`$id`。 |

**要求**

下列請求會擷取`Restaurant`混音的稽核記錄檔。

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/rpc/auditlog/_{TENANT_ID}.mixins.922a56b58c6b4e4aeb49e577ec82752106ffe8971b23b4d9 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的響應返回對資源所做更改的時間順序清單，從最近到最近。

```json
[
  {
    "id": "https://ns.adobe.com/{TENANT_ID}/mixins/922a56b58c6b4e4aeb49e577ec82752106ffe8971b23b4d9",
    "auditTrails": [
      {
        "id": "https://ns.adobe.com/{TENANT_ID}/mixins/922a56b58c6b4e4aeb49e577ec82752106ffe8971b23b4d9",
        "xdmType": "mixins",
        "action": "add",
        "path": "/definitions/customFields/properties/_{TENANT_ID}/properties/brand",
        "value": {
          "title": "Brand",
          "description": "",
          "type": "string",
          "isRequired": false,
          "meta:xdmType": "string"
        }
      },
      {
        "id": "https://ns.adobe.com/{TENANT_ID}/mixins/922a56b58c6b4e4aeb49e577ec82752106ffe8971b23b4d9",
        "xdmType": "mixins",
        "action": "add",
        "path": "/meta:usageCount",
        "value": 0
      }
    ],
    "updatedUser": "{USER_ID}",
    "imsOrg": "{IMS_ORG}",
    "updated": 1606255582281,
    "clientId": "{CLIENT_ID}",
    "sandBoxId": "{SANDBOX_ID}"
  }
]
```

| 屬性 | 說明 |
| --- | --- |
| `auditTrails` | 對象陣列，每個對象表示對指定資源或其從屬資源所做的更改。 |
| `id` | 已更改的資源的`$id`。 此值通常表示在請求路徑中指定的資源，但如果是變更的來源，則可能表示從屬資源。 |
| `action` | 所做的變更類型。 |
| `path` | [JSON指針](../../landing/api-fundamentals.md#json-pointer)字串，指出已變更或新增之特定欄位的路徑。 |
| `value` | 指派給新欄位或已更新欄位的值。 |
