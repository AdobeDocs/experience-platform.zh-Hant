---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 目錄服務概述
topic: overview
translation-type: tm+mt
source-git-commit: 1fce86193bc1660d0f16408ed1b9217368549f6c
workflow-type: tm+mt
source-wordcount: '804'
ht-degree: 5%

---


# 目錄服務概述

目錄服務是Adobe Experience Platform中資料位置和世系的記錄系統。 雖然所有收錄到Experience Platform的資料都會以檔案和目錄的形式儲存在資料湖中，但目錄會保留這些檔案和目錄的中繼資料和說明，以供查閱和監控之用。

簡而言之，Catalog可當成中繼資料存放區或「目錄」，您可在其中找到Experience Platform中資料的相關資訊。 您可以使用目錄回答下列問題：

* 我的資料位於何處？
* 這些資料處理的階段是什麼？
* 哪些系統或流程對我的資料有作用？
* 已成功處理多少資料？
* 處理期間發生了哪些錯誤？

Catalog提供REST風格的API，可讓您使用基本的CRUD作業，以程式設計方式管理平台中繼資料。 See the [Catalog developer guide](api/getting-started.md) for more information.

## 型錄與體驗平台服務

目錄服務追蹤的資源由多個Experience Platform服務使用。 為充份運用Catalog的功能，建議您熟悉這些服務以及它們與Catalog的互動方式。

### 體驗資料模型(XDM)系統

Experience Data Model(XDM)System是平台組織客戶體驗資料的標準化框架。 Experience Platform運用XDM架構，以一致且可重複使用的方式來描述資料結構。

當資料擷取至平台時，該資料的結構會對應至XDM架構，並儲存在資料湖中作為資料集的一 **部分**。 每個資料集的中繼資料都由目錄服務追蹤，目錄服務包括資料集所遵循的XDM架構參考。

有關XDM系統的更多一般資訊，請參閱 [XDM系統概述](../xdm/home.md)。

### 資料擷取

Experience Platform會從多個來源擷取資料，並將記錄保留為資料湖中的資料集。 目錄會追蹤這些資料集的中繼資料，不論其來源或擷取方法為何。

使用批次擷取方法時，Catalog也會追蹤批次檔案的其 **他中** 繼資料。 批次是多個資料單位，由一或多個要作為一個單位進行內嵌的檔案所組成。目錄會追蹤這些批次檔案的中繼資料，以及擷取後保留的資料集。 批次中繼資料包含成功擷取記錄的數目相關資訊，以及任何失敗記錄和相關的錯誤訊息。

如需詳細 [資訊，請參閱資料擷取](../ingestion/home.md) 概觀。

## 目錄物件

如上節所述，目錄會追蹤其他平台服務所使用之數種資源和作業的中繼資料。 Catalog會維護其自己的「物件」儲存，以封裝此中繼資料。 目錄物件是平台資料的可查詢表示法，可讓您搜尋、監視和標示資料，而不需存取資料本身。

下表概述目錄支援的不同對象類型：

| 物件 | API端點 | 定義 |
|---|---|---|
| 帳戶 | `/accounts` | 建立源連接時，必須提供驗證憑據。 帳戶代表用來建立特定類型連線的驗證憑證集合。 每個連接都有一組唯一參數，這些參數由目錄保存，並在Azure密鑰儲存庫中加以保護。 |
| 批次 | `/batches` | 批次是多個資料單位，由一或多個要作為一個單位進行內嵌的檔案所組成。Catalog中的批處理對象概述了批處理的接收度量（如已處理的記錄數或磁碟上的大小），並可能包括資料集、視圖和受批處理操作影響的其他資源的連結。 |
| 連線 | `/connections` | 連接是源連接器的單個實例，對於您的組織是唯一的，並且使用連接器類型的適當驗證憑據進行配置。 |
| 連接器 | `/connectors` | 連接器可定義來源連線如何從其他Adobe應用程式（例如Adobe Analytics和Adobe Audience Manager）、協力廠商雲端儲存來源（例如Azure Blob、Amazon S3、FTP伺服器和SFTP伺服器）以及協力廠商CRM系統（例如Microsoft Dynamics和Salesforce）收集資料。 |
| 資料集 | `/dataSets` | 資料集是用於收集資料（通常是表格）的儲存和管理結構，其中包含結構（欄）和欄（列）。 如需詳細 [資訊，請參閱資料集](./datasets/overview.md) 概觀。 |
| 資料集檔案 | `/datasetFiles` | 資料集檔案代表已儲存在平台上的資料區塊。 作為常值檔案的記錄，您可以在這些位置找到檔案的大小、檔案包含的記錄數，以及對接收檔案的批的引用。 |

## 後續步驟

本檔案介紹目錄服務，以及它在更廣泛的Experience Platform中的運作方式。 如需與 [該目錄API的不同端點互動的步驟](api/getting-started.md) ，請參閱目錄開發人員指南。 建議您也參閱「目錄」資料篩 [選指南](api/filter-data.md) ，以遵循限制API回應中傳回資料的最佳實務。