---
title: Adobe Experience Platform 發行說明
description: Experience Platform發行說明2020年8月10日
doc-type: release notes
last-update: August 10, 2020
author: crhoades, ens28527
translation-type: tm+mt
source-git-commit: 49c984a60fd699706eec508ec1d786340df40b57
workflow-type: tm+mt
source-wordcount: '568'
ht-degree: 7%

---


# Adobe Experience Platform 發行說明

**發行日期：2020 年 12 月 8 日**

Adobe Experience Platform 現有功能更新：

- [[!DNL Data Science Workspace]](#dsw)
- [[!DNL Destinations]](#destinations)
- [[!DNL Real-time Customer Data Platform]](#rtcdp)
- [[!DNL Sources]](#sources)

## [!DNL Data Science Workspace] {#dsw}

[!DNL Data Science Workspace] 運用機器學習和人工智慧，從資料中釋放見解。[!DNL Data Science Workspace]已整合至Adobe Experience Platform，可協助您使用Adobe解決方案中的內容和資料資產進行預測。

**新功能**

| 功能 | 說明 |
| ------- | ----------- |
| [!DNL JupyterLab]中的虛擬機改進 | 已改善長期運行[!DNL JupyterLab notebook]虛擬機的穩定性。 |

有關[!DNL JupyterLab]的更多資訊，請參閱[[!DNL JupyterLab] 使用手冊](../../data-science-workspace/jupyterlab/overview.md)。

## 目的地 {#destinations}

在[即時客戶資料平台](../../rtcdp/overview.md)中，目標是預先建立的與目標平台的整合，這些平台可順暢地向這些合作夥伴啟用資料。

**新目標**

您可以在新目的地啟用Adobe Experience Platform資料。 如需詳細資訊，請參閱以下：

| 目的地 | 說明 |
|--- | ---|
| [!DNL Google Customer Match] | Google Customer Match可讓您使用您的線上和離線資料，透過Google擁有和營運的資產觸及並重新與客戶互動，例如：[!DNL Search]、[!DNL Shopping]、Gmail和YouTube。 <br><br> 請造訪 [!DNL Google Customer Match] [](../../destinations/catalog/advertising/google-customer-match.md) 目標目錄中的頁面，以瞭解有關目標以及如何在即時CDP中設定該目標的詳細資訊。 |

**新功能**

| 功能 | 說明 |
|------- | -----------|
| 自訂檔案名稱編輯器 | 更新至電子郵件行銷目的地和雲端儲存空間目的地的資料啟動工作流程，讓您編輯匯出檔案的名稱。 如需詳細資訊，請參閱啟動工作流程中的「設定步驟[」。](../../destinations/ui/activate-destinations.md#configure) |
| 建議的屬性 | 更新至電子郵件行銷目的地和雲端儲存空間目的地的資料啟動工作流程，以顯示您要新增至匯出檔案的建議屬性。 如需詳細資訊，請參閱啟動工作流程中的「選取屬性」步驟[。](../../destinations/ui/activate-destinations.md#select-attributes) |

## [!DNL Real-time Customer Data Platform] {#rtcdp}

即時客戶資料平台([!DNL Real-time CDP])以Experience Platform為基礎，可協助公司將已知和未知的資料匯整在一起，在整個客戶歷程中運用智慧決策來啟動客戶個人檔案。 [!DNL Real-time CDP] 結合多個企業資料來源，即時建立客戶個人檔案。然後，從這些個人檔案建立的細分可以傳送至下游目的地，以便在所有通道和裝置上提供一對一的個人化客戶體驗。

**新功能**

| 功能 | 說明 |
| ------- | ----------- |
| IAB TCF 2.0支援 | [!DNL Real-time CDP] 如(IAB)所述，現在已是2.0版 [!DNL Transparency & Consent Framework] (TCF)的註冊 [!DNL Interactive Advertising Bureau] 廠商。您可以配置資料操作和概要檔案結構以接受由CMP生成的客戶許可資料，並在激活到下游目標的細分時強制執行客戶的許可偏好。 |

如需[!DNL Real-time CDP]的詳細資訊，請參閱[[!DNL Real-time CDP] overview](../../rtcdp/overview.md)。

## 來源 {#sources}

Adobe Experience Platform可以從外部來源收錄資料，同時允許您使用[!DNL Platform]服務來建構、標籤和增強該資料。 您可以從多種來源收集資料，例如Adobe應用程式、雲端儲存空間、協力廠商軟體和您的CRM系統。

[!DNL Experience Platform] 提供REST風格的API和互動式UI，讓您輕鬆地為各種資料提供者設定來源連線。這些源連接允許您驗證並連接到外部儲存系統和CRM服務、設定接收運行的時間，以及管理資料接收吞吐量。

**新功能**

| 功能 | 說明 |
| ------- | ----------- |
| 流運行監控 | 使用者可監控所有流程執行，並檢視每個執行的詳細檢視，包括完成狀態、執行持續時間、已處理檔案清單、錯誤和度量。 有關詳細資訊，請參見[監視資料流](../../sources/tutorials/ui/monitor.md)文檔。 |
| 流量執行通知 | 使用者可訂閱事件並註冊網頁勾點，以接收有關流量執行的狀態、量度和錯誤的即時通知。 |
| UI目錄改良 | 更新來源目錄畫面，讓您更輕鬆地存取選取物件的主要動作。 |

若要進一步瞭解來源，請參閱[來源概觀](../../sources/home.md)。