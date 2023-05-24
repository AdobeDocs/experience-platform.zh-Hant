---
title: Adobe Experience Platform發行說明2020年9月
description: 2020年9月為Adobe Experience Platform發佈的說明。
doc-type: release notes
last-update: September 8, 2020
author: crhoades, ens25212
exl-id: bf401f3a-b088-4cbd-9a64-224294b797b9
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '863'
ht-degree: 6%

---

# Adobe Experience Platform 發行說明

**發行日期：2020 年 9 月 9 日**

Adobe Experience Platform 現有功能更新：

- [資料治理](#governance)
- [[!DNL Destinations]](#destinations)
- [[!DNL Observability Insights]](#observability)
- [[!DNL Privacy Service]](#privacy)
- [[!DNL Real-Time Customer Profile]](#profile)
- [[!DNL Segmentation Service]](#segmentation)
- [[!DNL Sources]](#sources)

## 資料治理 {#governance}

Adobe Experience Platform資料治理是用於管理客戶資料和確保遵守適用於資料使用的法規、限制和策略的一系列戰略和技術。 它在 [!DNL Experience Platform] 包括編目、資料沿襲、資料使用標籤、資料存取策略和對資料的訪問控制，以執行市場營銷操作。

**新功能**

| 功能 | 說明 |
| ------- | ----------- |
| 資料集標籤UI增強 | 在資料集標籤UI中添加了幾個新的排序和篩選控制項，以便更輕鬆地處理大架構： <ul><li>根據完整架構路徑按字母順序對欄位排序。</li><li>對欄位路徑名執行部分搜索。</li><li>篩選沒有標籤、選定標籤或標籤類別的欄位。</li></ul> |

查看 [資料治理概述](../../data-governance/home.md) 的子菜單。

## 目的地 {#destinations}

在 [Real-time Customer Data Platform](../../rtcdp/overview.md)，目標是與目標平台預構建的整合，這些平台可以無縫地向這些合作夥伴激活資料。

**新功能**

| 功能 | 說明 |
| ------- | ----------- |
| UX改進 | 用戶可以訪問內聯表操作，以便更方便地訪問主操作，如添加資料、編輯計畫和添加段。 查看 [目標工作區](../../destinations/ui/destinations-workspace.md) 的子菜單。 |

要瞭解更多資訊，請訪問 [目標概述](../../destinations/home.md)

## [!DNL Observability Insights] {#observability}

[!DNL Observability Insights] 允許您使用統計度量和事件通知來監視Adobe Experience Platform的活動。

**新特性**

| 功能 | 說明 |
| --- | --- |
| Adobe I/O事件通知 | [!DNL Observability Insights] 利用Adobe I/O事件為多個Experience Platform服務建立事件通知。 通知負載將發送到已配置的Webhook，然後您可以使用它自動執行進一步的下游進程。 |

查看 [[!DNL Observability Insights] 概述](../../observability/home.md) 的子菜單。

## [!DNL Privacy Service] {#privacy}

一些法律和組織法規允許用戶根據請求訪問或刪除資料儲存中的個人資料。 Adobe Experience Platform [!DNL Privacy Service] 提供REST風格的API和用戶介面，幫助您管理客戶的這些資料請求。 與 [!DNL Privacy Service]，您可以提交訪問和刪除Adobe Experience Cloud應用程式中的私人或個人客戶資料的請求，以便自動遵守法律和組織隱私法規。

**新功能**

| 功能 | 說明 |
| ------- | ----------- |
| 支援LGPD（巴西） | 如今，在巴西的隱私政策下，可以創造隱私工作 [!DNL Lei Geral de Proteção de Dados] (LGPD)條例。 這些作業在法規代碼下被跟蹤 `lgpd_bra`。 |

查看 [Privacy Service概述](../../privacy-service/home.md) 的子菜單。

## 即時客戶設定檔 {#profile}

Adobe Experience Platform使您能夠為您的客戶提供協調、一致和相關的體驗，無論客戶在何處或何時與您的品牌進行交互。 與 [!DNL Real-Time Customer Profile]，您可以看到每個客戶的整體視圖，該視圖將來自多個渠道的資料組合在一起，包括線上、離線、CRM和第三方資料。 [!DNL Profile] 允許您將全異的客戶資料整合到一個統一視圖中，為每個客戶交互提供一個可操作且時間戳記的帳戶。

| 功能 | 說明 |
| ------- | ----------- |
| 配置檔案查看器 | 已在平台UI中將配置檔案查看器更新為具有完全自定義功能的儀表板。 用戶現在可以選擇執行以下任務： <ul><li>更新基本資訊構件中選定的標準屬性和自定義屬性。</li><li>建立、編輯和刪除自定義小部件</li><li>調整小部件大小並重新排列小部件</li></ul> |

有關 [!DNL Real-Time Customer Profile]包括教程和最佳實踐 [!DNL Profile] 資料，請閱讀 [即時客戶概要資訊概述](../../profile/home.md)。

## 分段服務 {#segmentation}

Adobe Experience Platform分段服務提供用戶介面和REST風格的API，使您能夠生成分段並從您的 [!DNL Real-Time Customer Profile] 資料。 這些段在 [!DNL Platform]使任何Adobe應用程式都可輕鬆訪問。

[!DNL Segmentation Service] 通過描述區分客戶群中可銷售人員組的標準來定義特定配置檔案子集。 段可以基於記錄資料（如人口統計資訊）或表示客戶與您品牌的交互的時間序列事件。

**新功能**

| 功能 | 說明 |
| ------- | ----------- |
| 導出作業 | 添加了標誌，以允許將段作為導出作業的一部分進行評估。 因此，用戶可以在單個作業中運行分段和導出。 |
| 合併策略 | 單個批處理分段作業中可以包含多個合併策略。 |

有關 [!DNL Segmentation Service]，請參閱 [分段概述](../../segmentation/home.md)

## 來源 {#sources}

Adobe Experience Platform可以從外部源接收資料，同時允許您使用 [!DNL Platform] 服務。 您可以從多種源(如Adobe應用程式、基於雲的儲存、第三方軟體和CRM系統)中接收資料。

[!DNL Experience Platform] 提供了REST風格的API和互動式UI，使您可以輕鬆地為各種資料提供程式設定源連接。 通過這些源連接，您可以驗證並連接到外部儲存系統和CRM服務，設定接收運行時間，並管理資料接收吞吐量。

**新功能**

| 功能 | 說明 |
| ------- | ----------- |
| 自動映射 | [!DNL Platform] 基於用戶選擇的目標模式或資料集，為資料接收工作流期間的自動映射提供智慧建議。 您可以手動調整靈活的自動映射規則以適合您的使用情形。 |
| UX改進 | 用戶可以訪問內聯表操作，以便更方便地訪問主操作，如添加資料、編輯計畫和添加段。 查看 [監視資料流](../../sources/tutorials/ui/monitor.md) 的子菜單。 |

要瞭解有關源的詳細資訊，請參閱 [源概述](../../sources/home.md)。
