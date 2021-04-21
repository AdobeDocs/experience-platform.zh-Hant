---
keywords: Experience Platform;home；熱門主題；目錄服務；目錄服務；目錄服務；目錄
solution: Experience Platform
title: 目錄服務API指南
topic-legacy: developer guide
description: Catalog Service API可讓開發人員管理Adobe Experience Platform的資料集中繼資料。 請依照本指南，瞭解如何使用API執行關鍵作業。
exl-id: 812fcdae-ed0e-4f2b-84d7-26f2f79e71b9
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '600'
ht-degree: 0%

---

# [!DNL Catalog Service] API指南

[!DNL Catalog Service] 是Adobe Experience Platform境內資料位置和世系記錄系統。[!DNL Catalog] 可當成中繼資料存放區或「目錄」，讓您在其中找到有關資料的資訊 [!DNL Experience Platform]，而不需存取資料本身。如需詳細資訊，請參閱[[!DNL Catalog] overview](../home.md)。

本開發人員指南提供協助您開始使用[!DNL Catalog] API的步驟。 然後，該指南提供使用[!DNL Catalog]執行鍵操作的示例API調用。

## 先決條件

[!DNL Catalog] 跟蹤中數種資源和操作的元資料 [!DNL Experience Platform]。本開發人員指南要求您對建立和管理這些資源時涉及的各種[!DNL Experience Platform]服務有良好的瞭解：

* [[!DNL Experience Data Model (XDM)]](../../xdm/home.md):組織客戶體驗資 [!DNL Platform] 料的標準化架構。
* [批次擷取](../../ingestion/batch-ingestion/overview.md):如何 [!DNL Experience Platform] 從資料檔案（例如CSV和Parpec）中擷取和儲存資料。
* [串流擷取](../../ingestion/streaming-ingestion/overview.md):如 [!DNL Experience Platform] 何即時從用戶端和伺服器端裝置收集和儲存資料。

以下各節提供您必須知道或掌握的額外資訊，才能成功呼叫[!DNL Catalog Service] API。

## 讀取範例API呼叫

本指南提供範例API呼叫，以示範如何格式化您的請求。 這些包括路徑、必要標題和正確格式化的請求負載。 也提供API回應中傳回的範例JSON。 如需範例API呼叫檔案中所用慣例的詳細資訊，請參閱[!DNL Experience Platform]疑難排解指南中[如何讀取範例API呼叫](../../landing/troubleshooting.md#how-do-i-format-an-api-request)一節。

## 收集必要標題的值

若要呼叫[!DNL Platform] API，您必須先完成[驗證教學課程](https://www.adobe.com/go/platform-api-authentication-en)。 完成驗證教學課程後，所有[!DNL Experience Platform] API呼叫中每個所需標題的值都會顯示在下面：

* 授權：載體`{ACCESS_TOKEN}`
* x-api-key:`{API_KEY}`
* x-gw-ims-org-id:`{IMS_ORG}`

[!DNL Experience Platform]中的所有資源都隔離到特定的虛擬沙盒。 對[!DNL Platform] API的所有請求都需要一個標題，該標題指定要在中執行操作的沙盒的名稱：

* x-sandbox-name:`{SANDBOX_NAME}`

>[!NOTE]
>
>如需[!DNL Platform]中沙盒的詳細資訊，請參閱[沙盒概述檔案](../../sandboxes/home.md)。

所有包含裝載(POST、PUT、PATCH)的請求都需要額外的標題：

* 內容類型：application/json

## [!DNL Catalog] API呼叫的最佳實務

當對[!DNL Catalog] API執行GET請求時，最佳實務是在請求中加入查詢參數，以便只傳回所需的物件和屬性。 未篩選的請求可能導致回應負載達到超過3GB的大小，進而降低整體效能。

您可以在請求路徑中加入特定物件的ID，或使用查詢參數（例如`properties`和`limit`）來篩選回應，以檢視特定物件。 篩選器可以作為標題和查詢參數傳遞，而傳遞的作為查詢參數優先。 如需詳細資訊，請參閱[篩選目錄資料](filter-data.md)上的檔案。

由於某些查詢會給API帶來沈重負載，因此[!DNL Catalog]查詢已實作全域限制，以進一步支援最佳實務。

## 後續步驟

本檔案涵蓋對[!DNL Catalog] API進行呼叫所需的先決條件知識。 您現在可以繼續閱讀本開發人員指南中提供的範例呼叫，並依照其指示進行。

本指南中的大多數示例使用`/dataSets`端點，但原則可套用至[!DNL Catalog]（例如`/batches`和`/accounts`）內的其他端點。 有關每個端點可用的所有調用和操作的完整清單，請參閱[目錄服務API參考](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml)。

如需示範[!DNL Catalog] API如何與資料擷取相關的逐步工作流程，請參閱[建立資料集](../datasets/create.md)的教學課程。
