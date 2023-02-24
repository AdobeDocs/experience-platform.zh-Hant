---
keywords: Experience Platform；首頁；熱門主題；來源連接器；來源連接器；來源；資料來源；資料來源；資料來源；資料來源連線
solution: Experience Platform
title: 來源連接器概述
description: Adobe Experience Platform可讓您從外部來源擷取資料，同時使用Platform服務來建構、加標籤及增強傳入資料。 您可以從多種來源(如Adobe應用程式、雲儲存、資料庫等)內嵌資料。
exl-id: efdbed4d-5697-43ef-a47a-a8bcf0f13237
source-git-commit: e880a643150de5cc2d2fb3948b15888da54f7244
workflow-type: tm+mt
source-wordcount: '1133'
ht-degree: 2%

---

# 來源連接器概觀

Adobe Experience Platform可讓您從外部來源擷取資料，同時使用Platform服務來建構、加標籤及增強傳入資料。 您可以從多種來源 (如 Adobe 應用程式、雲端型的儲存空間、資料庫和其他許多來源) 內嵌資料。 

[!DNL Flow Service] 用於收集和集中Platform內各種不同來源的客戶資料。 此服務提供使用者介面和RESTful API，讓您輕鬆設定與各種資料提供者的來源連線。 這些來源連線可讓您驗證您的協力廠商系統、設定擷取執行的時間，以及管理資料擷取吞吐量。

透過Experience Platform，您可以集中收集來自不同來源的資料，並利用從中獲得的見解執行更多工作。

## 來源類型

Experience Platform中的來源分為以下類別：

### Adobe應用程式 {#adobe-applications}

Experience Platform可從其他Adobe應用程式(包括Adobe Analytics和Adobe Audience Manager)擷取資料。 如需詳細資訊，請參閱下列相關檔案：

- [Adobe Audience Manager來源概述](connectors/adobe-applications/audience-manager.md)
   - [在UI中建立Adobe Audience Manager來源連線](./tutorials/ui/create/adobe-applications/audience-manager.md)
- [Adobe Analytics分類資料來源概觀](connectors/adobe-applications/classifications.md)
   - [在UI中建立Adobe Analytics分類資料來源連線](./tutorials/ui/create/adobe-applications/classifications.md)
- [Adobe Analytics報表套裝資料來源概觀](connectors/adobe-applications/analytics.md)
   - [在UI中建立Adobe Analytics來源連線](./tutorials/ui/create/adobe-applications/analytics.md)
- [Adobe Campaign Managed Cloud Services來源概述](connectors/adobe-applications/campaign.md)
   - [在UI中建立Adobe Campaign Managed Cloud Services來源連線](./tutorials/ui/create/adobe-applications/campaign.md)
- [Adobe資料收集來源概觀](connectors/adobe-applications/data-collection.md)
   - [在UI中建立客戶屬性來源連線](./tutorials/ui/create/adobe-applications/customer-attributes.md)
- [[!DNL Marketo Engage] 來源概觀](connectors/adobe-applications/marketo/marketo.md)
   - [建立 [!DNL Marketo Engage] UI中的源連接](./tutorials/ui/create/adobe-applications/marketo.md)
   - [建立 [!DNL Marketo Engage] 自訂活動資料的來源連線和資料流](./tutorials/ui/create/adobe-applications/marketo-custom-activities.md)
- [Adobe Workfront來源概述](connectors/adobe-applications/workfront.md)
   - [在UI中建立Workfront來源連線](./tutorials/ui/create/adobe-applications/workfront.md)

### Advertising {#advertising}

Experience Platform支援從協力廠商廣告系統擷取資料。 有關特定源連接器的詳細資訊，請參閱以下相關文檔：

- [Google Ads](connectors/advertising/ads.md)

### Analytics {#analytics}

Experience Platform支援從協力廠商分析平台擷取資料。 如需詳細資訊，請參閱下列相關檔案：

- [[!DNL Mixpanel]](connectors/analytics/mixpanel.md)

### 雲端儲存空間 {#cloud-storage}

雲端儲存來源可將您自己的資料匯入Platform，而無須下載、格式化或上傳。 擷取的資料可格式化為XDM JSON、XDM Parquet或分隔字元。 程式的每個步驟都會使用使用者介面整合至來源工作流程中。 如需詳細資訊，請參閱下列相關檔案：

