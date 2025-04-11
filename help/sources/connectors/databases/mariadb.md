---
title: MariaDB Source Connector概述
description: 瞭解如何使用API或使用者介面將MariaDB連線至Adobe Experience Platform。
exl-id: 37b8f991-dca9-4f85-9bdd-4927a015e4c0
source-git-commit: 0bf31c76f86b4515688d3aa60deb8744e38b4cd5
workflow-type: tm+mt
source-wordcount: '601'
ht-degree: 0%

---

# [!DNL MariaDB]

Adobe Experience Platform允許從外部來源擷取資料，同時讓您能夠使用[!DNL Experience Platform]服務來建構、加標籤及增強傳入資料。 您可以從多種來源(例如Adobe應用程式、雲端儲存、資料庫和許多其他來源)內嵌資料。

Experience Platform支援從協力廠商資料庫擷取資料。 [!DNL Experience Platform]可以連線到不同型別的資料庫，例如關聯式、NoSQL或資料倉儲。 支援的資料庫提供者包括[!DNL MariaDB]。

## 先決條件 {#prerequisites}

請先閱讀下列章節，完成先決條件設定，然後再將[!DNL MariaDB]帳戶連線至Experience Platform。

### IP位址允許清單

在Azure或Amazon Web Services (AWS)上將來源連線至Experience Platform之前，您必須將區域特定的IP位址新增至允許清單。 如需詳細資訊，請參閱[允許清單IP位址指南，以連線至Azure和AWS上的Experience Platform ](../../ip-address-allow-list.md)以取得詳細資訊。

### 在Azure上驗證Experience Platform {#azure}

您必須提供下列認證的值，才能將[!DNL MariaDB]連線至Azure上的Experience Platform。

>[!BEGINTABS]

>[!TAB 帳戶金鑰驗證]

若要使用帳戶金鑰驗證，請為下列認證提供適當的值。

| 認證 | 說明 |
| --- | --- |
| `connectionString` | 與您的[!DNL MariaDB]驗證關聯的連線字串。 [!DNL MariaDB]連線字串模式為： `Server={HOST};Port={PORT};Database={DATABASE};UID={USERNAME};PWD={PASSWORD}`。 |
| `connectionSpec.id` | 連線規格會傳回來源的聯結器屬性，包括與建立基礎連線和來源連線相關的驗證規格。 [!DNL MariaDB]的連線規格識別碼為`3000eb99-cd47-43f3-827c-43caf170f015`。 **注意**：只有在透過[!DNL Flow Service] API連線時才需要此認證。 |

如需有關取得連線字串的詳細資訊，請參閱此[[!DNL MariaDB] 檔案](https://mariadb.com/kb/en/about-mariadb-connector-odbc/)。

>[!TAB 基本驗證]

若要使用基本驗證，請為下列認證提供適當的值。

| 認證 | 說明 |
| --- | --- |
| `server` | [!DNL MariaDB]資料庫的名稱或IP。 |
| `username` | 資料庫的名稱。 |
| `port` | 您要連線的通訊端點的連線埠號碼。 |
| `password` | 與您的資料庫對應的使用者名稱。 |
| `database` | 與資料庫對應的密碼。 |
| `sslMode` | 資料傳輸期間加密資料的方法。 |
| `connectionSpec.id` | 連線規格會傳回來源的聯結器屬性，包括與建立基礎連線和來源連線相關的驗證規格。 [!DNL MariaDB]的連線規格識別碼為`3000eb99-cd47-43f3-827c-43caf170f015`。 **注意**：只有在透過[!DNL Flow Service] API連線時才需要此認證。 |

如需有關取得連線字串的詳細資訊，請參閱此[[!DNL MariaDB] 檔案](https://mariadb.com/kb/en/about-mariadb-connector-odbc/)。

>[!ENDTABS]

### 在Amazon Web Services (AWS)上驗證Experience Platform {#aws}

>[!AVAILABILITY]
>
>本節適用於在Amazon Web Services (AWS)上執行的Experience Platform實作。 目前有限數量的客戶可使用在AWS上執行的Experience Platform 。 若要進一步瞭解支援的Experience Platform基礎結構，請參閱[Experience Platform多雲端總覽](../../../landing/multi-cloud.md)。

您必須提供下列認證的值，才能將[!DNL MariaDB]連線至AWS上的Experience Platform。

| 認證 | 說明 |
| --- | --- |
| `server` | [!DNL MariaDB]資料庫的名稱或IP。 |
| `username` | 資料庫的名稱。 |
| `port` | 您要連線的通訊端點的連線埠號碼。 |
| `password` | 與您的資料庫對應的使用者名稱。 |
| `database` | 與資料庫對應的密碼。 |
| `sslMode` | 資料傳輸期間加密資料的方法。 |
| `connectionSpec.id` | 連線規格會傳回來源的聯結器屬性，包括與建立基礎連線和來源連線相關的驗證規格。 [!DNL MariaDB]的連線規格識別碼為`3000eb99-cd47-43f3-827c-43caf170f015`。 **注意**：只有在透過[!DNL Flow Service] API連線時才需要此認證。 |

如需有關取得連線字串的詳細資訊，請參閱此[[!DNL MariaDB] 檔案](https://mariadb.com/kb/en/about-mariadb-connector-odbc/)。

## 使用API連線[!DNL MariaDB]至Experience Platform

- [使用Flow Service API建立MariaDB基本連線](../../tutorials/api/create/databases/mariadb.md)
- [使用流量服務API探索資料表](../../tutorials/api/explore/tabular.md)
- [使用流程服務API為資料庫來源建立資料流](../../tutorials/api/collect/database-nosql.md)

## 使用UI連線[!DNL MariaDB]至Experience Platform

- [在使用者介面中建立MariaDB來源連線](../../tutorials/ui/create/databases/mariadb.md)
- [在UI中建立資料庫來源連線的資料流](../../tutorials/ui/dataflow/databases.md)
