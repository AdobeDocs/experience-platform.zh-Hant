---
keywords: Experience Platform；首頁；熱門主題；[!DNL PostgreSQL]；[!DNL PostgreSQL]；PostgreSQL
solution: Experience Platform
title: 在使用者介面中建立PostgreSQL Source連線
type: Tutorial
description: 瞭解如何使用Adobe Experience Platform UI建立PostgreSQL來源連線。
exl-id: e556d867-a1eb-4900-b8a9-189666a4f3f1
source-git-commit: ed92bdcd965dc13ab83649aad87eddf53f7afd60
workflow-type: tm+mt
source-wordcount: '496'
ht-degree: 2%

---

# 在使用者介面中建立[!DNL PostgreSQL]來源連線

Adobe Experience Platform中的Source聯結器可讓您依排程擷取外部來源資料。 本教學課程提供使用[!DNL Platform]使用者介面建立[!DNL PostgreSQL]來源聯結器的步驟。

## 快速入門

本教學課程需要您實際瞭解下列Adobe Experience Platform元件：

* [[!DNL Experience Data Model (XDM)] 系統](../../../../../xdm/home.md)： [!DNL Experience Platform]用來組織客戶體驗資料的標準化架構。
   * [結構描述組合的基本概念](../../../../../xdm/schema/composition.md)：瞭解XDM結構描述的基本建置區塊，包括結構描述組合中的關鍵原則和最佳實務。
   * [結構描述編輯器教學課程](../../../../../xdm/tutorials/create-schema-ui.md)：瞭解如何使用結構描述編輯器使用者介面建立自訂結構描述。
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md)：根據來自多個來源的彙總資料，提供統一的即時消費者設定檔。

如果您已經有有效的[!DNL PostgreSQL]連線，您可以略過本檔案的其餘部分，並繼續進行有關[設定資料流](../../dataflow/databases.md)的教學課程。

### 收集必要的認證

若要在[!DNL Platform]上存取您的[!DNL PostgreSQL]帳戶，您必須提供下列值：

| 認證 | 說明 |
| ---------- | ----------- |
| `connectionString` | 與您的[!DNL PostgreSQL]帳戶關聯的連線字串。 [!DNL PostgreSQL]連線字串模式為： `Server={SERVER};Database={DATABASE};Port={PORT};UID={USERNAME};Password={PASSWORD}`。 |

如需開始使用的詳細資訊，請參閱此[[!DNL PostgreSQL] 檔案](https://www.postgresql.org/docs/9.2/app-psql.html)。

#### 為您的連線字串啟用SSL加密

您可以使用下列屬性附加您的連線字串，以啟用[!DNL PostgreSQL]連線字串的SSL加密：

| 屬性 | 說明 | 範例 |
| --- | --- | --- |
| `EncryptionMethod` | 可讓您對[!DNL PostgreSQL]資料啟用SSL加密。 | <uL><li>`EncryptionMethod=0`（已停用）</li><li>`EncryptionMethod=1`（已啟用）</li><li>`EncryptionMethod=6`(RequestSSL)</li></ul> |
| `ValidateServerCertificate` | 套用`EncryptionMethod`時，驗證您的[!DNL PostgreSQL]資料庫傳送的憑證。 | <uL><li>`ValidationServerCertificate=0`（已停用）</li><li>`ValidationServerCertificate=1`（已啟用）</li></ul> |

下列是附加SSL加密的[!DNL PostgreSQL]連線字串範例： `Server={SERVER};Database={DATABASE};Port={PORT};UID={USERNAME};Password={PASSWORD};EncryptionMethod=1;ValidateServerCertificate=1`。

## 連線您的[!DNL PostgreSQL]帳戶

收集必要的認證後，您可以依照下列步驟將[!DNL PostgreSQL]帳戶連結至[!DNL Platform]。

登入[Adobe Experience Platform](https://platform.adobe.com)，然後從左側導覽列中選取&#x200B;**[!UICONTROL 來源]**&#x200B;以存取&#x200B;**[!UICONTROL 來源]**&#x200B;工作區。 **[!UICONTROL 目錄]**&#x200B;畫面會顯示您可以建立帳戶的各種來源。

您可以從熒幕左側的目錄中選取適當的類別。 或者，您可以使用搜尋選項來尋找您要使用的特定來源。

在&#x200B;**[!UICONTROL 資料庫]**&#x200B;類別下，選取&#x200B;**[!UICONTROL PostgreSQL DB]**。 如果這是您第一次使用此聯結器，請選取&#x200B;**[!UICONTROL 設定]**。 否則，請選取&#x200B;**[!UICONTROL 新增資料]**&#x200B;以建立新的[!DNL PostgreSQL]聯結器。

![](../../../../images/tutorials/create/postgresql/catalog.png)

**[!UICONTROL 連線至[!DNL PostgreSQL]]**&#x200B;頁面隨即顯示。 您可以在此頁面使用新的證明資料或現有的證明資料。

### 新帳戶

如果您正在使用新認證，請選取&#x200B;**[!UICONTROL 新帳戶]**。 在出現的輸入表單上，提供名稱、選擇性說明和您的[!DNL PostgreSQL]認證。 完成時，請選取&#x200B;**[!UICONTROL 連線]**，然後等待一段時間以建立新連線。

![](../../../../images/tutorials/create/postgresql/new.png)

### 現有帳戶

若要連線現有帳戶，請選取您要連線的[!DNL PostgreSQL]帳戶，然後選取[下一步]**[!UICONTROL 以繼續。]**

![](../../../../images/tutorials/create/postgresql/existing.png)

## 後續步驟

依照本教學課程中的指示，您已建立與[!DNL PostgreSQL]帳戶的連線。 您現在可以繼續進行下一個教學課程，並[設定資料流以將資料帶入 [!DNL Platform]](../../dataflow/databases.md)。
