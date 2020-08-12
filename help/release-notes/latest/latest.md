---
title: Adobe Experience Platform 發行說明
description: Experience Platform發行說明2020年8月10日
doc-type: release notes
last-update: August 10, 2020
author: crhoades, ens28527
translation-type: tm+mt
source-git-commit: c64d4cc01b5125fad5f7c75914dfc1e4b20bc069
workflow-type: tm+mt
source-wordcount: '297'
ht-degree: 7%

---


# Adobe Experience Platform 發行說明

**發行日期: 2020 年 8 月 12 日**

Adobe Experience Platform現有功能的更新：

- [[!DNL資料科學工作區]](#dsw)
- [[!DNL源]](#sources)

## [!DNL Data Science Workspace] {#dsw}

[!DNL Data Science Workspace] 運用機器學習和人工智慧，從資料中釋放見解。 與Adobe Experience Platform整合，可協 [!DNL Data Science Workspace] 助您使用Adobe解決方案的內容和資料資產進行預測。

**新功能**

| 功能 | 說明 |
| ------- | ----------- |
| 虛擬機在 [!DNL JupyterLab] | 已改善長期運行虛擬機的 [!DNL JupyterLab notebook] 穩定性。 |

如需詳細資訊 [!DNL JupyterLab]，請參閱使 [[!DNL JupyterLab] 用指南](../../data-science-workspace/jupyterlab/overview.md)。

## 來源 {#sources}

Adobe Experience Platform可以從外部來源擷取資料，同時讓您使用服務來建構、標示和增強該資 [!DNL Platform] 料。 您可以從多種來源收集資料，例如Adobe應用程式、雲端儲存空間、協力廠商軟體和您的CRM系統。

[!DNL Experience Platform] 提供REST風格的API和互動式UI，讓您輕鬆地為各種資料提供者設定來源連線。 這些源連接允許您驗證並連接到外部儲存系統和CRM服務、設定接收運行的時間，以及管理資料接收吞吐量。

**新功能**

| 功能 | 說明 |
| ------- | ----------- |
| 流運行監控 | 使用者可監控所有流程執行，並檢視每個執行的詳細檢視，包括完成狀態、執行持續時間、已處理檔案清單、錯誤和度量。 有關詳細信 [息，請參見](../../sources/tutorials/ui/monitor.md) 「監視資料流」文檔。 |
| 帳戶更新 | 使用者可以更新任何現有帳戶的認證、名稱和說明，以提供更有意義的資訊，並修正可能已建立的錯誤。 |
| 流量執行通知 | 使用者可訂閱事件並註冊網頁勾點，以接收有關流量執行的狀態、量度和錯誤的即時通知。 |
| UI目錄改良 | 更新來源目錄畫面，讓您更輕鬆地存取選取物件的主要動作。 |

若要進一步瞭解來源，請參閱 [來源概觀](../../sources/home.md)。
