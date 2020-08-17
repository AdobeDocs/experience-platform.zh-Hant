---
keywords: Experience Platform;home;popular topics;namespace;Namespace;namespaces;Namespaces;identity namespace;Identity namespace;identity;Identity
solution: Experience Platform
title: 建立自訂命名空間
topic: API guide
description: 使用Identity Namespace API，您可以建立自訂的身分名稱空間，該名稱空間僅供您的組織使用。
translation-type: tm+mt
source-git-commit: 3376d6cace9ab196f457e2bf7b84cde06693103c
workflow-type: tm+mt
source-wordcount: '95'
ht-degree: 4%

---


# 建立自訂命名空間

使用 [!DNL Identity Namespace] API，您可以建立自訂的身分名稱空間，該名稱空間僅供您的組織使用。

如需有關建立自訂名稱空間的建議，請參 [閱Identity Service常見問答檔案](../troubleshooting-guide.md)。

>[!NOTE]
>
>名稱空間是身份的限定詞。 因此，一旦建立了命名空間，就無法刪除。

**API格式**

```http
POST /idnamespace/identities
```

**請求**

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

繼續下一個教學課程， [列出身分的原生ID](./list-native-id.md)