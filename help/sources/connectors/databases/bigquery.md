---
title: Google BigQuery來源聯結器概述
description: 瞭解如何使用API或使用者介面將Google BigQuery連線至Adobe Experience Platform。
badgeUltimate: label="Ultimate" type="Positive"
exl-id: 35c61382-a909-47f4-a937-15cb725ecbe3
source-git-commit: 9a8139c26b5bb5ff937a51986967b57db58aab6c
workflow-type: tm+mt
source-wordcount: '396'
ht-degree: 0%

---

# [!DNL Google BigQuery] 來源

>[!IMPORTANT]
>
>此 [!DNL Google BigQuery] 已購買Real-time Customer Data Platform Ultimate的使用者可在來源目錄中取得來源。

Adobe Experience Platform可讓您從外部來源擷取資料，同時使用Platform服務來建構、加標籤及增強傳入資料。 您可以從多種來源(例如Adobe應用程式、雲端儲存、資料庫和許多其他來源)內嵌資料。

[!DNL Experience Platform] 支援從第三方資料庫擷取資料。 Platform可以連線到不同型別的資料庫，例如關聯式、NoSQL或資料倉儲。 對資料庫提供者的支援包括 [!DNL Google BigQuery].

## IP位址允許清單

使用來源聯結器之前，必須將IP位址清單新增至允許清單。 未能將您區域特定的IP位址新增到允許清單可能會導致使用來源時的錯誤或效能不佳。 請參閱 [IP位址允許清單](../../ip-address-allow-list.md) 頁面以取得詳細資訊。

## 先決條件

下節提供建立前所需的先決條件設定詳細資訊 [!DNL Google BigQuery] 來源連線。

### 產生您的 [!DNL Google BigQuery] 認證

若要連線 [!DNL Google BigQuery] 若使用Platform，您必須產生下列認證的值：

| 認證 | 說明 |
| ---------- | ----------- |
| `project` | 專案是您的基礎層級組織實體 [!DNL Google Cloud] 資源，包括 [!DNL Google BigQuery]. |
| `clientID` | 使用者端ID是您的的一半， [!DNL Google BigQuery] OAuth 2.0認證。 |
| `clientSecret` | 使用者端密碼是您密碼的另一半， [!DNL Google BigQuery] OAuth 2.0認證。 |
| `refreshToken` | 重新整理權杖可讓您取得API的新存取權杖。 存取Token的生命週期有限，且在您的專案期間可能會過期。 如有需要，您可以使用重新整理權杖來驗證並請求專案的後續存取權杖。 |
| `largeResultsDataSetId` | 預先建立的  [!DNL Google BigQuery] 啟用大型結果集支援所需的資料集ID。 |

如需如何產生OAuth 2.0憑證的詳細說明 [!DNL Google] API，請參閱下列內容 [[!DNL Google] OAuth 2.0驗證指南](https://developers.google.com/identity/protocols/oauth2).

## 連線 [!DNL Google BigQuery] 至平台

以下檔案提供有關如何連線的資訊 [!DNL Google BigQuery] 使用API或使用者介面至Platform：

### 使用API

- [使用流量服務API建立Google BigQuery基本連線](../../tutorials/api/create/databases/bigquery.md)
- [使用流量服務API探索資料表](../../tutorials/api/explore/tabular.md)
- [使用流程服務API為資料庫來源建立資料流](../../tutorials/api/collect/database-nosql.md)

### 使用UI

- [在使用者介面中建立Google BigQuery來源連線](../../tutorials/ui/create/databases/bigquery.md)
- [在UI中建立資料庫來源連線的資料流](../../tutorials/ui/dataflow/databases.md)
