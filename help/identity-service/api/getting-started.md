---
keywords: Experience Platform；首頁；熱門主題；identity service api；identity service開發人員指南；地區
solution: Experience Platform
title: Identity Service API指南
description: Identity Service API可讓開發人員使用Adobe Experience Platform中的身分圖表，管理跨裝置、跨頻道及幾乎即時的客戶身分識別。 請遵循本指南以了解如何使用 API 執行關鍵作業。
role: Developer
exl-id: d612af38-4648-4c3e-8cfd-3f306c9370e1
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
workflow-type: tm+mt
source-wordcount: '753'
ht-degree: 14%

---

# [!DNL Identity Service] API指南

Adobe Experience Platform [!DNL Identity Service] 在Adobe Experience Platform中管理跨裝置、跨頻道及幾乎即時的客戶身分識別，這稱為「身分圖表」。

## 快速入門

本指南需要您深入了解下列 Adobe Experience Platform 元件：

- [[!DNL Identity Service]](../home.md)：解決客戶設定檔資料片段化帶來的基本挑戰。 其做法是跨客戶與您品牌互動的裝置和系統橋接身分。
- [[!DNL Real-Time Customer Profile]](../../profile/home.md)：根據來自多個來源的彙總資料，即時提供統一的消費者設定檔。
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md)：作為依據的標準化架構 [!DNL Platform] 組織客戶體驗資料。

以下小節提供您需瞭解或有手頭的其他資訊，才能成功呼叫 [!DNL Identity Service] API。

### 讀取範例 API 呼叫

本指南提供範例 API 呼叫，示範如何格式化您的請求。 這些包括路徑、必要的標頭和正確格式化的請求承載。 此外，也提供 API 回應中傳回的範例 JSON。 如需檔案中用於範例API呼叫的慣例相關資訊，請參閱以下章節： [如何讀取範例API呼叫](../../landing/troubleshooting.md#how-do-i-format-an-api-request) 在 [!DNL Experience Platform] 疑難排解指南。

### 收集所需標頭的值

為了呼叫 [!DNL Platform] API，您必須先完成 [驗證教學課程](https://www.adobe.com/go/platform-api-authentication-en). 完成驗證教學課程會提供所有 [!DNL Experience Platform] API 呼叫中每個必要標頭的值，如下所示：

- 授權：持有人 `{ACCESS_TOKEN}`
- x-api-key： `{API_KEY}`
- x-gw-ims-org-id： `{ORG_ID}`

中的所有資源 [!DNL Experience Platform] 會隔離至特定的虛擬沙箱。 所有要求至 [!DNL Platform] API需要標頭，用以指定將進行作業的沙箱名稱：

- x-sandbox-name： `{SANDBOX_NAME}`

>[!NOTE]
>
>如需中沙箱的詳細資訊 [!DNL Platform]，請參閱 [沙箱概述檔案](../../sandboxes/home.md).

所有包含承載 (POST、PUT、PATCH) 的請求都需有額外的標頭：

- Content-Type： application/json

### 以區域為基準的製程

此 [!DNL Identity Service] API採用區域特定的端點，這些端點需要包含 `{REGION}` 做為請求路徑的一部分。 在貴組織布建期間，區域會進行判定，並儲存在貴組織設定檔中。 對每個端點使用正確的區域，可確保使用 [!DNL Identity Service] API會路由至適當的區域。

目前有兩個區域受到支援 [!DNL Identity Service] API： VA7和NLD2。

下表顯示使用區域的範例路徑：

| 服務 | 地區： VA7 | 地區： NLD2 |
| ------ | -------- |--------- |
| [!DNL Identity Service] API | https://</span>platform-va7.adobe.</span>io/data/core/identity/{ENDPOINT} | https://</span>platform-nld2.adobe.</span>io/data/core/identity/{ENDPOINT} |
| [!DNL Identity Namespace] API | https://</span>platform-va7.adobe.</span>io/data/core/idnamespace/{ENDPOINT} | https://</span>platform-nld2.adobe.</span>io/data/core/idnamespace{ENDPOINT} |

>[!NOTE]
>
>在沒有指定區域的情況下進行要求，可能會導致呼叫路由到不正確的區域，或導致呼叫意外失敗。

如果您在組織設定檔中找不到地區，請聯絡您的系統管理員以尋求支援。

## 使用 [!DNL Identity Service] API

這些服務中使用的身分引數可以採用以下兩種方式之一來表示：複合或XID。

複合身分是包含ID值和名稱空間的建構。 使用複合身分時，名稱空間可由任一名稱提供(`namespace.code`)或ID (`namespace.id`)。

當身分持續存在時， [!DNL Identity Service] 會產生並指派一個ID給該身分，稱為原生ID或XID。 Cluster和Mapping API的所有變數在其請求和回應中同時支援複合身分和XID。 需要其中一個引數 —  `xid` 或組合 [`ns` 或 `nsid`] 和 `id` 以使用這些API。

為了限制回應中的裝載，API會調整其回應，以符合所使用的身分建構型別。 也就是說，如果您傳遞XID，您的回應將具有XID；如果您傳遞複合身分，回應將遵循請求中使用的結構。

本檔案中的範例不涵蓋 [!DNL Identity Service] API。 如需完整的API，請參閱 [Swagger API參考](https://www.adobe.io/experience-platform-apis/references/identity-service).

>[!NOTE]
>
>當請求中使用原生XID時，所有傳回的身分都將採用原生XID格式。 建議使用ID/名稱空間表單。 如需詳細資訊，請參閱以下章節： [取得身分的XID](./create-custom-namespace.md).

## 後續步驟

現在您已收集到所需的認證，您可以繼續閱讀開發人員指南的其餘部分。 每個區段都提供有關其端點的重要資訊，並示範用於執行CRUD操作的範例API呼叫。 每個呼叫都包含一般API格式、顯示必要標題和正確格式負載的範例請求，以及成功呼叫的範例回應。
