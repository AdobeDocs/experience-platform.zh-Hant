---
keywords: Experience Platform；首頁；熱門主題；hubspot；Hubspot
solution: Experience Platform
title: 在使用者介面中建立HubSpot Source連線
type: Tutorial
description: 瞭解如何使用Adobe Experience Platform UI建立HubSpot來源連線。
exl-id: 452b7290-b9e8-4728-8b58-0e0c76bd9449
source-git-commit: b48c24ac032cbf785a26a86b50a669d7fcae5d97
workflow-type: tm+mt
source-wordcount: '461'
ht-degree: 2%

---

# 在使用者介面中建立[!DNL HubSpot]來源連線

Adobe Experience Platform中的Source聯結器可讓您依排程擷取外部來源資料。 本教學課程提供使用[!DNL Experience Platform]使用者介面建立[!DNL HubSpot]來源聯結器的步驟。

## 快速入門

本教學課程需要您實際瞭解下列Adobe Experience Platform元件：

* [[!DNL Experience Data Model (XDM)] 系統](../../../../../xdm/home.md)： [!DNL Experience Platform]用來組織客戶體驗資料的標準化架構。
   * [結構描述組合的基本概念](../../../../../xdm/schema/composition.md)：瞭解XDM結構描述的基本建置區塊，包括結構描述組合中的關鍵原則和最佳實務。
   * [結構描述編輯器教學課程](../../../../../xdm/tutorials/create-schema-ui.md)：瞭解如何使用結構描述編輯器使用者介面建立自訂結構描述。
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md)：根據來自多個來源的彙總資料，提供統一的即時消費者設定檔。

如果您已有[!DNL HubSpot]連線，可以略過本檔案的其餘部分，並繼續進行有關[設定資料流](../../dataflow/marketing-automation.md)的教學課程。

### 收集必要的認證

若要在[!DNL Experience Platform]上存取您的[!DNL HubSpot]帳戶，您必須提供下列值：

| 認證 | 說明 |
| ---------- | ----------- |
| `clientId` | 與您的[!DNL HubSpot]應用程式關聯的使用者端識別碼。 |
| `clientSecret` | 與您的[!DNL HubSpot]應用程式關聯的使用者端密碼。 |
| `accessToken` | 最初驗證您的OAuth整合時獲得的存取權杖。 |
| `refreshToken` | 重新整理權杖是在最初驗證您的OAuth整合時取得。 |

如需開始使用的詳細資訊，請參閱此[[!DNL HubSpot] 檔案](https://developers.hubspot.com/docs/methods/oauth2/oauth2-overview)。

## 連線您的[!DNL HubSpot]帳戶

收集必要的認證後，您可以依照下列步驟將[!DNL HubSpot]帳戶連結至[!DNL Experience Platform]。

登入[Adobe Experience Platform](https://platform.adobe.com)，然後從左側導覽列中選取&#x200B;**[!UICONTROL 來源]**&#x200B;以存取&#x200B;**[!UICONTROL 來源]**&#x200B;工作區。 **[!UICONTROL 目錄]**&#x200B;畫面會顯示您可以建立帳戶的各種來源。

您可以從熒幕左側的目錄中選取適當的類別。 或者，您可以使用搜尋選項來尋找您要使用的特定來源。

在&#x200B;**[!UICONTROL 行銷自動化]**&#x200B;類別下，選取&#x200B;**[!UICONTROL HubSpot]**。 如果這是您第一次使用此聯結器，請選取&#x200B;**[!UICONTROL 設定]**。 否則，請選取&#x200B;**[!UICONTROL 新增資料]**&#x200B;以建立新的[!DNL HubSpot]聯結器。

![目錄](../../../../images/tutorials/create/hubspot/catalog.png)

**[!UICONTROL 連線到HubSpot]**&#x200B;頁面就會顯示。 您可以在此頁面使用新的證明資料或現有的證明資料。

### 新帳戶

如果您正在使用新認證，請選取&#x200B;**[!UICONTROL 新帳戶]**。 在出現的輸入表單上，提供名稱、選擇性說明和您的[!DNL HubSpot]認證。 完成時，請選取&#x200B;**[!UICONTROL 連線]**，然後等待一段時間以建立新連線。

![連線](../../../../images/tutorials/create/hubspot/connect.png)

### 現有帳戶

若要連線現有帳戶，請選取您要連線的[!DNL HubSpot]帳戶，然後選取[下一步]&#x200B;**[!UICONTROL 以繼續。]**

![現有](../../../../images/tutorials/create/hubspot/existing.png)

## 後續步驟

依照本教學課程中的指示，您已建立與[!DNL HubSpot]帳戶的連線。 您現在可以繼續進行下一個教學課程，並[設定資料流，以將行銷自動化系統資料匯入 [!DNL Experience Platform]](../../dataflow/marketing-automation.md)。
