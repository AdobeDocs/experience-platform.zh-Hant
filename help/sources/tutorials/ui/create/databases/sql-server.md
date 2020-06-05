---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 在UI中建立Microsoft SQL Server源連接器
topic: overview
translation-type: tm+mt
source-git-commit: 75ba0bce7ce070af851bbf7e220dbf08febc4c20
workflow-type: tm+mt
source-wordcount: '511'
ht-degree: 0%

---


# 在UI中建立Microsoft SQL Server源連接器

> [!NOTE]
> Microsoft SQL Server連接器正在測試中。 功能和檔案可能會有所變更。

Adobe Experience Platform中的來源連接器可讓您依計畫吸收外部來源的資料。 本教程提供了使用平台用戶介面建立Microsoft SQL Server（以下稱為「SQL Server」）源連接器的步驟。

## 快速入門

本教學課程需要對Adobe Experience Platform的下列元件有正確的認識：

* [體驗資料模型(XDM)系統](../../../../../xdm/home.md): Experience Platform組織客戶體驗資料的標準化架構。
   * [架構構成基礎](../../../../../xdm/schema/composition.md): 瞭解XDM架構的基本建置區塊，包括架構組合的主要原則和最佳實務。
   * [架構編輯器教程](../../../../../xdm/tutorials/create-schema-ui.md): 瞭解如何使用架構編輯器UI建立自訂架構。
* [即時客戶個人檔案](../../../../../profile/home.md): 根據來自多個來源的匯整資料，提供統一、即時的消費者個人檔案。

如果您已經有SQL Server基本連接，則可以跳過本文檔的其餘部分，並繼續有關配置資料 [流的教程](../../dataflow/databases.md)。

### 收集必要的認證

要連接到平台上的SQL Server，必須提供以下連接屬性：

| 憑證 | 說明 |
| ---------- | ----------- |
| `connectionString` | 與SQL Server帳戶關聯的連接字串。 SQL Server連接字串模式為： `Data Source={SERVER_NAME}\\<{INSTANCE_NAME} if using named instance>;Initial Catalog={DATABASE};Integrated Security=False;User ID={USERNAME};Password={PASSWORD};`. |

有關開始使 [用SQL Server的詳細資訊](https://docs.microsoft.com/en-us/dotnet/framework/data/adonet/sql/authentication-in-sql-server) ，請參閱本文檔。

## 連接SQL Server帳戶

收集到所需憑據後，可以按照以下步驟建立新的入站基本連接，以將SQL Server帳戶連結到平台。

登入 <a href="https://platform.adobe.com" target="_blank">Adobe Experience Platform</a> ，然後從左側導覽列選取 **Sources** ，以存取 ** Sources工作區。 「目 *錄* 」螢幕顯示各種源，您可以為其建立入站基本連接，而每個源顯示與其關聯的現有基本連接數。

在「數 *據庫* 」類別下，選擇 **Microsoft SQL Server** ，以在螢幕右側顯示資訊欄。 資訊列提供所選來源的簡短說明，以及與來源連線或檢視其檔案的選項。 要建立新的入站基本連接，請選擇「 **連接源」**。

![](../../../../images/tutorials/create/microsoft-sql-server/catalog.png)

此時 *將顯示「連接到Microsoft SQL Server* 」頁。 在此頁上，您可以使用新認證或現有認證。

### 新帳戶

如果您使用新認證，請選擇「新 **帳戶」**。 在顯示的輸入表單上，為基本連接提供名稱、可選說明和SQL Server憑據。 完成後，選擇 **Connect** ，然後為建立新的基本連接留出一些時間。

![](../../../../images/tutorials/create/microsoft-sql-server/new.png)

### 現有帳戶

要連接現有帳戶，請選擇要連接的SQL Server帳戶，然後選擇「下 **一步** 」繼續。

![](../../../../images/tutorials/create/microsoft-sql-server/existing.png)

## 後續步驟

通過本教程，您已建立了與SQL Server帳戶的基本連接。 您現在可以繼續下一個教程，並 [配置資料流以將資料導入平台](../../dataflow/databases.md)。