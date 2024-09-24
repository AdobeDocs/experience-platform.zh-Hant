---
title: 在UI中建立Snowflake Source連線
type: Tutorial
description: 瞭解如何使用Adobe Experience Platform UI建立Snowflake來源連線。
badgeUltimate: label="Ultimate" type="Positive"
exl-id: fb2038b9-7f27-4818-b5de-cc8072122127
source-git-commit: ae322ee421edd73cd5a3fb8499267cd417491318
workflow-type: tm+mt
source-wordcount: '886'
ht-degree: 3%

---

# 在使用者介面中建立[!DNL Snowflake]來源連線

>[!IMPORTANT]
>
>[!DNL Snowflake]來源可在來源目錄中提供給已購買Real-time Customer Data Platform Ultimate的使用者。

本教學課程提供使用Adobe Experience Platform使用者介面建立[!DNL Snowflake]來源聯結器的步驟。

## 快速入門

本教學課程需要您實際瞭解下列Experience Platform元件：

* [來源](../../../../home.md)： [!DNL Experience Platform]允許從各種來源擷取資料，同時讓您能夠使用[!DNL Platform]服務來建構、加標籤以及增強傳入的資料。
* [沙箱](../../../../../sandboxes/home.md)： [!DNL Experience Platform]提供可將單一[!DNL Platform]執行個體分割成個別虛擬環境的虛擬沙箱，以利開發及改進數位體驗應用程式。

### 收集必要的認證

您必須提供下列認證屬性的值，才能驗證您的[!DNL Snowflake]來源。

>[!BEGINTABS]

>[!TAB 帳戶金鑰驗證]

