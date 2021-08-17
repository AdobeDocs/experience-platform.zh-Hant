---
title: Adobe Experience Platform 發行說明
description: Experience Platform發行說明2020年8月10日
doc-type: release notes
last-update: August 10, 2020
author: crhoades, ens28527
exl-id: 9347147f-e830-4487-aa12-f56723abb3c8
source-git-commit: a619227de30513bb06a22ce7b4f2fc13847c1ab6
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

[!DNL Data Science Workspace] 使用機器學習和人工智慧，釋放資料的深入見解。[!DNL Data Science Workspace]已整合至Adobe Experience Platform，可協助您跨Adobe解決方案使用內容和資料資產進行預測。

**新功能**

| 功能 | 說明 |
| ------- | ----------- |
| [!DNL JupyterLab]中的虛擬機改進 | 改善了長運行[!DNL JupyterLab notebook]虛擬機的穩定性。 |

有關[!DNL JupyterLab]的詳細資訊，請參閱[[!DNL JupyterLab] 使用手冊](../../data-science-workspace/jupyterlab/overview.md)。

## 目的地 {#destinations}

在[即時客戶資料平台](../../rtcdp/overview.md)中，目標是預先構建的與目標平台的整合，這些平台可無縫地向這些合作夥伴激活資料。

**新目的地**

您可以在新目的地啟用Adobe Experience Platform資料。 如需詳細資訊，請參閱下方：

| 目的地 | 說明 |
|--- | ---|
| [!DNL Google Customer Match] | Google Customer Match可讓您使用您的線上和離線資料，在Google擁有且運作的屬性中觸及客戶並與其重新互動，例如：[!DNL Search]、[!DNL Shopping]、Gmail及YouTube。 <br><br> 請造訪 [!DNL Google Customer Match] [](../../destinations/catalog/advertising/google-customer-match.md) 目的地目錄的頁面，以取得有關目的地以及如何在即時CDP中設定目的地的詳細資訊。 |

**新功能**

| 功能 | 說明 |
|------- | -----------|
| 自訂檔案名稱編輯器 | 更新電子郵件行銷目的地和雲端儲存空間目的地的資料啟用工作流程，讓您編輯匯出的檔案名稱。 如需詳細資訊，請參閱啟動工作流程中的[設定步驟](../../destinations/ui/activate-batch-profile-destinations.md) 。 |
| 建議的屬性 | 更新電子郵件行銷目的地和雲端儲存空間目的地的資料啟用工作流程，顯示您可新增至匯出檔案的建議屬性。 如需詳細資訊，請參閱啟動工作流程中的[選取屬性步驟](../../destinations/ui/activate-batch-profile-destinations.md)。 |

## [!DNL Real-time Customer Data Platform] {#rtcdp}

即時客戶資料平台([!DNL Real-time CDP])以Experience Platform為基礎，可協助公司匯集已知和未知的資料，在客戶歷程中透過智慧決策來啟用客戶設定檔。 [!DNL Real-time CDP] 結合多個企業資料來源，即時建立客戶設定檔。然後，從這些設定檔建立的區段可傳送至下游目的地，以在所有通道和裝置上提供一對一的個人化客戶體驗。

**新功能**

| 功能 | 說明 |
| ------- | ----------- |
| IAB TCF 2.0支援 | [!DNL Real-time CDP] 如(IAB)所述，現在是2.0 [!DNL Transparency & Consent Framework] 版(TCF)的註冊 [!DNL Interactive Advertising Bureau] 廠商。您可以設定資料操作和設定檔結構以接受CMP產生的客戶同意資料，並在將區段啟用至下游目的地時強制執行客戶同意偏好設定。 |

有關[!DNL Real-time CDP]的詳細資訊，請參閱[[!DNL Real-time CDP] overview](../../rtcdp/overview.md)。

## 來源 {#sources}

Adobe Experience Platform可以內嵌來自外部來源的資料，同時允許您使用[!DNL Platform]服務來建構、加標籤及增強該資料。 您可以從多種來源擷取資料，例如Adobe應用程式、雲端儲存、協力廠商軟體和您的CRM系統。

[!DNL Experience Platform] 提供RESTful API和互動式UI，讓您輕鬆為各種資料提供者設定來源連線。這些源連接允許您驗證並連接到外部儲存系統和CRM服務、設定獲取運行時間以及管理資料獲取吞吐量。

**新功能**

| 功能 | 說明 |
| ------- | ----------- |
| 流運行監視 | 使用者可以監視所有流程執行，並查看每次執行的詳細檢視，包括完成狀態、執行期間、已處理檔案清單、錯誤和量度。 有關詳細資訊，請參閱[監視資料流](../../sources/tutorials/ui/monitor.md)文檔。 |
| 流運行通知 | 使用者可訂閱事件並註冊WebHook，以接收有關流量執行的狀態、量度和錯誤的即時通知。 |
| UI目錄改良 | 更新源目錄螢幕，以便更輕鬆地訪問選定對象的主操作。 |

若要進一步了解來源，請參閱[來源概述](../../sources/home.md)。
