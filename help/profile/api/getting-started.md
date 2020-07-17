---
keywords: Experience Platform;profile;real-time customer profile;troubleshooting;API
solution: Adobe Experience Platform
title: 即時客戶個人檔案API快速入門
topic: guide
translation-type: tm+mt
source-git-commit: f910351d49de9c4a18a444b99b7f102f4ce3ed5b
workflow-type: tm+mt
source-wordcount: '364'
ht-degree: 0%

---


# API快速入 [!DNL Real-time Customer Profile] 門 {#getting-started}

使用 [!DNL Real-time Customer Profile] API，您可以對配置檔案資源執行基本的CRUD操作，例如配置計算屬性、訪問實體、導出配置檔案資料以及刪除不需要的資料集或批。

使用開發人員指南需要對使用資料時涉及的各種Adobe Experience Platform服務有正確的 [!DNL Profile] 瞭解。 在開始使用 [!DNL Real-time Customer Profile] API之前，請先閱讀下列服務的檔案：

* [!DNL Real-time Customer Profile](../home.md): 根據來自多個來源的匯整資料，即時提供統一的客戶個人檔案。
* [!DNL Adobe Experience Platform Identity Service](../../identity-service/home.md): 跨裝置和系統橋接身分，以更全面地瞭解客戶及其行為。
* [!DNL Adobe Experience Platform Segmentation Service](../../segmentation/home.md): 可讓您從即時客戶個人檔案資料建立受眾細分。
* [!DNL Experience Data Model (XDM)](../../xdm/home.md): 平台組織客戶體驗資料的標準化架構。
* [!DNL Sandboxes](../../sandboxes/home.md): [!DNL Experience Platform] 提供虛擬沙盒，可將單一執行個體分 [!DNL Platform] 割為不同的虛擬環境，以協助開發和發展數位體驗應用程式。

以下各節提供您必須知道的額外資訊，才能成功呼叫 [!DNL Profile] API端點。

## 讀取範例API呼叫

API文 [!DNL Real-time Customer Profile] 件提供範例API呼叫，以示範如何正確格式化請求。 這些包括路徑、必要標題和正確格式化的請求負載。 也提供API回應中傳回的範例JSON。 如需範例API呼叫檔案中所用慣例的詳細資訊，請參閱疑難排解指 [南中有關如何讀取範例API呼叫的](../../landing/troubleshooting.md#how-do-i-format-an-api-request)[!DNL Experience Platform] 章節。

## 必要的標題

API檔案也要求您完成驗證教學 [課程](../../tutorials/authentication.md) ，才能成功呼叫端點 [!DNL Platform] 。 完成驗證教學課程可提供 [!DNL Experience Platform] API呼叫中每個必要標題的值，如下所示：

* 授權： 生產者 `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

中的所有資 [!DNL Experience Platform] 源都與特定虛擬沙盒隔離。 對API的 [!DNL Platform] 請求需要一個標題，該標題指定要在中執行的操作的沙盒名稱：

* x-sandbox-name: `{SANDBOX_NAME}`

如需中沙盒的詳細資訊 [!DNL Platform]，請參閱沙 [盒概述檔案](../../sandboxes/home.md)。

請求正文中包含裝載的所有請求（例如POST、PUT和PATCH呼叫）都必須包含標 `Content-Type` 題。 在呼叫參數中提供每個呼叫的接受值。

## 後續步驟

若要開始使用 [!DNL Real-time Customer Profile] API進行呼叫，請選取其中一個可用的端點指南。