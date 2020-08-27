---
keywords: Experience Platform;home;popular topics;catalog service;catalog;Catalog service;Catalog
solution: Experience Platform
title: 目錄服務開發人員指南
topic: developer guide
description: 本開發人員指南提供協助您開始使用目錄API的步驟。 然後，本指南提供使用目錄執行關鍵操作的範例API調用。
translation-type: tm+mt
source-git-commit: c8e53a25c5b22e8d840658fe26ff47875947a6d0
workflow-type: tm+mt
source-wordcount: '588'
ht-degree: 0%

---


# [!DNL Catalog Service] 開發人員指南

[!DNL Catalog Service] 是Adobe Experience Platform中資料位置和世系的記錄系統。 [!DNL Catalog] 可當成中繼資料存放區或「目錄」，讓您在其中找到有關資料的資訊 [!DNL Experience Platform]，而不需存取資料本身。 如需詳細 [[!DNL Catalog] 資訊](../home.md) ，請參閱總覽。

本開發人員指南提供協助您開始使用 [!DNL Catalog] API的步驟。 然後，本指南提供使用執行關鍵操作的範例API調用 [!DNL Catalog]。

## 必要條件

[!DNL Catalog] 跟蹤中數種資源和操作的元資料 [!DNL Experience Platform]。 本開發人員指南需要對建立和管理這些資 [!DNL Experience Platform] 源所涉及的各種服務有良好的認識：

* [[!DNL體驗資料模型(XDM)]](../../xdm/home.md):組織客戶體驗資料 [!DNL Platform] 的標準化架構。
* [批次擷取](../../ingestion/batch-ingestion/overview.md):如何 [!DNL Experience Platform] 從資料檔案（例如CSV和Parpec）中擷取和儲存資料。
* [串流擷取](../../ingestion/streaming-ingestion/overview.md):如 [!DNL Experience Platform] 何即時從用戶端和伺服器端裝置擷取和儲存資料。

以下章節提供您必須知道或掌握的額外資訊，才能成功呼叫 [!DNL Catalog Service] API。

## 讀取範例API呼叫

本指南提供範例API呼叫，以示範如何格式化您的請求。 這些包括路徑、必要標題和正確格式化的請求負載。 也提供API回應中傳回的範例JSON。 如需範例API呼叫檔案中所用慣例的詳細資訊，請參閱疑難排解指 [南中有關如何讀取範例API呼叫的](../../landing/troubleshooting.md#how-do-i-format-an-api-request)[!DNL Experience Platform] 章節。

## 收集必要標題的值

若要呼叫API，您必 [!DNL Platform] 須先完成驗證教 [學課程](../../tutorials/authentication.md)。 完成驗證教學課程後，將提供所有 [!DNL Experience Platform] API呼叫中每個必要標題的值，如下所示：

* 授權：生產者 `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

中的所有資 [!DNL Experience Platform] 源都與特定虛擬沙盒隔離。 對API的所 [!DNL Platform] 有請求都需要一個標題，該標題會指定要在中執行的操作的沙盒名稱：

* x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>如需中沙盒的詳細資訊 [!DNL Platform]，請參閱沙 [盒概述檔案](../../sandboxes/home.md)。

所有包含裝載(POST、PUT、PATCH)的請求都需要額外的標題：

* 內容類型：application/json

## API呼叫的最 [!DNL Catalog] 佳實務

當對 [!DNL Catalog] API執行GET請求時，最佳實務是在請求中加入查詢參數，以便只傳回您需要的物件和屬性。 未篩選的請求可能導致回應負載達到超過3GB的大小，進而降低整體效能。

您可以在請求路徑中加入特定物件的ID，或使用查詢參數（例如和）來 `properties` 篩選 `limit` 回應，以檢視其。 篩選器可以作為標題和查詢參數傳遞，而傳遞的作為查詢參數優先。 如需詳細資訊，請 [參閱篩選目錄資料](filter-data.md) 的檔案。

由於某些查詢會給API帶來沈重負載，因此已對查詢實施全域限制，以進 [!DNL Catalog] 一步支援最佳實務。

## 後續步驟

本檔案涵蓋對 [!DNL Catalog] API進行呼叫所需的先決知識。 您現在可以繼續閱讀本開發人員指南中提供的範例呼叫，並依照其指示進行。

本指南中的大部分範例都使用端 `/dataSets` 點，但原則可套用至內部的其 [!DNL Catalog] 他端點( `/batches` 例如和 `/accounts`)。 如需每個 [端點所有可用呼叫和作業的完整清單](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml) ，請參閱目錄服務API參考。

如需示範API如何與資料擷取相關的逐步工作流程，請參閱有關建立資料集 [!DNL Catalog] 的教學課程 [](../datasets/create.md)。
