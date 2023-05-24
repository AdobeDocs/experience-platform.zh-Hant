---
keywords: Experience Platform；首頁；熱門主題；目錄服務；目錄服務；資料位置；資料位置；資料管理；沿襲；沿襲；目錄；啟用資料集
solution: Experience Platform
title: 目錄服務概述
description: 目錄服務是Adobe Experience Platform內資料位置和沿襲的記錄系統。 雖然所有被攝取到Experience Platform中的資料都作為檔案和目錄儲存在資料湖中，但目錄保存這些檔案和目錄的元資料和說明，以便進行查找和監視。
exl-id: ef0c173b-607b-41b8-8676-c54ae9472e23
source-git-commit: 74867f56ee13430cbfd9083a916b7167a9a24c01
workflow-type: tm+mt
source-wordcount: '805'
ht-degree: 5%

---

# [!DNL Catalog Service] 概覽

[!DNL Catalog Service] 是Adobe Experience Platform內資料位置和世系的記錄系統。 所有被攝入的資料 [!DNL Experience Platform] 儲存在 [!DNL Data Lake] 作為檔案和目錄， [!DNL Catalog] 保存這些檔案和目錄的元資料和說明，以便進行查找和監視。

簡單說， [!DNL Catalog] 充當元資料儲存或「目錄」，在此您可以查找有關資料的資訊 [!DNL Experience Platform]。 您可以使用 [!DNL Catalog] 回答以下問題：

* 我的資料在哪？
* 這些資料處理到什麼階段？
* 哪些系統或進程對我的資料有作用？
* 已成功處理多少資料？
* 處理過程中發生了哪些錯誤？

[!DNL Catalog] 提供了REST風格的API，允許您以寫程式方式管理 [!DNL Platform] 元資料。 查看 [目錄開發人員指南](api/getting-started.md) 的子菜單。

## [!DNL Catalog] 和 [!DNL Experience Platform] 服務

資源 [!DNL Catalog Service] 多個磁軌使用 [!DNL Experience Platform] 服務。 為了充分利用 [!DNL Catalog's] 功能，建議您熟悉這些服務及其與 [!DNL Catalog]。

### [!DNL Experience Data Model] (XDM)系統

[!DNL Experience Data Model] (XDM)系統是標準化框架， [!DNL Platform] 組織客戶體驗資料。 [!DNL Experience Platform] 利用XDM架構以一致且可重複使用的方式描述資料結構。

當資料被攝入 [!DNL Platform]，該資料的結構將映射到XDM架構並儲存在 [!DNL Data Lake] 作為資料集的一部分。 每個資料集的元資料由 [!DNL Catalog Service]，包括對資料集符合的XDM架構的引用。

有關XDM系統的更多一般資訊，請參閱 [XDM系統概述](../xdm/home.md)。

### [!DNL Data Ingestion]

[!DNL Experience Platform] 從多個源中接收資料，並將記錄作為資料集保留在 [!DNL Data Lake]。 [!DNL Catalog] 跟蹤這些資料集的元資料，而不管其來源或接收方法如何。

使用批量攝取法時， [!DNL Catalog] 還跟蹤批處理檔案的其他元資料。 批次是多個資料單位，由一或多個要作為一個單位進行內嵌的檔案所組成。[!DNL Catalog] 跟蹤這些批處理檔案的元資料，以及接收後保留的資料集。 批處理元資料包括有關成功接收的記錄數以及所有失敗記錄和相關錯誤消息的資訊。

查看 [資料攝取概述](../ingestion/home.md) 的子菜單。

## [!DNL Catalog] 對象

如上節所述， [!DNL Catalog] 跟蹤其他資源和操作使用的多種資源和操作的元資料 [!DNL Platform] 服務。 [!DNL Catalog] 維護自己的「對象」儲存，這些對象封裝了此元資料。 [!DNL Catalog] 對象的可查詢表示 [!DNL Platform] 資料，使您可以搜索、監視和標籤資料，而無需訪問資料本身。

下表概述了支援的不同對象類型 [!DNL Catalog]:

| 物件 | API終結點 | 定義 |
|---|---|---|
| 帳戶 | `/accounts` | 建立源連接時，必須提供身份驗證憑據。 帳戶表示用於建立特定類型連接的身份驗證憑據的集合。 每個連接都具有一組由 [!DNL Catalog] 並以 [!DNL Azure Key Vault]。 |
| 批 | `/batches` | 批次是多個資料單位，由一或多個要作為一個單位進行內嵌的檔案所組成。中的批處理對象 [!DNL Catalog] 概述批處理的攝取度量（如處理的記錄數或磁碟大小），還可能包括到資料集、視圖和受批處理操作影響的其他資源的連結。 |
| Connection | `/connections` | 連接是源連接器的單個實例，它對您的組織是唯一的，並且使用連接器類型的相應身份驗證憑據進行配置。 |
| 連接器 | `/connectors` | 連接器定義源連接如何從其他Adobe應用程式(如Adobe Analytics和Adobe Audience Manager)、第三方雲儲存源(如 [!DNL Azure Blob]。 [!DNL Amazon S3]、FTP伺服器和SFTP伺服器)，以及第三方CRM系統(如 [!DNL Microsoft Dynamics] 和 [!DNL Salesforce])。 |
| 資料集 | `/dataSets` | 資料集是用於收集資料（通常是表）的儲存和管理構造，該資料集包含模式（列）和欄位（行）。 查看 [資料集概述](./datasets/overview.md) 的子菜單。 |
| 資料集檔案 | `/datasetFiles` | 資料集檔案表示已保存的資料塊 [!DNL Platform]。 作為文本檔案的記錄，您可以在這些記錄中找到檔案的大小、包含的記錄數以及對接收檔案的批的引用。 |

## 後續步驟

本檔案介紹了 [!DNL Catalog Service] 以及它在更大範圍內的作用 [!DNL Experience Platform]。 查看 [[!DNL Catalog] 開發者指南](api/getting-started.md) 與其不同端點交互的步驟 [!DNL Catalog] API。 建議您也參考上的指南 [篩選目錄資料](api/filter-data.md) 以遵循限制API響應中返回的資料的最佳做法。
