---
keywords: Experience Platform;home；常用主題；Microsoft SQL Server;SQL Server;sql Server
solution: Experience Platform
title: 在UI中建立Microsoft SQL Server源連接
topic-legacy: overview
type: Tutorial
description: 瞭解如何使用Adobe Experience PlatformUI建立Microsoft SQL Server源連接。
exl-id: aba4e317-1c59-4999-a525-dba15f8d4df9
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '458'
ht-degree: 1%

---

# 在UI中建立[!DNL Microsoft SQL Server]源連接

>[!NOTE]
>
> [!DNL Microsoft SQL Server]介面處於測試狀態。 有關使用beta標籤連接器的詳細資訊，請參閱[ Sources綜覽](../../../../home.md#terms-and-conditions)。

Adobe Experience Platform的來源連接器提供按計畫接收外部來源資料的能力。 本教學課程提供使用[!DNL Platform]使用者介面建立[!DNL Microsoft SQL Server]（以下稱為&quot;[!DNL SQL Server]&quot;）來源連接器的步驟。

## 快速入門

本教學課程需要對Adobe Experience Platform的下列部分有正確的理解：

* [[!DNL Experience Data Model (XDM)] 系統](../../../../../xdm/home.md):Experience Platform組織客戶體驗資料的標準化架構。
   * [架構構成基礎](../../../../../xdm/schema/composition.md):瞭解XDM架構的基本建置區塊，包括架構組合的主要原則和最佳實務。
   * [架構編輯器教程](../../../../../xdm/tutorials/create-schema-ui.md):瞭解如何使用架構編輯器UI建立自訂架構。
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md):根據來自多個來源的匯整資料，提供統一、即時的消費者個人檔案。

如果您已經有有效的[!DNL SQL Server]連接，則可跳過本文檔的其餘部分，繼續[配置資料流](../../dataflow/databases.md)的教程。

### 收集必要的認證

要連接到[!DNL Platform]上的[!DNL SQL Server]，必須提供以下連接屬性：

| 憑證 | 說明 |
| ---------- | ----------- |
| `connectionString` | 與[!DNL SQL Server]帳戶關聯的連接字串。 [!DNL SQL Server]連接字串模式是：`Data Source={SERVER_NAME}\\<{INSTANCE_NAME} if using named instance>;Initial Catalog={DATABASE};Integrated Security=False;User ID={USERNAME};Password={PASSWORD};`。 |

有關入門的詳細資訊，請參閱[this [!DNL SQL Server] document](https://docs.microsoft.com/en-us/dotnet/framework/data/adonet/sql/authentication-in-sql-server)。

## 連接您的[!DNL SQL Server]帳戶

收集完所需憑證後，您可以按照以下步驟將[!DNL SQL Server]帳戶連結至[!DNL Platform]。

登入[Adobe Experience Platform](https://platform.adobe.com)，然後從左側導覽列選擇&#x200B;**[!UICONTROL Sources]**&#x200B;以存取&#x200B;**[!UICONTROL Sources]**&#x200B;工作區。 **[!UICONTROL Catalog]**&#x200B;畫面會顯示各種來源，您可以用來建立帳戶。

您可以從畫面左側的目錄中選取適當的類別。 或者，您也可以使用搜尋選項找到您要使用的特定來源。

在&#x200B;**[!UICONTROL Databases]**&#x200B;類別下，選擇&#x200B;**[!UICONTROL Microsoft SQL Server]**。 如果這是您第一次使用此連接器，請選擇&#x200B;**[!UICONTROL Configure]**。 否則，請選擇&#x200B;**[!UICONTROL Add data]**&#x200B;以建立新的[!DNL SQL Server]連接器。

![](../../../../images/tutorials/create/microsoft-sql-server/catalog.png)

此時將顯示&#x200B;**[!UICONTROL Connect to Microsoft SQL Server]**&#x200B;頁。 在此頁上，您可以使用新認證或現有認證。

### 新帳戶

如果使用新憑據，請選擇&#x200B;**[!UICONTROL New account]**。 在顯示的輸入表單上，提供名稱、可選說明和您的[!DNL SQL Server]憑證。 完成後，選擇&#x200B;**[!UICONTROL Connect]** ，然後允許一些時間建立新連接。

![](../../../../images/tutorials/create/microsoft-sql-server/new.png)

### 現有帳戶

要連接現有帳戶，請選擇要連接的[!DNL SQL Server]帳戶，然後選擇&#x200B;**[!UICONTROL Next]**&#x200B;繼續。

![](../../../../images/tutorials/create/microsoft-sql-server/existing.png)

## 後續步驟

在本教學課程之後，您已建立與[!DNL SQL Server]帳戶的連線。 現在，您可以繼續下一個教程，並[配置資料流以將資料導入 [!DNL Platform]](../../dataflow/databases.md)。
