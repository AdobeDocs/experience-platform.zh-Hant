---
title: Snowflake概觀
description: 瞭解Adobe Experience Platform中事件轉送的Snowflake。
last-substantial-update: 2023-06-21T00:00:00Z
exl-id: abddf0c4-3d4c-4f66-a6e0-c10b54ea3430
source-git-commit: b4334b4f73428f94f5a7e5088f98e2459afcaf3c
workflow-type: tm+mt
source-wordcount: '321'
ht-degree: 0%

---

# [!DNL Snowflake] 概觀

[[!DNL Snowflake]](https://www.snowflake.com/en/)是一個雲端資料倉儲，可以在一處儲存和分析您的所有資料記錄。 它可用於資料倉儲、資料湖、資料工程、資料科學、資料應用程式開發，以及即時或共用資料的安全共用和使用。

[!DNL Snowflake]是以Amazon Web Services (AWS)、Microsoft Azure (Azure)和Google雲端平台(GCP)為基礎所建置。

![顯示[!DNL Snowflake]資料架構的圖表。](../../../images/extensions/server/snowflake/snowflake.png)

## 我們的Snowflake整合

Snowflake帳戶可託管於下列任一雲端平台：

- [Amazon Web Services ([!DNL AWS])](https://aws.amazon.com/) - [!DNL AWS]是雲端運算平台，提供各種服務，例如分散式運算、資料庫儲存、內容傳遞，以及客戶關係管理(CRM)和企業資源規劃(ERP)的軟體即服務(SaaS)整合服務。

請參閱[[!DNL AWS] 總覽](../aws/overview.md)，以取得關於安裝擴充功能及設定事件轉送規則的詳細資訊。

- [Microsoft Azure ([!DNL Azure])](https://azure.microsoft.com/en-us/products/event-hubs/#overview) - [!DNL Azure]是雲端運算平台和線上入口網站，可讓您存取和管理Microsoft提供的雲端服務和資源。

請參閱[[!DNL Azure] 總覽](../azure/overview.md)，以取得關於安裝擴充功能及設定事件轉送規則的詳細資訊。

- [[!DNL Google Cloud Platform]](https://cloud.google.com/) - [!DNL Google Cloud Platform]是雲端運算平台，提供各種服務，例如分散式運算、資料庫儲存、內容傳遞，以及客戶關係管理(CRM)和企業資源規劃(ERP)的軟體即服務(SaaS)整合服務。

請參閱[[!DNL Google Cloud Platform] 總覽](../google-cloud-platform/overview.md)，以取得關於安裝擴充功能及設定事件轉送規則的詳細資訊。

我們的原生[[!DNL AWS]](../aws/overview.md)、[[!DNL Azure]](../azure/overview.md)和[[!DNL Google Cloud Platform]](../google-cloud-platform/overview.md)事件轉送擴充功能可讓客戶即時收集、擴充及轉送其事件資料伺服器端至其雲端服務，以供[!DNL Snowflake]使用。 請參閱下文：

![顯示[!DNL AWS]與[!DNL Azure]之間連結的[!DNL Snowflake]報告圖表。](../../../images/extensions/server/snowflake/snowflake-workflow.png)

## 後續步驟

本指南提供[!DNL Snowflake]的概觀，以及[!DNL AWS]和[!DNL Azure]事件轉送擴充功能的使用。

如需Experience Platform中[!DNL AWS]和[!DNL Azure]事件轉送功能的詳細資訊，請參閱[[!DNL AWS] 擴充功能概觀](../aws/overview.md)和[[!DNL Azure] 擴充功能概觀](../azure/overview.md)。
