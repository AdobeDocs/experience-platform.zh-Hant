---
keywords: Experience Platform；首頁；熱門主題；API; XDM; XDM系統；體驗資料模型；體驗資料模型；資料模型；資料模型；稽核；稽核記錄；變更記錄；變更記錄；rpc;
solution: Experience Platform
title: 稽核記錄API端點
description: 架構註冊表API中的/auditlog端點可讓您擷取已對現有XDM資源進行之變更的時間順序清單。
topic-legacy: developer guide
exl-id: 8d33ae7c-0aa4-4f38-a183-a2ff1801e291
source-git-commit: e4bf5bb77ac4186b24580329699d74d653310d93
workflow-type: tm+mt
source-wordcount: '406'
ht-degree: 3%

---

# 審核日誌端點

對於每個Experience Data Model(XDM)資源， [!DNL Schema Registry]會維護在不同更新之間發生的所有變更記錄。 [!DNL Schema Registry] API中的`/auditlog`端點可讓您擷取ID所指定之任何類別、架構欄位群組、資料類型或架構的稽核記錄。

## 快速入門

本指南中使用的端點是[[!DNL Schema Registry] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/schema-registry.yaml)的一部分。 繼續之前，請檢閱[快速入門手冊](./getting-started.md)，取得相關檔案的連結、閱讀本檔案中範例API呼叫的指南，以及成功呼叫任何Experience PlatformAPI所需的必要標頭的重要資訊。

`/auditlog`端點是[!DNL Schema Registry]支援的遠程過程調用(RPC)的一部分。 與[!DNL Schema Registry] API中的其他端點不同，RPC端點不需要額外的標題，如`Accept`或`Content-Type`，也不使用`CONTAINER_ID`。 因此，他們必須使用`/rpc`命名空間，如下方API呼叫所示。

## 檢索資源的審核日誌

您可以在`/auditlog`端點的GET請求路徑中指定資源的ID，以檢索架構庫內任何類、欄位組、資料類型或架構的審核日誌。

**API格式**

```http
GET /rpc/auditlog/{RESOURCE_ID}
```

| 參數 | 說明 |
| --- | --- |
| `{RESOURCE_ID}` | 您要擷取其稽核記錄的資源的`meta:altId`或URL編碼的`$id`。 |

{style=&quot;table-layout:auto&quot;}

**要求**

以下請求將檢索`Restaurant`欄位組的審核日誌。

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/rpc/auditlog/_{TENANT_ID}.mixins.922a56b58c6b4e4aeb49e577ec82752106ffe8971b23b4d9 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應會傳回對資源所做變更（從最近到最近）的時間順序清單。

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
| `auditTrails` | 對象的陣列，每個對象表示對指定資源或其一個相關資源所做的更改。 |
| `id` | 已更改的資源的`$id`。 此值通常會代表請求路徑中指定的資源，但如果是變更的來源，則可能代表相依資源。 |
| `action` | 已進行的變更類型。 |
| `path` | [JSON指針](../../landing/api-fundamentals.md#json-pointer)字串，用於指示已變更或新增之特定欄位的路徑。 |
| `value` | 指派給新欄位或更新欄位的值。 |

{style=&quot;table-layout:auto&quot;}
