---
title: Adobe Experience Platform發行說明2022年8月
description: 2022年8月發佈的Adobe Experience Platform說明。
source-git-commit: b8513fa214ea74eec6809796cc194466e05cbb21
workflow-type: tm+mt
source-wordcount: '497'
ht-degree: 9%

---

# Adobe Experience Platform 發行說明

**發行日期：2022 年 24 月 8 日**

Adobe Experience Platform 現有功能更新：

- [資料準備](#data-prep)
- [來源](#sources)

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] 允許資料工程師將資料映射到體驗資料模型(XDM)並驗證資料。

**已更新功能**

| 功能 | 說明 |
| --- | --- |
| 支援插入帶警告的記錄 | Data Prep現在將警告（非嚴重錯誤）本地化到欄位，並允許接收行的其餘部分。 現在，所有映射器轉換錯誤都會報告為警告，部分攝取的行被視為成功，並帶有警告。  對包含警告和診斷詳細資訊的記錄也支援監視。 當前，只有流資料才能部分接收帶有警告的記錄。 查看文檔 [正在接收帶警告的記錄](../../sources/tutorials/ui/monitor-streaming.md) 的子菜單。 |

{style=&quot;table-layout:auto&quot;}

瞭解有關 [!DNL Data Prep]，請參見 [[!DNL Data Prep] 概述](../../data-prep/home.md)。

## 來源 {#sources}

Adobe Experience Platform可以從外部源接收資料，同時允許您使用平台服務來構建、標籤和增強資料。 您可以從多種來源(如Adobe應用程式、基於雲的儲存、第三方軟體和您的CRM系統)接收資料。

Experience Platform提供REST風格的API和互動式UI，讓您能夠輕鬆地為各種資料提供程式設定源連接。 通過這些源連接，您可以驗證並連接到外部儲存系統和CRM服務，設定接收運行時間，並管理資料接收吞吐量。

**新功能**

| 功能 | 說明 |
| --- | --- |
| 自助源的一般可用性（批SDK） | 開發、test和整合基於REST API的資料源，以便使用易於配置的源規範將批資料Experience Platform。 使用Sources SDK，您可以： <ul><li>為Experience Platform目錄配置新源。</li><li>定義源的規範，包括與支援的驗證類型、計畫以及獲取資源資料的方式有關的資訊。</li><li>為新源建立面向用戶的文檔。</li></ul> 有關詳細資訊，請閱讀 [自助源（批處理SDK）](../../sources/sources-sdk/overview.md)。 |
| 2004年12月 [!DNL Google BigQuery] 源 | 使用 [!DNL Google BigQuery] 從您的 [!DNL Google BigQuery] 資料倉庫到Experience Platform。 有關詳細資訊，請閱讀 [[!DNL Google BigQuery] 源](../../sources/connectors/databases/bigquery.md)。 |
| [!DNL Teradata Vantage] 源(Beta) | 使用 [!DNL Teradata Vantage] 將資料從混合多雲環境中接收到Experience Platform。 有關詳細資訊，請閱讀 [[!DNL Teradata Vantage] 源](../../sources/connectors/databases/teradata-vantage.md)。 |
| 跨區域支助Adobe Analytics來源 | 您現在可以從任何區域擷取報告套裝 (美國、英國或新加坡)。報表套件必須映射到與正在其中建立源連接的Experience Platform沙盒實例相同的組織。 有關詳細資訊，請閱讀上的指南 [在UI中建立Adobe Analytics源連接](../../sources/tutorials/ui/create/adobe-applications/analytics.md)。 |
| API支援按需接收 | 使用按需接收為給定資料流建立專用流運行， [!DNL Flow Service] API。 建立的流運行必須設定為一次性接收。 有關詳細資訊，請閱讀上的指南 [使用API建立用於按需接收的流運行](../../sources/tutorials/api/on-demand-ingestion.md) 的子菜單。 |

{style=&quot;table-layout:auto&quot;&quot;

要瞭解有關源的詳細資訊，請參閱 [源概述](../../sources/home.md)。
