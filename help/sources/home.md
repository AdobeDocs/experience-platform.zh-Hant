---
keywords: Experience Platform；首頁；熱門主題；來源連接器；來源連接器；來源；資料來源；資料來源；資料來源；資料來源連線
solution: Experience Platform
title: 來源連接器概述
topic-legacy: overview
description: Adobe Experience Platform可讓您從外部來源擷取資料，同時使用Platform服務來建構、加標籤及增強傳入資料。 您可以從多種來源(如Adobe應用程式、雲儲存、資料庫等)內嵌資料。
exl-id: efdbed4d-5697-43ef-a47a-a8bcf0f13237
source-git-commit: 9c8f19e8b5259bcef526273addbd7711ef6082fb
workflow-type: tm+mt
source-wordcount: '979'
ht-degree: 0%

---

# 來源連接器概觀

Adobe Experience Platform可讓您從外部來源擷取資料，同時使用Platform服務來建構、加標籤及增強傳入資料。 您可以從多種來源(如Adobe應用程式、基於雲的儲存、資料庫和其他許多源)內嵌資料。

[!DNL Flow Service] 用於收集和集中Platform內各種不同來源的客戶資料。此服務提供使用者介面和RESTful API，讓您輕鬆設定與各種資料提供者的來源連線。 這些來源連線可讓您驗證您的協力廠商系統、設定擷取執行的時間，以及管理資料擷取吞吐量。

透過Experience Platform，您可以集中收集來自不同來源的資料，並利用從中獲得的見解執行更多工作。

## 來源類型

Experience Platform中的來源分為以下類別：

### Adobe應用程式

Experience Platform可從其他Adobe應用程式(包括Adobe Analytics、Adobe Audience Manager和[!DNL Experience Platform Launch])擷取資料。 如需詳細資訊，請參閱下列相關檔案：

- [Adobe Audience Manager connector概述](connectors/adobe-applications/audience-manager.md)
- [在UI中建立Adobe Audience Manager來源連線](./tutorials/ui/create/adobe-applications/audience-manager.md)
- [Adobe Analytics分類資料來源連線概觀](connectors/adobe-applications/classifications.md)
- [在UI中建立Adobe Analytics分類資料來源連線](./tutorials/ui/create/adobe-applications/classifications.md)
- [Adobe Analytics報表套裝資料來源連線概觀](connectors/adobe-applications/analytics.md)
- [在UI中建立Adobe Analytics來源連線](./tutorials/ui/create/adobe-applications/analytics.md)
- [在UI中建立客戶屬性來源連線](./tutorials/ui/create/adobe-applications/customer-attributes.md)
- [[!DNL Marketo Engage] 連接器概觀](connectors/adobe-applications/marketo/marketo.md)
- [在UI中建立 [!DNL Marketo Engage] 源連接](./tutorials/ui/create/adobe-applications/marketo.md)

### Advertising

Experience Platform支援從協力廠商廣告系統擷取資料。 有關特定源連接器的詳細資訊，請參閱以下相關文檔：

- [[!DNL Google AdWords]](connectors/advertising/ads.md) 連接器

### 雲端儲存空間

雲端儲存來源可將您自己的資料匯入Platform，而無須下載、格式化或上傳。 擷取的資料可格式化為XDM JSON、XDM Parquet或分隔字元。 程式的每個步驟都會使用使用者介面整合至來源工作流程中。 如需詳細資訊，請參閱下列相關檔案：

- [[!DNL Azure Data Lake Storage Gen2] 連接器](connectors/cloud-storage/adls-gen2.md)
- [[!DNL Azure Blob] 連接器](connectors/cloud-storage/blob.md)
- [[!DNL Amazon Kinesis] 連接器](connectors/cloud-storage/kinesis.md)
- [[!DNL Amazon S3] 連接器](connectors/cloud-storage/s3.md)
- [[!DNL Apache HDFS] 連接器](connectors/cloud-storage/hdfs.md)
- [[!DNL Azure Event Hubs] 連接器](connectors/cloud-storage/eventhub.md)
- [[!DNL Azure File Storage] 連接器](connectors/cloud-storage/azure-file-storage.md)
- [[!DNL FTP] 連接器](connectors/cloud-storage/ftp.md)
- [[!DNL Google Cloud Storage] 連接器](connectors/cloud-storage/google-cloud-storage.md)
- [[!DNL Google PubSub] 連接器](connectors/cloud-storage/google-pubsub.md)
- [[!DNL Oracle Object Storage] 連接器](connectors/cloud-storage/oracle-object-storage.md)
- [[!DNL SFTP] 連接器](connectors/cloud-storage/sftp.md)

### 客戶關係管理(CRM)

CRM系統提供的資料可協助建立客戶關係，進而建立忠誠度並促進客戶保留率。 Experience Platform支援從[!DNL Microsoft Dynamics 365]和[!DNL Salesforce]擷取CRM資料。 如需詳細資訊，請參閱下列相關檔案：

- [[!DNL Microsoft Dynamics] 連接器](connectors/crm/ms-dynamics.md)
- [[!DNL Salesforce] 連接器](connectors/crm/salesforce.md)

### 客戶成功

Experience Platform支援從協力廠商客戶成功應用程式擷取資料。 如需詳細資訊，請參閱下列相關檔案：

- [[!DNL Salesforce Service Cloud] 連接器](connectors/customer-success/salesforce-service-cloud.md)
- [[!DNL ServiceNow] 連接器](connectors/customer-success/servicenow.md)

### 資料庫

