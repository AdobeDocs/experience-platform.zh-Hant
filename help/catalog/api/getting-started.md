---
keywords: Experience Platform；首頁；熱門主題；目錄服務；目錄；目錄服務；目錄
solution: Experience Platform
title: 目錄服務API指南
description: 目錄服務API可讓開發人員管理Adobe Experience Platform中的資料集中繼資料。 請遵循本指南以了解如何使用 API 執行關鍵作業。
exl-id: 812fcdae-ed0e-4f2b-84d7-26f2f79e71b9
source-git-commit: 07451b8ab4bcb7ca43ad0c8a821478b2c9682894
workflow-type: tm+mt
source-wordcount: '588'
ht-degree: 22%

---

# [!DNL Catalog Service] API指南

[!DNL Catalog Service]是Adobe Experience Platform中資料位置和歷程的記錄系統。 [!DNL Catalog]充當中繼資料存放區或「目錄」，您可在[!DNL Experience Platform]中找到有關您資料的資訊，而無需存取資料本身。 如需詳細資訊，請參閱[[!DNL Catalog] 概觀](../home.md)。

本開發人員指南提供了協助您開始使用 [!DNL Catalog] API 的步驟。 然後指南會提供使用[!DNL Catalog]執行關鍵作業的API呼叫範例。

## 先決條件

[!DNL Catalog]追蹤[!DNL Experience Platform]內多種資源與作業的中繼資料。 此開發人員指南需要實際瞭解與建立和管理這些資源有關的各種[!DNL Experience Platform]服務：

* [[!DNL Experience Data Model (XDM)]](../../xdm/home.md)： [!DNL Platform]用來組織客戶體驗資料的標準化架構。
* [批次內嵌](../../ingestion/batch-ingestion/overview.md)： [!DNL Experience Platform]如何內嵌及儲存資料檔案（例如CSV和Parquet）中的資料。
* [串流擷取](../../ingestion/streaming-ingestion/overview.md)： [!DNL Experience Platform]如何從使用者端和伺服器端裝置即時擷取及儲存資料。

下列章節提供您需知道或有手頭的其他資訊，才能成功呼叫[!DNL Catalog Service] API。

## 讀取範例 API 呼叫

本指南提供範例 API 呼叫，示範如何格式化您的請求。 這些包括路徑、必要的標頭和正確格式化的請求承載。 此外，也提供 API 回應中傳回的範例 JSON。 如需檔案中所使用範例API呼叫慣例的詳細資訊，請參閱[!DNL Experience Platform]疑難排解指南中[如何讀取範例API呼叫](../../landing/troubleshooting.md#how-do-i-format-an-api-request)一節。

## 收集所需標頭的值

若要呼叫[!DNL Platform] API，您必須先完成[驗證教學課程](https://www.adobe.com/go/platform-api-authentication-en)。 完成驗證教學課程會提供所有 [!DNL Experience Platform] API 呼叫中每個必要標頭的值，如下所示：

* 授權：持有人`{ACCESS_TOKEN}`
* x-api-key： `{API_KEY}`
* x-gw-ims-org-id： `{ORG_ID}`

[!DNL Experience Platform]中的所有資源都與特定的虛擬沙箱隔離。 對[!DNL Platform] API的所有請求都需要標頭，以指定將在其中執行作業的沙箱名稱：

* x-sandbox-name： `{SANDBOX_NAME}`

>[!NOTE]
>
>如需[!DNL Platform]中沙箱的詳細資訊，請參閱[沙箱概觀檔案](../../sandboxes/home.md)。

所有包含承載 (POST、PUT、PATCH) 的請求都需有額外的標頭：

* Content-Type： application/json

## [!DNL Catalog] API呼叫的最佳實務

對[!DNL Catalog] API執行GET要求時，最佳實務是在要求中包含查詢引數，以便僅傳回您需要的物件和屬性。 未篩選的請求可能會導致回應裝載的大小超過3GB，進而減慢整體效能。

您可以在要求路徑中包含特定物件的識別碼，或使用`properties`和`limit`等查詢引數來篩選回應，藉此檢視特定物件。 篩選器可作為標題和查詢引數傳遞，以作為查詢引數傳遞的篩選器優先。 如需詳細資訊，請參閱[篩選目錄資料](filter-data.md)上的檔案。

由於某些查詢可能會對API造成大量負載，因此已在[!DNL Catalog]個查詢上實作全域限制，以進一步支援最佳實務。

## 後續步驟

本文件說明對 [!DNL Catalog] API 進行呼叫所需的先決條件知識。您現在可以繼續進行本開發人員指南中提供的範例呼叫，並遵循其指示進行作業。

本指南中的大多數範例使用`/dataSets`端點，但原則可套用至[!DNL Catalog]內的其他端點（例如`/batches`）。 如需每個端點可用的所有呼叫和作業的完整清單，請參閱[目錄服務API參考](https://www.adobe.io/experience-platform-apis/references/catalog/)。

如需示範[!DNL Catalog] API如何參與資料擷取的逐步工作流程，請參閱[建立資料集](../datasets/create.md)的教學課程。
