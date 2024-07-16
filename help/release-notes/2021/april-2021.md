---
title: Adobe Experience Platform 發行說明 (2021 年 4 月)
description: Adobe Experience Platform 2021 年 4 月版發行說明。
doc-type: release notes
last-update: April 21, 2021
author: ens72741
exl-id: cc78e48a-3578-4c55-ae86-1946d62bddb9
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '886'
ht-degree: 33%

---

# Adobe Experience Platform 發行說明

**發行日期： 2021年4月21日**

Adobe Experience Platform 現有功能的更新：

- [[!DNL Data Prep]](#data-prep)
- [[!DNL Experience Data Model (XDM)]](#xdm)
- [[!DNL Intelligent Services]](#intelligent-services)
- [[!DNL Segmentation Service]](#segmentation)
- [[!DNL Sources]](#sources)

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep]可讓資料工程師對應、轉換及驗證與Experience Data Model (XDM)之間的資料。

**新功能**

| 功能 | 說明 |
| ------- | ----------- |
| 支援編輯現有資料流的對應 | 您現在可以更新現有資料流的對應集。 您無法更新排程為一次性內嵌之資料流程的對應集。 HTTP API、Adobe Analytics、Adobe Audience Manager和[!DNL Marketo Engage]不支援此功能。 如需詳細資訊，請參閱有關[在UI](../../sources/tutorials/ui/update-dataflows.md)中更新來源資料流程的教學課程。 |
| 支援串流擷取 | 您現在可以在建立串流來源連線時使用資料準備功能。 如需詳細資訊，請參閱有關[在UI](../../sources/tutorials/ui/create/streaming/http.md)中建立串流來源連線的教學課程。 |

如需詳細資訊，請參閱[[!DNL Data Prep] 總覽](../../data-prep/home.md)。

## [!DNL Experience Data Model (XDM)] {#xdm}

Experience Data Model (XDM)是開放原始碼規格，旨在改善數位體驗的力量。 它為任何應用程式提供通用結構和定義，以便與Adobe Experience Platform上的服務通訊。 若遵守 XDM 標準，即可將所有客戶體驗資料合併到一個常用表述中，以更快速、更整合的方式傳遞分析。您可以從客戶行為中獲得有價值的分析，透過區段定義客戶對象，並使用客戶屬性實現個人化的目的。

| 功能 | 說明 |
| --- | --- |
| 依產業區分的結構描述建議 | 在結構描述編輯器UI中選取類別和結構描述欄位群組時，您可以使用新的篩選器來根據您的特定產業檢視建議的標準元件。 請參閱[產業資料模型](https://www.adobe.com/go/xdm-industry-erds-en)的相關檔案，以取得有關這些元件在不同產業使用案例中如何相互關聯的詳細資訊。 |

## [!DNL Intelligent Services] {#intelligent-services}

智慧型服務可讓行銷分析師及從業人員運用客戶體驗使用案例中人工智慧和機器學習的強大功能。 這可讓行銷分析人員利用業務層級設定，針對公司需求設定專屬預測，而無需資料科學的專業知識。

### Customer AI

Real-time Customer Data Platform中可用的Customer AI可產生自訂傾向評分，例如大規模個別設定檔的流失和轉換情形。 不必將企業需求轉換為機器學習問題、挑選演算法、訓練或部署，即可達成上述目的。

| 功能 | 說明 |
| ------- | ----------- |
| 支援Adobe Analytics資料 | 更新功能，透過Analytics來源聯結器支援Adobe Analytics資料集，無需ETL您的資料符合消費者體驗事件(CEE)結構描述。 |
| 支援Adobe Audience Manager資料 | 更新功能，透過Audience Manager來源聯結器支援Adobe Audience Manager資料集，無需ETL您的資料符合消費者體驗事件(CEE)結構描述。 |
| 模型效能摘要 | Customer AI現在在服務執行個體深入分析頁面中有[模型效能摘要標籤](../../intelligent-services/customer-ai/user-guide/discover-insights.md#performance-metrics)。 模型績效標籤會顯示所有實際轉換率和流失率。 這可讓您解密並瞭解每個傾向性貯體中發生的情況。 |

如需支援資料集的詳細資訊，請參閱[[!DNL Intelligent Services] 資料準備檔案](../../intelligent-services/data-preparation.md)。

### Attribution AI

Attribution AI 可將點數歸因到促成轉換事件的接觸點。行銷人員可善用此工具，協助量化客戶歷程中各個獨立行銷接觸點對行銷的影響。

| 功能 | 說明 |
| ------- | ----------- |
| 支援Adobe Analytics資料 | 更新功能，透過Analytics來源聯結器支援Adobe Analytics資料集，無需ETL您的資料符合消費者體驗事件(CEE)結構描述。 |

如需支援資料集的詳細資訊，請參閱[[!DNL Intelligent Services] 資料準備檔案](../../intelligent-services/data-preparation.md)。

## Segmentation Service {#segmentation}

Adobe Experience Platform Segmentation Service提供使用者介面和RESTful API，可讓您建立區段，並從[!DNL Real-Time Customer Profile]資料產生對象。 這些區段是在Platform上集中設定和維護的，因此任何Adobe應用程式都可輕鬆存取。

[!DNL Segmentation Service] 會說明區分客戶群中可行銷的一群人的標準，從而定義設定檔的特定子集。區段的基礎可能是記錄資料 (例如人口統計資訊) 或表示客戶與您的品牌互動的時間序列事件。

**新功能**

| 功能 | 說明 |
| ------- | ----------- |
| 其他彙總函式 | 已在區段產生器中新增計數函式。 計數函式可讓您計算指定事件的完成次數。 如需計數函式的詳細資訊，請參閱[區段產生器指南](../../segmentation/ui/segment-builder.md#count-functions)的計數函式區段 |

如需有關 [!DNL Segmentation Service] 的詳細資訊，請參閱[分段概觀](../../segmentation/home.md)。

## [!DNL Sources] {#sources}

Adobe Experience Platform可內嵌來自外部來源的資料，同時允許您使用Platform服務來建構、加標籤及增強這些資料。 您可以從各種來源擷取資料，例如 Adob&#x200B;&#x200B;e 應用程式、雲端型儲存空間、協力廠商軟體和 CRM 系統。

Experience Platform 可提供 RESTful API 和互動式 UI，可讓您輕鬆為各種資料提供者設定來源連線。這些來源連線可讓您進行驗證並連線到外部儲存系統和 CRM 服務、設定擷取執行的時間並管理資料擷取輸送量。

| 功能 | 說明 |
| ------- | ----------- |
| [!DNL Marketo Engage] (Beta) | 您現在可以使用UI建立[!DNL Marketo Engage]來源連線，以將B2B資料帶入Platform，並使用平台連線的應用程式保持此資料在最新狀態。 如需詳細資訊，請參閱[[!DNL Marketo Engage] 來源聯結器檔案](../../sources/connectors/adobe-applications/marketo/marketo.md)。 |
| Beta來源移至GA | 下列來源已從Beta版升級至GA版： <ul><li>[[!DNL Amazon Kinesis]](../../sources/connectors/cloud-storage/kinesis.md)</li><li>[[!DNL Azure EventHubs]](../../sources/connectors/cloud-storage/eventhub.md)</li><li>[[!DNL HTTP API]](../../sources/connectors/streaming/http.md)</li><li>[[!DNL MariaDB]](../../sources/connectors/databases/mariadb.md)</li><li>[[!DNL Microsoft SQL Server]](../../sources/connectors/databases/sql-server.md)</li><li>[[!DNL Oracle]](../../sources/connectors/databases/oracle.md)</li></ul> |

若要深入瞭解來源，請參閱[來源概觀](../../sources/home.md)。
