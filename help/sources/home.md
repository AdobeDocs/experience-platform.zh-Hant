---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Adobe Experience Platform來源連接器概觀
topic: overview
translation-type: tm+mt
source-git-commit: 492adad9b38c8850130931d3d393f28c67057d07
workflow-type: tm+mt
source-wordcount: '746'
ht-degree: 0%

---


# 來源連接器概觀

Adobe Experience Platform可讓您從外部來源擷取資料，同時提供您使用平台服務來建構、標示及增強傳入資料的能力。 您可以從多種來源（例如Adobe應用程式、雲端儲存空間、資料庫等）擷取資料。

Experience Platform提供REST風格的API和互動式UI，讓您輕鬆設定與各種資料提供者的來源連線。 這些來源連線可讓您驗證您的協力廠商系統、設定擷取執行的時間，以及管理資料擷取總處理能力。

借助Experience Platform，您可以集中管理從不同來源收集到的資料，並運用從中獲得的見解做更多事。

## 來源類型

Experience Platform中的來源可分為下列類別：

### Adobe應用程式

Experience Platform可讓您從其他Adobe應用程式擷取資料，包括Adobe Analytics、Adobe Audience Manager和Experience Platform Launch。 如需詳細資訊，請參閱下列相關檔案：

- [Adobe Audience Manager連接器概觀](connectors/adobe-applications/audience-manager.md)
- [在UI中建立Adobe Audience Manager來源連接器](./tutorials/ui/create/adobe-applications/audience-manager.md)
- [Adobe Analytics資料連接器概觀](connectors/adobe-applications/analytics.md)
- [在UI中建立Adobe Analytics來源連接器](./tutorials/ui/create/adobe-applications/analytics.md)
- [在UI中建立客戶屬性來源連接器](./tutorials/ui/create/adobe-applications/customer-attributes.md)

### 廣告

Experience Platform支援從協力廠商廣告系統擷取資料。 有關特定來源連接器的詳細資訊，請參閱下列相關檔案：

- [Google Ads連接器](connectors/advertising/ads.md)

### 雲端儲存空間

雲端儲存來源可將您自己的資料匯入平台，而不需下載、格式化或上傳。 收錄的資料可格式化為XDM JSON、XDM鑲木地板或分隔字元。 此程式的每個步驟都會使用使用者介面整合至Sources工作流程。 如需詳細資訊，請參閱下列相關檔案：

- [Azure Data Lake Storage Gen2連接器](connectors/cloud-storage/adls-gen2.md)
- [Azure Blob和Amazon S3連接器](connectors/cloud-storage/blob-s3.md)
- [Azure檔案儲存連接器](connectors/cloud-storage/azure-file-storage.md)
- [FTP和SFTP連接器](connectors/cloud-storage/ftp-sftp.md)
- [Google雲端儲存空間連接器](connectors/cloud-storage/google-cloud-storage.md)

### 客戶關係管理(CRM)

CRM系統提供的資料有助於建立客戶關係，進而建立忠誠度並推動客戶維繫。 Experience Platform可支援從Microsoft Dynamics 365和Salesforce擷取CRM資料。 如需詳細資訊，請參閱下列相關檔案：

- [Microsoft Dynamics連接器](connectors/crm/ms-dynamics.md)
- [Salesforce連接器](connectors/crm/salesforce.md)

### 客戶成功

Experience Platform可支援從協力廠商客戶成功應用程式擷取資料。 如需詳細資訊，請參閱下列相關檔案：

- [Salesforce Service Cloud連接器](connectors/customer-success/salesforce-service-cloud.md)
- [ServiceNow連接器](connectors/customer-success/servicenow.md)

### 資料庫

Experience Platform支援從協力廠商資料庫擷取資料。 有關特定來源連接器的詳細資訊，請參閱下列相關檔案：

- [Amazon Redshift連接器](connectors/databases/redshift.md)
- [Apache Hive on Azure HDInsights連接器](connectors/databases/hive.md)
- [Apache Spark on Azure HDInsights連接器](connectors/databases/spark.md)
- [Azure資料總管連接器](connectors/databases/data-explorer.md)
- [Azure Synapse Analytics連接器](connectors/databases/synapse-analytics.md)
- [Azure表格儲存連接器](connectors/databases/ats.md)
- [Google BigQuery連接器](connectors/databases/bigquery.md)
- [IBM DB2連接器](connectors/databases/ibm-db2.md)
- [MariaDB連接器](connectors/databases/mariadb.md)
- [Microsoft SQL Server連接器](connectors/databases/sql-server.md)
- [MySQL連接器](connectors/databases/mysql.md)
- [Oracle連接器](connectors/databases/oracle.md)
- [菲尼克斯連接器](connectors/databases/phoenix.md)
- [PostgreSQL連接器](connectors/databases/postgres.md)

### 行銷自動化

Experience Platform支援從協力廠商行銷自動化系統擷取資料。 有關特定來源連接器的詳細資訊，請參閱下列相關檔案：

- [HubSpot連接器](connectors/marketing-automation/hubspot.md)

### 付款

Experience Platform支援從協力廠商付款系統擷取資料。 有關特定來源連接器的詳細資訊，請參閱下列相關檔案：

- [PayPal連接器](connectors/payments/paypal.md)

### 通訊協定

Experience Platform支援從協力廠商通訊協定系統擷取資料。 有關特定來源連接器的詳細資訊，請參閱下列相關檔案：

- [通用OData連接器](connectors/protocols/odata.md)

## 資料擷取中的來源存取控制

您可在Adobe Admin Console中管理資料擷取來源的權限。 您可以透過特定產品設定檔 *的「權限* 」索引標籤來存取權限。 從「編 **輯權限** 」面板，您可以透過資料擷取功能表項目存取與來 *源相關的權* 限。 「檢 **視來源** 」權限授予對「目錄 *」頁籤中可用來源的只讀訪問權，並授予「瀏覽」頁籤中已驗證的源的只讀訪問權，而「管理來源******* 」權限授予讀取、建立、編輯和禁用源的完全訪問權限。

下表概述UI根據這些權限的不同組合而運作的方式：

| 權限層級 | 說明 |
| ---- | ----|
| **檢視來源** On | 授予對 *Catalog* （目錄）頁籤中每個源類型以及 *Browse*、 *Accounts*（帳戶）和 ** DataFlow（資料流）頁籤中的源的只讀訪問權。 |
| **管理來源** On | 除了 **View Sources中的函式外**，還授與對Catalog *中* Connect Sources *選項和Select Data***** Select BrowseConnect Option中函式的訪問權。 **Manage Sources** 也可讓您啟用或停用 *DataFlows* ，並編輯其排程。 |
| **關閉Sources** 並管 **理Sources** Off | 撤銷對來源的所有存取權。 |

如需透過「管理控制台」授予之可用權限（包括這四個來源）的詳細資訊，請參閱存 [取控制概觀](../access-control/home.md)。
