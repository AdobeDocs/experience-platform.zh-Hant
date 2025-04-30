---
keywords: Experience Platform；首頁；熱門主題；來源聯結器；來源聯結器；來源；資料來源；資料來源；資料來源連線
solution: Experience Platform
title: Source聯結器概觀
description: Adobe Experience Platform可讓您從外部來源擷取資料，同時使用Experience Platform服務來建構、加標籤及增強傳入資料。 您可以從多種來源(例如Adobe應用程式、雲端儲存、資料庫和許多其他來源)內嵌資料。
exl-id: efdbed4d-5697-43ef-a47a-a8bcf0f13237
source-git-commit: 9bc7d372eba9ffcfe64f90d2d58a532411e5f1ce
workflow-type: tm+mt
source-wordcount: '1558'
ht-degree: 3%

---

# Source聯結器概觀

Adobe Experience Platform可讓您從外部來源擷取資料，同時使用Experience Platform服務來建構、加標籤及增強傳入資料。 您可以從多種來源 (如 Adobe 應用程式、雲端型的儲存空間、資料庫和其他許多來源) 內嵌資料。 

[!DNL Flow Service]用於收集及集中來自Experience Platform內各種不同來源的客戶資料。 此服務提供使用者介面和RESTful API，可讓您輕鬆設定與各種資料提供者的來源連線。 這些來源連線可讓您驗證協力廠商系統、設定擷取執行時間，以及管理資料擷取輸送量。

有了Experience Platform，您可以集中從不同來源收集的資料，並使用從中獲得的見解做更多事情。

<div id="recs-overview-body-1"></div>
<div id="recs-overview-body-2"></div>
<div id="recs-overview-body-3"></div>
<div id="recs-overview-body-4"></div>
<div id="recs-overview-body-5"></div>
<div id="recs-overview-body-6"></div>

## 進階企業原始碼 {#advanced-enterprise-sources}

下列來源僅供[Adobe Real-Time Customer Data Platform Ultimate](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2c-edition-prime-and-ultimate-packages.html)客戶使用。

- [[!DNL Amazon Kinesis]](connectors/cloud-storage/kinesis.md) [!BADGE 串流]{type=Positive}
- [[!DNL Amazon Redshift]](connectors/databases/redshift.md) [!BADGE 批次]{type=Informative}
- [[!DNL Azure Event Hubs]](connectors/cloud-storage/eventhub.md) [!BADGE 串流]{type=Positive}
- [[!DNL Azure Synapse Analytics]](connectors/databases/synapse-analytics.md) [!BADGE 批次]{type=Informative}
- [[!DNL Google BigQuery]](connectors/databases/bigquery.md) [!BADGE 批次]{type=Informative}
- [[!DNL Google PubSub]](connectors/cloud-storage/google-pubsub.md) [!BADGE 串流]{type=Positive}
- [[!DNL Snowflake]](connectors/databases/snowflake-streaming.md) [!BADGE 串流]{type=Positive}
- [[!DNL Snowflake]](connectors/databases/snowflake.md) [!BADGE 批次]{type=Informative}

## Adobe建置和合作夥伴建置的來源 {#adobe-and-partner-built-sources}

Experience Platform來源目錄中的部分聯結器是由Adobe建置和維護的，而其他聯結器則是由合作夥伴公司使用[來源SDK](/help/sources/sources-sdk/overview.md)建置和維護的。 若合作夥伴已建立並維護來源，檔案頁面頂端的備註會指出每個合作夥伴建立的聯結器。 例如，[Amazon S3聯結器](/help/sources/connectors/cloud-storage/s3.md)是由Adobe建立，而[RainFocus聯結器](/help/sources/connectors/analytics/rainfocus.md)是由RainFocus團隊建立及維護。

對於合作夥伴編寫和維護的聯結器，這表示聯結器的問題可能需要由合作夥伴團隊解決（聯絡方法提供在檔案頁面的附註中）。 如需Adobe編寫和維護的聯結器發生問題，請聯絡您的Adobe代表或客戶服務。

## 來源類別

Experience Platform中的來源分為下列類別：

### Adobe 應用程式 {#adobe-applications}

Experience Platform可從其他Adobe應用程式(包括Adobe Analytics和Adobe Audience Manager)擷取資料。 如需詳細資訊，請參閱下列相關檔案：

