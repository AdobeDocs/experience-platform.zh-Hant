---
keywords: Experience Platform；首頁；熱門主題；Teradata
title: 在UI中建立TeradataVantage源連接
description: 瞭解如何使用Adobe Experience PlatformUI建立TeradataVantage源連接。
source-git-commit: f140dac67ccd09ec1e6cab794f53e0090af55442
workflow-type: tm+mt
source-wordcount: '394'
ht-degree: 1%

---

# (Beta)建立 [!DNL Teradata Vantage] UI中的源連接

>[!NOTE]
>
> 的 [!DNL Teradata Vantage] 源為beta。 查看 [源概述](../../../../home.md#terms-and-conditions) 的子菜單。

本教程提供建立 [!DNL Teradata Vantage] 使用Adobe Experience Platform用戶介面的源連接器。

## 快速入門

本教程需要瞭解平台的以下元件：

* [源](../../../../home.md):Experience Platform允許從各種源接收資料，同時讓您能夠使用Experience Platform服務構建、標籤和增強傳入資料。
* [沙箱](../../../../../sandboxes/home.md):Experience Platform提供虛擬沙箱，將單個平台實例分區為獨立的虛擬環境，以幫助開發和發展數字型驗應用程式。

### 收集所需憑據

為了訪問 [!DNL Teradata Vantage] 帳戶，必須提供以下驗證值：

| 憑據 | 說明 |
| ---------- | ----------- |
| 連接字串 | 連接字串是提供有關資料源以及如何連接到資料源的資訊的字串。 的連接字串模式 [!DNL Teradata Vantage] 是 `DBCName={SERVER};Uid={USERNAME};Pwd={PASSWORD}`。 |

有關入門的詳細資訊，請參閱此 [[!DNL Teradata Vantage] 文檔](https://docs.teradata.com/r/Teradata-VantageTM-Advanced-SQL-Engine-Security-Administration/July-2021/Setting-Up-the-Administrative-Infrastructure/Controlling-Access-to-the-Operating-System/Working-with-OS-Level-Security-Options)。

## 連接 [!DNL Teradata Vantage] 帳戶

在平台UI中，選擇 **[!UICONTROL 源]** 從左側導航 [!UICONTROL 源] 工作區。 的 [!UICONTROL 目錄] 螢幕顯示可建立帳戶的各種源。

可以從螢幕左側的目錄中選擇相應的類別。 或者，您可以使用搜索欄找到要使用的特定源。

在 [!UICONTROL 資料庫] 類別，選擇 **[!UICONTROL Teradata]** ，然後選擇 **[!UICONTROL 添加資料]**。

![](../../../../images/tutorials/create/teradata/catalog.png)

的 **[!UICONTROL 連接到TeradataVantage]** 的子菜單。 在此頁上，您可以使用新憑據或現有憑據。

### 現有帳戶

要連接現有帳戶，請選擇 [!DNL Teradata Vantage] 要連接的帳戶，然後選擇 **[!UICONTROL 下一個]** 繼續。

![](../../../../images/tutorials/create/teradata/existing.png)

### 新帳戶

如果使用新憑據，請選擇 **[!UICONTROL 新帳戶]**。 在顯示的輸入表單上，提供名稱、可選說明和 [!DNL Teradata Vantage] 憑據。 完成後，選擇 **[!UICONTROL 連接]** 然後再給新連接建立一段時間。

![](../../../../images/tutorials/create/teradata/new.png)

## 後續步驟

通過學完本教程，您已建立了與TeradataVantage帳戶的連接。 現在，您可以繼續下一個教程， [配置資料流以將資料引入平台](../../dataflow/databases.md)。
