---
title: Adobe Experience Platform發行說明2021年4月
description: 2021年4月Adobe Experience Platform發行說明。
doc-type: release notes
last-update: April 21, 2021
author: ens72741
exl-id: cc78e48a-3578-4c55-ae86-1946d62bddb9
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '888'
ht-degree: 12%

---

# Adobe Experience Platform 發行說明

**發行日期：2021 年 4 月 21 日**

Adobe Experience Platform 現有功能更新：

- [[!DNL Data Prep]](#data-prep)
- [[!DNL Experience Data Model (XDM)]](#xdm)
- [[!DNL Intelligent Services]](#intelligent-services)
- [[!DNL Segmentation Service]](#segmentation)
- [[!DNL Sources]](#sources)

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] 可讓資料工程師將資料對應、轉換及驗證至Experience Data Model(XDM)。

**新功能**

| 功能 | 說明 |
| ------- | ----------- |
| 支援編輯現有資料流的映射 | 您現在可以更新現有資料流的映射集。 無法更新已為一次性獲取安排的資料流的映射集。 HTTP API、Adobe Analytics、Adobe Audience Manager和 [!DNL Marketo Engage]. 如需詳細資訊，請參閱 [更新UI中的源資料流](../../sources/tutorials/ui/update-dataflows.md). |
| 支援串流內嵌 | 現在，建立串流來源連線時，可以使用資料準備函式。 如需詳細資訊，請參閱 [在UI中建立串流來源連線](../../sources/tutorials/ui/create/streaming/http.md). |

如需詳細資訊，請參閱 [[!DNL Data Prep] 概述](../../data-prep/home.md).

## [!DNL Experience Data Model (XDM)] {#xdm}

Experience Data Model(XDM)是開放原始碼規格，旨在提升數位體驗的效能。 它為與Adobe Experience Platform上的服務通訊的任何應用程式提供共同的結構和定義。 遵循XDM標準，所有客戶體驗資料皆可整合至通用表示法，以更快速、更整合的方式提供深入分析。 您可以從客戶動作中獲得寶貴的深入分析、透過區段定義客戶受眾，以及將客戶屬性用於個人化目的。

| 功能 | 說明 |
| --- | --- |
| 依產業的綱要建議 | 在結構編輯器UI中選取類別和結構欄位群組時，您可以使用新篩選器，根據您的特定產業檢視建議的標準元件。 請參閱 [產業資料模型](https://www.adobe.com/go/xdm-industry-erds-en) 有關不同行業使用案例中這些元件彼此關聯的詳細資訊。 |

## [!DNL Intelligent Services] {#intelligent-services}

智慧服務讓行銷分析師和從業人員能夠在客戶體驗使用案例中運用人工智慧和機器學習的強大功能。 這可讓行銷分析人員利用業務層級設定，針對公司需求設定專屬預測，而無需資料科學的專業知識。

### Customer AI

Real-time Customer Data Platform提供的Customer AI可產生自訂傾向分數，例如大規模個別設定檔的流失和轉換。 不必將企業需求轉換為機器學習問題、挑選演算法、培訓或部署，就能達成上述目的。

| 功能 | 說明 |
| ------- | ----------- |
| 支援Adobe Analytics資料 | 更新功能，可透過Analytics來源連接器支援Adobe Analytics資料集，而無須對資料進行ETL，以符合消費者體驗事件(CEE)結構。 |
| 支援Adobe Audience Manager資料 | 更新功能，可透過Audience Manager來源連接器支援Adobe Audience Manager資料集，而無須對資料進行ETL，以符合消費者體驗事件(CEE)結構。 |
| 模型效能摘要 | Customer AI現在有 [「模型效能摘要」頁簽](../../intelligent-services/customer-ai/user-guide/discover-insights.md#performance-metrics) 在「服務例項分析」頁面中。 模型效能索引標籤會顯示所有實際的轉換率和流失率。 這可讓您解譯並了解每個傾向貯體中發生的情況。 |

如需支援資料集的詳細資訊，請參閱 [[!DNL Intelligent Services] 資料準備檔案](../../intelligent-services/data-preparation.md).

### Attribution AI

Attribution AI 可將點數歸因到促成轉換事件的接觸點。 行銷人員可善用此工具，協助量化客戶歷程中各個獨立行銷接觸點對行銷的影響。

| 功能 | 說明 |
| ------- | ----------- |
| 支援Adobe Analytics資料 | 更新功能，可透過Analytics來源連接器支援Adobe Analytics資料集，而無須對資料進行ETL，以符合消費者體驗事件(CEE)結構。 |

如需支援資料集的詳細資訊，請參閱 [[!DNL Intelligent Services] 資料準備檔案](../../intelligent-services/data-preparation.md).

## 分段服務 {#segmentation}

Adobe Experience Platform劃分服務提供使用者介面和RESTful API，可讓您建立區段，並從 [!DNL Real-Time Customer Profile] 資料。 這些區段會在Platform上集中設定和維護，讓任何Adobe應用程式都能輕鬆存取。

[!DNL Segmentation Service] 會透過說明區分客戶群中可行銷人員群組的條件，來定義特定設定檔子集。 區段可以根據記錄資料（例如人口統計資訊）或代表客戶與您品牌互動的時間序列事件。

**新功能**

| 功能 | 說明 |
| ------- | ----------- |
| 其他聚合函式 | 區段產生器中已新增計數函式。 計數函式可讓您計算指定事件完成的次數。 有關計數函式的詳細資訊，請參閱 [區段產生器指南](../../segmentation/ui/segment-builder.md#count-functions) |

如需 [!DNL Segmentation Service]，請參閱 [區段概觀](../../segmentation/home.md).

## [!DNL Sources] {#sources}

Adobe Experience Platform可內嵌來自外部來源的資料，同時允許您使用Platform服務來建構、加標籤及增強該資料。 您可以內嵌來自各種來源的資料，例如Adobe應用程式、雲端儲存、協力廠商軟體和您的CRM系統。

Experience Platform提供RESTful API和互動式UI，讓您輕鬆為各種資料提供者設定來源連線。 這些源連接允許您驗證並連接到外部儲存系統和CRM服務、設定獲取運行時間以及管理資料獲取吞吐量。

| 功能 | 說明 |
| ------- | ----------- |
| [!DNL Marketo Engage] （測試版） | 您現在可以建立 [!DNL Marketo Engage] 使用UI進行來源連線，將B2B資料帶入Platform，並使用與平台連線的應用程式讓此資料保持最新。 如需詳細資訊，請參閱 [[!DNL Marketo Engage] 來源連接器說明](../../sources/connectors/adobe-applications/marketo/marketo.md). |
| 測試版來源轉至GA | 下列來源已從測試版提升為正式發行： <ul><li>[[!DNL Amazon Kinesis]](../../sources/connectors/cloud-storage/kinesis.md)</li><li>[[!DNL Azure EventHubs]](../../sources/connectors/cloud-storage/eventhub.md)</li><li>[[!DNL HTTP API]](../../sources/connectors/streaming/http.md)</li><li>[[!DNL MariaDB]](../../sources/connectors/databases/mariadb.md)</li><li>[[!DNL Microsoft SQL Server]](../../sources/connectors/databases/sql-server.md)</li><li>[[!DNL Oracle]](../../sources/connectors/databases/oracle.md)</li></ul> |

若要進一步了解來源，請參閱 [來源概觀](../../sources/home.md).
