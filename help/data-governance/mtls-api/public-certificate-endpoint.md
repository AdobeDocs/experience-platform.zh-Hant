---
title: 公用憑證端點
description: 瞭解如何使用MTLS服務API的/public-certificate端點擷取您的公開憑證。
role: Developer
exl-id: 8369c783-e595-476f-9546-801cf4f10f71
source-git-commit: d74353e70e992150c031397009d0c8add3df5e7b
workflow-type: tm+mt
source-wordcount: '471'
ht-degree: 2%

---

# 公用憑證端點

>[!NOTE]
>
>Adobe不再支援公開mTLS憑證的靜態下載。 使用此API來擷取整合的有效憑證。 現在需要自動擷取以避免服務中斷。

本指南說明如何使用公開憑證端點來安全地擷取您組織Adobe應用程式的公開憑證。 它包含範例API呼叫和詳細指示，以協助開發人員驗證及驗證資料交換。

## 快速入門

在繼續之前，請檢閱[快速入門手冊](./getting-started.md)，以取得有關所需標題以及如何解譯範例API呼叫的重要詳細資訊。

## API路徑 {#paths}

以下資訊為使用mTLS服務API所需的基本API路徑。 這些功能包括平台閘道URL、API的基本路徑，以及擷取公開憑證的完整路徑範例。

- 平台閘道URL： `https://platform.adobe.io/`
- 此API的基礎路徑： `/data/core/mtls`
- 完整路徑的範例： `https://platform.adobe.io/data/core/mtls/v1/certificate/public-certificate`

## 擷取您的公開憑證 {#list}

向`/v1/certificate/public-certificate`端點發出GET要求，以擷取您組織的任何Adobe應用程式的公開憑證。

**API格式**

```http
GET /v1/certificate/public-certificate
```

擷取您的公用憑證時，可以使用以下選用的查詢引數。

| 查詢參數 | 說明 | 範例 |
| --------------- | ----------- | ------- |
| `page` | 指定請求結果的開始頁面。 | `page=5` |
| `limit` | 每頁要擷取的公開憑證數目上限。 | `limit=20` |

{style="table-layout:auto"}

**要求**

可收合的區段顯示傳回與貴組織相關聯之公開憑證的範例要求。

+++範例要求

```shell
curl -X GET https://platform.adobe.io/data/core/mtls/v1/certificate/public-certificate
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

## 憑證生命週期自動化 {#certificate-lifecycle-automation}

Adobe會自動執行公用mTLS憑證的生命週期，以確保連續性並減少服務中斷。

- 憑證會在到期前60天重新核發。
- 憑證會在到期前30天被撤銷。

>[!NOTE]
>
>這些時間表會隨著[CA/B論壇准則](https://www.digicert.com/blog/tls-certificate-lifetimes-will-officially-reduce-to-47-days)的調整而縮短，該准則旨在將憑證存留期減少到最多47天。

您必須更新整合，以支援透過API自動擷取。 請勿依賴手動憑證下載或靜態副本，否則可能會導致憑證過期或撤銷。

## 後續步驟

使用API擷取您的公開憑證後，請更新您的整合，以在憑證過期之前定期呼叫此端點。 若要以互動方式測試此呼叫，請造訪[MTLS API參考頁面](https://developer.adobe.com/experience-platform-apis/references/mtls-service/)。 如需憑證式整合的更廣泛指引，請參閱Adobe Experience Platform中的[資料加密總覽](../../landing/governance-privacy-security/encryption.md)或[資料控管總覽](../home.md)。
