---
title: Adobe Experience Platform 發行說明
description: Adobe Experience Platform的最新發行說明。
source-git-commit: 0c507a26f551af1eb17889e8e77a036e3c106240
workflow-type: tm+mt
source-wordcount: '235'
ht-degree: 10%

---

# Adobe Experience Platform 發行說明

**發行日期：2021 年 10 月 27 日**

Adobe Experience Platform 現有功能更新：

- [來源](#sources)

## 來源 {#sources}

Adobe Experience Platform可內嵌來自外部來源的資料，同時允許您使用Platform服務來建構、加標籤及增強該資料。 您可以內嵌來自各種來源的資料，例如Adobe應用程式、雲端儲存、協力廠商軟體和您的CRM系統。

Experience Platform提供RESTful API和互動式UI，讓您輕鬆為各種資料提供者設定來源連線。 這些源連接允許您驗證並連接到外部儲存系統和CRM服務、設定獲取運行時間以及管理資料獲取吞吐量。

| 功能 | 說明 |
| --- | --- |
| [!DNL Amazon S3] 來源增強功能 | 您現在可以使用 `s3SessionToken` 參數來連接 [!DNL Amazon S3] 帳戶傳至Platform（使用暫時安全性憑證）。 此代號可讓您提供對 [!DNL Amazon S3] 資源給不受信任環境中的用戶。 請參閱 [[!DNL Amazon S3] 檔案](../../sources/connectors/cloud-storage/s3.md#prerequisites) 以取得更多資訊。 |
| [!DNL Generic REST API] （測試版） | 您現在可以建立 [!DNL Generic REST API] 源連接使用 [[!DNL Flow Service] API](../../sources/tutorials/api/create/protocols/generic-rest.md) 或 [使用者介面](../../sources/tutorials/ui/create/protocols/generic-rest.md) 將一般REST應用程式的資料帶入Platform。 請參閱 [[!DNL Generic REST API] 概述](../../sources/connectors/protocols/generic-rest.md) 以取得更多資訊。 |
| [!DNL Zoho CRM] （測試版） | 您現在可以建立 [!DNL Zoho CRM] 源連接使用 [[!DNL Flow Service] API](../../sources/tutorials/api/create/crm/zoho.md) 或 [使用者介面](../../sources/tutorials/ui/create/crm/zoho.md) 從 [!DNL Zoho CRM] 帳戶至Platform。 請參閱 [[!DNL Zoho CRM] 概述](../../sources/connectors/crm/zoho.md) 以取得更多資訊。 |

若要進一步了解來源，請參閱 [來源概觀](../../sources/home.md).
