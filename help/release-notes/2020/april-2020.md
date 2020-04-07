---
title: Adobe Experience Platform 發行說明
description: Experience Platform發行說明2020年4月8日
doc-type: release notes
last-update: March 4, 2020
author: ens71067
translation-type: tm+mt
source-git-commit: 1e2299980572116d589e7164dd20e171433a284a

---


# Adobe Experience Platform 發行說明

## 發行日期: 2020 年 4 月 8 日

## 資料控管

Adobe Experience Platform資料治理是一系列策略和技術，用於管理客戶資料並確保符合適用於資料使用的法規、限制和政策。 它在Experience Platform的不同層次發揮關鍵作用，包括編目、資料傳承、資料使用標籤、資料存取政策，以及行銷動作的資料存取控制。

開始使用資料治理需要對適用於客戶資料的法規、合約義務和公司政策有深入的瞭解。 在此基礎上，通過應用適當的資料使用標籤對資料進行分類，並通過定義資料使用策略來控制其使用。

DULE架構透過Experience Platform使用者介面和DULE Policy Service API簡化資料分類和建立資料使用原則的程式。

### 新功能

| 功能 | 說明 |
| -----------| ---------- |
| 在UI中管理資料使用原則 | 資料使用原則現在可以在Experience Platform UI的「 _原則_ 」工作區中管理。 如需詳細 [資訊，請參閱原則使用指南](../../data-governance/policies/user-guide.md) 。 |

**已知問題**

* 無.

如需詳細資訊，請參閱資 [料管理概觀](../../data-governance/home.md)。

## 智慧型服務

智慧型服務可讓行銷分析師和從業人員在客戶體驗使用案例中運用人工智慧和機器學習的強大功能。 這可讓行銷分析人員使用商業層級的組態來設定特定公司需求的預測，而不需要資料科學的專業知識。 此外，行銷從業人員可在Adobe Experience Cloud、Adobe Experience Platform和第三方應用程式中啟動預測。

**主要功能**

| 功能 | 說明 |
|---|---|
| 客戶人工智慧 | 客戶人工智慧為行銷人員提供能力，讓他們在個別層級產生客戶預測並加上說明。 借助影響因素，客戶人工智慧可以告訴您客戶可能做什麼以及為什麼。 此外，行銷人員可從客戶人工智慧預測和見解中獲益，透過提供最適當的優惠和訊息來個人化客戶體驗。 |
| 歸因AI | 歸因人工智慧是一種多通道的算法歸因服務，可計算客戶互動對特定結果的影響和增量影響。 借助Attribution AI，行銷人員可以透過瞭解客戶歷程各個階段的每個個別客戶互動的影響，衡量並最佳化行銷和廣告支出。 |

**已知問題**

* 目前沒有已知問題。

如需智慧型服務的詳細資訊，請參閱智慧型服務 [概觀](../../intelligent-services/home.md)。

## 隱私權服務

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

## 來源

Adobe Experience Platform可以從外部來源擷取資料，同時允許您使用平台服務來建構、標示和增強該資料。 您可以從多種來源收集資料，例如Adobe應用程式、雲端儲存空間、協力廠商軟體和您的CRM系統。

Experience Platform提供REST風格的API和互動式UI，讓您輕鬆為各種資料提供者設定來源連線。 這些源連接允許您驗證並連接到外部儲存系統和CRM服務、設定接收運行的時間，以及管理資料接收吞吐量。

### 新功能

| 功能 | 說明 |
| ------- | ----------- |
| 資料庫的API和UI支援 | Apache Spark（在HDInsights上）、Azure Synapse Analytics、Azure表格儲存、Hive（在HDInsights上）和Phoenix的新來源連接器。 |
| 支援付款型應用程式的API和UI | PayPal的新來源連接器。 |
| API和UI支援以通訊協定為基礎的應用程式 | 通用OData的新來源連接器。 |

### 已知問題

* 無

如需來源的詳細資訊，請參閱來 [源概觀](../../source-connectors/home.md)。