---
title: Adobe Experience Platform發行說明2020年12月
description: 2020年12月發佈Adobe Experience Platform說明。
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

資料流能呈現資料處理作業在平台上移動資料的情形。這些資料流是跨不同的服務配置的，有助於將資料從源連接器移動到目標資料集、到Identity and Profile Service以及移動到目標。

**關鍵功能**

| 功能 | 說明 |
| ------- | ----------- |
| 資料流的透明度 | 您可以監視源和目標的資料流。 有關詳細資訊，請閱讀 [監控源的教程](../../dataflows/ui/monitor-sources.md) 或 [監視目標的教程](../../dataflows/ui/monitor-destinations.md)。 |

要瞭解有關資料流的詳細資訊，請閱讀 [資料流概述](../../dataflows/home.md)。

## [!DNL Data Science Workspace] {#dsw}

Data Science Workspace使用機器學習和人工智慧從資料中建立洞見。 整合到Adobe Experience Platform的Data Science Workspace可幫助您跨Adobe解決方案使用內容和資料資產進行預測。

**主要功能**

| 功能 | 說明 |
| --- | ---|
| Adobe Experience Platform情報包附件 | Adobe Experience Platform智慧軟體包附加是資料科學工作區升級，它解鎖了其他關鍵功能，如： <li> UI驅動的模型實驗和評估。</li><li> 能夠部署模型並將其運行，並安排培訓和引用作業。</li><li> 支援Tensorflow模型（GPU計算）中的深度學習。</li><li> 基於Spark的分佈式計算，可針對大資料集（10MM +行）進行訓練和評分。</li><li>更多</li> |

要瞭解有關Adobe Experience Platform智慧軟體包附加的詳細資訊，請參閱 [Data Science工作區訪問和功能](../../data-science-workspace/access-features-dsw.md)。

## [!DNL Sources] {#sources}

Adobe Experience Platform可以從外部源接收資料，同時允許您使用 [!DNL Platform] 服務。 您可以從多種源(如Adobe應用程式、基於雲的儲存、第三方軟體和CRM系統)中接收資料。

[!DNL Experience Platform] 提供了REST風格的API和互動式UI，使您可以輕鬆地為各種資料提供程式設定源連接。 通過這些源連接，您可以驗證並連接到外部儲存系統和CRM服務，設定接收運行時間，並管理資料接收吞吐量。

**主要功能**

| 功能 | 說明 |
| ------- | ----------- |
| 更新流源的帳戶和連接詳細資訊 | 現在，您可以使用 [!DNL Flow Service] API和UI。 有關詳細資訊，請參見上的教程 [使用API更新連接](../../sources/tutorials/api/update.md) 和 [使用UI編輯帳戶詳細資訊](../../sources/tutorials/ui/monitor.md)。 |
| 刪除資料流 | 現在，可以使用 [!DNL Flow Service] API和UI。 有關詳細資訊，請參見上的教程 [使用API刪除資料流](../../sources/tutorials/api/delete-dataflows.md) 和 [使用UI刪除資料流](../../sources/tutorials/ui/delete.md)。 |

要瞭解有關源的詳細資訊，請參閱 [源概述](../../sources/home.md)。
