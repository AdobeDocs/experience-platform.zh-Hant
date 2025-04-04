---
keywords: Experience Platform；首頁；熱門主題；mysql；MySQL
solution: Experience Platform
title: 在使用者介面中建立MySQL Source連線
type: Tutorial
description: 瞭解如何使用Adobe Experience Platform UI建立MySQL來源連線。
exl-id: 75e74bde-6199-4970-93d2-f95ec3a59aa5
source-git-commit: b48c24ac032cbf785a26a86b50a669d7fcae5d97
workflow-type: tm+mt
source-wordcount: '411'
ht-degree: 2%

---

# 在使用者介面中建立[!DNL MySQL]來源連線

Adobe Experience Platform中的Source聯結器可讓您依排程擷取外部來源資料。 本教學課程提供使用Adobe Experience Platform UI建立[!DNL MySQL]來源連線的步驟。

## 快速入門

本教學課程需要您實際瞭解下列Adobe Experience Platform元件：

* [[!DNL Experience Data Model (XDM)] 系統](../../../../../xdm/home.md)： Experience Platform用來組織客戶體驗資料的標準化架構。
   * [結構描述組合的基本概念](../../../../../xdm/schema/composition.md)：瞭解XDM結構描述的基本建置區塊，包括結構描述組合中的關鍵原則和最佳實務。
   * [結構描述編輯器教學課程](../../../../../xdm/tutorials/create-schema-ui.md)：瞭解如何使用結構描述編輯器使用者介面建立自訂結構描述。
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md)：根據來自多個來源的彙總資料，提供統一的即時消費者設定檔。

如果您已有[!DNL MySQL]連線，可以略過本檔案的其餘部分，並繼續進行有關[設定資料流](../../dataflow/databases.md)的教學課程。

### 收集必要的認證

若要在[!DNL Experience Platform]上存取您的[!DNL MySQL]帳戶，您必須提供下列值：

| 認證 | 說明 |
| ---------- | ----------- |
| `connectionString` | 與您的帳戶相關聯的[!DNL MySQL]連線字串。 [!DNL MySQL]連線字串模式為： `Server={SERVER};Port={PORT};Database={DATABASE};UID={USERNAME};PWD={PASSWORD}`。 您可以閱讀[[!DNL MySQL] 檔案](https://dev.mysql.com/doc/connector-net/en/connector-net-connections-string.html)，深入瞭解連線字串以及如何取得連線字串。 |

## 連線您的[!DNL MySQL]帳戶

收集必要的認證後，您可以依照下列步驟將[!DNL MySQL]帳戶連結至[!DNL Experience Platform]。

登入[Adobe Experience Platform](https://platform.adobe.com)，然後從左側導覽列中選取&#x200B;**[!UICONTROL 來源]**&#x200B;以存取&#x200B;**[!UICONTROL 來源]**&#x200B;工作區。 **[!UICONTROL 目錄]**&#x200B;畫面會顯示您可以建立帳戶的各種來源。

在&#x200B;**[!UICONTROL 資料庫]**&#x200B;類別下，選取&#x200B;**[!UICONTROL MySQL]**。 如果這是您第一次使用此聯結器，請選取&#x200B;**[!UICONTROL 設定]**。 否則，請選取&#x200B;**[!UICONTROL 新增資料]**&#x200B;以建立新的[!DNL MySQL]聯結器。

![](../../../../images/tutorials/create/my-sql/catalog.png)

會顯示&#x200B;**[!UICONTROL 連線至MySQL]**&#x200B;頁面。 您可以在此頁面使用新的證明資料或現有的證明資料。

### 新帳戶

如果您正在使用新認證，請選取&#x200B;**[!UICONTROL 新帳戶]**。 在出現的輸入表單上，提供名稱、選擇性說明和您的[!DNL MySQL]認證。 完成時，請選取&#x200B;**[!UICONTROL 連線]**，然後等待一段時間以建立新連線。

![](../../../../images/tutorials/create/my-sql/new.png)

### 現有帳戶

若要連線現有帳戶，請選取您要連線的[!DNL MySQL]帳戶，然後選取[下一步]**[!UICONTROL 以繼續。]**

![](../../../../images/tutorials/create/my-sql/existing.png)

## 後續步驟

依照本教學課程中的指示，您已建立與MySQL帳戶的連線。 您現在可以繼續進行下一個教學課程，並[設定資料流以將資料帶入 [!DNL Experience Platform]](../../dataflow/databases.md)。
