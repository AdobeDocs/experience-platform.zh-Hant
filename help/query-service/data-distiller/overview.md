---
title: 資料Distiller概述
description: 與您的授權權限相關的查詢服務資料的資料Distiller使用限制摘要。
source-git-commit: c7e753e54f087ee45daabb9094edeb51e54271fc
workflow-type: tm+mt
source-wordcount: '154'
ht-degree: 1%

---

# 資料Distiller概觀

Data Distiller是套件，包含Adobe Experience Platform中的一部分功能。 透過Data Distiller，您可以在Query Service中執行批次查詢，針對即時客戶設定檔或分析使用案例，執行擷取後資料準備（例如清理、整形和操作）。 您使用Data Distiller的方式取決於您對平台型應用程式的權限。

## 授權使用情況 {#license-usage}

此 [Data Distiller授權使用控制面板](./license-usage.md) 在您購買Data Distiller計算小時數後即可使用。 許可證使用控制面板幫助您監控已授權計算小時數的使用情況。 請參閱 [資料Distiller授權使用檔案](./license-usage.md) 查看貴組織的查詢服務許可證使用情況的重要資訊。

<!-- Update these descriptions post 23.3 release
## Scoping parameters {#scoping-parameters}

Scoping parameters are usage limits that relate to the scoping of your required set up, and are defined by your license capacity. Without add-ons, Data Distiller's scoping parameters are as follows: 

* **Compute Hours**: You can use PSQL or the Query Service API to run batch queries executed in any sandbox (scheduled or otherwise) to scan and write data. This uses your allotted Compute Hours per year as determined in the scoping process of your license agreement. Total Compute Hours is accumulated across all Sandboxes.
* **Data Ingested**: The data ingested into Adobe Experience Platform which can be queried using Data Distiller is subject to the limitations described in your then-current license to Adobe Real-Time Customer Data Platform, Customer Journey Analytics, and/or Adobe Journey Optimizer.
* **Data Lake Storage**: The data lake storage provided in your then-current license to Adobe Real-Time Customer Data Platform, Customer Journey Analytics, and/or Adobe Journey Optimizer may also be used with Data Distiller. Data Lake Storage is a shared feature.
* **Query Service Users**: The number of Query Service users detailed in your then-current license to Adobe Real-Time Customer Data Platform, Customer Journey Analytics, and/or Adobe Journey Optimizer may also be used with Data Distiller. Query Service Users is a shared feature. 
-->

## 護欄

請參閱 [查詢服務護欄](../guardrails.md) 有關與您的授權權限相關的查詢服務資料預設使用限制的檔案。

<!-- Update these descriptions post 23.3 release
## Static limits

A static limit is the usage limit that relates to the functional boundaries of Adobe Experience Platform Activation. [More information on Adobe Experience Platform Activation](https://helpx.adobe.com/ca/legal/product-descriptions/adobe-experience-platform0.html) can be found in the Adobe help documents. A summary of Data Distiller static limits are listed below, for more complete information please refer to the Query Service guardrail document.  

* **Batch Queries**: Scheduled batch queries time out after 24 hours.
* **Query Service**: You can use Query Service for the following purposes: 
    * To run SQL queries for data analysis and post ingestion data preparation (cleaning, shaping, and manipulation).
    * To run SQL queries to create roll-up metrics to surface directly into a BI tool.
    * To quickly inspect data within Adobe Experience Platform.
    * To generate meaningful insights from your data.
* **Reporting API Call**: To ensure queries run on aggregated data using the reporting API have enough resources to execute efficiently. This includes queries that enhance existing data models such as those provided by Real-Time Customer Data Platform. The reporting API tracks resource utilization by assigning concurrency slots to each query. A maximum of four reporting API calls are available concurrently. If you access the reporting API through a BI tool and require more concurrency slots, a BI server is required.
-->