- [Adobe Audience Manager來源概觀](connectors/adobe-applications/audience-manager.md)
   - [在UI中建立Adobe Audience Manager來源連線](./tutorials/ui/create/adobe-applications/audience-manager.md)
- [Adobe Analytics分類資料來源概觀](connectors/adobe-applications/classifications.md)
   - [在UI中建立Adobe Analytics分類資料來源連線](./tutorials/ui/create/adobe-applications/classifications.md)
- [Adobe Analytics報表套裝資料來源概觀](connectors/adobe-applications/analytics.md)
   - [在UI中建立Adobe Analytics來源連線](./tutorials/ui/create/adobe-applications/analytics.md)
- [Adobe Campaign Managed Cloud Services來源概觀](connectors/adobe-applications/campaign.md)
   - [在UI中建立Adobe Campaign Managed Cloud Services來源連線](./tutorials/ui/create/adobe-applications/campaign.md)
- [Adobe Commerce來源概觀](connectors/adobe-applications/commerce.md)
- [Adobe資料收集來源概觀](connectors/adobe-applications/data-collection.md)
   - [在UI中建立客戶屬性來源連線](./tutorials/ui/create/adobe-applications/customer-attributes.md)
- [[!DNL Marketo Engage]來源總覽](connectors/adobe-applications/marketo/marketo.md)
   - [在使用者介面中建立 [!DNL Marketo Engage] 來源連線](./tutorials/ui/create/adobe-applications/marketo.md)
   - [為自訂活動資料建立 [!DNL Marketo Engage] 來源連線和資料流](./tutorials/ui/create/adobe-applications/marketo-custom-activities.md)

### Advertising {#advertising}

Experience Platform支援從協力廠商廣告系統擷取資料。 如需特定來源聯結器的詳細資訊，請參閱下列相關檔案：

- [Google廣告](connectors/advertising/ads.md) [!BADGE 批次]{type=Informative}

### Analytics {#analytics}

Experience Platform支援從協力廠商分析平台擷取資料。 如需詳細資訊，請閱讀下列相關檔案：

- [[!DNL Mixpanel]](connectors/analytics/mixpanel.md) [!BADGE 批次]{type=Informative}
- [[!DNL Pendo]](connectors/analytics/pendo-webhook.md) [!BADGE 串流]{type=Positive}
- [[!DNL RainFocus]](connectors/analytics/rainfocus.md) [!BADGE 串流]{type=Positive}

### 雲端儲存空間 {#cloud-storage}

雲端儲存空間來源可將您自己的資料帶入Experience Platform，無需下載、格式化或上傳。 內嵌的資料可以格式化為XDM JSON、XDM Parquet或分隔。 流程的每個步驟都會使用使用者介面整合到來源工作流程中。 如需詳細資訊，請參閱下列相關檔案：

- [[!DNL Azure Data Lake Storage Gen2]](connectors/cloud-storage/adls-gen2.md) [!BADGE 批次]{type=Informative}
- [[!DNL Azure Blob]](connectors/cloud-storage/blob.md) [!BADGE 批次]{type=Informative}
- [[!DNL Amazon S3]](connectors/cloud-storage/s3.md) [!BADGE 批次]{type=Informative}
- [[!DNL Apache HDFS]](connectors/cloud-storage/hdfs.md) [!BADGE 批次]{type=Informative}
- [[!DNL Azure File Storage]](connectors/cloud-storage/azure-file-storage.md) [!BADGE 批次]{type=Informative}
- [[!DNL Data Landing Zone]](connectors/cloud-storage/data-landing-zone.md) [!BADGE 批次]{type=Informative}
- [[!DNL FTP]](connectors/cloud-storage/ftp.md) [!BADGE 批次]{type=Informative}
- [[!DNL Google Cloud Storage]](connectors/cloud-storage/google-cloud-storage.md) [!BADGE 批次]{type=Informative}
- [[!DNL Oracle Object Storage]](connectors/cloud-storage/oracle-object-storage.md) [!BADGE 批次]{type=Informative}
- [[!DNL SFTP]](connectors/cloud-storage/sftp.md) [!BADGE 批次]{type=Informative}

### 同意與偏好設定 {#consent}

Experience Platform支援從第三方同意和偏好設定管理平台擷取資料。 如需詳細資訊，請參閱下列相關檔案：

- [[!DNL OneTrust Integration]](connectors/consent-and-preferences/onetrust.md) [!BADGE 批次]{type=Informative}

