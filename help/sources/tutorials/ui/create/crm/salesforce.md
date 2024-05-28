---
title: 使用Experience Platform使用者介面連線您的Salesforce帳戶
description: 瞭解如何使用使用者介面連線您的Salesforce帳戶並將您的CRM資料帶入Experience Platform。
exl-id: b67fa4c4-d8ff-4d2d-aa76-5d9d32aa22d6
source-git-commit: 7930a869627130a5db34780e64b809cda0c1e5f4
workflow-type: tm+mt
source-wordcount: '829'
ht-degree: 3%

---

# 連線您的 [!DNL Salesforce] 要使用UIExperience Platform的帳戶

本教學課程提供如何連線至 [!DNL Salesforce] 透過Experience Platform使用者介面，將您的CRM資料帶入Adobe Experience Platform。

## 快速入門

本教學課程需要您實際瞭解下列Experience Platform元件：

* [[!DNL Experience Data Model (XDM)] 系統](../../../../../xdm/home.md)：Experience Platform組織客戶體驗資料的標準化架構。
   * [結構描述組合基本概念](../../../../../xdm/schema/composition.md)：瞭解XDM結構描述的基本建置區塊，包括結構描述組合中的關鍵原則和最佳實務。
   * [結構描述編輯器教學課程](../../../../../xdm/tutorials/create-schema-ui.md)：瞭解如何使用結構編輯器UI建立自訂結構描述。
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md)：根據來自多個來源的彙總資料，提供統一的即時消費者個人檔案。

如果您已經驗證 [!DNL Salesforce] 帳戶，您可以略過本檔案的其餘部分，並前往上的教學課程 [為CRM資料設定資料流](../../dataflow/crm.md).

### 收集必要的認證 {#gather-required-credentials}

此 [!DNL Salesforce] 來源支援基本驗證和OAuth2使用者端認證。

>[!BEGINTABS]

>[!TAB 基本驗證]

您必須提供下列認證的值，才能連線 [!DNL Salesforce] 使用基本驗證的帳戶。

| 認證 | 說明 |
| --- | --- |
| 環境 URL | 的URL [!DNL Salesforce] 來源執行個體。 |
| 使用者名稱 | 的使用者名稱 [!DNL Salesforce] 使用者帳戶。 |
| 密碼 | 的密碼 [!DNL Salesforce] 使用者帳戶。 |
| 安全性權杖 | 的安全性權杖 [!DNL Salesforce] 使用者帳戶。 |
| API版本 | （選用）的REST API版本 [!DNL Salesforce] 您正在使用的例項。 API版本的值必須使用小數點格式化。 例如，如果您使用API版本 `52`，則您必須輸入值為 `52.0`. 如果此欄位留空，則Experience Platform將自動使用最新可用版本。 |

有關驗證的詳細資訊，請參閱 [此 [!DNL Salesforce] 驗證指南](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/quickstart_oauth.htm).

>[!TAB OAuth2使用者端認證]

您必須提供下列認證的值，才能連線 [!DNL Salesforce] 使用OAuth2使用者端認證的帳戶。

| 認證 | 說明 |
| --- | --- |
| 環境 URL | 的URL [!DNL Salesforce] 來源執行個體。 |
| 用戶端 ID | 使用者端ID會與使用者端密碼搭配使用，作為OAuth2驗證的一部分。 使用者端ID和使用者端密碼可讓您的應用程式透過識別您的應用程式來代表您的帳戶運作。 [!DNL Salesforce]. |
| 用戶端密碼 | 使用者端密碼會與使用者端ID搭配使用，做為OAuth2驗證的一部分。 使用者端ID和使用者端密碼可讓您的應用程式透過識別您的應用程式來代表您的帳戶運作。 [!DNL Salesforce]. |
| API版本 | 的REST API版本 [!DNL Salesforce] 您正在使用的例項。 API版本的值必須使用小數點格式化。 例如，如果您使用API版本 `52`，則您必須輸入值為 `52.0`. 如果此欄位留空，則Experience Platform將自動使用最新可用版本。 |

如需為使用OAuth的詳細資訊 [!DNL Salesforce]，閱讀 [[!DNL Salesforce] OAuth授權流程指南](https://help.salesforce.com/s/articleView?id=sf.remoteaccess_oauth_flows.htm&amp;type=5).

>[!ENDTABS]

收集必要的認證後，您可以依照下列步驟連線 [!DNL Salesforce] 要Experience Platform的帳戶。

## 連線您的 [!DNL Salesforce] 帳戶

在Platform UI中選取 **[!UICONTROL 來源]** 從左側導覽存取 [!UICONTROL 來源] 工作區。 您可以從熒幕左側的目錄中選取適當的類別。 或者，您可以使用搜尋選項來尋找您要使用的特定來源。

選取 **[!DNL Salesforce]** 在 *[!UICONTROL CRM]* 類別，然後選取 **[!UICONTROL 新增資料]**.

>[!TIP]
>
>來源目錄中的來源會顯示 **[!UICONTROL 設定]** 選項，當指定的來源尚未擁有已驗證的帳戶時。 一旦驗證帳戶存在，此選項就會變更為 **[!UICONTROL 新增資料]**.

![已選取Salesforce來源卡片的Experience PlatformUI上的來源目錄。](../../../../images/tutorials/create/salesforce/catalog.png)

此 **[!UICONTROL 連線到Salesforce]** 頁面便會顯示。 您可以在此頁面使用新的證明資料或現有的證明資料。

### 使用現有帳戶

若要使用現有帳戶，請選取 **[!UICONTROL 現有帳戶]** 然後從顯示的清單中選取您要使用的帳戶。 完成後，選取 **[!UICONTROL 下一個]** 以繼續進行。

![貴組織中已經存在的已驗證Salesforce帳戶清單。](../../../../images/tutorials/create/salesforce/existing.png)

### 建立新帳戶

若要建立新帳戶，請選取 **[!UICONTROL 新帳戶]** 並為您的新檔案提供名稱和說明 [!DNL Salesforce] 帳戶。

![您可以在其中提供適當的驗證憑證來建立新Salesforce帳戶的介面。](../../../../images/tutorials/create/salesforce/new.png)

接著，選取您要用於新帳戶的驗證型別。

>[!BEGINTABS]

>[!TAB 基本驗證]

對於基本驗證，請選取 **[!UICONTROL 基本驗證]** 然後提供下列認證的值：

* 環境 URL
* 使用者名稱
* 密碼
* API版本（選擇性）

完成後，選取 **[!UICONTROL 連線到來源]**.

![建立Salesforce帳戶的基本驗證介面。](../../../../images/tutorials/create/salesforce/basic.png)

>[!TAB OAuth2使用者端認證]

針對OAuth 2使用者端認證，選取 **[!UICONTROL OAuth2使用者端認證]** 然後提供下列認證的值：

* 環境 URL
* 用戶端 ID
* 用戶端密碼
* API版本

完成後，選取 **[!UICONTROL 連線到來源]**.

![Salesforce帳戶建立的OAuth介面。](../../../../images/tutorials/create/salesforce/oauth2.png)

>[!ENDTABS]

## 後續步驟

依照本教學課程中的指示，您已建立與的連線， [!DNL Salesforce] 帳戶。 您現在可以繼續進行下一個教學課程及 [設定資料流以將資料帶入 [!DNL Platform]](../../dataflow/crm.md).
