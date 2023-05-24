---
title: 配置檔案終結點
description: 瞭解如何調用Reactor API中的/profiles端點。
exl-id: d0434098-f49a-45f3-9772-488bd3c134aa
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '169'
ht-degree: 5%

---

# 配置檔案終結點

在Reactor API中，配置檔案表示Adobe Experience Platform用戶。 Reactor API不維護其自己的用戶和權限資料庫，而是依賴於由管理的AdobeID [Adobe身份管理系統](https://helpx.adobe.com/tw/enterprise/using/identity.html)。

配置檔案包含有關登錄用戶的所有資訊，包括其所屬的所有組織、其所屬在每個組織中的產品配置檔案以及它們從每個產品配置檔案中擁有的權限。

## 快速入門

本指南中使用的端點是 [反應堆API](https://www.adobe.io/experience-platform-apis/references/reactor/)。 在繼續之前，請查看 [入門指南](../getting-started.md) 有關如何驗證到API的重要資訊。

## 檢索當前配置檔案 {#lookup}

您可以通過向以下站點發出GET請求來檢索當前登錄的配置檔案的詳細資訊 `/profile` 端點。

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**回應**

成功的響應將返回配置檔案的詳細資訊。

```json
{
  "data": {
    "id": "UR0bd696624e844d6ba5bfc248ba1eca11",
    "type": "users",
    "attributes": {
      "active_org": "{ORG_1}",
      "expires_in": 0,
      "display_name": "John Smith",
      "job_function": null,
      "email": "jsmith@example.com",
      "organizations": {
        "{ORG_1}": {
          "name": "Example organization A",
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
        "{ORG_2}": {
          "name": "Example organization B",
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
