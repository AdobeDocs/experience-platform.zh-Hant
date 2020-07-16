---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 同意
topic: developer guide
translation-type: tm+mt
source-git-commit: 5b32c1955fac4f137ba44e8189376c81cdbbfc40
workflow-type: tm+mt
source-wordcount: '220'
ht-degree: 1%

---


# 同意

某些法規要求客戶明確同意才能收集其個人資料。 API `/consent` 的端點可 [!DNL Privacy Service] 讓您處理客戶同意要求，並將它們整合到您的隱私權工作流程中。

在使用本指南之前，請參閱快速入 [門](./getting-started.md) ，以取得以下範例API呼叫中所需驗證標題的相關資訊。

## 處理客戶同意請求

對端點發出POST請求，即可處理同意 `/consent` 請求。

**API格式**

```http
POST /consent
```

**請求**

下列請求會為陣列中提供的使用者ID建立新的許可 `entities` 工作。

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
| `optOutOfSale` | 設為true時，表示依據提供的使 `entities` 用者希望退出銷售或分享其個人資料。 |
| `entities` | 一系列對象，用於指示對許可請求申請的用戶。 每個物件都包含一 `namespace` 個和一個陣列，以 `values` 搭配具有該命名空間的個別使用者。 |
| `nameSpace` | 陣列中的每個對 `entities` 像都必須包含Privacy Service API所識 [別的標準身份名稱空間](./appendix.md#standard-namespaces) 。 |
| `values` | 每個用戶的值陣列，對應於所提供的值 `nameSpace`。 |

>[!NOTE]
>
>如需如何決定要傳送給哪些客戶身分值的詳細資訊，請 [!DNL Privacy Service]參閱提供身 [分資料指南](../identity-data.md)。

**回應**

成功的回應會傳回沒有裝載的HTTP狀態202（已接受），表示請求已被接受， [!DNL Privacy Service] 且正在處理中。