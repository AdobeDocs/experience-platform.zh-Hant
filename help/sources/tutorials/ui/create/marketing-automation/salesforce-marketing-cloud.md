---
title: 連線您的SalesforceMarketing Cloud帳戶，以透過UIExperience Platform
description: 瞭解如何連線您的SalesforceMarketing Cloud帳戶，以透過UIExperience Platform。
exl-id: 1d9bde60-31e0-489c-9c1c-b6471e0ea554
source-git-commit: 0e3fee4d78646b1d1d6730495358b3ced4127f4e
workflow-type: tm+mt
source-wordcount: '517'
ht-degree: 2%

---

# 連線您的[!DNL Salesforce Marketing Cloud]帳戶以透過UIExperience Platform

>[!IMPORTANT]
>
>[!DNL Salesforce Marketing Cloud]來源將於2025年5月底淘汰。 作為替代方法，您可以使用[[!DNL Data Landing Zone]](../cloud-storage/data-landing-zone.md)來源。

本教學課程提供如何透過UI將您的[!DNL Salesforce Marketing Cloud]帳戶連線至Adobe Experience Platform的步驟。

## 快速入門

本教學課程需要您實際瞭解下列Experience Platform元件：

* [[!DNL Experience Data Model (XDM)] 系統](../../../../../xdm/home.md)： [!DNL Experience Platform]用來組織客戶體驗資料的標準化架構。
   * [結構描述組合的基本概念](../../../../../xdm/schema/composition.md)：瞭解XDM結構描述的基本建置區塊，包括結構描述組合中的關鍵原則和最佳實務。
   * [結構描述編輯器教學課程](../../../../../xdm/tutorials/create-schema-ui.md)：瞭解如何使用結構描述編輯器使用者介面建立自訂結構描述。
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md)：根據來自多個來源的彙總資料，提供統一的即時消費者設定檔。

如果您已有[!DNL Salesforce Marketing Cloud]帳戶，您可以略過本檔案的其餘部分，並繼續進行有關[使用UI](../../dataflow/marketing-automation.md)將行銷自動化資料帶入Experience Platform的教學課程。

### 收集必要的認證

若要在Platform上存取您的[!DNL Salesforce Marketing Cloud]帳戶，您必須提供下列值：

| 認證 | 說明 |
| ---------- | ----------- |
| Host | 應用程式的主機伺服器。 這通常是您的子網域。 **注意：**&#x200B;輸入`host`值時，您必須指定`{subdomain}.rest.marketingcloudapis.com`。 例如，如果您的主機URL是`https://acme-ab12c3d4e5fg6hijk7lmnop8qrst.auth.marketingcloudapis.com/`，則必須輸入`acme-ab12c3d4e5fg6hijk7lmnop8qrst.rest.marketingcloudapis.com/`作為主機值。 |
| 用戶端 ID | 與您的[!DNL Salesforce Marketing Cloud]應用程式關聯的使用者端識別碼。 |
| 用戶端密碼 | 與您的[!DNL Salesforce Marketing Cloud]應用程式關聯的使用者端密碼。 |

如需[!DNL Salesforce Marketing Cloud]驗證的詳細資訊，請瀏覽[[!DNL Salesforce] 驗證檔案](https://developer.salesforce.com/docs/atlas.en-us.mc-apis.meta/mc-apis/authentication.htm)。

## 連線您的[!DNL Salesforce Marketing Cloud]帳戶

>[!IMPORTANT]
>
>[!DNL Salesforce Marketing Cloud]來源整合目前不支援自訂物件擷取。

在Platform UI中，從左側導覽選取&#x200B;**[!UICONTROL 來源]**&#x200B;以存取[!UICONTROL 來源]工作區。 [!UICONTROL 目錄]顯示Experience Platform支援的各種來源。

您可以從類別清單中選取適當的類別。 您也可以使用搜尋列來篩選特定來源。

在[!UICONTROL 行銷自動化]類別下，選取&#x200B;**[!UICONTROL SalesforceMarketing Cloud]**，然後選取&#x200B;**[!UICONTROL 設定]**。

![已選取SalesforceMarketing Cloud來源的來源目錄。](../../../../images/tutorials/create/salesforce-marketing-cloud/catalog.png)

**[!UICONTROL 連線至SalesforceMarketing Cloud]**&#x200B;頁面隨即顯示。 您可以在此頁面上建立新帳戶或使用現有帳戶。

### 新帳戶

若要建立新帳戶，請選取「**[!UICONTROL 新帳戶]**」，並提供您帳戶的名稱、選擇性說明，以及與您[!DNL Salesforce Marketing Cloud]帳戶對應的驗證認證。

完成時，請選取&#x200B;**[!UICONTROL 連線到來源]**，然後等待一段時間以建立新連線。

![新帳戶介面，您可以在此介面驗證SalesforceMarketing Cloud的新帳戶。](../../../../images/tutorials/create/salesforce-marketing-cloud/new.png)

### 現有帳戶

如果您已有現有的帳戶，請選取&#x200B;**[!UICONTROL 現有的帳戶]**，然後從顯示的清單中選取您要使用的帳戶。

![您可以從現有SalesforceMarketing Cloud帳戶清單中選取的現有帳戶介面。](../../../../images/tutorials/create/salesforce-marketing-cloud/existing.png)

## 後續步驟

依照本教學課程中的指示，您已建立[!DNL Salesforce Marketing Cloud]帳戶與Experience Platform之間的連線。 您現在可以繼續進行下一個教學課程，並[建立資料流，將您的行銷自動化資料匯入Experience Platform](../../dataflow/marketing-automation.md)。
