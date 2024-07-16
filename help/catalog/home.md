---
keywords: Experience Platform；首頁；熱門主題；目錄服務；目錄；目錄服務；資料位置；資料位置；資料管理；資料管理；譜系；譜系；目錄；啟用資料集
solution: Experience Platform
title: 目錄服務總覽
description: 目錄服務是在 Adobe Experience Platform 內針對資料位置和連結的記錄系統。雖然擷取至 Experience Platform 中的所有資料都以檔案和目錄形式儲存在資料湖中，但是為了查詢和監控目的，目錄會留存這些檔案和目錄的中繼資料和說明。
exl-id: ef0c173b-607b-41b8-8676-c54ae9472e23
source-git-commit: 0ebe9eadb1bce6252b43a50af009ce1b0f6e5d6e
workflow-type: tm+mt
source-wordcount: '694'
ht-degree: 8%

---

# [!DNL Catalog Service] 概觀

[!DNL Catalog Service]是Adobe Experience Platform中資料位置和歷程的記錄系統。 雖然所有擷取至[!DNL Experience Platform]的資料都以檔案和目錄的形式儲存在[!DNL Data Lake]中，但[!DNL Catalog]仍保留這些檔案和目錄的中繼資料和描述，以供查閱和監視。

簡言之，[!DNL Catalog]充當中繼資料存放區或「目錄」，您可在[!DNL Experience Platform]中找到有關您資料的資訊。 您可以使用[!DNL Catalog]來回答下列問題：

* 我的資料位於何處？
* 這些資料處於哪個處理階段？
* 哪些系統或程式對我的資料採取行動？
* 已成功處理多少資料？
* 處理期間發生哪些錯誤？

[!DNL Catalog]提供RESTful API，可讓您使用基本CRUD作業以程式設計方式管理[!DNL Platform]中繼資料。 如需詳細資訊，請參閱[目錄開發人員指南](api/getting-started.md)。

## [!DNL Catalog]和[!DNL Experience Platform]服務

[!DNL Catalog Service]個追蹤的資源已由多個[!DNL Experience Platform]服務使用。 為了充分利用[!DNL Catalog's]功能，建議您熟悉這些服務以及它們如何與[!DNL Catalog]互動。

### [!DNL Experience Data Model] (XDM)系統

[!DNL Experience Data Model] (XDM)系統是[!DNL Platform]用來組織客戶體驗資料的標準化架構。 [!DNL Experience Platform]運用XDM結構描述，以一致且可重複使用的方式描述資料結構。

將資料內嵌至[!DNL Platform]時，該資料的結構會對映至XDM結構描述，並作為資料集的一部分儲存在[!DNL Data Lake]中。 [!DNL Catalog Service]會追蹤每個資料集的中繼資料，其中包括資料集所符合之XDM結構描述的參考。

如需XDM系統的一般資訊，請參閱[XDM系統概覽](../xdm/home.md)。

### [!DNL Data Ingestion]

[!DNL Experience Platform]從多個來源擷取資料，並將記錄儲存為[!DNL Data Lake]內的資料集。 [!DNL Catalog]會追蹤這些資料集的中繼資料，不論資料集的來源或擷取方法為何。

使用批次擷取方法時，[!DNL Catalog]也會追蹤批次檔案的其他中繼資料。 批次是資料單位，由一或多個要作為單一單位內嵌的檔案組成。 [!DNL Catalog]會追蹤這些批次檔案的中繼資料，及其在擷取後持續存在的資料集。 批次中繼資料包含有關成功擷取的記錄數，以及任何失敗記錄和關聯的錯誤訊息的資訊。

如需詳細資訊，請參閱[資料擷取概觀](../ingestion/home.md)。

## [!DNL Catalog]個物件

如上一節所述，[!DNL Catalog]會追蹤其他[!DNL Platform]服務使用的幾種資源與作業的中繼資料。 [!DNL Catalog]會維護自己封裝此中繼資料的「物件」存放區。 [!DNL Catalog]物件是[!DNL Platform]資料的可查詢表示法，可讓您搜尋、監視和標示您的資料，而不需要存取資料本身。

下表概述[!DNL Catalog]支援的不同物件型別：

| 物件 | API端點 | 定義 |
|---|---|---|
| 批次 | `/batches` | 批次是資料單位，由一或多個要作為單一單位內嵌的檔案組成。 [!DNL Catalog]中的批次物件概述批次的擷取量度（例如處理的記錄數或磁碟大小），也可能包含資料集、檢視和其他受批次作業影響的資源的連結。 |
| 資料集 | `/dataSets` | 資料集是一種儲存和管理結構，用於收集包含方案（欄）和欄位（列）的資料（通常是表格）。 如需詳細資訊，請參閱[資料集總覽](./datasets/overview.md)。 |
| 資料集檔案 | `/datasetFiles` | 資料集檔案代表儲存在[!DNL Platform]上的資料區塊。 作為常值檔案的記錄，您可以在這裡找到檔案的大小、檔案包含的記錄數，以及對擷取檔案之批次的參照。 |

## 後續步驟

本檔案提供[!DNL Catalog Service]的簡介，以及它在[!DNL Experience Platform]較大範圍內的運作方式。 請參閱[[!DNL Catalog] 開發人員指南](api/getting-started.md)，以瞭解與該[!DNL Catalog] API的不同端點互動的步驟。 建議您參考有關[篩選目錄資料](api/filter-data.md)的指南，以遵循限制API回應中傳回資料的最佳實務。
