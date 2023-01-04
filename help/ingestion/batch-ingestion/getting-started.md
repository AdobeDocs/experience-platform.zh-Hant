---
keywords: Experience Platform；設定檔；即時客戶設定檔；疑難排解；API
title: 資料擷取API快速入門
type: Documentation
description: 資料擷取API快速入門手冊概述您必須先了解的重要概念和基本功能，才能開始使用API將資料內嵌至Experience Platform。
exl-id: 0653de2b-3268-478b-a23f-c458b6d3df7c
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '367'
ht-degree: 0%

---

# 資料擷取API快速入門 {#getting-started}

您可以使用資料擷取API端點來執行基本CRUD操作，以在Adobe Experience Platform中內嵌資料。

若要使用API指南，您必須妥善了解使用資料時涉及的多項Adobe Experience Platform服務。 使用資料擷取API之前，請先檢閱下列服務的檔案：

* [批次內嵌](./overview.md):可讓您將資料以批次檔案的形式內嵌至Adobe Experience Platform。
* [[!DNL Real-Time Customer Profile]](../home.md):根據來自多個來源的匯總資料，即時提供統一的客戶設定檔。
* [[!DNL Experience Data Model (XDM)]](../../xdm/home.md):Platform用來組織客戶體驗資料的標準化架構。
* [[!DNL Sandboxes]](../../sandboxes/home.md): [!DNL Experience Platform] 提供可分割單一沙箱的虛擬沙箱 [!DNL Platform] 例項放入個別的虛擬環境，以協助開發及改進數位體驗應用程式。

以下小節提供您需要知道的其他資訊，以便成功對 [!DNL Profile] API端點。

## 讀取範例API呼叫

資料擷取API檔案提供範例API呼叫，以示範如何正確格式化請求。 這些功能包括路徑、必要標題和格式正確的請求裝載。 也提供API回應中傳回的範例JSON。 如需範例API呼叫檔案中所使用慣例的相關資訊，請參閱 [如何閱讀API呼叫範例](../../landing/troubleshooting.md#how-do-i-format-an-api-request) 在 [!DNL Experience Platform] 疑難排解指南。

## 必要標題

API檔案也要求您完成 [驗證教學課程](https://www.adobe.com/go/platform-api-authentication-en) 以便成功呼叫 [!DNL Platform] 端點。 完成驗證教學課程，可提供 [!DNL Experience Platform] API呼叫，如下所示：

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

要求內文中包含裝載的所有要求(例如POST、PUT和PATCH呼叫)都必須包含 `Content-Type` 頁首。 呼叫參數中會提供每個呼叫專屬的接受值。

中的所有資源 [!DNL Experience Platform] 與特定虛擬沙箱隔離。 請求 [!DNL Platform] API需要標頭，以指定要在中執行操作的沙箱名稱：

* `x-sandbox-name: {SANDBOX_NAME}`

如需中沙箱的詳細資訊，請參閱 [!DNL Platform]，請參閱 [沙箱概述檔案](../../sandboxes/home.md).
