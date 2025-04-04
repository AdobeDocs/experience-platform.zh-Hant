---
title: Adobe Experience Platform 發行說明 (2020 年 3 月版)
description: Adobe Experience Platform 2020 年 3 月版發行說明。
doc-type: release notes
last-update: March 10, 2020
author: ens71067
keywords: 發行說明；
exl-id: 407c2bac-4c8a-4939-b3dd-788250f15650
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '859'
ht-degree: 20%

---

# Adobe Experience Platform 發行說明

**發行日期： 2020年3月11日**

Adobe Experience Platform 現有功能的更新：

* [資料治理](#governance)
* [[!DNL Data Ingestion]](#ingestion)
* [[!DNL Destinations]](#destinations)
* [[!DNL Identity Service]](#identity)
* [[!DNL Sources]](#sources)

## 資料治理 {#governance}

[!DNL Experience Platform]可讓公司整合來自多個企業系統的資料，讓行銷人員更能識別、瞭解客戶並與之互動。 [!DNL Experience Platform]包含端對端資料治理基礎結構，以確保在[!DNL Experience Platform]內以及系統之間共用資料時能正確使用資料。

Adobe Experience Platform 資料治理是一系列的策略和技術，用於管理客戶資料並確保符合適用於資料使用方式的法規、限制和政策。它在 [!DNL Experience Platform] 的不同階層都扮演重要的角色，包括編目、資料譜系、資料使用標籤、資料存取政策，以及對行銷動作資料的存取控制。

**新功能**

>[!NOTE]
>
>下列部分新功能目前仍在測試階段，並未開放所有使用者使用。 Beta功能可能會有所變更。

| 功能 | 說明 |
| ------- | ----------- |
| 自動強制執行[!DNL Real-Time Customer Data Platform]的資料使用原則 | 在啟用資料至目的地的工作流程中，現在會強制執行資料使用原則。 在進行影響現有啟用的變更時（例如變更資料集標籤、合併原則、區段定義等），也會內嵌並強制執行資料控管。 |
| 強制執行的資料譜系 | 在Real-Time CDP中違反資料使用原則時，UI會顯示包含資料歷程資訊的通知，以協助使用者瞭解違反原則的原因以及他們可採取哪些措施來解決違規。 |


**已知問題**

* None

如需資料控管的詳細資訊，請參閱[資料控管概觀](../../data-governance/home.md)。

## 資料攝取 {#ingestion}

Adobe Experience Platform提供豐富的功能，可擷取任何型別和延遲的資料。 Adobe Experience Platform [!DNL Data Ingestion]提供多種擷取資料的替代方案，包括批次API、串流API、原生Adobe聯結器、資料整合合作夥伴或Adobe Experience Platform UI。

**新功能**

| 功能 | 說明 |
|------- | -----------|
| 部分批次擷取 | 部分批次擷取是擷取包含錯誤的資料的能力，上限為特定臨界值。 透過這項功能，使用者可以成功將其所有正確資料擷取到Adobe Experience Platform，同時將其所有不正確的資料分別分批處理。 會將詳細資料新增至失敗的批次，以說明未通過驗證的原因。 如需部分批次擷取的詳細資訊，請參閱[部分批次擷取檔案](../../ingestion/batch-ingestion/partial.md)。 |

**已知問題**

* None

若要進一步瞭解如何將資料擷取至Experience Platform，請瀏覽[資料擷取檔案](../../ingestion/home.md)。


## 目標 {#destinations}

在[Real-Time Customer Data Platform](../../rtcdp/overview.md)中，目的地是預先建立的與目的地平台的整合，可透過順暢的方式為這些合作夥伴啟用資料。

**新目的地**

有新的目的地可供您啟用Adobe Experience Platform資料。 如需詳細資訊，請參閱下文：

| 目標 | 說明 |
|--- | ---|
| 雲端儲存空間目的地 | Real-Time CDP現在可以將您的區段以資料檔案的形式傳送至您的[!DNL Amazon S3]或SFTP雲端儲存位置。 這可讓您透過CSV或定位字元分隔的檔案，將對象及其設定檔屬性傳送至您的內部系統。 |
| Advertising目的地 | 針對Real-Time CDP目前支援的三個不同[!DNL Google]平台： [!DNL Google Ads]、[!DNL Google Ad Manager]、[!DNL Google]顯示和視訊360，[!DNL Google]目的地卡現在會分割為三個目的地卡。 |

若要深入瞭解，請造訪[目的地概觀](../../destinations/home.md)

## [!DNL Identity Service] {#identity}

提供相關的數位體驗需要完全瞭解您的客戶。 當您的客戶資料分散於不同的系統時，這會使工作變得更困難，導致每個個別客戶似乎擁有多個「身分」。

Adobe Experience Platform [!DNL Identity Service]可跨裝置和系統橋接身分，讓您即時提供具影響力的個人數位體驗，協助您更清楚瞭解客戶及其行為。

**新功能**

| 功能 | 說明 |
| ------- | ----------- |
| 增強型私密圖表 | 專用圖表功能已增強，可將圖表產生延遲從每週批次程式減少為每日重新整理圖表，讓[!DNL Identity Service]名客戶能存取更新的身分圖表和連結。 |

**已知問題**

* None

如需[!DNL Identity Service]的詳細資訊，請參閱[身分識別服務總覽](../../identity-service/home.md)。

## 來源 {#sources}

Adobe Experience Platform可從外部來源擷取資料，同時允許您使用[!DNL Experience Platform]服務來建構、加標籤及增強該資料。 您可以從各種來源擷取資料，例如 Adob&#x200B;&#x200B;e 應用程式、雲端型儲存空間、協力廠商軟體和 CRM 系統。

[!DNL Experience Platform]提供RESTful API和互動式UI，讓您輕鬆設定各種資料提供者的來源連線。 這些來源連線可讓您進行驗證並連線到外部儲存系統和 CRM 服務、設定攝取執行的時間並管理資料攝取輸送量。

**新功能**

| 功能 | 說明 |
| ------- | ----------- |
| Adobe Audience Manager聯結器已棄用的訊號 | 將不再傳送Audience Manger的訊號層級資料。 請注意，仍會包含特徵和區段的區段會籍。 由於此變更，將不再產生傳入資料集。 |
| 已重新命名資料集 | Audience Manger聯結器產生的資料集會有更新的名稱和說明。 |
| 在Audience Manger中啟用[!DNL Profile]切換 | 可以啟用或停用[!DNL Profile]切換功能，以將資料集提升至[!DNL Real-Time Customer Profile]。 切換預設為啟用。 |
| 雲端儲存系統的UI支援 | UI中[!DNL Azure Data Lake Storage Gen2]的新來源聯結器。 |
| CRM系統的UI支援 | UI中[!DNL HubSpot]、[!DNL Salesforce Service Cloud]和[!DNL ServiceNow]的新來源聯結器。 |
| 資料庫系統的UI支援 | UI中[!DNL AWS Redshift]、[!DNL Google BigQuery]、[!DNL MariaDB]、[!DNL Microsoft SQL Server]和[!DNL MySQL]的新來源聯結器。 |

**已知問題**

* None

若要深入瞭解來源，請參閱[來源概觀](../../sources/home.md)。
