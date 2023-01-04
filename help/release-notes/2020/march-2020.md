---
title: Adobe Experience Platform發行說明2020年3月
description: 2020年3月Adobe Experience Platform發行說明。
doc-type: release notes
last-update: March 10, 2020
author: ens71067
keywords: 發行說明;
exl-id: 407c2bac-4c8a-4939-b3dd-788250f15650
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '855'
ht-degree: 6%

---

# Adobe Experience Platform 發行說明

**發行日期：2020 年 3 月 11 日**

Adobe Experience Platform 現有功能更新：

* [資料治理](#governance)
* [[!DNL Data Ingestion]](#ingestion)
* [[!DNL Destinations]](#destinations)
* [[!DNL Identity Service]](#identity)
* [[!DNL Sources]](#sources)

## 資料治理 {#governance}

[!DNL Experience Platform] 可讓公司將來自多個企業系統的資料匯整在一起，讓行銷人員更能識別、了解客戶，並與其互動。 [!DNL Experience Platform] 包括端到端的資料治理基礎架構，以確保在中正確使用資料 [!DNL Platform] 和在系統之間共用時。

Adobe Experience Platform資料控管是一系列策略和技術，用於管理客戶資料及確保符合適用於資料使用的法規、限制和政策。 在 [!DNL Experience Platform] 在各個層級，包括編目、資料處理、資料使用標籤、資料存取策略，以及針對行銷動作的資料存取控制。

**新功能**

>[!NOTE]
>
>下列部分新功能目前仍在測試中，並非所有使用者都能使用。 測試版功能可能會有所變更。

| 功能 | 說明 |
| ------- | ----------- |
| 自動執行 [!DNL Real-Time Customer Data Platform] | 現在，在將資料啟用至目的地的工作流程中，會強制執行資料使用原則。 進行會影響現有啟用的變更時（例如資料集標籤的變更、合併原則、區段定義等），也會嵌入並強制執行資料控管。 |
| 用於執行的資料處理 | 在Real-Time CDP中違反資料使用原則時，UI會顯示包含資料處理資訊的通知，以協助使用者了解違反原則的原因，以及他們可以採取哪些措施來解決違反問題。 |


**已知問題**

* None

如需資料控管的詳細資訊，請參閱 [資料控管概觀](../../data-governance/home.md).

## 資料擷取 {#ingestion}

Adobe Experience Platform提供一組豐富的功能，可擷取任何類型和資料延遲。 Adobe Experience Platform [!DNL Data Ingestion] 提供多種資料擷取替代選項，包括批次API、串流API、原生Adobe連接器、資料整合合作夥伴或Adobe Experience Platform UI。

**新功能**

| 功能 | 說明 |
|------- | -----------|
| 部分批次內嵌 | 部分批次內嵌是指內嵌包含錯誤的資料的功能，最多可達特定臨界值。 透過此功能，使用者可成功將其所有正確資料內嵌至Adobe Experience Platform，同時將其所有不正確的資料分別批次處理。 詳細資訊會新增至失敗的批次，以說明為何未通過驗證。 如需部分批次內嵌的詳細資訊，請參閱 [部分批次內嵌檔案](../../ingestion/batch-ingestion/partial.md). |

**已知問題**

* None

若要進一步了解將資料擷取至Platform，請造訪 [資料擷取檔案](../../ingestion/home.md).


## 目的地 {#destinations}

在 [Real-time Customer Data Platform](../../rtcdp/overview.md)，目的地是與目的地平台預先建立的整合，可順暢地向這些合作夥伴啟用資料。

**新目的地**

您可以在新目的地啟用Adobe Experience Platform資料。 如需詳細資訊，請參閱下方：

| 目的地 | 說明 |
|--- | ---|
| 雲端儲存目的地 | Real-Time CDP現在可以將區段以資料檔案的形式傳送至 [!DNL Amazon S3] 或SFTP雲端儲存空間位置。 這可讓您透過CSV或以Tab分隔的檔案，將對象及其設定檔屬性傳送至內部系統。 |
| 廣告目的地 | 此 [!DNL Google] 目的地卡現在分為三個目的地卡，適用於三個不同的目的地卡 [!DNL Google] Real-Time CDP目前支援的平台： [!DNL Google Ads], [!DNL Google Ad Manager], [!DNL Google] 顯示與影片360。 |

若要進一步了解，請造訪 [目的地概述](../../destinations/home.md)

## [!DNL Identity Service] {#identity}

要提供相關的數位體驗，必須全面了解客戶。 當您的客戶資料分散於不同的系統，導致每個個別客戶看起來都有多個「身分」時，就會更加困難。

Adobe Experience Platform [!DNL Identity Service] 可協助您跨裝置和系統橋接身分，以便即時提供具影響力的個人數位體驗，進而更全面了解客戶及其行為。

**新功能**

| 功能 | 說明 |
| ------- | ----------- |
| 增強的專用圖表 | 「專用圖表」功能已增強，可減少圖表產生延遲，從每週批次處理縮短為每日重新整理，以允許 [!DNL Identity Service] 客戶，以存取更新的身分圖表和連結。 |

**已知問題**

* None

如需 [!DNL Identity Service]，請參閱 [Identity服務概述](../../identity-service/home.md).

## 來源 {#sources}

Adobe Experience Platform可以內嵌來自外部來源的資料，同時允許您使用 [!DNL Platform] 服務。 您可以內嵌來自各種來源的資料，例如Adobe應用程式、雲端儲存、協力廠商軟體和您的CRM系統。

[!DNL Experience Platform] 提供RESTful API和互動式UI，讓您輕鬆為各種資料提供者設定來源連線。 這些源連接允許您驗證並連接到外部儲存系統和CRM服務、設定獲取運行時間以及管理資料獲取吞吐量。

**新功能**

| 功能 | 說明 |
| ------- | ----------- |
| 已棄用的Adobe Audience Manager連接器訊號 | 來自Audience Manger的訊號層級資料將不再傳送。 請注意，特徵和區段的區段成員資格仍會包含在內。 此變更後，將不再產生傳入資料集。 |
| 重新命名的資料集 | Audience Manger連接器產生的資料集會有更新的名稱和說明。 |
| 啟用 [!DNL Profile] 在Audience Manger中切換 | [!DNL Profile] 可以啟用或停用切換，將資料集提升至 [!DNL Real-Time Customer Profile]. 切換預設為啟用。 |
| 雲端儲存系統的UI支援 | 新源連接器 [!DNL Azure Data Lake Storage Gen2] 在UI中。 |
| CRM系統的UI支援 | 新源連接器 [!DNL HubSpot], [!DNL Salesforce Service Cloud]，和 [!DNL ServiceNow] 在UI中。 |
| 資料庫系統的UI支援 | 新源連接器 [!DNL AWS Redshift], [!DNL Google BigQuery], [!DNL MariaDB], [!DNL Microsoft SQL Server]，和 [!DNL MySQL] 在UI中。 |

**已知問題**

* None

若要進一步了解來源，請參閱 [來源概觀](../../sources/home.md).
