---
title: Snowflake Source聯結器總覽
description: 瞭解如何使用API或使用者介面將Snowflake連線至Adobe Experience Platform。
badgeUltimate: label="Ultimate" type="Positive"
exl-id: df066463-1ae6-4ecd-ae0e-fb291cec4bd5
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '694'
ht-degree: 0%

---

# [!DNL Snowflake]來源

>[!IMPORTANT]
>
>* [!DNL Snowflake]來源可在來源目錄中提供給已購買Real-Time Customer Data Platform Ultimate的使用者。
>* 根據預設，[!DNL Snowflake]來源會將`null`解譯為空字串。 請聯絡您的Adobe代表，以確保您的`null`值在Adobe Experience Platform中正確寫入`null`。
>* 為了讓Experience Platform擷取資料，所有表格型批次來源的時區都必須設定為UTC。 [!DNL Snowflake]來源唯一支援的時間戳記是TIMESTAMP_NTZ與UTC時間。

Adobe Experience Platform可讓您從外部來源擷取資料，同時使用Experience Platform服務來建構、加標籤及增強傳入資料。 您可以從多種來源(例如Adobe應用程式、雲端儲存、資料庫和許多其他來源)內嵌資料。

Experience Platform支援從協力廠商資料庫擷取資料。 Experience Platform可連線至不同型別的資料庫，例如關聯式、NoSQL或資料倉儲。 支援的資料庫提供者包括[!DNL Snowflake]。

## 先決條件 {#prerequisites}

本節概述將[!DNL Snowflake]來源連線至Experience Platform之前，需要完成的設定工作。

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
-----BEGIN ENCRYPTED PRIVATE KEY-----
MIIE6T...
-----END ENCRYPTED PRIVATE KEY-----
```

>[!TAB 建立未加密的私密金鑰]

若要產生未加密的[!DNL Snowflake]私密金鑰，請在終端機上執行下列命令：

```shell
openssl genrsa 2048 | openssl pkcs8 -topk8 -inform PEM -out rsa_key.p8 -nocrypt
```

如果成功，您應該會收到PEM格式的私密金鑰。

```shell
-----BEGIN PRIVATE KEY-----
MIIE6T...
-----END PRIVATE KEY-----
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

## IP位址允許清單

使用來源聯結器之前，必須將IP位址清單新增至允許清單。 未能將您區域特定的IP位址新增到允許清單可能會導致使用來源時的錯誤或效能不佳。 如需詳細資訊，請參閱[IP位址允許清單](../../ip-address-allow-list.md)頁面。

以下檔案提供如何使用API或使用者介面將[!DNL Snowflake]連線至Experience Platform的資訊：

## 使用API連線[!DNL Snowflake]至Experience Platform

* [使用Flow Service API建立Snowflake基本連線](../../tutorials/api/create/databases/snowflake.md)
* [使用流量服務API探索資料表](../../tutorials/api/explore/tabular.md)
* [使用流程服務API為資料庫來源建立資料流](../../tutorials/api/collect/database-nosql.md)

## 使用UI連線[!DNL Snowflake]至Experience Platform

* [在UI中建立Snowflake來源連線](../../tutorials/ui/create/databases/snowflake.md)
* [在UI中建立資料庫來源連線的資料流](../../tutorials/ui/dataflow/databases.md)
