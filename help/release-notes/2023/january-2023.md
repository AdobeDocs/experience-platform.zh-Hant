---
title: Adobe Experience Platform發行說明2023年1月
description: 2023年1月Adobe Experience Platform發行說明。
source-git-commit: 01c220147312108649e036d93288823df5389235
workflow-type: tm+mt
source-wordcount: '217'
ht-degree: 9%

---

# Adobe Experience Platform 發行說明

**發行日期：2023 年 1 月 25 日**

Adobe Experience Platform 現有功能更新：

- [來源](#sources)

## 來源 {#sources}

Adobe Experience Platform可內嵌來自外部來源的資料，並可讓您使用Platform服務來建構、加標籤及增強該資料。 您可以內嵌來自各種來源的資料，例如Adobe應用程式、雲端儲存、協力廠商軟體和您的CRM系統。

Experience Platform提供RESTful API和互動式UI，讓您輕鬆為各種資料提供者設定來源連線。 這些源連接允許您驗證並連接到外部儲存系統和CRM服務、設定獲取運行時間以及管理資料獲取吞吐量。

| 功能 | 說明 |
| --- | --- |
| 允許用戶訪問雲儲存源的子資料夾 | 現在，當您建立新帳戶時，可以定義對雲端儲存來源之特定子資料夾的存取權。 建立後，使用者將只能存取允許的子資料夾中的資料。 此功能適用於下列雲端儲存空間來源： [Azure Blob儲存](../../sources/connectors/cloud-storage/blob.md), [Google雲端儲存空間](../../sources/connectors/cloud-storage/google-cloud-storage.md), [Google PubSub](../../sources/connectors/cloud-storage/google-pubsub.md)，和 [SFTP](../../sources/connectors/cloud-storage/sftp.md). |
| 測試版可用性 [!DNL SugarCRM] | [!DNL SugarCRM] 來源現在可在測試版中使用。 使用 [!DNL SugarCRM Accounts & Contacts] 和 [!DNL SugarCRM Events] 來源將資料從 [!DNL SugarCRM] 帳戶Experience Platform。 如需詳細資訊，請閱讀 [[!DNL SugarCRM] 概述](../../sources/connectors/crm/sugarcrm.md). |