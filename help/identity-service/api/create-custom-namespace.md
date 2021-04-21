---
keywords: Experience Platform;home；常用主題；namespace；命名空間；命名空間；標識命名空間；標識命名空間；標識名稱空間；標識
solution: Experience Platform
title: 在Identity Service API中建立自訂命名空間
topic-legacy: API guide
description: 使用Identity Namespace API，您可以建立自訂的身分名稱空間，該名稱空間僅供您的組織使用。
exl-id: 6015a225-4508-49cc-9dda-fb9f73a8746c
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '120'
ht-degree: 3%

---

# 在Identity Service API中建立自訂命名空間

使用[!DNL Identity Namespace] API，您可以建立自訂的身分名稱空間，該名稱空間僅供您的組織使用。

如需有關建立自訂名稱空間的建議，請參閱[Identity Service常見問答集檔案](../troubleshooting-guide.md)。

>[!NOTE]
>
>名稱空間是身份的限定詞。 因此，一旦建立了命名空間，就無法刪除。

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
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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

繼續下一個教學課程[列出身分的原生ID](./list-native-id.md)
