---
title: 使用UI連線MySQL至Experience Platform
description: 瞭解如何使用UI將MySQL資料庫連結至Experience Platform。
exl-id: 75e74bde-6199-4970-93d2-f95ec3a59aa5
source-git-commit: 659af23c6d05f184b745e13ab8545941f3892e7e
workflow-type: tm+mt
source-wordcount: '540'
ht-degree: 0%

---

# 在使用者介面中建立[!DNL MySQL]來源連線

閱讀本指南，瞭解如何使用Experience Platform使用者介面中的來源工作區將您的[!DNL MySQL]資料庫連線至Adobe Experience Platform。

## 快速入門

本教學課程需要您實際瞭解下列Adobe Experience Platform元件：

* [[!DNL Experience Data Model (XDM)] 系統](../../../../../xdm/home.md)： Experience Platform用來組織客戶體驗資料的標準化架構。
   * [結構描述組合的基本概念](../../../../../xdm/schema/composition.md)：瞭解XDM結構描述的基本建置區塊，包括結構描述組合中的關鍵原則和最佳實務。
   * [結構描述編輯器教學課程](../../../../../xdm/tutorials/create-schema-ui.md)：瞭解如何使用結構描述編輯器使用者介面建立自訂結構描述。
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md)：根據來自多個來源的彙總資料，提供統一的即時消費者設定檔。

如果您已有[!DNL MySQL]連線，可以略過本檔案的其餘部分，並繼續進行有關[設定資料流](../../dataflow/databases.md)的教學課程。

### 收集必要的認證

閱讀[[!DNL MySQL] 總覽](../../../../connectors/databases/mysql.md#prerequisites)以取得驗證的相關資訊。

## 瀏覽來源目錄

在Experience Platform UI中，從左側導覽選取&#x200B;**[!UICONTROL 來源]**&#x200B;以存取&#x200B;*[!UICONTROL 來源]*&#x200B;工作區。 選擇類別或使用搜尋列來尋找您的來源。

若要連線到[!DNL MySQL]，請移至&#x200B;*[!UICONTROL 資料庫]*&#x200B;類別，選取&#x200B;**[!UICONTROL MySQL]**&#x200B;來源卡，然後選取&#x200B;**[!UICONTROL 設定]**。

>[!TIP]
>
>當指定的來源尚未具有已驗證的帳戶時，來源目錄中的來源會顯示&#x200B;**[!UICONTROL 設定]**&#x200B;選項。 建立已驗證的帳戶後，此選項會變更為&#x200B;**[!UICONTROL 新增資料]**。

![已選取MySQL來源卡的來源目錄。](../../../../images/tutorials/create/my-sql/catalog.png)

## 使用現有帳戶 {#existing}

若要使用現有帳戶，請選取&#x200B;**[!UICONTROL 現有帳戶]**，然後選取您要使用的[!DNL MySQL]帳戶。

![來源工作流程中已選取「現有帳戶」的現有帳戶介面。](../../../../images/tutorials/create/my-sql/existing.png)

## 建立新帳戶 {#new}

若要建立新帳戶，請選取&#x200B;**[!UICONTROL 新帳戶]**，然後提供名稱並選擇性地為您的帳戶新增說明。

![來源工作流程中的新帳戶介面已提供帳戶名稱和選擇性說明。](../../../../images/tutorials/create/my-sql/new.png)

### 在Azure上連線到Experience Platform {#azure}

您可以使用帳戶金鑰或基本驗證，將您的[!DNL MySQL]資料庫連線至Azure上的Experience Platform。

>[!BEGINTABS]

>[!TAB 帳戶金鑰驗證]

若要使用帳戶金鑰驗證，請選取&#x200B;**[!UICONTROL 帳戶金鑰驗證]**，提供您的[連線字串](../../../../connectors/databases/mysql.md#azure)，然後選取&#x200B;**[!UICONTROL 連線至來源]**。

![來源工作流程中的新帳戶介面已選取「帳戶金鑰驗證」。](../../../../images/tutorials/create/my-sql/account-key.png)

>[!TAB 基本驗證]

若要使用基本驗證，請選取&#x200B;**[!UICONTROL 基本驗證]**，提供您的[驗證認證](../../../../connectors/databases/mysql.md#azure)的值，然後選取&#x200B;**[!UICONTROL 連線到來源]**。

![來源工作流程中的新帳戶介面已選取「基本驗證」。](../../../../images/tutorials/create/my-sql/basic-auth.png)

>[!ENDTABS]

### 在Amazon Web Services (AWS)上連線至Experience Platform {#aws}

>[!AVAILABILITY]
>
>本節適用於在Amazon Web Services (AWS)上執行的Experience Platform實作。 目前有限數量的客戶可使用在AWS上執行的Experience Platform 。 若要進一步瞭解支援的Experience Platform基礎結構，請參閱[Experience Platform多雲端總覽](../../../../../landing/multi-cloud.md)。

若要建立新的[!DNL MySQL]帳戶並連線至AWS上的Experience Platform，請確定您位於VA6沙箱，然後提供驗證所需的[認證](../../../../connectors/databases/mysql.md#aws)。

![來源工作流程中的新帳戶介面可連線至AWS。](../../../../images/tutorials/create/my-sql/aws.png)

## 建立[!DNL MySQL]資料的資料流

現在您已經成功連線[!DNL MySQL]資料庫，您現在可以[建立資料流，並將資料庫中的資料擷取到Experience Platform](../../dataflow/databases.md)。
