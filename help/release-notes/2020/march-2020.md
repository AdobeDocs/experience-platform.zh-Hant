---
title: Adobe Experience Platform 發行說明
description: Experience Platform發行說明2020年3月11日
doc-type: release notes
last-update: March 10, 2020
author: ens71067
keywords: 發行說明;
translation-type: tm+mt
source-git-commit: 126b3d1cf6d47da73c6ab045825424cf6f99e5ac
workflow-type: tm+mt
source-wordcount: '841'
ht-degree: 6%

---


# Adobe Experience Platform 發行說明

**發行日期：2020 年 3 月 11 日**

Adobe Experience Platform 現有功能更新：

* [[!DNL Data Governance]](#governance)
* [[!DNL Data Ingestion]](#ingestion)
* [[!DNL Destinations]](#destinations)
* [[!DNL Identity Service]](#identity)
* [[!DNL Sources]](#sources)

## [!DNL Data Governance] {#governance}

[!DNL Experience Platform] 讓公司將多個企業系統的資料整合在一起，讓行銷人員更能識別、瞭解並吸引客戶。[!DNL Experience Platform] 包括端對端資料治理基礎架構，以確保在系統內和系統之間共用資料 [!DNL Platform] 時正確使用資料。

Adobe Experience Platform[!DNL Data Governance]是一系列策略和技術，用於管理客戶資料並確保遵守適用於資料使用的法規、限制和策略。 它在[!DNL Experience Platform]的不同層次中發揮關鍵作用，包括編目、資料承傳、資料使用標籤、資料存取政策，以及行銷動作的資料存取控制。

**新功能**

>[!NOTE]
>
>下列部分新功能目前已在測試版中，並非所有使用者都能使用。 測試版功能可能會有所變更。

| 功能 | 說明 |
| ------- | ----------- |
| 自動實施[!DNL Real-time Customer Data Platform]的資料使用策略 | 資料使用原則現在會在啟動資料至目的地的工作流程中執行。 [!DNL Data Governance] 也會在進行影響現有啟動的變更（例如變更資料集標籤、合併原則、區段定義等）時嵌入並強制執行。 |
| 用於實施的資料世系 | 當Real-time CDP中違反資料使用原則時，UI會顯示一則通知，其中包含資料世系資訊，以協助使用者瞭解違反原則的原因，以及他們可以採取哪些措施來解決違規問題。 |


**已知問題**

* None

如需[!DNL Data Governance]的詳細資訊，請參閱[資料治理概觀](../../data-governance/home.md)。

## 資料擷取 {#ingestion}

Adobe Experience Platform提供豐富的功能集，可吸收任何類型和延遲的資料。 Adobe Experience Platform[!DNL Data Ingestion]提供多種替代方式來擷取資料，包括批次API、串流API、原生Adobe連接器、資料整合合作夥伴或Adobe Experience PlatformUI。

**新功能**

| 功能 | 說明 |
|------- | -----------|
| 部分批次擷取 | 部分批次擷取是指能夠擷取包含錯誤的資料，最高可達到特定臨界值。 有了這項功能，使用者就可以成功將所有正確的資料收錄到Adobe Experience Platform，而且將所有不正確的資料分開批次處理。 詳細資訊會新增至不成功的批次，以說明為何未通過驗證。 有關部分批處理提取的詳細資訊，請參閱[部分批處理提取文檔](../../ingestion/batch-ingestion/partial.md)。 |

**已知問題**

* 無

若要進一步瞭解如何將資料擷取至平台，請造訪[資料擷取檔案](../../ingestion/home.md)。


## 目的地 {#destinations}

在[即時客戶資料平台](../../rtcdp/overview.md)中，目標是預先建立的與目標平台的整合，這些平台可順暢地向這些合作夥伴啟用資料。

**新目標**

您可以在新目的地啟用Adobe Experience Platform資料。 如需詳細資訊，請參閱以下：

| 目的地 | 說明 |
|--- | ---|
| 雲端儲存空間目標 | 即時CDP現在可將區段作為資料檔案傳送至您的[!DNL Amazon S3]或SFTP雲端儲存位置。 這可讓您透過CSV或Tab分隔檔案，將觀眾及其描述檔屬性傳送至內部系統。 |
| 廣告目的地 | [!DNL Google]目標卡現在分為三個目標卡，用於即時CDP當前支援的三種不同的[!DNL Google]平台：[!DNL Google Ads]、[!DNL Google Ad Manager]、[!DNL Google]顯示與視訊360。 |

若要進一步瞭解，請造訪[目標概觀](../../destinations/home.md)

## [!DNL Identity Service] {#identity}

要提供相關的數位體驗，必須全面瞭解客戶。 當客戶資料分散在不同的系統上時，這會更加困難，導致每個客戶看起來都有多個「身分」。

Adobe Experience Platform[!DNL Identity Service]可跨裝置和系統橋接身份，協助您更全面地瞭解客戶及其行為，讓您即時提供具影響力的個人化數位體驗。

**新功能**

| 功能 | 說明 |
| ------- | ----------- |
| 增強的私用圖表 | 專用圖表功能已增強，可減少從每週批次處理到每日重新整理的圖表產生延遲，讓[!DNL Identity Service]客戶存取更新的身分圖表和連結。 |

**已知問題**

* 無

如需[!DNL Identity Service]的詳細資訊，請參閱[身分服務概觀](../../identity-service/home.md)。

## 來源 {#sources}

Adobe Experience Platform可以從外部來源收集資料，同時允許您使用[!DNL Platform]服務來建構、標籤和增強該資料。 您可以從多種來源收集資料，例如Adobe應用程式、雲端儲存空間、協力廠商軟體和您的CRM系統。

[!DNL Experience Platform] 提供REST風格的API和互動式UI，讓您輕鬆地為各種資料提供者設定來源連線。這些源連接允許您驗證並連接到外部儲存系統和CRM服務、設定接收運行的時間，以及管理資料接收吞吐量。

**新功能**

| 功能 | 說明 |
| ------- | ----------- |
| 不建議使用的Adobe Audience Manager連接器信號 | Audience Manger的訊號層級資料將不再傳送。 請注意，「特徵」和「區段」的區段會籍仍將包含在內。 由於此更改，將不再生成入站資料集。 |
| 重新命名的資料集 | 由Audience Manger連接器產生的資料集會有更新的名稱和說明。 |
| 啟用[!DNL Profile]在Audience Manger中切換 | [!DNL Profile] 可以啟用或停用切換，將資料集提升為 [!DNL Real-time Customer Profile]。預設會啟用切換。 |
| 雲端儲存系統的UI支援 | UI中[!DNL Azure Data Lake Storage Gen2]的新源連接器。 |
| CRM系統的UI支援 | UI中[!DNL HubSpot]、[!DNL Salesforce Service Cloud]和[!DNL ServiceNow]的新來源連接器。 |
| 資料庫系統的UI支援 | UI中[!DNL AWS Redshift]、[!DNL Google BigQuery]、[!DNL MariaDB]、[!DNL Microsoft SQL Server]和[!DNL MySQL]的新來源連接器。 |

**已知問題**

* 無

若要進一步瞭解來源，請參閱[來源概觀](../../sources/home.md)。