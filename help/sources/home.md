---
keywords: Experience Platform；首頁；熱門主題；來源聯結器；來源聯結器；來源；資料來源；資料來源；資料來源連線
solution: Experience Platform
title: Source聯結器概觀
description: Adobe Experience Platform可讓您從外部來源擷取資料，同時使用Experience Platform服務來建構、加標籤及增強傳入資料。 您可以從多種來源(例如Adobe應用程式、雲端儲存、資料庫和許多其他來源)內嵌資料。
exl-id: efdbed4d-5697-43ef-a47a-a8bcf0f13237
source-git-commit: 952fc2fac819c545304aca4505208fe59841097f
workflow-type: tm+mt
source-wordcount: '1640'
ht-degree: 8%

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

>[!BEGINSHADEBOX]

## Adobe建置和合作夥伴建置的來源 {#adobe-and-partner-built-sources}

Experience Platform來源目錄中的部分聯結器是由Adobe建置和維護的，而其他聯結器則是由合作夥伴公司使用[來源SDK](/help/sources/sources-sdk/overview.md)建置和維護的。 若合作夥伴已建立並維護來源，檔案頁面頂端的備註會指出每個合作夥伴建立的聯結器。 例如，[Amazon S3聯結器](/help/sources/connectors/cloud-storage/s3.md)是由Adobe建立，而[RainFocus聯結器](/help/sources/connectors/analytics/rainfocus.md)是由RainFocus團隊建立及維護。

對於合作夥伴編寫和維護的聯結器，這表示聯結器的問題可能需要由合作夥伴團隊解決（聯絡方法提供在檔案頁面的附註中）。 如需Adobe編寫和維護的聯結器發生問題，請聯絡您的Adobe代表或客戶服務。

>[!ENDSHADEBOX]

## 來源目錄

請閱讀下列章節，以取得來源目錄中的所有可用來源清單。

### Adobe 應用程式 {#adobe-applications}

Experience Platform可從其他Adobe應用程式(包括Adobe Analytics和Adobe Audience Manager)擷取資料。 如需詳細資訊，請閱讀下列相關檔案：

- [Adobe Audience Manager](connectors/adobe-applications/audience-manager.md)
   - [在UI中建立Adobe Audience Manager來源連線](./tutorials/ui/create/adobe-applications/audience-manager.md)
- [Adobe Analytics分類資料](connectors/adobe-applications/classifications.md)
   - [在UI中建立Adobe Analytics分類資料來源連線](./tutorials/ui/create/adobe-applications/classifications.md)
- [Adobe Analytics報表套裝資料](connectors/adobe-applications/analytics.md)
   - [在UI中建立Adobe Analytics來源連線](./tutorials/ui/create/adobe-applications/analytics.md)
- [Adobe Campaign Managed Cloud Services](connectors/adobe-applications/campaign.md)
   - [在UI中建立Adobe Campaign Managed Cloud Services來源連線](./tutorials/ui/create/adobe-applications/campaign.md)
- [Adobe Commerce](connectors/adobe-applications/commerce.md)
- [Adobe 資料彙集](connectors/adobe-applications/data-collection.md)
   - [在UI中建立客戶屬性來源連線](./tutorials/ui/create/adobe-applications/customer-attributes.md)
- [[!DNL Marketo Engage]](connectors/adobe-applications/marketo/marketo.md)
   - [在使用者介面中建立 [!DNL Marketo Engage] 來源連線](./tutorials/ui/create/adobe-applications/marketo.md)
   - [為自訂活動資料建立 [!DNL Marketo Engage] 來源連線和資料流](./tutorials/ui/create/adobe-applications/marketo-custom-activities.md)

### 進階企業原始碼 {#advanced-enterprise-sources}

下列來源僅供[Adobe Real-Time Customer Data Platform Ultimate](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2c-edition-prime-and-ultimate-packages.html)客戶使用。

