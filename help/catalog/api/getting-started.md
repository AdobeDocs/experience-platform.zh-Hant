---
keywords: Experience Platform；首頁；熱門主題；目錄服務；目錄服務；目錄
solution: Experience Platform
title: 目錄服務API指南
description: 目錄服務API可讓開發人員管理Adobe Experience Platform中的資料集中繼資料。 請遵循本指南以了解如何使用 API 執行關鍵作業。
exl-id: 812fcdae-ed0e-4f2b-84d7-26f2f79e71b9
source-git-commit: 74867f56ee13430cbfd9083a916b7167a9a24c01
workflow-type: tm+mt
source-wordcount: '596'
ht-degree: 3%

---

# [!DNL Catalog Service] API指南

[!DNL Catalog Service] 是Adobe Experience Platform內用於資料位置和世系的記錄系統。 [!DNL Catalog] 可做為中繼資料存放區或「目錄」，您可在其中找到資料的相關資訊 [!DNL Experience Platform]，而無須存取資料本身。 請參閱 [[!DNL Catalog] 概述](../home.md) 以取得更多資訊。

本開發人員指南提供步驟，協助您開始使用 [!DNL Catalog] API。 然後，指南會提供範例API呼叫，以使用 [!DNL Catalog].

## 先決條件

[!DNL Catalog] 跟蹤內多種資源和操作的元資料 [!DNL Experience Platform]. 本開發人員指南需要妥善了解 [!DNL Experience Platform] 與建立和管理這些資源有關的服務：

* [[!DNL Experience Data Model (XDM)]](../../xdm/home.md):標準化框架 [!DNL Platform] 組織客戶體驗資料。
* [批次內嵌](../../ingestion/batch-ingestion/overview.md):如何 [!DNL Experience Platform] 擷取並儲存資料檔案（例如CSV和Parquet）中的資料。
* [串流內嵌](../../ingestion/streaming-ingestion/overview.md):如何 [!DNL Experience Platform] 即時從用戶端和伺服器端裝置擷取和儲存資料。

以下小節提供您必須知道或擁有的其他資訊，才能成功呼叫 [!DNL Catalog Service] API。

## 讀取範例API呼叫

本指南提供範例API呼叫，以示範如何設定請求格式。 這些功能包括路徑、必要標題和格式正確的請求裝載。 也提供API回應中傳回的範例JSON。 如需範例API呼叫檔案中所使用慣例的相關資訊，請參閱 [如何閱讀API呼叫範例](../../landing/troubleshooting.md#how-do-i-format-an-api-request) 在 [!DNL Experience Platform] 疑難排解指南。

## 收集必要標題的值

若要對 [!DNL Platform] API，您必須先完成 [驗證教學課程](https://www.adobe.com/go/platform-api-authentication-en). 完成驗證教學課程會提供所有 [!DNL Experience Platform] API呼叫，如下所示：

* 授權：承載 `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{ORG_ID}`

中的所有資源 [!DNL Experience Platform] 與特定虛擬沙箱隔離。 所有請求 [!DNL Platform] API需要標頭，以指定要在中執行操作的沙箱名稱：

* x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>如需中沙箱的詳細資訊，請參閱 [!DNL Platform]，請參閱 [沙箱概述檔案](../../sandboxes/home.md).

所有包含裝載(POST、PUT、PATCH)的請求都需要額外的標題：

* 內容類型：application/json

## 最佳實務 [!DNL Catalog] API呼叫

對執行GET請求時 [!DNL Catalog] API，最佳實務是在要求中納入查詢參數，以便只傳回您需要的物件和屬性。 未篩選的請求可能會導致回應裝載的大小超過3GB，進而降低整體效能。

您可以在請求路徑中加入特定物件的ID，或使用查詢參數，例如 `properties` 和 `limit` 來篩選回應。 篩選器可以作為標題和查詢參數傳遞，而傳遞的則以查詢參數為優先。 請參閱 [篩選目錄資料](filter-data.md) 以取得更多資訊。

由於某些查詢可能會對API造成大量負載，因此已對實作全域限制 [!DNL Catalog] 查詢以進一步支援最佳實務。

## 後續步驟

本檔案說明呼叫 [!DNL Catalog] API。 您現在可以繼續閱讀開發人員指南中提供的範例呼叫，並遵循其指示。

本指南中的大部分範例都使用 `/dataSets` 端點，但原則可套用至內的其他端點 [!DNL Catalog] (例如 `/batches` 和 `/accounts`)。 請參閱 [目錄服務API參考](https://www.adobe.io/experience-platform-apis/references/catalog/) 以取得每個端點可用的所有呼叫和操作的完整清單。

用於示範如何 [!DNL Catalog] API與資料擷取相關，請參閱 [建立資料集](../datasets/create.md).
