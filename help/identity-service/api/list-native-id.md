---
keywords: Experience Platform；首頁；熱門主題；身分xid；XID
solution: Experience Platform
title: 取得身分的原生ID
description: 在擷取的XDM資料中，以及在API呼叫中提供身分使用時，身分資料通常會以ID字串值和身分名稱空間的形式提供。 當身分持續存在身分服務中時，就會產生ID並指派給該身分（稱為原生XID）。 需要身分資料支援的平台API會針對彙總ID和名稱空間使用此更精簡的表單。 XID是base64編碼字串。
role: Developer
exl-id: e734f5d8-e00b-43fa-b06c-97c73e1f7c71
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
workflow-type: tm+mt
source-wordcount: '231'
ht-degree: 0%

---

# 取得身分的原生ID

在擷取的XDM資料中，以及在API呼叫中提供身分使用時，身分資料通常會以ID字串值和身分名稱空間的形式提供。 當身分持續存在中 [!DNL Identity Service]，系統會產生一個ID並指派給該身分，稱為原生XID。 [!DNL Platform] 需要身分資料支援的API會針對彙總ID和名稱空間使用此更精簡的表單。 XID是base64編碼字串。

>[!NOTE]
>
>此格式主要供內部Adobe使用。 原生XID作為單一值更能節省空間，且為內部使用 [!DNL Platform] 儲存與序列化的解決方案。 然而，它不是人類看得懂的、不透明，需要個別呼叫才能使用。

使用本節所述的服務，取得指定ID值和名稱空間的XID。

**API格式**

```http
GET https://platform-{REGION}.adobe.io/data/core/identity/identity?namespace={NAMESPACE}&id={ID_VALUE}
```

**要求**

```shell
curl -X GET \
  'https://platform-va7.adobe.io/data/core/identity/identity?namespace=email&id=test@adobetest.com' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

```json
{
    "xid":"BVrqzwVuzbXrLfmnaG3rXrLf3KJg"
}
```
