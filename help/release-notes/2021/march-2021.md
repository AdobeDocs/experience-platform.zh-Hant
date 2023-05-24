---
title: Adobe Experience Platform發行說明2021年3月
description: 2021年3月為Adobe Experience Platform發佈的說明。
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

[!DNL Data Prep] 允許資料工程師將資料映射到體驗資料模型(XDM)並驗證資料。

| 功能 | 說明 |
| ------- | ----------- |
| `add_to_array` 函數 | 已更新功能，以支援陣列作為參數。 |
| `to_array` 函數 | 已更新功能，以支援對象作為參數。 |

有關詳細資訊，請參閱 [[!DNL Data Prep] 概述](../../data-prep/home.md)。

## 分段服務 {#segmentation}

Adobe Experience Platform分段服務提供用戶介面和REST風格的API，使您能夠生成分段並從您的 [!DNL Real-Time Customer Profile] 資料。 這些段在 [!DNL Platform]使任何Adobe應用程式都可輕鬆訪問。

[!DNL Segmentation Service] 通過描述區分客戶群中可銷售人員組的標準來定義特定配置檔案子集。 段可以基於記錄資料（如人口統計資訊）或表示客戶與您品牌的交互的時間序列事件。

**新功能**

| 功能 | 說明 |
| ------- | ----------- |
| (Beta)邊緣分割 | 邊緣分割即時評估段，這允許使用相同的頁面和下一頁個性化使用案例。 有關邊緣分割的詳細資訊，請參閱 [分段UI概述](../../segmentation/ui/overview.md)。 |
| (Beta)增量分段 | 將在批處理分段中評估的現有段定義的新鮮度提高到最多一小時。 |

有關 [!DNL Segmentation Service]，請參閱 [分段概述](../../segmentation/home.md)。

## [!DNL Sources] {#sources}

Adobe Experience Platform可以從外部源接收資料，同時允許您使用平台服務來構建、標籤和增強資料。 您可以從多種來源(如Adobe應用程式、基於雲的儲存、第三方軟體和您的CRM系統)接收資料。

Experience Platform提供REST風格的API和互動式UI，讓您能夠輕鬆地為各種資料提供程式設定源連接。 通過這些源連接，您可以驗證並連接到外部儲存系統和CRM服務，設定接收運行時間，並管理資料接收吞吐量。

| 功能 | 說明 |
| ------- | ----------- |
| Beta源移至GA | 已將以下源從beta升級為GA: <ul><li>[[!DNL MySQL]](../../sources/connectors/databases/mysql.md)</li><li>[[!DNL PostGres]](../../sources/connectors/databases/postgres.md)</li><li>[[!DNL Salesforce Service Cloud]](../../sources/connectors/customer-success/salesforce-service-cloud.md)</li><li>[[!DNL SFTP]](../../sources/connectors/cloud-storage/sftp.md)</li><li>[[!DNL Shopify]](../../sources/connectors/ecommerce/shopify.md)</li></ul> |
| API支援壓縮檔案接收 | 您現在可以使用雲儲存源預覽和接收壓縮的JSON或分隔檔案。 有關詳細資訊，請參見上的教程 [使用API收集雲儲存資料](../../sources/tutorials/api/collect/cloud-storage.md)。 |
| 遞歸檔案上載的UI支援 | 現在，使用雲儲存源時可以遞歸地接收整個資料夾。 在插入整個資料夾時，必須確保其內容共用同一架構。 有關詳細資訊，請參見上的教程 [為UI中的雲儲存連接器配置資料流](../../sources/tutorials/ui/dataflow/batch/cloud-storage.md)。 |

要瞭解有關源的詳細資訊，請參閱 [源概述](../../sources/home.md)。
