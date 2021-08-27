---
keywords: Experience Platform；首頁；熱門主題；目錄服務；目錄服務；目錄
solution: Experience Platform
title: 目錄服務API指南
topic-legacy: developer guide
description: 目錄服務API可讓開發人員管理Adobe Experience Platform中的資料集中繼資料。 請依照本指南，了解如何使用API執行重要作業。
exl-id: 812fcdae-ed0e-4f2b-84d7-26f2f79e71b9
source-git-commit: 5160bc8057a7f71e6b0f7f2d594ba414bae9d8f6
workflow-type: tm+mt
source-wordcount: '596'
ht-degree: 1%

---

# [!DNL Catalog Service] API指南

[!DNL Catalog Service] 是Adobe Experience Platform內用於資料位置和世系的記錄系統。[!DNL Catalog] 可做為中繼資料存放區或「目錄」，讓您在內尋找有關資料的資 [!DNL Experience Platform]訊，而不需存取資料本身。如需詳細資訊，請參閱[[!DNL Catalog] 概述](../home.md) 。

本開發人員指南提供步驟，協助您開始使用[!DNL Catalog] API。 然後，指南提供使用[!DNL Catalog]執行關鍵操作的API呼叫範例。

## 先決條件

[!DNL Catalog] 追蹤內數種資源和作業的中繼資 [!DNL Experience Platform]料。本開發人員指南需要有效了解與建立和管理這些資源相關的各種[!DNL Experience Platform]服務：

* [[!DNL Experience Data Model (XDM)]](../../xdm/home.md):組織客戶體驗資 [!DNL Platform] 料的標準化架構。
* [批次內嵌](../../ingestion/batch-ingestion/overview.md):如 [!DNL Experience Platform] 何從資料檔案（例如CSV和Parquet）擷取和儲存資料。
* [串流內嵌](../../ingestion/streaming-ingestion/overview.md):如 [!DNL Experience Platform] 何即時從用戶端和伺服器端裝置擷取和儲存資料。

以下各節提供您需要知道或掌握的其他資訊，以便成功呼叫[!DNL Catalog Service] API。

## 讀取範例API呼叫

本指南提供範例API呼叫，以示範如何設定請求格式。 這些功能包括路徑、必要標題和格式正確的請求裝載。 也提供API回應中傳回的範例JSON。 如需範例API呼叫檔案中所使用慣例的資訊，請參閱[!DNL Experience Platform]疑難排解指南中[如何讀取範例API呼叫](../../landing/troubleshooting.md#how-do-i-format-an-api-request)一節。

## 收集必要標題的值

若要呼叫[!DNL Platform] API，您必須先完成[authentication tutorial](https://www.adobe.com/go/platform-api-authentication-en)。 完成驗證教學課程後，將提供所有[!DNL Experience Platform] API呼叫中每個必要標題的值，如下所示：

* 授權：承載`{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

[!DNL Experience Platform]中的所有資源都與特定虛擬沙箱隔離。 對[!DNL Platform] API的所有請求都需要標題，以指定作業將在下列位置進行的沙箱名稱：

* x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>如需[!DNL Platform]中沙箱的詳細資訊，請參閱[沙箱概觀檔案](../../sandboxes/home.md)。

所有包含裝載(POST、PUT、PATCH)的請求都需要額外的標題：

* 內容類型：application/json

## [!DNL Catalog] API呼叫的最佳作法

對[!DNL Catalog] API執行GET要求時，最佳實務是在要求中納入查詢參數，以便只傳回您需要的物件和屬性。 未篩選的請求可能會導致回應裝載的大小超過3GB，進而降低整體效能。

您可以在請求路徑中加入特定物件的ID，或使用`properties`和`limit`等查詢參數來篩選回應，以檢視特定物件。 篩選器可以作為標題和查詢參數傳遞，而傳遞的則以查詢參數為優先。 如需詳細資訊，請參閱[篩選目錄資料](filter-data.md)的相關檔案。

由於某些查詢可能會對API造成大量負載，因此已對[!DNL Catalog]查詢實作全域限制，以進一步支援最佳實務。

## 後續步驟

本檔案說明呼叫[!DNL Catalog] API所需的先決條件知識。 您現在可以繼續閱讀開發人員指南中提供的範例呼叫，並遵循其指示。

本指南中的大多數範例使用`/dataSets`端點，但原則可套用至[!DNL Catalog]內的其他端點（例如`/batches`和`/accounts`）。 如需每個端點可用的所有呼叫和操作的完整清單，請參閱[目錄服務API參考](https://www.adobe.io/experience-platform-apis/references/catalog/)。

如需示範[!DNL Catalog] API如何與資料擷取相關的逐步工作流程，請參閱[建立資料集](../datasets/create.md)的教學課程。
