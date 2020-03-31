---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 目錄服務開發人員指南
topic: developer guide
translation-type: tm+mt
source-git-commit: eec5b07427aa9daa44d23f09cfaf1b38f8e811f3

---


# 目錄服務開發人員指南

目錄服務是Adobe Experience Platform中資料位置和世系的記錄系統。 目錄可當成中繼資料存放區或「目錄」，讓您在Experience Platform中尋找有關資料的資訊，而不需存取資料本身。 如需詳細 [資訊，請參閱](../home.md) 「目錄」總覽。

本開發人員指南提供協助您開始使用目錄API的步驟。 然後，本指南提供使用目錄執行關鍵操作的範例API調用。

## 必要條件

目錄可追蹤Experience Platform中數種資源與作業的中繼資料。 本開發人員指南需要對建立和管理這些資源時涉及的各種Experience Platform服務有良好的認識：

* [體驗資料模型(XDM)](../../xdm/home.md):平台組織客戶體驗資料的標準化架構。
* [批次擷取](../../ingestion/batch-ingestion/overview.md):Experience Platform如何從資料檔案（例如CSV和Parpec）擷取和儲存資料。
* [串流擷取](../../ingestion/streaming-ingestion/overview.md):Experience Platform如何即時從用戶端和伺服器端裝置擷取和儲存資料。

以下各節提供您必須知道或掌握的額外資訊，才能成功呼叫目錄服務API。

## 讀取範例API呼叫

本指南提供範例API呼叫，以示範如何格式化您的請求。 這些包括路徑、必要標題和正確格式化的請求負載。 也提供API回應中傳回的範例JSON。 如需範例API呼叫檔案中所用慣例的詳細資訊，請參閱「Experience Platform疑難排解指 [南」中有關如何讀取範例API呼叫的章節](../../landing/troubleshooting.md#how-do-i-format-an-api-request) 。

## 收集必要標題的值

若要呼叫平台API，您必須先完成驗證教 [學課程](../../tutorials/authentication.md)。 完成驗證教學課程後，所有Experience Platform API呼叫中每個必要標題的值都會顯示在下方：

* 授權：生產者 `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Experience Platform中的所有資源都隔離至特定的虛擬沙盒。 所有對平台API的請求都需要一個標題，該標題會指定要在中執行的操作的沙盒名稱：

* x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE] 如需平台中沙盒的詳細資訊，請參閱沙盒 [概觀檔案](../../sandboxes/home.md)。

所有包含裝載(POST、PUT、PATCH)的請求都需要額外的標題：

* 內容類型：application/json

## 目錄API呼叫的最佳實務

當對目錄API執行GET請求時，最佳實務是在請求中加入查詢參數，以便只傳回所需的物件和屬性。 未篩選的請求可能導致回應負載達到超過3GB的大小，進而降低整體效能。

您可以在請求路徑中加入特定物件的ID，或使用查詢參數（例如和）來 `properties` 篩選 `limit` 回應，以檢視其。 篩選器可以作為標題和查詢參數傳遞，而傳遞的作為查詢參數優先。 如需詳細資訊，請 [參閱篩選目錄資料](filter-data.md) 的檔案。

由於某些查詢會給API帶來沈重負載，因此已對目錄查詢實施全域限制，以進一步支援最佳實務。

## 後續步驟

本檔案涵蓋進行目錄API呼叫所需的先決條件知識。 您現在可以繼續閱讀本開發人員指南中提供的範例呼叫，並依照其指示進行。

本指南中的大部分範例都使用端 `/dataSets` 點，但原則可套用至目錄內的其他端點( `/batches` 例如 `/accounts`和)。 如需每個 [端點所有可用呼叫和作業的完整清單](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml) ，請參閱目錄服務API參考。

如需示範目錄API如何與資料擷取相關的逐步工作流程，請參閱建立資料集 [的教學課程](../datasets/create.md)。
