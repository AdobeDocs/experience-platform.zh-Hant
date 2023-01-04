---
keywords: Experience Platform；首頁；熱門主題；Maria DB;Maria db
solution: Experience Platform
title: 在UI中建立MariaDB源連接
topic-legacy: overview
type: Tutorial
description: 了解如何使用Adobe Experience Platform UI建立Maria DB源連接。
exl-id: 259ca112-01f1-414a-bf9f-d94caf4c69df
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '416'
ht-degree: 1%

---

# 建立 [!DNL MariaDB] UI中的源連接

Adobe Experience Platform中的來源連接器可讓您依排程內嵌外部來源資料。 本教學課程提供使用 [!DNL Platform] 使用者介面。

## 快速入門

本教學課程需要妥善了解下列Adobe Experience Platform元件：

* [[!DNL Experience Data Model (XDM)] 系統](../../../../../xdm/home.md):標準化框架 [!DNL Experience Platform] 組織客戶體驗資料。
   * [結構構成基本概念](../../../../../xdm/schema/composition.md):了解XDM結構描述的基本建置組塊，包括結構描述的主要原則和最佳實務。
   * [結構編輯器教學課程](../../../../../xdm/tutorials/create-schema-ui.md):了解如何使用結構編輯器UI建立自訂結構。
* [即時客戶個人檔案](../../../../../profile/home.md):根據來自多個來源的匯總資料，提供統一的即時消費者設定檔。

如果您已有 [!DNL MariaDB] 連線，您可以略過本檔案的其餘部分，並繼續進行有關 [配置資料流](../../dataflow/databases.md).

### 收集所需憑據

若要存取 [!DNL MariaDB] 帳戶 [!DNL Platform]，您必須提供下列值：

| 憑據 | 說明 |
| ---------- | ----------- |
| `connectionString` | 與您的MariaDB身份驗證相關聯的連接字串。 此 [!DNL MariaDB] 連線字串模式為： `Server={HOST};Port={PORT};Database={DATABASE};UID={USERNAME};PWD={PASSWORD}`. |

如需快速入門的詳細資訊，請參閱 [[!DNL MariaDB] 檔案](https://mariadb.com/kb/en/about-mariadb-connector-odbc/).

## 連接您的 [!DNL Maria DB] 帳戶

收集完所需憑證後，您可以依照下列步驟連結您的 [!DNL Maria DB] 帳戶 [!DNL Platform].

登入 [Adobe Experience Platform](https://platform.adobe.com) 然後選取 **[!UICONTROL 來源]** 從左側導覽列存取 **[!UICONTROL 來源]** 工作區。 此 **[!UICONTROL 目錄]** 畫面會顯示您可以為其建立帳戶的各種來源。

在 **[!UICONTROL 資料庫]** 類別，選擇 **[!UICONTROL 瑪麗亞DB]**. 如果這是您第一次使用此連接器，請選取 **[!UICONTROL 設定]**. 否則，請選取 **[!UICONTROL 新增資料]** 建立新 [!DNL Maria DB] 連接器。

![](../../../../images/tutorials/create/maria-db/catalog.png)

此 **[!UICONTROL 連接到Maria DB]** 頁。 在此頁面上，您可以使用新憑證或現有憑證。

### 新帳戶

如果使用新憑據，請選擇 **[!UICONTROL 新帳戶]**. 在顯示的輸入表單中，提供名稱、選用說明和您的 [!DNL MariaDB] 憑證。 完成後，請選取 **[!UICONTROL Connect]** 然後讓新連接建立一段時間。

![](../../../../images/tutorials/create/maria-db/new.png)

### 現有帳戶

若要連線現有帳戶，請選取 [!DNL MariaDB] 要連接的帳戶，然後選擇 **[!UICONTROL 下一個]** 繼續。

![](../../../../images/tutorials/create/maria-db/existing.png)

## 後續步驟

依照本教學課程，您已建立與 [!DNL MariaDB] 帳戶。 您現在可以繼續下一個教學課程，以及 [配置資料流以將資料帶入 [!DNL Platform]](../../dataflow/databases.md).
