---
keywords: Experience Platform；首頁；熱門主題；identity service api;identity service開發人員指南；地區
solution: Experience Platform
title: Identity服務API指南
description: Identity服務API可讓開發人員使用Adobe Experience Platform中的身分圖表，管理客戶的跨裝置、跨通道和近乎即時的身分識別。 請遵循本指南以了解如何使用 API 執行關鍵作業。
exl-id: d612af38-4648-4c3e-8cfd-3f306c9370e1
source-git-commit: 81f48de908b274d836f551bec5693de13c5edaf1
workflow-type: tm+mt
source-wordcount: '764'
ht-degree: 3%

---

# [!DNL Identity Service] API指南

Adobe Experience Platform [!DNL Identity Service] 在Adobe Experience Platform內稱為身分圖表，可管理客戶的跨裝置、跨管道和近乎即時身分識別。

## 快速入門

本指南需要妥善了解下列Adobe Experience Platform元件：

- [[!DNL Identity Service]](../home.md):解決了客戶設定檔資料分散帶來的根本難題。 它可跨裝置和系統橋接身分，讓客戶與您的品牌互動。
- [[!DNL Real-Time Customer Profile]](../../profile/home.md):根據來自多個來源的匯總資料，即時提供統一的消費者設定檔。
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md):標準化框架 [!DNL Platform] 組織客戶體驗資料。

以下小節提供您必須知道或擁有的其他資訊，才能成功呼叫 [!DNL Identity Service] API。

### 讀取範例API呼叫

本指南提供範例API呼叫，以示範如何設定請求格式。 這些功能包括路徑、必要標題和格式正確的請求裝載。 也提供API回應中傳回的範例JSON。 如需範例API呼叫檔案中所使用慣例的相關資訊，請參閱 [如何閱讀API呼叫範例](../../landing/troubleshooting.md#how-do-i-format-an-api-request) 在 [!DNL Experience Platform] 疑難排解指南。

### 收集必要標題的值

若要對 [!DNL Platform] API，您必須先完成 [驗證教學課程](https://www.adobe.com/go/platform-api-authentication-en). 完成驗證教學課程會提供所有 [!DNL Experience Platform] API呼叫，如下所示：

- 授權：承載 `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{ORG_ID}`

中的所有資源 [!DNL Experience Platform] 與特定虛擬沙箱隔離。 所有請求 [!DNL Platform] API需要標頭，以指定要在中執行操作的沙箱名稱：

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>如需中沙箱的詳細資訊，請參閱 [!DNL Platform]，請參閱 [沙箱概述檔案](../../sandboxes/home.md).

所有包含裝載(POST、PUT、PATCH)的請求都需要額外的標題：

- 內容類型：application/json

### 基於區域的路由

此 [!DNL Identity Service] API採用地區專屬端點，需要納入 `{REGION}` 作為請求路徑的一部分。 在布建組織期間，會決定某個地區並將其儲存在您的組織設定檔中。 使用每個端點的正確區域可確保使用 [!DNL Identity Service] API會路由至適當的地區。

目前支援兩個地區 [!DNL Identity Service] API:VA7和NLD2。

下表顯示使用區域的路徑範例：

| 服務 | 地區：VA7 | 地區：NLD2 |
| ------ | -------- |--------- |
| [!DNL Identity Service] API | https://</span>platform-va7.adobe。</span>io/data/core/identity/{ENDPOINT} | https://</span>platform-nld2.adobe。</span>io/data/core/identity/{ENDPOINT} |
| [!DNL Identity Namespace] API | https://</span>platform-va7.adobe。</span>io/data/core/idnamespace/{ENDPOINT} | https://</span>platform-nld2.adobe。</span>io/data/core/idnamespace{ENDPOINT} |

>[!NOTE]
>
>未指定區域的請求可能會導致呼叫路由到不正確的區域，或導致呼叫意外失敗。

如果您無法在組織配置檔案中找到該地區，請與系統管理員聯繫以尋求支援。

## 使用 [!DNL Identity Service] API

這些服務中使用的身份參數可以用兩種方式之一表示；複合或XID。

複合身分是包含ID值和命名空間的建構。 使用複合身分識別時，命名空間可由下列任一名稱提供：`namespace.code`)或ID(`namespace.id`)。

當身分持續存在時， [!DNL Identity Service] 會產生ID，並指派給該身分識別（稱為原生ID或XID）。 叢集和對應API的所有變數，在其要求和回應中都支援複合身分和XID。 其中一個參數為必要 —  `xid` 或組合 [`ns` 或 `nsid`] 和 `id` 來使用這些API。

為了限制回應中的裝載，API會調整其回應，使其符合使用的身分建構類型。 也就是說，如果您傳遞XID，您的回應就會有XID，如果您傳遞複合身分，回應就會遵循要求中使用的結構。

本檔案中的範例不涵蓋 [!DNL Identity Service] API。 如需完整API，請參閱 [Swagger API參考](https://www.adobe.io/experience-platform-apis/references/identity-service).

>[!NOTE]
>
>請求中使用原生XID時，傳回的所有身分都會以原生XID形式。 建議使用ID/命名空間表單。 如需詳細資訊，請參閱 [獲取XID以獲取身份](./create-custom-namespace.md).

## 後續步驟

現在您已收集必要的認證，您可以繼續閱讀開發人員指南的其餘部分。 每個區段都提供其端點的重要資訊，並示範執行CRUD作業的範例API呼叫。 每個呼叫都包含一般API格式、顯示必要標題和格式正確之裝載的範例要求，以及成功呼叫的範例回應。
