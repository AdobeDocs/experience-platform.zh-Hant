---
keywords: Experience Platform；首頁；熱門主題；源連接器；源連接器；源；資料源；資料源；資料源；資料源；資料源；資料源連接
solution: Experience Platform
title: 源連接器概述
topic-legacy: overview
description: Adobe Experience Platform允許從外部源接收資料，同時讓您能夠使用平台服務構建、標籤和增強傳入資料。 您可以從多種源(如Adobe應用程式、基於雲的儲存、資料庫和許多其他源)接收資料。
exl-id: efdbed4d-5697-43ef-a47a-a8bcf0f13237
source-git-commit: 6ae0560607c1e5f80ddfe752e59850f438794351
workflow-type: tm+mt
source-wordcount: '1022'
ht-degree: 0%

---

# 源連接器概述

Adobe Experience Platform允許從外部源接收資料，同時讓您能夠使用平台服務構建、標籤和增強傳入資料。 您可以從多種源(如Adobe應用程式、基於雲的儲存、資料庫和許多其他源)接收資料。

[!DNL Flow Service] 用於收集和集中平台內不同來源的客戶資料。 該服務提供用戶介面和REST風格的API，使您可以輕鬆地設定到各種資料提供程式的源連接。 通過這些源連接，您可以驗證第三方系統，設定接收運行時間，並管理資料接收吞吐量。

通過Experience Platform，您可以集中從不同來源收集的資料，並利用從中獲得的洞察力做更多工作。

## 源類型

Experience Platform中的源分為以下類別：

### Adobe應用程式 {#adobe-applications}

Experience Platform允許從包括Adobe Analytics和Adobe Audience Manager在內的其他Adobe應用程式中接收資料。 有關詳細資訊，請參閱以下相關文檔：

- [Adobe Audience Manager源概述](connectors/adobe-applications/audience-manager.md)
- [在UI中建立Adobe Audience Manager源連接](./tutorials/ui/create/adobe-applications/audience-manager.md)
- [Adobe Analytics分類資料源連接概述](connectors/adobe-applications/classifications.md)
- [在UI中建立Adobe Analytics分類資料源連接](./tutorials/ui/create/adobe-applications/classifications.md)
- [Adobe Analytics報表套件資料源連接概述](connectors/adobe-applications/analytics.md)
- [在UI中建立Adobe Analytics源連接](./tutorials/ui/create/adobe-applications/analytics.md)
- [Adobe資料收集源概述](connectors/adobe-applications/data-collection.md)
- [在UI中建立客戶屬性源連接](./tutorials/ui/create/adobe-applications/customer-attributes.md)
- [[!DNL Marketo Engage] 源概述](connectors/adobe-applications/marketo/marketo.md)
- [建立 [!DNL Marketo Engage] UI中的源連接](./tutorials/ui/create/adobe-applications/marketo.md)

### Advertising {#advertising}

Experience Platform支援從第三方廣告系統接收資料。 有關特定源連接器的詳細資訊，請參閱以下相關文檔：

- [[!DNL Google AdWords]](connectors/advertising/ads.md)

### Analytics {#analytics}

Experience Platform支援從第三方分析平台接收資料。 有關詳細資訊，請參閱以下相關文檔：

- [[!DNL Mixpanel]](connectors/analytics/mixpanel.md)

### 雲儲存 {#cloud-storage}

雲儲存源可以將您自己的資料帶入平台，而無需下載、格式化或上載。 所攝取的資料可以格式化為XDM JSON、XDM Parke或分隔。 每個步驟都使用用戶介面整合到「源」工作流中。 有關詳細資訊，請參閱以下相關文檔：

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

### 同意和首選項 {#consent}

Experience Platform支援從第三方同意和偏好管理平台接收資料。 有關詳細資訊，請參閱以下相關文檔：

- [[!DNL OneTrust Integration]](connectors/consent-and-preferences/onetrust.md)

### 客戶關係管理(CRM) {#customer-relationship-management}

CRM系統提供的資料可以幫助建立客戶關係，而這反過來又會創造忠誠度並推動客戶的保留。 Experience Platform支援從中插入CRM資料 [!DNL Microsoft Dynamics 365] 和 [!DNL Salesforce]。 有關詳細資訊，請參閱以下相關文檔：

- [[!DNL Microsoft Dynamics]](connectors/crm/ms-dynamics.md)
- [[!DNL Salesforce]](connectors/crm/salesforce.md)
- [[!DNL Veeva CRM]](connectors/crm/veeva.md)
- [[!DNL Zoho CRM]](connectors/crm/zoho.md)

### 客戶成功 {#customer-success}

Experience Platform支援從第三方客戶成功應用程式接收資料。 有關詳細資訊，請參閱以下相關文檔：

