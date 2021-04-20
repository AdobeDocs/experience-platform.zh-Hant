---
title: Adobe Experience Platform 發行說明
description: 2021年4月21日的Experience Platform發行說明。
doc-type: release notes
last-update: April 21, 2021
author: ens72741
translation-type: tm+mt
source-git-commit: 73ecf6e6f9796088e2d14f9dc3d9667104b22a8e
workflow-type: tm+mt
source-wordcount: '586'
ht-degree: 14%

---


# Adobe Experience Platform 發行說明

**發行日期：2021 年 4 月 21 日**

Adobe Experience Platform 現有功能更新：

- [[!DNL Data Prep]](#data-prep)
- [[!DNL Intelligent Services]](#intelligent-services)
- [[!DNL Sources]](#sources)

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] 可讓資料工程師將資料對應、轉換及驗證資料與Experience Data Model(XDM)。

**新功能**

| 功能 | 說明 |
| ------- | ----------- |
| 支援編輯現有資料流的對應 | 您現在可以更新現有資料流的映射集。 不能更新為一次性提取調度的資料流的映射集。 HTTP API、Adobe Analytics、Adobe Audience Manager和[!DNL Marketo Engage]不支援此功能。 如需詳細資訊，請參閱UI](../../sources/tutorials/ui/update-dataflows.md)中有關[更新來源資料流的教學課程。 |
| 支援串流擷取 | 現在，您可以在建立串流來源連線時使用資料準備功能。 如需詳細資訊，請參閱UI](../../sources/tutorials/ui/create/streaming/http.md)中有關建立串流來源連線的教學課程。[ |

如需詳細資訊，請參閱[[!DNL Data Prep] overview](../../data-prep/home.md)。

## [!DNL Intelligent Services] {#intelligent-services}

智慧型服務可讓行銷分析師和從業人員在客戶體驗使用案例中運用人工智慧和機器學習的強大功能。 這可讓行銷分析師使用商業層級的組態來設定特定公司需求的預測，而不需要資料科學的專業知識。

### 客戶人工智慧

即時客戶資料平台中提供的客戶人工智慧可用來產生自訂傾向分數，例如大規模的個人個人檔案的流失和轉換。 不必將企業需求轉換為機器學習問題、挑選演算法、培訓或部署，就能達成上述目的。

| 功能 | 說明 |
| ------- | ----------- |
| 支援Adobe Analytics資料 | 更新功能，可透過Analytics來源連接器支援Adobe Analytics資料集，而不需要ETL您的資料，以符合消費者體驗事件(CEE)架構。 |
| 支援Adobe Audience Manager資料 | 更新功能，透過Audience Manager來源連接器支援Adobe Audience Manager資料集，毋需ETL您的資料，以符合消費者體驗事件(CEE)架構。 |
| 模型效能摘要 | 客戶人工智慧現在在服務例項深入分析頁面中有[模型效能摘要標籤](../../intelligent-services/customer-ai/user-guide/discover-insights.md#performance-metrics)。 模型績效標籤會顯示所有實際的轉換率和流失率。 這可讓您解讀並瞭解每個傾向區間的情況。 |

有關受支援資料集的詳細資訊，請參閱[[!DNL Intelligent Services] 資料準備文檔](../../intelligent-services/data-preparation.md)。

### Attribution AI

Attribution AI 可將點數歸因到促成轉換事件的接觸點。行銷人員可善用此工具，協助量化客戶歷程中各個獨立行銷接觸點對行銷的影響。

| 功能 | 說明 |
| ------- | ----------- |
| 支援Adobe Analytics資料 | 更新功能，可透過Analytics來源連接器支援Adobe Analytics資料集，而不需要ETL您的資料，以符合消費者體驗事件(CEE)架構。 |

有關受支援資料集的詳細資訊，請參閱[[!DNL Intelligent Services] 資料準備文檔](../../intelligent-services/data-preparation.md)。

## [!DNL Sources] {#sources}

Adobe Experience Platform可以從外部來源收集資料，同時允許您使用平台服務來建構、標籤和增強該資料。 您可以從多種來源收集資料，例如Adobe應用程式、雲端儲存空間、協力廠商軟體和您的CRM系統。

Experience Platform提供REST風格的API和互動式UI，讓您輕鬆地為各種資料提供者設定來源連線。 這些源連接允許您驗證並連接到外部儲存系統和CRM服務、設定接收運行的時間，以及管理資料接收吞吐量。

| 功能 | 說明 |
| ------- | ----------- |
| [!DNL Marketo Engage] （測試版） | 您現在可以使用UI建立[!DNL Marketo Engage]來源連線，將B2B資料帶入平台，並使用與平台連接的應用程式，讓此資料保持最新狀態。 有關詳細資訊，請參見[[!DNL Marketo Engage] 源連接器文檔](../../sources/connectors/adobe-applications/marketo/marketo.md)。 |

若要進一步瞭解來源，請參閱[來源概觀](../../sources/home.md)。
