---
title: Adobe Experience Platform發行說明2020年12月
description: 2020年12月Adobe Experience Platform發行說明。
doc-type: release notes
last-update: December 9, 2020
author: ens60013 & ens72471
exl-id: 89d631f1-1b11-4a18-98e1-08e1d5bd8b0d
source-git-commit: ce967ae176fce81aa26d92b3f0ee8be006808657
workflow-type: tm+mt
source-wordcount: '430'
ht-degree: 8%

---

# Adobe Experience Platform 發行說明

**發行日期：2020年12月9日**

Adobe Experience Platform的新功能：

- [[!DNL Dataflows]](#dataflows)

Adobe Experience Platform 現有功能更新：

- [[!DNL Data Science Workspace]](#dsw)
- [[!DNL Sources]](#sources)

## [!DNL Dataflows] {#dataflows}

資料流能呈現資料處理作業在平台上移動資料的情形。這些資料流是在不同服務之間配置的，有助於將資料從源連接器移動到目標資料集、到身份和配置檔案服務以及到目標。

**主要功能**

| 功能 | 說明 |
| ------- | ----------- |
| 資料流的透明度 | 您可以監視源和目標的資料流。 欲知更多資訊，請閱讀 [監控來源的教學課程](../../dataflows/ui/monitor-sources.md) 或 [監控目的地的教學課程](../../dataflows/ui/monitor-destinations.md). |

要了解有關資料流的詳細資訊，請閱讀 [資料流概述](../../dataflows/home.md).

## [!DNL Data Science Workspace] {#dsw}

Data Science Workspace使用機器學習和人工智慧，從您的資料建立深入分析。 整合至Adobe Experience Platform的Data Science Workspace可協助您跨Adobe解決方案，使用內容和資料資產進行預測。

**主要功能**

| 功能 | 說明 |
| --- | ---|
| Adobe Experience Platform Intelligence套件新增功能 | Adobe Experience Platform Intelligence套件addon是Data Science Workspace升級，可解鎖其他重要功能，例如： <li> UI驅動的模型實驗和評估。</li><li> 能夠部署和操作模型，並安排培訓和參考工作。</li><li> 支援網頁流量模型（GPU計算）的深度學習。</li><li> 基於Spark的分佈式計算，可針對大型資料集（10MM +列）進行訓練和評分。</li><li>還有更多</li> |

若要進一步了解Adobe Experience Platform Intelligence套件addon，請參閱 [Data Science Workspace存取與功能](../../data-science-workspace/access-features-dsw.md).

## [!DNL Sources] {#sources}

Adobe Experience Platform可以內嵌來自外部來源的資料，同時允許您使用 [!DNL Platform] 服務。 您可以從多種來源擷取資料，例如Adobe應用程式、雲端儲存、協力廠商軟體和您的CRM系統。

[!DNL Experience Platform] 提供RESTful API和互動式UI，讓您輕鬆為各種資料提供者設定來源連線。 這些源連接允許您驗證並連接到外部儲存系統和CRM服務、設定獲取運行時間以及管理資料獲取吞吐量。

**主要功能**

| 功能 | 說明 |
| ------- | ----------- |
| 更新串流來源的帳戶和連線詳細資訊 | 您現在可以使用 [!DNL Flow Service] API和UI。 如需詳細資訊，請參閱 [使用API更新連線](../../sources/tutorials/api/update.md) 和 [使用UI編輯帳戶詳細資訊](../../sources/tutorials/ui/monitor.md). |
| 刪除資料流 | 現在，可以使用 [!DNL Flow Service] API和UI。 如需詳細資訊，請參閱 [使用API刪除資料流](../../sources/tutorials/api/delete-dataflows.md) 和 [使用UI刪除資料流](../../sources/tutorials/ui/delete.md). |

若要進一步了解來源，請參閱 [來源概觀](../../sources/home.md).
