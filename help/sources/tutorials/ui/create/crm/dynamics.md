---
keywords: Experience Platform；首頁；熱門主題；Microsoft Dynamics；microsoft dynamics；Dynamics；Dynamics
solution: Experience Platform
title: 在使用者介面中建立Microsoft Dynamics Source連線
type: Tutorial
description: 瞭解如何使用Microsoft Dynamics UI建立Adobe Experience Platform來源連線。
exl-id: 1a7a66de-dc57-4a72-8fdd-5fd80175db69
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '617'
ht-degree: 1%

---

# 在使用者介面中建立[!DNL Microsoft Dynamics]來源連線

本教學課程提供使用Adobe Experience Platform UI建立[!DNL Microsoft Dynamics] （以下稱為「[!DNL Dynamics]」）來源連線的步驟。

## 快速入門

本教學課程需要您實際瞭解下列Adobe Experience Platform元件：

* [[!DNL Experience Data Model (XDM)] 系統](../../../../../xdm/home.md)： Experience Platform用來組織客戶體驗資料的標準化架構。
   * [結構描述組合的基本概念](../../../../../xdm/schema/composition.md)：瞭解XDM結構描述的基本建置區塊，包括結構描述組合中的關鍵原則和最佳實務。
   * [結構描述編輯器教學課程](../../../../../xdm/tutorials/create-schema-ui.md)：瞭解如何使用結構描述編輯器使用者介面建立自訂結構描述。
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md)：根據來自多個來源的彙總資料，提供統一的即時消費者設定檔。

如果您已經有有效的[!DNL Dynamics]帳戶，您可以略過本檔案的其餘部分，並繼續進行有關[為CRM來源設定資料流](../../dataflow/crm.md)的教學課程。

### 收集必要的認證

為了驗證您的[!DNL Dynamics]來源，您必須提供下列連線屬性的值：

>[!BEGINTABS]

>[!TAB 基本驗證]

| 認證 | 說明 |
| --- | --- |
| `serviceUri` | [!DNL Dynamics]執行個體的服務URL。 |
| `username` | 您的[!DNL Dynamics]使用者帳戶的使用者名稱。 |
| `password` | 您的[!DNL Dynamics]帳戶密碼。 |

>[!TAB 服務主體和金鑰驗證]

| 認證 | 說明 |
| --- | --- |
| `servicePrincipalId` | 您[!DNL Dynamics]帳戶的使用者端識別碼。 使用服務主體和金鑰式驗證時，需要此ID。 |
| `servicePrincipalKey` | 服務主體秘密金鑰。 使用服務主體和金鑰式驗證時，需要此認證。 |

>[!ENDTABS]

如需開始使用的詳細資訊，請參閱[此 [!DNL Dynamics] 檔案](https://docs.microsoft.com/en-us/powerapps/developer/common-data-service/authenticate-oauth)。

## 連線您的[!DNL Dynamics]帳戶

在Experience Platform UI中，從左側導覽選取&#x200B;**[!UICONTROL 來源]**&#x200B;以存取[!UICONTROL 來源]工作區。 [!UICONTROL 目錄]畫面會顯示您可以用來建立帳戶的各種來源。

您可以從熒幕左側的目錄中選取適當的類別。 或者，您可以使用搜尋選項來尋找您要使用的特定來源。

在[!UICONTROL CRM]類別下，選取&#x200B;**[!UICONTROL Microsoft Dynamics]**，然後選取&#x200B;**[!UICONTROL 新增資料]**。

![已選取Microsoft Dynamics的來源目錄。](../../../../images/tutorials/create/ms-dynamics/catalog.png)

**[!UICONTROL 連線Microsoft Dynamics帳戶]**&#x200B;頁面隨即顯示。 您可以在此頁面使用新的證明資料或現有的證明資料。

### 現有帳戶

若要使用現有帳戶，請選取您要使用的[!DNL Dynamics]帳戶，然後在右上角選取「**[!UICONTROL 下一步]**」以繼續。

![現有的帳戶介面。](../../../../images/tutorials/create/ms-dynamics/existing.png)

### 新帳戶

>[!TIP]
>
>建立後，您無法變更[!DNL Dynamics]基本連線的驗證型別。 若要變更驗證型別，您必須建立新的基礎連線。

若要建立新帳戶，請選取&#x200B;**[!UICONTROL 新帳戶]**，然後為您的新[!DNL Dynamics]帳戶提供名稱和選擇性描述。

![新帳戶建立介面。](../../../../images/tutorials/create/ms-dynamics/new.png)

建立[!DNL Dynamics]帳戶時，您可以使用基本驗證或服務主體和金鑰驗證。

>[!BEGINTABS]

>[!TAB 基本驗證]

若要建立具有基本驗證的[!DNL Dynamics]帳戶，請選取[!UICONTROL 基本驗證]，然後提供您的[!UICONTROL 服務URI]、[!UICONTROL 使用者名稱]和[!UICONTROL 密碼]的值。 **注意**： [!DNL Dynamics]中的基本驗證可能被Experience Platform目前不支援的雙重因素驗證封鎖。 在此情況下，建議使用金鑰式驗證，以使用[!DNL Dynamics]建立來源聯結器。

完成時，請選取&#x200B;**[!UICONTROL 連線到來源]**，然後留出一些時間建立新帳戶。

![基本驗證介面。](../../../../images/tutorials/create/ms-dynamics/basic-authentication.png)

>[!TAB 服務主體和金鑰驗證]

若要建立具有服務主體和金鑰驗證的[!DNL Dynamics]帳戶，請選取&#x200B;**[!UICONTROL 服務主體和金鑰驗證]**，然後提供您的[!UICONTROL 服務主體識別碼]和[!UICONTROL 服務主體金鑰]的值。

完成時，請選取&#x200B;**[!UICONTROL 連線到來源]**，然後留出一些時間建立新帳戶。

![服務主體金鑰驗證介面。](../../../../images/tutorials/create/ms-dynamics/service-principal.png)

>[!ENDTABS]

## 後續步驟

依照本教學課程中的指示，您已建立與[!DNL Dynamics]帳戶的連線。 您現在可以繼續進行下一個教學課程，並[設定資料流以將資料帶入Experience Platform](../../dataflow/crm.md)。