| 來源 | 類別 | 擷取型別 | 雲端 |
| --- | --- | --- | --- |
| [[!DNL Amazon Kinesis]](connectors/cloud-storage/kinesis.md) | 雲端儲存空間 | 串流 | Azure、AWS |
| [[!DNL Amazon Redshift]](connectors/databases/redshift.md) | 資料庫 | 批次 | Azure、AWS |
| [[!DNL Azure Databricks]](connectors/databases/databricks.md) | 資料庫 | 批次 | Azure |
| [[!DNL Azure Event Hubs]](connectors/cloud-storage/eventhub.md) | 雲端儲存空間 | 串流 | Azure、AWS |
| [[!DNL Azure Synapse Analytics]](connectors/databases/synapse-analytics.md) | 資料庫 | 批次 | Azure |
| [[!DNL Google BigQuery]](connectors/databases/bigquery.md) | 資料庫 | 批次 | Azure |
| [[!DNL Google PubSub]](connectors/cloud-storage/google-pubsub.md) | 雲端儲存空間 | 串流 | Azure |
| [[!DNL Snowflake]](connectors/databases/snowflake-streaming.md) | 資料庫 | 串流 | Azure、AWS |
| [[!DNL Snowflake]](connectors/databases/snowflake.md) | 資料庫 | 批次 | Azure、AWS |

{style="table-layout:auto"}

### Advertising {#advertising}

您可以使用以下來源將廣告資料擷取至Experience Platform。

| 來源 | 擷取型別 | 雲端 |
| --- | --- | --- |
| [Google廣告](connectors/advertising/ads.md) | 批次 | Azure |

{style="table-layout:auto"}

### Analytics {#analytics}

您可以使用下列來源將分析資料擷取至Experience Platform。

| 來源 | 擷取型別 | 雲端 |
| --- | --- | --- |
| [[!DNL Mixpanel]](connectors/analytics/mixpanel.md) | 批次 | Azure |
| [[!DNL Pendo]](connectors/analytics/pendo-webhook.md) | 串流 | Azure |
| [[!DNL RainFocus]](connectors/analytics/rainfocus.md) | 串流 | Azure |

{style="table-layout:auto"}

### 雲端儲存空間 {#cloud-storage}

雲端儲存空間來源可將您自己的資料帶入Experience Platform，無需下載、格式化或上傳。 內嵌的資料可以格式化為XDM JSON、XDM Parquet或分隔。 流程的每個步驟都會使用使用者介面整合到來源工作流程中。 如需詳細資訊，請參閱下列相關檔案：

您可以使用以下來源將雲端儲存空間資料擷取至Experience Platform。

| 來源 | 擷取型別 | 雲端 |
| --- | --- | --- |
| [[!DNL Azure Data Lake Storage Gen2]](connectors/cloud-storage/adls-gen2.md) | 批次 | Azure |
| [[!DNL Azure Blob]](connectors/cloud-storage/blob.md) | 批次 | Azure |
| [[!DNL Amazon S3]](connectors/cloud-storage/s3.md) | 批次 | Azure、AWS |
| [[!DNL Apache HDFS]](connectors/cloud-storage/hdfs.md) | 批次 | Azure |
| [[!DNL Azure File Storage]](connectors/cloud-storage/azure-file-storage.md) | 批次 | Azure |
| [[!DNL Data Landing Zone]](connectors/cloud-storage/data-landing-zone.md) | 批次 | Azure、AWS |
| [[!DNL FTP]](connectors/cloud-storage/ftp.md) | 批次 | Azure |
| [[!DNL Google Cloud Storage]](connectors/cloud-storage/google-cloud-storage.md) | 批次 | Azure |
| [[!DNL Oracle Object Storage]](connectors/cloud-storage/oracle-object-storage.md) | 批次 | Azure |
| [[!DNL SFTP]](connectors/cloud-storage/sftp.md) | 批次 | Azure |

{style="table-layout:auto"}

### 同意與偏好設定 {#consent}

您可以使用以下來源將同意和偏好設定資料擷取至Experience Platform。

