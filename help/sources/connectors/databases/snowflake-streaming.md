---
title: Snowflake串流Source聯結器概觀
description: 瞭解如何建立來源連線和資料流，以將串流資料從您的Snowflake執行個體擷取到Adobe Experience Platform
badgeUltimate: label="Ultimate" type="Positive"
exl-id: ed937689-e844-487e-85fb-e3536c851fe5
source-git-commit: be2ad7a02d4bdf5a26a0847c8ee7a9a93746c2ad
workflow-type: tm+mt
source-wordcount: '1510'
ht-degree: 3%

---

# [!DNL Snowflake]串流來源

>[!IMPORTANT]
>
>* 已購買Real-Time CDP Ultimate的使用者可在API中使用[!DNL Snowflake]串流來源。
>
>* 您現在可以在Amazon Web Services (AWS)上執行Adobe Experience Platform時使用[!DNL Snowflake]串流來源。 目前有限數量的客戶可使用在AWS上執行的Experience Platform 。 若要進一步瞭解支援的Experience Platform基礎結構，請參閱[Experience Platform多雲端總覽](../../../landing/multi-cloud.md)。

Adobe Experience Platform 讓您可以從外部來源擷取資料，同時可以使用 Experience Platform 服務來建立、加標籤，同時強化傳入資料。 您可以從多種來源(例如Adobe應用程式、雲端儲存、資料庫和許多其他來源)內嵌資料。

Experience Platform支援從[!DNL Snowflake]資料庫串流資料。

## 瞭解[!DNL Snowflake]串流來源

[!DNL Snowflake]串流來源的運作方式是定期執行SQL查詢來載入資料，並為結果集中的每一列建立輸出記錄。

藉由使用[!DNL Kafka Connect]，[!DNL Snowflake]串流來源會追蹤它從每個資料表收到的最新記錄，以便它可以在下一個反複專案的正確位置開始。 來源使用此功能來篩選資料，並只從每個疊代的表格中取得更新的列。

## 先決條件

以下章節概述從[!DNL Snowflake]資料庫將資料串流到Experience Platform之前要完成的先決條件步驟：

### IP位址允許清單

將來源連線至Experience Platform之前，您必須先將區域特定的IP位址新增至允許清單。 如需詳細資訊，請參閱[允許清單IP位址以連線至Experience Platform](../../ip-address-allow-list.md)的指南以瞭解詳細資訊。

以下檔案提供如何使用API或使用者介面將[!DNL Amazon Redshift]連線至Experience Platform的資訊：

### 收集必要的認證

若要讓[!DNL Flow Service]與[!DNL Snowflake]連線，您必須提供下列連線屬性：

>[!BEGINTABS]

>[!TAB 基本驗證]