### 客戶關係管理(CRM) {#customer-relationship-management}

CRM系統提供的資料可協助建立客戶關係，進而建立忠誠度並提升客戶保留率。 Experience Platform支援從[!DNL Microsoft Dynamics 365]和[!DNL Salesforce]擷取CRM資料。 如需詳細資訊，請參閱下列相關檔案：

- [[!DNL Microsoft Dynamics]](connectors/crm/ms-dynamics.md) [!BADGE 批次]{type=Informative}
- [[!DNL Salesforce]](connectors/crm/salesforce.md) [!BADGE 批次]{type=Informative}
- [[!DNL SugarCRM]](connectors/crm/sugarcrm.md) [!BADGE 批次]{type=Informative}
- [[!DNL Veeva CRM]](connectors/crm/veeva.md) [!BADGE 批次]{type=Informative}
- [[!DNL Zoho CRM]](connectors/crm/zoho.md) [!BADGE 批次]{type=Informative}

### 客戶成功 {#customer-success}

Experience Platform支援從協力廠商客戶成功應用程式擷取資料。 如需詳細資訊，請參閱下列相關檔案：

- [[!DNL Oracle Service Cloud]](connectors/customer-success/oracle-service-cloud.md) [!BADGE 批次]{type=Informative}
- [[!DNL Salesforce Service Cloud]](connectors/customer-success/salesforce-service-cloud.md) [!BADGE 批次]{type=Informative}
- [[!DNL ServiceNow]](connectors/customer-success/servicenow.md) [!BADGE 批次]{type=Informative}
- [[!DNL Zendesk]](connectors/customer-success/zendesk.md) [!BADGE 批次]{type=Informative}

### 資料庫 {#database}

Experience Platform支援從協力廠商資料庫擷取資料。 如需特定來源聯結器的詳細資訊，請參閱下列相關檔案：

- [[!DNL Apache Hive on Azure HDInsights]](connectors/databases/hive.md) [!BADGE 批次]{type=Informative}
- [[!DNL Apache Spark on Azure HDInsights]](connectors/databases/spark.md) [!BADGE 批次]{type=Informative}
- [[!DNL Azure Databricks]](connectors/databases/databricks.md) [!BADGE 批次]{type=Informative}
- [[!DNL Azure Data Explorer]](connectors/databases/data-explorer.md) [!BADGE 批次]{type=Informative}
- [[!DNL Azure Table Storage]](connectors/databases/ats.md) [!BADGE 批次]{type=Informative}
- [[!DNL Couchbase]](connectors/databases/couchbase.md) [!BADGE 批次]{type=Informative}
- [[!DNL GreenPlum]](connectors/databases/greenplum.md) [!BADGE 批次]{type=Informative}
- [[!DNL HP Vertica]](connectors/databases/hp-vertica.md) [!BADGE 批次]{type=Informative}
- [[!DNL IBM DB2]](connectors/databases/ibm-db2.md) [!BADGE 批次]{type=Informative}
- [[!DNL MariaDB]](connectors/databases/mariadb.md) [!BADGE 批次]{type=Informative}
- [[!DNL Microsoft SQL Server]](connectors/databases/sql-server.md) [!BADGE 批次]{type=Informative}
- [[!DNL MySQL]](connectors/databases/mysql.md) [!BADGE 批次]{type=Informative}
- [[!DNL Oracle]](connectors/databases/oracle.md) [!BADGE 批次]{type=Informative}
- [[!DNL Phoenix]](connectors/databases/phoenix.md) [!BADGE 批次]{type=Informative}
- [[!DNL PostgreSQL]](connectors/databases/postgres.md) [!BADGE 批次]{type=Informative}
- [[!DNL Teradata Vantage]](connectors/databases/teradata-vantage.md) [!BADGE 批次]{type=Informative}

### 資料與身分識別合作夥伴 {#data-partner}

Experience Platform支援從資料和身分識別合作夥伴擷取資料。 如需特定來源聯結器的詳細資訊，請參閱下列相關檔案：

