---
title: Adobe Experience Platform 發行說明
description: Experience Platform發行說明2020年3月11日
doc-type: release notes
last-update: March 10, 2020
author: ens71067
keywords: release notes;
translation-type: tm+mt
source-git-commit: f881c1365684b1ca9e6bf9a8ce866d234dc54128
workflow-type: tm+mt
source-wordcount: '848'
ht-degree: 5%

---


# Adobe Experience Platform 發行說明

**發行日期：2020 年 3 月 11 日**

Adobe Experience Platform現有功能的更新：

* [!DNL Data Governance](#governance)
* [!DNL Data Ingestion](#ingestion)
* [!DNL Destinations](#destinations)
* [!DNL Identity Service](#identity)
* [!DNL Sources](#sources)

## [!DNL Data Governance] {#governance}

[!DNL Experience Platform] 讓公司將多個企業系統的資料整合在一起，讓行銷人員更能識別、瞭解並吸引客戶。 [!DNL Experience Platform] 包括端對端資料治理基礎架構，包括資料使用標籤與實施(DULE)，以確保在系統內和系統間共用資料時，能 [!DNL Platform] 夠正確使用資料。

Adobe Experience Platform是一 [!DNL Data Governance] 系列用於管理客戶資料及確保符合資料使用相關法規、限制和政策的策略與技術。 它在各個層級中都扮演了關 [!DNL Experience Platform] 鍵角色，包括編目、資料傳承、資料使用標籤、資料存取政策，以及對行銷動作資料的存取控制。

**新功能**

>[!NOTE]
>
>下列部分新功能目前已在測試版中，並非所有使用者都能使用。 測試版功能可能會有所變更。

| 功能 | 說明 |
| ------- | ----------- |
| 自動執行 [!DNL Real-time Customer Data Platform] | 資料使用原則現在會在啟動資料至目的地的工作流程中執行。 [!DNL Data Governance] 也會在進行影響現有啟動的變更（例如變更資料集標籤、合併原則、區段定義等）時嵌入並強制執行。 |
| 用於實施的資料世系 | 當Real-time CDP中違反資料使用原則時，UI會顯示一則通知，其中包含資料世系資訊，以協助使用者瞭解違反原則的原因，以及他們可以採取哪些措施來解決違規問題。 |


**已知問題**

* 無

如需詳細資訊， [!DNL Data Governance]請參閱資 [料治理概觀](../../data-governance/home.md)。

## 資料擷取 {#ingestion}

Adobe Experience Platform提供一組豐富的功能，可吸收任何類型的資料和延遲。 Adobe Experience Platform提供 [!DNL Data Ingestion] 多種替代方式來擷取資料，包括批次API、串流API、原生Adobe連接器、資料整合合作夥伴或Adobe Experience Platform UI。

**新功能**

| 功能 | 說明 |
|------- | -----------|
| 部分批次擷取 | 部分批次擷取是指能夠擷取包含錯誤的資料，最高可達到特定臨界值。 透過這項功能，使用者可以成功將所有正確的資料內嵌至Adobe Experience Platform，同時將所有不正確的資料分別批次處理。 詳細資訊會新增至不成功的批次，以說明為何未通過驗證。 如需部分批次擷取的詳細資訊，請參閱部分批次擷取 [檔案](../../ingestion/batch-ingestion/partial.md)。 |

**已知問題**

* 無

若要進一步瞭解將資料擷取至平台，請造訪資 [料擷取檔案](../../ingestion/home.md)。


## 目的地 {#destinations}

在 [Adobe即時客戶資料平台中](../../rtcdp/overview.md)，目標是與目標平台預先建立的整合，以順暢的方式將資料啟動給這些合作夥伴。

**新目標**

您可以在新目的地啟用Adobe Experience Platform資料。 如需詳細資訊，請參閱以下：

| 目的地 | 說明 |
|--- | ---|
| 雲端儲存空間目標 | Adobe即時CDP現在可將區段作為資料檔案傳送至您的或SFTP雲 [!DNL Amazon S3] 端儲存位置。 這可讓您透過CSV或Tab分隔檔案，將觀眾及其描述檔屬性傳送至內部系統。 |
| 廣告目的地 | 目 [!DNL Google] 標卡現在分為三個目標卡，適用於Adobe即時CDP [!DNL Google] 目前支援的三種不同平台： [!DNL Google Ads]、 [!DNL Google Ad Manager]顯示 [!DNL Google] 與視訊360。 |

若要進一步瞭解，請造訪目 [標總覽](../../rtcdp/destinations/destinations-overview.md)

## [!DNL Identity Service] {#identity}

要提供相關的數位體驗，必須全面瞭解客戶。 當客戶資料分散在不同的系統上時，這會更加困難，導致每個客戶看起來都有多個「身分」。

Adobe Experience Platform可 [!DNL Identity Service] 協助您跨裝置和系統橋接身分，以便即時提供具影響力的個人化數位體驗，從而更全面地瞭解客戶及其行為。

**新功能**

| 功能 | 說明 |
| ------- | ----------- |
| 增強的私用圖表 | 專用圖表功能已增強，可減少從每週批次處理到每日重新整理的圖表產生延遲，讓客 [!DNL Identity Service] 戶存取更新的身分圖表和連結。 |

**已知問題**

* 無

如需詳細資訊 [!DNL Identity Service]，請參 [閱Identity Service總覽](../../identity-service/home.md)。

## 來源 {#sources}

Adobe Experience Platform可以從外部來源擷取資料，同時讓您使用服務來建構、標示和增強該資 [!DNL Platform] 料。 您可以從多種來源收集資料，例如Adobe應用程式、雲端儲存空間、協力廠商軟體和您的CRM系統。

[!DNL Experience Platform] 提供REST風格的API和互動式UI，讓您輕鬆地為各種資料提供者設定來源連線。 這些源連接允許您驗證並連接到外部儲存系統和CRM服務、設定接收運行的時間，以及管理資料接收吞吐量。

**新功能**

| 功能 | 說明 |
| ------- | ----------- |
| Adobe Audience Manager連接器不建議使用的信號 | Audience Manger的訊號層級資料將不再傳送。 請注意，「特徵」和「區段」的區段會籍仍將包含在內。 由於此更改，將不再生成入站資料集。 |
| 重新命名的資料集 | 由Audience Manger連接器產生的資料集會有更新的名稱和說明。 |
| 在Audience [!DNL Profile] Manger中啟用切換 | [!DNL Profile] 可以啟用或停用切換，將資料集提升為 [!DNL Real-time Customer Profile]。 預設會啟用切換。 |
| 雲端儲存系統的UI支援 | UI中的新 [!DNL Azure Data Lake Storage Gen2] 來源連接器。 |
| CRM系統的UI支援 | 在UI中為 [!DNL HubSpot]、 [!DNL Salesforce Service Cloud]和 [!DNL ServiceNow] 新增來源連接器。 |
| 資料庫系統的UI支援 | UI中的、、、 [!DNL AWS Redshift]、和 [!DNL Google BigQuery]新的來 [!DNL MariaDB][!DNL Microsoft SQL Server][!DNL MySQL] 源連接器。 |

**已知問題**

* 無

若要進一步瞭解來源，請參閱 [來源概觀](../../sources/home.md)。