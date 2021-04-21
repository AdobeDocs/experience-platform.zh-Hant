---
keywords: Experience Platform；首頁；熱門主題
solution: Experience Platform
title: 許可API端點
topic-legacy: developer guide
description: 瞭解如何使用Experience CloudAPI管理Privacy Service應用程式的客戶同意要求。
exl-id: ec505749-c0a9-4050-be56-4c0657807ec7
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '244'
ht-degree: 1%

---

# 許可端點

某些法規要求客戶明確同意才能收集其個人資料。 [!DNL Privacy Service] API中的`/consent`端點可讓您處理客戶同意請求，並將它們整合到您的隱私權工作流程中。

在使用本指南之前，請參閱[快速入門](./getting-started.md)一節，以取得以下範例API呼叫中所需驗證標題的相關資訊。

## 處理客戶同意請求

對`/consent`端點發出POST請求，以處理許可請求。

**API格式**

```http
POST /consent
```

**要求**

以下請求會為`entities`陣列中提供的用戶ID建立新的許可作業。

```shell
curl -X POST \
  https://platform.adobe.io/data/core/privacy/consent \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -d '{
        "optOutOfSale": true,
        "entities": [
          {
            "nameSpace": "email",
            "values": [
              "dsmith@acme.com",
              "ajones@acme.com"
            ]
          },
          {
            "nameSpace": "ECID",
            "values": [
              "443636576799758681021090721276"
            ]
          }
        ]
      }'
```

| 屬性 | 說明 |
| --- | --- |
| `optOutOfSale` | 設為true時，表示`entities`下提供的使用者希望退出銷售或分享其個人資料。 |
| `entities` | 一系列對象，用於指示對許可請求申請的用戶。 每個物件都包含`namespace`和`values`陣列，以搭配個別使用者與該命名空間。 |
| `nameSpace` | `entities`陣列中的每個對象都必須包含Privacy ServiceAPI所識別的[標準身份名稱空間](./appendix.md#standard-namespaces)中的一個。 |
| `values` | 每個用戶的值陣列，與提供的`nameSpace`相對應。 |

>[!NOTE]
>
>有關如何確定要發送到[!DNL Privacy Service]的客戶身份值的詳細資訊，請參閱[提供身份資料](../identity-data.md)的指南。

**回應**

成功的回應會傳回沒有裝載的HTTP狀態202（已接受），指出[!DNL Privacy Service]已接受請求，且正在處理中。
