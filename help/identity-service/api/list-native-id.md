---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 取得身分的原生ID
topic: API guide
translation-type: tm+mt
source-git-commit: 6ffdcc2143914e2ab41843a52dc92344ad51bcfb
workflow-type: tm+mt
source-wordcount: '151'
ht-degree: 1%

---


# 取得XID以取得身分識別

身分資料通常在所接收的XDM資料中以ID字串值和身分命名空間的形式提供，並在提供身分以供API呼叫使用時提供。 當身分持續存在 [!DNL Identity Service]時，會產生ID並指派給該身分，稱為原生XID。 [!DNL Platform] 需要身分資料支援的API，使用這個更精簡的表單來匯整ID和命名空間。 XID是base64編碼字串。

>[!NOTE] 此格式主要供內部Adobe使用。 原生XID是個奇異值，可提高空間效率，而且是解決方案內部用於儲存 [!DNL Platform] 和序列化的功能。 但是，它不是人類可讀的，不透明，而且需要單獨呼叫才能使用。

使用本節所述的服務，取得特定ID值和命名空間的XID。

**API格式**

```http
GET https://platform-{REGION}.adobe.io/data/core/identity/identity?namespace={NAMESPACE}&id={ID_VALUE}
```

**請求**

```shell
curl -X GET \
  'https://platform-va7.adobe.io/data/core/identity/identity?namespace=email&id=test@adobetest.com' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

```json
{
    "xid":"BVrqzwVuzbXrLfmnaG3rXrLf3KJg"
}
```
