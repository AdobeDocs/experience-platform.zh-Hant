---
title: Adobe Experience Platform發行說明2021年4月
description: 2021年4月為Adobe Experience Platform發佈的說明。
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

[!DNL Data Prep] 允許資料工程師將資料映射到體驗資料模型(XDM)並驗證資料。

**新功能**

| 功能 | 說明 |
| ------- | ----------- |
| 支援編輯現有資料流的映射 | 現在可以更新現有資料流的映射集。 無法更新為一次性接收計畫的資料流的映射集。 HTTP API、Adobe Analytics、Adobe Audience Manager和 [!DNL Marketo Engage]。 有關詳細資訊，請參見上的教程 [更新UI中的源資料流](../../sources/tutorials/ui/update-dataflows.md)。 |
| 支援流式接收 | 現在，在建立流源連接時可以使用資料準備功能。 有關詳細資訊，請參見上的教程 [在UI中建立流源連接](../../sources/tutorials/ui/create/streaming/http.md)。 |

有關詳細資訊，請參閱 [[!DNL Data Prep] 概述](../../data-prep/home.md)。

## [!DNL Experience Data Model (XDM)] {#xdm}

體驗資料模型(XDM)是一種開源規範，旨在提高數字型驗的威力。 它為任何與Adobe Experience Platform服務通信的應用程式提供了共同的結構和定義。 通過遵守XDM標準，所有客戶體驗資料都可以納入到共同的表示形式中，以更快、更整合的方式提供見解。 您可以從客戶操作中獲得有價值的見解，通過細分市場定義客戶受眾，並將客戶屬性用於個性化目的。

| 功能 | 說明 |
| --- | --- |
| 按行業分列的方案建議 | 在架構編輯器UI中選擇類和架構欄位組時，可以使用新篩選器根據特定行業查看推薦的標準元件。 請參閱 [行業資料模型](https://www.adobe.com/go/xdm-industry-erds-en) 有關這些元件在不同行業使用案例中如何相互關聯的詳細資訊。 |

## [!DNL Intelligent Services] {#intelligent-services}

智慧服務使營銷分析師和從業人員能夠利用人工智慧和機器學習在客戶體驗使用案例中的威力。 這可讓行銷分析人員利用業務層級設定，針對公司需求設定專屬預測，而無需資料科學的專業知識。

### 客戶AI

在Real-time Customer Data Platform提供的客戶AI用於生成定制傾向得分，如按規模對個人配置檔案的流失和轉換。 不必將企業需求轉換為機器學習問題、挑選演算法、培訓或部署，就能達成上述目的。

| 功能 | 說明 |
| ------- | ----------- |
| 支援Adobe Analytics資料 | 更新了通過分析源連接器支援Adobe Analytics資料集的功能，而無需ETL資料以符合消費者體驗事件(CEE)架構。 |
| 支援Adobe Audience Manager資料 | 更新了通過Audience Manager源連接器支援Adobe Audience Manager資料集的功能，而無需ETL資料以符合消費者體驗事件(CEE)架構。 |
| 模型效能摘要 | 客戶AI現在有 [模型效能摘要頁籤](../../intelligent-services/customer-ai/user-guide/discover-insights.md#performance-metrics) 在「服務實例透視」頁中。 「模型效能」頁籤顯示所有實際轉換率和流失率。 這樣你就能破解和理解你的每個傾向桶里發生了什麼。 |

有關支援的資料集的詳細資訊，請參閱 [[!DNL Intelligent Services] 資料準備文檔](../../intelligent-services/data-preparation.md)。

### Attribution AI

Attribution AI 可將點數歸因到促成轉換事件的接觸點。 行銷人員可善用此工具，協助量化客戶歷程中各個獨立行銷接觸點對行銷的影響。

| 功能 | 說明 |
| ------- | ----------- |
| 支援Adobe Analytics資料 | 更新了通過分析源連接器支援Adobe Analytics資料集的功能，而無需ETL資料以符合消費者體驗事件(CEE)架構。 |

有關支援的資料集的詳細資訊，請參閱 [[!DNL Intelligent Services] 資料準備文檔](../../intelligent-services/data-preparation.md)。

## 分段服務 {#segmentation}

Adobe Experience Platform分段服務提供用戶介面和REST風格的API，使您能夠生成分段並從您的 [!DNL Real-Time Customer Profile] 資料。 這些段在平台上集中配置和維護，使任何Adobe應用程式都可輕鬆訪問。

[!DNL Segmentation Service] 通過描述區分客戶群中可銷售人員組的標準來定義特定配置檔案子集。 段可以基於記錄資料（如人口統計資訊）或表示客戶與您品牌的交互的時間序列事件。

**新功能**

| 功能 | 說明 |
| ------- | ----------- |
| 附加聚合函式 | 已在段生成器中添加計數函式。 計數函式用於計算指定事件已完成的次數。 有關計數函式的詳細資訊，請參閱 [段生成器指南](../../segmentation/ui/segment-builder.md#count-functions) |

有關 [!DNL Segmentation Service]，請參閱 [分段概述](../../segmentation/home.md)。

## [!DNL Sources] {#sources}

Adobe Experience Platform可以從外部源接收資料，同時允許您使用平台服務來構建、標籤和增強資料。 您可以從多種來源(如Adobe應用程式、基於雲的儲存、第三方軟體和您的CRM系統)接收資料。

Experience Platform提供REST風格的API和互動式UI，讓您能夠輕鬆地為各種資料提供程式設定源連接。 通過這些源連接，您可以驗證並連接到外部儲存系統和CRM服務，設定接收運行時間，並管理資料接收吞吐量。

| 功能 | 說明 |
| ------- | ----------- |
| [!DNL Marketo Engage] (Beta) | 現在可以建立 [!DNL Marketo Engage] 源連接使用UI將B2B資料帶到平台，並使用與平台連接的應用程式保持此資料的最新。 有關詳細資訊，請參見 [[!DNL Marketo Engage] 源連接器文檔](../../sources/connectors/adobe-applications/marketo/marketo.md)。 |
| Beta源移至GA | 已將以下源從beta升級為GA: <ul><li>[[!DNL Amazon Kinesis]](../../sources/connectors/cloud-storage/kinesis.md)</li><li>[[!DNL Azure EventHubs]](../../sources/connectors/cloud-storage/eventhub.md)</li><li>[[!DNL HTTP API]](../../sources/connectors/streaming/http.md)</li><li>[[!DNL MariaDB]](../../sources/connectors/databases/mariadb.md)</li><li>[[!DNL Microsoft SQL Server]](../../sources/connectors/databases/sql-server.md)</li><li>[[!DNL Oracle]](../../sources/connectors/databases/oracle.md)</li></ul> |

要瞭解有關源的詳細資訊，請參閱 [源概述](../../sources/home.md)。
