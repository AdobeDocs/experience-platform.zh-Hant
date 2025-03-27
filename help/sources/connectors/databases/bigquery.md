---
title: Google BigQuery Source聯結器總覽
description: 瞭解如何使用API或使用者介面將Google BigQuery連線至Adobe Experience Platform。
badgeUltimate: label="Ultimate" type="Positive"
exl-id: 35c61382-a909-47f4-a937-15cb725ecbe3
source-git-commit: 1900a8c6a3f3119c8b9049b12f5660cc9fd181a2
workflow-type: tm+mt
source-wordcount: '582'
ht-degree: 0%

---

# [!DNL Google BigQuery]來源

>[!IMPORTANT]
>
>[!DNL Google BigQuery]來源可在來源目錄中提供給已購買Real-Time Customer Data Platform Ultimate的使用者。

閱讀本檔案以瞭解您必須完成哪些先決條件步驟，才能在Azure或Amazon Web Services (AWS)上成功將您的[!DNL Google BigQuery]帳戶連線至Adobe Experience Platform。

## 先決條件 {#prerequisites}

請閱讀下列章節，瞭解必須先完成哪些先決條件設定，您才能將[!DNL Google BigQuery]帳戶連線至Experience Platform。

### IP位址允許清單

在Azure或Amazon Web Services (AWS)上將來源連線至Experience Platform之前，您必須將區域特定的IP位址新增至允許清單。 如需詳細資訊，請參閱[允許清單IP位址指南，以連線至Azure和AWS上的Experience Platform ](../../ip-address-allow-list.md)以取得詳細資訊。

### 在Azure上驗證Experience Platform {#azure}

您必須提供下列認證，才能將您的[!DNL Google BigQuery]帳戶連線至Azure上的Experience Platform。

>[!BEGINTABS]

>[!TAB 基本驗證]

若要使用OAuth 2.0和基本驗證的組合進行驗證，請為以下憑證提供適當的值。

| 認證 | 說明 |
| --- | --- |
| `project` | 專案是您[!DNL Google Cloud]資源（包括[!DNL Google BigQuery]）的基礎層級組織實體。 |
| `clientID` | 使用者端ID是您[!DNL Google BigQuery] OAuth 2.0認證的一半。 |
| `clientSecret` | 使用者端密碼是您[!DNL Google BigQuery] OAuth 2.0認證的另一半。 |
| `refreshToken` | 重新整理權杖可讓您取得API的新存取權杖。 存取Token的生命週期有限，且在您的專案期間可能會過期。 如有需要，您可以使用重新整理權杖來驗證並請求專案的後續存取權杖。 |
| `largeResultsDataSetId` | （選用）啟用大型結果集支援所需的預先建立[!DNL Google BigQuery]資料集ID。 |

如需有關如何為[!DNL Google] API產生OAuth 2.0認證的詳細指示，請參閱下列[[!DNL Google] OAuth 2.0驗證指南](https://developers.google.com/identity/protocols/oauth2)。

>[!TAB 服務驗證]

若要使用服務驗證來進行驗證，請為下列認證提供適當的值。

**注意**：您的服務帳戶必須有足夠的許可權，例如： **[!DNL BigQuery Job User]**、**[!DNL BigQuery Data Viewer]**、**[!DNL BigQuery Read Session User]**&#x200B;和&#x200B;**[!DNL BigQuery Data Owner]**，才能成功驗證服務。

| 認證 | 說明 |
| --- | --- |
| `projectId` | 您要查詢的[!DNL Google BigQuery]識別碼。 |
| `keyFileContent` | 用來驗證服務帳戶的金鑰檔案。 您可以從[[!DNL Google Cloud service accounts] 儀表板](https://console.cloud.google.com)擷取此值。 金鑰檔案內容為JSON格式。 向Experience Platform驗證時，您必須在[!DNL Base64]中編碼此專案。 |
| `largeResultsDataSetId` | （選用）啟用大型結果集支援所需的預先建立[!DNL Google BigQuery]資料集ID。 |

如需在[!DNL Google BigQuery]中使用服務帳戶的詳細資訊，請閱讀[在 [!DNL Google BigQuery]](https://cloud.google.com/bigquery/docs/use-service-accounts)中使用服務帳戶的指南。

>[!ENDTABS]

### 在AWS上驗證Experience Platform {#aws}

您必須提供下列認證，才能將您的[!DNL Google BigQuery]帳戶連線至AWS上的Experience Platform。

| 認證 | 說明 |
| --- | --- |
| `projectId` | 您要查詢的[!DNL Google BigQuery]識別碼。 |
| `keyFileContent` | 用來驗證服務帳戶的金鑰檔案。 您可以從[[!DNL Google Cloud service accounts] 儀表板](https://console.cloud.google.com)擷取此值。 金鑰檔案內容為JSON格式。 向Experience Platform驗證時，您必須在[!DNL Base64]中編碼此專案。 |
| `datasetId` | [!DNL Google BigQuery]資料集識別碼。 此ID代表資料表所在的位置。 |

## 將[!DNL Google BigQuery]連線至Experience Platform

以下檔案提供如何使用API或使用者介面將[!DNL Google BigQuery]連線至Experience Platform的資訊：

### 使用API

- [使用流量服務API建立Google BigQuery基本連線](../../tutorials/api/create/databases/bigquery.md)
- [使用流量服務API探索資料表](../../tutorials/api/explore/tabular.md)
- [使用流程服務API為資料庫來源建立資料流](../../tutorials/api/collect/database-nosql.md)

### 使用UI

- [在使用者介面中建立Google BigQuery來源連線](../../tutorials/ui/create/databases/bigquery.md)
- [在UI中建立資料庫來源連線的資料流](../../tutorials/ui/dataflow/databases.md)
