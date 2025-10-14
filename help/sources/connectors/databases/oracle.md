---
title: Oracle DB Source聯結器總覽
description: 瞭解如何使用API或使用者介面將Oracle連線至Adobe Experience Platform。
last-substantial-update: 2025-08-06T00:00:00Z
exl-id: be422cf8-fb24-48c7-8369-34f0f2ec95fc
source-git-commit: aa5496be968ee6f117649a6fff2c9e83a4ed7681
workflow-type: tm+mt
source-wordcount: '477'
ht-degree: 2%

---

# [!DNL Oracle DB]

[!DNL Oracle DB]是由[!DNL Oracle Corporation]開發的功能強大的關聯式資料庫管理系統。 您可以使用[!DNL Oracle DB]來有效且安全地儲存、管理及擷取大量結構化資料。

使用Adobe Experience Platform來源目錄中的[!DNL Oracle DB]來源連線您的資料庫並將資料擷取到Experience Platform。

## 先決條件 {#prerequisites}

請先閱讀下列章節，完成先決條件設定，然後再將[!DNL Oracle DB]帳戶連線至Experience Platform。

### IP位址允許清單

在Azure或Amazon Web Services (AWS)上將來源連線至Experience Platform之前，您必須將區域特定的IP位址新增至允許清單。 如需詳細資訊，請參閱[允許清單IP位址指南，以連線至Azure和AWS上的Experience Platform &#x200B;](../../ip-address-allow-list.md)以取得詳細資訊。

### 在Azure上驗證Experience Platform {#azure}

提供連線字串以驗證並將您的[!DNL Oracle DB]帳戶連線至Azure上的Experience Platform。

| 認證 | 說明 |
| --- | --- |
| 連接字串 | 連線字串是應用程式用來連線資料庫的文字字串。 [!DNL Oracle DB]連線字串模式為： `Host={HOST};Port={PORT};Sid={SID};User Id={USERNAME};Password={PASSWORD}`。 |
| 連線規格ID | 連線規格ID會傳回來源的連線器屬性，包括與建立基礎連線和來源連線相關的驗證規格。 [!DNL Oracle]的連線規格識別碼為`d6b52d86-f0f8-475f-89d4-ce54c8527328`。 **注意**：只有在透過[!DNL Flow Service] API連線時才需要此認證。 |

### 在Amazon Web Services上驗證Experience Platform {#aws}

>[!AVAILABILITY]
>
>本節適用於在Amazon Web Services (AWS)上執行的Experience Platform實作。 目前有限數量的客戶可使用在AWS上執行的Experience Platform 。 若要進一步瞭解支援的Experience Platform基礎結構，請參閱[Experience Platform多雲端總覽](../../../landing/multi-cloud.md)。

提供下列認證的值，以驗證並將您的[!DNL Oracle DB]帳戶連線至AWS上的Experience Platform。

| 認證 | 說明 |
| --- | --- |
| 伺服器 | [!DNL Oracle DB]伺服器的IP位址或主機名稱。 |
| 連接埠 | 資料庫伺服器的連線埠號碼。 預設連線埠號碼為`1521`。 |
| 使用者名稱 | 用於驗證及存取資料庫的[!DNL Oracle DB]使用者帳戶。 |
| 密碼 | 與您的使用者名稱相關聯的秘密金鑰，用於驗證。 |
| 資料庫 | 您要連線的特定[!DNL Oracle]資料庫執行個體。 |
| 結構描述 | 資料庫物件的容器，例如表格、檢視表或程式。 |
| SSL模式 | 布林值，控制是否強制執行SSL。 此設定取決於您的伺服器支援，預設值為`false`。 |
| 連線規格ID | 連線規格ID會傳回來源的連線器屬性，包括與建立基礎連線和來源連線相關的驗證規格。 [!DNL Oracle]的連線規格識別碼為`d6b52d86-f0f8-475f-89d4-ce54c8527328`。 **注意**：只有在透過[!DNL Flow Service] API連線時才需要此認證。 |


## 使用API連線[!DNL Oracle]至[!DNL Experience Platform]

- [使用流量服務API連線Oracle DB](../../tutorials/api/create/databases/oracle.md)
- [使用流量服務API探索資料表](../../tutorials/api/explore/tabular.md)
- [使用流程服務API為資料庫來源建立資料流](../../tutorials/api/collect/database-nosql.md)

## 使用UI連線[!DNL Oracle]至[!DNL Experience Platform]

- [使用Oracle UI工作區連線Experience Platform DB。](../../tutorials/ui/create/databases/oracle.md)
- [在UI中建立資料庫來源連線的資料流](../../tutorials/ui/dataflow/databases.md)
