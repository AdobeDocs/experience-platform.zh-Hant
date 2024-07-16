---
keywords: Experience Platform；設定檔；即時客戶設定檔；疑難排解；API
title: 開始使用Data Ingestion API
type: Documentation
description: 資料擷取API快速入門手冊概述重要概念和基本功能，讓您在開始使用API將資料擷取到Experience Platform之前需要瞭解這些概念和功能。
exl-id: 0653de2b-3268-478b-a23f-c458b6d3df7c
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '364'
ht-degree: 6%

---

# 開始使用Data Ingestion API {#getting-started}

使用資料擷取API端點，您可以執行基本的CRUD操作，以便在Adobe Experience Platform中擷取資料。

使用API指南需要實際瞭解與使用資料有關的多個Adobe Experience Platform服務。 在使用資料擷取API之前，請檢閱以下服務的檔案：

* [批次內嵌](./overview.md)：可讓您將資料以批次檔案的形式內嵌到Adobe Experience Platform中。
* [[!DNL Real-Time Customer Profile]](../home.md)：根據來自多個來源的彙總資料，即時提供統一的客戶設定檔。
* [[!DNL Experience Data Model (XDM)]](../../xdm/home.md)： Platform用來組織客戶體驗資料的標準化架構。
* [[!DNL Sandboxes]](../../sandboxes/home.md)： [!DNL Experience Platform]提供的虛擬沙箱可將單一[!DNL Platform]執行個體分割成個別的虛擬環境，以利開發及改進數位體驗應用程式。

下列章節提供您需瞭解的其他資訊，才能成功呼叫[!DNL Profile] API端點。

## 讀取範例 API 呼叫

資料擷取API檔案提供範例API呼叫，示範如何正確格式化請求。 這些包括路徑、必要的標頭和正確格式化的請求承載。 此外，也提供 API 回應中傳回的範例 JSON。 如需檔案中所使用範例API呼叫慣例的詳細資訊，請參閱[!DNL Experience Platform]疑難排解指南中[如何讀取範例API呼叫](../../landing/troubleshooting.md#how-do-i-format-an-api-request)一節。

## 必要的標頭

API檔案也要求您完成[驗證教學課程](https://www.adobe.com/go/platform-api-authentication-en)，才能成功呼叫[!DNL Platform]端點。 完成驗證教學課程會提供[!DNL Experience Platform] API呼叫中每個必要標題的值，如下所示：

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

要求內文中具有裝載的所有要求(例如POST、PUT和PATCH呼叫)都必須包含`Content-Type`標頭。 呼叫引數中會提供每個呼叫專屬的接受值。

[!DNL Experience Platform]中的所有資源都與特定的虛擬沙箱隔離。 對[!DNL Platform] API的請求需要一個標頭，該標頭會指定將在其中執行操作的沙箱的名稱：

* `x-sandbox-name: {SANDBOX_NAME}`

如需[!DNL Platform]中沙箱的詳細資訊，請參閱[沙箱概觀檔案](../../sandboxes/home.md)。
