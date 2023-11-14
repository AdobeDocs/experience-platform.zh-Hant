---
keywords: Experience Platform；首頁；熱門主題；目錄服務；目錄；目錄服務；目錄
solution: Experience Platform
title: 目錄服務API指南
description: 目錄服務API可讓開發人員管理Adobe Experience Platform中的資料集中繼資料。 請遵循本指南以了解如何使用 API 執行關鍵作業。
exl-id: 812fcdae-ed0e-4f2b-84d7-26f2f79e71b9
source-git-commit: 07451b8ab4bcb7ca43ad0c8a821478b2c9682894
workflow-type: tm+mt
source-wordcount: '595'
ht-degree: 31%

---

# [!DNL Catalog Service] API指南

[!DNL Catalog Service] 是Adobe Experience Platform中資料位置和譜系的記錄系統。 [!DNL Catalog] 做為中繼資料存放區或「目錄」，您可在其中找到有關您資料的資訊 [!DNL Experience Platform]，而不需要存取資料本身。 請參閱 [[!DNL Catalog] 概述](../home.md) 以取得詳細資訊。

本開發人員指南提供了協助您開始使用 [!DNL Catalog] API 的步驟。 接著，指南會提供範例API呼叫，說明如何使用執行關鍵作業 [!DNL Catalog].

## 先決條件

[!DNL Catalog] 在中追蹤數種資源和作業的中繼資料 [!DNL Experience Platform]. 這份開發人員指南需要您實際瞭解各種 [!DNL Experience Platform] 與建立和管理這些資源相關的服務：

* [[!DNL Experience Data Model (XDM)]](../../xdm/home.md)：[!DNL Platform] 據以組織客戶體驗資料的標準化框架。
* [批次擷取](../../ingestion/batch-ingestion/overview.md)：如何 [!DNL Experience Platform] 從資料檔案擷取及儲存資料，例如CSV和Parquet。
* [串流擷取](../../ingestion/streaming-ingestion/overview.md)：如何 [!DNL Experience Platform] 從使用者端和伺服器端裝置即時擷取及儲存資料。

以下小節提供您需瞭解或有手頭的其他資訊，才能成功呼叫 [!DNL Catalog Service] API。

## 讀取範例 API 呼叫

本指南提供範例 API 呼叫，示範如何格式化您的請求。 這些包括路徑、必要的標頭和正確格式化的請求承載。 此外，也提供 API 回應中傳回的範例 JSON。 如需文件中用於範例 API 呼叫的慣例相關資訊，請參閱 [ 疑難排解指南中的](../../landing/troubleshooting.md#how-do-i-format-an-api-request)如何讀取範例 API 呼叫[!DNL Experience Platform]一節。

## 收集所需標頭的值

為了對 [!DNL Platform] API 進行呼叫，您必須先完成[驗證教學課程](https://www.adobe.com/go/platform-api-authentication-en)。完成驗證教學課程會提供所有 [!DNL Experience Platform] API 呼叫中每個必要標頭的值，如下所示：

* 授權：持有人 `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{ORG_ID}`

中的所有資源 [!DNL Experience Platform] 會隔離至特定的虛擬沙箱。 所有要求至 [!DNL Platform] API需要標頭，用以指定將進行作業的沙箱名稱：

* x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>如需中沙箱的詳細資訊 [!DNL Platform]，請參閱 [沙箱概述檔案](../../sandboxes/home.md).

所有包含承載 (POST、PUT、PATCH) 的請求都需有額外的標頭：

* Content-Type： application/json

## 以下專案的最佳實務 [!DNL Catalog] API呼叫

執行對的GET請求時 [!DNL Catalog] API的最佳作法是在您的要求中包含查詢引數，以便僅傳回您需要的物件和屬性。 未篩選的請求可能會導致回應裝載的大小超過3GB，進而減慢整體效能。

您可以在請求路徑中包含特定物件的ID來檢視這些物件，或使用查詢引數，例如 `properties` 和 `limit` 以篩選回應。 篩選器可作為標題和查詢引數傳遞，以作為查詢引數傳遞的篩選器優先。 檢視檔案： [篩選目錄資料](filter-data.md) 以取得詳細資訊。

由於某些查詢可能會對API造成大量負載，因此已在上實施全域限制 [!DNL Catalog] 進一步支援最佳實務的查詢。

## 後續步驟

本文件說明對 [!DNL Catalog] API 進行呼叫所需的先決條件知識。您現在可以繼續進行本開發人員指南中提供的範例呼叫，並遵循其指示進行作業。

本指南中的大多數範例使用 `/dataSets` 端點，但原則可套用至內的其他端點 [!DNL Catalog] (例如 `/batches`)。 請參閱 [目錄服務API參考](https://www.adobe.io/experience-platform-apis/references/catalog/) 以取得每個端點所有可用呼叫和作業的完整清單。

如需逐步工作流程，此工作流程會示範 [!DNL Catalog] API與資料擷取有關，請參閱以下主題上的教學課程： [建立資料集](../datasets/create.md).
