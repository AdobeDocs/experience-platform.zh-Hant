---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 刪除資源
topic: developer guide
translation-type: tm+mt
source-git-commit: d9ab2b1226b051be43f8fc0dd222bc075caed6f0

---


# 刪除資源

有時可能需要從架構註冊表中刪除（刪除）資源。 只能刪除您在租用戶容器中建立的資源。 這是通過使用要刪除的資 `$id` 源執行DELETE請求來完成的。

**API格式**

```http
DELETE /tenant/{RESOURCE_TYPE}/{RESOURCE_ID} 
```

| 參數 | 說明 |
| --- | --- |
| `{RESOURCE_TYPE}` | 要從架構庫中刪除的資源類型。 有效類 `datatypes`型有 `mixins`、 `schemas`和 `classes`。 |
| `{RESOURCE_ID}` | URL編碼的 `$id` URI或 `meta:altId` 資源。 |

**請求**

DELETE請求不需要「接受」標題。

```SHELL
curl -X DELETE \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/mixins/https%3A%2F%2Fns.adobe.com%2F{TENANT_ID}%2Fmixins%2F4fbd5368aa67f0e74d5838f67694c867 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應會傳回HTTP狀態204（無內容）和空白的內文。

您可以嘗試對資源進行查閱(GET)請求，以確認刪除。 您需要在請求中加入「接受」標題，但應接收HTTP狀態404（找不到），因為資源已從架構註冊表中移除。