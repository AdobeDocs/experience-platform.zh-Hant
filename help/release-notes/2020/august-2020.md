---
title: Adobe Experience Platform發行說明2020年8月
description: 2020年8月為Adobe Experience Platform發行的說明。
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

[!DNL Data Science Workspace] 利用機器學習和人工智慧從資料中釋放洞見。 融入Adobe Experience Platform, [!DNL Data Science Workspace] 幫助您跨Adobe解決方案使用內容和資料資產進行預測。

**新功能**

| 功能 | 說明 |
| ------- | ----------- |
| 虛擬機改進 [!DNL JupyterLab] | 提高長跑穩定性 [!DNL JupyterLab notebook] 虛擬機。 |

有關 [!DNL JupyterLab]，請參閱 [[!DNL JupyterLab] 使用手冊](../../data-science-workspace/jupyterlab/overview.md)。

## 目的地 {#destinations}

在 [Real-time Customer Data Platform](../../rtcdp/overview.md)，目標是與目標平台預構建的整合，這些平台可以無縫地向這些合作夥伴激活資料。

**新目標**

新目標可用，您可以在其中激活Adobe Experience Platform資料。 有關詳細資訊，請參閱下面：

| 目的地 | 說明 |
|--- | ---|
| [!DNL Google Customer Match] | Google客戶匹配允許您使用線上和離線資料，跨Google自有和運營的物業與客戶聯繫和重新接觸，例如： [!DNL Search]。 [!DNL Shopping]、Gmail和YouTube。 <br><br> 訪問 [!DNL Google Customer Match] [頁](../../destinations/catalog/advertising/google-customer-match.md) 目標目錄中，以瞭解有關目標以及如何在Real-Time CDP設定目標的詳細資訊。 |

**新功能**

| 功能 | 說明 |
|------- | -----------|
| 自定義檔案名編輯器 | 更新到電子郵件營銷目標和雲儲存目標的資料激活工作流，以便您編輯導出檔案的名稱。 有關詳細資訊，請參閱 [ 配置步驟](../../destinations/ui/activate-batch-profile-destinations.md) 中。 |
| 建議的屬性 | 更新到電子郵件營銷目標和雲儲存目標的資料激活工作流，該工作流顯示建議的屬性，供您添加到導出的檔案。 有關詳細資訊，請參閱 [選擇屬性步驟](../../destinations/ui/activate-batch-profile-destinations.md) 中。 |

## [!DNL Real-Time Customer Data Platform] {#rtcdp}

基於Experience Platform,Real-time Customer Data Platform([!DNL Real-Time CDP])幫助公司將已知和未知資料匯集起來，在整個客戶過程中通過智慧決策激活客戶配置檔案。 [!DNL Real-Time CDP] 合併多個企業資料源以即時建立客戶配置檔案。 然後，可以將這些配置檔案構建的資料段發送到下游目的地，以便跨所有渠道和設備提供一對一的個性化客戶體驗。

**新功能**

| 功能 | 說明 |
| ------- | ----------- |
| IAB TCF 2.0支援 | [!DNL Real-Time CDP] 現在是2.0版的 [!DNL Transparency & Consent Framework] (TCF)，如 [!DNL Interactive Advertising Bureau] (IAB)。 您可以配置資料操作和配置檔案架構以接受由CMP生成的客戶同意資料，並在將段激活到下游目標時強制客戶的同意首選項。 |

有關 [!DNL Real-Time CDP]，請參見 [[!DNL Real-Time CDP] 概述](../../rtcdp/overview.md)。

## 來源 {#sources}

Adobe Experience Platform可以從外部源接收資料，同時允許您使用 [!DNL Platform] 服務。 您可以從多種源(如Adobe應用程式、基於雲的儲存、第三方軟體和CRM系統)中接收資料。

[!DNL Experience Platform] 提供了REST風格的API和互動式UI，使您可以輕鬆地為各種資料提供程式設定源連接。 通過這些源連接，您可以驗證並連接到外部儲存系統和CRM服務，設定接收運行時間，並管理資料接收吞吐量。

**新功能**

| 功能 | 說明 |
| ------- | ----------- |
| 流運行監控 | 用戶可以監視所有流運行並查看每個運行的詳細視圖，包括完成狀態、運行持續時間、已處理檔案清單、錯誤和度量。 查看 [監視資料流](../../sources/tutorials/ui/monitor.md) 的子菜單。 |
| 流運行通知 | 用戶可以訂閱事件並註冊Webhook，以接收有關流運行的狀態、度量和錯誤的即時通知。 |
| UI目錄改進 | 更新到源目錄螢幕，以便更方便地訪問選定對象的主要操作。 |

要瞭解有關源的詳細資訊，請參閱 [源概述](../../sources/home.md)。
