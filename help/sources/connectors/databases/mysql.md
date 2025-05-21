---
title: MySQL Source Connector概述
description: 瞭解如何使用API或使用者介面將MySQL連線至Adobe Experience Platform。
last-substantial-update: 2025-05-20T00:00:00Z
exl-id: a18e8e69-880f-4bee-b339-726091d6f858
source-git-commit: b73ced639100c95f6c62be92d4796a206a688958
workflow-type: tm+mt
source-wordcount: '625'
ht-degree: 0%

---

# [!DNL MySQL]

[!DNL MySQL]是用來儲存和管理結構化資料的開放原始碼關聯式資料庫管理系統。 它將資料組織成表格，並使用SQL （結構化查詢語言）來查詢和更新資訊。 [!DNL MySQL]廣泛用於Web應用程式，支援多種平台，並以其速度、可靠性和易用性而聞名。

您可以使用[!DNL MySQL]來源來連線您的帳戶，並將資料從您的[!DNL MySQL]資料庫擷取到Adobe Experience Platform。

## 先決條件 {#prerequisites}

請先閱讀下列章節，完成先決條件設定，然後再將[!DNL MySQl]帳戶連線至Experience Platform。

### IP位址允許清單

在Azure或Amazon Web Services (AWS)上將來源連線至Experience Platform之前，您必須將區域特定的IP位址新增至允許清單。 如需詳細資訊，請參閱[允許清單IP位址指南，以連線至Azure和AWS上的Experience Platform ](../../ip-address-allow-list.md)以取得詳細資訊。

### 在Azure上驗證Experience Platform {#azure}

您可以使用帳戶金鑰驗證或基本驗證，將您的[!DNL MySQL]資料庫連線至Azure上的Experience Platform。

>[!BEGINTABS]

>[!TAB 帳戶金鑰驗證]

提供下列認證的值，以使用帳戶金鑰驗證將您的[!DNL MySQL]資料庫連線至Experience Platform。

| 認證 | 說明 |
| --- | --- |
| `connectionString` | 與您的帳戶相關聯的[!DNL MySQL]連線字串。 [!DNL MySQL]連線字串模式為： `Server={SERVER};Port={PORT};Database={DATABASE};UID={USERNAME};PWD={PASSWORD}`。 |
| `connectionSpec.id` | 連線規格會傳回來源的聯結器屬性，包括與建立基礎連線和來源連線相關的驗證規格。 [!DNL MySQL]的連線規格識別碼為`26d738e0-8963-47ea-aadf-c60de735468a`。 |

如需詳細資訊，請閱讀有關連線字串](https://dev.mysql.com/doc/connector-net/en/connector-net-connections-string.html)的[[!DNL MySQL] 檔案。

>[!TAB 基本驗證]

提供下列認證的值，以使用基本驗證將您的[!DNL MySQL]資料庫連線至Experience Platform。

| 認證 | 說明 |
| --- | --- |
| `server` | [!DNL MySQL]資料庫的名稱或IP位址。 |
| `username` | 與您的[!DNL MySQL]資料庫驗證相關聯的使用者名稱。 |
| `password` | 與您的[!DNL MySQL]資料庫驗證關聯的密碼。 |
| `database` | 您要連線的[!DNL MySQL]資料庫名稱。 |
| `sslMode` | 要套用至您連線的[!DNL Secure Sockets Layer] (SSL)方法。 可用的值包括： <ul><li>`DISABLED`：使用此選項來停用SSL。 如果您的伺服器需要SSL設定，則連線將會失敗</li><li>`PREFERRED`：使用此選項可偏好SSL連線，因為伺服器支援這些連線。 此選項也允許非SSL連線。</li><li>`REQUIRED`：使用此選項讓SSL連線成為必要。 如果伺服器不支援SSL，連線將會失敗。</li><li>`Verify-Ca`：如果伺服器不支援SSL，在連線失敗時使用此選項來驗證伺服器憑證。</li><li>`Verify Identity`：如果伺服器不支援SSL，在連線失敗時，使用此選項以主機的名稱驗證伺服器憑證。</li></ul> |

>[!ENDTABS]

### 在Amazon Web Services (AWS)上驗證Experience Platform {#aws}

>[!AVAILABILITY]
>
>本節適用於在Amazon Web Services (AWS)上執行的Experience Platform實作。 目前有限數量的客戶可使用在AWS上執行的Experience Platform 。 若要進一步瞭解支援的Experience Platform基礎結構，請參閱[Experience Platform多雲端總覽](../../../landing/multi-cloud.md)。

您必須提供下列認證的值，才能將[!DNL MySQL]連線至AWS上的Experience Platform。

| 認證 | 說明 |
| --- | --- |
| `server` | [!DNL MySQL]資料庫的名稱或IP。 |
| `username` | 資料庫的名稱。 |
| `password` | 與您的資料庫對應的使用者名稱。 |
| `database` | 與資料庫對應的密碼。 |
| `sslMode` | 根據您的伺服器支援，控制SSL是否強制執行的布林值。 此設定預設為`false`。 |
| `connectionSpec.id` | 連線規格會傳回來源的聯結器屬性，包括與建立基礎連線和來源連線相關的驗證規格。 [!DNL MySQL]的連線規格識別碼為`26d738e0-8963-47ea-aadf-c60de735468a`。 **注意**：只有在透過[!DNL Flow Service] API連線時才需要此認證。 |

## 使用API連線[!DNL MySQL]至Experience Platform

- [使用流程服務API連線您的 [!DNL MySQL] 資料庫](../../tutorials/api/create/databases/mysql.md)
- [使用流量服務API探索資料表](../../tutorials/api/explore/tabular.md)
- [使用流程服務API為資料庫來源建立資料流](../../tutorials/api/collect/database-nosql.md)

## 使用UI連線MySQL至Experience Platform

- [使用UI將您的 [!DNL MySQL] 資料庫連線到Experience Platform](../../tutorials/ui/create/databases/mysql.md)
- [在UI中建立資料庫來源連線的資料流](../../tutorials/ui/dataflow/databases.md)
