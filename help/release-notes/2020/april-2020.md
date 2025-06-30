---
title: Adobe Experience Platform 發行說明 (2020 年 4 月)
description: Adobe Experience Platform 2020 年 4 月版發行說明。
doc-type: release notes
last-update: April 13, 2020
author: ens71067
keywords: 發行說明；
exl-id: 0f68c71e-3c9d-453b-a953-1cd1b6ca2e35
source-git-commit: 104db777446b19fa9e3ea7538ae1dda6f51a00b1
workflow-type: tm+mt
source-wordcount: '972'
ht-degree: 28%

---

# Adobe Experience Platform 發行說明

**發行日期： 2020年4月8日**

Adobe Experience Platform 的新功能：
* [[!DNL Intelligent Services]](#intelligent)

更新現有功能：
* [[!DNL Experience Data Model (XDM)]](#xdm)
* [資料治理](#governance)
* [[!DNL Destinations]](#destinations)
* [[!DNL Privacy Service]](#privacy)
* [[!DNL Sources]](#sources)

## [!DNL Intelligent Services] {#intelligent}

[!DNL Intelligent Services]讓行銷分析師及從業人員運用客戶體驗使用案例中人工智慧和機器學習的強大功能。 這可讓行銷分析人員使用業務層級設定，針對公司需求設定專屬預測，而不需要資料科學專業知識。 此外，行銷從業人員可以在Adobe Experience Cloud、Adobe Experience Platform和第三方應用程式中啟用預測。

**主要功能**

| 功能 | 說明 |
|---|---|
| [!DNL Customer AI] | [!DNL Customer AI]可讓行銷人員產生個人層面的客戶預測並提供解釋。 在影響因子的協助下，[!DNL Customer AI]可以告訴您客戶可能會做什麼以及為什麼。 此外，行銷人員可受益於[!DNL Customer AI]個預測和深入分析，藉由提供最適合的方案和訊息來個人化客戶體驗。 |
| [!DNL Attribution AI] | [!DNL Attribution AI]是多管道的演演算法歸因服務，可計算客戶互動對指定結果的影響和累加影響。 透過[!DNL Attribution AI]，行銷人員可經由瞭解每個客戶在客戶歷程各個階段的互動所產生的影響，來衡量行銷和廣告支出並予以最佳化。 |

**已知問題**

* 目前沒有已知問題。

如需[!DNL Intelligent Services]及其所提供內容的詳細資訊，請參閱[Intelligent Services概述](../../intelligent-services/home.md)。

## [!DNL Experience Data Model] (XDM)系統 {#xdm}

標準化和互通性是[!DNL Experience Platform]背後的重要概念。 由Adobe驅動的[!DNL Experience Data Model] (XDM)致力於標準化客戶體驗資料並定義客戶體驗管理的結構描述。

XDM是公開記錄的規格，旨在改善數位體驗的效能。 它為任何應用程式提供通用結構和定義，以便與Adobe Experience Platform上的服務通訊。 只要遵循XDM標準，所有客戶體驗資料都能整合到共同表現中，以更快、更整合的方式提供深入分析。 您可以從客戶行為中獲得有價值的分析洞察、透過區段定義客戶客群，並基於個人化目的使用客戶屬性。

**新功能**

| 功能 | 說明 |
| --- | --- |
| 自動替代顯示資訊 | [!DNL Schema Registry]會自動套用`alternateDisplayInfo`描述項中設定的自訂標題和描述值。 |
| 純量欄位限制 | [!DNL Schema Registry]不允許單一結構描述中有超過6000個純量欄位。 |
| 效能檢修 | [!DNL Schema Registry]已全面整修，以更好地執行並滿足[!DNL Experience Platform]的需求。 |

**錯誤修正**

* 將XDM更新為XED已轉換，以支援標準XDM中巢狀URI欄位的較乾淨的XED格式。

**已知問題**

* 已知

## 資料治理 {#governance}

Adobe Experience Platform 資料治理是一系列的策略和技術，用於管理客戶資料並確保符合適用於資料使用方式的法規、限制和政策。它在 [!DNL Experience Platform] 的不同階層都扮演重要的角色，包括編目、資料譜系、資料使用標籤、資料存取政策，以及對行銷動作資料的存取控制。

開始使用資料控管需要徹底瞭解適用於客戶資料的規定、合約義務和公司政策。 從那裡，可以套用適當的資料使用標籤來分類資料，並且可以透過資料使用原則的定義來控制其使用。

資料控管架構可簡化並簡化分類資料，以及透過[!DNL Experience Platform]使用者介面和[!DNL Policy Service] API建立資料使用原則的程式。

**新功能**

| 功能 | 說明 |
| -----------| ---------- |
| 管理 UI 中的資料使用原則 | 現在可以在[!DNL Experience Platform] UI的&#x200B;**原則**&#x200B;工作區中管理資料使用原則。 如需詳細資訊，請參閱[原則使用手冊](../../data-governance/policies/user-guide.md)。 |

**已知問題**

* 無。

如需詳細資訊，請參閱[資料控管概觀](../../data-governance/home.md)。


## 目標 {#destinations}

在[Real-Time Customer Data Platform](../../rtcdp/overview.md)中，目的地是預先建立的與目的地平台的整合，可透過順暢的方式為這些合作夥伴啟用資料。

**新目的地**

Real-Time CDP現在支援五十個以上的[!DNL Experience Cloud Launch]擴充功能啟用資料，以啟用Analytics、個人化和其他使用案例。 如需詳細資訊，請參閱下文：

| 文件 | 說明 |
|--- | ---|
| [目的地型別和類別](../../destinations/destination-types.md) | 本文說明Real-Time CDP介面中的連線和擴充功能之間的差異，並建議何時應使用各個目的地。 |
| [Experience Platform Launch擴充功能](../../destinations/catalog/launch-extensions/overview.md) | 此頁面說明何謂[!DNL Launch]擴充功能，列出使用這些擴充功能的使用案例，以及Real-Time CDP中每個[!DNL Launch]擴充功能的檔案連結。 |

如需詳細資訊，請參閱[目的地概觀](../../destinations/home.md)。

## [!DNL Privacy Service] {#privacy}

新的法律和組織法規授予使用者權利，讓使用者有權應要求從您的資料存放區存取或刪除其個人資料。 Adobe Experience Platform [!DNL Privacy Service] 提供 RESTful API 和使用者介面，協助您管理這些來自客戶的資料請求。透過 [!DNL Privacy Service]，您可以提交請求來存取和刪除 Adobe Experience Cloud 應用程式中的私人或個人客戶資料，進而促進法律和組織隱私法規的自動化合規。

**新功能**

| 功能 | 說明 |
| --- | --- |
| PDPA 支援 | 隱私權請求現在可以在泰國根據個人資料保護法(PDPA)進行建立和追蹤。 在 API 中提出隱私權請求時，`regulation` 陣列會接受「pdpa_tha」值。 |
| UI 中的命名空間類型 | 您現在可於 [!DNL Privacy Service] UI 的請求產生器中指定不同的命名空間類型。若需要更多資訊，請參閱[使用手冊](../../privacy-service/ui/user-guide.md)。 |
| 舊端點不再使用不用 | 舊 API 端點 (`data/privacy/gdpr`) 已不再使用。 |

已知問題

* None

如需[!DNL Privacy Service]的詳細資訊，請先閱讀[Privacy Service概觀](../../privacy-service/home.md)。

## 來源 {#sources}

Adobe Experience Platform可從外部來源擷取資料，同時允許您使用[!DNL Experience Platform]服務來建構、加標籤及增強該資料。 您可以內嵌來自各種來源的資料，例如Adobe應用程式、雲端儲存、協力廠商軟體和您的CRM系統。

[!DNL Experience Platform]提供RESTful API和互動式UI，讓您輕鬆設定各種資料提供者的來源連線。 這些來源連線可讓您進行驗證，並連線到外部儲存系統和 CRM 服務、設定攝取執行的時間，並管理資料攝取輸送量。

**新功能**

| 功能 | 說明 |
| ------- | ----------- |
| 資料庫的API和UI支援 | [!DNL Apache Spark] （在HDInsights）、[!DNL Azure Synapse Analytics]、[!DNL Azure Table Storage]和[!DNL Hive]的新來源聯結器。 |
| 通訊協定型應用程式的API和UI支援 | [!DNL Generic OData]的新來源聯結器。 |

**已知問題**

* None

若要深入瞭解來源，請參閱[來源概觀](../../sources/home.md)。
