---
title: Adobe Experience Platform 發行說明
description: Experience Platform發行說明2020年4月8日
doc-type: release notes
last-update: March 4, 2020
author: ens71067
translation-type: tm+mt
source-git-commit: 3f3704cc1e11a4d11278a34800c8bfdc24a80753

---


# Adobe Experience Platform 發行說明

## 發行日期: 2020 年 4 月 8 日

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

<!-- ## Access control

Experience Platform leverages [Adobe Admin Console](https://adminconsole.adobe.com) product profiles to link users with permissions and sandboxes. Permissions control access to a variety of Platform capabilities, including data modeling, profile management, and sandbox administration.

### Key features

|Feature | Description|
|--- | ---|
|Permissions | In the Admin Console, the _Permissions_ tab within a Platform product profile allows you customize which Platform capabilities are available for the users attached to that profile. Available permission categories include: Data Modeling, Data Management, Profile Management, Identities, Data Monitoring, Sandbox Administration, Destinations, Sources.|
|Access to sandboxes | The _Permissions_ tab within a Platform product profile can grant users access to specific sandboxes. See the section on [sandboxes](#sandboxes) below for more information.|

For more information, please see the [access control overview](../../access-control/home.md).

## Sandboxes

Experience Platform is built to enrich digital experience applications on a global scale. Companies often run multiple digital experience applications in parallel and need to cater for the development, testing, and deployment of these applications while ensuring operational compliance. In order to address this need, Experience Platform provides sandboxes which partition a single Platform instance into separate virtual environments to help develop and evolve digital experience applications.

### Key features

|Feature | Description|
|--- | ---|
|Production sandbox | Experience Platform provides a single production sandbox, which cannot be deleted or reset.|
|Non-production sandboxes | Multiple non-production sandboxes can be created for a single Platform instance, allowing you to test features, run experiments, and make custom configurations without impacting your production sandbox.|
|Sandbox switcher | In the Experience Platform user interface, the sandbox switcher in the top-left corner of the screen allows you to switch between available sandboxes through a dropdown menu.|
|`x-sandbox-name` header | All calls to Experience Platform APIs must now include the new `x-sandbox-name` header, whose value references the `name` attribute of the sandbox the operation will take place in.|

For more information, please see the [sandboxes overview](../../sandboxes/home.md). -->