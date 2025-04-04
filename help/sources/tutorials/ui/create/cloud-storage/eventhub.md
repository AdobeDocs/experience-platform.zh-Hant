---
title: 在使用者介面中建立Azure事件中樞Source連線
description: 瞭解如何使用Adobe Experience Platform UI建立Azure事件中樞來源連線。
badgeUltimate: label="Ultimate" type="Positive"
exl-id: 7e67e213-8ccb-4fa5-b09f-ae77aba8614c
source-git-commit: fded2f25f76e396cd49702431fa40e8e4521ebf8
workflow-type: tm+mt
source-wordcount: '1098'
ht-degree: 3%

---

# 在使用者介面中建立[!DNL Azure Event Hubs]來源連線

>[!IMPORTANT]
>
>[!DNL Azure Event Hubs]來源可在來源目錄中提供給已購買Real-Time Customer Data Platform Ultimate的使用者。

閱讀本教學課程，瞭解如何使用Adobe Experience Platform使用者介面建立[!DNL Azure Event Hubs]帳戶。

## 快速入門

本教學課程需要您實際瞭解下列Adobe Experience Platform元件：

* [[!DNL Experience Data Model (XDM)] 系統](../../../../../xdm/home.md)： [!DNL Experience Platform]用來組織客戶體驗資料的標準化架構。
   * [結構描述組合的基本概念](../../../../../xdm/schema/composition.md)：瞭解XDM結構描述的基本建置區塊，包括結構描述組合中的關鍵原則和最佳實務。
   * [結構描述編輯器教學課程](../../../../../xdm/tutorials/create-schema-ui.md)：瞭解如何使用結構描述編輯器使用者介面建立自訂結構描述。
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md)：根據來自多個來源的彙總資料，提供統一的即時消費者設定檔。

如果您已經有有效的[!DNL Event Hubs]連線，您可以略過本檔案的其餘部分，並繼續進行有關[設定資料流](../../dataflow/streaming/cloud-storage-streaming.md)的教學課程。

### 收集必要的認證

為了驗證您的[!DNL Event Hubs]來源聯結器，您必須提供下列連線屬性的值：

>[!BEGINTABS]

>[!TAB 標準驗證]

| 認證 | 說明 |
| --- | --- |
| SAS 金鑰名稱 | 授權規則的名稱，也稱為SAS金鑰名稱。 |
| SAS 金鑰 | [!DNL Event Hubs]名稱空間的主索引鍵。 `sasKey`對應的`sasPolicy`必須已設定`manage`許可權，才能填入[!DNL Event Hubs]清單。 |
| 命名空間 | 您正在存取的[!DNL Event Hub]的名稱空間。 [!DNL Event Hub]名稱空間提供唯一的範圍設定容器，您可以在其中建立一或多個[!DNL Event Hubs]。 |

>[!TAB SAS驗證]

