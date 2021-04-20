---
keywords: Experience Platform;home；熱門主題；源連接器；源連接器；源；資料源；資料源；資料源；資料源；資料源連接
solution: Experience Platform
title: 來源連接器概觀
topic: overview
description: Adobe Experience Platform可讓您從外部來源擷取資料，同時提供您使用平台服務來建構、標示及增強傳入資料的能力。 您可以從多種來源（例如Adobe應用程式、雲端儲存空間、資料庫等）擷取資料。
translation-type: tm+mt
source-git-commit: 0e4fda4abf5c02df81b74f15d2fbcafb68548070
workflow-type: tm+mt
source-wordcount: '943'
ht-degree: 0%

---


# 來源連接器概觀

Adobe Experience Platform可讓您從外部來源擷取資料，同時提供您使用平台服務來建構、標示及增強傳入資料的能力。 您可以從多種來源擷取資料，例如Adobe應用程式、雲端儲存空間、資料庫和其他許多來源。

[!DNL Flow Service] 用於收集和集中平台內不同來源的客戶資料。此服務提供使用者介面和REST風格的API，讓您輕鬆設定與各種資料提供者的來源連線。 這些來源連線可讓您驗證您的協力廠商系統、設定擷取執行的時間，以及管理資料擷取總處理能力。

借助Experience Platform，您可以集中管理從不同來源收集到的資料，並運用從中獲得的見解做更多事。

## 來源類型

Experience Platform中的來源可分為下列類別：

### Adobe應用程式

Experience Platform可讓您從其他Adobe應用程式擷取資料，包括Adobe Analytics、Adobe Audience Manager和[!DNL Experience Platform Launch]。 如需詳細資訊，請參閱下列相關檔案：

- [Adobe Audience Manager連接器概觀](connectors/adobe-applications/audience-manager.md)
- [在UI中建立Adobe Audience Manager來源連線](./tutorials/ui/create/adobe-applications/audience-manager.md)
- [Adobe Analytics分類資料連接器概觀](connectors/adobe-applications/classifications.md)
- [在UI中建立Adobe Analytics分類資料來源連線](./tutorials/ui/create/adobe-applications/classifications.md)
- [Adobe Analytics資料連接器概觀](connectors/adobe-applications/analytics.md)
- [在UI中建立Adobe Analytics來源連線](./tutorials/ui/create/adobe-applications/analytics.md)
- [在UI中建立客戶屬性來源連線](./tutorials/ui/create/adobe-applications/customer-attributes.md)

### 廣告

Experience Platform支援從協力廠商廣告系統擷取資料。 有關特定來源連接器的詳細資訊，請參閱下列相關檔案：

- [[!DNL Google AdWords]](connectors/advertising/ads.md) 連接器

### 雲端儲存空間

雲端儲存來源可將您自己的資料匯入平台，而不需下載、格式化或上傳。 收錄的資料可格式化為XDM JSON、XDM Parce或分隔。 此程式的每個步驟都會使用使用者介面，整合至Sources工作流程中。 如需詳細資訊，請參閱下列相關檔案：

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

CRM系統提供的資料有助於建立客戶關係，進而建立忠誠度並推動客戶維繫。 Experience Platform支援從[!DNL Microsoft Dynamics 365]和[!DNL Salesforce]擷取CRM資料。 如需詳細資訊，請參閱下列相關檔案：

- [[!DNL Microsoft Dynamics] 連接器](connectors/crm/ms-dynamics.md)
- [[!DNL Salesforce] 連接器](connectors/crm/salesforce.md)

### 客戶成功

Experience Platform可支援從協力廠商客戶成功應用程式擷取資料。 如需詳細資訊，請參閱下列相關檔案：

- [[!DNL Salesforce Service Cloud] 連接器](connectors/customer-success/salesforce-service-cloud.md)
- [[!DNL ServiceNow] 連接器](connectors/customer-success/servicenow.md)

### 資料庫

