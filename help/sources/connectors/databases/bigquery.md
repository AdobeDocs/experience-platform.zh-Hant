---
title: Google BigQuery Source聯結器總覽
description: 瞭解如何使用API或使用者介面將Google BigQuery連線至Adobe Experience Platform。
badgeUltimate: label="Ultimate" type="Positive"
exl-id: 35c61382-a909-47f4-a937-15cb725ecbe3
source-git-commit: 2136ace3e3c1157ac7bbfe56071af3dc9bc66fd6
workflow-type: tm+mt
source-wordcount: '841'
ht-degree: 0%

---

# [!DNL Google BigQuery]來源

>[!IMPORTANT]
>
>[!DNL Google BigQuery]來源可在來源目錄中提供給已購買Real-Time Customer Data Platform Ultimate的使用者。

閱讀本檔案以瞭解您必須完成的必要步驟，才能在Azure或Amazon Web Services (AWS)上成功將您的[!DNL Google BigQuery]帳戶連線至Adobe Experience Platform。

## 先決條件 {#prerequisites}

請閱讀下列章節，瞭解必須先完成哪些先決條件設定，您才能將[!DNL Google BigQuery]帳戶連線至Experience Platform。

### IP位址允許清單

在Azure或Amazon Web Services (AWS)上將來源連線到Experience Platform之前，您必須將地區特定的IP位址新增到允許清單。 如需詳細資訊，請參閱[允許清單IP位址指南，以連線至Azure和AWS上的Experience Platform &#x200B;](../../ip-address-allow-list.md)以取得詳細資訊。

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
| `refreshToken` | 重新整理權杖可讓您取得API的新存取權杖。 存取Token的生命週期有限，且在您的專案期間可能會過期。 如有需要，您可以使用重新整理權杖來驗證並請求專案的後續存取權杖。 確定您的重新整理權杖包含下列[!DNL Google] OAuth範圍： <ul><li>`https://www.googleapis.com/auth/bigquery`</li><li>`https://www.googleapis.com/auth/cloud-platform`</li></ul> 這些範圍可讓Experience Platform提交BigQuery工作，並從您設定的專案讀取資料。 |
| `largeResultsDataSetId` | （選用）啟用大型結果集支援所需的預先建立[!DNL Google BigQuery]資料集ID。<ul><li>`largeResultsDataSetId`必須參考預先建立的[!DNL BigQuery]資料集，用於儲存大型結果集的臨時資料表。</li><li>值必須僅包含資料集識別碼（例如`marketing_temp_results`），而非專案限定名稱（請勿使用`my-project.marketing_temp_results`）。</li><li>在`largeResultsDataSetId`中指定的資料集位置（區域）必須符合正在查詢的資料表位置。</li><li>聯結器使用的帳戶必須有權讀取和寫入此資料集中的臨時結果。 至少在[!DNL BigQuery Data Editor]中指定的資料集上指派`largeResultsDataSetId`角色。</li></ul> |

#### [!DNL Google]身分識別的必要IAM角色

用來產生OAuth認證（使用者端識別碼、使用者端密碼和refreshToken）的[!DNL Google]身分必須在目標[!DNL Google Cloud]專案中具有下列IAM角色：

- [!DNL BigQuery Job User]
- [!DNL BigQuery Data Viewer]
- [!DNL BigQuery Read Session User]

這些角色可確保Experience Platform能夠建立並執行[!DNL BigQuery]個作業、從已設定的資料表讀取資料，以及根據聯結器的需求使用讀取工作階段。 確定這些角色是在包含您計畫與來源搭配使用的[!DNL BigQuery]資料集的相同專案中授與的。

如需有關如何為[!DNL Google] API產生OAuth 2.0認證的詳細指示，請參閱下列[[!DNL Google] OAuth 2.0驗證指南](https://developers.google.com/identity/protocols/oauth2)。

>[!TAB 服務驗證]

若要使用服務驗證來進行驗證，請為下列認證提供適當的值。

**注意**：您的服務帳戶必須有足夠的許可權，例如： **[!DNL BigQuery Job User]**、**[!DNL BigQuery Data Viewer]**、**[!DNL BigQuery Read Session User]**&#x200B;和&#x200B;**[!DNL BigQuery Data Owner]**，才能成功驗證服務。

| 認證 | 說明 |
| --- | --- |
| `projectId` | 您要查詢的[!DNL Google BigQuery]識別碼。 |
| `keyFileContent` | 用來驗證服務帳戶的金鑰檔案。 您可以從[[!DNL Google Cloud service accounts] 儀表板](https://console.cloud.google.com)擷取此值。 金鑰檔案內容為JSON格式。 向Experience Platform驗證時，您必須在[!DNL Base64]中編碼此專案。 |
| `largeResultsDataSetId` | （選用）啟用大型結果集支援所需的預先建立[!DNL Google BigQuery]資料集ID。<ul><li>`largeResultsDataSetId`必須參考預先建立的[!DNL BigQuery]資料集，用於儲存大型結果集的臨時資料表。</li><li>值必須僅包含資料集識別碼（例如`marketing_temp_results`），而非專案限定名稱（請勿使用`my-project.marketing_temp_results`）。</li><li>在`largeResultsDataSetId`中指定的資料集位置（區域）必須符合正在查詢的資料表位置。</li><li>聯結器使用的帳戶必須有權讀取和寫入此資料集中的臨時結果。 至少在[!DNL BigQuery Data Editor]中指定的資料集上指派`largeResultsDataSetId`角色。</li></ul> |

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
