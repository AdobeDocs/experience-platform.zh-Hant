---
keywords: Experience Platform;home；熱門主題；查找沙盒；查找沙盒
solution: Experience Platform
title: 在API中尋找沙盒
topic-legacy: developer guide
description: 您可以提出GET請求，在請求路徑中包含沙盒的名稱屬性，以尋找個別沙盒。
exl-id: de8d965c-ca58-436e-b5b1-05a492de70f5
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '243'
ht-degree: 2%

---

# 在API中尋找沙盒

您可以提出GET請求，在請求路徑中包含沙盒的`name`屬性，以尋找個別沙盒。

**API格式**

```http
GET /sandboxes/{SANDBOX_NAME}
```

| 參數 | 說明 |
| --- | --- |
| `{SANDBOX_NAME}` | 您要尋找的沙盒的`name`屬性。 |

**要求**

下列請求會擷取名為&quot;dev-2&quot;的沙盒。

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/sandbox-management/sandboxes/dev-2 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應會傳回沙盒的詳細資訊，包括其`name`、`title`、`state`和`type`。

```json
{
    "name": "dev-2",
    "title": "Development 2",
    "state": "creating",
    "type": "development",
    "region": "VA7",
    "isDefault": false,
    "eTag": 1,
    "createdDate": "2019-09-07 10:16:02",
    "lastModifiedDate": "2019-09-07 10:16:02",
    "createdBy": "{USER_ID}",
    "modifiedBy": "{USER_ID}"
}
```

| 屬性 | 說明 |
| --- | --- |
| `name` | 沙盒的名稱。 用於API呼叫中的查閱用途。 |
| `title` | 沙盒的顯示名稱。 |
| `state` | 沙盒的目前處理狀態。 沙盒的狀態可以是下列任一項： <ul><li>**建立**:沙盒已建立，但系統仍在布建中。</li><li>**作用中**:沙盒會建立並啟用。</li><li>**失敗**:由於發生錯誤，系統無法布建沙盒並停用沙盒。</li><li>**已刪除**:沙盒已手動停用。</li></ul> |
| `type` | 沙盒類型，「開發」或「生產」。 |
| `isDefault` | 布林屬性，指出此沙盒是否為組織的預設沙盒。 通常這是生產沙盒。 |
| `eTag` | 沙盒特定版本的識別碼。 用於版本控制和快取效率，此值會在每次對沙盒進行變更時更新。 |