Experience Platform支援從協力廠商資料庫擷取資料。 有關特定源連接器的詳細資訊，請參閱以下相關文檔：

- [[!DNL Amazon Redshift] 連接器](connectors/databases/redshift.md)
- [[!DNL Apache Hive on Azure HDInsights] 連接器](connectors/databases/hive.md)
- [[!DNL Apache Spark on Azure HDInsights] 連接器](connectors/databases/spark.md)
- [[!DNL Azure Data Explorer] 連接器](connectors/databases/data-explorer.md)
- [[!DNL Azure Synapse Analytics] 連接器](connectors/databases/synapse-analytics.md)
- [[!DNL Azure Table Storage] 連接器](connectors/databases/ats.md)
- [[!DNL Couchbase] 連接器](connectors/databases/couchbase.md)
- [[!DNL Google BigQuery] 連接器](connectors/databases/bigquery.md)
- [[!DNL GreenPlum] 連接器](connectors/databases/greenplum.md)
- [[!DNL HP Vertica] 連接器](connectors/databases/hp-vertica.md)
- [[!DNL IBM DB2] 連接器](connectors/databases/ibm-db2.md)
- [[!DNL MariaDB] 連接器](connectors/databases/mariadb.md)
- [[!DNL Microsoft SQL Server] 連接器](connectors/databases/sql-server.md)
- [[!DNL MySQL] 連接器](connectors/databases/mysql.md)
- [[!DNL Oracle] 連接器](connectors/databases/oracle.md)
- [[!DNL Phoenix] 連接器](connectors/databases/phoenix.md)
- [[!DNL PostgreSQL] 連接器](connectors/databases/postgres.md)

### 電子商務

Experience Platform支援從協力廠商電子商務系統擷取資料。 有關特定源連接器的詳細資訊，請參閱以下相關文檔：

- [[!DNL Shopify]](connectors/ecommerce/shopify.md)

### 行銷自動化

Experience Platform支援從協力廠商行銷自動化系統擷取資料。 有關特定源連接器的詳細資訊，請參閱以下相關文檔：

- [[!DNL HubSpot] 連接器](connectors/marketing-automation/hubspot.md)

### 付款

Experience Platform支援從第三方支付系統擷取資料。 有關特定源連接器的詳細資訊，請參閱以下相關文檔：

- [[!DNL PayPal] 連接器](connectors/payments/paypal.md)

### 串流

Experience Platform支援從串流來源擷取資料。 有關特定源連接器的詳細資訊，請參閱以下相關文檔：

- [[!DNL HTTP API]](connectors/streaming/http.md)


### 通訊協定

Experience Platform支援從協力廠商通訊協定系統擷取資料。 有關特定源連接器的詳細資訊，請參閱以下相關文檔：

- [[!DNL Generic OData] 連接器](connectors/protocols/odata.md)

## 資料擷取中來源的存取控制

資料擷取中來源的權限可在Adobe Admin Console中管理。 您可以透過特定產品設定檔中的&#x200B;**[!UICONTROL Permissions]**&#x200B;標籤來存取權限。 從&#x200B;**[!UICONTROL 編輯權限]**&#x200B;面板，您可以透過&#x200B;**[!UICONTROL 資料擷取]**&#x200B;功能表項目存取與來源相關的權限。 **[!UICONTROL 查看源]**&#x200B;權限授予對&#x200B;**[!UICONTROL 目錄]**&#x200B;頁簽中可用源和&#x200B;**[!UICONTROL 瀏覽]**&#x200B;頁簽中已驗證源的只讀訪問權，而&#x200B;**[!UICONTROL 管理源]**&#x200B;權限授予對源的讀取、建立、編輯和禁用的完全訪問權。

下表概述UI根據這些權限的不同組合而執行的操作方式：

| 權限層級 | 說明 |
| ---- | ----|
| **[!UICONTROL 查看]** 源 | 在「目錄」頁簽中授予對每個源類型以及「瀏覽」、「帳戶」和「資料流」頁簽中的源的只讀訪問權限。 |
| **[!UICONTROL 管理來]** 源 | 除了&#x200B;**[!UICONTROL 查看源]**&#x200B;中包含的函式外，還授予對&#x200B;**[!UICONTROL 目錄]**&#x200B;中&#x200B;**[!UICONTROL 連接源]**&#x200B;選項和&#x200B;**[!UICONTROL 瀏覽]**&#x200B;中&#x200B;**[!UICONTROL 選擇資料]**&#x200B;選項的訪問權。 **[!UICONTROL 「管]** 理來源」也可讓您啟用或停用 **** 資料流程及編輯其排程。 |
| **[!UICONTROL 查看]** 源關閉 **[!UICONTROL 和管]** 理源關閉 | 撤消對源的所有訪問。 |

有關通過Admin Console授予的可用權限（包括這四個來源）的詳細資訊，請參閱[訪問控制概述](../access-control/home.md)。

## 條款與條件 {#terms-and-conditions}

使用任何標示為測試版（「測試版」）的來源，即表示您承認測試版是按&#x200B;***「原樣」提供的，不提供任何類型的擔保***。

Adobe無義務維護、更正、更新、變更、修改或以其他方式支援測試版。 建議您小心，不要依賴這類測試版和/或隨附材料的正確功能或效能。 測試版被視為Adobe的機密資訊。

您提供給Adobe的任何「意見」（關於測試版的資訊，包括但不限於使用測試版時遇到的問題或缺陷、建議、改進和建議），特此指派給Adobe，包括對此意見的所有權利、標題和興趣。

提交開放意見或建立支援票證以分享您的建議或回報錯誤、尋求功能增強功能。
