---
title: 在使用者介面中建立Microsoft SQL Server來源連線
description: 瞭解如何使用Adobe Experience Platform UI建立Microsoft SQL Server來源連線。
exl-id: aba4e317-1c59-4999-a525-dba15f8d4df9
source-git-commit: 1828dd76e9ff317f97e9651331df3e49e44efff5
workflow-type: tm+mt
source-wordcount: '465'
ht-degree: 1%

---

# 建立 [!DNL Microsoft SQL Server] ui中的來源連線

閱讀本教學課程以瞭解如何連結 [!DNL Microsoft SQL Server] 使用使用者介面登入Adobe Experience Platform帳戶。

## 快速入門

本教學課程需要您實際瞭解下列Adobe Experience Platform元件：

* [[!DNL Experience Data Model (XDM)] 系統](../../../../../xdm/home.md)：Experience Platform組織客戶體驗資料的標準化架構。
   * [結構描述組合基本概念](../../../../../xdm/schema/composition.md)：瞭解XDM結構描述的基本建置區塊，包括結構描述組合中的關鍵原則和最佳實務。
   * [結構描述編輯器教學課程](../../../../../xdm/tutorials/create-schema-ui.md)：瞭解如何使用結構編輯器UI建立自訂結構描述。
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md)：根據來自多個來源的彙總資料，提供統一的即時消費者個人檔案。

如果您已有有效的 [!DNL SQL Server] 連線時，您可以略過本檔案的其餘部分，並繼續進行上的教學課程 [設定資料流](../../dataflow/databases.md).

### 收集必要的認證

為了連線到 [!DNL SQL Server] 於 [!DNL Platform]，您必須提供下列連線屬性：

| 認證 | 說明 |
| ---------- | ----------- |
| 連線字串 | 與您的關聯的連線字串 [!DNL Microsoft SQL Server] 帳戶。 您的連線字串模式取決於您是使用伺服器名稱或執行個體名稱作為資料來源：<ul><li>使用伺服器名稱的連線字串： `Data Source={SERVER_NAME};Initial Catalog={DATABASE};Integrated Security=False;User ID={USER_ID};Password={PASSWORD};`</li><li>使用執行個體名稱的連線字串：`Data Source={INSTANCE_NAME};Initial Catalog={DATABASE};Integrated Security=False;User ID={USER_ID};Password={PASSWORD};` | `Data Source=mssqlserver.database.windows.net;Initial Catalog=mssqlserver_e2e_db;Integrated Security=False;User ID=mssqluser;Password=mssqlpassword` |

如需開始使用的詳細資訊，請參閱 [此 [!DNL SQL Server] 檔案](https://docs.microsoft.com/en-us/dotnet/framework/data/adonet/sql/authentication-in-sql-server).

## 連線您的 [!DNL SQL Server] 帳戶

在Platform UI中選取 **[!UICONTROL 來源]** 從左側導覽存取 [!UICONTROL 來源] 工作區。 您可以從熒幕左側的目錄中選取適當的類別。 或者，您可以使用搜尋選項來尋找您要使用的特定來源。

在 *資料庫* 類別，選取 **[!DNL Microsoft SQL Server]**，然後選取 **[!UICONTROL 設定]**.

>[!TIP]
>
>來源目錄中的來源會顯示 **[!UICONTROL 設定]** 選項，當指定的來源尚未擁有已驗證的帳戶時。 一旦驗證帳戶存在，此選項就會變更為 **[!UICONTROL 新增資料]**.

![已選取Microsoft SQL Server來源的來源目錄。](../../../../images/tutorials/create/microsoft-sql-server/catalog.png)

此 **[!UICONTROL 連線至Microsoft SQL Server]** 頁面便會顯示。 您可以在此頁面使用新的證明資料或現有的證明資料。

>[!BEGINTABS]

>[!TAB 建立新帳戶]

若要建立新帳戶，請選取 **[!UICONTROL 新帳戶]** 並提供名稱、選擇性說明和您的認證。

完成後，選取 **[!UICONTROL 連線到來源]** 然後等待一段時間以建立新連線。

![已輸入並反白來源連線詳細資料的新帳戶介面。](../../../../images/tutorials/create/microsoft-sql-server/new.png)

>[!TAB 使用現有帳戶]

若要使用現有帳戶，請選取 **[!UICONTROL 現有帳戶]** 然後從現有帳戶目錄中選取您要使用的帳戶。

選取 **[!UICONTROL 下一個]** 以繼續進行。

![顯示現有帳戶清單的現有帳戶介面。](../../../../images/tutorials/create/microsoft-sql-server/existing.png)

>[!ENDTABS]

## 後續步驟

依照本教學課程中的指示，您已建立與的連線， [!DNL SQL Server] 帳戶。 您現在可以繼續進行下一個教學課程及 [設定資料流以將資料帶入 [!DNL Platform]](../../dataflow/databases.md).
