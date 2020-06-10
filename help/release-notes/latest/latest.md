---
title: Adobe Experience Platform 發行說明
description: Experience Platform發行說明2020年6月10日
doc-type: release notes
last-update: June 10, 2020
author: crhoades, ens28527
translation-type: tm+mt
source-git-commit: 35af498a41d779cc155cff7f030cccb57f68b8fa
workflow-type: tm+mt
source-wordcount: '429'
ht-degree: 5%

---


# Adobe Experience Platform 發行說明

**發行日期: 2020 年 6 月 10 日**

Adobe Experience Platform現有功能的更新：

- [資料科學工作區](#dsw)
- [區段](#segmentation)
- [來源](#sources)

## 資料科學工作區 {#dsw}

Data Science Workspace使用機器學習和人工智慧，從您的資料中釋放深入資訊。 Data Science Workspace整合至Adobe Experience Platform，可協助您透過Adobe解決方案使用內容和資料資產進行預測。

Data Science Workspace一直在研發新方式，透過即時機器學習提供更佳的體驗和預測。 即時機器學習提供以業界標準可互操作模型格式編寫、測試和部署自訂或已匯入的預先訓練機器學習模型的能力，以便透過API端點進行即時計分／啟動。

請注意，即時機器學習是alpha版，目前仍在開發中。

| 功能 | 說明 |
|--- | ---|
| JupyterLab Launcher Real-time ML啟動器 | JupyterLab Launcher現在包含Python筆記型筆記型啟動器，可用於即時機器學習(Alpha)。 |

如需「即時機器學習alpha版」的詳細資訊，請參閱「即 [時機器學習」總覽](../../data-science-workspace/real-time-machine-learning/home.md)。

## 區段 {#segmentation}

Adobe Experience Platform Segmentation Service提供使用者介面和REST風格的API，可讓您建立細分並從即時客戶個人檔案資料產生受眾。 這些區段是在Platform上集中設定和維護的，讓任何Adobe應用程式都能輕鬆存取。

區段服務會透過說明區分客戶群中可銷售人員群組的標準，來定義特定的設定檔子集。 區段可以根據記錄資料（例如人口統計資訊）或代表客戶與品牌互動的時間系列事件來劃分。

**新功能**

| 功能 | 說明 |
| ------- | ----------- |
| 日期欄位 | 已新增日期功能的「週年」功能，讓使用者可評估不含年份的日期。 |

如需劃分的詳細資訊，請參閱劃分 [概觀](../../segmentation/home.md)

## 來源 {#sources}

Adobe Experience Platform可以從外部來源擷取資料，同時允許您使用平台服務來建構、標示和增強該資料。 您可以從多種來源收集資料，例如Adobe應用程式、雲端儲存空間、協力廠商軟體和您的CRM系統。

Experience Platform提供REST風格的API和互動式UI，讓您輕鬆為各種資料提供者設定來源連線。 這些源連接允許您驗證並連接到外部儲存系統和CRM服務、設定接收運行的時間，以及管理資料接收吞吐量。

**新功能**

| 功能 | 說明 |
| ------- | ----------- |
| 雲端儲存系統的其他API和UI支援 | Apache HDFS的新來源連接器 |
| 其他資料庫的API和UI支援 | Couchbase的新來源連接器。 |

若要進一步瞭解來源，請參閱 [來源概觀](../../sources/home.md)。
