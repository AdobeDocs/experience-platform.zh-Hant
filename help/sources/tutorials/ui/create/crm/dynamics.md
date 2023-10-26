---
keywords: Experience Platform；首頁；熱門主題；Microsoft Dynamics；microsoft dynamics；Dynamics；dynamics
solution: Experience Platform
title: 在UI中建立Microsoft Dynamics來源連線
type: Tutorial
description: 瞭解如何使用Microsoft UI建立Adobe Experience Platform Dynamics來源連線。
exl-id: 1a7a66de-dc57-4a72-8fdd-5fd80175db69
source-git-commit: d22c71fb77655c401f4a336e339aaf8b3125d1b6
workflow-type: tm+mt
source-wordcount: '620'
ht-degree: 0%

---

# 建立 [!DNL Microsoft Dynamics] ui中的來源連線

本教學課程提供建立 [!DNL Microsoft Dynamics] (以下稱「[!DNL Dynamics]&quot;)使用Adobe Experience Platform UI的來源連線。

## 快速入門

本教學課程需要您實際瞭解下列Adobe Experience Platform元件：

* [[!DNL Experience Data Model (XDM)] 系統](../../../../../xdm/home.md)：Experience Platform組織客戶體驗資料的標準化架構。
   * [結構描述組合基本概念](../../../../../xdm/schema/composition.md)：瞭解XDM結構描述的基本建置區塊，包括結構描述組合中的關鍵原則和最佳實務。
   * [結構描述編輯器教學課程](../../../../../xdm/tutorials/create-schema-ui.md)：瞭解如何使用結構編輯器UI建立自訂結構描述。
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md)：根據來自多個來源的彙總資料，提供統一的即時消費者個人檔案。

如果您已有有效的 [!DNL Dynamics] 帳戶，您可以略過本檔案的其餘部分，並前往上的教學課程 [為CRM來源設定資料流](../../dataflow/crm.md).

### 收集必要的認證

為了驗證您的 [!DNL Dynamics] 來源，您必須提供下列連線屬性的值：

>[!BEGINTABS]

>[!TAB 基本驗證]

| 認證 | 說明 |
| --- | --- |
| `serviceUri` | 您的服務URL [!DNL Dynamics] 執行個體。 |
| `username` | 您的使用者名稱 [!DNL Dynamics] 使用者帳戶。 |
| `password` | 您的密碼 [!DNL Dynamics] 帳戶。 |

>[!TAB 服務主體和金鑰驗證]

| 認證 | 說明 |
| --- | --- |
| `servicePrincipalId` | 您的使用者端識別碼 [!DNL Dynamics] 帳戶。 使用服務主體和金鑰式驗證時，需要此ID。 |
| `servicePrincipalKey` | 服務主體秘密金鑰。 使用服務主體和金鑰式驗證時，需要此認證。 |

>[!ENDTABS]

如需開始使用的詳細資訊，請參閱 [此 [!DNL Dynamics] 檔案](https://docs.microsoft.com/en-us/powerapps/developer/common-data-service/authenticate-oauth).

## 連線您的 [!DNL Dynamics] 帳戶

在Platform UI中選取 **[!UICONTROL 來源]** 從左側導覽存取 [!UICONTROL 來源] 工作區。 此 [!UICONTROL 目錄] 畫面會顯示各種來源，供您建立帳戶。

您可以從熒幕左側的目錄中選取適當的類別。 或者，您可以使用搜尋選項來尋找您要使用的特定來源。

在 [!UICONTROL CRM] 類別，選取 **[!UICONTROL Microsoft Dynamics]**，然後選取 **[!UICONTROL 新增資料]**.

![已選取Microsoft Dynamics的來源目錄。](../../../../images/tutorials/create/ms-dynamics/catalog.png)

此 **[!UICONTROL 連線Microsoft Dynamics帳戶]** 頁面便會顯示。 您可以在此頁面使用新的證明資料或現有的證明資料。

### 現有帳戶

若要使用現有帳戶，請選取 [!DNL Dynamics] 要使用的帳戶，然後選取 **[!UICONTROL 下一個]** 前往右上角繼續。

![現有的帳戶介面。](../../../../images/tutorials/create/ms-dynamics/existing.png)

### 新帳戶

>[!TIP]
>
>建立後，您就無法變更的驗證型別 [!DNL Dynamics] 基礎連線。 若要變更驗證型別，您必須建立新的基礎連線。

若要建立新帳戶，請選取 **[!UICONTROL 新帳戶]**，然後為您的新專案提供名稱和說明（選用） [!DNL Dynamics] 帳戶。

![新帳戶建立介面。](../../../../images/tutorials/create/ms-dynamics/new.png)

建立時，您可以使用基本驗證或服務主體和金鑰驗證 [!DNL Dynamics] 帳戶。

>[!BEGINTABS]

>[!TAB 基本驗證]

若要建立 [!DNL Dynamics] 具有基本驗證的帳戶，請選取 [!UICONTROL 基本驗證] 然後為您的欄位提供值 [!UICONTROL 服務URI]， [!UICONTROL 使用者名稱]、和 [!UICONTROL 密碼]. **注意**：中的基本驗證 [!DNL Dynamics] 雙因素驗證可能會加以封鎖，目前平台不支援此功能。 在此情況下，建議使用金鑰式驗證來建立來源聯結器，使用 [!DNL Dynamics].

完成後，選取 **[!UICONTROL 連線到來源]** 然後留出一些時間建立新帳戶。

![基本驗證介面。](../../../../images/tutorials/create/ms-dynamics/basic-authentication.png)

>[!TAB 服務主體和金鑰驗證]

若要建立 [!DNL Dynamics] 具有服務主體和金鑰驗證的帳戶，請選取 **[!UICONTROL 服務主體和金鑰驗證]** 然後為您的欄位提供值 [!UICONTROL 服務主體ID] 和 [!UICONTROL 服務主體金鑰].

完成後，選取 **[!UICONTROL 連線到來源]** 然後留出一些時間建立新帳戶。

![服務主體金鑰驗證介面。](../../../../images/tutorials/create/ms-dynamics/service-principal.png)

>[!ENDTABS]

## 後續步驟

依照本教學課程中的指示，您已建立與的連線， [!DNL Dynamics] 帳戶。 您現在可以繼續進行下一個教學課程及 [設定資料流以將資料匯入Platform](../../dataflow/crm.md).
