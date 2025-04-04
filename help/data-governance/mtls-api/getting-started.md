---
title: MTLS服務API快速入門
description: 本檔案提供成功使用MTLS API所需瞭解的其他資訊。
role: Developer
exl-id: db5978cf-fe47-4b76-86ba-c8ea1ee6b12f
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '215'
ht-degree: 6%

---

# MTLS服務API快速入門 {#getting-started}

MTLS服務API可讓您安全地擷取及驗證Adobe所發行的公開憑證。

以下小節提供成功使用MTLS服務API所需瞭解的其他資訊。

## 讀取範例 API 呼叫

MTLS服務API檔案提供範例API呼叫，示範如何格式化您的請求。 這包括路徑、必要的標頭及正確格式化的請求裝載。 此外，也提供 API 回應中傳回的範例 JSON。 如需檔案中所使用範例API呼叫慣例的詳細資訊，請參閱Experience Platform疑難排解指南中有關[如何讀取範例API呼叫](../../landing/troubleshooting.md#how-do-i-format-an-api-request)的章節。

## 必要的標頭

API檔案也要求您完成[驗證教學課程](https://www.adobe.com/go/platform-api-authentication-en)，才能成功呼叫Experience Platform端點。 完成驗證教學課程，提供Experience Platform API呼叫中每個必要標題的值，如下所示：

- 授權： `Bearer {ACCESS_TOKEN}`
- x-api-key： `{API_KEY}`
- x-gw-ims-org-id： `{ORG_ID}`

## 後續步驟

若要使用MTLS服務API進行呼叫，請使用左側導覽或[開發人員指南概觀](./overview.md)選取端點指南
