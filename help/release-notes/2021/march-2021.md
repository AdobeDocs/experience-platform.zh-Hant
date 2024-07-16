---
title: Adobe Experience Platform 發行說明 (2021 年 3 月)
description: Adobe Experience Platform 2021 年 3 月的發行說明。
doc-type: release notes
last-update: March 31, 2021
author: ens72741
exl-id: 027cd7b1-1651-4939-bc97-968a41824117
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '427'
ht-degree: 37%

---

# Adobe Experience Platform 發行說明

**發行日期： 2021年3月31日**

Adobe Experience Platform 現有功能的更新：

- [[!DNL Data Prep]](#data-prep)
- [[!DNL Segmentation Service]](#segmentation)
- [[!DNL Sources]](#sources)

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep]可讓資料工程師對應、轉換及驗證與Experience Data Model (XDM)之間的資料。

| 功能 | 說明 |
| ------- | ----------- |
| `add_to_array`函式 | 更新支援陣列作為引數的功能。 |
| `to_array`函式 | 更新支援物件作為引數的功能。 |

如需詳細資訊，請參閱[[!DNL Data Prep] 總覽](../../data-prep/home.md)。

## Segmentation Service {#segmentation}

Adobe Experience Platform Segmentation Service提供使用者介面和RESTful API，可讓您建立區段，並從[!DNL Real-Time Customer Profile]資料產生對象。 這些區段是在[!DNL Platform]上集中設定和維護，讓任何Adobe應用程式都能輕鬆存取。

[!DNL Segmentation Service] 會說明區分客戶群中可行銷的一群人的標準，從而定義設定檔的特定子集。區段的基礎可能是記錄資料 (例如人口統計資訊) 或表示客戶與您的品牌互動的時間序列事件。

**新功能**

| 功能 | 說明 |
| ------- | ----------- |
| (Beta) Edge區段 | Edge區段會即時評估區段，以允許相同頁面和下一頁個人化使用案例。 您可以在[區段UI總覽](../../segmentation/ui/overview.md)中找到邊緣區段的詳細資訊。 |
| (Beta)增量細分 | 將批次分段中評估之現有區段定義的更新時間提高至最多一小時。 |

如需有關 [!DNL Segmentation Service] 的詳細資訊，請參閱[分段概觀](../../segmentation/home.md)。

## [!DNL Sources] {#sources}

Adobe Experience Platform可內嵌來自外部來源的資料，同時允許您使用Platform服務來建構、加標籤及增強這些資料。 您可以從各種來源擷取資料，例如 Adob&#x200B;&#x200B;e 應用程式、雲端型儲存空間、協力廠商軟體和 CRM 系統。

Experience Platform 可提供 RESTful API 和互動式 UI，可讓您輕鬆為各種資料提供者設定來源連線。這些來源連線可讓您進行驗證並連線到外部儲存系統和 CRM 服務、設定擷取執行的時間並管理資料擷取輸送量。

| 功能 | 說明 |
| ------- | ----------- |
| Beta來源移至GA | 下列來源已從Beta版升級至GA版： <ul><li>[[!DNL MySQL]](../../sources/connectors/databases/mysql.md)</li><li>[[!DNL PostGres]](../../sources/connectors/databases/postgres.md)</li><li>[[!DNL Salesforce Service Cloud]](../../sources/connectors/customer-success/salesforce-service-cloud.md)</li><li>[[!DNL SFTP]](../../sources/connectors/cloud-storage/sftp.md)</li><li>[[!DNL Shopify]](../../sources/connectors/ecommerce/shopify.md)</li></ul> |
| 壓縮檔案擷取的API支援 | 您現在可以使用雲端儲存空間來源預覽及擷取壓縮的JSON或分隔檔案。 如需詳細資訊，請參閱[使用API收集雲端儲存空間資料的教學課程](../../sources/tutorials/api/collect/cloud-storage.md)。 |
| UI支援遞回檔案上傳 | 您現在可以在使用雲端儲存空間來源時，遞回擷取整個資料夾。 擷取整個資料夾時，您必須確保其內容共用相同的結構描述。 如需詳細資訊，請參閱有關[在UI](../../sources/tutorials/ui/dataflow/batch/cloud-storage.md)中為雲端儲存聯結器設定資料流的教學課程。 |

若要深入瞭解來源，請參閱[來源概觀](../../sources/home.md)。
