---
title: PostgreSQL Source聯結器總覽
description: 瞭解Adobe Experience Platform上的PostgreSQL來源。
last-substantial-update: 2025-05-20T00:00:00Z
exl-id: 27b891c5-5fc5-4539-8f98-e3a53e2eefe3
source-git-commit: f4200ca71479126e585ac76dd399af4092fdf683
workflow-type: tm+mt
source-wordcount: '667'
ht-degree: 0%

---

# [!DNL PostgreSQL]

閱讀本檔案以瞭解在將[!DNL PostgreSQL]資料庫連線至Adobe Experience Platform之前需要完成的先決條件步驟。

## 先決條件 {#prerequisites}

請先閱讀下列章節，完成先決條件設定，然後再將[!DNL PostgreSQL]資料庫連線至Experience Platform。

### IP位址允許清單

在Azure或Amazon Web Services (AWS)上將來源連線至Experience Platform之前，您必須將區域特定的IP位址新增至允許清單。 如需詳細資訊，請參閱[允許清單IP位址指南，以連線至Azure和AWS上的Experience Platform ](../../ip-address-allow-list.md)以取得詳細資訊。

### 在Azure上驗證Experience Platform {#azure}

您必須提供下列驗證認證的值，才能將[!DNL PostgreSQL]連線至Azure上的Experience Platform。

>[!BEGINTABS]

>[!TAB 帳戶金鑰驗證]

提供下列認證的值，以使用帳戶金鑰驗證將您的[!DNL PostgreSQL]資料庫連線至Azure上的Experience Platform。

| 認證 | 說明 |
| --- | --- |
| `connectionString` | 與您的[!DNL PostgreSQL]帳戶關聯的連線字串。 [!DNL PostgreSQL]連線字串模式為： `Server={SERVER};Database={DATABASE};Port={PORT};UID={USERNAME};Password={PASSWORD}`。 |
| `connectionSpec.id` | 連線規格會傳回來源的聯結器屬性，包括與建立基礎連線和來源連線相關的驗證規格。 [!DNL PostgreSQL]的連線規格識別碼為`74a1c565-4e59-48d7-9d67-7c03b8a13137`。 只有在透過[!DNL Flow Service] API連線時才需要此認證。 |

如需詳細資訊，請參閱[[!DNL PostgreSQL] 檔案](https://www.postgresql.org/docs/current/)。

>[!TAB 基本驗證]

提供下列認證的值，以使用基本驗證將您的[!DNL PostgreSQL]資料庫連線至Azure上的Experience Platform。

| 認證 | 說明 |
| --- | --- |
| `server` | [!DNL PostgreSQL]資料庫的名稱或IP位址。 |
| `port` | [!DNL PostgreSQL]伺服器的TCP連線埠。 |
| `username` | 與您的[!DNL PostgreSQL]資料庫驗證相關聯的使用者名稱。 |
| `password` | 與您的[!DNL PostgreSQL]資料庫驗證關聯的密碼。 |
| `database` | 您要連線的[!DNL PostgreSQL]資料庫名稱。 |
| `sslMode` | 要套用至您連線的[!DNL Secure Sockets Layer] (SSL)方法。 可用的值包括： <ul><li>`Disable`：使用此選項來停用SSL。 如果您的伺服器需要SSL設定，則連線將會失敗。</li><li>`Allow`：使用此選項可允許SSL連線。 如果伺服器支援非SSL連線，仍可使用這些連線。</li><li>`Prefer`：使用此選項可偏好SSL連線，因為伺服器支援這些連線。 此選項也允許非SSL連線。</li><li>`Require`：使用此選項讓SSL連線成為必要。 如果伺服器不支援SSL，連線將會失敗。</li><li>`Verify-Ca`：如果伺服器不支援SSL，在連線失敗時使用此選項來驗證伺服器憑證。</li><li>`Verify-Full`：如果伺服器不支援SSL，在連線失敗時，使用此選項以主機的名稱驗證伺服器憑證。</li></ul> |
| `connectionSpec.id` | 連線規格會傳回來源的聯結器屬性，包括與建立基礎連線和來源連線相關的驗證規格。 [!DNL PostgreSQL]的連線規格識別碼為`74a1c565-4e59-48d7-9d67-7c03b8a13137`。 只有在透過[!DNL Flow Service] API連線時才需要此認證。 |

如需詳細資訊，請參閱[[!DNL PostgreSQL] 檔案](https://www.postgresql.org/docs/current/)。

>[!ENDTABS]

### 在Amazon Web Services (AWS)上驗證Experience Platform {#aws}

>[!AVAILABILITY]
>
>本節適用於在Amazon Web Services (AWS)上執行的Experience Platform實作。 目前有限數量的客戶可使用在AWS上執行的Experience Platform 。 若要進一步瞭解支援的Experience Platform基礎結構，請參閱[Experience Platform多雲端總覽](../../../landing/multi-cloud.md)。

提供下列認證的值，以使用基本驗證將您的[!DNL PostgreSQL]資料庫連線至AWS上的Experience Platform。

| 認證 | 說明 |
| --- | --- |
| `server` | [!DNL PostgreSQL]資料庫的名稱或IP位址。 |
| `port` | [!DNL PostgreSQL]伺服器的TCP連線埠。 |
| `username` | 與您的[!DNL PostgreSQL]資料庫驗證相關聯的使用者名稱。 |
| `password` | 與您的[!DNL PostgreSQL]資料庫驗證關聯的密碼。 |
| `database` | 您要連線的[!DNL PostgreSQL]資料庫名稱。 |
| `sslMode` | 根據您的伺服器支援，控制SSL是否強制執行的布林值。 此設定預設為`false`。 |
| `connectionSpec.id` | 連線規格會傳回來源的聯結器屬性，包括與建立基礎連線和來源連線相關的驗證規格。 [!DNL PostgreSQL]的連線規格識別碼為`74a1c565-4e59-48d7-9d67-7c03b8a13137`。 只有在透過[!DNL Flow Service] API連線時才需要此認證。 |

如需詳細資訊，請參閱[[!DNL PostgreSQL] 檔案](https://www.postgresql.org/docs/current/)。

## 使用API連線[!DNL PostgreSQL]至Experience Platform

* [使用Flow Service API建立 [!DNL PostgreSQL] 基本連線](../../tutorials/api/create/databases/postgres.md)
* [使用流量服務API探索資料表](../../tutorials/api/explore/tabular.md)
* [使用流程服務API為資料庫來源建立資料流](../../tutorials/api/collect/database-nosql.md)

## 使用UI連線[!DNL PostgreSQL]至Experience Platform

* [在使用者介面中建立 [!DNL PostgreSQL] 來源連線](../../tutorials/ui/create/databases/postgres.md)
* [在UI中建立資料庫來源連線的資料流](../../tutorials/ui/dataflow/databases.md)
