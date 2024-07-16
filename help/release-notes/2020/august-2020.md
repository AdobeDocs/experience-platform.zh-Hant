---
title: Adobe Experience Platform發行說明2020年8月
description: Adobe Experience Platform 2020 年 8 月版發行說明。
doc-type: release notes
last-update: August 10, 2020
author: crhoades, ens28527
exl-id: 9347147f-e830-4487-aa12-f56723abb3c8
source-git-commit: 14e3eff3ea2469023823a35ee1112568f5b5f4f7
workflow-type: tm+mt
source-wordcount: '576'
ht-degree: 24%

---

# Adobe Experience Platform 發行說明

**發行日期： 2020年8月12日**

Adobe Experience Platform 現有功能的更新：

- [[!DNL Data Science Workspace]](#dsw)
- [[!DNL Destinations]](#destinations)
- [[!DNL Real-Time Customer Data Platform]](#rtcdp)
- [[!DNL Sources]](#sources)

## [!DNL Data Science Workspace] {#dsw}

[!DNL Data Science Workspace]使用機器學習和人工智慧來釋放您資料的深入分析。 [!DNL Data Science Workspace]已整合至Adobe Experience Platform中，可協助您在各個Adobe解決方案中使用您的內容和資料資產進行預測。

**新功能**

| 功能 | 說明 |
| ------- | ----------- |
| [!DNL JupyterLab]中的VM改善 | 改善長期執行[!DNL JupyterLab notebook]虛擬機器器的穩定性。 |

如需[!DNL JupyterLab]的詳細資訊，請參閱[[!DNL JupyterLab] 使用手冊](../../data-science-workspace/jupyterlab/overview.md)。

## 目的地 {#destinations}

在[Real-time Customer Data Platform](../../rtcdp/overview.md)中，目的地是預先建立的與目的地平台的整合，可透過順暢的方式為這些合作夥伴啟用資料。

**新目的地**

有新的目的地可供您啟用Adobe Experience Platform資料。 如需詳細資訊，請參閱下文：

| 目的地 | 說明 |
|--- | ---|
| [!DNL Google Customer Match] | Google Customer Match可讓您使用線上和離線資料，透過Google所擁有和運作的屬性(例如： [!DNL Search]、[!DNL Shopping]、Gmail和YouTube)聯絡及重新與客戶互動。 <br><br>造訪目的地目錄中的[!DNL Google Customer Match] [頁面](../../destinations/catalog/advertising/google-customer-match.md)，以取得有關目的地以及如何在Real-Time CDP中設定的詳細資訊。 |

**新功能**

| 功能 | 說明 |
|------- | -----------|
| 自訂檔案名稱編輯器 | 電子郵件行銷目的地和雲端儲存目的地的資料啟用工作流程更新，可讓您編輯匯出檔案的名稱。 如需詳細資訊，請參閱啟動工作流程中的[設定步驟](../../destinations/ui/activate-batch-profile-destinations.md)。 |
| 建議的屬性 | 電子郵件行銷目的地和雲端儲存目的地的資料啟用工作流程更新，此工作流程會顯示建議您新增至匯出檔案的屬性。 如需詳細資訊，請參閱啟動工作流程中的[選取屬性步驟](../../destinations/ui/activate-batch-profile-destinations.md)。 |

## [!DNL Real-Time Customer Data Platform] {#rtcdp}

建置在 Experience Platform、Real-Time Customer Data Platform ([!DNL Real-Time CDP]) 上有助於公司匯集已知和未知的資料，以使用整個客戶歷程中的智慧型決策啟動客戶設定檔。[!DNL Real-Time CDP] 會結合多個企業資料來源以即時建立客戶設定檔。然後，根據這些設定檔建置的區段即可傳送到下游目的地，以便在所有管道和裝置上提供一對一的個人化客戶體驗。

**新功能**

| 功能 | 說明 |
| ------- | ----------- |
| IAB TCF 2.0支援 | [!DNL Real-Time CDP]現在是[!DNL Transparency & Consent Framework] (TCF) 2.0版的註冊廠商，如[!DNL Interactive Advertising Bureau] (IAB)所概述。 您可以將資料作業和設定檔結構描述設定為接受CMP產生的客戶同意資料，並在對下游目的地啟用區段時強制實施客戶的同意偏好設定。 |

如需有關 [!DNL Real-Time CDP] 的詳細資訊，請參閱 [[!DNL Real-Time CDP]  概觀](../../rtcdp/overview.md)。

## 來源 {#sources}

Adobe Experience Platform可從外部來源擷取資料，同時允許您使用[!DNL Platform]服務來建構、加標籤及增強該資料。 您可以內嵌來自各種來源的資料，例如Adobe應用程式、雲端儲存、協力廠商軟體和您的CRM系統。

[!DNL Experience Platform]提供RESTful API和互動式UI，讓您輕鬆設定各種資料提供者的來源連線。 這些來源連線可讓您進行驗證並連線到外部儲存系統和 CRM 服務、設定擷取執行的時間並管理資料擷取輸送量。

**新功能**

| 功能 | 說明 |
| ------- | ----------- |
| 資料流執行監視 | 使用者可以監視所有流程執行，並檢視每個執行的詳細檢視，包括完成狀態、執行持續時間、已處理檔案的清單、錯誤和量度。 如需詳細資訊，請參閱[監視資料流](../../sources/tutorials/ui/monitor.md)檔案。 |
| 資料流執行通知 | 使用者可以訂閱事件並註冊Webhook，以接收有關流程執行的狀態、量度和錯誤的即時通知。 |
| UI目錄改善 | 更新來源目錄畫面，更輕鬆地存取所選物件的主要動作。 |

若要深入瞭解來源，請參閱[來源概觀](../../sources/home.md)。
