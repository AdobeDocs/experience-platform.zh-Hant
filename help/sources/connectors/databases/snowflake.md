---
title: Snowflake Source聯結器總覽
description: 瞭解如何使用API或使用者介面將Snowflake連線至Adobe Experience Platform。
badgeUltimate: label="Ultimate" type="Positive"
exl-id: df066463-1ae6-4ecd-ae0e-fb291cec4bd5
source-git-commit: 1b507e9846a74b7ac2d046c89fd7c27a818035ba
workflow-type: tm+mt
source-wordcount: '1502'
ht-degree: 3%

---

# [!DNL Snowflake]來源

>[!IMPORTANT]
>
>* [!DNL Snowflake]來源可在來源目錄中提供給已購買Real-Time Customer Data Platform Ultimate的使用者。
>* 根據預設，[!DNL Snowflake]來源會將`null`解譯為空字串。 請聯絡您的Adobe代表，以確保您的`null`值在Adobe Experience Platform中正確寫入`null`。
>* 為了讓Experience Platform擷取資料，所有表格型批次來源的時區都必須設定為UTC。 [!DNL Snowflake]來源唯一支援的時間戳記是TIMESTAMP_NTZ與UTC時間。

Adobe Experience Platform 讓您可以從外部來源擷取資料，同時可以使用 Experience Platform 服務來建立、加標籤，同時強化傳入資料。 您可以從多種來源(例如Adobe應用程式、雲端儲存、資料庫和許多其他來源)內嵌資料。

Experience Platform支援從協力廠商資料庫擷取資料。 Experience Platform可連線至不同型別的資料庫，例如關聯式、NoSQL或資料倉儲。 支援的資料庫提供者包括[!DNL Snowflake]。

## 先決條件 {#prerequisites}

本節概述將[!DNL Snowflake]來源連線至Experience Platform之前，需要完成的設定工作。

### IP位址允許清單

將來源連線至Experience Platform之前，您必須先將區域特定的IP位址新增至允許清單。 如需詳細資訊，請參閱[允許清單IP位址以連線至Experience Platform](../../ip-address-allow-list.md)的指南以瞭解詳細資訊。

### 收集必要的認證

您必須提供下列認證屬性的值，才能驗證您的[!DNL Snowflake]來源。

>[!BEGINTABS]

>[!TAB 帳戶金鑰驗證(Azure)]

提供下列認證的值，以使用帳戶金鑰驗證將[!DNL Snowflake]連線至Azure上的Experience Platform。

