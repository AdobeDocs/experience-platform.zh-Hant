---
title: Adobe Experience Platform 發行說明
description: Experience Platform發行說明2020年9月9日
doc-type: release notes
last-update: September 8, 2020
author: crhoades, ens25212
translation-type: tm+mt
source-git-commit: adf8e8457c8ffef263223a38d3f9c345cf7c6ab2
workflow-type: tm+mt
source-wordcount: '862'
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

Adobe Experience Platform資料治理是一系列策略和技術，用於管理客戶資料並確保符合適用於資料使用的法規、限制和政策。 它在各個層級中都扮演了關 [!DNL Experience Platform] 鍵角色，包括編目、資料傳承、資料使用標籤、資料存取政策，以及對行銷動作資料的存取控制。

**新功能**

| 功能 | 說明 |
| ------- | ----------- |
| 資料集標籤UI增強功能 | 為了讓處理大型結構描述更輕鬆，在資料集標籤UI時新增了數種排序和篩選控制項： <ul><li>根據完整方案路徑，依字母順序排序欄位。</li><li>對欄位路徑名執行部分搜索。</li><li>篩選沒有標籤的欄位、選取的標籤或標籤類別。</li></ul> |

如需服務 [的詳細資訊](../../data-governance/home.md) ，請參閱資料管理概觀。

## 目的地 {#destinations}

在即 [時客戶資料平台中](../../rtcdp/overview.md)，目標是與目標平台預先建立的整合，以順暢的方式將資料啟動給這些合作夥伴。

**新功能**

| 功能 | 說明 |
| ------- | ----------- |
| UX改進 | 使用者可存取內嵌表格動作，以更輕鬆地存取主要動作，例如新增資料、編輯排程和新增區段。 如需詳細 [資訊，請參閱目標工作區](../../destinations/ui/destinations-workspace.md) 檔案。 |

若要進一步瞭解，請造訪目 [標總覽](../../destinations/home.md)

## [!DNL Observability Insights] {#observability}

[!DNL Observability Insights] 可讓您透過使用統計量度和事件通知，監控Adobe Experience Platform上的活動。

**新特性**

| 功能 | 說明 |
| --- | --- |
| Adobe I/O活動通知 | [!DNL Observability Insights] 運用Adobe I/O Events為數種Experience Platform服務建立事件通知。 通知負載會傳送至已設定的網頁掛接，然後您便可使用此網頁掛接來自動化下遊程式。 See the [notifications overview](../../observability/notifications/overview.md) for more information. |

如需服務 [[!DNL Observability Insights] 的詳細資訊](../../observability/home.md) ，請參閱總覽。

## [!DNL Privacy Service] {#privacy}

數項法律和組織法規授予使用者在要求時從資料存放區存取或刪除其個人資料的權利。 Adobe Experience Platform提 [!DNL Privacy Service] 供REST風格的API和使用者介面，可協助您管理客戶的這些資料要求。 您可 [!DNL Privacy Service]以提交要求，以便從Adobe Experience Cloud應用程式存取和刪除私人或個人客戶資料，以利自動符合法律和組織的隱私權法規。

**新功能**

| 功能 | 說明 |
| ------- | ----------- |
| 支援LGPD（巴西） | 現在，可以根據巴西的(LGPD)法規創 [!DNL Lei Geral de Proteção de Dados] 造隱私崗位。 這些工作是根據法規代碼進行跟蹤的 `lgpd_bra`。 |

如需服務 [的詳細資訊](../../privacy-service/home.md) ，請參閱隱私權服務概觀。

## 即時客戶個人檔案 {#profile}

Adobe Experience Platform可讓您為客戶推動協調、一致且相關的體驗，不論客戶在何處或何時與您的品牌互動。 透過 [!DNL Real-time Customer Profile]此功能，您可以全面瞭解每個客戶，並結合來自多個通道的資料，包括線上、離線、CRM和第三方資料。 [!DNL Profile] 可讓您將分散的客戶資料整合為統一的檢視，提供每個客戶互動的可操作、時間戳記帳戶。

| 功能 | 說明 |
| ------- | ----------- |
| 設定檔檢視器 | 在「平台UI」中，描述檔檢視器已更新為具有完整自訂功能的控制面板。 使用者現在可以選擇執行下列工作： <ul><li>在基本資訊介面工具集中更新選取的標準屬性和自訂屬性。</li><li>建立、編輯和移除自訂Widget</li><li>調整Widget大小並重新排列</li></ul> |

有關使用資 [!DNL Real-time Customer Profile]料的更多資訊，包括教學課程和最佳實務，請 [!DNL Profile] 閱讀即時客 [戶資料概觀](../../profile/home.md)。

## 劃分服務 {#segmentation}

Adobe Experience Platform Segmentation Service提供使用者介面和REST風格的API，可讓您建立細分並從資料中產生受 [!DNL Real-time Customer Profile] 眾。 這些區段是集中設定並維護的， [!DNL Platform]讓任何Adobe應用程式都可輕鬆存取。

[!DNL Segmentation Service] 定義個人檔案的特定子集，方法是描述區分客戶群中有價人群的標準。 區段可以根據記錄資料（例如人口統計資訊）或代表客戶與品牌互動的時間系列事件來劃分。

**新功能**

| 功能 | 說明 |
| ------- | ----------- |
| 匯出工作 | 已新增旗標，以允許評估區段為匯出工作的一部分。 因此，使用者可以在單一工作中執行區段和匯出。 |
| 合併原則 | 單一批次分段工作可包含多個合併原則。 |

如需詳細資訊， [!DNL Segmentation Service]請參閱區 [段概觀](../../segmentation/home.md)

## 來源 {#sources}

Adobe Experience Platform可以從外部來源擷取資料，同時讓您使用服務來建構、標示和增強該資 [!DNL Platform] 料。 您可以從多種來源收集資料，例如Adobe應用程式、雲端儲存空間、協力廠商軟體和您的CRM系統。

[!DNL Experience Platform] 提供REST風格的API和互動式UI，讓您輕鬆地為各種資料提供者設定來源連線。 這些源連接允許您驗證並連接到外部儲存系統和CRM服務、設定接收運行的時間，以及管理資料接收吞吐量。

**新功能**

| 功能 | 說明 |
| ------- | ----------- |
| 自動對應 | [!DNL Platform] 根據使用者選擇的目標架構或資料集，提供在資料擷取工作流程期間自動對應的智慧建議。 您可以手動調整有彈性的自動對應規則，以符合您的使用案例。 |
| UX改進 | 使用者可存取內嵌表格動作，以更輕鬆地存取主要動作，例如新增資料、編輯排程和新增區段。 有關詳細信 [息，請參見](../../sources/tutorials/ui/monitor.md) 「監視資料流」文檔。 |

若要進一步瞭解來源，請參閱 [來源概觀](../../sources/home.md)。
