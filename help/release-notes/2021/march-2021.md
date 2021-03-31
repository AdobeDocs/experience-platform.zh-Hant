---
title: Adobe Experience Platform 發行說明
description: 2021年3月31日的Experience Platform發行說明。
doc-type: release notes
last-update: March 31, 2021
author: ens72741
translation-type: tm+mt
source-git-commit: 9b4395d423bbc62c8a1a9427ea91248a0f693794
workflow-type: tm+mt
source-wordcount: '422'
ht-degree: 7%

---


# Adobe Experience Platform 發行說明

**發行日期：2021 年 3 月 31 日**

Adobe Experience Platform 現有功能更新：

- [[!DNL Data Prep]](#data-prep)
- [[!DNL Segmentation Service]](#segmentation)
- [[!DNL Sources]](#sources)

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] 可讓資料工程師將資料對應、轉換及驗證資料與Experience Data Model(XDM)。

| 功能 | 說明 |
| ------- | ----------- |
| `add_to_array` 函數 | 更新功能，以支援陣列做為參數。 |
| `to_array` 函數 | 更新功能以支援物件做為參數。 |

如需詳細資訊，請參閱[[!DNL Data Prep] overview](../../data-prep/home.md)。

## 劃分服務 {#segmentation}

Adobe Experience Platform區段服務提供使用者介面和REST風格的API，可讓您建立區段並從您的[!DNL Real-time Customer Profile]資料產生觀眾。 這些區段是集中設定並維護在[!DNL Platform]上，讓任何Adobe應用程式都可輕鬆存取。

[!DNL Segmentation Service] 定義個人檔案的特定子集，方法是描述區分客戶群中有價人群的標準。區段可以根據記錄資料（例如人口統計資訊）或代表客戶與品牌互動的時間系列事件來劃分。

**新功能**

| 功能 | 說明 |
| ------- | ----------- |
| （測試版）邊緣區隔 | 邊緣區段會即時評估區段，允許相同頁面和下一頁個人化使用案例。 有關邊緣分段的詳細資訊，請參閱[分段UI概觀](../../segmentation/ui/overview.md)。 |
| （測試版）增量細分 | 將批次分段中評估的現有區段定義新鮮度提高至一小時。 |

如需[!DNL Segmentation Service]的詳細資訊，請參閱[區段概述](../../segmentation/home.md)。

## [!DNL Sources] {#sources}

Adobe Experience Platform可以從外部來源收集資料，同時允許您使用平台服務來建構、標籤和增強該資料。 您可以從多種來源收集資料，例如Adobe應用程式、雲端儲存空間、協力廠商軟體和您的CRM系統。

Experience Platform提供REST風格的API和互動式UI，讓您輕鬆地為各種資料提供者設定來源連線。 這些源連接允許您驗證並連接到外部儲存系統和CRM服務、設定接收運行的時間，以及管理資料接收吞吐量。

| 功能 | 說明 |
| ------- | ----------- |
| Beta版來源正在推出 | 下列來源已從測試版提升至正式發行： <ul><li>[[!DNL MySQL]](../../sources/connectors/databases/mysql.md)</li><li>[[!DNL PostGres]](../../sources/connectors/databases/postgres.md)</li><li>[[!DNL Salesforce Service Cloud]](../../sources/connectors/customer-success/salesforce-service-cloud.md)</li><li>[[!DNL SFTP]](../../sources/connectors/cloud-storage/sftp.md)</li><li>[[!DNL Shopify]](../../sources/connectors/ecommerce/shopify.md)</li></ul> |
| 壓縮檔案擷取的API支援 | 您現在可以使用雲端儲存來源預覽並內嵌壓縮的JSON或分隔檔案。 如需詳細資訊，請參閱[使用API收集雲端儲存資料的教學課程。](../../sources/tutorials/api/collect/cloud-storage.md) |
| 遞歸檔案上傳的UI支援 | 您現在可以使用雲端儲存來源，以遞歸方式收錄整個資料夾。 在提取整個資料夾時，必須確保其內容共用相同的模式。 如需詳細資訊，請參閱UI](../../sources/tutorials/ui/dataflow/batch/cloud-storage.md)中的[設定雲端儲存連接器的資料流教學課程。 |

若要進一步瞭解來源，請參閱[來源概觀](../../sources/home.md)。
