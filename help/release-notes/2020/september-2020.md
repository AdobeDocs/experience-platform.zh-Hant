---
title: Adobe Experience Platform 發行說明
description: Experience Platform發行說明2020年9月9日
doc-type: release notes
last-update: September 8, 2020
author: crhoades, ens25212
exl-id: bf401f3a-b088-4cbd-9a64-224294b797b9
source-git-commit: a455134a45137b171636d6525ce9124bc95f4335
workflow-type: tm+mt
source-wordcount: '855'
ht-degree: 6%

---

# Adobe Experience Platform 發行說明

**發行日期：2020 年 9 月 9 日**

Adobe Experience Platform 現有功能更新：

- [[!DNL Data Governance]](#governance)
- [[!DNL Destinations]](#destinations)
- [[!DNL Observability Insights]](#observability)
- [[!DNL Privacy Service]](#privacy)
- [[!DNL Real-time Customer Profile]](#profile)
- [[!DNL Segmentation Service]](#segmentation)
- [[!DNL Sources]](#sources)

## [!DNL Data Governance] {#governance}

Adobe Experience Platform資料控管是一系列策略和技術，用於管理客戶資料及確保符合適用於資料使用的法規、限制和政策。 它在[!DNL Experience Platform]中在各個層級發揮關鍵作用，包括編目、資料處理、資料使用標籤、資料訪問策略以及對用於市場營銷操作的資料的訪問控制。

**新功能**

| 功能 | 說明 |
| ------- | ----------- |
| 資料集標籤UI增強功能 | 資料集標籤UI已新增數種排序和篩選控制項，讓您更輕鬆處理大型結構描述： <ul><li>根據完整架構路徑，依字母順序排序欄位。</li><li>對欄位路徑名稱執行部分搜尋。</li><li>篩選沒有標籤的欄位、選取的標籤或標籤類別。</li></ul> |

如需服務的詳細資訊，請參閱[資料控管概述](../../data-governance/home.md) 。

## 目的地 {#destinations}

在[即時客戶資料平台](../../rtcdp/overview.md)中，目標是預先構建的與目標平台的整合，這些平台可無縫地向這些合作夥伴激活資料。

**新功能**

| 功能 | 說明 |
| ------- | ----------- |
| UX改良功能 | 使用者可存取內嵌表格動作，以更輕鬆存取主要動作，例如新增資料、編輯排程和新增區段。 如需詳細資訊，請參閱[destinations workspace](../../destinations/ui/destinations-workspace.md)檔案。 |

若要深入了解，請造訪[目的地概述](../../destinations/home.md)

## [!DNL Observability Insights] {#observability}

[!DNL Observability Insights] 可讓您透過使用統計量度和事件通知來監控Adobe Experience Platform上的活動。

**新特性**

| 功能 | 說明 |
| --- | --- |
| Adobe I/O事件通知 | [!DNL Observability Insights] 會運用Adobe I/O事件來建立數個Experience Platform服務的事件通知。通知裝載會傳送至已設定的網頁連結，然後您可使用該網頁連結來自動執行後續的下遊程式。 |

如需服務的詳細資訊，請參閱[[!DNL Observability Insights] 概述](../../observability/home.md) 。

## [!DNL Privacy Service] {#privacy}

數個法律和組織法規授予使用者權利，可應要求從您的資料存放區存取或刪除其個人資料。 Adobe Experience Platform [!DNL Privacy Service]提供RESTful API和使用者介面，協助您管理客戶的這些資料請求。 透過[!DNL Privacy Service]，您可以提交從Adobe Experience Cloud應用程式存取和刪除私人或個人客戶資料的請求，協助您自動遵守法律和組織隱私權法規。

**新功能**

| 功能 | 說明 |
| ------- | ----------- |
| 支援LGPD（巴西） | 現在可以根據巴西的[!DNL Lei Geral de Proteção de Dados](LGPD)規則建立隱私權工作。 這些作業在規則代碼`lgpd_bra`下被跟蹤。 |

如需服務的詳細資訊，請參閱[Privacy Service概述](../../privacy-service/home.md) 。

## 即時客戶個人檔案 {#profile}

Adobe Experience Platform可讓您為客戶提供協調、一致且相關的體驗，無論客戶在何處或何時與您的品牌互動。 透過[!DNL Real-time Customer Profile]，您可以全面了解將多個管道資料結合在一起的每個客戶，包括線上、離線、CRM和第三方資料。 [!DNL Profile] 可讓您將不同的客戶資料整合至統一的檢視中，提供每個客戶互動的可操作、時間戳記帳戶。

| 功能 | 說明 |
| ------- | ----------- |
| 設定檔檢視器 | Platform UI中的設定檔檢視器已更新為具有完全自訂的控制面板。 使用者現在可以選擇執行下列工作： <ul><li>更新基本資訊Widget中選取的標準屬性和自訂屬性。</li><li>建立、編輯和刪除自定義小部件</li><li>調整小部件大小和重新排列小部件</li></ul> |

有關[!DNL Real-time Customer Profile]的詳細資訊，包括使用[!DNL Profile]資料的教學課程和最佳實務，請參閱[即時客戶設定檔概述](../../profile/home.md)。

## 分段服務 {#segmentation}

Adobe Experience Platform劃分服務提供使用者介面和RESTful API，可讓您建立區段，並從[!DNL Real-time Customer Profile]資料產生對象。 這些區段在[!DNL Platform]上集中配置和維護，使任何Adobe應用程式都可輕鬆訪問。

[!DNL Segmentation Service] 會透過說明區分客戶群中可行銷人員群組的條件，來定義特定設定檔子集。區段可以根據記錄資料（例如人口統計資訊）或代表客戶與您品牌互動的時間序列事件。

**新功能**

| 功能 | 說明 |
| ------- | ----------- |
| 匯出工作 | 已新增標幟，以允許在匯出工作中評估區段。 因此，使用者可以在單一工作中執行分段和匯出。 |
| 合併策略 | 單個批分段作業中可以包含多個合併策略。 |

如需[!DNL Segmentation Service]的詳細資訊，請參閱[分段概述](../../segmentation/home.md)

## 來源 {#sources}

Adobe Experience Platform可以內嵌來自外部來源的資料，同時允許您使用[!DNL Platform]服務來建構、加標籤及增強該資料。 您可以從多種來源擷取資料，例如Adobe應用程式、雲端儲存、協力廠商軟體和您的CRM系統。

[!DNL Experience Platform] 提供RESTful API和互動式UI，讓您輕鬆為各種資料提供者設定來源連線。這些源連接允許您驗證並連接到外部儲存系統和CRM服務、設定獲取運行時間以及管理資料獲取吞吐量。

**新功能**

| 功能 | 說明 |
| ------- | ----------- |
| 自動對應 | [!DNL Platform] 根據使用者選取的目標結構或資料集，提供在資料擷取工作流程期間自動對應的智慧型建議。您可以手動調整有彈性的自動對應規則，以符合您的使用案例。 |
| UX改良功能 | 使用者可存取內嵌表格動作，以更輕鬆存取主要動作，例如新增資料、編輯排程和新增區段。 有關詳細資訊，請參閱[監視資料流](../../sources/tutorials/ui/monitor.md)文檔。 |

若要進一步了解來源，請參閱[來源概述](../../sources/home.md)。
