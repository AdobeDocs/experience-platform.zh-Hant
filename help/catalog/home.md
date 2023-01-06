---
keywords: Experience Platform；首頁；熱門主題；目錄服務；目錄服務；資料位置；資料位置；資料管理；資料管理；世系；世系；目錄；啟用資料集
solution: Experience Platform
title: 目錄服務概述
description: 目錄服務是Adobe Experience Platform內用於資料位置和歷程的記錄系統。 雖然所有擷取到Experience Platform中的資料都會以檔案和目錄的形式儲存在Data Lake中，但「目錄」會保留這些檔案和目錄的中繼資料和說明，以供查閱和監控之用。
exl-id: ef0c173b-607b-41b8-8676-c54ae9472e23
source-git-commit: 74867f56ee13430cbfd9083a916b7167a9a24c01
workflow-type: tm+mt
source-wordcount: '805'
ht-degree: 5%

---

# [!DNL Catalog Service] 概覽

[!DNL Catalog Service] 是Adobe Experience Platform內用於資料位置和世系的記錄系統。 而所有擷取至 [!DNL Experience Platform] 儲存於 [!DNL Data Lake] 作為檔案和目錄， [!DNL Catalog] 保存這些檔案和目錄的元資料和說明，以用於查找和監視。

簡言之， [!DNL Catalog] 可做為中繼資料存放區或「目錄」，您可在其中找到資料的相關資訊 [!DNL Experience Platform]. 您可以使用 [!DNL Catalog] 回答下列問題：

* 我的資料位於何處？
* 這些資料是在哪個處理階段？
* 哪些系統或程式對我的資料有作用？
* 已成功處理多少資料？
* 處理期間發生什麼錯誤？

[!DNL Catalog] 提供RESTful API，可讓您以程式設計方式管理 [!DNL Platform] 使用基本CRUD操作的中繼資料。 請參閱 [目錄開發人員指南](api/getting-started.md) 以取得更多資訊。

## [!DNL Catalog] 和 [!DNL Experience Platform] 服務

資源 [!DNL Catalog Service] 多個使用磁軌 [!DNL Experience Platform] 服務。 為了充分利用 [!DNL Catalog's] 功能，建議您熟悉這些服務，以及它們與 [!DNL Catalog].

### [!DNL Experience Data Model] (XDM)系統

[!DNL Experience Data Model] (XDM)系統是透過 [!DNL Platform] 組織客戶體驗資料。 [!DNL Experience Platform] 運用XDM結構，以一致且可重複使用的方式說明資料結構。

資料擷取至時 [!DNL Platform]，則該資料的結構會對應至XDM架構，並儲存在 [!DNL Data Lake] 做為資料集的一部分。 每個資料集的中繼資料由 [!DNL Catalog Service]，包含對資料集符合之XDM架構的參考。

如需XDM系統的更一般資訊，請參閱 [XDM系統概觀](../xdm/home.md).

### [!DNL Data Ingestion]

[!DNL Experience Platform] 從多個來源擷取資料，並將記錄保存為資料集 [!DNL Data Lake]. [!DNL Catalog] 追蹤這些資料集的中繼資料，無論其來源或擷取方法為何。

使用批次內嵌方法時， [!DNL Catalog] 也會追蹤批次檔案的其他中繼資料。 批次是多個資料單位，由一或多個要作為一個單位進行內嵌的檔案所組成。[!DNL Catalog] 追蹤這些批次檔案的中繼資料，以及擷取後保存的資料集。 批次中繼資料包含成功內嵌記錄數的相關資訊，以及任何失敗記錄和相關的錯誤訊息。

請參閱 [資料擷取概觀](../ingestion/home.md) 以取得更多資訊。

## [!DNL Catalog] 物件

如前一節所述， [!DNL Catalog] 會追蹤其他使用的多種資源和作業的中繼資料 [!DNL Platform] 服務。 [!DNL Catalog] 維護自己儲存的「對象」，這些對象會封裝此元資料。 [!DNL Catalog] 對象是可查詢的表示 [!DNL Platform] 資料，讓您無需存取資料本身即可搜尋、監控及標示資料。

下表概述了支援的不同對象類型 [!DNL Catalog]:

| 物件 | API端點 | 定義 |
|---|---|---|
| 帳戶 | `/accounts` | 建立源連接時，必須提供身份驗證憑據。 帳戶代表用來建立特定類型連線的驗證憑證集合。 每個連線都有一組唯一參數，由 [!DNL Catalog] 和 [!DNL Azure Key Vault]. |
| 批次 | `/batches` | 批次是多個資料單位，由一或多個要作為一個單位進行內嵌的檔案所組成。中的批處理對象 [!DNL Catalog] 概述批次的擷取量度（例如已處理的記錄數或磁碟大小），並可能包含受批次操作影響的資料集、檢視和其他資源的連結。 |
| Connection | `/connections` | 連線是來源連接器的單一例項，對您的組織來說是唯一的，並使用連接器類型的適當驗證憑證進行設定。 |
| 連接器 | `/connectors` | 連接器定義來源連線如何從其他Adobe應用程式(例如Adobe Analytics和Adobe Audience Manager)、第三方雲端儲存來源(例如 [!DNL Azure Blob], [!DNL Amazon S3]、FTP伺服器和SFTP伺服器)以及協力廠商CRM系統(例如 [!DNL Microsoft Dynamics] 和 [!DNL Salesforce])。 |
| 資料集 | `/dataSets` | 資料集是用於收集資料（通常是表格）的儲存和管理結構，其中包含結構（欄）和欄位（列）。 請參閱 [資料集概述](./datasets/overview.md) 以取得更多資訊。 |
| 資料集檔案 | `/datasetFiles` | 資料集檔案代表儲存在的資料區塊 [!DNL Platform]. 作為常值檔案的記錄，您可以在這些位置找到檔案的大小、其包含的記錄數，以及對擷取檔案的批次的參考。 |

## 後續步驟

本檔案介紹 [!DNL Catalog Service] 以及它在 [!DNL Experience Platform]. 請參閱 [[!DNL Catalog] 開發人員指南](api/getting-started.md) 以了解與其不同端點互動的步驟 [!DNL Catalog] API。 建議您也參閱 [篩選目錄資料](api/filter-data.md) 以遵循限制API回應中傳回資料的最佳實務。
