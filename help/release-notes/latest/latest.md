---
title: Adobe Experience Platform 發行說明
description: 2021年7月28日的Experience Platform發行說明。
doc-type: release notes
last-update: July 28, 2021
author: ens60013
exl-id: 8f2c9bf8-1487-46e4-993b-bd9b63774cab
source-git-commit: 3aac1e7c7fe838201368379da8504efc8e316e1c
workflow-type: tm+mt
source-wordcount: '802'
ht-degree: 7%

---


# Adobe Experience Platform 發行說明

**發行日期：2021 年 7 月 28 日**

Adobe Experience Platform 現有功能更新：

- [Data Science Workspace](#dsw)
- [資料流](#destinations)
- [目的地](#destinations)
- [Experience Data Model(XDM)](#xdm)
- [查詢服務](#query)
- [來源](#sources)

## Data Science Workspace {#dsw}

Data Science Workspace使用機器學習和人工智慧，從您的資料建立深入分析。 整合至Adobe Experience Platform的Data Science Workspace可協助您跨Adobe解決方案，使用內容和資料資產進行預測。

**新功能**

| 功能 | 說明 |
| --- | --- |
| 程式庫和作業系統更新 | Data Science Workspace已對程式庫和作業系統進行重大更新，以改善功能和可用性。 這包括JupyterLab 1.2.20、Python 3.7、Pancits 1.2.4、Tensorflow 2.4.1（支援CUDA 11和CUDNN 8）等。 若要了解如何在JupyterLab中檢視可用的程式庫，請造訪JupyterLab筆記型電腦概述檔案中的[支援的程式庫](../../data-science-workspace/jupyterlab/overview.md#supported-libraries)區段。 |

如需Data Science Workspace的更多一般資訊，請參閱[Data Science Workspace概述](../../data-science-workspace/home.md)。

## 資料流 {#dataflows}

在Platform中，會從許多不同來源擷取資料、在系統內進行分析，並啟動至各種目的地。 Platform借由提供資料流的透明度，讓追蹤此潛在非線性資料流的程式更輕鬆。

資料流是跨平台移動資料的作業的表示。 這些資料流是在不同服務間配置的，有助於將資料從源連接器移動到目標資料集，然後由Identity Service和即時客戶配置檔案使用，最終激活到目標。

**新功能**

| 功能 | 說明 |
| ------- | ----------- |
| 目的地控制面板 | 您現在可以使用監控控制面板來監控目的地的資料流。 若要進一步了解，請閱讀UI](../../dataflows/ui/monitor-destinations.md#monitoring-destinations-dashboard)中[監控目的地的教學課程 |

有關資料流的更一般資訊，請參閱[資料流概述](../../dataflows/home.md)。 若要深入了解目的地，請參閱[目的地概述](../../destinations/home.md)。

## 目的地 {#destinations}

目的地是預先建置與目的地平台的整合，可順暢地從Adobe Experience Platform啟動資料。 您可以使用目的地來針對跨通路行銷活動、電子郵件行銷活動、目標廣告和其他許多使用案例，啟用已知和未知的資料。

**新功能**

| 功能 | 說明 |
| --- | --- |
| [更快的增量檔案導出](../../destinations/ui/activate-batch-profile-destinations.md#export-incremental-files) | 您現在可以每3、6、8和12小時為基於檔案的目的地安排增量檔案導出時間。 目前不支援針對已儲存的區段變更檔案匯出排程。 若要使用不同排程重新匯出區段，您必須建立新的目的地例項。 這是將在未來版本中解決的限制。 |
| [支援重複資料刪除金鑰](../../destinations/ui/activate-batch-profile-destinations.md#deduplication-keys) | 選取重複資料刪除金鑰，即可在匯出檔案中消除相同設定檔的多個記錄。 您可以選取單一命名空間或最多兩個XDM架構屬性作為重複資料刪除索引鍵。 |

## Experience Data Model(XDM) {#xdm}

Experience Data Model(XDM)是開放原始碼規格，旨在提升數位體驗的效能。 它以結構形式提供資料的通用結構和定義，可讓任何應用程式與Platform服務通訊。

| 功能 | 說明 |
| --- | --- |
| 電信工業過濾器 | 現在，在UI中將欄位群組新增至結構時，您可以依電信產業進行篩選。 請參閱[電信行業實體關係圖(ERD)](../../xdm/schema/industries/telecom.md) ，查看電信使用案例的建議資料模型。 |

如需Platform中XDM的更多一般資訊，請參閱[XDM系統概述](../../xdm/home.md)。

## 查詢服務 {#query}

Query Service提供使用標準SQL在Adobe Experience Platform中查詢資料的功能，支援各種分析和資料管理使用案例。 這是一種無伺服器工具，可讓您從Data Lake加入資料集，並將查詢結果擷取為新資料集，以用於報表、Data Science Workspace或擷取至即時客戶個人檔案。

您可以使用Query Service建立資料分析生態系統，了解客戶在不同互動管道中的狀況。 這些管道可能包括銷售點、網頁、行動裝置或CRM系統。

**新功能**

| 功能 | 說明 |
| ------- | ----------- |
| 排程查詢 | 您現在可以使用查詢編輯器在Platform中排程查詢。 若要進一步了解，請閱讀[查詢編輯器](../../query-service/ui/user-guide.md#scheduled-queries)上的檔案。 |

如需詳細資訊，請參閱[查詢服務檔案](../../query-service/home.md)。

## 來源 {#sources}

Adobe Experience Platform可內嵌來自外部來源的資料，同時允許您使用Platform服務來建構、加標籤及增強該資料。 您可以內嵌來自各種來源的資料，例如Adobe應用程式、雲端儲存、協力廠商軟體和您的CRM系統。

Experience Platform提供RESTful API和互動式UI，讓您輕鬆為各種資料提供者設定來源連線。 這些源連接允許您驗證並連接到外部儲存系統和CRM服務、設定獲取運行時間以及管理資料獲取吞吐量。

| 功能 | 說明 |
| ------- | ----------- |
| 測試版來源轉至GA | 下列來源已從測試版提升為正式發行： <ul><li>[[!DNL Amazon Redshift]](../../sources/connectors/databases/redshift.md)</li><li>[[!DNL Azure Table Storage]](../../sources/connectors/databases/ats.md)</li><li>[[!DNL PayPal]](../../sources/connectors/payments/paypal.md)</li></ul> |
| [!DNL Salesforce Marketing Cloud] （測試版） | 您現在可以使用[!DNL Flow Service] API或UI將[!DNL Salesforce Marketing Cloud]連線至Experience Platform。 如需詳細資訊，請參閱[[!DNL Salesforce Marketing Cloud] 連接器概述](../../sources/connectors/marketing-automation/salesforce-marketing-cloud.md) 。 |

若要進一步了解來源，請參閱[來源概述](../../sources/home.md)。
