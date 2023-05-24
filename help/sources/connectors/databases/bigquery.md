---
keywords: Experience Platform；首頁；熱門主題；BigQuery;bigquery;GoogleBigQuery;google bigquery
solution: Experience Platform
title: GoogleBigQuery源連接器概述
description: 瞭解如何使用API或用戶介面將GoogleBigQuery連接到Adobe Experience Platform。
exl-id: 35c61382-a909-47f4-a937-15cb725ecbe3
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '387'
ht-degree: 0%

---

# [!DNL Google BigQuery]

Adobe Experience Platform允許從外部源接收資料，同時讓您能夠使用平台服務構建、標籤和增強傳入資料。 您可以從多種源(如Adobe應用程式、基於雲的儲存、資料庫和許多其他源)接收資料。

[!DNL Experience Platform] 支援從第三方資料庫中接收資料。 平台可以連接到不同類型的資料庫，如關係型、NoSQL或資料倉庫。 對資料庫提供程式的支援包括 [!DNL Google BigQuery]。

## IP地址允許清單

在使用源連接器之前，必須將IP地址清單添加到允許清單。 如果無法將特定於區域的IP地址添加到允許清單，則在使用源時可能會導致錯誤或效能不佳。 查看 [IP地址允許清單](../../ip-address-allow-list.md) 的子菜單。

## 先決條件

以下部分提供了在建立 [!DNL Google BigQuery] 源連接。

### 生成 [!DNL Google BigQuery] 憑據

連接 [!DNL Google BigQuery] 在平台中，需要為以下憑據生成值：

| 憑據 | 說明 |
| ---------- | ----------- |
| `project` | 項目是您的基層組織實體 [!DNL Google Cloud] 資源，包括 [!DNL Google BigQuery]。 |
| `clientID` | 客戶端ID是您 [!DNL Google BigQuery] OAuth 2.0憑據。 |
| `clientSecret` | 客戶機密碼是 [!DNL Google BigQuery] OAuth 2.0憑據。 |
| `refreshToken` | 刷新令牌允許您獲取API的新訪問令牌。 訪問令牌的生命週期有限，在項目過程中可能會過期。 您可以使用刷新令牌來驗證並請求項目的後續訪問令牌（如果需要）。 |
| `largeResultsDataSetId` | 預先建立的  [!DNL Google BigQuery] 為支援大型結果集而需要的資料集ID。 |

有關如何為生成OAuth 2.0憑據的詳細說明 [!DNL Google] API，請參見以下 [[!DNL Google] OAuth 2.0身份驗證指南](https://developers.google.com/identity/protocols/oauth2)。

## 連接 [!DNL Google BigQuery] 到平台

以下文檔提供了有關如何連接的資訊 [!DNL Google BigQuery] 到使用API或用戶介面的平台：

### 使用API

- [使用流服務API建立GoogleBigQuery基連接](../../tutorials/api/create/databases/bigquery.md)
- [使用流服務API瀏覽資料表](../../tutorials/api/explore/tabular.md)
- [使用流服務API為資料庫源建立資料流](../../tutorials/api/collect/database-nosql.md)

### 使用UI

- [在UI中建立GoogleBigQuery源連接](../../tutorials/ui/create/databases/bigquery.md)
- [在UI中為資料庫源連接建立資料流](../../tutorials/ui/dataflow/databases.md)
