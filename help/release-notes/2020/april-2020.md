---
title: Adobe Experience Platform 發行說明
description: Experience Platform發行說明2020年4月8日
doc-type: release notes
last-update: April 13, 2020
author: ens71067
keywords: release notes;
translation-type: tm+mt
source-git-commit: 1b398e479137a12bcfc3208d37472aae3d6721e1
workflow-type: tm+mt
source-wordcount: '993'
ht-degree: 5%

---


# Adobe Experience Platform 發行說明

**發行日期：2020 年 4 月 8 日**

Adobe Experience Platform的新功能：
* [[!DNL Intelligent Services]](#intelligent)

更新現有功能：
* [[!DNL體驗資料模型(XDM)]](#xdm)
* [[!DNL資料治理]](#governance)
* [[!DNL目標]](#destinations)
* [[!DNL隱私服務]](#privacy)
* [[!DNL源]](#sources)

## [!DNL Intelligent Services] {#intelligent}

[!DNL Intelligent Services] 讓行銷分析師和從業人員在客戶體驗使用案例中運用人工智慧和機器學習的力量。 這可讓行銷分析人員使用商業層級的組態來設定特定公司需求的預測，而不需要資料科學的專業知識。 此外，行銷從業人員可在Adobe Experience Cloud、Adobe Experience Platform和第三方應用程式中啟動預測。

**主要功能**

| 功能 | 說明 |
|---|---|
| [!DNL Customer AI] | [!DNL Customer AI] 為行銷人員提供在個別層級產生客戶預測的能力，並提供說明。 借助有影響力的因素， [!DNL Customer AI] 您可以瞭解客戶可能做什麼以及為什麼。 此外，行銷人員可從預測和洞 [!DNL Customer AI] 見中獲益，透過提供最適當的優惠和訊息，個人化客戶體驗。 |
| [!DNL Attribution AI] | [!DNL Attribution AI] 是一種多通道的算法歸因服務，可計算客戶互動對特定結果的影響和增量影響。 有了 [!DNL Attribution AI]，行銷人員可以透過瞭解客戶歷程各個階段的每個個別客戶互動的影響，衡量並最佳化行銷和廣告支出。 |

**已知問題**

* 目前沒有已知問題。

如需詳細資訊 [!DNL Intelligent Services] 及其功能，請參閱智慧型服 [務概觀](../../intelligent-services/home.md)。

## [!DNL Experience Data Model] (XDM)系統 {#xdm}

標準化和互操作性是其背後的關鍵概念 [!DNL Experience Platform]。 [!DNL Experience Data Model] (XDM)是由Adobe推動，旨在標準化客戶體驗資料並定義客戶體驗管理的架構。

XDM是公開記載的規格，旨在改善數位體驗的強大功能。 它提供任何應用程式的通用結構和定義，以便與Adobe Experience Platform上的服務通訊。 遵循XDM標準，所有客戶體驗資料都可整合在以更快速、更整合的方式提供見解的通用表現形式中。 您可以從客戶行動中獲得寶貴見解，透過細分定義客戶受眾，並將客戶屬性用於個人化目的。

**新功能**

| 功能 | 說明 |
| --- | --- |
| 自動替代顯示資訊 | 自 [!DNL Schema Registry] 動應用描述符中配置的自定義標題和說 `alternateDisplayInfo` 明值。 |
| 標量欄位限制 | 單 [!DNL Schema Registry] 個方案中不允許超過6000個標量欄位。 |
| 效能大修 | 已 [!DNL Schema Registry] 經全面改造，以滿足更好的需 [!DNL Experience Platform] 求。 |

**錯誤修正**

* 將XDM更新為XED，以支援標準XDM中巢狀URI欄位的更簡潔XED格式。

**已知問題**

* 已知

## [!DNL Data Governance] {#governance}

Adobe Experience Platform是一 [!DNL Data Governance] 系列用於管理客戶資料及確保符合資料使用相關法規、限制和政策的策略與技術。 它在各個層級中都扮演了關 [!DNL Experience Platform] 鍵角色，包括編目、資料傳承、資料使用標籤、資料存取政策，以及對行銷動作資料的存取控制。

開始使用資料治理需要對適用於客戶資料的法規、合約義務和公司政策有深入的瞭解。 在此基礎上，通過應用適當的資料使用標籤對資料進行分類，並通過定義資料使用策略來控制其使用。

DULE框架通過用戶介面和DULE [!DNL Experience Platform][!DNL Policy Service] API簡化了資料分類和建立資料使用策略的過程。

**新功能**

| 功能 | 說明 |
| -----------| ---------- |
| 在UI中管理資料使用原則 | 資料使用原則現在可以在 _UI_ 的 [!DNL Experience Platform] 「原則」工作區中管理。 如需詳細 [資訊，請參閱原則使用指南](../../data-governance/policies/user-guide.md) 。 |

**已知問題**

* 無.

如需詳細資訊，請參閱資 [料管理概觀](../../data-governance/home.md)。


## 目的地 {#destinations}

在 [Adobe即時客戶資料平台中](../../rtcdp/overview.md)，目標是與目標平台預先建立的整合，以順暢的方式將資料啟動給這些合作夥伴。

**新目標**

Adobe Real-time CDP現在支援將資料啟動至超過50種擴充功能 [!DNL Experience Cloud Launch] ，以便進行分析、個人化和其他使用案例。 如需詳細資訊，請參閱以下：

| 文件 | 說明 |
|--- | ---|
| [目標類型和類別](/help/rtcdp/destinations/destination-types.md) | 本文將說明Adobe即時CDP介面中連線與擴充功能的差異，並建議何時使用這些目標。 |
| [Experience Platform Launch擴充功能](/help/rtcdp/destinations/experience-platform-launch-extensions.md) | 本頁說明 [!DNL Launch] Adobe Real-time CDP中各個擴充功能的擴充功能、列出使用案例，以及 [!DNL Launch] 檔案連結。 |

如需詳細資訊，請參閱「目 [標」概觀](/help/rtcdp/destinations/destinations-overview.md)。

## [!DNL Privacy Service] {#privacy}

新的法律和組織法規讓使用者有權應要求從資料存放區存取或刪除其個人資料。 Adobe Experience Platform提 [!DNL Privacy Service] 供REST風格的API和使用者介面，可協助您管理客戶的這些資料要求。 您可 [!DNL Privacy Service]以提交要求，以便從Adobe Experience Cloud應用程式存取和刪除私人或個人客戶資料，以利自動符合法律和組織的隱私權法規。

**新功能**

| 功能 | 說明 |
| --- | --- |
| PDPA支援 | 現在，您可以根據泰國的個人資料保護法(PDPA)來建立和追蹤隱私權要求。 在API中提出隱私權要求時， `regulation` 陣列接受&quot;pdpa_tha&quot;值。 |
| UI中的名稱空間類型 | 您現在可以在UI的「請求產生器」中指定不同的命名空 [!DNL Privacy Service] 間類型。 如需詳細 [資訊，請參閱](../../privacy-service/ui/user-guide.md) 「使用指南」。 |
| 淘汰舊端點 | 舊API端點(`data/privacy/gdpr`)已過時。 |

已知問題

* 無

如需詳細資訊， [!DNL Privacy Service]請先閱讀隱私權服務 [概觀](../../privacy-service/home.md)。

## 來源 {#sources}

Adobe Experience Platform可以從外部來源擷取資料，同時讓您使用服務來建構、標示和增強該資 [!DNL Platform] 料。 您可以從多種來源收集資料，例如Adobe應用程式、雲端儲存空間、協力廠商軟體和您的CRM系統。

[!DNL Experience Platform] 提供REST風格的API和互動式UI，讓您輕鬆地為各種資料提供者設定來源連線。 這些源連接允許您驗證並連接到外部儲存系統和CRM服務、設定接收運行的時間，以及管理資料接收吞吐量。

**新功能**

| 功能 | 說明 |
| ------- | ----------- |
| 資料庫的API和UI支援 | 新的來源 [!DNL Apache Spark] 連接器，適用 [!DNL Azure Synapse Analytics]於 [!DNL Azure Table Storage](HDInsights)、、( [!DNL Hive] 適用於HDInsights)和 [!DNL Phoenix]。 |
| 支援付款型應用程式的API和UI | 新的來源連接器 [!DNL PayPal]。 |
| API和UI支援以通訊協定為基礎的應用程式 | 新的來源連接器 [!DNL Generic OData]。 |

**已知問題**

* 無

若要進一步瞭解來源，請參閱 [來源概觀](../../sources/home.md)。
