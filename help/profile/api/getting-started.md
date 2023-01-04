---
keywords: Experience Platform；設定檔；即時客戶設定檔；疑難排解；API
title: 即時客戶設定檔API快速入門
topic-legacy: guide
type: Documentation
description: 設定檔API快速入門手冊概述使用即時客戶設定檔API端點，對設定檔資料執行基本CRUD作業時需知的重要概念和基本功能。
exl-id: 7e30610a-a7e7-43ab-a45d-fd84ef6e36ef
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '411'
ht-degree: 0%

---

# 開始使用 [!DNL Real-Time Customer Profile] API {#getting-started}

您可以使用即時客戶設定檔API端點，對設定檔資料執行基本CRUD操作，例如設定計算屬性、存取實體、匯出設定檔資料，以及刪除不需要的資料集或批次。

若要使用開發人員指南，您必須妥善了解搭配使用時涉及的各種Adobe Experience Platform服務 [!DNL Profile] 資料。 開始使用之前 [!DNL Real-Time Customer Profile] API，請檢閱以下服務的檔案：

* [[!DNL Real-Time Customer Profile]](../home.md):根據來自多個來源的匯總資料，即時提供統一的客戶設定檔。
* [[!DNL Adobe Experience Platform Identity Service]](../../identity-service/home.md):跨裝置和系統橋接身分，以更全面了解客戶及其行為。
* [[!DNL Adobe Experience Platform Segmentation Service]](../../segmentation/home.md):可讓您從即時客戶設定檔資料建立受眾區段。
* [[!DNL Experience Data Model (XDM)]](../../xdm/home.md):Platform用來組織客戶體驗資料的標準化架構。
* [[!DNL Sandboxes]](../../sandboxes/home.md): [!DNL Experience Platform] 提供可分割單一沙箱的虛擬沙箱 [!DNL Platform] 例項放入個別的虛擬環境，以協助開發及改進數位體驗應用程式。

以下小節提供您需要知道的其他資訊，以便成功對 [!DNL Profile] API端點。

## 讀取範例API呼叫

此 [!DNL Real-Time Customer Profile] API檔案提供範例API呼叫，以示範如何正確格式化請求。 這些功能包括路徑、必要標題和格式正確的請求裝載。 也提供API回應中傳回的範例JSON。 如需範例API呼叫檔案中所使用慣例的相關資訊，請參閱 [如何閱讀API呼叫範例](../../landing/troubleshooting.md#how-do-i-format-an-api-request) 在 [!DNL Experience Platform] 疑難排解指南。

## 必要標題

API檔案也要求您完成 [驗證教學課程](https://www.adobe.com/go/platform-api-authentication-en) 以便成功呼叫 [!DNL Platform] 端點。 完成驗證教學課程，可提供 [!DNL Experience Platform] API呼叫，如下所示：

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

中的所有資源 [!DNL Experience Platform] 與特定虛擬沙箱隔離。 請求 [!DNL Platform] API需要標頭，以指定要在中執行操作的沙箱名稱：

* `x-sandbox-name: {SANDBOX_NAME}`

如需中沙箱的詳細資訊，請參閱 [!DNL Platform]，請參閱 [沙箱概述檔案](../../sandboxes/home.md).

要求內文中包含裝載的所有要求(例如POST、PUT和PATCH呼叫)都必須包含 `Content-Type` 頁首。 呼叫參數中會提供每個呼叫專屬的接受值。

## 後續步驟

若要開始使用進行呼叫 [!DNL Real-Time Customer Profile] API，請選取任一可用的端點指南。
