---
keywords: Experience Platform；首頁；熱門主題；命名空間；命名空間；命名空間；標識命名空間；標識命名空間；標識名空間；標識名空間；標識；標識
solution: Experience Platform
title: 在Identity Service API中建立自定義命名空間
description: 使用Identity Namespace API，您可以建立僅對您的組織可用的自定義標識命名空間。
exl-id: 6015a225-4508-49cc-9dda-fb9f73a8746c
source-git-commit: ad9fb0bcc7bca55da432c72adc94d49e3c63ad6e
workflow-type: tm+mt
source-wordcount: '120'
ht-degree: 3%

---

# 在Identity Service API中建立自定義命名空間

使用 [!DNL Identity Namespace] API，您可以建立僅對您的組織可用的自定義標識命名空間。

有關建立自定義命名空間的建議，請參見 [Identity Service常見問題文檔](../troubleshooting-guide.md)。

>[!NOTE]
>
>命名空間是標識的限定符。 因此，一旦建立了命名空間，就無法刪除該命名空間。

**API格式**

```http
POST /idnamespace/identities
```

**要求**

```shell
curl -X POST \
  https://platform-va7.adobe.io/data/core/idnamespace/identities \
  -H 'Accept-Encoding: gzip, deflate' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -d '{
        "name": "Loyalty Member",
        "code": "Loyalty",
        "description": "Loyalty Program Member ID",
        "idType": "Cross_device"
      }'
```

**回應**

```json
{
    "updateTime": 1576286879075,
    "code": "Loyalty",
    "status": "ACTIVE",
    "description": "Loyalty Program Member ID",
    "id": 10093197,
    "createTime": 1576286879075,
    "idType": "Cross_device",
    "name": "Loyalty Member",
    "custom": true
}
```

## 後續步驟

繼續下一教程， [列出標識的本機ID](./list-native-id.md)