| 來源 | 擷取型別 | 雲端 |
| --- | --- | --- |
| [[!DNL OneTrust Integration]](connectors/consent-and-preferences/onetrust.md) | 批次 | Azure |

{style="table-layout:auto"}

### 客戶關係管理(CRM) {#customer-relationship-management}

CRM系統提供的資料可協助建立客戶關係，進而建立忠誠度並提升客戶保留率。 Experience Platform支援從[!DNL Microsoft Dynamics 365]和[!DNL Salesforce]擷取CRM資料。 如需詳細資訊，請參閱下列相關檔案：

您可以使用以下來源將CRM資料擷取至Experience Platform。

| 來源 | 擷取型別 | 雲端 |
| --- | --- | --- |
| [[!DNL Microsoft Dynamics]](connectors/crm/ms-dynamics.md) | 批次 | Azure |
| [[!DNL Salesforce]](connectors/crm/salesforce.md) | 批次 | Azure、AWS |
| [[!DNL SugarCRM]](connectors/crm/sugarcrm.md) | 批次 | Azure |
| [[!DNL Veeva CRM]](connectors/crm/veeva.md) | 批次 | Azure |

{style="table-layout:auto"}

### 客戶成功 {#customer-success}

您可以使用以下來源將客戶成功資料擷取至Experience Platform。

| 來源 | 擷取型別 | 雲端 |
| --- | --- | --- |
| [[!DNL Salesforce Service Cloud]](connectors/customer-success/salesforce-service-cloud.md) | 批次 | Azure |
| [[!DNL ServiceNow]](connectors/customer-success/servicenow.md) | 批次 | Azure |
| [[!DNL Zendesk]](connectors/customer-success/zendesk.md) | 批次 | Azure |

{style="table-layout:auto"}

### 資料庫 {#database}

Experience Platform支援從協力廠商資料庫擷取資料。 如需特定來源聯結器的詳細資訊，請參閱下列相關檔案：

您可以使用下列來源將資料從資料庫擷取至Experience Platform。

| 來源 | 擷取型別 | 雲端 |
| --- | --- | --- |
| [[!DNL Apache Hive on Azure HDInsights]](connectors/databases/hive.md) | 批次 | Azure |
| [[!DNL Apache Spark on Azure HDInsights]](connectors/databases/spark.md) | 批次 | Azure |
| [[!DNL Azure Data Explorer]](connectors/databases/data-explorer.md) | 批次 | Azure |
| [[!DNL Azure Table Storage]](connectors/databases/ats.md) | 批次 | Azure |
| [[!DNL GreenPlum]](connectors/databases/greenplum.md) | 批次 | Azure |
| [[!DNL HP Vertica]](connectors/databases/hp-vertica.md) | 批次 | Azure |
| [[!DNL IBM DB2]](connectors/databases/ibm-db2.md) | 批次 | Azure |
| [[!DNL MariaDB]](connectors/databases/mariadb.md) | 批次 | Azure |
| [[!DNL Microsoft SQL Server]](connectors/databases/sql-server.md) | 批次 | Azure |
| [[!DNL MySQL]](connectors/databases/mysql.md) | 批次 | Azure、AWS |
| [[!DNL Oracle]](connectors/databases/oracle.md) | 批次 | Azure |
| [[!DNL PostgreSQL]](connectors/databases/postgres.md) | 批次 | Azure、AWS |
| [[!DNL Teradata Vantage]](connectors/databases/teradata-vantage.md) | 批次 | Azure |

{style="table-layout:auto"}

### 資料與身分識別合作夥伴 {#data-partner}

您可以使用下列來源將資料和身分識別合作夥伴資料擷取至Experience Platform。

