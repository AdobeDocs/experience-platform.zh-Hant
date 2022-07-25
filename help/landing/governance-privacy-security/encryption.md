---
title: Adobe Experience Platform資料加密
topic-legacy: data protection
description: 瞭解資料在傳輸過程中和在Adobe Experience Platform的休息時如何加密。
exl-id: 184b2b2d-8cd7-4299-83f8-f992f585c336
source-git-commit: 1ab1c269fd43368e059a76f96b3eb3ac4e7b8388
workflow-type: tm+mt
source-wordcount: '398'
ht-degree: 3%

---

# Adobe Experience Platform資料加密

Adobe Experience Platform是一個功能強大且可擴展的系統，可跨企業解決方案集中和標準化客戶體驗資料。 平台使用的所有資料在傳輸過程中和靜止時都經過加密，以保證資料安全。 本文檔從高級別描述了平台的加密過程。

以下流程圖說明了資料如何被攝取、加密和保留 [!DNL Experience Platform]:

![](../images/governance-privacy-security/encryption/flow.png)

## 在途資料 {#in-transit}

平台和任何外部元件之間傳輸的所有資料都通過使用HTTPS的安全加密連接進行 [TLS 1.2版](https://datatracker.ietf.org/doc/html/rfc5246)。

通常，資料通過三種方式被引入平台：

* [資料收集](../../collection/home.md) 功能允許網站和移動應用程式將資料發送到平台邊緣網路，以便準備準備接收。
* [源連接器](../../sources/home.md) 將資料從Adobe Experience Cloud應用程式和其他企業資料源直接流到平台。
* 非AdobeETL（提取、轉換、載入）工具將資料發送到 [批處理接收API](../../ingestion/batch-ingestion/overview.md) 為消費。

在將資料引入系統後 [在靜止時加密](#at-rest)然後通過平台服務來豐富並通過以下方式從系統中引出：

* [目標](../../destinations/home.md) 允許您激活資料以Adobe應用程式和合作夥伴應用程式。
* 本機平台應用程式，如 [Customer Journey Analytics](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-overview/cja-overview.html?lang=zh-Hant) 和 [Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/ajo-home.html?lang=zh-Hant) 也可以利用資料。

## 靜態資料 {#at-rest}

平台所攝取和使用的資料儲存在資料湖中，該資料湖是一個高度精細的資料儲存庫，包含由系統管理的所有資料，而不管其來源或檔案格式如何。 資料湖中保留的所有資料都在隔離的環境中加密、儲存和管理 [[!DNL Microsoft Azure Data Lake] 儲存](https://docs.microsoft.com/en-us/azure/storage/blobs/data-lake-storage-introduction) 對您的組織唯一的實例。

有關在Azure Data Lake Storage和Cosmos DB中如何加密靜態資料的詳細資訊，請參閱 [正式Azure文檔](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-encryption)。

## 後續步驟

本文檔提供了在平台中如何加密資料的高級概述。 有關平台中安全過程的詳細資訊，請參閱 [治理、隱私和安全](./overview.md) Experience League，或者看看 [平台安全白皮書](https://www.adobe.com/content/dam/cc/en/security/pdfs/AEP_SecurityOverview.pdf)。
