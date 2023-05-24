---
keywords: Experience Platform；首頁；熱門主題；Snowflake
title: 在UI中建立Snowflake源連接
type: Tutorial
description: 瞭解如何使用Adobe Experience PlatformUI建立Snowflake源連接。
exl-id: fb2038b9-7f27-4818-b5de-cc8072122127
source-git-commit: ed92bdcd965dc13ab83649aad87eddf53f7afd60
workflow-type: tm+mt
source-wordcount: '445'
ht-degree: 2%

---

# 建立 [!DNL Snowflake] UI中的源連接

本教程提供建立 [!DNL Snowflake] 使用Adobe Experience Platform用戶介面的源連接器。

## 快速入門

本教程需要瞭解平台的以下元件：

* [源](../../../../home.md): [!DNL Experience Platform] 允許從各種源接收資料，同時讓您能夠使用 [!DNL Platform] 服務。
* [沙箱](../../../../../sandboxes/home.md): [!DNL Experience Platform] 提供虛擬沙箱，將單個沙箱 [!DNL Platform] 實例到獨立的虛擬環境，以幫助開發和發展數字型驗應用程式。

### 收集所需憑據

為了訪問您的Snowflake帳戶 [!DNL Platform]，必須提供以下驗證值：

| 憑據 | 說明 |
| ---------- | ----------- |
| 帳戶 | 與您的 [!DNL Snowflake] 帳戶。 完全合格 [!DNL Snowflake] 帳戶名包括您的帳戶名、區域和雲平台。 例如 `cj12345.east-us-2.azure`。有關帳戶名的詳細資訊，請參閱 [[!DNL Snowflake document on account identifiers]](https://docs.snowflake.com/en/user-guide/admin-account-identifier.html)。 |
| 倉庫 | 的 [!DNL Snowflake] 倉庫管理應用程式的查詢執行過程。 每個 [!DNL Snowflake] 倉庫彼此獨立，在將資料傳送到平台時必須單獨訪問。 |
| 資料庫 | 的 [!DNL Snowflake] 資料庫包含要帶入平台的資料。 |
| 用戶名 | 用戶名 [!DNL Snowflake] 帳戶。 |
| 密碼 | 的密碼 [!DNL Snowflake] 用戶帳戶。 |
| 連接字串 | 用於連接到您的 [!DNL Snowflake] 實例。 的連接字串模式 [!DNL Snowflake] 是 `jdbc:snowflake://{ACCOUNT_NAME}.snowflakecomputing.com/?user={USERNAME}&password={PASSWORD}&db={DATABASE}&warehouse={WAREHOUSE}` |

有關這些值的詳細資訊，請參閱 [此Snowflake文檔](https://docs.snowflake.com/en/user-guide/key-pair-auth.html)。

## 連接Snowflake帳戶

在平台UI中，選擇 **[!UICONTROL 源]** 從左側導航 [!UICONTROL 源] 工作區。 的 [!UICONTROL 目錄] 螢幕顯示可建立帳戶的各種源。

可以從螢幕左側的目錄中選擇相應的類別。 或者，您可以使用搜索欄找到要使用的特定源。

在 [!UICONTROL 資料庫] 類別，選擇 **[!UICONTROL Snowflake]** ，然後選擇 **[!UICONTROL 添加資料]**。

![](../../../../images/tutorials/create/snowflake/catalog.png)

的 **[!UICONTROL 連接到Snowflake]** 的子菜單。 在此頁上，您可以使用新憑據或現有憑據。

### 現有帳戶

要連接現有帳戶，請選擇要連接的Snowflake帳戶，然後選擇 **[!UICONTROL 下一個]** 繼續。

![](../../../../images/tutorials/create/snowflake/existing.png)

### 新帳戶

如果使用新憑據，請選擇 **[!UICONTROL 新帳戶]**。 在顯示的輸入表單上，提供名稱、可選說明和您的Snowflake憑據。 完成後，選擇 **[!UICONTROL 連接]** 然後再給新連接建立一段時間。

![](../../../../images/tutorials/create/snowflake/new.png)

## 後續步驟

按照本教程，您已建立了與Snowflake帳戶的連接。 現在，您可以繼續下一個教程， [配置資料流以將資料 [!DNL Platform]](../../dataflow/databases.md)。
