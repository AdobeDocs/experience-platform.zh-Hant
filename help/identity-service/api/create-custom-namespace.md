---
keywords: Experience Platform；首頁；熱門主題；名稱空間；名稱空間；名稱空間；名稱空間；身分名稱空間；身分名稱空間；身分名稱空間；身分
solution: Experience Platform
title: 在Identity Service API中建立自訂名稱空間
description: 使用身分名稱空間API，您可以建立僅供您的組織使用的自訂身分名稱空間。
role: Developer
exl-id: 6015a225-4508-49cc-9dda-fb9f73a8746c
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
workflow-type: tm+mt
source-wordcount: '120'
ht-degree: 3%

---

# 在Identity Service API中建立自訂名稱空間

使用[!DNL Identity Namespace] API，您可以建立僅供您的組織使用的自訂身分名稱空間。

如需建立自訂名稱空間的建議，請參閱[Identity Service常見問題集檔案](../troubleshooting-guide.md)。

>[!NOTE]
>
>名稱空間是身分的限定詞。 因此，建立名稱空間後就無法刪除。

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

繼續下一個教學課程，以[列出身分識別的原生ID](./list-native-id.md)
