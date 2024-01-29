---
title: 在使用者介面中建立Snowflake來源連線
type: Tutorial
description: 瞭解如何使用Adobe Experience Platform UI建立Snowflake來源連線。
badgeUltimate: label="Ultimate" type="Positive"
exl-id: fb2038b9-7f27-4818-b5de-cc8072122127
source-git-commit: 4de2193a45fc2925af310b5e2475eabe26d13adc
workflow-type: tm+mt
source-wordcount: '786'
ht-degree: 1%

---

# 建立 [!DNL Snowflake] ui中的來源連線

>[!IMPORTANT]
>
>此 [!DNL Snowflake] 已購買Real-time Customer Data Platform Ultimate的使用者可在來源目錄中取得來源。

本教學課程提供建立 [!DNL Snowflake] 來源聯結器，使用Adobe Experience Platform使用者介面。

## 快速入門

本教學課程需要您實際瞭解下列Experience Platform元件：

* [來源](../../../../home.md)： [!DNL Experience Platform] 允許從各種來源擷取資料，同時讓您能夠使用以下專案來建構、加標籤及增強傳入資料 [!DNL Platform] 服務。
* [沙箱](../../../../../sandboxes/home.md)： [!DNL Experience Platform] 提供分割單一區域的虛擬沙箱 [!DNL Platform] 將執行個體整合至個別的虛擬環境中，協助開發及改進數位體驗應用程式。

### 收集必要的認證

您必須提供下列認證屬性的值，才能驗證您的 [!DNL Snowflake] 來源。

>[!BEGINTABS]

>[!TAB 帳戶金鑰驗證]

