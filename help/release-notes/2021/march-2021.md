---
title: Adobe Experience Platform發行說明2021年3月
description: 2021年3月Adobe Experience Platform發行說明。
doc-type: release notes
last-update: March 31, 2021
author: ens72741
exl-id: 027cd7b1-1651-4939-bc97-968a41824117
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '425'
ht-degree: 6%

---

# Adobe Experience Platform 發行說明

**發行日期：2021 年 3 月 31 日**

Adobe Experience Platform 現有功能更新：

- [[!DNL Data Prep]](#data-prep)
- [[!DNL Segmentation Service]](#segmentation)
- [[!DNL Sources]](#sources)

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] 可讓資料工程師將資料對應、轉換及驗證至Experience Data Model(XDM)。

| 功能 | 說明 |
| ------- | ----------- |
| `add_to_array` 函數 | 更新支援陣列作為參數的功能。 |
| `to_array` 函數 | 更新功能以支援物件作為參數。 |

如需詳細資訊，請參閱 [[!DNL Data Prep] 概述](../../data-prep/home.md).

## 分段服務 {#segmentation}

Adobe Experience Platform劃分服務提供使用者介面和RESTful API，可讓您建立區段，並從 [!DNL Real-Time Customer Profile] 資料。 這些區段是在 [!DNL Platform]，讓任何Adobe應用程式都能輕鬆存取。

[!DNL Segmentation Service] 會透過說明區分客戶群中可行銷人員群組的條件，來定義特定設定檔子集。 區段可以根據記錄資料（例如人口統計資訊）或代表客戶與您品牌互動的時間序列事件。

**新功能**

| 功能 | 說明 |
| ------- | ----------- |
| （測試版）邊緣劃分 | 邊緣區段會即時評估區段，以允許使用相同的頁面和下一頁個人化使用案例。 如需邊緣分段的詳細資訊，請參閱 [區段UI概觀](../../segmentation/ui/overview.md). |
| （測試版）增量細分 | 將批次分段中評估的現有區段定義的時效性提高至最多一小時。 |

如需 [!DNL Segmentation Service]，請參閱 [區段概觀](../../segmentation/home.md).

## [!DNL Sources] {#sources}

Adobe Experience Platform可內嵌來自外部來源的資料，同時允許您使用Platform服務來建構、加標籤及增強該資料。 您可以內嵌來自各種來源的資料，例如Adobe應用程式、雲端儲存、協力廠商軟體和您的CRM系統。

Experience Platform提供RESTful API和互動式UI，讓您輕鬆為各種資料提供者設定來源連線。 這些源連接允許您驗證並連接到外部儲存系統和CRM服務、設定獲取運行時間以及管理資料獲取吞吐量。

| 功能 | 說明 |
| ------- | ----------- |
| 測試版來源轉至GA | 下列來源已從測試版提升為正式發行： <ul><li>[[!DNL MySQL]](../../sources/connectors/databases/mysql.md)</li><li>[[!DNL PostGres]](../../sources/connectors/databases/postgres.md)</li><li>[[!DNL Salesforce Service Cloud]](../../sources/connectors/customer-success/salesforce-service-cloud.md)</li><li>[[!DNL SFTP]](../../sources/connectors/cloud-storage/sftp.md)</li><li>[[!DNL Shopify]](../../sources/connectors/ecommerce/shopify.md)</li></ul> |
| 壓縮檔案擷取的API支援 | 您現在可以使用雲端儲存來源預覽並內嵌壓縮的JSON或分隔檔案。 如需詳細資訊，請參閱 [使用API收集雲端儲存空間資料](../../sources/tutorials/api/collect/cloud-storage.md). |
| 遞歸檔案上傳的UI支援 | 現在，使用雲儲存源時，您可以遞回內嵌整個資料夾。 擷取整個資料夾時，您必須確保其內容共用相同的結構。 如需詳細資訊，請參閱 [在UI中為雲儲存連接器配置資料流](../../sources/tutorials/ui/dataflow/batch/cloud-storage.md). |

若要進一步了解來源，請參閱 [來源概觀](../../sources/home.md).
