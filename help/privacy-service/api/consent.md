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

特定法規要求客戶明確同意才能收集其個人資料。 此 `/consent` 中的端點 [!DNL Privacy Service] API可讓您處理客戶同意請求，並將這些請求整合至您的隱私權工作流程中。

在使用本指南之前，請參閱 [快速入門](./getting-started.md) 指南，以瞭解有關以下範例API呼叫中呈現的必要驗證標題的資訊。

## 處理客戶同意請求

處理同意請求的方式為向發出POST請求 `/consent` 端點。

**API格式**

```http
POST /consent
```

**要求**

以下請求會針對中提供的使用者ID建立新的同意工作 `entities` 陣列。

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
| `optOutOfSale` | 若設為true，表示下方提供的使用者 `entities` 希望退出銷售或分享其個人資料。 |
| `entities` | 表示同意要求套用至的使用者的物件陣列。 每個物件都包含 `namespace` 和陣列 `values` 以比對具有該名稱空間的個別使用者。 |
| `nameSpace` | 中的每一個物件 `entities` 陣列必須包含一個 [標準身分名稱空間](./appendix.md#standard-namespaces) 由Privacy ServiceAPI識別。 |
| `values` | 每個使用者的值陣列，對應提供的值 `nameSpace`. |

{style="table-layout:auto"}

>[!NOTE]
>
>如需如何判斷要傳送至哪些客戶身分值的詳細資訊 [!DNL Privacy Service]，請參閱以下指南： [提供身分資料](../identity-data.md).

**回應**

成功的回應會傳回HTTP狀態202 （已接受），而且沒有裝載，表示已接受要求 [!DNL Privacy Service] 且正在處理中。
