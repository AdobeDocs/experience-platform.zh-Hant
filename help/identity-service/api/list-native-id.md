---
keywords: Experience Platform；首頁；熱門主題；身分xid;XID
solution: Experience Platform
title: 取得身分的原生ID
description: 在擷取的XDM資料中，以及提供要在API呼叫中使用的身分識別時，身分資料通常會以ID字串值和身分命名空間的形式提供。 當身分識別保存在Identity Service中時，會產生ID並指派給該身分識別，稱為原生XID。 需要身分資料支援的Platform API，會使用此更精簡的表單來匯總ID和命名空間。 XID是base64編碼的字串。
exl-id: e734f5d8-e00b-43fa-b06c-97c73e1f7c71
source-git-commit: 6d01bb4c5212ed1bb69b9a04c6bfafaad4b108f9
workflow-type: tm+mt
source-wordcount: '231'
ht-degree: 0%

---

# 取得身分的原生ID

在擷取的XDM資料中，以及提供要在API呼叫中使用的身分識別時，身分資料通常會以ID字串值和身分命名空間的形式提供。 當身分持續存在 [!DNL Identity Service]，則會產生ID並指派給該身分識別，稱為原生XID。 [!DNL Platform] 需要身分資料支援的API，請使用此更精簡的表單來匯總ID和命名空間。 XID是base64編碼的字串。

>[!NOTE]
>
>此格式主要供內部Adobe使用。 本機XID作為奇異值，空間效率更高，是內部使用的 [!DNL Platform] 儲存和序列化解決方案。 不過，它不是人類看得懂的，也不透明，需要個別呼叫才能取得使用。

使用本節所述的服務，取得指定ID值和命名空間的XID。

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
