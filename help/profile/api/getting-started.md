---
keywords: Experience Platform；配置檔案；即時客戶配置檔案；故障排除；API
title: 即時客戶個人檔案API快速入門
topic: guide
type: Documentation
description: 描述檔API快速入門手冊概述了使用即時客戶描述檔API端點，對描述檔資料執行基本CRUD作業時，您需要知道的主要概念和基本功能。
translation-type: tm+mt
source-git-commit: 126b3d1cf6d47da73c6ab045825424cf6f99e5ac
workflow-type: tm+mt
source-wordcount: '413'
ht-degree: 0%

---


# [!DNL Real-time Customer Profile] API {#getting-started}快速入門

使用即時客戶配置檔案API端點，您可以對配置檔案資料執行基本的CRUD操作，例如配置計算屬性、訪問實體、導出配置檔案資料以及刪除不需要的資料集或批。

使用開發人員指南需要對使用[!DNL Profile]資料時涉及的各種Adobe Experience Platform服務有良好的瞭解。 開始使用[!DNL Real-time Customer Profile] API之前，請先閱讀下列服務的檔案：

* [[!DNL Real-time Customer Profile]](../home.md):根據來自多個來源的匯總資料即時提供統一的客戶個人檔案。
* [[!DNL Adobe Experience Platform Identity Service]](../../identity-service/home.md):跨裝置和系統橋接身分，以更全面地瞭解客戶及其行為。
* [[!DNL Adobe Experience Platform Segmentation Service]](../../segmentation/home.md):可讓您從即時客戶個人檔案資料建立受眾細分。
* [[!DNL Experience Data Model (XDM)]](../../xdm/home.md):平台組織客戶體驗資料的標準化架構。
* [[!DNL Sandboxes]](../../sandboxes/home.md): [!DNL Experience Platform] 提供虛擬沙盒，可將單一執行個體分 [!DNL Platform] 割為不同的虛擬環境，以協助開發和發展數位體驗應用程式。

以下各節提供您必須知道的其他資訊，以便成功呼叫[!DNL Profile] API端點。

## 讀取範例API呼叫

[!DNL Real-time Customer Profile] API檔案提供範例API呼叫，以示範如何正確格式化請求。 這些包括路徑、必要標題和正確格式化的請求負載。 也提供API回應中傳回的範例JSON。 如需範例API呼叫檔案中所用慣例的詳細資訊，請參閱[!DNL Experience Platform]疑難排解指南中[如何讀取範例API呼叫](../../landing/troubleshooting.md#how-do-i-format-an-api-request)一節。

## 必要的標題

API檔案也要求您完成[驗證教學課程](https://www.adobe.com/go/platform-api-authentication-en)，才能成功呼叫[!DNL Platform]端點。 完成驗證教學課程可為[!DNL Experience Platform] API呼叫中的每個必要標題提供值，如下所示：

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

[!DNL Experience Platform]中的所有資源都隔離到特定的虛擬沙盒。 對[!DNL Platform] API的請求需要一個標題，該標題指定要在中執行操作的沙盒的名稱：

* `x-sandbox-name: {SANDBOX_NAME}`

如需[!DNL Platform]中沙盒的詳細資訊，請參閱[沙盒概述檔案](../../sandboxes/home.md)。

所有在請求正文中包含裝載的請求(例如POST、PUT和PATCH呼叫)都必須包含`Content-Type`標題。 在呼叫參數中提供每個呼叫的接受值。

## 後續步驟

若要開始使用[!DNL Real-time Customer Profile] API進行呼叫，請選取其中一個可用的端點指南。