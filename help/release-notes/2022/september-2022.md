---
title: Adobe Experience Platform發行說明2022年9月
description: 2022年9月Adobe Experience Platform發行說明。
source-git-commit: 1890bd9dbce6a217951c28fc2fb3fec2634e714d
workflow-type: tm+mt
source-wordcount: '349'
ht-degree: 7%

---


# Adobe Experience Platform 發行說明

**發行日期：2022 年 9 月 28 日**

Adobe Experience Platform 現有功能更新：

- [身份識別服務](#identity-service)
- [來源](#sources)

## 身份識別服務 {#identity-service}

要提供相關的數位體驗，必須全面了解客戶。 當您的客戶資料分散到不同的系統中，導致每個客戶看起來都有多個「身分」時，就會更難做到這一點。

Adobe Experience Platform Identity Service可跨裝置和系統橋接身分，協助您即時提供具影響力的個人數位體驗，進而協助您更清楚掌握客戶及其行為。

**更新功能**

| 功能 | 說明 |
| --- | --- |
| 支援刪除資料集 | Identity Service現在支援透過 [目錄服務API](https://developer.adobe.com/experience-platform-apis/references/catalog/)、UI或資料衛生。 閱讀指南 [在UI中刪除資料集](../../catalog/datasets/user-guide.md#delete-a-dataset) 以取得更多資訊。 |

若要進一步了解Identity Service，請閱讀 [Identity服務概述](../../identity-service/home.md).

## 來源 {#sources}

Adobe Experience Platform可內嵌來自外部來源的資料，同時允許您使用Platform服務來建構、加標籤及增強該資料。 您可以內嵌來自各種來源的資料，例如Adobe應用程式、雲端儲存、協力廠商軟體和您的CRM系統。

Experience Platform提供RESTful API和互動式UI，讓您輕鬆為各種資料提供者設定來源連線。 這些源連接允許您驗證並連接到外部儲存系統和CRM服務、設定獲取運行時間以及管理資料獲取吞吐量。

**更新功能**

| 功能 | 說明 |
| --- | --- |
| Audience Manager區段母體對即時客戶設定檔的影響 | 首次使用Audience Manager來源將Audience Manager區段傳送至Platform時，擷取大量Audience Manager區段母體會直接影響您的設定檔總數。 這表示選取所有區段可能會導致設定檔計數超過您的授權使用權限。 如需詳細資訊，請閱讀 [Audience Manager來源概觀](../../sources/connectors/adobe-applications/audience-manager.md). 如需您使用授權的詳細資訊，請參閱 [使用授權使用控制面板](../../dashboards/guides/license-usage.md). |

若要進一步了解來源，請閱讀 [來源概觀](../../sources/home.md).