- [[!DNL Acxiom Data Ingestion]](connectors/data-partners/acxiom-data-ingestion.md) [!BADGE 批次]{type=Informative}
- [[!DNL Acxiom Prospecting Data Import]](connectors/data-partners/acxiom-prospecting-data-import.md) [!BADGE 批次]{type=Informative}
- [[!DNL Algolia User Profiles]](connectors/data-partners/algolia-user-profiles.md)
- [[!DNL Bombora Intent]](connectors/data-partners/bombora.md) [!BADGE 批次]{type=Informative}
- [[!DNL Demandbase Intent]](connectors/data-partners/demandbase.md) [!BADGE 批次]{type=Informative}
- [[!DNL Merkury Enterprise Identity Resolution]](connectors/data-partners/merkury.md) [!BADGE 批次]{type=Informative}

### 電子商務 {#ecommerce}

Experience Platform支援從協力廠商電子商務系統擷取資料。 如需特定來源聯結器的詳細資訊，請參閱下列相關檔案：

- [[!DNL SAP Commerce]](connectors/ecommerce/sap-commerce.md) [!BADGE 批次]{type=Informative}
- [[!DNL Shopify]](connectors/ecommerce/shopify.md) [!BADGE 批次]{type=Informative}
- [[!DNL Shopify]](connectors/ecommerce/shopify-streaming.md) [!BADGE 串流]{type=Positive}

### 本機系統 {#local-system}

Experience Platform支援從本機系統擷取資料。 如需特定來源聯結器的詳細資訊，請參閱下列相關檔案：

- [本機檔案上傳](connectors/local-system/local-file-upload.md)

### 行銷自動化 {#marketing-automation}

Experience Platform支援從協力廠商行銷自動化系統擷取資料。 如需特定來源聯結器的詳細資訊，請參閱下列相關檔案：

- [[!DNL Braze]](connectors/marketing-automation/braze.md) [!BADGE 串流]{type=Positive}
- [[!DNL Chatlio]](connectors/marketing-automation/chatlio-webhook.md) [!BADGE 串流]{type=Positive}
- [[!DNL Customer.io]](connectors/marketing-automation/customerio-webhook.md) [!BADGE 串流]{type=Positive}
- [[!DNL HubSpot]](connectors/marketing-automation/hubspot.md) [!BADGE 批次]{type=Informative}
- [[!DNL Mailchimp]](connectors/marketing-automation/mailchimp.md) [!BADGE 批次]{type=Informative}
- [[!DNL Oracle Eloqua]](connectors/marketing-automation/oracle-eloqua.md) [!BADGE 批次]{type=Informative}
- [[!DNL Oracle NetSuite]](connectors/marketing-automation/oracle-netsuite.md) [!BADGE 批次]{type=Informative}
- [[!DNL PathFactory]](connectors/marketing-automation/pathfactory.md) [!BADGE 批次]{type=Informative}
- [[!DNL Salesforce Marketing Cloud]](connectors/marketing-automation/salesforce-marketing-cloud.md) [!BADGE 批次]{type=Informative}
<!-- 
- [[!DNL Oracle Responsys]](connectors/marketing-automation/oracle-responsys.md)
-->

### 付款 {#payments}

Experience Platform支援從協力廠商支付系統擷取資料。 如需特定來源聯結器的詳細資訊，請參閱下列相關檔案：

- [[!DNL PayPal]](connectors/payments/paypal.md) [!BADGE 批次]{type=Informative}
- [[!DNL Square]](connectors/payments/square.md) [!BADGE 批次]{type=Informative}
- [[!DNL Stripe]](connectors/payments/stripe.md) [!BADGE 批次]{type=Informative}

### 串流 {#streaming}

Experience Platform支援從串流來源擷取資料。 如需特定來源聯結器的詳細資訊，請參閱下列相關檔案：

- [[!DNL HTTP API]](connectors/streaming/http.md) [!BADGE 串流]{type=Positive}

### 通訊協定 {#protocols}

Experience Platform支援從協力廠商通訊協定系統擷取資料。 如需特定來源聯結器的詳細資訊，請參閱下列相關檔案：

- [[!DNL Generic OData]](connectors/protocols/odata.md) [!BADGE 批次]{type=Informative}
- [[!DNL Generic REST API]](connectors/protocols/generic-rest.md) [!BADGE 批次]{type=Informative}

## 資料擷取中來源的存取控制