| 認證 | 說明 |
| ---------- | ----------- |
| 帳戶 | 帳戶名稱可唯一識別組織內的帳戶。 在此情況下，您必須唯一識別跨不同帳戶的身分 [!DNL Snowflake] 組織。 若要這麼做，您必須在帳戶名稱前加上組織名稱。 例如: `orgname-account_name`。如需帳戶名稱的詳細資訊，請參閱 [!DNL Snowflake] 檔案： [帳戶識別碼](https://docs.snowflake.com/en/user-guide/admin-account-identifier#format-1-preferred-account-name-in-your-organization). |
| 倉儲 | 此 [!DNL Snowflake] warehouse會管理應用程式的查詢執行程式。 每個 [!DNL Snowflake] Warehouse彼此獨立，將資料帶到Platform時必須個別存取。 |
| 資料庫 | 此 [!DNL Snowflake] 資料庫包含您要帶入Platform的資料。 |
| 使用者名稱 | 的使用者名稱 [!DNL Snowflake] 帳戶。 |
| 密碼 | 的密碼 [!DNL Snowflake] 使用者帳戶。 |
| 角色 | 要使用的預設存取控制角色 [!DNL Snowflake] 工作階段。 該角色應為已指派給指定使用者的現有角色。 預設角色為 `PUBLIC`. |
| 連線字串 | 用來連線至您的裝置的連線字串 [!DNL Snowflake] 執行個體。 的連線字串模式 [!DNL Snowflake] 是 `jdbc:snowflake://{ACCOUNT_NAME}.snowflakecomputing.com/?user={USERNAME}&password={PASSWORD}&db={DATABASE}&warehouse={WAREHOUSE}` |

>[!TAB 金鑰組驗證]

若要使用金鑰組驗證，您必須產生2048位元RSA金鑰組，然後在建立帳戶時提供下列值 [!DNL Snowflake] 來源。

| 認證 | 說明 |
| --- | --- |
| 帳戶 | 帳戶名稱可唯一識別組織內的帳戶。 在此情況下，您必須唯一識別跨不同帳戶的身分 [!DNL Snowflake] 組織。 若要這麼做，您必須在帳戶名稱前加上組織名稱。 例如: `orgname-account_name`。如需帳戶名稱的詳細資訊，請參閱 [!DNL Snowflake] 檔案： [帳戶識別碼](https://docs.snowflake.com/en/user-guide/admin-account-identifier#format-1-preferred-account-name-in-your-organization). |
| 使用者名稱 | 您的使用者名稱 [!DNL Snowflake] 帳戶。 |
| 私密金鑰 | 此 [!DNL Base64-]您的加密私密金鑰 [!DNL Snowflake] 帳戶。 您可以產生加密或未加密的私密金鑰。 如果您使用加密的私密金鑰，則在針對Experience Platform進行驗證時，也必須提供私密金鑰複雜密碼。 |
| 私密金鑰複雜密碼 | 私密金鑰複雜密碼是附加的安全性層級，在使用加密的私密金鑰進行驗證時必須使用此層級。 如果您使用未加密的私密金鑰，則不需要提供複雜密碼。 |
| 資料庫 | 此 [!DNL Snowflake] 包含您要擷取以Experience Platform之資料的資料庫。 |
| 倉儲 | 此 [!DNL Snowflake] warehouse會管理應用程式的查詢執行程式。 每個 [!DNL Snowflake] Warehouse彼此獨立，將資料帶到Platform時必須個別存取。 |

如需這些值的詳細資訊，請參閱 [此Snowflake檔案](https://docs.snowflake.com/en/user-guide/key-pair-auth.html).

>[!ENDTABS]

若要在Experience Platform上存取您的Snowflake帳戶，您必須提供下列驗證值：

>[!NOTE]
>
>您必須設定 `PREVENT_UNLOAD_TO_INLINE_URL` 標幟到 `FALSE` 允許從解除安裝資料 [!DNL Snowflake] 要Experience Platform的資料庫

## 連線您的Snowflake帳戶

在Platform UI中選取 **[!UICONTROL 來源]** 從左側導覽存取 [!UICONTROL 來源] 工作區。

您可以從熒幕左側的目錄中選取適當的類別。 或者，您可以使用搜尋列來尋找您要使用的特定來源。

在 [!UICONTROL 資料庫] 類別，選取 **[!UICONTROL Snowflake]** 然後選取 **[!UICONTROL 新增資料]**.

![來源目錄與 [!DNL Snowflake] 反白顯示。](../../../../images/tutorials/create/snowflake/catalog.png)

此 **[!UICONTROL 連線到Snowflake]** 頁面便會顯示。 您可以在此頁面使用新的證明資料或現有的證明資料。

### 現有帳戶

若要使用現有帳戶，請選取 [!DNL Snowflake] 您要連線的帳戶，然後選取 **[!UICONTROL 下一個]** 以繼續進行。

![來源工作流程中的現有帳戶介面。](../../../../images/tutorials/create/snowflake/existing.png)

### 新帳戶

若要建立新帳戶，請選取 **[!UICONTROL 新帳戶]**，然後為您的新專案提供名稱和說明（選用） [!DNL Snowflake] 帳戶。

![來源工作流程中的新帳戶介面。](../../../../images/tutorials/create/snowflake/new.png)

>[!BEGINTABS]

>[!TAB 帳戶金鑰驗證]

若要使用帳戶金鑰驗證，請在輸入表單中提供您的連線字串，然後選取 **[!UICONTROL 連線到來源]**.

![帳戶金鑰驗證介面。](../../../../images/tutorials/create/snowflake/connection-string.png)

>[!TAB 金鑰組驗證]

若要使用金鑰組驗證，請提供帳戶、使用者名稱、私密金鑰、私密金鑰密碼、資料庫和倉儲的值，然後選取 **[!UICONTROL 連線到來源]**.

![帳戶金鑰組驗證介面。](../../../../images/tutorials/create/snowflake/key-pair.png)

>[!ENDTABS]

## 後續步驟

依照本教學課程中的指示，您已建立與Snowflake帳戶的連線。 您現在可以繼續進行下一個教學課程及 [設定資料流以將資料帶入 [!DNL Platform]](../../dataflow/databases.md).