| 來源 | 擷取型別 | 雲端 |
| --- | --- | --- |
| [[!DNL Acxiom Data Ingestion]](connectors/data-partners/acxiom-data-ingestion.md) | 批次 | Azure |
| [[!DNL Acxiom Prospecting Data Import]](connectors/data-partners/acxiom-prospecting-data-import.md) | 批次 | Azure |
| [[!DNL Algolia User Profiles]](connectors/data-partners/algolia-user-profiles.md) | 批次 | Azure |
| [[!DNL Bombora Intent]](connectors/data-partners/bombora.md) | 批次 | Azure |
| [[!DNL Demandbase Intent]](connectors/data-partners/demandbase.md) | 批次 | Azure |
| [[!DNL Merkury Enterprise Identity Resolution]](connectors/data-partners/merkury.md) | 批次 | Azure |

{style="table-layout:auto"}

### 電子商務 {#ecommerce}

您可以使用以下來源將電子商務資料內嵌至Experience Platform。

| 來源 | 擷取型別 | 雲端 |
| --- | --- | --- |
| [[!DNL SAP Commerce]](connectors/ecommerce/sap-commerce.md) | 批次 | Azure |
| [[!DNL Shopify]](connectors/ecommerce/shopify.md) | 批次 | Azure |
| [[!DNL Shopify]](connectors/ecommerce/shopify-streaming.md) | 串流 | Azure |

{style="table-layout:auto"}

### 本機系統 {#local-system}

您可以使用下列來源將資料從本機系統擷取至Experience Platform。

| 來源 | 擷取型別 | 雲端 |
| --- | --- | --- |
| [本機檔案上傳](connectors/local-system/local-file-upload.md) | 批次 | Azure |

{style="table-layout:auto"}

### 行銷自動化 {#marketing-automation}

您可以使用下列來源將行銷自動化資料擷取至Experience Platform。

| 來源 | 擷取型別 | 雲端 |
| --- | --- | --- |
| [[!DNL Braze]](connectors/marketing-automation/braze.md) | 串流 | Azure |
| [[!DNL Chatlio]](connectors/marketing-automation/chatlio-webhook.md) | 串流 | Azure |
| [[!DNL Customer.io]](connectors/marketing-automation/customerio-webhook.md) | 串流 | Azure |
| [[!DNL HubSpot]](connectors/marketing-automation/hubspot.md) | 批次 | Azure |
| [[!DNL Mailchimp]](connectors/marketing-automation/mailchimp.md) | 批次 | Azure |
| [[!DNL Oracle Eloqua]](connectors/marketing-automation/oracle-eloqua.md) | 批次 | Azure |
| [[!DNL Oracle NetSuite]](connectors/marketing-automation/oracle-netsuite.md) | 批次 | Azure |
| [[!DNL PathFactory]](connectors/marketing-automation/pathfactory.md) | 批次 | Azure |
| [[!DNL Salesforce Marketing Cloud]](connectors/marketing-automation/salesforce-marketing-cloud.md) | 批次 | Azure、AWS |

{style="table-layout:auto"}

### 付款 {#payments}

您可以使用以下來源將付款資料擷取至Experience Platform。

| 來源 | 擷取型別 | 雲端 |
| --- | --- | --- |
| [[!DNL Square]](connectors/payments/square.md) | 批次 | Azure |
| [[!DNL Stripe]](connectors/payments/stripe.md) | 批次 | Azure |

{style="table-layout:auto"}

### 串流 {#streaming}

您可以使用以下來源將資料串流至Experience Platform。

| 來源 | 擷取型別 | 雲端支援 |
| --- | --- | --- |
| [[!DNL HTTP API]](connectors/streaming/http.md) | 串流 | Azure、AWS |

{style="table-layout:auto"}

### 通訊協定 {#protocols}

您可以使用以下來源將通訊協定資料擷取至Experience Platform。

| 來源 | 擷取型別 | 雲端支援 |
| --- | --- | --- |
| [[!DNL Generic OData]](connectors/protocols/odata.md) | 批次 | Azure |
| [[!DNL Generic REST API]](connectors/protocols/generic-rest.md) | 批次 | Azure |

{style="table-layout:auto"}

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