Experience Platform支援從協力廠商資料庫擷取資料。 有關特定來源連接器的詳細資訊，請參閱下列相關檔案：

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
- [[!DNL Microsoft SQL Server] 連接器](connectors/databases/sql-server.md)
- [[!DNL MySQL] 連接器](connectors/databases/mysql.md)
- [[!DNL Oracle] 連接器](connectors/databases/oracle.md)
- [[!DNL Phoenix] 連接器](connectors/databases/phoenix.md)
- [[!DNL PostgreSQL] 連接器](connectors/databases/postgres.md)

### 電子商務

Experience Platform支援從協力廠商電子商務系統擷取資料。 有關特定來源連接器的詳細資訊，請參閱下列相關檔案：

- [[!DNL Shopify]](connectors/ecommerce/shopify.md)

### 行銷自動化

Experience Platform支援從協力廠商行銷自動化系統擷取資料。 有關特定來源連接器的詳細資訊，請參閱下列相關檔案：

- [[!DNL HubSpot] 連接器](connectors/marketing-automation/hubspot.md)

### 付款

Experience Platform支援從協力廠商付款系統擷取資料。 有關特定來源連接器的詳細資訊，請參閱下列相關檔案：

- [[!DNL PayPal] 連接器](connectors/payments/paypal.md)

### 通訊協定

Experience Platform支援從協力廠商通訊協定系統擷取資料。 有關特定來源連接器的詳細資訊，請參閱下列相關檔案：

- [[!DNL Generic OData] 連接器](connectors/protocols/odata.md)

## 資料擷取中的來源存取控制

您可在Adobe Admin Console中管理資料擷取來源的權限。 您可以透過特定產品設定檔中的&#x200B;**[!UICONTROL Permissions]**&#x200B;標籤來存取權限。 從&#x200B;**[!UICONTROL 編輯權限]**&#x200B;面板，您可以通過&#x200B;**[!UICONTROL 資料擷取]**&#x200B;功能表項目存取與來源相關的權限。 **[!UICONTROL 檢視來源]**&#x200B;權限授與對&#x200B;**[!UICONTROL 目錄]**&#x200B;標籤中可用來源的唯讀存取權，以及對&#x200B;**[!UICONTROL 瀏覽]**&#x200B;標籤中已驗證來源的唯讀存取權，而&#x200B;**[!UICONTROL 管理來源]**&#x200B;權限則授與讀取、建立、編輯和停用來源的完整存取權。

下表概述UI根據這些權限的不同組合而運作的方式：

| 權限層級 | 說明 |
| ---- | ----|
| **[!UICONTROL 檢視來]** 源 | 授予對「目錄」頁籤中每個源類型以及「瀏覽」、「帳戶」和「資料流」頁籤中源的只讀訪問權。 |
| **[!UICONTROL 管理來]** 源 | 除了&#x200B;**[!UICONTROL 查看源]**&#x200B;中包含的函式外，還授予對&#x200B;**[!UICONTROL 目錄]**&#x200B;中&#x200B;**[!UICONTROL 連接源]**&#x200B;選項和&#x200B;**[!UICONTROL 瀏覽]**&#x200B;中&#x200B;**[!UICONTROL 選擇資料]**&#x200B;選項的訪問權。 **[!UICONTROL 「管]** 理來源」還允許您啟用或禁用 **** DataFlow並編輯其時間表。 |
| **[!UICONTROL 檢視來]** 源並管 **[!UICONTROL 理來]** 源關閉 | 撤銷對來源的所有存取權。 |

如需透過Admin Console授予的可用權限（包括這四個來源）的詳細資訊，請參閱[存取控制概觀](../access-control/home.md)。

## 條款與條件{#terms-and-conditions}

使用任何標示為beta(「Beta」)的「來源」，即表示您承認該「測試版」依「現狀」提供，不提供任何類型的「***」保證。***

Adobe無義務維護、更正、更新、變更、修改或以其他方式支援測試版。 建議您務必小心謹慎，不要依賴測試版及／或隨附材料的正確運作或效能。 測試版視為Adobe的機密資訊。

您提供給Adobe的任何「回饋」（有關測試版的資訊，包括但不限於您使用測試版時遇到的問題或缺陷、建議、改進和建議），茲此指派給Adobe，包括您對此等回饋的所有權利、所有權和興趣。

提交開放意見或建立支援票證，以分享您的建議或報告錯誤，尋求功能增強功能。
