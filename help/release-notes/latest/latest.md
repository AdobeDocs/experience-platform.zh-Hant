---
title: Adobe Experience Platform 發行說明
description: Experience Platform發行說明2020年12月9日
doc-type: release notes
last-update: December 9, 2020
author: ens60013 & ens72471
translation-type: tm+mt
source-git-commit: a411ac92d946080abd7b22b9d57c7154d263a30a
workflow-type: tm+mt
source-wordcount: '343'
ht-degree: 7%

---


# Adobe Experience Platform 發行說明

**發行日期：2020年12月9日**

Adobe Experience Platform 現有功能更新：

- [[!DNL Data Science Workspace]](#dsw)
- [[!DNL Sources]](#sources)

## [!DNL Data Science Workspace] {#dsw}

Data Science Workspace使用機器學習和人工智慧，從您的資料中建立見解。 Data Science Workspace整合至Adobe Experience Platform，可協助您透過Adobe解決方案使用內容和資料資產進行預測。

### 主要功能

| 功能 | 說明 |
|--- | ---|
| Adobe Experience Platform Intelligence套件addon | Adobe Experience Platform Intelligence套件addon是Data Science Workspace升級版，可解除鎖定其他主要功能，例如： <li> UI驅動的模型實驗與評估。</li><li> 能夠部署模型並將模型與排定的培訓和推薦工作一起運作。</li><li> 支援Tensorflow模型(GPU Compute)的深入學習。</li><li> 基於Spark的分佈式計算，可針對大型資料集（10MM +列）進行訓練和評分。</li><li>還有更多</li> |

若要進一步瞭解Adobe Experience Platform Intelligence套件說明，請參閱資料科學工作區存 [取與功能的相關檔案](../../data-science-workspace/access-features-dsw.md)。

## [!DNL Sources] {#sources}

Adobe Experience Platform可以從外部來源擷取資料，同時讓您使用服務來建構、標示和增強該資 [!DNL Platform] 料。 您可以從多種來源收集資料，例如Adobe應用程式、雲端儲存空間、協力廠商軟體和您的CRM系統。

[!DNL Experience Platform] 提供REST風格的API和互動式UI，讓您輕鬆地為各種資料提供者設定來源連線。 這些源連接允許您驗證並連接到外部儲存系統和CRM服務、設定接收運行的時間，以及管理資料接收吞吐量。

**主要功能**

| 功能 | 說明 |
| ------- | ----------- |
| 更新串流來源的帳戶和連線詳細資訊 | 您現在可以使用 [!DNL Flow Service] API和UI更新現有串流連線的名稱、說明和認證。 如需詳細資訊，請參閱使用API更 [新連線](../../sources/tutorials/api/update.md) ，以及 [使用UI編輯帳戶詳細資訊的教學課程](../../sources/tutorials/ui/monitor.md)。 |
| 刪除資料流 | 現在，可以使用 [!DNL Flow Service] API和UI刪除包含錯誤或已變得不必要的流資料流。 如需詳細資訊，請參閱使用API刪 [除資料流](../../sources/tutorials/api/delete-dataflows.md) ，以及 [使用UI刪除資料流的教學課程](../../sources/tutorials/ui/delete.md)。 |

若要進一步瞭解來源，請參閱 [來源概觀](../../sources/home.md)。