| 認證 | 說明 |
| --- | --- |
| SAS 金鑰名稱 | 授權規則的名稱，也稱為SAS金鑰名稱。 |
| SAS 金鑰 | [!DNL Event Hub]名稱空間的主索引鍵。 `sasKey`對應的`sasPolicy`必須已設定`manage`許可權，才能填入[!DNL Event Hubs]清單。 |
| 命名空間 | 您正在存取的[!DNL Event Hub]的名稱空間。 [!DNL Event Hub]名稱空間提供唯一的範圍設定容器，您可以在其中建立一或多個[!DNL Event Hubs]。 |
| 事件中心名稱 | 填寫您的[!DNL Azure Event Hub]名稱。 閱讀[Microsoft檔案](https://learn.microsoft.com/en-us/azure/event-hubs/event-hubs-create#create-an-event-hub)以瞭解[!DNL Event Hub]名稱的詳細資訊。 |

>[!TAB 事件中心Azure Active Directory驗證]

| 認證 | 說明 |
| --- | --- |
| 租用戶 ID | 您要向其請求許可權的租使用者ID。 您可以將您的租使用者ID格式化為GUID或友好名稱。 **注意**：租使用者ID在[!DNL Microsoft Azure]介面中稱為「目錄ID」。 |
| 用戶端 ID | 指派給應用程式的應用程式ID。 您可以從您註冊[!DNL Azure Active Directory]的[!DNL Microsoft Entra ID]入口網站擷取此ID。 |
| 使用者端密碼值 | 使用者端密碼與使用者端ID搭配使用，用來驗證您的應用程式。 您可以從您註冊[!DNL Azure Active Directory]的[!DNL Microsoft Entra ID]入口網站擷取您的使用者端密碼。 |
| 命名空間 | 您正在存取的[!DNL Event Hub]的名稱空間。 [!DNL Event Hub]名稱空間提供唯一的範圍設定容器，您可以在其中建立一或多個[!DNL Event Hubs]。 |

如需[!DNL Azure Active Directory]的詳細資訊，請閱讀[使用Microsoft Entra ID](https://learn.microsoft.com/en-us/azure/healthcare-apis/register-application)的Azure指南。

>[!TAB 事件中樞範圍的Azure Active Directory驗證]

| 認證 | 說明 |
| --- | --- |
| 租用戶 ID | 您要向其請求許可權的租使用者ID。 您可以將您的租使用者ID格式化為GUID或友好名稱。 **注意**：租使用者ID在[!DNL Microsoft Azure]介面中稱為「目錄ID」。 |
| 用戶端 ID | 指派給應用程式的應用程式ID。 您可以從您註冊[!DNL Azure Active Directory]的[!DNL Microsoft Entra ID]入口網站擷取此ID。 |
| 使用者端密碼值 | 使用者端密碼與使用者端ID搭配使用，用來驗證您的應用程式。 您可以從您註冊[!DNL Azure Active Directory]的[!DNL Microsoft Entra ID]入口網站擷取您的使用者端密碼。 |
| 命名空間 | 您正在存取的[!DNL Event Hub]的名稱空間。 [!DNL Event Hub]名稱空間提供唯一的範圍設定容器，您可以在其中建立一或多個[!DNL Event Hubs]。 |
| 事件中心名稱 | 填寫您的[!DNL Azure Event Hub]名稱。 閱讀[Microsoft檔案](https://learn.microsoft.com/en-us/azure/event-hubs/event-hubs-create#create-an-event-hub)以瞭解[!DNL Event Hub]名稱的詳細資訊。 |

如需[!DNL Azure Active Directory]的詳細資訊，請閱讀[使用Microsoft Entra ID](https://learn.microsoft.com/en-us/azure/healthcare-apis/register-application)的Azure指南。

>[!ENDTABS]

收集必要的認證後，您可以依照下列步驟將[!DNL Event Hubs]帳戶連結至Experience Platform。

## 連線您的[!DNL Event Hubs]帳戶

在Experience Platform UI中，從左側導覽選取&#x200B;**[!UICONTROL 來源]**&#x200B;以存取[!UICONTROL 來源]工作區。 [!UICONTROL 目錄]畫面會顯示您可以用來建立帳戶的各種來源。

您可以從熒幕左側的目錄中選取適當的類別。 或者，您可以使用搜尋選項來尋找您要使用的特定來源。

在[!UICONTROL 雲端儲存空間]類別下，選取&#x200B;**[!UICONTROL Azure事件中樞]**，然後選取&#x200B;**[!UICONTROL 新增資料]**。

![已選取Azure事件中樞的來源目錄。](../../../../images/tutorials/create/eventhub/catalog.png)

**[!UICONTROL 連線到Azure事件中樞]**&#x200B;對話方塊就會顯示。 您可以在此頁面使用新的證明資料或現有的證明資料。

### 現有帳戶

若要使用現有帳戶，請選取您要使用的[!DNL Event Hubs]帳戶，然後選取[下一步] **[!UICONTROL 以繼續。]**

![現有Azure事件中樞來源帳戶的清單。](../../../../images/tutorials/create/eventhub/existing.png)

### 新帳戶

>[!TIP]
>
>建立後，您無法變更[!DNL Event Hubs]基本連線的驗證型別。 若要變更驗證型別，您必須建立新的基礎連線。

若要建立新帳戶，請選取&#x200B;**[!UICONTROL 新帳戶]**，然後為您的新[!DNL Event Hubs]帳戶提供名稱和選擇性描述。

![Azure事件中樞的新帳戶建立介面。](../../../../images/tutorials/create/eventhub/new.png)

>[!BEGINTABS]

>[!TAB 標準驗證]

若要使用標準驗證建立[!DNL Event Hubs]帳戶，請使用[!UICONTROL 帳戶驗證]下拉式功能表，然後選取&#x200B;**[!UICONTROL 標準驗證]**。 接下來，提供您的[!UICONTROL SAS金鑰名稱]、[!UICONTROL SAS金鑰]和[!UICONTROL 名稱空間]的值。

輸入驗證認證後，請選取&#x200B;**[!UICONTROL 連線至來源]**。

![Azure事件中樞的標準驗證介面。](../../../../images/tutorials/create/eventhub/standard.png)

>[!TAB SAS驗證]

若要建立具有SAS驗證的[!DNL Event Hubs]帳戶，請使用[!UICONTROL 帳戶驗證]下拉式功能表，然後選取&#x200B;**[!UICONTROL SAS驗證]**。 接著，提供您的[!UICONTROL SAS金鑰名稱]、[!UICONTROL SAS金鑰]、[!UICONTROL 名稱空間]和[!UICONTROL 事件中樞名稱]的值。

輸入驗證認證後，請選取&#x200B;**[!UICONTROL 連線至來源]**。

![Azure事件中樞的SAS驗證介面。](../../../../images/tutorials/create/eventhub/sas.png)

>[!TAB 事件中心Azure Active Directory驗證]

若要建立具有事件中心Azure Active Directory驗證的[!DNL Event Hubs]帳戶，請使用[!UICONTROL 帳戶驗證]下拉式功能表，然後選取&#x200B;**[!UICONTROL 事件中心Azure Active Directory]**。 接著，提供您[!UICONTROL 租使用者識別碼]、[!UICONTROL 使用者端識別碼]、[!UICONTROL 使用者端密碼值]和[!UICONTROL 名稱空間]的值。

![Azure事件中心Azure Active Directory驗證](../../../../images/tutorials/create/eventhub/active-directory.png)

>[!TAB 事件中樞範圍的Azure Active Directory驗證]

若要建立具有事件中心範圍的Azure Active Directory驗證的[!DNL Event Hubs]帳戶，請使用[!UICONTROL 帳戶驗證]下拉式功能表，然後選取&#x200B;**[!UICONTROL 事件中心範圍的Azure Active Directory]**。 接著，提供您[!UICONTROL 租使用者識別碼]、[!UICONTROL 使用者端識別碼]、[!UICONTROL 使用者端密碼值]、[!UICONTROL 名稱空間]和[!UICONTROL 事件中心名稱]的值。

![Azure事件中心範圍的Azure活動目錄驗證](../../../../images/tutorials/create/eventhub/scoped.png)

>[!ENDTABS]


## 後續步驟

依照此教學課程，您已將[!DNL Event Hubs]帳戶連線至Experience Platform。 您現在可以繼續進行下一個教學課程，並[設定資料流，將您的雲端儲存空間中的資料匯入Experience Platform](../../dataflow/streaming/cloud-storage-streaming.md)。
