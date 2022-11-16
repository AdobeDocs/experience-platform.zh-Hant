---
title: Adobe Experience Platform中的資料加密
topic-legacy: data protection
description: 了解在傳輸中和在Adobe Experience Platform中儲存資料時如何加密。
exl-id: 184b2b2d-8cd7-4299-83f8-f992f585c336
source-git-commit: d99a9081edc483831d56af3d838b67d9aba25bea
workflow-type: tm+mt
source-wordcount: '396'
ht-degree: 3%

---

# Adobe Experience Platform中的資料加密

Adobe Experience Platform是功能強大且可擴充的系統，可跨企業解決方案集中化及標準化客戶體驗資料。 Platform使用的所有資料都會在傳輸中和閒置時進行加密，以確保資料安全。 本檔案從高層次說明Platform的加密程式。

以下流程圖說明資料如何被擷取、加密及保存 [!DNL Experience Platform]:

![](../images/governance-privacy-security/encryption/flow.png)

## 傳輸中的資料 {#in-transit}

在Platform和任何外部元件之間傳輸的所有資料都會透過使用HTTPS的安全加密連線進行 [TLS v1.2](https://datatracker.ietf.org/doc/html/rfc5246).

一般而言，資料傳入Platform的方式有三種：

* [資料收集](../../collection/home.md) 功能可讓網站和行動應用程式將資料傳送至Platform Edge Network，以進行測試和準備擷取。
* [源連接器](../../sources/home.md) 從Adobe Experience Cloud應用程式和其他企業資料來源直接將資料串流至Platform。
* 非AdobeETL（擷取、轉換、載入）工具會將資料傳送至 [批次內嵌API](../../ingestion/batch-ingestion/overview.md) 用於消耗。

將資料帶入系統後， [靜態加密](#at-rest)，之後便能透過Platform服務加以擴充，並以下列方式從系統中推出：

* [目的地](../../destinations/home.md) 可讓您啟動資料，以Adobe應用程式和合作夥伴應用程式。
* 本機平台應用程式，例如 [Customer Journey Analytics](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-overview/cja-overview.html?lang=zh-Hant) 和 [Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/ajo-home.html) 也可以利用資料。

## 閒置資料 {#at-rest}

Platform擷取和使用的資料會儲存在資料湖中，這是一個高度精細的資料存放區，包含由系統管理的所有資料，無論來源或檔案格式為何。 所有保存在資料湖中的資料都會經過加密、儲存，並在隔離的 [[!DNL Microsoft Azure Data Lake] 儲存](https://docs.microsoft.com/en-us/azure/storage/blobs/data-lake-storage-introduction) 貴組織專屬的例項。

有關Azure Data Lake Storage中靜態資料的加密方式的詳細資訊，請參閱 [官方Azure檔案](https://learn.microsoft.com/en-us/azure/storage/common/storage-service-encryption).

## 後續步驟

本檔案概略說明Platform中資料加密的方式。 如需Platform中安全性程式的詳細資訊，請參閱 [控管、隱私權和安全性](./overview.md) Experience League，或查看 [平台安全性白皮書](https://www.adobe.com/content/dam/cc/en/security/pdfs/AEP_SecurityOverview.pdf).
