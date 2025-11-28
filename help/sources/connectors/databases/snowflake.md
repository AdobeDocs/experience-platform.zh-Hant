---
title: Snowflake Source聯結器總覽
description: 瞭解如何使用API或使用者介面將Snowflake連線至Adobe Experience Platform。
badgeUltimate: label="Ultimate" type="Positive"
exl-id: df066463-1ae6-4ecd-ae0e-fb291cec4bd5
source-git-commit: 687363ab664e43cc854b535760dfbfc55acefd2c
workflow-type: tm+mt
source-wordcount: '1570'
ht-degree: 2%

---

# [!DNL Snowflake]來源

>[!IMPORTANT]
>
>* [!DNL Snowflake]來源可在來源目錄中提供給已購買Real-Time Customer Data Platform Ultimate的使用者。
>* 根據預設，[!DNL Snowflake]來源會將`null`解譯為空字串。 請聯絡您的Adobe代表，以確保您的`null`值在Adobe Experience Platform中正確寫入`null`。
>* 為了讓Experience Platform擷取資料，所有表格型批次來源的時區都必須設定為UTC。 [!DNL Snowflake]來源唯一支援的時間戳記是TIMESTAMP_NTZ與UTC時間。

[!DNL Snowflake]是雲端型資料倉儲平台，專為讓組織有效儲存、處理及分析大量資料而設計。 [!DNL Snowflake]是專為善用雲端的可擴充性和彈性而建置，可支援資料整合、進階分析以及跨團隊的順暢共用。 作為完全受管理的服務，[!DNL Snowflake]消除了傳統資料庫常見的維護複雜性，讓您能夠專注於從資料中獲取見解和價值。

