---
title: Adobe Experience Platform中的資料加密
description: 瞭解如何在Adobe Experience Platform中加密傳輸和待用資料。
exl-id: 184b2b2d-8cd7-4299-83f8-f992f585c336
source-git-commit: f6eaba4c0622318ba713c562ba0a4c20bba02338
workflow-type: tm+mt
source-wordcount: '849'
ht-degree: 0%

---

# Adobe Experience Platform中的資料加密

Adobe Experience Platform是功能強大且可擴充的系統，可集中化及標準化各企業解決方案的客戶體驗資料。 Experience Platform使用的所有資料在傳輸和待用時都會經過加密，以確保您的資料安全。 本檔案以高層級方式說明Experience Platform的加密程式。

下列程式流程圖說明Experience Platform如何擷取、加密及儲存資料：

![圖表可說明Experience Platform如何擷取、加密及儲存資料。](../images/governance-privacy-security/encryption/flow.png)

## 傳輸中的資料 {#in-transit}

Experience Platform與任何外部元件之間傳輸的所有資料都是使用HTTPS [TLS v1.2](https://datatracker.ietf.org/doc/html/rfc5246)，透過安全、加密的連線進行。

一般而言，資料會透過三種方式帶入Experience Platform：

- [資料彙集](../../collection/home.md)功能可讓網站和行動應用程式將資料傳送至Experience Platform Edge Network，以進行測試和擷取準備。
- [Source聯結器](../../sources/home.md)會從Adobe Experience Cloud應用程式和其他企業資料來源，直接將資料串流到Experience Platform。
- 非Adobe ETL （擷取、轉換、載入）工具會將資料傳送至[批次擷取API](../../ingestion/batch-ingestion/overview.md)以供使用。

將資料帶入系統並[加密待用](#at-rest)後，Experience Platform服務會以下列方式擴充及匯出資料：

- [目的地](../../destinations/home.md)可讓您對Adobe應用程式和合作夥伴應用程式啟用資料。
- 原生Experience Platform應用程式(例如[Customer Journey Analytics](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-overview/cja-overview.html?lang=zh-Hant)和[Adobe Journey Optimizer](https://experienceleague.adobe.com/zh-hant/docs/journey-optimizer/using/ajo-home))也可以使用資料。

### mTLS通訊協定支援 {#mtls-protocol-support}

您現在可以使用相互傳輸層安全性(mTLS)來確保與[HTTP API目的地](../../destinations/catalog/streaming/http-destination.md)和Adobe Journey Optimizer [自訂動作](https://experienceleague.adobe.com/zh-hant/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/using-custom-actions)的輸出連線中的增強安全性。 mTLS是一種用於相互驗證的端對端安全性方法，可確保共用資訊的雙方在共用資料之前，都是聲稱的身分。 mTLS包括相較於TLS的額外步驟，其中伺服器也會要求使用者端的憑證並在其末端驗證它。

若您要[搭配Adobe Journey Optimizer自訂動作](https://experienceleague.adobe.com/zh-hant/docs/journey-optimizer/using/configuration/configure-journeys/action-journeys/about-custom-action-configuration)和Experience Platform HTTP API目的地工作流程使用mTLS，則您放入Adobe Journey Optimizer客戶動作UI或目的地UI的伺服器位址必須停用TLS通訊協定，並且僅啟用mTLS。 如果仍在端點上啟用TLS 1.2通訊協定，則不會傳送使用者端驗證的憑證。 這表示若要搭配這些工作流程使用mTLS，您的「接收」伺服器端點必須是mTLS **僅限**&#x200B;啟用的連線端點。

>[!IMPORTANT]
>
>您的Adobe Journey Optimizer自訂動作或HTTP API目的地中不需要進行額外的設定，即可啟用mTLS；當偵測到啟用mTLS的端點時，此程式會自動發生。 每個憑證的一般名稱(CN)和主體替代名稱(SAN)都可在檔案中作為憑證的一部分提供，如果您希望這樣做，還可以用作其他所有權驗證層。
>
>RFC 2818於2000年5月發行，它不建議在HTTPS憑證中使用一般名稱(CN)欄位來進行主體名稱驗證。 它建議改用「dns名稱」型別的「主體替代名稱」延伸模組(SAN)。

### 下載憑證 {#download-certificates}

>[!NOTE]
>
>您有責任確保您的系統使用有效的公開憑證。 定期檢閱您的憑證，尤其是在到期日臨近時。 使用API在憑證過期之前擷取和更新憑證。

不再提供公開mTLS憑證的直接下載連結。 請改用[公用憑證端點](../../data-governance/mtls-api/public-certificate-endpoint.md)來擷取憑證。 這是存取目前公開憑證唯一支援的方法。 這可確保您一律收到整合適用的有效最新憑證。

依賴憑證式加密的整合必須更新其工作流程，以支援使用API的自動化憑證擷取。 依賴靜態連結或手動更新可能會導致使用過期或撤銷的憑證，進而導致整合失敗。

#### 憑證生命週期自動化 {#certificate-lifecycle-automation}

Adobe現在自動化mTLS整合的憑證生命週期，以提高可靠性並防止服務中斷。 公開憑證為：

- 在到期前60天重新發行。
- 過期30天前撤銷。

這些間隔會根據[不斷發展的CA/B論壇指導方針](https://www.digicert.com/blog/tls-certificate-lifetimes-will-officially-reduce-to-47-days)而持續縮短，其目的是將憑證存留期減少到最多47天。

如果您先前使用此頁面上的連結來下載憑證，請更新您的程式，以專門透過API擷取憑證。

## 靜態資料 {#at-rest}

Experience Platform所擷取和使用的資料會儲存在Data Lake中，這是高精細度的資料存放區，包含系統管理的所有資料，無論來源或檔案格式為何。 資料湖中儲存的所有資料都會加密、儲存，並在貴組織獨有的獨立[[!DNL Microsoft Azure Data Lake] 儲存](https://docs.microsoft.com/en-us/azure/storage/blobs/data-lake-storage-introduction)執行個體中進行管理。

如需如何在Azure Data Lake Storage中加密閒置資料的詳細資訊，請參閱[Azure官方檔案](https://learn.microsoft.com/en-us/azure/storage/common/storage-service-encryption)。

## 後續步驟

本檔案提供Experience Platform中資料加密方式的高層級概觀。 如需Experience Platform中安全性程式的詳細資訊，請參閱Experience League的[治理、隱私權和安全性](./overview.md)概述，或檢視[Experience Platform安全性白皮書](https://www.adobe.com/content/dam/cc/en/security/pdfs/AEP_SecurityOverview.pdf)。