- [[!DNL Azure Data Lake Storage Gen2]](connectors/cloud-storage/adls-gen2.md)
- [[!DNL Azure Blob]](connectors/cloud-storage/blob.md)
- [[!DNL Amazon Kinesis]](connectors/cloud-storage/kinesis.md)
- [[!DNL Amazon S3]](connectors/cloud-storage/s3.md)
- [[!DNL Apache HDFS]](connectors/cloud-storage/hdfs.md)
- [[!DNL Azure Event Hubs]](connectors/cloud-storage/eventhub.md)
- [[!DNL Azure File Storage]](connectors/cloud-storage/azure-file-storage.md)
- [[!DNL Data Landing Zone]](connectors/cloud-storage/data-landing-zone.md)
- [[!DNL FTP]](connectors/cloud-storage/ftp.md)
- [[!DNL Google Cloud Storage]](connectors/cloud-storage/google-cloud-storage.md)
- [[!DNL Google PubSub]](connectors/cloud-storage/google-pubsub.md)
- [[!DNL Oracle Object Storage]](connectors/cloud-storage/oracle-object-storage.md)
- [[!DNL SFTP]](connectors/cloud-storage/sftp.md)

### 同意和偏好設定 {#consent}

Experience Platform支援從協力廠商同意和偏好設定管理平台擷取資料。 如需詳細資訊，請參閱下列相關檔案：

- [[!DNL OneTrust Integration]](connectors/consent-and-preferences/onetrust.md)

### 客戶關係管理(CRM) {#customer-relationship-management}

CRM系統提供的資料可協助建立客戶關係，進而建立忠誠度並促進客戶保留率。 Experience Platform支援從 [!DNL Microsoft Dynamics 365] 和 [!DNL Salesforce]. 如需詳細資訊，請參閱下列相關檔案：

- [[!DNL Microsoft Dynamics]](connectors/crm/ms-dynamics.md)
- [[!DNL Salesforce]](connectors/crm/salesforce.md)
- [[!DNL SugarCRM]](connectors/crm/sugarcrm.md)
- [[!DNL Veeva CRM]](connectors/crm/veeva.md)
- [[!DNL Zoho CRM]](connectors/crm/zoho.md)

### 客戶成功 {#customer-success}

Experience Platform支援從協力廠商客戶成功應用程式擷取資料。 如需詳細資訊，請參閱下列相關檔案：

- [[!DNL Oracle Service Cloud]](connectors/customer-success/oracle-service-cloud.md)
- [[!DNL Salesforce Service Cloud]](connectors/customer-success/salesforce-service-cloud.md)
- [[!DNL ServiceNow]](connectors/customer-success/servicenow.md)
- [[!DNL Zendesk]](connectors/customer-success/zendesk.md)

### 資料庫 {#database}

Experience Platform支援從協力廠商資料庫擷取資料。 有關特定源連接器的詳細資訊，請參閱以下相關文檔：

- [[!DNL Amazon Redshift]](connectors/databases/redshift.md)
- [[!DNL Apache Hive on Azure HDInsights]](connectors/databases/hive.md)
- [[!DNL Apache Spark on Azure HDInsights]](connectors/databases/spark.md)
- [[!DNL Azure Data Explorer]](connectors/databases/data-explorer.md)
- [[!DNL Azure Synapse Analytics]](connectors/databases/synapse-analytics.md)
- [[!DNL Azure Table Storage]](connectors/databases/ats.md)
- [[!DNL Couchbase]](connectors/databases/couchbase.md)
- [[!DNL Google BigQuery]](connectors/databases/bigquery.md)
- [[!DNL GreenPlum]](connectors/databases/greenplum.md)
- [[!DNL HP Vertica]](connectors/databases/hp-vertica.md)
- [[!DNL IBM DB2]](connectors/databases/ibm-db2.md)
- [[!DNL MariaDB]](connectors/databases/mariadb.md)
- [[!DNL Microsoft SQL Server]](connectors/databases/sql-server.md)
- [[!DNL MySQL]](connectors/databases/mysql.md)
- [[!DNL Oracle]](connectors/databases/oracle.md)
- [[!DNL Phoenix]](connectors/databases/phoenix.md)
- [[!DNL PostgreSQL]](connectors/databases/postgres.md)
- [[!DNL Snowflake]](connectors/databases/snowflake.md)
- [[!DNL Teradata Vantage]](connectors/databases/teradata-vantage.md)

### 電子商務 {#ecommerce}

Experience Platform支援從協力廠商電子商務系統擷取資料。 有關特定源連接器的詳細資訊，請參閱以下相關文檔：

- [[!DNL Shopify]](connectors/ecommerce/shopify.md)

### 本地系統 {#local-system}

Experience Platform支援從本機系統擷取資料。 有關特定源連接器的詳細資訊，請參閱以下相關文檔：

- [本機檔案上傳](connectors/local-system/local-file-upload.md)

