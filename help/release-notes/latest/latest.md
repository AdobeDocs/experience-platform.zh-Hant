---
title: Adobe Experience Platform 發行說明
description: Experience Platform發行說明2020年4月8日
doc-type: release notes
last-update: April 13, 2020
author: ens71067
keywords: release notes;
translation-type: tm+mt
source-git-commit: 43db1992ae45e27134bc0c4405963c405275750e

---


# Adobe Experience Platform 發行說明

**發行日期：2020 年 4 月 8 日**

Adobe Experience Platform的新功能：
* [智慧型服務](#intelligent)

更新現有功能：
* [體驗資料模型(XDM)](#xdm)
* [資料控管](#governance)
* [目的地](#destinations)
* [隱私權服務](#privacy)
* [來源](#sources)

## 智慧型服務 {#intelligent}

智慧型服務可讓行銷分析師和從業人員在客戶體驗使用案例中運用人工智慧和機器學習的強大功能。 這可讓行銷分析人員使用商業層級的組態來設定特定公司需求的預測，而不需要資料科學的專業知識。 此外，行銷從業人員可在Adobe Experience Cloud、Adobe Experience Platform和第三方應用程式中啟動預測。

**主要功能**

| 功能 | 說明 |
|---|---|
| 客戶人工智慧 | 客戶人工智慧為行銷人員提供能力，讓他們在個別層級產生客戶預測並加上說明。 借助影響因素，客戶人工智慧可以告訴您客戶可能做什麼以及為什麼。 此外，行銷人員可從客戶人工智慧預測和見解中獲益，透過提供最適當的優惠和訊息來個人化客戶體驗。 |
| 歸因AI | 歸因人工智慧是一種多通道的算法歸因服務，可計算客戶互動對特定結果的影響和增量影響。 借助Attribution AI，行銷人員可以透過瞭解客戶歷程各個階段的每個個別客戶互動的影響，衡量並最佳化行銷和廣告支出。 |

**已知問題**

* 目前沒有已知問題。

如需智慧型服務的詳細資訊，請參閱智慧型服務 [概觀](../../intelligent-services/home.md)。

## 體驗資料模型(XDM)系統 {#xdm}

標準化和互操作性是Experience Platform的主要概念。 Adobe推動的Experience Data Model(XDM)旨在標準化客戶體驗資料並定義客戶體驗管理的架構。

XDM是公開記載的規格，旨在改善數位體驗的強大功能。 它提供任何應用程式的通用結構和定義，以便與Adobe Experience Platform上的服務通訊。 遵循XDM標準，所有客戶體驗資料都可整合在以更快速、更整合的方式提供見解的通用表現形式中。 您可以從客戶行動中獲得寶貴見解，透過細分定義客戶受眾，並將客戶屬性用於個人化目的。

**新功能**

| 功能 | 說明 |
| --- | --- |
| 自動替代顯示資訊 | 方案註冊表會自動應用描述符中配置的自定義標題和說明 `alternateDisplayInfo` 值。 |
| 標量欄位限制 | 方案註冊表不允許在單個方案中有超過6000個標量欄位。 |
| 效能大修 | 架構註冊表已進行全面改造，以更好地執行並滿足Experience Platform的需求。 |

**錯誤修正**

* 將XDM更新為XED，以支援標準XDM中巢狀URI欄位的更簡潔XED格式。

**已知問題**

* 已知

## 資料控管 {#governance}

Adobe Experience Platform資料治理是一系列策略和技術，用於管理客戶資料並確保符合適用於資料使用的法規、限制和政策。 它在Experience Platform的不同層次發揮關鍵作用，包括編目、資料傳承、資料使用標籤、資料存取政策，以及行銷動作的資料存取控制。

開始使用資料治理需要對適用於客戶資料的法規、合約義務和公司政策有深入的瞭解。 在此基礎上，通過應用適當的資料使用標籤對資料進行分類，並通過定義資料使用策略來控制其使用。

DULE架構透過Experience Platform使用者介面和DULE Policy Service API簡化資料分類和建立資料使用原則的程式。

**新功能**

| 功能 | 說明 |
| -----------| ---------- |
| 在UI中管理資料使用原則 | 資料使用原則現在可以在Experience Platform UI的「 _原則_ 」工作區中管理。 如需詳細 [資訊，請參閱原則使用指南](../../data-governance/policies/user-guide.md) 。 |

**已知問題**

* 無.

如需詳細資訊，請參閱資 [料管理概觀](../../data-governance/home.md)。


## 目的地 {#destinations}

在 [Adobe即時客戶資料平台中](../../rtcdp/overview.md)，目標是與目標平台預先建立的整合，以順暢的方式將資料啟動給這些合作夥伴。

**新目標**

Adobe Real-time CDP現在支援將資料啟動至超過50種Experience Cloud Launch擴充功能，以便進行分析、個人化和其他使用案例。 如需詳細資訊，請參閱以下：

| 文件 | 說明 |
|--- | ---|
| [目標類型和類別](/help/rtcdp/destinations/destination-types.md) | 本文將說明Adobe即時CDP介面中連線與擴充功能的差異，並建議何時使用這些目標。 |
| [Experience Platform Launch擴充功能](/help/rtcdp/destinations/experience-platform-launch-extensions.md) | 本頁說明Launch擴充功能，列出使用這些擴充功能的使用案例，以及Adobe Real-time CDP中每個Launch擴充功能的檔案連結。 |

如需詳細資訊，請參閱「目 [標」概觀](/help/rtcdp/destinations/destinations-overview.md)。

## 隱私權服務 {#privacy}

新的法律和組織法規讓使用者有權應要求從資料存放區存取或刪除其個人資料。 Adobe Experience Platform Privacy Service提供REST風格的API和使用者介面，可協助您管理客戶的這些資料要求。 透過隱私權服務，您可以提交從Adobe Experience Cloud應用程式存取和刪除私人或個人客戶資料的要求，以利自動符合法律和組織的隱私權法規。

**新功能**

| 功能 | 說明 |
| --- | --- |
| PDPA支援 | 現在，您可以根據泰國的個人資料保護法(PDPA)來建立和追蹤隱私權要求。 在API中提出隱私權要求時， `regulation` 陣列接受&quot;pdpa_tha&quot;值。 |
| UI中的名稱空間類型 | 您現在可以在「隱私服務」UI的「請求產生器」中指定不同的命名空間類型。 如需詳細 [資訊，請參閱](../../privacy-service/ui/user-guide.md) 「使用指南」。 |
| 淘汰舊端點 | 舊API端點(`data/privacy/gdpr`)已過時。 |

已知問題

* 無

如需隱私權服務的詳細資訊，請先閱讀隱私權服務 [概觀](../../privacy-service/home.md)。

## 來源 {#sources}

Adobe Experience Platform可以從外部來源擷取資料，同時允許您使用平台服務來建構、標示和增強該資料。 您可以從多種來源收集資料，例如Adobe應用程式、雲端儲存空間、協力廠商軟體和您的CRM系統。

Experience Platform提供REST風格的API和互動式UI，讓您輕鬆為各種資料提供者設定來源連線。 這些源連接允許您驗證並連接到外部儲存系統和CRM服務、設定接收運行的時間，以及管理資料接收吞吐量。

**新功能**

| 功能 | 說明 |
| ------- | ----------- |
| 資料庫的API和UI支援 | Apache Spark（在HDInsights上）、Azure Synapse Analytics、Azure表格儲存、Hive（在HDInsights上）和Phoenix的新來源連接器。 |
| 支援付款型應用程式的API和UI | PayPal的新來源連接器。 |
| API和UI支援以通訊協定為基礎的應用程式 | 通用OData的新來源連接器。 |

**已知問題**

* 無

若要進一步瞭解來源，請參閱 [來源概觀](../../sources/home.md)。
