---
title: Adobe Experience Platform中的資料加密
description: 瞭解如何在Adobe Experience Platform中加密傳輸和待用資料。
exl-id: 184b2b2d-8cd7-4299-83f8-f992f585c336
source-git-commit: fd31d54339b8d87b80799a9c0fa167cc9a07a33f
workflow-type: tm+mt
source-wordcount: '736'
ht-degree: 0%

---

# Adobe Experience Platform中的資料加密

Adobe Experience Platform是功能強大且可擴充的系統，可集中化及標準化各企業解決方案的客戶體驗資料。 Platform使用的所有資料在傳輸和待用時都會經過加密，以確保您的資料安全。 本檔案以高階方式說明Platform的加密程式。

下列程式流程圖說明Experience Platform如何擷取、加密及儲存資料：

![此圖表會說明資料如何透過Experience Platform擷取、加密及持續儲存。](../images/governance-privacy-security/encryption/flow.png)

## 傳輸中的資料 {#in-transit}

Platform與任何外部元件之間傳輸的所有資料，都會使用HTTPS透過安全、加密的連線進行 [TLS v1.2](https://datatracker.ietf.org/doc/html/rfc5246).

一般而言，資料會透過三種方式帶入Platform：

- [資料彙集](../../collection/home.md) 功能可讓網站和行動應用程式將資料傳送至PlatformEdge Network，以進行測試和擷取準備。
- [來源聯結器](../../sources/home.md) 從Adobe Experience Cloud應用程式和其他企業資料來源直接將資料串流到Platform。
- 非AdobeETL （擷取、轉換、載入）工具會將資料傳送至 [批次擷取API](../../ingestion/batch-ingestion/overview.md) 以消耗。

將資料帶入系統之後，以及 [靜態加密](#at-rest)，Platform服務會透過下列方式擴充及匯出資料：

- [目的地](../../destinations/home.md) 可讓您啟用資料以Adobe應用程式和合作夥伴應用程式。
- 原生平台應用程式，例如 [Customer Journey Analytics](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-overview/cja-overview.html?lang=zh-Hant) 和 [Adobe Journey Optimizer](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/ajo-home) 也可以使用資料。

### mTLS通訊協定支援 {#mtls-protocol-support}

您現在可以使用相互傳輸層安全性(mTLS)，確保對HTTP API目的地和Adobe Journey Optimizer自訂動作的輸出連線具有增強的安全性。 mTLS是一種用於相互驗證的端對端安全性方法，可確保共用資訊的雙方在共用資料之前，都是聲稱的身分。 mTLS包括相較於TLS的額外步驟，其中伺服器也會要求使用者端的憑證並在其末端驗證它。

#### Adobe Journey Optimizer中的mTLS {#mtls-in-adobe-journey-optimizer}

在Adobe Journey Optimizer中，mTLS會與 [自訂動作](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/using-custom-actions). 無其他 [Adobe Journey Optimizer自訂動作的設定](https://experienceleague.adobe.com/zh-hant/docs/journey-optimizer/using/configuration/configure-journeys/action-journeys/about-custom-action-configuration) 是啟用mTLS的必要條件。 當自訂動作的端點啟用mTLS時，系統會從Adobe Experience Platform金鑰存放區擷取憑證，並自動將其提供給端點（這是mTLS連線的必要）。

如果您想要將mTLS與這些Adobe Journey Optimizer和Experience PlatformHTTP API目標工作流程搭配使用，您放入Adobe Journey Optimizer客戶動作UI或目標UI的伺服器位址必須停用TLS通訊協定，並且僅啟用mTLS。 如果仍在端點上啟用TLS 1.2通訊協定，則不會傳送使用者端驗證的憑證。 這表示若要搭配這些工作流程使用mTLS，您的「接收」伺服器端點必須是mTLS **僅限** 已啟用連線端點。

>[!IMPORTANT]
>
>您的Adobe Journey Optimizer自訂動作或歷程中不需要額外設定，即可啟用mTLS；當偵測到啟用mTLS的端點時，此程式會自動發生。 每個憑證的一般名稱(CN)和主體替代名稱(SAN)都可在檔案中作為憑證的一部分提供，如果您希望這樣做，還可以用作其他所有權驗證層。
>
>RFC 2818於2000年5月發行，它不建議在HTTPS憑證中使用一般名稱(CN)欄位來進行主體名稱驗證。 它建議改用「dns名稱」型別的「主體替代名稱」延伸模組(SAN)。

### 下載憑證 {#download-certificates}

如果您要檢查CN或SAN以進行其他協力廠商驗證，可以在這裡下載相關憑證：

- [Adobe Journey Optimizer公開憑證](../images/governance-privacy-security/encryption/AJO-public-certificate.pem)
- [目的地服務公開憑證](../images/governance-privacy-security/encryption/destinations-public-cert.pem).

## 靜態資料 {#at-rest}

Platform擷取及使用的資料會儲存在Data Lake中，這是高精細度的資料存放區，包含系統管理的所有資料，無論來源或檔案格式為何。 資料湖中儲存的所有資料都會加密、儲存，並在隔離環境中進行管理 [[!DNL Microsoft Azure Data Lake] 儲存](https://docs.microsoft.com/en-us/azure/storage/blobs/data-lake-storage-introduction) 您的組織專屬的例項。

如需如何在Azure Data Lake儲存體中對閒置資料進行加密的詳細資訊，請參閱 [Azure官方檔案](https://learn.microsoft.com/en-us/azure/storage/common/storage-service-encryption).

## 後續步驟

本檔案提供Platform中資料加密方式的高層級概觀。 如需Platform安全性程式的詳細資訊，請參閱以下內容的概觀： [治理、隱私和安全性](./overview.md) Experience League，或檢視 [平台安全性白皮書](https://www.adobe.com/content/dam/cc/en/security/pdfs/AEP_SecurityOverview.pdf).
