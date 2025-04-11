---
title: 使用UI連線MariaDB至Experience Platform
description: 瞭解如何使用Experience Platform使用者介面中的來源工作區，將您的MariaDB帳戶連結至Experience Platform。
exl-id: 259ca112-01f1-414a-bf9f-d94caf4c69df
source-git-commit: 0bf31c76f86b4515688d3aa60deb8744e38b4cd5
workflow-type: tm+mt
source-wordcount: '590'
ht-degree: 0%

---

# 使用UI連線[!DNL MariaDB]至Experience Platform

閱讀本指南，瞭解如何使用Experience Platform使用者介面中的來源工作區將您的[!DNL MariaDB]帳戶連結至Adobe Experience Platform。

## 快速入門

本教學課程需要您實際瞭解下列Experience Platform元件：

* [[!DNL Experience Data Model (XDM)] 系統](../../../../../xdm/home.md)： Experience Platform用來組織客戶體驗資料的標準化架構。
   * [結構描述組合的基本概念](../../../../../xdm/schema/composition.md)：瞭解XDM結構描述的基本建置區塊，包括結構描述組合中的關鍵原則和最佳實務。
   * [結構描述編輯器教學課程](../../../../../xdm/tutorials/create-schema-ui.md)：瞭解如何使用結構描述編輯器使用者介面建立自訂結構描述。
* [即時客戶個人檔案](../../../../../profile/home.md)：根據來自多個來源的彙總資料，提供統一的即時客戶個人檔案。

如果您已有[!DNL MariaDB]連線，可以略過本檔案的其餘部分，並繼續進行有關[設定資料流](../../dataflow/databases.md)的教學課程。

### 收集必要的認證

閱讀[[!DNL MariaDB] 總覽](../../../../connectors/databases/mariadb.md#prerequisites)以取得驗證的相關資訊。

## 瀏覽來源目錄

在Experience Platform UI中，從左側導覽選取&#x200B;**[!UICONTROL 來源]**&#x200B;以存取&#x200B;*[!UICONTROL 來源]*&#x200B;工作區。 在&#x200B;*[!UICONTROL 類別]*&#x200B;面板中選取適當的類別或者，使用搜尋列導覽至您要使用的特定來源。

若要使用[!DNL MariaDB]，請選取&#x200B;*[!UICONTROL 資料庫]*&#x200B;下的&#x200B;**[!UICONTROL MariaDB]**&#x200B;來源卡，然後選取&#x200B;**[!UICONTROL 設定]**。

>[!TIP]
>
>當指定的來源尚未具有已驗證的帳戶時，來源目錄中的來源會顯示&#x200B;**[!UICONTROL 設定]**&#x200B;選項。 建立已驗證的帳戶後，此選項會變更為&#x200B;**[!UICONTROL 新增資料]**。

![已選取MariaDB卡的UI中的來源目錄。](../../../../images/tutorials/create/maria-db/catalog.png)

## 使用現有帳戶 {#existing}

若要使用現有帳戶，請選取&#x200B;**[!UICONTROL 現有帳戶]**，然後選取您要使用的[!DNL MariaDB]帳戶。

![來源工作流程中已選取「現有帳戶」的現有帳戶介面。](../../../../images/tutorials/create/maria-db/existing.png)

## 建立新帳戶 {#create}

如果您沒有現有的帳戶，則必須提供與您來源對應的必要驗證認證，以建立新的帳戶。

若要建立新帳戶，請選取&#x200B;**[!UICONTROL 新帳戶]**，然後提供名稱並選擇性地為您的帳戶新增說明。

![來源工作流程中的新帳戶介面已提供帳戶名稱和選擇性說明。](../../../../images/tutorials/create/maria-db/new.png)

### 在Azure上連線到Experience Platform {#azure}

您可以使用帳戶金鑰或基本驗證，將您的[!DNL MariaDB]帳戶連線至Azure上的Experience Platform。

>[!BEGINTABS]

>[!TAB 帳戶金鑰驗證]

若要使用帳戶金鑰驗證，請選取&#x200B;**[!UICONTROL 帳戶金鑰驗證]**，提供您的[連線字串](../../../../connectors/databases/mariadb.md#azure)，然後選取&#x200B;**[!UICONTROL 連線至來源]**。

![來源工作流程中的新帳戶介面已選取「帳戶金鑰驗證」。](../../../../images/tutorials/create/maria-db/account-key.png)

>[!TAB 基本驗證]

若要使用基本驗證，請選取&#x200B;**[!UICONTROL 基本驗證]**，提供您的[驗證認證](../../../../connectors/databases/mariadb.md#azure)的值，然後選取&#x200B;**[!UICONTROL 連線到來源]**。

![來源工作流程中的新帳戶介面已選取「基本驗證」。](../../../../images/tutorials/create/maria-db/basic-auth.png)

>[!ENDTABS]

### 在Amazon Web Services (AWS)上連線至Experience Platform {#aws}

>[!AVAILABILITY]
>
>本節適用於在Amazon Web Services (AWS)上執行的Experience Platform實作。 目前有限數量的客戶可使用在AWS上執行的Experience Platform 。 若要進一步瞭解支援的Experience Platform基礎結構，請參閱[Experience Platform多雲端總覽](../../../../../landing/multi-cloud.md)。

若要建立新的[!DNL MariaDB]帳戶並連線至AWS上的Experience Platform，請確定您位於VA6沙箱，然後提供驗證所需的[認證](../../../../connectors/databases/mariadb.md#aws)。

![來源工作流程中的新帳戶介面可連線至AWS。](../../../../images/tutorials/create/maria-db/basic-auth.png)

## 後續步驟

依照本教學課程中的指示，您已建立與[!DNL MariaDB]帳戶的連線。 您現在可以繼續進行下一個教學課程，並[設定資料流以將資料帶入Experience Platform](../../dataflow/databases.md)。
