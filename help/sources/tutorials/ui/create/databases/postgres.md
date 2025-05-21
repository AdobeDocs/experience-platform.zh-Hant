---
title: 使用UI連線PostgreSQL至Experience Platform
description: 瞭解如何使用Experience Platform使用者介面中的來源工作區將您的PostgreSQL資料庫連結至Experience Platform。
exl-id: e556d867-a1eb-4900-b8a9-189666a4f3f1
source-git-commit: f4200ca71479126e585ac76dd399af4092fdf683
workflow-type: tm+mt
source-wordcount: '653'
ht-degree: 0%

---

# 使用UI連線[!DNL PostgreSQL]至Experience Platform

閱讀本指南，瞭解如何使用Experience Platform使用者介面中的來源工作區將您的[!DNL PostgreSQL]資料庫連線至Adobe Experience Platform。

## 快速入門

本教學課程需要您實際瞭解下列Adobe Experience Platform元件：

* [[!DNL Experience Data Model (XDM)] 系統](../../../../../xdm/home.md)： Experience Platform用來組織客戶體驗資料的標準化架構。
   * [結構描述組合的基本概念](../../../../../xdm/schema/composition.md)：瞭解XDM結構描述的基本建置區塊，包括結構描述組合中的關鍵原則和最佳實務。
   * [結構描述編輯器教學課程](../../../../../xdm/tutorials/create-schema-ui.md)：瞭解如何使用結構描述編輯器使用者介面建立自訂結構描述。
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md)：根據來自多個來源的彙總資料，提供統一的即時消費者設定檔。

如果您已經有有效的[!DNL PostgreSQL]連線，您可以略過本檔案的其餘部分，並繼續進行有關[設定資料流](../../dataflow/databases.md)的教學課程。

### 收集必要的認證

如需驗證的詳細資訊，請閱讀[[!DNL PostgreSQL] 概觀](../../../../connectors/databases/postgres.md)。

### 為您的連線字串啟用SSL加密

您可以使用下列屬性附加您的連線字串，以啟用[!DNL PostgreSQL]連線字串的SSL加密：

| 屬性 | 說明 | 範例 |
| --- | --- | --- |
| `EncryptionMethod` | 可讓您對[!DNL PostgreSQL]資料啟用SSL加密。 | <uL><li>`EncryptionMethod=0`（已停用）</li><li>`EncryptionMethod=1`（已啟用）</li><li>`EncryptionMethod=6`(RequestSSL)</li></ul> |
| `ValidateServerCertificate` | 套用`EncryptionMethod`時，驗證您的[!DNL PostgreSQL]資料庫傳送的憑證。 | <uL><li>`ValidationServerCertificate=0`（已停用）</li><li>`ValidationServerCertificate=1`（已啟用）</li></ul> |

下列是附加SSL加密的[!DNL PostgreSQL]連線字串範例： `Server={SERVER};Database={DATABASE};Port={PORT};UID={USERNAME};Password={PASSWORD};EncryptionMethod=1;ValidateServerCertificate=1`。

## 瀏覽來源目錄 {#navigate}

在Experience Platform UI中，從左側導覽選取&#x200B;**[!UICONTROL 來源]**&#x200B;以存取&#x200B;*[!UICONTROL 來源]*&#x200B;工作區。 在&#x200B;*[!UICONTROL 類別]*&#x200B;面板中選取適當的類別或者，使用搜尋列導覽至您要使用的特定來源。

若要使用[!DNL PostgreSQL]，請選取&#x200B;*[!UICONTROL 資料庫]*&#x200B;下的&#x200B;**[!UICONTROL PostgreSQL DB]**&#x200B;來源卡，然後選取&#x200B;**[!UICONTROL 設定]**。

>[!TIP]
>
>當指定的來源尚未具有已驗證的帳戶時，來源目錄中的來源會顯示&#x200B;**[!UICONTROL 設定]**&#x200B;選項。 建立已驗證的帳戶後，此選項會變更為&#x200B;**[!UICONTROL 新增資料]**。

![已選取PostgreSQL來源卡的來源目錄。](../../../../images/tutorials/create/postgresql/catalog.png)


## 使用現有帳戶 {#existing}

若要使用現有帳戶，請選取&#x200B;**[!UICONTROL 現有帳戶]**，然後選取您要使用的[!DNL PostgreSQL]帳戶。

![來源工作流程的現有帳戶介面。](../../../../images/tutorials/create/postgresql/existing.png)

## 建立新帳戶 {#create}

如果您沒有現有的帳戶，則必須提供與您來源對應的必要驗證認證，以建立新的帳戶。

若要建立新帳戶，請選取&#x200B;**[!UICONTROL 新帳戶]**，然後提供名稱並選擇性地為您的帳戶新增說明。

![來源工作流程中的新帳戶介面已提供帳戶名稱和選擇性說明。](../../../../images/tutorials/create/postgresql/new.png)

### 在Azure上連線到Experience Platform {#azure}

您可以使用帳戶金鑰或基本驗證，將您的[!DNL PostgreSQL]帳戶連線至Azure上的Experience Platform。

>[!BEGINTABS]

>[!TAB 帳戶金鑰驗證]

若要使用帳戶金鑰驗證，請選取&#x200B;**[!UICONTROL 帳戶金鑰驗證]**，提供您的[連線字串](../../../../connectors/databases/postgres.md#azure)，然後選取&#x200B;**[!UICONTROL 連線至來源]**。

![來源工作流程中的新帳戶介面已選取「帳戶金鑰驗證」。](../../../../images/tutorials/create/postgresql/account-key.png)

>[!TAB 基本驗證]

若要使用基本驗證，請選取&#x200B;**[!UICONTROL 基本驗證]**，提供您的[驗證認證](../../../../connectors/databases/postgres.md#azure)的值，然後選取&#x200B;**[!UICONTROL 連線到來源]**。

![來源工作流程中的新帳戶介面已選取「基本驗證」。](../../../../images/tutorials/create/postgresql/basic-auth.png)

>[!ENDTABS]

### 在Amazon Web Services (AWS)上連線至Experience Platform {#aws}

>[!AVAILABILITY]
>
>本節適用於在Amazon Web Services (AWS)上執行的Experience Platform實作。 目前有限數量的客戶可使用在AWS上執行的Experience Platform 。 若要進一步瞭解支援的Experience Platform基礎結構，請參閱[Experience Platform多雲端總覽](../../../../../landing/multi-cloud.md)。

若要建立新的[!DNL PostgreSQL]帳戶並連線至AWS上的Experience Platform，請確定您位於VA6沙箱，然後提供驗證所需的[認證](../../../../connectors/databases/postgres.md#aws)。

![來源工作流程中的新帳戶介面可連線至AWS。](../../../../images/tutorials/create/postgresql/aws.png)

## 為您的[!DNL PostgreSQL]資料建立資料流

依照本教學課程中的指示，您已建立與[!DNL MariaDB]帳戶的連線。 您現在可以繼續進行下一個教學課程，並[設定資料流以將資料帶入Experience Platform](../../dataflow/databases.md)。