資料內嵌來源的許可權可在Adobe Admin Console中管理。 您可以透過特定產品設定檔中的&#x200B;**[!UICONTROL 許可權]**&#x200B;索引標籤來存取許可權。 從&#x200B;**[!UICONTROL 編輯許可權]**&#x200B;面板，您可以透過&#x200B;**[!UICONTROL 資料擷取]**&#x200B;功能表專案來存取與來源相關的許可權。 **[!UICONTROL 檢視來源]**&#x200B;許可權會授予&#x200B;**[!UICONTROL 目錄]**&#x200B;標籤中可用來源的唯讀存取權，以及&#x200B;**[!UICONTROL 瀏覽]**&#x200B;標籤中經過驗證的來源，而&#x200B;**[!UICONTROL 管理來源]**&#x200B;許可權會授與讀取、建立、編輯和停用來源的完整存取權。

下表概述UI根據這些許可權的不同組合時的行為方式：

| 許可權層級 | 說明 |
| ---- | ----|
| **[!UICONTROL 檢視來源]**&#x200B;於 | 授予「目錄」標籤中每個來源型別以及「瀏覽」、「帳戶」和「資料流」標籤的來源的唯讀存取權。 |
| **[!UICONTROL 管理來源]**&#x200B;於 | 除了&#x200B;**[!UICONTROL 檢視來源]**&#x200B;中包含的功能外，還授與&#x200B;**[!UICONTROL 目錄]**&#x200B;中&#x200B;**[!UICONTROL 連線Source]**&#x200B;選項的存取權，以及&#x200B;**[!UICONTROL 瀏覽]**&#x200B;中&#x200B;**[!UICONTROL 選取資料]**&#x200B;選項的存取權。 **[!UICONTROL 管理來源]**&#x200B;也可讓您啟用或停用&#x200B;**[!UICONTROL DataFlows]**&#x200B;並編輯其排程。 |
| **[!UICONTROL 關閉檢視來源]**&#x200B;和&#x200B;**[!UICONTROL 關閉管理來源]** | 撤銷對來源的所有存取權。 |

如需透過「Adobe許可權」授與之可用許可權的詳細資訊，請參閱[存取控制總覽](../access-control/home.md)。

### 屬性型存取控制

Adobe Experience Platform中基於屬性的存取控制可讓管理員根據屬性控制對特定物件和/或權能的存取。

透過以屬性為基礎的存取控制，您可以將對應設定套用至您有許可權的欄位。 此外，如果您無法存取資料集中的所有欄位，則無法將資料內嵌至資料集。

#### 支援來源中基於屬性的存取控制

>[!TIP]
>
>屬性型存取控制的運作方式如下： **角色**&#x200B;的建立是為了分類與您的Experience Platform執行個體互動的使用者型別。 **標籤**&#x200B;已套用至&#x200B;**角色**，以指定該指定角色的存取權。 **標籤**&#x200B;也會套用至結構描述欄位和區段之類的資源。 為了讓使用者能夠存取某些結構描述欄位和區段，必須將其新增至具有指派給查詢資源&#x200B;*之相同標籤的*&#x200B;角色。 如需詳細資訊，請閱讀[屬性型存取控制端對端指南](../access-control/abac/end-to-end-guide.md)。

- 將標籤套用至結構描述欄位，以定義對貴組織中特定結構描述欄位的存取權。 建立對特定結構描述欄位的存取權後，使用者將只能為他們有權存取的欄位建立對應。
- 沒有適當角色的使用者將無法使用包含無法存取之結構描述欄位的對應來建立或更新資料流程。 此外，未經授權的使用者無法更新、刪除、啟用或停用具有無法存取之結構描述欄位的現有資料流。
- 此外，資料流在其對應、目標資料集和目標連線中，必須有完全相同的結構描述ID和版本。

如需屬性型存取控制的詳細資訊，請閱讀[屬性型存取控制總覽](../access-control/abac/overview.md)。

## 條款與條件 {#terms-and-conditions}

使用任何標示為Beta版(「Beta」)的來源，即表示您在此確認Beta係依&#x200B;***「原樣」提供，並無任何保證***。

Adobe沒有義務維護、更正、更新、變更、修改或以其他方式支援Beta。 建議您使用資訊性，切勿依賴這類Beta及/或隨附資料的正確功能或效能。 Beta視為Adobe的機密資訊。

任何「意見回饋」(有關Beta的資訊，包括但不限於您在使用Beta時遇到的問題或缺陷、建議、改進和建議)會在此指派給Adobe Adobe，包括所有權利、標題，以及對此等意見回饋的興趣。

提交開放式意見或建立支援票證以分享您的建議或報告錯誤，並尋求功能增強。
