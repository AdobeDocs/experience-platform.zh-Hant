---
title: Adobe Experience Platform發行說明2020年4月
description: 2020年4月Adobe Experience Platform發行說明。
doc-type: release notes
last-update: April 13, 2020
author: ens71067
keywords: 發行說明;
exl-id: 0f68c71e-3c9d-453b-a953-1cd1b6ca2e35
source-git-commit: 14e3eff3ea2469023823a35ee1112568f5b5f4f7
workflow-type: tm+mt
source-wordcount: '983'
ht-degree: 10%

---

# Adobe Experience Platform 發行說明

**發行日期：2020 年 4 月 8 日**

Adobe Experience Platform的新功能：
* [[!DNL Intelligent Services]](#intelligent)

更新現有功能：
* [[!DNL Experience Data Model (XDM)]](#xdm)
* [資料治理](#governance)
* [[!DNL Destinations]](#destinations)
* [[!DNL Privacy Service]](#privacy)
* [[!DNL Sources]](#sources)

## [!DNL Intelligent Services] {#intelligent}

[!DNL Intelligent Services] 讓行銷分析師和從業人員在客戶體驗使用案例中，善用人工智慧和機器學習的強大功能。 這可讓行銷分析人員使用業務層級設定，針對公司的需求設定專屬預測，而不需要資料科學的專業知識。 此外，行銷從業人員可在Adobe Experience Cloud、Adobe Experience Platform和第三方應用程式中啟用預測。

**主要功能**

| 功能 | 說明 |
|---|---|
| [!DNL Customer AI] | [!DNL Customer AI] 為行銷人員提供在個人層級產生客戶預測的能力，並提供說明。 在影響因素的幫助下， [!DNL Customer AI] 可以告訴您客戶可能做什麼以及為什麼。 此外，行銷人員也可從 [!DNL Customer AI] 預測和深入分析，提供最合適的選件和訊息，以個人化客戶體驗。 |
| [!DNL Attribution AI] | [!DNL Attribution AI] 是多管道的演算法歸因服務，可計算客戶互動對指定結果的影響和增量影響。 透過 [!DNL Attribution AI]，行銷人員可經由了解每個客戶在客戶歷程各個階段的互動所產生的影響，來衡量行銷和廣告支出並予以最佳化。 |

**已知問題**

* 目前沒有已知問題。

如需 [!DNL Intelligent Services] 以及它所提供的，請參閱 [Intelligent Services概觀](../../intelligent-services/home.md).

## [!DNL Experience Data Model] (XDM)系統 {#xdm}

標準化和互操作性是背後的關鍵概念 [!DNL Experience Platform]. [!DNL Experience Data Model] (XDM)受Adobe推動，致力標準化客戶體驗資料並定義客戶體驗管理的結構。

XDM是公開記錄的規格，旨在改善數位體驗的強大功能。 它為與Adobe Experience Platform上的服務通訊的任何應用程式提供共同的結構和定義。 遵循XDM標準，所有客戶體驗資料皆可整合至以更快速、更整合的方式提供深入分析的通用表示法中。 您可以從客戶動作中獲得寶貴的深入分析、透過區段定義客戶受眾，以及將客戶屬性用於個人化目的。

**新功能**

| 功能 | 說明 |
| --- | --- |
| 自動替代顯示資訊 | 此 [!DNL Schema Registry] 自動套用在 `alternateDisplayInfo` 描述符。 |
| 標量欄位限制 | 此 [!DNL Schema Registry] 在單個架構中不允許超過6000個標量欄位。 |
| 效能檢修 | 此 [!DNL Schema Registry] 已全面檢修，以執行和滿足 [!DNL Experience Platform] 更好。 |

**錯誤修正**

* 將XDM更新為XED，以支援標準XDM中巢狀URI欄位的簡潔XED格式。

**已知問題**

* 已知

## 資料治理 {#governance}

Adobe Experience Platform資料控管是一系列策略和技術，用於管理客戶資料及確保符合適用於資料使用的法規、限制和政策。 在 [!DNL Experience Platform] 在各個層級，包括編目、資料處理、資料使用標籤、資料存取策略，以及針對行銷動作的資料存取控制。

若要開始使用資料控管功能，您必須全面了解適用於客戶資料的法規、合約義務和公司政策。 從那裡，資料可以通過應用適當的資料使用標籤來分類，而資料的使用可以通過定義資料使用策略來控制。

資料控管架構透過 [!DNL Experience Platform] 使用者介面和 [!DNL Policy Service] API。

**新功能**

| 功能 | 說明 |
| -----------| ---------- |
| 在UI中管理資料使用原則 | 現在可以在 **原則** 工作區中 [!DNL Experience Platform] UI。 請參閱 [原則使用手冊](../../data-governance/policies/user-guide.md) 以取得更多資訊。 |

**已知問題**

* None.

如需詳細資訊，請參閱 [資料控管概觀](../../data-governance/home.md).


## 目的地 {#destinations}

在 [Real-time Customer Data Platform](../../rtcdp/overview.md)，目的地是與目的地平台預先建立的整合，可順暢地向這些合作夥伴啟用資料。

**新目的地**

Real-Time CDP現在支援將資料啟動至超過五十個 [!DNL Experience Cloud Launch] 擴充功能，啟用分析、個人化和其他使用案例。 如需詳細資訊，請參閱下方：

| 文件 | 說明 |
|--- | ---|
| [目的地類型和類別](../../destinations/destination-types.md) | 本文說明Real-Time CDP介面中連線和擴充功能之間的差異，並建議何時分別使用這些目的地。 |
| [Experience Platform Launch擴充功能](../../destinations/catalog/launch-extensions/overview.md) | 本頁說明 [!DNL Launch] 擴充功能包括：列出使用案例，以及各個擴充功能的檔案連結 [!DNL Launch] 擴充功能。 |

如需詳細資訊，請參閱 [目的地概觀](../../destinations/home.md).

## [!DNL Privacy Service] {#privacy}

新的法律和組織法規授予使用者權利，讓使用者有權應要求從您的資料存放區存取或刪除其個人資料。Adobe Experience Platform [!DNL Privacy Service] 提供RESTful API和使用者介面，協助您管理客戶的這些資料請求。 使用 [!DNL Privacy Service]，您可以提交從Adobe Experience Cloud應用程式存取和刪除私人或個人客戶資料的請求，協助您自動遵循法律和組織隱私權法規。

**新功能**

| 功能 | 說明 |
| --- | --- |
| PDPA支援 | 現在可根據泰國的個人資料保護法(PDPA)建立及追蹤隱私權要求。 在API中提出隱私權要求時， `regulation` array接受「pdpa_tha」值。 |
| UI中的命名空間類型 | 您現在可以在「請求產生器」中指定不同的命名空間類型，位於 [!DNL Privacy Service] UI。 請參閱 [使用手冊](../../privacy-service/ui/user-guide.md) 以取得更多資訊。 |
| 淘汰舊端點 | 舊的API端點(`data/privacy/gdpr`)已過時。 |

已知問題

* None

如需 [!DNL Privacy Service]，請先閱讀 [Privacy Service概述](../../privacy-service/home.md).

## 來源 {#sources}

Adobe Experience Platform可以內嵌來自外部來源的資料，同時允許您使用 [!DNL Platform] 服務。 您可以從多種來源擷取資料，例如Adobe應用程式、雲端儲存、協力廠商軟體和您的CRM系統。

[!DNL Experience Platform] 提供RESTful API和互動式UI，讓您輕鬆為各種資料提供者設定來源連線。 這些源連接允許您驗證並連接到外部儲存系統和CRM服務、設定獲取運行時間以及管理資料獲取吞吐量。

**新功能**

| 功能 | 說明 |
| ------- | ----------- |
| 資料庫的API和UI支援 | 新源連接器 [!DNL Apache Spark] （在HDInsights上）, [!DNL Azure Synapse Analytics], [!DNL Azure Table Storage], [!DNL Hive] （在HDInsights上），以及 [!DNL Phoenix]. |
| 支援支付型應用程式的API和UI | 新源連接器 [!DNL PayPal]. |
| 適用於通訊協定型應用程式的API和UI支援 | 新源連接器 [!DNL Generic OData]. |

**已知問題**

* 無

若要進一步了解來源，請參閱 [來源概觀](../../sources/home.md).
