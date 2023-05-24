---
title: Adobe Experience Platform發行說明2020年4月
description: 2020年4月為Adobe Experience Platform發行的說明。
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

對現有功能的更新：
* [[!DNL Experience Data Model (XDM)]](#xdm)
* [資料治理](#governance)
* [[!DNL Destinations]](#destinations)
* [[!DNL Privacy Service]](#privacy)
* [[!DNL Sources]](#sources)

## [!DNL Intelligent Services] {#intelligent}

[!DNL Intelligent Services] 使營銷分析員和從業人員能夠利用人工智慧和機器學習在客戶體驗使用案例中的威力。 這使市場營銷分析員能夠使用業務級配置來設定特定於公司需要的預測，而無需資料科學專業知識。 此外，營銷從業者可以激活Adobe Experience Cloud、Adobe Experience Platform和第三方應用程式中的預測。

**主要功能**

| 功能 | 說明 |
|---|---|
| [!DNL Customer AI] | [!DNL Customer AI] 為營銷人員提供了在個人層面生成客戶預測的能力，並提供解釋。 在影響因素的幫助下， [!DNL Customer AI] 可以告訴您客戶可能做什麼以及為什麼。 此外，營銷人員還可以從 [!DNL Customer AI] 預測和洞察力，通過提供最合適的優惠和消息服務來個性化客戶體驗。 |
| [!DNL Attribution AI] | [!DNL Attribution AI] 是一種多渠道的算法歸屬服務，它計算客戶交互對特定結果的影響和增量影響。 透過 [!DNL Attribution AI]，行銷人員可經由了解每個客戶在客戶歷程各個階段的互動所產生的影響，來衡量行銷和廣告支出並予以最佳化。 |

**已知問題**

* 當前沒有已知問題。

有關 [!DNL Intelligent Services] 以及它提供的，看看 [智慧服務概述](../../intelligent-services/home.md)。

## [!DNL Experience Data Model] (XDM)系統 {#xdm}

標準化和互操作性是其背後的關鍵概念 [!DNL Experience Platform]。 [!DNL Experience Data Model] (XDM)在Adobe的推動下，致力於標準化客戶體驗資料並定義客戶體驗管理模式。

XDM是一種公開記錄的規範，旨在提高數字型驗的威力。 它為任何與Adobe Experience Platform服務通信的應用程式提供了共同的結構和定義。 通過遵守XDM標準，所有客戶體驗資料都可以納入到一個通用的表示形式中，以更快、更整合的方式提供洞察力。 您可以從客戶操作中獲得有價值的見解，通過細分市場定義客戶受眾，並將客戶屬性用於個性化目的。

**新功能**

| 功能 | 說明 |
| --- | --- |
| 自動備用顯示資訊 | 的 [!DNL Schema Registry] 自動應用在 `alternateDisplayInfo` 描述符。 |
| 標量欄位限制 | 的 [!DNL Schema Registry] 不允許單個架構中超過6000個標量欄位。 |
| 效能大修 | 的 [!DNL Schema Registry] 已經進行了全面改造，以執行和滿足 [!DNL Experience Platform] 更好。 |

**錯誤修正**

* 已將XDM更新為XDM，以支援標準XDM中嵌套URI欄位的清除程式XED格式。

**已知問題**

* 已知

## 資料治理 {#governance}

Adobe Experience Platform資料治理是用於管理客戶資料和確保遵守適用於資料使用的法規、限制和策略的一系列戰略和技術。 它在 [!DNL Experience Platform] 包括編目、資料沿襲、資料使用標籤、資料存取策略和對資料的訪問控制，以執行市場營銷操作。

開始資料治理需要對適用於您的客戶資料的法規、合同義務和公司策略有透徹的瞭解。 從那裡，可以通過應用適當的資料使用標籤來對資料進行分類，並且可以通過定義資料使用策略來控制其使用。

Data Governance框架通過以下幾項簡化並優化了資料分類和建立資料使用策略的過程： [!DNL Experience Platform] 用戶介面和 [!DNL Policy Service] API。

**新功能**

| 功能 | 說明 |
| -----------| ---------- |
| 在UI中管理資料使用策略 | 資料使用策略現在可以在 **策略** 工作區 [!DNL Experience Platform] UI。 查看 [策略使用手冊](../../data-governance/policies/user-guide.md) 的子菜單。 |

**已知問題**

* None.

有關詳細資訊，請參閱 [資料治理概述](../../data-governance/home.md)。


## 目的地 {#destinations}

在 [Real-time Customer Data Platform](../../rtcdp/overview.md)，目標是與目標平台預構建的整合，這些平台可以無縫地向這些合作夥伴激活資料。

**新目標**

Real-Time CDP現在支援資料激活，超過50個 [!DNL Experience Cloud Launch] 擴展、啟用分析、個性化和其他使用案例。 有關詳細資訊，請參閱下面：

| 文件 | 說明 |
|--- | ---|
| [目標類型和類別](../../destinations/destination-types.md) | 本文解釋了Real-Time CDP介面中連接和擴展的區別，並建議何時使用這些目標。 |
| [Experience Platform Launch擴展](../../destinations/catalog/launch-extensions/overview.md) | 本頁說明了 [!DNL Launch] 擴展是，列出使用它們的使用案例，以及每個文檔的文檔連結 [!DNL Launch] Real-Time CDP。 |

有關詳細資訊，請參閱 [目標概述](../../destinations/home.md)。

## [!DNL Privacy Service] {#privacy}

新的法律和組織法規授予使用者權利，讓使用者有權應要求從您的資料存放區存取或刪除其個人資料。Adobe Experience Platform [!DNL Privacy Service] 提供REST風格的API和用戶介面，幫助您管理客戶的這些資料請求。 與 [!DNL Privacy Service]，您可以提交訪問和刪除Adobe Experience Cloud應用程式中的私人或個人客戶資料的請求，以便自動遵守法律和組織隱私法規。

**新功能**

| 功能 | 說明 |
| --- | --- |
| PDPA支援 | 現在，可以根據泰國的個人資料保護法(PDPA)建立和跟蹤隱私請求。 在API中發出隱私請求時， `regulation` array接受值「pdpa_tha」。 |
| UI中的命名空間類型 | 現在，您可以在中的請求生成器中指定不同的命名空間類型 [!DNL Privacy Service] UI。 查看 [使用手冊](../../privacy-service/ui/user-guide.md) 的子菜單。 |
| 舊終結點棄用 | 舊API終結點(`data/privacy/gdpr`)已棄用。 |

已知問題

* None

有關 [!DNL Privacy Service]，請從閱讀 [Privacy Service概述](../../privacy-service/home.md)。

## 來源 {#sources}

Adobe Experience Platform可以從外部源接收資料，同時允許您使用 [!DNL Platform] 服務。 您可以從多種源(如Adobe應用程式、基於雲的儲存、第三方軟體和CRM系統)中接收資料。

[!DNL Experience Platform] 提供了REST風格的API和互動式UI，使您可以輕鬆地為各種資料提供程式設定源連接。 通過這些源連接，您可以驗證並連接到外部儲存系統和CRM服務，設定接收運行時間，並管理資料接收吞吐量。

**新功能**

| 功能 | 說明 |
| ------- | ----------- |
| 資料庫的API和UI支援 | 新的源連接器 [!DNL Apache Spark] (HDInsights) [!DNL Azure Synapse Analytics]。 [!DNL Azure Table Storage]。 [!DNL Hive] (HDInsights), [!DNL Phoenix]。 |
| API和UI支援基於付款的應用程式 | 新的源連接器 [!DNL PayPal]。 |
| API和UI支援基於協定的應用程式 | 新的源連接器 [!DNL Generic OData]。 |

**已知問題**

* None

要瞭解有關源的詳細資訊，請參閱 [源概述](../../sources/home.md)。
