---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 在UI中建立Microsoft SQL Server源連接器
topic: overview
translation-type: tm+mt
source-git-commit: 598b29f681ac930a4e1781f7f298608c8344d807
workflow-type: tm+mt
source-wordcount: '508'
ht-degree: 0%

---


# 在UI中 [!DNL Microsoft] 建立SQL Server源連接器

>[!NOTE]
> SQL [!DNL Microsoft] Server連接器正在測試中。 如需使用 [測試版標籤連接器的詳細資訊](../../../../home.md#terms-and-conditions) ，請參閱來源概觀。

Adobe Experience Platform中的來源連接器可讓您依計畫吸收外部來源的資料。 本教程提供了使用用戶介面創 [!DNL Microsoft] 建SQL Server（以下稱為「SQL Server」）源連接器的 [!DNL Platform] 步驟。

## 快速入門

本教學課程需要對Adobe Experience Platform的下列元件有正確的認識：

* [體驗資料模型(XDM)系統](../../../../../xdm/home.md):Experience Platform組織客戶體驗資料的標準化架構。
   * [架構構成基礎](../../../../../xdm/schema/composition.md):瞭解XDM架構的基本建置區塊，包括架構組合的主要原則和最佳實務。
   * [架構編輯器教程](../../../../../xdm/tutorials/create-schema-ui.md):瞭解如何使用架構編輯器UI建立自訂架構。
* [即時客戶個人檔案](../../../../../profile/home.md):根據來自多個來源的匯整資料，提供統一、即時的消費者個人檔案。

如果您已經有SQL Server基本連接，則可以跳過本文檔的其餘部分，並繼續有關配置資料 [流的教程](../../dataflow/databases.md)。

### 收集必要的認證

要在上連接到SQL Server [!DNL Platform]，必須提供以下連接屬性：

| 憑證 | 說明 |
| ---------- | ----------- |
| `connectionString` | 與SQL Server帳戶關聯的連接字串。 SQL Server連接字串模式為： `Data Source={SERVER_NAME}\\<{INSTANCE_NAME} if using named instance>;Initial Catalog={DATABASE};Integrated Security=False;User ID={USERNAME};Password={PASSWORD};`. |

有關開始使 [用SQL Server的詳細資訊](https://docs.microsoft.com/en-us/dotnet/framework/data/adonet/sql/authentication-in-sql-server) ，請參閱本文檔。

## 連接SQL Server帳戶

收集到所需憑據後，可以按照以下步驟建立新的入站基本連接，以將SQL Server帳戶連結到 [!DNL Platform]。

登入 [Adobe Experience Platform](https://platform.adobe.com) ，然後從左側導覽列選取 **[!UICONTROL Sources]** ，以存取 ** Sources工作區。 「目 *[!UICONTROL 錄]* 」螢幕顯示各種源，您可以為其建立入站基本連接，而每個源顯示與其關聯的現有基本連接數。

在「數 *[!UICONTROL 據庫]* 」類別下，選擇 **[!UICONTROL Microsoft SQL Server]** ，以在螢幕右側顯示資訊欄。 資訊列提供所選來源的簡短說明，以及與來源連線或檢視其檔案的選項。 要建立新的入站基本連接，請選擇「添 **[!UICONTROL 加資料」]**。

![](../../../../images/tutorials/create/microsoft-sql-server/catalog.png)

此時 *[!UICONTROL 將顯示「連接到Microsoft SQL Server]* 」頁。 在此頁上，您可以使用新認證或現有認證。

### 新帳戶

如果您使用新認證，請選擇「新 **[!UICONTROL 帳戶」]**。 在顯示的輸入表單上，為基本連接提供名稱、可選說明和SQL Server憑據。 完成後，選擇 **[!UICONTROL Connect]** ，然後為建立新的基本連接留出一些時間。

![](../../../../images/tutorials/create/microsoft-sql-server/new.png)

### 現有帳戶

要連接現有帳戶，請選擇要連接的SQL Server帳戶，然後選擇「下 **[!UICONTROL 一步]** 」繼續。

![](../../../../images/tutorials/create/microsoft-sql-server/existing.png)

## 後續步驟

通過本教程，您已建立了與SQL Server帳戶的基本連接。 您現在可以繼續下一個教程，並 [配置資料流以將資料導入平台](../../dataflow/databases.md)。