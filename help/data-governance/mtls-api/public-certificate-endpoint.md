---
title: 公用憑證端點
description: 瞭解如何使用MTLS服務API的/public-certificate端點擷取您的公開憑證。
role: Developer
source-git-commit: ce02c1a15d4e87c130de5e6133edda6b66cc2196
workflow-type: tm+mt
source-wordcount: '358'
ht-degree: 2%

---

# 公用憑證端點

本指南說明如何使用公開憑證端點安全地擷取您組織Adobe應用程式的公開憑證。 它包含範例API呼叫和詳細指示，以協助開發人員驗證及驗證資料交換。

## 快速入門

繼續之前，請檢閱[快速入門手冊](./getting-started.md)以取得您成功呼叫API所需瞭解的重要資訊，包括必要的標頭以及如何讀取範例API呼叫。

## API路徑 {#paths}

以下資訊為使用mTLS服務API所需的基本API路徑。 這些功能包括平台閘道URL、API的基本路徑，以及擷取公開憑證的完整路徑範例。

- 平台閘道URL： `https://platform.adobe.io/`
- 此API的基礎路徑： `/data/core/mtls`
- 完整路徑的範例： `https://platform.adobe.io/data/core/mtls/v1/certificate/public-certificate`

## 擷取您的公開憑證 {#list}

您可以透過向`/v1/certificate/public-certificate`端點發出GET要求，擷取您組織的任何Adobe應用程式的公開憑證。

**API格式**

```http
GET /v1/certificate/public-certificate
```

擷取您的公用憑證時，可以使用以下選用的查詢引數。

| 查詢引數 | 說明 | 範例 |
| --------------- | ----------- | ------- |
| `page` | 指定請求結果的開始頁面。 | `page=5` |
| `limit` | 每頁要擷取的公開憑證數目上限。 | `limit=20` |

{style="table-layout:auto"}

**要求**

可收合的區段顯示傳回與貴組織相關聯之公開憑證的範例要求。

+++範例要求

```shell
curl -X GET https://experience.adobe.io/data/core/mtls/v1/certificate/public-certificate
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' 
```

+++

**回應**

成功的回應會傳回HTTP狀態200，並列出組織的公開憑證。

+++成功回應的範例

```json
{
   "results":[
      {
         "certCommonName":"Adobe Experience Platform",
         "publicCertificate":"-----BEGIN CERTIFICATE-----\nMIIDQTCCAimgAwIBAgITBmyfACAfma......KJY5u89CjAwj\n-----END CERTIFICATE-----",
         "expiryDate":"2024-07-17T21:27:57.434Z"
      }
   ],
   "total":0,
   "count":0,
   "_links":{
      "next":{
         "href":"string",
         "templated":true
      },
      "prev":{
         "href":"string",
         "templated":true
      },
      "page":{
         "href":"string",
         "templated":true
      }
   }
}
```

| 屬性 | 說明 |
| --- | --- |
| `certCommonName` | 憑證的一般名稱(CN)，通常代表憑證核發目標之伺服器或實體的名稱或身分。 |
| `publicCertificate` | 字串格式的實際公用憑證，用於驗證及加密通訊。 |
| `expiryDate` | 公用憑證到期的日期和時間，格式為ISO 8601 (UTC)。 |

{style="table-layout:auto"}

+++

## 後續步驟

閱讀本指南後，您現在瞭解如何使用Adobe Experience Platform API擷取公開憑證。 若要進一步瞭解管理客戶資料以確保符合法規和組織政策，請參閱[資料控管概觀](../home.md)。

<!-- To test this API call, navigate to the [MTLS API reference page]() to interact with the Experience Platform API endpoints. -->

<!-- Add link after developer page is live -->

