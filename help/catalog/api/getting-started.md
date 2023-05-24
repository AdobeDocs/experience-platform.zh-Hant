---
keywords: Experience Platform；首頁；熱門主題；目錄服務；目錄服務；目錄服務；目錄
solution: Experience Platform
title: 目錄服務API指南
description: 目錄服務API允許開發人員管理Adobe Experience Platform的資料集元資料。 請遵循本指南以了解如何使用 API 執行關鍵作業。
exl-id: 812fcdae-ed0e-4f2b-84d7-26f2f79e71b9
source-git-commit: 74867f56ee13430cbfd9083a916b7167a9a24c01
workflow-type: tm+mt
source-wordcount: '596'
ht-degree: 3%

---

# [!DNL Catalog Service] API指南

[!DNL Catalog Service] 是Adobe Experience Platform內資料位置和世系的記錄系統。 [!DNL Catalog] 充當元資料儲存或「目錄」，在此您可以查找有關資料的資訊 [!DNL Experience Platform]而不需要訪問資料本身。 查看 [[!DNL Catalog] 概述](../home.md) 的子菜單。

本開發人員指南提供了幫助您開始使用 [!DNL Catalog] API。 然後，指南提供了用於使用 [!DNL Catalog]。

## 先決條件

[!DNL Catalog] 跟蹤內多種資源和操作的元資料 [!DNL Experience Platform]。 本開發人員指南要求對各種 [!DNL Experience Platform] 建立和管理這些資源所涉及的服務：

* [[!DNL Experience Data Model (XDM)]](../../xdm/home.md):標準化框架 [!DNL Platform] 組織客戶體驗資料。
* [批量攝取](../../ingestion/batch-ingestion/overview.md):如何 [!DNL Experience Platform] 從資料檔案（如CSV和Parket）中接收和儲存資料。
* [流攝入](../../ingestion/streaming-ingestion/overview.md):如何 [!DNL Experience Platform] 即時從客戶端和伺服器端設備接收和儲存資料。

以下各節提供了您需要瞭解或掌握的其他資訊，以便成功呼叫 [!DNL Catalog Service] API。

## 讀取示例API調用

本指南提供了示例API調用，以演示如何格式化請求。 這些包括路徑、必需的標頭和正確格式化的請求負載。 還提供了API響應中返回的示例JSON。 有關示例API調用文檔中使用的約定的資訊，請參見上的 [如何讀取示例API調用](../../landing/troubleshooting.md#how-do-i-format-an-api-request) 的 [!DNL Experience Platform] 疑難解答指南。

## 收集所需標題的值

為了呼叫 [!DNL Platform] API，必須首先完成 [驗證教程](https://www.adobe.com/go/platform-api-authentication-en)。 完成身份驗證教程將提供所有中每個必需標頭的值 [!DNL Experience Platform] API調用，如下所示：

* 授權：持 `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{ORG_ID}`

中的所有資源 [!DNL Experience Platform] 與特定虛擬沙箱隔離。 所有請求 [!DNL Platform] API需要一個標頭，該標頭指定操作將在以下位置進行的沙盒的名稱：

* x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>有關中的沙箱的詳細資訊 [!DNL Platform]，請參見 [沙盒概述文檔](../../sandboxes/home.md)。

包含負載(POST、PUT、PATCH)的所有請求都需要附加的標頭：

* 內容類型：應用程式/json

## 最佳實踐 [!DNL Catalog] API調用

執行GET請求時 [!DNL Catalog] API，最佳做法是將查詢參數包括在請求中，以便僅返回所需的對象和屬性。 未篩選的請求可能導致響應負載大小超過3GB，從而降低整體效能。

可以通過將特定對象的ID包括在請求路徑中或使用查詢參數(如 `properties` 和 `limit` 來篩選響應。 篩選器可以作為標題和查詢參數傳遞，而作為查詢參數傳遞的篩選器優先。 查看上的文檔 [篩選目錄資料](filter-data.md) 的子菜單。

由於某些查詢可能給API帶來沈重負載，因此已對 [!DNL Catalog] 查詢以進一步支援最佳實踐。

## 後續步驟

本文檔涵蓋了呼叫 [!DNL Catalog] API。 現在，您可以繼續閱讀本開發人員指南中提供的示例調用，並按照其說明進行操作。

本指南中的大多數示例使用 `/dataSets` 端點，但該原則可應用於內部的其他端點 [!DNL Catalog] (例如 `/batches` 和 `/accounts`)。 查看 [目錄服務API參考](https://www.adobe.io/experience-platform-apis/references/catalog/) 以獲取每個端點可用的所有調用和操作的完整清單。

對於演示如何 [!DNL Catalog] API涉及資料接收，請參見上的教程 [建立資料集](../datasets/create.md)。
