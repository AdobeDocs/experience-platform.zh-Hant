---
keywords: Experience Platform；首頁；熱門主題；TeradataVantage
title: 在UI中建立TeradataVantage來源連線
description: 了解如何使用Adobe Experience Platform UI建立TeradataVantage來源連線。
exl-id: 3fdb09fa-128a-477b-9144-d4ef3ed18ea6
source-git-commit: 322b9aa5b817276eb4b56daf6e410944591c1d51
workflow-type: tm+mt
source-wordcount: '394'
ht-degree: 1%

---

# （測試版）建立 [!DNL Teradata Vantage] UI中的源連接

>[!NOTE]
>
> 此 [!DNL Teradata Vantage] 來源為測試版。 請參閱 [來源概觀](../../../../home.md#terms-and-conditions) 以取得使用測試版標籤來源的詳細資訊。

本教學課程提供建立 [!DNL Teradata Vantage] 來源連接器(使用Adobe Experience Platform使用者介面)。

## 快速入門

本教學課程需要妥善了解Platform的下列元件：

* [來源](../../../../home.md):Experience Platform可讓您從各種來源擷取資料，同時使用Experience Platform服務來建構、加標籤及增強傳入資料。
* [沙箱](../../../../../sandboxes/home.md):Experience Platform提供可將單一Platform執行個體分割成個別虛擬環境的虛擬沙箱，以協助開發及改進數位體驗應用程式。

### 收集所需憑據

若要存取 [!DNL Teradata Vantage] 帳戶，您必須提供下列驗證值：

| 憑據 | 說明 |
| ---------- | ----------- |
| 連線字串 | 連線字串是字串，提供資料來源的相關資訊以及您如何連線至它。 的連接字串模式 [!DNL Teradata Vantage] is `DBCName={SERVER};Uid={USERNAME};Pwd={PASSWORD}`. |

如需快速入門的詳細資訊，請參閱 [[!DNL Teradata Vantage] 檔案](https://docs.teradata.com/r/Teradata-VantageTM-Advanced-SQL-Engine-Security-Administration/July-2021/Setting-Up-the-Administrative-Infrastructure/Controlling-Access-to-the-Operating-System/Working-with-OS-Level-Security-Options).

## 連接您的 [!DNL Teradata Vantage] 帳戶

在平台UI中，選取 **[!UICONTROL 來源]** 從左側導覽器存取 [!UICONTROL 來源] 工作區。 此 [!UICONTROL 目錄] 畫面會顯示您可以用來建立帳戶的各種來源。

您可以從畫面左側的目錄中選取適當的類別。 或者，您也可以使用搜尋列找到您要使用的特定來源。

在 [!UICONTROL 資料庫] 類別，選擇 **[!UICONTROL Teradata]** 然後選取 **[!UICONTROL 新增資料]**.

![](../../../../images/tutorials/create/teradata/catalog.png)

此 **[!UICONTROL 連接到VantageTeradata]** 頁。 在此頁面上，您可以使用新憑證或現有憑證。

### 現有帳戶

若要連線現有帳戶，請選取 [!DNL Teradata Vantage] 要連接的帳戶，然後選擇 **[!UICONTROL 下一個]** 繼續。

![](../../../../images/tutorials/create/teradata/existing.png)

### 新帳戶

如果使用新憑據，請選擇 **[!UICONTROL 新帳戶]**. 在顯示的輸入表單中，提供名稱、選用說明和您的 [!DNL Teradata Vantage] 憑證。 完成後，請選取 **[!UICONTROL Connect]** 然後讓新連接建立一段時間。

![](../../../../images/tutorials/create/teradata/new.png)

## 後續步驟

依照本教學課程，您已建立與您的TeradataVantage帳戶的連線。 您現在可以繼續下一個教學課程，以及 [配置資料流以將資料導入Platform](../../dataflow/databases.md).