- [[!DNL Salesforce Service Cloud]](connectors/customer-success/salesforce-service-cloud.md)
- [[!DNL ServiceNow]](connectors/customer-success/servicenow.md)
- [[!DNL Zendesk]](connectors/customer-success/zendesk.md)

### 資料庫 {#database}

Experience Platform支援從第三方資料庫接收資料。 有關特定源連接器的詳細資訊，請參閱以下相關文檔：

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

Experience Platform支援從第三方電子商務系統接收資料。 有關特定源連接器的詳細資訊，請參閱以下相關文檔：

- [[!DNL Shopify]](connectors/ecommerce/shopify.md)

### 本地系統 {#local-system}

Experience Platform支援從本地系統接收資料。 有關特定源連接器的詳細資訊，請參閱以下相關文檔：

- [本地檔案上載](connectors/local-system/local-file-upload.md)

### 營銷自動化 {#marketing-automation}

Experience Platform支援從第三方營銷自動化系統接收資料。 有關特定源連接器的詳細資訊，請參閱以下相關文檔：

- [[!DNL HubSpot]](connectors/marketing-automation/hubspot.md)
- [[!DNL Mailchimp]](connectors/marketing-automation/mailchimp.md)
- [[!DNL Oracle Eloqua]](connectors/marketing-automation/oracle-eloqua.md)
- [[!DNL Salesforce Marketing Cloud]](connectors/marketing-automation/salesforce-marketing-cloud.md)

### 付款 {#payments}

Experience Platform支援從第三方支付系統接收資料。 有關特定源連接器的詳細資訊，請參閱以下相關文檔：

- [[!DNL PayPal]](connectors/payments/paypal.md)
- [[!DNL Square]](connectors/payments/square.md)

### 流 {#streaming}

Experience Platform支援從流源接收資料。 有關特定源連接器的詳細資訊，請參閱以下相關文檔：

- [[!DNL HTTP API]](connectors/streaming/http.md)

### 協定 {#protocols}

Experience Platform支援從第三方協定系統接收資料。 有關特定源連接器的詳細資訊，請參閱以下相關文檔：

- [[!DNL Generic OData]](connectors/protocols/odata.md)
- [[!DNL Generic REST API]](connectors/protocols/generic-rest.md)

## 資料接收中源的訪問控制

資料接收源的權限可在Adobe Admin Console內管理。 您可以通過 **[!UICONTROL 權限]** 的子菜單。 從 **[!UICONTROL 編輯權限]** 面板，您可以通過 **[!UICONTROL 資料攝取]** 的子菜單。 的 **[!UICONTROL 查看源]** 權限授予對可用源的只讀訪問權限 **[!UICONTROL 目錄]** 頁籤和經過驗證的源 **[!UICONTROL 瀏覽]** 的 **[!UICONTROL 管理源]** 權限授予對讀取、建立、編輯和禁用源的完全訪問權限。

下表概述了UI基於這些權限的不同組合的行為：

| 權限級別 | 說明 |
| ---- | ----|
| **[!UICONTROL 查看源]** 開 | 授予對「目錄」頁籤中每個源類型以及「瀏覽」、「帳戶」和「資料流」頁籤中源的只讀訪問權限。 |
| **[!UICONTROL 管理源]** 開 | 除包括於 **[!UICONTROL 查看源]**，授予訪問權限 **[!UICONTROL 連接源]** 選項 **[!UICONTROL 目錄]** 和 **[!UICONTROL 選擇資料]** 選項 **[!UICONTROL 瀏覽]**。 **[!UICONTROL 管理源]** 也允許您啟用或禁用 **[!UICONTROL 資料流]** 並編輯他們的日程表。 |
| **[!UICONTROL 查看源]** 關閉和 **[!UICONTROL 管理源]** 關閉 | 撤消對源的所有訪問權限。 |

有關通過Admin Console（包括這四個源）授予的可用權限的詳細資訊，請參見 [訪問控制概述](../access-control/home.md)。

## 條款和條件 {#terms-and-conditions}

通過使用標為beta(「beta」)的任何源，您特此確認提供了beta ***「原樣」，不提供任何保證***。

Adobe沒有義務維護、更正、更新、更改、修改或以其他方式支援測試版。 建議您謹慎行事，切勿以任何方式依賴此類測試版和/或隨附材料的正確功能或效能。 Beta被視為Adobe的機密資訊。

您向Adobe提供的任何「反饋」（有關測試版的資訊，包括但不限於您在使用測試版時遇到的問題或缺陷、建議、改進和建議）將分配給Adobe，包括您對此反饋的所有權利、標題和興趣。

提交開啟反饋或建立支援票證以共用您的建議或報告錯誤，尋求功能增強。
