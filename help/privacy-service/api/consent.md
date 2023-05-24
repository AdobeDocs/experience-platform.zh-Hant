---
keywords: Experience Platform；首頁；熱門主題
solution: Experience Platform
title: 同意API終結點
description: 瞭解如何使用Experience CloudAPI管理Privacy Service應用程式的客戶同意請求。
exl-id: ec505749-c0a9-4050-be56-4c0657807ec7
source-git-commit: 0f7ef438db5e7141197fb860a5814883d31ca545
workflow-type: tm+mt
source-wordcount: '244'
ht-degree: 1%

---

# 同意終結點

某些法規要求客戶明確同意才能收集其個人資料。 的 `/consent` 端點 [!DNL Privacy Service] API允許您處理客戶同意請求並將其整合到您的隱私工作流中。

使用本指南之前，請參閱 [開始](./getting-started.md) 指南，瞭解有關以下示例API調用中提供的所需驗證標頭的資訊。

## 處理客戶同意請求

通過向C.A.C.M.C.M.C.M.C.M.C.M.M.M.M.M.M.M.M.M.M.M.M.M.M.M.M.M.M.M.M.M.M. `/consent` 端點。

**API格式**

```http
POST /consent
```

**要求**

以下請求為中提供的用戶ID建立新的同意作業 `entities` 陣列。

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
| `optOutOfSale` | 設定為true時，表示在 `entities` 希望選擇不出售或共用個人資料。 |
| `entities` | 表示同意請求所適用的用戶的對象陣列。 每個對象都包含 `namespace` 還有 `values` 將單個用戶與該命名空間匹配。 |
| `nameSpace` | 中的每個對象 `entities` 陣列必須包含其中一個 [標準標識命名空間](./appendix.md#standard-namespaces) 被Privacy ServiceAPI識別。 |
| `values` | 每個用戶的與所提供的相應的值的陣列 `nameSpace`。 |

{style="table-layout:auto"}

>[!NOTE]
>
>有關如何確定要發送給的客戶標識值的詳細資訊 [!DNL Privacy Service]，請參閱上的指南 [提供身份資料](../identity-data.md)。

**回應**

成功的響應返回HTTP狀態202（已接受），無負載，表示請求已被接受 [!DNL Privacy Service] 正在處理中。
