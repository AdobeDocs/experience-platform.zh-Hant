---
title: Adobe Experience Platform 發行說明
description: 2021年3月31日的Experience Platform發行說明。
doc-type: release notes
last-update: March 31, 2021
author: ens72741
translation-type: tm+mt
source-git-commit: 8d4270d9168a570fcf92ba60d70dbc8e9af98136
workflow-type: tm+mt
source-wordcount: '244'
ht-degree: 9%

---


# Adobe Experience Platform 發行說明

**發行日期：2021 年 3 月 31 日**

Adobe Experience Platform 現有功能更新：

- [[!DNL Sources]](#sources)

## [!DNL Sources] {#sources}

Adobe Experience Platform可以從外部來源收集資料，同時允許您使用平台服務來建構、標籤和增強該資料。 您可以從多種來源收集資料，例如Adobe應用程式、雲端儲存空間、協力廠商軟體和您的CRM系統。

Experience Platform提供REST風格的API和互動式UI，讓您輕鬆地為各種資料提供者設定來源連線。 這些源連接允許您驗證並連接到外部儲存系統和CRM服務、設定接收運行的時間，以及管理資料接收吞吐量。

2021年3月發行的Experience Platform包含下列來源更新：

| 功能 | 說明 |
| ------- | ----------- |
| Beta版來源正在推出 | 下列來源已從測試版提升至正式發行： <ul><li>[[!DNL MySQL]](../../sources/connectors/databases/mysql.md)</li><li>[[!DNL PostGres]](../../sources/connectors/databases/postgres.md)</li><li>[[!DNL Salesforce Service Cloud]](../../sources/connectors/customer-success/salesforce-service-cloud.md)</li><li>[[!DNL SFTP]](../../sources/connectors/cloud-storage/sftp.md)</li><li>[[!DNL Shopify]](../../sources/connectors/ecommerce/shopify.md)</li></ul> |
| 壓縮檔案擷取的API支援 | 您現在可以使用雲端儲存來源預覽並內嵌壓縮的JSON或分隔檔案。 如需詳細資訊，請參閱[使用API收集雲端儲存資料的教學課程。](../../sources/tutorials/api/collect/cloud-storage.md) |
| 遞歸檔案上傳的UI支援 | 您現在可以使用雲端儲存來源，以遞歸方式收錄整個資料夾。 在提取整個資料夾時，必須確保其內容共用相同的模式。 如需詳細資訊，請參閱UI](../../sources/tutorials/ui/dataflow/batch/cloud-storage.md)中的[設定雲端儲存連接器的資料流教學課程。 |

若要進一步瞭解來源，請參閱[來源概觀](../../sources/home.md)。