| 認證 | 說明 |
| ---------- | ----------- |
| 帳戶 | 帳戶名稱可唯一識別組織內的帳戶。 在此情況下，您必須跨不同的[!DNL Snowflake]組織唯一識別帳戶。 若要這麼做，您必須在帳戶名稱前加上組織名稱。 例如： `orgname-account_name`。 閱讀[擷取 [!DNL Snowflake] 帳戶識別碼](../../../../connectors/databases/snowflake.md#retrieve-your-account-identifier)的指南，以取得其他指引。 如需詳細資訊，請參閱[[!DNL Snowflake] 文件](https://docs.snowflake.com/en/user-guide/admin-account-identifier#format-1-preferred-account-name-in-your-organization)，以瞭解詳情。 |
| 倉儲 | [!DNL Snowflake]倉儲管理應用程式的查詢執行程式。 每個[!DNL Snowflake]倉儲彼此獨立，在將資料傳送至Platform時必須個別存取。 |
| 資料庫 | [!DNL Snowflake]資料庫包含您要帶入Platform的資料。 |
| 使用者名稱 | [!DNL Snowflake]帳戶的使用者名稱。 |
| 密碼 | [!DNL Snowflake]使用者帳戶的密碼。 |
| 角色 | 在[!DNL Snowflake]工作階段中使用的預設存取控制角色。 該角色應為已指派給指定使用者的現有角色。 預設角色為`PUBLIC`。 |
| 連接字串 | 用來連線至您[!DNL Snowflake]執行個體的連線字串。 [!DNL Snowflake]的連線字串模式為`jdbc:snowflake://{ACCOUNT_NAME}.snowflakecomputing.com/?user={USERNAME}&password={PASSWORD}&db={DATABASE}&warehouse={WAREHOUSE}` |

>[!TAB 金鑰組驗證]

若要使用金鑰組驗證，您必須產生2048位元RSA金鑰組，然後在建立[!DNL Snowflake]來源的帳戶時提供下列值。

| 認證 | 說明 |
| --- | --- |
| 帳戶 | 帳戶名稱可唯一識別組織內的帳戶。 在此情況下，您必須跨不同的[!DNL Snowflake]組織唯一識別帳戶。 若要這麼做，您必須在帳戶名稱前加上組織名稱。 例如： `orgname-account_name`。 閱讀[擷取 [!DNL Snowflake] 帳戶識別碼](../../../../connectors/databases/snowflake.md#retrieve-your-account-identifier)的指南，以取得其他指引。 如需詳細資訊，請參閱[[!DNL Snowflake] 文件](https://docs.snowflake.com/en/user-guide/admin-account-identifier#format-1-preferred-account-name-in-your-organization)，以瞭解詳情。 |
| 使用者名稱 | 您[!DNL Snowflake]帳戶的使用者名稱。 |
| 私密金鑰 | 您[!DNL Snowflake]帳戶的[!DNL Base64-]編碼私密金鑰。 您可以產生加密或未加密的私密金鑰。 如果您使用加密的私密金鑰，則在針對Experience Platform進行驗證時，也必須提供私密金鑰複雜密碼。 如需詳細資訊，請參閱[擷取 [!DNL Snowflake] 私密金鑰](../../../../connectors/databases/snowflake.md)的指南。 |
| 私密金鑰複雜密碼 | 私密金鑰複雜密碼是附加的安全性層級，在使用加密的私密金鑰進行驗證時必須使用此層級。 如果您使用未加密的私密金鑰，則不需要提供複雜密碼。 |
| 資料庫 | 包含您要擷取以Experience Platform之資料的[!DNL Snowflake]資料庫。 |
| 倉儲 | [!DNL Snowflake]倉儲管理應用程式的查詢執行程式。 每個[!DNL Snowflake]倉儲彼此獨立，在將資料傳送至Platform時必須個別存取。 |

如需這些值的詳細資訊，請參閱[此Snowflake檔案](https://docs.snowflake.com/en/user-guide/key-pair-auth.html)。

>[!ENDTABS]

>[!NOTE]
>
>您必須將`PREVENT_UNLOAD_TO_INLINE_URL`標幟設定為`FALSE`，以允許從[!DNL Snowflake]資料庫解除安裝資料以Experience Platform。

## 連線您的Snowflake帳戶

在Platform UI中，從左側導覽選取&#x200B;**[!UICONTROL 來源]**&#x200B;以存取[!UICONTROL 來源]工作區。

您可以從熒幕左側的目錄中選取適當的類別。 或者，您可以使用搜尋列來尋找您要使用的特定來源。

在[!UICONTROL 資料庫]類別下，選取&#x200B;**[!UICONTROL Snowflake]**，然後選取&#x200B;**[!UICONTROL 新增資料]**。

![標示有[!DNL Snowflake]的來源目錄。](../../../../images/tutorials/create/snowflake/catalog.png)

**[!UICONTROL 連線至Snowflake]**&#x200B;頁面隨即顯示。 您可以在此頁面使用新的證明資料或現有的證明資料。

### 現有帳戶

若要使用現有的帳戶，請選取您要連線的[!DNL Snowflake]帳戶，然後選取[下一步]**[!UICONTROL 以繼續。]**

![來源工作流程中的現有帳戶介面。](../../../../images/tutorials/create/snowflake/existing.png)

### 新帳戶

若要建立新帳戶，請選取&#x200B;**[!UICONTROL 新帳戶]**，然後為您的新[!DNL Snowflake]帳戶提供名稱和選擇性描述。

![來源工作流程中的新帳戶介面。](../../../../images/tutorials/create/snowflake/new.png)

>[!BEGINTABS]

>[!TAB 帳戶金鑰驗證]

若要使用帳戶金鑰驗證，請在輸入表單中提供您的連線字串，然後選取&#x200B;**[!UICONTROL 連線到來源]**。

![帳戶金鑰驗證介面。](../../../../images/tutorials/create/snowflake/connection-string.png)

>[!TAB 金鑰組驗證]

若要使用金鑰組驗證，請提供帳戶、使用者名稱、私密金鑰、私密金鑰密碼、資料庫和倉儲的值，然後選取&#x200B;**[!UICONTROL 連線到來源]**。

![帳戶金鑰組驗證介面。](../../../../images/tutorials/create/snowflake/key-pair.png)

>[!ENDTABS]

### 略過範例資料預覽 {#skip-preview-of-sample-data}

在資料選擇步驟中，您可能會在擷取大型資料表或資料檔案時遭遇逾時。 您可以略過資料預覽以避開逾時，並且仍可檢視您的結構描述，不過沒有範例資料。 若要略過資料預覽，請啟用&#x200B;**[!UICONTROL 略過預覽範例資料]**&#x200B;切換按鈕。

工作流程的其餘部分將維持不變。 唯一的警告是，略過資料預覽可能會阻止在對應步驟期間自動驗證計算和必填欄位，然後您就必須在對應期間手動驗證這些欄位。

## 後續步驟

依照本教學課程中的指示，您已建立與Snowflake帳戶的連線。 您現在可以繼續進行下一個教學課程，並[設定資料流以將資料帶入 [!DNL Platform]](../../dataflow/databases.md)。
