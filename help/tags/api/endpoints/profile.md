---
title: 設定檔端點
description: 了解如何在Reactor API中呼叫/profiles端點。
source-git-commit: 59592154eeb8592fa171b5488ecb0385e0e59f39
workflow-type: tm+mt
source-wordcount: '174'
ht-degree: 5%

---

# 設定檔端點

在Reactor API中，設定檔代表Adobe Experience Platform使用者。 Reactor API不會維護自己的使用者和權限資料庫，而是仰賴由[Adobe的身分管理系統(IMS)](https://helpx.adobe.com/tw/enterprise/using/identity.html)管理的AdobeID。

設定檔包含登入使用者的所有資訊，包括其所屬的所有IMS組織、每個組織內其所屬的產品設定檔，以及各產品設定檔所擁有的權限。

## 快速入門

本指南中使用的端點是[Reactor API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/reactor.yaml)的一部分。 繼續操作之前，請參閱[快速入門手冊](../getting-started.md)，了解如何驗證API的重要資訊。

## 擷取目前的設定檔 {#lookup}

您可以向`/profile`端點提出GET請求，以擷取目前登入設定檔的詳細資訊。

**API格式**

```http
GET /profile
```

**要求**

```shell
curl -X GET \
  https://reactor.adobe.io/profile \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**回應**

成功的回應會傳回設定檔的詳細資訊。

```json
{
  "data": {
    "id": "UR0bd696624e844d6ba5bfc248ba1eca11",
    "type": "users",
    "attributes": {
      "active_org": "{IMS_ORG_1}",
      "expires_in": 0,
      "display_name": "John Smith",
      "job_function": null,
      "email": "jsmith@example.com",
      "organizations": {
        "{IMS_ORG_1}": {
          "name": "Example IMS Org A",
          "admin": true,
          "active": true,
          "login_companies": [

          ],
          "product_contexts": [
            "dma_audiencemanager_int",
            "dma_tartan",
            "dma_dtm",
            "dma_reactor",
            "dma_auditor"
          ],
          "tenant_id": "{TENANT_ID_1}"
        },
        "{IMS_ORG_2}": {
          "name": "Example IMS Org B",
          "admin": false,
          "active": false,
          "login_companies": [

          ],
          "product_contexts": [
            "dma_reactor",
            "dma_auditor",
            "dma_tartan"
          ],
          "tenant_id": "{TENANT_ID_2}"
        }
      }
    },
    "links": {
      "self": "https://reactor.adobe.io/profile"
    },
    "meta": {
      "rights": [
        "manage_companies"
      ]
    }
  }
}
```

