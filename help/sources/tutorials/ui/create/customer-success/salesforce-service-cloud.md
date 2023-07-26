---
title: 使用Experience Platform使用者介面連線您的Salesforce Service Cloud帳戶
description: 瞭解如何使用使用者介面連線您的Salesforce Service Cloud帳戶並將您的客戶成功資料帶入Experience Platform。
exl-id: 38480a29-7852-46c6-bcea-5dc6bffdbd15
source-git-commit: 57cdcbd5018e7f57261f09c6bddf5e2a8dcfd0d5
workflow-type: tm+mt
source-wordcount: '540'
ht-degree: 0%

---

# 連線您的 [!DNL Salesforce Service Cloud] 要使用UIExperience Platform的帳戶

本教學課程提供如何連線至 [!DNL Salesforce Service Cloud] 透過Experience Platform使用者介面將客戶成功資料帶入Adobe Experience Platform。

## 快速入門

本教學課程需要您實際瞭解下列Experience Platform元件：

* [[!DNL Experience Data Model (XDM)] 系統](../../../../../xdm/home.md)：Experience Platform組織客戶體驗資料的標準化架構。
   * [結構描述組合基本概念](../../../../../xdm/schema/composition.md)：瞭解XDM結構描述的基本建置區塊，包括結構描述組合中的關鍵原則和最佳實務。
   * [結構描述編輯器教學課程](../../../../../xdm/tutorials/create-schema-ui.md)：瞭解如何使用結構編輯器UI建立自訂結構描述。
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md)：根據來自多個來源的彙總資料，提供統一的即時消費者個人檔案。

如果您已有有效的 [!DNL Salesforce Service Cloud] 連線時，您可以略過本檔案的其餘部分，並繼續進行上的教學課程 [設定資料流讓客戶成功](../../dataflow/customer-success.md)

### 收集必要的認證

為了存取您的 [!DNL Salesforce Service Cloud] account onExperience Platform，您必須提供下列值：

| 認證 | 說明 |
| --- | --- |
| `environmentUrl` | 的URL [!DNL Salesforce Service Cloud] 來源執行個體。 |
| `username` | 的使用者名稱 [!DNL Salesforce Service Cloud] 使用者帳戶。 |
| `password` | 的密碼 [!DNL Salesforce Service Cloud] 使用者帳戶。 |
| `securityToken` | 的安全性權杖 [!DNL Salesforce Service Cloud] 使用者帳戶。 |
| `apiVersion` | （選用）的REST API版本 [!DNL Salesforce Service Cloud] 您正在使用的例項。 如果此欄位留空，則Experience Platform將自動使用最新可用版本。 |

有關驗證的詳細資訊，請參閱 [此 [!DNL Salesforce] 驗證指南](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/quickstart_oauth.htm).

## 連線您的 [!DNL Salesforce Service Cloud] 帳戶

收集必要的認證後，您可以依照下列步驟連結 [!DNL Salesforce] 要Experience Platform的帳戶。

在Platform UI中選取 **[!UICONTROL 來源]** 從左側導覽存取來源工作區。 此 *[!UICONTROL 目錄]* 畫面會顯示Experience Platform來源目錄中的各種可用來源。

您可以從熒幕左側的目錄中選取適當的類別。 或者，您可以使用搜尋選項來尋找特定來源。

選取 **[!UICONTROL 客戶成功]** 從來源類別清單中，然後選取 **[!UICONTROL 新增資料]** 從 [!DNL Salesforce Service Cloud] 卡片。

![已選取Salesforce Service Cloud來源卡的Experience PlatformUI上的來源目錄。](../../../../images/tutorials/create/salesforce-service-cloud/catalog.png)

此 **[!UICONTROL 連線到Salesforce Service Cloud]** 頁面便會顯示。 您可以在此頁面使用新的證明資料或現有的證明資料。

>[!BEGINTABS]

>[!TAB 使用現有的Salesforce Service Cloud帳戶]

若要使用現有帳戶，請選取 **[!UICONTROL 現有帳戶]** 然後從顯示的清單中選取您要使用的帳戶。 完成後，選取 **[!UICONTROL 下一個]** 以繼續進行。

![貴組織中已經存在的已驗證Salesforce帳戶清單。](../../../../images/tutorials/create/salesforce-service-cloud/existing.png)

>[!TAB 建立新的Salesforce Service Cloud帳戶]

若要使用新帳戶，請選取 **[!UICONTROL 新帳戶]** 並提供名稱、說明，以及 [!DNL Salesforce Service Cloud] 驗證認證。 完成後，選取 **[!UICONTROL 連線到來源]** 並等待幾秒鐘，以便建立新連線。

![您可以在其中提供適當的驗證憑證來建立新Salesforce帳戶的介面。](../../../../images/tutorials/create/salesforce-service-cloud/new.png)

>[!ENDTABS]

## 後續步驟

依照本教學課程中的指示，您已建立與的連線， [!DNL Salesforce Service Cloud] 帳戶。 您現在可以繼續進行下一個教學課程及 [設定資料流以將客戶成功資料匯入Experience Platform](../../dataflow/customer-success.md).
