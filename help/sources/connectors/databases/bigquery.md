---
keywords: Experience Platform；首頁；熱門主題；BigQuery;bigquery;Google BigQuery;google bigquery
solution: Experience Platform
title: Google BigQuery來源連接器概觀
description: 了解如何使用API或使用者介面將Google BigQuery連線至Adobe Experience Platform。
exl-id: 35c61382-a909-47f4-a937-15cb725ecbe3
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '387'
ht-degree: 0%

---

# [!DNL Google BigQuery]

Adobe Experience Platform可讓您從外部來源擷取資料，同時使用Platform服務來建構、加標籤及增強傳入資料。 您可以從多種來源(如Adobe應用程式、雲儲存、資料庫等)內嵌資料。

[!DNL Experience Platform] 支援從協力廠商資料庫擷取資料。 平台可以連接到不同類型的資料庫，如關係型、 NoSQL或資料倉庫。 對資料庫提供程式的支援包括 [!DNL Google BigQuery].

## IP位址允許清單

使用來源連接器前，必須將IP位址清單新增至允許清單。 若未將您地區專屬的IP位址新增至允許清單，在使用來源時可能會導致錯誤或效能不佳。 請參閱 [IP位址允許清單](../../ip-address-allow-list.md) 頁面以取得詳細資訊。

## 先決條件

以下章節提供建立之前所需先決條件設定的詳細資訊 [!DNL Google BigQuery] 源連接。

### 產生您的 [!DNL Google BigQuery] 憑據

連接 [!DNL Google BigQuery] 若要使用Platform，您必須產生下列憑證的值：

| 憑據 | 說明 |
| ---------- | ----------- |
| `project` | 專案是您 [!DNL Google Cloud] 資源，包括 [!DNL Google BigQuery]. |
| `clientID` | 用戶端ID是您 [!DNL Google BigQuery] OAuth 2.0憑證。 |
| `clientSecret` | 用戶端密碼是 [!DNL Google BigQuery] OAuth 2.0憑證。 |
| `refreshToken` | 重新整理Token可讓您取得API的新存取Token。 存取權杖的存留期有限，且可能會在您的專案期間到期。 您可以視需要使用重新整理Token來驗證及要求您專案的後續存取Token。 |
| `largeResultsDataSetId` | 預先建立  [!DNL Google BigQuery] 啟用對大型結果集的支援所需的資料集ID。 |

如需如何為產生OAuth 2.0憑證的詳細指示 [!DNL Google] API，請參閱下列 [[!DNL Google] OAuth 2.0驗證指南](https://developers.google.com/identity/protocols/oauth2).

## Connect [!DNL Google BigQuery] 到平台

以下檔案提供如何連線的資訊 [!DNL Google BigQuery] 若要使用API或使用者介面來建立平台：

### 使用API

- [使用Flow Service API建立Google BigQuery基本連線](../../tutorials/api/create/databases/bigquery.md)
- [使用流量服務API探索資料表](../../tutorials/api/explore/tabular.md)
- [使用流服務API為資料庫源建立資料流](../../tutorials/api/collect/database-nosql.md)

### 使用UI

- [在UI中建立Google BigQuery來源連線](../../tutorials/ui/create/databases/bigquery.md)
- [在UI中為資料庫源連接建立資料流](../../tutorials/ui/dataflow/databases.md)