### 行銷自動化 {#marketing-automation}

Experience Platform支援從協力廠商行銷自動化系統擷取資料。 有關特定源連接器的詳細資訊，請參閱以下相關文檔：

- [[!DNL Chatlio]](connectors/marketing-automation/chatlio-webhook.md)
- [[!DNL Customer.io]](connectors/marketing-automation/customerio-webhook.md)
- [[!DNL HubSpot]](connectors/marketing-automation/hubspot.md)
- [[!DNL Mailchimp]](connectors/marketing-automation/mailchimp.md)
- [[!DNL Oracle Eloqua]](connectors/marketing-automation/oracle-eloqua.md)
- [[!DNL Salesforce Marketing Cloud]](connectors/marketing-automation/salesforce-marketing-cloud.md)
<!-- - [[!DNL Oracle Responsys]](connectors/marketing-automation/oracle-responsys.md) -->

### 付款 {#payments}

Experience Platform支援從第三方支付系統擷取資料。 有關特定源連接器的詳細資訊，請參閱以下相關文檔：

- [[!DNL PayPal]](connectors/payments/paypal.md)
- [[!DNL Square]](connectors/payments/square.md)

### 串流 {#streaming}

Experience Platform支援從串流來源擷取資料。 有關特定源連接器的詳細資訊，請參閱以下相關文檔：

- [[!DNL HTTP API]](connectors/streaming/http.md)

### 通訊協定 {#protocols}

Experience Platform支援從協力廠商通訊協定系統擷取資料。 有關特定源連接器的詳細資訊，請參閱以下相關文檔：

- [[!DNL Generic OData]](connectors/protocols/odata.md)
- [[!DNL Generic REST API]](connectors/protocols/generic-rest.md)

## 資料擷取中來源的存取控制

資料擷取中來源的權限可在Adobe Admin Console中管理。 您可以透過 **[!UICONTROL 權限]** 標籤。 從 **[!UICONTROL 編輯權限]** 面板中，您可以透過 **[!UICONTROL 資料擷取]** 的上界。 此 **[!UICONTROL 查看源]** 權限授予對中可用來源的唯讀存取權 **[!UICONTROL 目錄]** 標籤和已驗證的來源(在 **[!UICONTROL 瀏覽]** 標籤，而 **[!UICONTROL 管理來源]** 權限授予讀取、建立、編輯和停用來源的完整存取權。

下表概述UI根據這些權限的不同組合而執行的操作方式：

| 權限層級 | 說明 |
| ---- | ----|
| **[!UICONTROL 查看源]** 開啟 | 在「目錄」頁簽中授予對每個源類型以及「瀏覽」、「帳戶」和「資料流」頁簽中的源的只讀訪問權限。 |
| **[!UICONTROL 管理來源]** 開啟 | 除了 **[!UICONTROL 查看源]**，授予存取權 **[!UICONTROL 連接源]** 選項 **[!UICONTROL 目錄]** 和 **[!UICONTROL 選擇資料]** 選項 **[!UICONTROL 瀏覽]**. **[!UICONTROL 管理來源]** 也可讓您啟用或停用 **[!UICONTROL 資料流]** 並編輯其排程。 |
| **[!UICONTROL 查看源]** 關閉和 **[!UICONTROL 管理來源]** 關閉 | 撤消對源的所有訪問。 |

如需透過「Adobe權限」授予的可用權限詳細資訊，請參閱 [存取控制概觀](../access-control/home.md).

### 基於屬性的源訪問控制

Adobe Experience Platform中以屬性為基礎的存取控制可讓管理員根據屬性來控制特定物件和/或功能的存取。

使用基於屬性的訪問控制，您可以將映射配置應用到您有權限的欄位。 此外，如果您無法存取資料集中的所有欄位，便無法將資料內嵌至資料集。

有關基於屬性的訪問控制的詳細資訊，請閱讀 [基於屬性的訪問控制概述](../access-control/abac/overview.md).

## 條款與條件 {#terms-and-conditions}

若使用任何標示為測試版（「測試版」）的來源，即表示您確認已提供測試版 ***「原樣」，不提供任何擔保***.

Adobe無義務維護、更正、更新、變更、修改或以其他方式支援測試版。 建議您小心，不要依賴這類測試版和/或隨附材料的正確功能或效能。 測試版被視為Adobe的機密資訊。

您提供給Adobe的任何「意見」（關於測試版的資訊，包括但不限於使用測試版時遇到的問題或缺陷、建議、改進和建議），特此指派給Adobe，包括對此意見的所有權利、標題和興趣。

提交開放意見或建立支援票證以分享您的建議或回報錯誤、尋求功能增強功能。
