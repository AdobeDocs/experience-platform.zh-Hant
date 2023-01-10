---
keywords: Experience Platform；首頁；熱門主題
solution: Experience Platform
title: 同意API端點
description: 了解如何使用Experience CloudAPI管理Privacy Service應用程式的客戶同意請求。
exl-id: ec505749-c0a9-4050-be56-4c0657807ec7
source-git-commit: 0f7ef438db5e7141197fb860a5814883d31ca545
workflow-type: tm+mt
source-wordcount: '247'
ht-degree: 2%

---

# 同意端點

某些法規需要客戶明確同意，才能收集其個人資料。 此 `/consent` 端點 [!DNL Privacy Service] API可讓您處理客戶同意請求，並將它們整合至您的隱私權工作流程中。

使用本指南之前，請參閱 [快速入門](./getting-started.md) 指南，取得以下範例API呼叫中所呈現之必要驗證標題的相關資訊。

## 處理客戶同意請求

向發出POST要求以處理同意要求 `/consent` 端點。

**API格式**

```http
POST /consent
```

**要求**

下列要求會針對 `entities` 陣列。

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
| `optOutOfSale` | 設為true時，表示底下提供的使用者 `entities` 想要退出個人資料的銷售或分享。 |
| `entities` | 一系列物件，指出同意請求適用的使用者。 每個物件都包含 `namespace` 和 `values` 以便讓個別使用者與該命名空間相符。 |
| `nameSpace` | 中的每個物件 `entities` 陣列必須包含其中一個 [標準身分命名空間](./appendix.md#standard-namespaces) 由Privacy ServiceAPI辨識。 |
| `values` | 每個使用者的值陣列，與提供的 `nameSpace`. |

{style=&quot;table-layout:auto&quot;}

>[!NOTE]
>
>如需如何判斷要傳送至哪些客戶身分值的詳細資訊 [!DNL Privacy Service]，請參閱 [提供身分資料](../identity-data.md).

**回應**

成功的回應會傳回HTTP狀態202（已接受），但沒有裝載，表示已接受要求 [!DNL Privacy Service] 和正在處理中。
