---
title: Adobe Experience Platform發行說明2020年8月
description: 2020年8月Adobe Experience Platform發行說明。
doc-type: release notes
last-update: August 10, 2020
author: crhoades, ens28527
exl-id: 9347147f-e830-4487-aa12-f56723abb3c8
source-git-commit: 14e3eff3ea2469023823a35ee1112568f5b5f4f7
workflow-type: tm+mt
source-wordcount: '572'
ht-degree: 6%

---

# Adobe Experience Platform 發行說明

**發行日期：2020 年 12 月 8 日**

Adobe Experience Platform 現有功能更新：

- [[!DNL Data Science Workspace]](#dsw)
- [[!DNL Destinations]](#destinations)
- [[!DNL Real-Time Customer Data Platform]](#rtcdp)
- [[!DNL Sources]](#sources)

## [!DNL Data Science Workspace] {#dsw}

[!DNL Data Science Workspace] 使用機器學習和人工智慧，釋放資料的深入見解。 整合至Adobe Experience Platform, [!DNL Data Science Workspace] 可協助您跨Adobe解決方案使用內容和資料資產進行預測。

**新功能**

| 功能 | 說明 |
| ------- | ----------- |
| 虛擬機在 [!DNL JupyterLab] | 提高長跑的穩定性 [!DNL JupyterLab notebook] 虛擬機。 |

如需 [!DNL JupyterLab]，請參閱 [[!DNL JupyterLab] 使用手冊](../../data-science-workspace/jupyterlab/overview.md).

## 目的地 {#destinations}

在 [Real-time Customer Data Platform](../../rtcdp/overview.md)，目的地是與目的地平台預先建立的整合，可順暢地向這些合作夥伴啟用資料。

**新目的地**

您可以在新目的地啟用Adobe Experience Platform資料。 如需詳細資訊，請參閱下方：

| 目的地 | 說明 |
|--- | ---|
| [!DNL Google Customer Match] | Google Customer Match可讓您使用您的線上和離線資料，觸及Google擁有且運作的屬性並與客戶重新互動，例如： [!DNL Search], [!DNL Shopping]、Gmail和YouTube。 <br><br> 造訪 [!DNL Google Customer Match] [頁面](../../destinations/catalog/advertising/google-customer-match.md) 目的地目錄，以取得目的地以及如何在Real-Time CDP中設定的詳細資訊。 |

**新功能**

| 功能 | 說明 |
|------- | -----------|
| 自訂檔案名稱編輯器 | 更新電子郵件行銷目的地和雲端儲存空間目的地的資料啟用工作流程，讓您編輯匯出的檔案名稱。 如需詳細資訊，請參閱 [ 配置步驟](../../destinations/ui/activate-batch-profile-destinations.md) 在啟動工作流程中。 |
| 建議的屬性 | 更新電子郵件行銷目的地和雲端儲存空間目的地的資料啟用工作流程，顯示您可新增至匯出檔案的建議屬性。 如需詳細資訊，請參閱 [選擇屬性步驟](../../destinations/ui/activate-batch-profile-destinations.md) 在啟動工作流程中。 |

## [!DNL Real-Time Customer Data Platform] {#rtcdp}

建置於Experience Platform上，Real-time Customer Data Platform([!DNL Real-Time CDP])可協助公司整合已知和未知的資料，在客戶歷程中運用智慧決策功能啟用客戶設定檔。 [!DNL Real-Time CDP] 結合多個企業資料來源，即時建立客戶設定檔。 然後，從這些設定檔建立的區段可傳送至下游目的地，以在所有通道和裝置上提供一對一的個人化客戶體驗。

**新功能**

| 功能 | 說明 |
| ------- | ----------- |
| IAB TCF 2.0支援 | [!DNL Real-Time CDP] 現在是2.0版的 [!DNL Transparency & Consent Framework] (TCF)，如 [!DNL Interactive Advertising Bureau] (IAB)。 您可以設定資料操作和設定檔結構以接受CMP產生的客戶同意資料，並在將區段啟用至下游目的地時強制執行客戶同意偏好設定。 |

如需 [!DNL Real-Time CDP]，請參閱 [[!DNL Real-Time CDP] 概述](../../rtcdp/overview.md).

## 來源 {#sources}

Adobe Experience Platform可以內嵌來自外部來源的資料，同時允許您使用 [!DNL Platform] 服務。 您可以從多種來源擷取資料，例如Adobe應用程式、雲端儲存、協力廠商軟體和您的CRM系統。

[!DNL Experience Platform] 提供RESTful API和互動式UI，讓您輕鬆為各種資料提供者設定來源連線。 這些源連接允許您驗證並連接到外部儲存系統和CRM服務、設定獲取運行時間以及管理資料獲取吞吐量。

**新功能**

| 功能 | 說明 |
| ------- | ----------- |
| 流運行監視 | 使用者可以監視所有流程執行，並查看每次執行的詳細檢視，包括完成狀態、執行期間、已處理檔案清單、錯誤和量度。 請參閱 [監視資料流](../../sources/tutorials/ui/monitor.md) 文檔以了解更多資訊。 |
| 流運行通知 | 使用者可訂閱事件並註冊WebHook，以接收有關流量執行的狀態、量度和錯誤的即時通知。 |
| UI目錄改良 | 更新源目錄螢幕，以便更輕鬆地訪問選定對象的主操作。 |

若要進一步了解來源，請參閱 [來源概觀](../../sources/home.md).
