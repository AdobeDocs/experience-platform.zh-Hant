---
keywords: Experience Platform;home；熱門主題；identity xid;XID
solution: Experience Platform
title: 取得身分的原生ID
topic-legacy: API guide
description: 身分資料通常在所接收的XDM資料中以ID字串值和身分命名空間的形式提供，並在提供身分以供API呼叫使用時提供。 當身分識別保存在Identity Service中時，會產生ID並指派給該身分，稱為原生XID。 需要身分資料支援的平台API，使用這個更精簡的表單來匯整ID和命名空間。 XID是base64編碼字串。
exl-id: e734f5d8-e00b-43fa-b06c-97c73e1f7c71
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '231'
ht-degree: 0%

---

# 取得身分的原生ID

身分資料通常在所接收的XDM資料中以ID字串值和身分命名空間的形式提供，並在提供身分以供API呼叫使用時提供。 當身分持續存在[!DNL Identity Service]時，會產生ID並指派給該身分，稱為原生XID。 [!DNL Platform] 需要身分資料支援的API，使用這個更精簡的表單來匯整ID和命名空間。XID是base64編碼字串。

>[!NOTE]
>
>此格式主要供內部Adobe使用。 原生XID是個奇異值，可提高空間效率，是[!DNL Platform]解決方案內部用於儲存和序列化的功能。 但是，它不是人類可讀的，不透明，而且需要單獨呼叫才能使用。

使用本節所述的服務，取得特定ID值和命名空間的XID。

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
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

```json
{
    "xid":"BVrqzwVuzbXrLfmnaG3rXrLf3KJg"
}
```
