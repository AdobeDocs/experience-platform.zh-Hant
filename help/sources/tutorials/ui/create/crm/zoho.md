---
keywords: Experience Platform；首頁；熱門主題；Zoho CRM；zoho crm；Zoho；zoho
solution: Experience Platform
title: 在使用者介面中建立Zoho CRM Source連線
type: Tutorial
description: 瞭解如何使用Adobe Experience Platform UI建立Zoho CRM來源連線。
exl-id: c648fc3e-beea-4030-8d36-dd8a7e2c281e
source-git-commit: 474b81aa8caf58013f8ea7cff9ad59d92466aac8
workflow-type: tm+mt
source-wordcount: '550'
ht-degree: 2%

---

# 在使用者介面中建立[!DNL Zoho CRM]來源連線

>[!WARNING]
>
>[!DNL Zoho CRM]來源將於2025年6月底淘汰。

Adobe Experience Platform中的Source聯結器可讓您依排程擷取外部來源的CRM資料。 本教學課程提供使用[!DNL Platform]使用者介面建立[!DNL Zoho CRM]來源聯結器的步驟。

## 快速入門

本教學課程需要您實際瞭解下列Adobe Experience Platform元件：

* [[!DNL Experience Data Model (XDM)] 系統](../../../../../xdm/home.md)： [!DNL Experience Platform]用來組織客戶體驗資料的標準化架構。
   * [結構描述組合的基本概念](../../../../../xdm/schema/composition.md)：瞭解XDM結構描述的基本建置區塊，包括結構描述組合中的關鍵原則和最佳實務。
   * [結構描述編輯器教學課程](../../../../../xdm/tutorials/create-schema-ui.md)：瞭解如何使用結構描述編輯器使用者介面建立自訂結構描述。
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md)：根據來自多個來源的彙總資料，提供統一的即時消費者設定檔。

如果您已經有有效的[!DNL Zoho CRM]帳戶，您可以略過本檔案的其餘部分，並繼續進行有關[設定資料流](../../dataflow/crm.md)的教學課程。

### 收集必要的認證

為了將[!DNL Zoho CRM]連線到Platform，您必須提供下列連線屬性的值：

| 認證 | 說明 |
| --- | --- |
| 端點 | 您向其提出請求的[!DNL Zoho CRM]伺服器端點。 |
| 帳戶URL | 帳戶URL會用於產生存取和重新整理Token。 URL必須是網域專屬的。 |
| 用戶端 ID | 與您的[!DNL Zoho CRM]使用者帳戶對應的使用者端識別碼。 |
| 使用者端密碼 | 與您的[!DNL Zoho CRM]使用者帳戶對應的使用者端密碼。 |
| 存取權杖 | 存取Token授權您對您的[!DNL Zoho CRM]帳戶的安全與暫時存取。 |
| 重新整理Token | 重新整理權杖是在您的存取權杖過期後，用來產生新存取權杖的權杖。 |

如需這些認證的詳細資訊，請參閱有關[[!DNL Zoho CRM] 驗證](https://www.zoho.com/crm/developer/docs/api/v2/oauth-overview.html)的檔案。

## 連線您的[!DNL Zoho CRM]帳戶

收集必要的認證後，您可以依照下列步驟將[!DNL Zoho CRM]帳戶連結至[!DNL Platform]。

在Platform UI中，從左側導覽列選取&#x200B;**[!UICONTROL 來源]**&#x200B;以存取[!UICONTROL 來源]工作區。 [!UICONTROL 目錄]畫面會顯示您可以建立帳戶的各種來源。

您可以從熒幕左側的目錄中選取適當的類別。 或者，您可以使用搜尋選項來尋找您要使用的特定來源。

在[!UICONTROL CRM]類別下，選取&#x200B;**[!UICONTROL Zoho CRM]**，然後選取&#x200B;**[!UICONTROL 新增資料]**。

![目錄](../../../../images/tutorials/create/zoho/catalog.png)

**[!UICONTROL Connect Zoho CRM帳戶]**&#x200B;頁面隨即顯示。 您可以在此頁面使用新的證明資料或現有的證明資料。

### 現有帳戶

若要使用現有帳戶，請選取您要用來建立新資料流的[!DNL Zoho CRM]帳戶，然後選取[下一步] ]**以繼續。**[!UICONTROL 

![現有](../../../../images/tutorials/create/zoho/existing.png)

### 新帳戶

如果您正在建立新帳戶，請選取&#x200B;**[!UICONTROL 新帳戶]**，然後提供名稱、選擇性說明以及您的[!DNL Zoho CRM]認證。 完成時，請選取&#x200B;**[!UICONTROL 連線到來源]**，然後等待一段時間以建立新連線。

>[!TIP]
>
>您的帳戶URL網域必須符合您適當的網域位置。 以下是各種網域及其對應的帳戶URL：<ul><li>美國： https://accounts.zoho.com</li><li>澳洲： https://accounts.zoho.com.au</li><li>歐洲： https://accounts.zoho.eu</li><li>印度： https://accounts.zoho.in</li><li>中國： https://accounts.zoho.com.cn</li></ul>

![新](../../../../images/tutorials/create/zoho/new.png)

## 後續步驟

依照本教學課程中的指示，您已建立與[!DNL Zoho CRM]帳戶的連線。 您現在可以繼續進行下一個教學課程，並[設定資料流以將資料帶入Platform](../../dataflow/crm.md)。
