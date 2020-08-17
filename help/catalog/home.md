---
keywords: Experience Platform;home;popular topics;catalog service;catalog;Catalog service;data location;Data Location;Data management;data management;Lineage;lineage;Catalog;enable dataset
solution: Experience Platform
title: 目錄服務概述
topic: overview
description: 目錄服務是Adobe Experience Platform中資料位置和世系的記錄系統。 雖然所有收錄到Experience Platform的資料都會以檔案和目錄的形式儲存在資料湖中，但目錄會保留這些檔案和目錄的中繼資料和說明，以供查閱和監控之用。
translation-type: tm+mt
source-git-commit: bf99b08a1093a815687cc06372407949e170a0b3
workflow-type: tm+mt
source-wordcount: '783'
ht-degree: 5%

---


# [!DNL Catalog Service]概述

[!DNL Catalog Service] 是Adobe Experience Platform中資料位置和世系的記錄系統。 雖然所有收錄到中的資 [!DNL Experience Platform] 料都會以檔案和目錄 [!DNL Data Lake] 的形式儲存在中， [!DNL Catalog] 但會保留這些檔案和目錄的中繼資料和說明，以供查閱和監控之用。

簡單地說， [!DNL Catalog] 您可以當做中繼資料存放區或「[!UICONTROL 目錄]」，在其中找到有關資料的資訊 [!DNL Experience Platform]。 您可以使 [!DNL Catalog] 用來回答下列問題：

* 我的資料位於何處？
* 這些資料處理的階段是什麼？
* 哪些系統或流程對我的資料有作用？
* 已成功處理多少資料？
* 處理期間發生了哪些錯誤？

[!DNL Catalog] 提供REST風格的API，可讓您使用基本的CRUD作業，以程 [!DNL Platform] 式設計方式管理中繼資料。 See the [Catalog developer guide](api/getting-started.md) for more information.

## [!DNL Catalog] 和服 [!DNL Experience Platform] 務

追蹤的資 [!DNL Catalog Service] 源會由多個服務 [!DNL Experience Platform] 使用。 為充份運用功能，建 [!DNL Catalog's] 議您熟悉這些服務及其互動方式 [!DNL Catalog]。

### [!DNL Experience Data Model] (XDM)系統

[!DNL Experience Data Model] (XDM)系統是組織客戶體驗資料的 [!DNL Platform] 標準化架構。 [!DNL Experience Platform] 利用XDM架構，以一致且可重複使用的方式來描述資料結構。

當資料被擷取 [!DNL Platform]時，該資料的結構會映射至XDM架構，並儲存在資料集 [!DNL Data Lake] 的一部 **分**。 每個資料集的元資料由跟蹤 [!DNL Catalog Service]，該元資料包括對資料集所符合的XDM模式的引用。

有關XDM系統的更多一般資訊，請參閱 [XDM系統概述](../xdm/home.md)。

### [!DNL Data Ingestion]

[!DNL Experience Platform] 從多個來源擷取資料，並將記錄保留為資料集 [!DNL Data Lake]。 [!DNL Catalog] 追蹤這些資料集的中繼資料，不論其來源或擷取方法為何。

使用批次擷取方法時，也 [!DNL Catalog] 會追蹤批次檔案的其 **他中繼** 資料。 批次是多個資料單位，由一或多個要作為一個單位進行內嵌的檔案所組成。[!DNL Catalog] 追蹤這些批次檔案的中繼資料，以及擷取後保留的資料集。 批次中繼資料包含成功擷取記錄的數目相關資訊，以及任何失敗記錄和相關的錯誤訊息。

如需詳細 [資訊，請參閱資料擷取](../ingestion/home.md) 概觀。

## [!DNL Catalog] 對象

如上節所述，會追蹤 [!DNL Catalog] 其他服務使用之多種資源和作業的中繼資料 [!DNL Platform] 。 [!DNL Catalog] 維護其自己的「物件」儲存，可封裝此中繼資料。 [!DNL Catalog] 物件是資料的可 [!DNL Platform] 查詢表示，可讓您搜尋、監視和標示資料，而不需存取資料本身。

下表概述了支援的不同對象類型 [!DNL Catalog]:

| 物件 | API端點 | 定義 |
|---|---|---|
| 帳戶 | `/accounts` | 建立源連接時，必須提供驗證憑據。 帳戶代表用來建立特定類型連線的驗證憑證集合。 每個連接都有一組唯一參數，這些參數由 [!DNL Catalog] 並保護在中 [!DNL Azure Key Vault]。 |
| 批次 | `/batches` | 批次是多個資料單位，由一或多個要作為一個單位進行內嵌的檔案所組成。中的批處理對 [!DNL Catalog] 像概述了批處理的接收度量（如已處理的記錄數或磁碟上的大小），還可能包括資料集、視圖和其他受批處理操作影響的資源的連結。 |
| 連線 | `/connections` | 連接是源連接器的單個實例，對於您的組織是唯一的，並且使用連接器類型的適當驗證憑據進行配置。 |
| 連接器 | `/connectors` | 連接器可定義來源連線如何從其他Adobe應用程式（例如Adobe Analytics和Adobe Audience Manager）、協力廠商雲端儲存來源(例如 [!DNL Azure Blob], [!DNL Amazon S3]FTP伺服器和SFTP伺服器)以及協力廠商CRM系統(例如 [!DNL Microsoft Dynamics] 和 [!DNL Salesforce])收集資料。 |
| 資料集 | `/dataSets` | 資料集是用於收集資料（通常是表格）的儲存和管理結構，其中包含結構（欄）和欄（列）。 如需詳細 [資訊，請參閱資料集](./datasets/overview.md) 概觀。 |
| 資料集檔案 | `/datasetFiles` | 資料集檔案代表已儲存在的資料區塊 [!DNL Platform]。 作為常值檔案的記錄，您可以在這些位置找到檔案的大小、檔案包含的記錄數，以及對接收檔案的批的引用。 |

## 後續步驟

本檔案介紹了它在 [!DNL Catalog Service] 更大範圍內的作用及其運作方式 [!DNL Experience Platform]。 如需與 [該API不同端點互動的步驟](api/getting-started.md) ，請參閱目錄開發人員 [!DNL Catalog] 指南。 建議您也參閱「目錄」資料篩 [選指南](api/filter-data.md) ，以遵循限制API回應中傳回資料的最佳實務。