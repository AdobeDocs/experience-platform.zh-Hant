---
keywords: Experience Platform;home；熱門主題；目錄服務；目錄服務；資料位置；資料管理；資料管理；世系；目錄；啟用資料集
solution: Experience Platform
title: 目錄服務概述
topic-legacy: overview
description: 目錄服務是Adobe Experience Platform境內資料位置和世系的記錄系統。 雖然所有吸收到Experience Platform中的資料都會以檔案和目錄的形式儲存在資料湖中，但目錄會保留這些檔案和目錄的中繼資料和說明，以供查閱和監控之用。
exl-id: ef0c173b-607b-41b8-8676-c54ae9472e23
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '805'
ht-degree: 5%

---

# [!DNL Catalog Service] 概觀

[!DNL Catalog Service] 是Adobe Experience Platform境內資料位置和世系記錄系統。雖然所有收錄到[!DNL Experience Platform]的資料都以檔案和目錄的形式儲存在[!DNL Data Lake]中，但[!DNL Catalog]會保留這些檔案和目錄的中繼資料和說明，以供查閱和監控之用。

簡單地說，[!DNL Catalog]可當成中繼資料存放區或「目錄」，您可在[!DNL Experience Platform]中找到有關資料的資訊。 您可以使用[!DNL Catalog]回答下列問題：

* 我的資料位於何處？
* 這些資料處理的階段是什麼？
* 哪些系統或流程對我的資料有作用？
* 已成功處理多少資料？
* 處理期間發生了哪些錯誤？

[!DNL Catalog] 提供REST風格的API，可讓您使用基本的CRUD作業，以程 [!DNL Platform] 式設計方式管理中繼資料。如需詳細資訊，請參閱[目錄開發人員指南](api/getting-started.md)。

## [!DNL Catalog] 和服 [!DNL Experience Platform] 務

[!DNL Catalog Service]追蹤的資源由多個[!DNL Experience Platform]服務使用。 為充份運用[!DNL Catalog's]功能，建議您熟悉這些服務，以及它們與[!DNL Catalog]的互動方式。

### [!DNL Experience Data Model] (XDM)系統

[!DNL Experience Data Model] (XDM)系統是組織客戶體驗資料的 [!DNL Platform] 標準化架構。[!DNL Experience Platform] 利用XDM架構，以一致且可重複使用的方式來描述資料結構。

當資料被擷取至[!DNL Platform]時，該資料的結構會映射至XDM架構，並儲存在[!DNL Data Lake]中，作為資料集的一部分。 每個資料集的元資料由[!DNL Catalog Service]跟蹤，該包括對資料集符合的XDM模式的引用。

有關XDM系統的更多一般資訊，請參閱[XDM系統概述](../xdm/home.md)。

### [!DNL Data Ingestion]

[!DNL Experience Platform] 從多個來源擷取資料，並將記錄保留為資料集 [!DNL Data Lake]。[!DNL Catalog] 追蹤這些資料集的中繼資料，不論其來源或擷取方法為何。

使用批次擷取方法時，[!DNL Catalog]也會追蹤批次檔案的其他中繼資料。 批次是多個資料單位，由一或多個要作為一個單位進行內嵌的檔案所組成。[!DNL Catalog] 追蹤這些批次檔案的中繼資料，以及擷取後保留的資料集。批次中繼資料包含成功擷取記錄的數目相關資訊，以及任何失敗記錄和相關的錯誤訊息。

如需詳細資訊，請參閱[資料擷取概觀](../ingestion/home.md)。

## [!DNL Catalog] 對象

如上節所述，[!DNL Catalog]會追蹤其他[!DNL Platform]服務使用的數種資源和作業的中繼資料。 [!DNL Catalog] 維護其自己的「物件」儲存，可封裝此中繼資料。[!DNL Catalog] 物件是資料的可 [!DNL Platform] 查詢表示，可讓您搜尋、監視和標示資料，而不需存取資料本身。

下表概述[!DNL Catalog]支援的不同物件類型：

| 物件 | API端點 | 定義 |
|---|---|---|
| 帳戶 | `/accounts` | 建立源連接時，必須提供驗證憑據。 帳戶代表用來建立特定類型連線的驗證憑證集合。 每個連接都有一組唯一參數，這些參數由[!DNL Catalog]保存，並在[!DNL Azure Key Vault]中保護。 |
| 批次 | `/batches` | 批次是多個資料單位，由一或多個要作為一個單位進行內嵌的檔案所組成。[!DNL Catalog]中的批處理對象概述了批處理的提取度量（如已處理的記錄數或磁碟上的大小），還可能包括資料集、視圖和受批處理操作影響的其他資源的連結。 |
| Connection | `/connections` | 連接是源連接器的單個實例，對於您的組織是唯一的，並且使用連接器類型的適當驗證憑據進行配置。 |
| 連接器 | `/connectors` | 連接器定義來源連線如何從其他Adobe應用程式(例如Adobe Analytics和Adobe Audience Manager)、協力廠商雲端儲存來源（例如[!DNL Azure Blob]、[!DNL Amazon S3]、FTP伺服器和SFTP伺服器）以及協力廠商CRM系統（例如[!DNL Microsoft Dynamics]和[!DNL Salesforce]）收集資料。 |
| 資料集 | `/dataSets` | 資料集是用於收集資料（通常是表格）的儲存和管理結構，其中包含結構（欄）和欄（列）。 如需詳細資訊，請參閱[資料集綜覽](./datasets/overview.md)。 |
| 資料集檔案 | `/datasetFiles` | 資料集檔案代表已儲存在[!DNL Platform]上的資料區塊。 作為常值檔案的記錄，您可以在這些位置找到檔案的大小、檔案包含的記錄數，以及對接收檔案的批的引用。 |

## 後續步驟

本檔案介紹了[!DNL Catalog Service]及其在[!DNL Experience Platform]更大範圍內的功能。 如需與該[!DNL Catalog] API的不同端點互動的步驟，請參閱[[!DNL Catalog] 開發人員指南](api/getting-started.md)。 建議您也參閱[篩選目錄資料](api/filter-data.md)指南，以遵循限制API回應中傳回資料的最佳實務。
