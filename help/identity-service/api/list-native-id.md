---
keywords: Experience Platform；主題；熱門主題；標識xid;XID
solution: Experience Platform
title: 獲取標識的本機ID
description: 標識資料通常作為ID字串值和標識命名空間在接收的XDM資料中提供，並且當提供標識用於API調用時提供。 當身份保留在Identity Service中時，將生成ID並將其分配給該身份，稱為本地XID。 需要身份資料支援的平台API使用此更緊湊的表單（用於聚合ID和命名空間）。 XID是base64編碼字串。
exl-id: e734f5d8-e00b-43fa-b06c-97c73e1f7c71
source-git-commit: 6d01bb4c5212ed1bb69b9a04c6bfafaad4b108f9
workflow-type: tm+mt
source-wordcount: '231'
ht-degree: 0%

---

# 獲取標識的本機ID

標識資料通常作為ID字串值和標識命名空間在接收的XDM資料中提供，並且當提供標識用於API調用時提供。 當身份持續存在時 [!DNL Identity Service]，將生成ID，並將其分配給該標識，稱為本地XID。 [!DNL Platform] 需要身份資料支援的API使用聚合ID和命名空間的此更緊湊的表單。 XID是base64編碼字串。

>[!NOTE]
>
>此格式主要供內部Adobe使用。 本機XID作為奇數值，空間效率更高，內部使用 [!DNL Platform] 儲存和序列化解決方案。 但是，它不是人類可讀的，是不透明的，並且需要單獨調用才能使用它。

使用本節中介紹的服務獲取給定ID值和命名空間的XID。

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