| 認證 | 說明 |
| --- | --- |
| `account` | [!DNL Snowflake]帳戶的完整帳戶識別碼（帳戶名稱或帳戶定位器）已附加尾碼`snowflakecomputing.com`。 帳戶識別碼可以是不同的格式： <ul><li>{ORG_NAME}-{ACCOUNT_NAME}.snowflakecomputing.com （例如`acme-abc12345.snowflakecomputing.com`）</li><li>{ACCOUNT_LOCATOR}。{CLOUD_REGION_ID}.snowflakecomputing.com （例如`acme12345.ap-southeast-1.snowflakecomputing.com`）</li><li>{ACCOUNT_LOCATOR}。{CLOUD_REGION_ID}。{CLOUD}.snowflakecomputing.com （例如`acme12345.east-us-2.azure.snowflakecomputing.com`）</li></ul> 如需詳細資訊，請閱讀[[!DNL Snowflake document on account identifiers]](<https://docs.snowflake.com/en/user-guide/admin-account-identifier.html>)。 |
| `warehouse` | [!DNL Snowflake]倉儲管理應用程式的查詢執行程式。 每個[!DNL Snowflake]倉儲彼此獨立，在將資料帶到Experience Platform時必須個別存取。 |
| `database` | [!DNL Snowflake]資料庫包含您要帶入Experience Platform的資料。 |
| `username` | [!DNL Snowflake]帳戶的使用者名稱。 |
| `password` | [!DNL Snowflake]使用者帳戶的密碼。 |
| `role` | （選用）可以為使用者針對指定連線提供的自訂定義角色。 如果未提供，此值會預設為`public`。 |
| `connectionSpec.id` | 連線規格會傳回來源的聯結器屬性，包括與建立基礎連線和來源連線相關的驗證規格。 [!DNL Snowflake]的連線規格識別碼為`51ae16c2-bdad-42fd-9fce-8d5dfddaf140`。 |

>[!TAB 金鑰組驗證]

若要使用金鑰組驗證，您必須產生2048位元RSA金鑰組，然後在建立[!DNL Snowflake]來源的帳戶時提供下列值。

| 認證 | 說明 |
| --- | --- |
| `account` | 帳戶名稱可唯一識別組織內的帳戶。 在此情況下，您必須跨不同的[!DNL Snowflake]組織唯一識別帳戶。 若要這麼做，您必須在帳戶名稱前加上組織名稱。 例如： `orgname-account_name`。 閱讀[擷取 [!DNL Snowflake] 帳戶識別碼](./snowflake.md#retrieve-your-account-identifier)的指南，以取得其他指引。 如需詳細資訊，請參閱[[!DNL Snowflake] 文件](https://docs.snowflake.com/en/user-guide/admin-account-identifier#format-1-preferred-account-name-in-your-organization)，以瞭解詳情。 |
| `username` | 您[!DNL Snowflake]帳戶的使用者名稱。 |
| `privateKey` | 您[!DNL Base64-]帳戶的[!DNL Snowflake]編碼私密金鑰。 您可以產生加密或未加密的私密金鑰。 如果您使用加密的私密金鑰，則在對Experience Platform進行驗證時，也必須提供私密金鑰複雜密碼。 如需詳細資訊，請參閱[擷取 [!DNL Snowflake] 私密金鑰](./snowflake.md)的指南。 |
| `passphrase` | 複雜密碼是附加的安全性層級，在使用加密的私密金鑰進行驗證時必須使用此層級。 如果您使用未加密的私密金鑰，則不需要提供複雜密碼。 |
| `database` | 包含您要擷取至Experience Platform之資料的[!DNL Snowflake]資料庫。 |
| `warehouse` | [!DNL Snowflake]倉儲管理應用程式的查詢執行程式。 每個[!DNL Snowflake]倉儲彼此獨立，在將資料帶到Experience Platform時必須個別存取。 |

如需這些值的詳細資訊，請參閱[[!DNL Snowflake] 金鑰組驗證指南](https://docs.snowflake.com/en/user-guide/key-pair-auth.html)。

>[!ENDTABS]

### 擷取您的帳戶識別碼 {#retrieve-your-account-identifier}

若要使用Experience Platform驗證您的[!DNL Snowflake]執行個體，您必須從[!DNL Snowflake] UI儀表板取得帳戶識別碼。

請依照下列步驟尋找您的帳戶識別碼：

* 在[[!DNL Snowflake] 應用程式UI儀表板](https://app.snowflake.com/)上瀏覽至您的帳戶。
* 在左側導覽中，選取&#x200B;**[!DNL Accounts]**，然後從標頭中選取&#x200B;**[!DNL Active Accounts]**。
* 接著，選取資訊圖示，然後選取並複製目前URL的網域名稱。

### 擷取您的私密金鑰 {#retrieve-your-private-key}

如果您打算針對[!DNL Snowflake]連線使用金鑰組驗證，則必須在連線至Experience Platform之前產生私密金鑰。

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

產生您的私密金鑰後，直接在[!DNL Base64]中進行編碼，無需對其格式或內容進行任何變更。 編碼之前，請確定私密金鑰的結尾沒有額外的空格或空白行（包括結尾的新行）。

### 驗證設定

在建立[!DNL Snowflake]資料的來源連線之前，您還必須確定符合下列設定：

* 指派給特定使用者的預設倉儲必須與您在向Experience Platform進行驗證時輸入的倉儲相同。
* 指派給特定使用者的預設角色，必須能存取您在向Experience Platform進行驗證時輸入的相同資料庫。

若要驗證您的角色與倉儲：

* 在左側導覽中選取&#x200B;**[!DNL Admin]**，然後選取&#x200B;**[!DNL Users & Roles]**。
* 選取適當的使用者，然後選取右上角的省略符號(`...`)。
* 在出現的[!DNL Edit user]視窗中，瀏覽至[!DNL Default Role]以檢視與指定使用者相關聯的角色。
* 在相同視窗中，瀏覽至[!DNL Default Warehouse]以檢視與指定使用者相關聯的倉儲。

成功編碼後，您就可以在Experience Platform上使用該[!DNL Base64]編碼私密金鑰來驗證您的[!DNL Snowflake]帳戶。

### 設定角色設定 {#configure-role-settings}

您必須設定角色的許可權（即使已指派預設公用角色），以允許來源連線存取相關[!DNL Snowflake]資料庫、結構描述和表格。 不同[!DNL Snowflake]個實體的各種許可權如下：

| [!DNL Snowflake]實體 | 需要角色許可權 |
| --- | --- |
| 倉儲 | 操作，使用 |
| 資料庫 | 使用狀況 |
| 結構描述 | 使用狀況 |
| 表格 | 選取 |

>[!NOTE]
>
>您必須在倉儲的進階設定組態中啟用自動恢復和自動暫停。

如需角色與許可權管理的詳細資訊，請參閱[[!DNL Snowflake] API參考](<https://docs.snowflake.com/en/sql-reference/sql/grant-privilege>)。

## 將Unix時間轉換為日期欄位

[!DNL Snowflake Streaming]會剖析並將`DATE`欄位寫入為自Unix紀元以來的天數(1970-01-01)。 例如，`DATE`值為0表示1970年1月1日，而值為1表示1970年1月2日。 因此，在準備檔案以在[!DNL Snowflake Streaming]來源中建立對應時，請確定`DATE`資料行以整數表示。

您可以使用[資料準備資料和時間函式](../../../data-prep/functions.md#date-and-time-functions)，將Unix時間轉換為可擷取至Experience Platform的日期欄位。 例如：

```shell
dformat({DATE_COLUMN} * 86400000, "yyyy-MM-dd")
```

在此函式中：

* `{DATE_COLUMN}`是包含epoch日整數的日期欄。
* 乘以86400000可將epoch天數轉換為毫秒。
* &#39;yyyy-MM-dd&#39;指定需要的日期格式。

此轉換可確保資料集中的日期可正確呈現。


## 限制和常見問答 {#limitations-and-frequently-asked-questions}

* [!DNL Snowflake]來源的資料輸送量為每秒2000筆記錄。
* 訂價會因倉儲的有效時間長短及倉儲大小而有所不同。 對於[!DNL Snowflake]來源整合，最小大小x小型倉儲就足夠了。 建議啟用自動暫停，以便倉儲在不使用時能夠自行暫停。
* [!DNL Snowflake]來源每10秒輪詢資料庫是否有新資料。
* 設定選項：
   * 建立來源連線時，您可以為`backfill`來源啟用[!DNL Snowflake]布林值標幟。
      * 如果回填設為true，則timestamp.initial的值會設為0。 這表示會擷取時間戳記欄超過0紀元時間的資料。
      * 如果回填設為false，則timestamp.initial的值會設為–1。 這表示會擷取時間戳記欄大於目前時間（來源開始擷取的時間）的資料。
   * 時間戳記資料行的格式應該是： `TIMESTAMP_LTZ`或`TIMESTAMP_NTZ`。 如果時間戳記資料行設為`TIMESTAMP_NTZ`，則儲存值的對應時區應透過`timezoneValue`引數傳遞。 如果未提供，此值將預設為UTC。
      * `TIMESTAMP_TZ`不能用於時間戳記資料行或對應中。

## 後續步驟

>[!NOTE]
>
>在您建立或更新串流資料流後，需要短暫暫停資料擷取5分鐘，以防止任何可能的資料遺失或資料中斷情況。

下列教學課程提供如何使用API將您的[!DNL Snowflake]串流來源連線至Experience Platform的步驟：

* [使用流程服務API將資料從 [!DNL Snowflake] 資料庫串流到Experience Platform](../../tutorials/api/create/databases/snowflake-streaming.md)
* [使用Experience Platform使用者介面中的來源工作區將資料從 [!DNL Snowflake] 資料庫串流到Experience Platform](../../tutorials/ui/create/databases/snowflake-streaming.md)