您可以使用[!DNL Snowflake]來源連線，並將資料從[!DNL Snowflake]帶到Adobe Experience Platform。 請閱讀以下檔案，瞭解如何設定您的[!DNL Snowflake]來源並連線至Experience Platform。

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
| `account` | 帳戶名稱可唯一識別組織內的帳戶。 在此情況下，您必須跨不同的[!DNL Snowflake]組織唯一識別帳戶。 若要這麼做，您必須在帳戶名稱前加上組織名稱。 例如： `myorg-myaccount.snowflakecomputing.com`。 閱讀[擷取 [!DNL Snowflake] 帳戶識別碼](#retrieve-your-account-identifier)的相關章節以取得其他指引。 如需詳細資訊，請參閱[[!DNL Snowflake] 文件](https://docs.snowflake.com/en/user-guide/admin-account-identifier#format-1-preferred-account-name-in-your-organization)，以瞭解詳情。 |
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
| `account` | 帳戶名稱可唯一識別組織內的帳戶。 在此情況下，您必須跨不同的[!DNL Snowflake]組織唯一識別帳戶。 若要這麼做，您必須在帳戶名稱前加上組織名稱。 例如： `myorg-myaccount.snowflakecomputing.com`。 閱讀[擷取 [!DNL Snowflake] 帳戶識別碼](#retrieve-your-account-identifier)的相關章節以取得其他指引。 如需詳細資訊，請參閱[[!DNL Snowflake] 文件](https://docs.snowflake.com/en/user-guide/admin-account-identifier#format-1-preferred-account-name-in-your-organization)，以瞭解詳情。 |
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
| `account` | 帳戶名稱可唯一識別組織內的帳戶。 在此情況下，您必須跨不同的[!DNL Snowflake]組織唯一識別帳戶。 若要這麼做，您必須在帳戶名稱前加上組織名稱。 例如： `http://myorg-myaccount.snowflakecomputing.com/`。 閱讀[擷取 [!DNL Snowflake] 帳戶識別碼](#etrieve-your-account-identifier)的指南，以取得其他指引。 如需詳細資訊，請參閱[[!DNL Snowflake] 文件](https://docs.snowflake.com/en/user-guide/admin-account-identifier#format-1-preferred-account-name-in-your-organization)，以瞭解詳情。 |
| `username` | 您[!DNL Snowflake]帳戶的使用者名稱。 |
| `privateKey` | 您的[!DNL Snowflake]使用者的私密金鑰，以base64編碼為單行，沒有標頭或分行符號。 若要準備它，請複製PEM檔案的內容、移除`BEGIN`/`END`行及所有分行符號，然後以base64編碼結果。 如需詳細資訊，請閱讀[擷取您的私密金鑰](#retrieve-your-private-key)的相關章節。 **注意：** AWS連線目前不支援加密的私密金鑰。 |
| `port` | [!DNL Snowflake]透過網際網路連線到伺服器時使用的連線埠號碼。 |
| `database` | 包含您要擷取至Experience Platform之資料的[!DNL Snowflake]資料庫。 |
| `warehouse` | [!DNL Snowflake]倉儲管理應用程式的查詢執行程式。 每個[!DNL Snowflake]倉儲彼此獨立，在將資料帶到Experience Platform時必須個別存取。 |

如需這些值的詳細資訊，請參閱[[!DNL Snowflake] 金鑰組驗證指南](https://docs.snowflake.com/en/user-guide/key-pair-auth.html)。

>[!ENDTABS]

### 擷取您的帳戶識別碼 {#retrieve-your-account-identifier}

您必須從[!DNL Snowflake] UI儀表板擷取帳戶識別碼，因為您將使用此項在Experience Platform上驗證您的[!DNL Snowflake]執行個體。

若要擷取您的帳戶識別碼：

* 使用[[!DNL Snowflake] 應用程式UI儀表板](https://app.snowflake.com/)存取您的帳戶。
* 在左側導覽中，選取&#x200B;**[!DNL Accounts]**，然後從標題中選取&#x200B;**[!DNL Active Accounts]**。
* 接著，選取資訊圖示，然後選取並複製目前URL的網域名稱。

![已選取網域名稱的Snowflake UI儀表板。](../../images/tutorials/create/snowflake/snowflake-dashboard.png)

### 產生您的RSA金鑰組

在命令列介面中使用OpenSSL，產生PKCS#8格式的2048位元RSA金鑰組。 最佳實務是建立加密的私密金鑰以提供安全性，這需要複雜密碼。

>[!BEGINTABS]

>[!TAB 產生加密的私密金鑰]

若要產生加密的[!DNL Snowflake]私密金鑰，請在終端機上執行下列命令：

```bash
openssl genrsa 2048 | openssl pkcs8 -topk8 -v2 des3 -inform PEM -out rsa_key.p8# You will be prompted to enter a passphrase. Store this securely!
```

>[!TAB 產生未加密的私密金鑰]

若要產生未加密的[!DNL Snowflake]私密金鑰，請在終端機上執行下列命令：

```bash
openssl genrsa 2048 | openssl pkcs8 -topk8 -inform PEM -out rsa_key.p8 -nocrypt
```

>[!ENDTABS]

### 從您的私密金鑰產生公開金鑰

接下來，在命令列介面中執行以下命令，根據您的私密金鑰建立公開金鑰。

```bash
openssl rsa -in rsa_key.p8 -pubout -out rsa_key.pub# You will be prompted to enter the passphrase if the private key is encrypted.
```

### 將公開金鑰指派給[!DNL Snowflake]使用者

您必須使用[!DNL Snowflake]系統管理員角色（例如&#x200B;**SECURITYADMIN**），將產生的公開金鑰與Experience Platform將使用的[!DNL Snowflake]服務使用者建立關聯。 若要擷取公開金鑰內容，請開啟`rsa_key.pub`檔案並複製整個內容，不包括`-----BEGIN PUBLIC KEY----- and -----END PUBLIC KEY-----`行。 接下來，在[!DNL Snowflake]中執行下列SQL：

```sql
ALTER USER {YOUR_SNOWFLAKE_USERNAME}>SET RSA_PUBLIC_KEY='{PUBLIC_KEY_CONTENT}';
```

### 在[!DNL Base64]中編碼私密金鑰

Experience Platform要求私密金鑰必須是[!DNL Base64]編碼，並在連線設定期間提供為字串。 使用適當的工具或指令碼將`rsa_key.p8`檔案的內容編碼為單一[!DNL Base64]字串。

>[!TIP]
>
>在編碼程式之前或之後，請確定沒有額外的空格或分行符號，包括頁首/頁尾行`(-----BEGIN ENCRYPTED PRIVATE KEY----- and -----END ENCRYPTED PRIVATE KEY-----)`，因為這會造成驗證錯誤。

### 驗證設定

在Experience Platform中建立[!DNL Snowflake]來源連線之前，您必須確定使用者的&#x200B;**[!DNL Default Role]**&#x200B;和&#x200B;**[!DNL Default Warehouse]**&#x200B;符合您在Experience Platform中提供的值。 您可以使用[!DNL Snowflake] SQL命令在`DESCRIBE USER {USERNAME}` UI中驗證這些設定。

或者，您可以按照以下步驟驗證您的設定：

* 在左側導覽中選取&#x200B;**[!DNL Admin]**，然後選取&#x200B;**[!DNL Users & Roles]**。
* 選取適當的使用者，然後選取右上角的省略符號(`...`)。
* 在出現的[!DNL Edit user]視窗中，瀏覽至[!DNL Default Role]以檢視與指定使用者相關聯的角色。
* 在相同視窗中，瀏覽至[!DNL Default Warehouse]以檢視與指定使用者相關聯的倉儲。

![您可在其中驗證角色與倉儲的Snowflake UI。](../../images/tutorials/create/snowflake/snowflake-configs.png)

## 後續步驟

完成設定後，您現在可以繼續將您的[!DNL Snowflake]帳戶連線至Experience Platform。 請閱讀下列文件以了解更多資訊：

### 使用API連線[!DNL Snowflake]至Experience Platform

* [使用API連線 [!DNL Snowflake] 至Experience Platform](../../tutorials/api/create/databases/snowflake.md)
* [使用流量服務API探索資料表](../../tutorials/api/explore/tabular.md)
* [使用流程服務API為資料庫來源建立資料流](../../tutorials/api/collect/database-nosql.md)

### 使用UI連線[!DNL Snowflake]至Experience Platform

* [使用UI連線 [!DNL Snowflake] 至Experience Platform](../../tutorials/ui/create/databases/snowflake.md)
* [在UI中建立資料庫來源連線的資料流](../../tutorials/ui/dataflow/databases.md)
