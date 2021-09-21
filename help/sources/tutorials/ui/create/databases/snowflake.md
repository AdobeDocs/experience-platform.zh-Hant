---
keywords: Experience Platform；首頁；熱門主題；Snowflake
title: 在UI中建立Snowflake來源連線
topic-legacy: overview
type: Tutorial
description: 了解如何使用Adobe Experience Platform UI建立Snowflake來源連線。
source-git-commit: 2e717f33b487430220bd3bb7812558cde81d8852
workflow-type: tm+mt
source-wordcount: '431'
ht-degree: 1%

---

# 在UI中建立[!DNL Snowflake]源連接

>[!NOTE]
>
> [!DNL Snowflake]連接器為測試版。 有關使用測試版標籤連接器的詳細資訊，請參閱[來源概述](../../../../home.md#terms-and-conditions)。

本教學課程提供使用Adobe Experience Platform使用者介面建立[!DNL Snowflake]來源連接器的步驟。

## 快速入門

本教學課程需要妥善了解Platform的下列元件：

* [來源](../../../../home.md): [!DNL Experience Platform] 可讓您從各種來源擷取資料，同時使用服務來建構、加標籤及增強傳入 [!DNL Platform] 資料。
* [沙箱](../../../../../sandboxes/home.md): [!DNL Experience Platform] 提供可將單一執行個體分割成個 [!DNL Platform] 別虛擬環境的虛擬沙箱，以協助開發及改進數位體驗應用程式。

### 收集所需憑據

若要在[!DNL Platform]上存取您的Snowflake帳戶，您必須提供下列驗證值：

| 憑據 | 說明 |
| ---------- | ----------- |
| 帳戶 | 要連接到Platform的[!DNL Snowflake]帳戶。 |
| 倉庫 | [!DNL Snowflake]倉庫管理應用程式的查詢執行過程。 每個[!DNL Snowflake]倉庫彼此獨立，在將資料傳至Platform時必須個別存取。 |
| 資料庫 | [!DNL Snowflake]包含您要帶入平台的資料。 |
| 使用者名稱 | [!DNL Snowflake]帳戶的用戶名。 |
| 密碼 | [!DNL Snowflake]用戶帳戶的密碼。 |
| 連線字串 | 用於連接到[!DNL Snowflake]實例的連接字串。 [!DNL Snowflake]的連接字串模式為`jdbc:snowflake://{ACCOUNT_NAME}.snowflakecomputing.com/?user={USERNAME}&password={PASSWORD}&db={DATABASE}&warehouse={WAREHOUSE}`。 |

有關這些值的詳細資訊，請參閱[此Snowflake文檔](https://docs.snowflake.com/en/user-guide/oauth-custom.html)。

## 連接您的Snowflake帳戶

在平台UI中，從左側導覽中選取&#x200B;**[!UICONTROL Sources]**&#x200B;以存取[!UICONTROL Sources]工作區。 [!UICONTROL 目錄]畫面會顯示您可以用來建立帳戶的各種來源。

您可以從畫面左側的目錄中選取適當的類別。 或者，您也可以使用搜尋列找到您要使用的特定來源。

在[!UICONTROL 資料庫]類別下，選擇&#x200B;**[!UICONTROL Snowflake]**，然後選擇&#x200B;**[!UICONTROL 添加資料]**。

![](../../../../images/tutorials/create/snowflake/catalog.png)

此時將顯示&#x200B;**[!UICONTROL 連接到Snowflake]**&#x200B;頁。 在此頁面上，您可以使用新憑證或現有憑證。

### 現有帳戶

要連接現有帳戶，請選擇要連接的Snowflake帳戶，然後選擇&#x200B;**[!UICONTROL Next]**&#x200B;以繼續。

![](../../../../images/tutorials/create/snowflake/existing.png)

### 新帳戶

如果您正在使用新憑據，請選擇&#x200B;**[!UICONTROL 新帳戶]**。 在顯示的輸入表單中，提供名稱、選用說明和您的Snowflake憑證。 完成後，選擇&#x200B;**[!UICONTROL Connect]**，然後允許一些時間建立新連接。

![](../../../../images/tutorials/create/snowflake/new.png)

## 後續步驟

依照本教學課程，您已建立與Snowflake帳戶的連線。 您現在可以繼續下一個教程，並[配置資料流以將資料帶入 [!DNL Platform]](../../dataflow/databases.md)。
