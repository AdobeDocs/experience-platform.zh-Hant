---
keywords: Experience Platform；首頁；熱門主題
solution: Experience Platform
title: 同意API端點
description: 瞭解如何使用Privacy Service API管理Experience Cloud應用程式的客戶同意請求。
role: Developer
exl-id: ec505749-c0a9-4050-be56-4c0657807ec7
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
workflow-type: tm+mt
source-wordcount: '245'
ht-degree: 1%

---

# 同意端點

特定法規要求客戶明確同意才能收集其個人資料。 [!DNL Privacy Service] API中的`/consent`端點可讓您處理客戶同意要求，並將這些要求整合至您的隱私權工作流程。

使用本指南之前，請參閱[快速入門](./getting-started.md)指南，以取得有關以下範例API呼叫中所需驗證標頭的資訊。

## 處理客戶同意請求

同意要求是透過向`/consent`端點發出POST要求來處理。

**API格式**

```http
POST /consent
```

**要求**

下列要求會針對`entities`陣列中提供的使用者ID建立新的同意工作。

```shell
curl -X POST \
  https://platform.adobe.io/data/core/privacy/consent \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `optOutOfSale` | 若設為true，表示在`entities`底下提供的使用者希望退出銷售或分享其個人資料。 |
| `entities` | 表示同意要求套用至的使用者的物件陣列。 每個物件包含一個`namespace`和一個`values`陣列，以比對具有該名稱空間的個別使用者。 |
| `nameSpace` | `entities`陣列中的每個物件都必須包含Privacy ServiceAPI可辨識的[標準身分名稱空間](./appendix.md#standard-namespaces)之一。 |
| `values` | 每個使用者的值陣列，對應提供的`nameSpace`。 |

{style="table-layout:auto"}

>[!NOTE]
>
>如需如何判斷要傳送給[!DNL Privacy Service]之客戶身分值的詳細資訊，請參閱[提供身分資料](../identity-data.md)的指南。

**回應**

成功的回應傳回HTTP狀態202 （已接受），沒有承載，表示[!DNL Privacy Service]已接受要求且正在處理。
