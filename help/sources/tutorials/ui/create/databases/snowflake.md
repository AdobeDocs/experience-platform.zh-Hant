---
keywords: Experience Platform；首頁；熱門主題；Snowflake
title: 在UI中建立Snowflake來源連線
type: Tutorial
description: 了解如何使用Adobe Experience Platform UI建立Snowflake來源連線。
exl-id: fb2038b9-7f27-4818-b5de-cc8072122127
source-git-commit: ed92bdcd965dc13ab83649aad87eddf53f7afd60
workflow-type: tm+mt
source-wordcount: '445'
ht-degree: 2%

---

# 建立 [!DNL Snowflake] UI中的源連接

本教學課程提供建立 [!DNL Snowflake] 來源連接器(使用Adobe Experience Platform使用者介面)。

## 快速入門

本教學課程需要妥善了解Platform的下列元件：

* [來源](../../../../home.md): [!DNL Experience Platform] 可讓您從各種來源擷取資料，同時使用來建構、加標籤及增強傳入資料 [!DNL Platform] 服務。
* [沙箱](../../../../../sandboxes/home.md): [!DNL Experience Platform] 提供可分割單一沙箱的虛擬沙箱 [!DNL Platform] 例項放入個別的虛擬環境，以協助開發及改進數位體驗應用程式。

### 收集所需憑據

若要存取您的Snowflake帳戶，請依 [!DNL Platform]，您必須提供下列驗證值：

| 憑據 | 說明 |
| ---------- | ----------- |
| 帳戶 | 與您的 [!DNL Snowflake] 帳戶。 完全合格 [!DNL Snowflake] 帳戶名稱包含您的帳戶名稱、地區和雲端平台。 例如 `cj12345.east-us-2.azure`。有關帳戶名稱的詳細資訊，請參閱 [[!DNL Snowflake document on account identifiers]](https://docs.snowflake.com/en/user-guide/admin-account-identifier.html). |
| 倉庫 | 此 [!DNL Snowflake] 倉庫管理應用程式的查詢執行過程。 每個 [!DNL Snowflake] 倉庫彼此獨立，且在將資料移至Platform時必須個別存取。 |
| 資料庫 | 此 [!DNL Snowflake] 資料庫包含您要帶入Platform的資料。 |
| 使用者名稱 | 的使用者名稱 [!DNL Snowflake] 帳戶。 |
| 密碼 | 的密碼 [!DNL Snowflake] 使用者帳戶。 |
| 連線字串 | 用來連線至您的 [!DNL Snowflake] 例項。 的連接字串模式 [!DNL Snowflake] is `jdbc:snowflake://{ACCOUNT_NAME}.snowflakecomputing.com/?user={USERNAME}&password={PASSWORD}&db={DATABASE}&warehouse={WAREHOUSE}` |

如需這些值的詳細資訊，請參閱 [此Snowflake文檔](https://docs.snowflake.com/en/user-guide/key-pair-auth.html).

## 連接您的Snowflake帳戶

在平台UI中，選取 **[!UICONTROL 來源]** 從左側導覽器存取 [!UICONTROL 來源] 工作區。 此 [!UICONTROL 目錄] 畫面會顯示您可以用來建立帳戶的各種來源。

您可以從畫面左側的目錄中選取適當的類別。 或者，您也可以使用搜尋列找到您要使用的特定來源。

在 [!UICONTROL 資料庫] 類別，選擇 **[!UICONTROL Snowflake]** 然後選取 **[!UICONTROL 新增資料]**.

![](../../../../images/tutorials/create/snowflake/catalog.png)

此 **[!UICONTROL 連接到Snowflake]** 頁。 在此頁面上，您可以使用新憑證或現有憑證。

### 現有帳戶

若要連線現有帳戶，請選取您要連線的Snowflake帳戶，然後選取 **[!UICONTROL 下一個]** 繼續。

![](../../../../images/tutorials/create/snowflake/existing.png)

### 新帳戶

如果使用新憑據，請選擇 **[!UICONTROL 新帳戶]**. 在顯示的輸入表單中，提供名稱、選用說明和您的Snowflake憑證。 完成後，請選取 **[!UICONTROL Connect]** 然後讓新連接建立一段時間。

![](../../../../images/tutorials/create/snowflake/new.png)

## 後續步驟

依照本教學課程，您已建立與Snowflake帳戶的連線。 您現在可以繼續下一個教學課程，以及 [配置資料流以將資料帶入 [!DNL Platform]](../../dataflow/databases.md).
