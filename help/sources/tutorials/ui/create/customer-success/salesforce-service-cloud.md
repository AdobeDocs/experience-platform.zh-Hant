---
title: 使用Salesforce使用者介面連線您的Experience Platform服務雲端帳戶
description: 瞭解如何使用使用者介面連線您的Salesforce Service Cloud帳戶，並將您的客戶成功資料匯入Experience Platform。
exl-id: 38480a29-7852-46c6-bcea-5dc6bffdbd15
source-git-commit: b9a9b00114b3c1159a14b7e39484d250fa7563ba
workflow-type: tm+mt
source-wordcount: '423'
ht-degree: 2%

---

# 使用使用者介面將您的[!DNL Salesforce Service Cloud]帳戶連線至Experience Platform

請依照此逐步指南，順暢地連線您的[!DNL Salesforce Service Cloud]帳戶，並將您的客戶成功資料匯入Adobe Experience Platform。

## 快速入門

本教學課程需要您實際瞭解下列Experience Platform元件：

* [[!DNL Experience Data Model (XDM)] 系統](../../../../../xdm/home.md)： Experience Platform用來組織客戶體驗資料的標準化架構。
   * [結構描述組合的基本概念](../../../../../xdm/schema/composition.md)：瞭解XDM結構描述的基本建置區塊，包括結構描述組合中的關鍵原則和最佳實務。
   * [結構描述編輯器教學課程](../../../../../xdm/tutorials/create-schema-ui.md)：瞭解如何使用結構描述編輯器使用者介面建立自訂結構描述。
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md)：根據來自多個來源的彙總資料，提供統一的即時消費者設定檔。

如果您已有有效的[!DNL Salesforce Service Cloud]連線，可以略過本檔案的其餘部分，並繼續進行教學課程： [設定資料流以取得客戶成功](../../dataflow/customer-success.md)

### 收集必要的認證

閱讀[驗證指南](../../../../connectors/customer-success/salesforce-service-cloud.md#credentials)，以取得擷取認證的詳細資訊。

## 連線您的[!DNL Salesforce Service Cloud]帳戶

在Experience Platform UI中，從左側導覽選取「**[!UICONTROL Sources]**」以存取[!UICONTROL Sources]工作區。 您可以從熒幕左側的目錄中選取適當的類別。 或者，您可以使用搜尋選項來尋找您要使用的特定來源。

在&#x200B;*[!UICONTROL Customer success]*&#x200B;類別下選取&#x200B;**[!DNL Salesforce Service Cloud]**，然後選取&#x200B;**[!UICONTROL Add data]**。

>[!TIP]
>
>當指定的來源尚未具有已驗證的帳戶時，來源目錄中的來源會顯示&#x200B;**[!UICONTROL Set up]**&#x200B;選項。 一旦驗證帳戶存在，此選項就會變更為&#x200B;**[!UICONTROL Add data]**。

![已選取Experience Platform Service Cloud來源卡的Salesforce UI上的來源目錄。](../../../../images/tutorials/create/salesforce-service-cloud/catalog.png)

**[!UICONTROL Connect to Salesforce Service Cloud]**&#x200B;頁面隨即顯示。 您可以在此頁面使用新的證明資料或現有的證明資料。

### 使用現有帳戶

若要使用現有帳戶，請選取&#x200B;**[!UICONTROL Existing account]**，然後從顯示的清單中選取所需的帳戶。 完成後，選取&#x200B;**[!UICONTROL Next]**&#x200B;以繼續。

![貴組織中已經存在的已驗證Salesforce Service Cloud帳戶清單。](../../../../images/tutorials/create/salesforce-service-cloud/existing.png)

### 建立新帳戶

若要建立新帳戶，請選取&#x200B;**[!UICONTROL New account]**&#x200B;並為您的新[!DNL Salesforce Service Cloud]帳戶提供名稱和說明。 接著，選取&#x200B;**[!UICONTROL OAuth2 Client Credential]**，然後提供下列認證的值：

* 環境 URL
* 用戶端 ID
* 用戶端密碼
* API 版本

完成後，選取&#x200B;**[!UICONTROL Connect to source]**。

![用於建立Salesforce帳戶的OAuth介面。](../../../../images/tutorials/create/salesforce-service-cloud/new.png)

## 後續步驟

依照本教學課程中的指示，您已建立與[!DNL Salesforce Service Cloud]帳戶的連線。 您現在可以繼續進行下一個教學課程，並[設定資料流，將客戶成功資料匯入Experience Platform](../../dataflow/customer-success.md)。