| 認證 | 說明 |
| ---------- | ----------- |
| `account` | 帳戶名稱可唯一識別組織內的帳戶。 在此情況下，您必須跨不同的[!DNL Snowflake]組織唯一識別帳戶。 若要這麼做，您必須在帳戶名稱前加上組織名稱。 例如： `orgname-account_name`。 閱讀[擷取 [!DNL Snowflake] 帳戶識別碼](#retrieve-your-account-identifier)的相關章節以取得其他指引。 如需詳細資訊，請參閱[[!DNL Snowflake] 文件](https://docs.snowflake.com/en/user-guide/admin-account-identifier#format-1-preferred-account-name-in-your-organization)，以瞭解詳情。 |
| `warehouse` | [!DNL Snowflake]倉儲管理應用程式的查詢執行程式。 每個[!DNL Snowflake]倉儲彼此獨立，在將資料帶到Experience Platform時必須個別存取。 |
| `database` | [!DNL Snowflake]資料庫包含您要帶入Experience Platform的資料。 |
| `username` | [!DNL Snowflake]帳戶的使用者名稱。 |
| `password` | [!DNL Snowflake]使用者帳戶的密碼。 |
| `role` | 在[!DNL Snowflake]工作階段中使用的預設存取控制角色。 該角色應為已指派給指定使用者的現有角色。 預設角色為`PUBLIC`。 |
| `connectionString` | 用來連線至您[!DNL Snowflake]執行個體的連線字串。 [!DNL Snowflake]的連線字串模式為`jdbc:snowflake://{ACCOUNT_NAME}.snowflakecomputing.com/?user={USERNAME}&password={PASSWORD}&db={DATABASE}&warehouse={WAREHOUSE}`。 |

>[!TAB 金鑰組驗證(Azure)]

若要使用金鑰組驗證，請先產生2048位元的RSA金鑰組。 接下來，提供以下憑證的值，以使用金鑰組驗證連線至Azure上的Experience Platform。

| 認證 | 說明 |
| --- | --- |
| `account` | 帳戶名稱可唯一識別組織內的帳戶。 在此情況下，您必須跨不同的[!DNL Snowflake]組織唯一識別帳戶。 若要這麼做，您必須在帳戶名稱前加上組織名稱。 例如： `orgname-account_name`。 閱讀[擷取 [!DNL Snowflake] 帳戶識別碼](#retrieve-your-account-identifier)的相關章節以取得其他指引。 如需詳細資訊，請參閱[[!DNL Snowflake] 文件](https://docs.snowflake.com/en/user-guide/admin-account-identifier#format-1-preferred-account-name-in-your-organization)，以瞭解詳情。 |
| `username` | 您[!DNL Snowflake]帳戶的使用者名稱。 |
| `privateKey` | 您[!DNL Base64-]帳戶的[!DNL Snowflake]編碼私密金鑰。 您可以產生加密或未加密的私密金鑰。 如果您使用加密的私密金鑰，則在對Experience Platform進行驗證時，也必須提供私密金鑰複雜密碼。 如需詳細資訊，請閱讀[擷取您的私密金鑰](#retrieve-your-private-key)的相關章節。 |
| `privateKeyPassphrase` | 私密金鑰複雜密碼是附加的安全性層級，在使用加密的私密金鑰進行驗證時必須使用此層級。 如果您使用未加密的私密金鑰，則不需要提供複雜密碼。 |
| `port` | [!DNL Snowflake]透過網際網路連線到伺服器時使用的連線埠號碼。 |
| `database` | 包含您要擷取至Experience Platform之資料的[!DNL Snowflake]資料庫。 |
| `warehouse` | [!DNL Snowflake]倉儲管理應用程式的查詢執行程式。 每個[!DNL Snowflake]倉儲彼此獨立，在將資料帶到Experience Platform時必須個別存取。 |

如需這些值的詳細資訊，請參閱[[!DNL Snowflake] 金鑰組驗證指南](https://docs.snowflake.com/en/user-guide/key-pair-auth.html)。

>[!TAB 基本驗證(AWS)]

提供下列認證的值，以使用基本驗證將[!DNL Snowflake]連線至AWS上的Experience Platform。

>[!WARNING]
>
>[!DNL Snowflake]來源的基本驗證（或帳戶金鑰驗證）將於2025年11月被取代。 您必須移至金鑰組型驗證，才能繼續使用該來源，並將資料庫中的資料擷取至Experience Platform。 如需有關棄用的詳細資訊，請閱讀[[!DNL Snowflake] 減少認證洩露風險的最佳實務指南](https://www.snowflake.com/en/resources/white-paper/best-practices-to-mitigate-the-risk-of-credential-compromise/)。

| 認證 | 說明 |
| --- | --- |
| `host` | 您的[!DNL Snowflake]帳戶連線到的主機URL。 |
| `port` | [!DNL Snowflake]透過網際網路連線到伺服器時使用的連線埠號碼。 |
| `username` | 與您的[!DNL Snowflake]帳戶相關聯的使用者名稱。 |
| `password` | 與您的[!DNL Snowflake]帳戶關聯的密碼。 |
| `database` | 將從其中提取資料的[!DNL Snowflake]資料庫。 |
| `schema` | 與您的[!DNL Snowflake]資料庫關聯的結構描述名稱。 您必須確保您要授與資料庫存取權的使用者也擁有此綱要的存取權。 |
| `warehouse` | 您正在使用的[!DNL Snowflake]倉儲。 |

>[!TAB 金鑰組驗證(AWS)]

若要使用金鑰組驗證，請先產生2048位元的RSA金鑰組。 接下來，提供以下憑證的值，以使用金鑰組驗證連線至AWS上的Experience Platform。

| 認證 | 說明 |
| --- | --- |
| `account` | 帳戶名稱可唯一識別組織內的帳戶。 在此情況下，您必須跨不同的[!DNL Snowflake]組織唯一識別帳戶。 若要這麼做，您必須在帳戶名稱前加上組織名稱。 例如： `orgname-account_name`。 閱讀[擷取 [!DNL Snowflake] 帳戶識別碼](#etrieve-your-account-identifier)的指南，以取得其他指引。 如需詳細資訊，請參閱[[!DNL Snowflake] 文件](https://docs.snowflake.com/en/user-guide/admin-account-identifier#format-1-preferred-account-name-in-your-organization)，以瞭解詳情。 |
| `username` | 您[!DNL Snowflake]帳戶的使用者名稱。 |
| `privateKey` | 您的[!DNL Snowflake]使用者的私密金鑰，以base64編碼為單行，沒有標頭或分行符號。 若要準備它，請複製PEM檔案的內容、移除`BEGIN`/`END`行及所有分行符號，然後以base64編碼結果。 如需詳細資訊，請閱讀[擷取您的私密金鑰](#retrieve-your-private-key)的相關章節。 **注意：** AWS連線目前不支援加密的私密金鑰。 |
| `port` | [!DNL Snowflake]透過網際網路連線到伺服器時使用的連線埠號碼。 |
| `database` | 包含您要擷取至Experience Platform之資料的[!DNL Snowflake]資料庫。 |
| `warehouse` | [!DNL Snowflake]倉儲管理應用程式的查詢執行程式。 每個[!DNL Snowflake]倉儲彼此獨立，在將資料帶到Experience Platform時必須個別存取。 |

如需這些值的詳細資訊，請參閱[[!DNL Snowflake] 金鑰組驗證指南](https://docs.snowflake.com/en/user-guide/key-pair-auth.html)。

>[!ENDTABS]

### 擷取您的帳戶識別碼 {#retrieve-your-account-identifier}

您必須從[!DNL Snowflake] UI儀表板擷取帳戶識別碼，因為您將使用該帳戶識別碼在Experience Platform上驗證您的[!DNL Snowflake]執行個體。

若要擷取您的帳戶識別碼：

* 在[[!DNL Snowflake] 應用程式UI儀表板](https://app.snowflake.com/)上瀏覽至您的帳戶。
* 在左側導覽中，選取&#x200B;**[!DNL Accounts]**，然後從標頭中選取&#x200B;**[!DNL Active Accounts]**。
* 接著，選取資訊圖示，然後選取並複製目前URL的網域名稱。

![已選取網域名稱的Snowflake UI儀表板。](../../images/tutorials/create/snowflake/snowflake-dashboard.png)

### 擷取您的私密金鑰 {#retrieve-your-private-key}

如果您正在使用[!DNL Snowflake]連線的金鑰組驗證，則您也必須先產生私密金鑰，才能連線至Experience Platform。

>[!BEGINTABS]

>[!TAB 建立加密的私密金鑰]

若要產生加密的[!DNL Snowflake]私密金鑰，請在終端機上執行下列命令：

```shell
openssl genrsa 2048 | openssl pkcs8 -topk8 -v2 des3 -inform PEM -out rsa_key.p8
```

如果成功，您應該會收到PEM格式的私密金鑰。

```shell
|-----BEGIN ENCRYPTED PRIVATE KEY-----
MIIE6T...
|-----END ENCRYPTED PRIVATE KEY-----
```

>[!TAB 建立未加密的私密金鑰]

若要產生未加密的[!DNL Snowflake]私密金鑰，請在終端機上執行下列命令：

```shell
openssl genrsa 2048 | openssl pkcs8 -topk8 -inform PEM -out rsa_key.p8 -nocrypt
```

如果成功，您應該會收到PEM格式的私密金鑰。

```shell
|-----BEGIN PRIVATE KEY-----
MIIE6T...
|-----END PRIVATE KEY-----
```

>[!ENDTABS]

接下來，取得您的私密金鑰並在[!DNL Base64]中進行編碼。 請確定您未對[!DNL Snowflake]私密金鑰進行任何轉換或格式轉換。 此外，您必須確保私密金鑰的結尾沒有尾端的新行字元，才能在[!DNL Base64]中進行編碼。

### 驗證設定

在建立[!DNL Snowflake]資料的來源連線之前，您還必須確定符合下列設定：

* 指派給特定使用者的預設倉儲必須與您在向Experience Platform進行驗證時輸入的倉儲相同。
* 指派給特定使用者的預設角色，必須能存取您在向Experience Platform進行驗證時輸入的相同資料庫。

若要驗證您的角色與倉儲：

* 在左側導覽中選取&#x200B;**[!DNL Admin]**，然後選取&#x200B;**[!DNL Users & Roles]**。
* 選取適當的使用者，然後選取右上角的省略符號(`...`)。
* 在出現的[!DNL Edit user]視窗中，瀏覽至[!DNL Default Role]以檢視與指定使用者相關聯的角色。
* 在相同視窗中，瀏覽至[!DNL Default Warehouse]以檢視與指定使用者相關聯的倉儲。

![您可在其中驗證角色與倉儲的Snowflake UI。](../../images/tutorials/create/snowflake/snowflake-configs.png)

成功編碼後，您就可以在Experience Platform上使用該[!DNL Base64]編碼私密金鑰來驗證您的[!DNL Snowflake]帳戶。

以下檔案提供如何使用API或使用者介面將[!DNL Snowflake]連線至Experience Platform的資訊：

## 使用API連線[!DNL Snowflake]至Experience Platform

* [使用Flow Service API建立Snowflake基本連線](../../tutorials/api/create/databases/snowflake.md)
* [使用流量服務API探索資料表](../../tutorials/api/explore/tabular.md)
* [使用流程服務API為資料庫來源建立資料流](../../tutorials/api/collect/database-nosql.md)

## 使用UI連線[!DNL Snowflake]至Experience Platform

* [在UI中建立Snowflake來源連線](../../tutorials/ui/create/databases/snowflake.md)
* [在UI中建立資料庫來源連線的資料流](../../tutorials/ui/dataflow/databases.md)
