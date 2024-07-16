---
title: 在使用者介面中建立Google Ads Source連線
description: 瞭解如何使用Google UI建立Adobe Experience Platform Ads來源連線。
exl-id: 33dd2857-aed3-4e35-bc48-1c756a8b3638
source-git-commit: ce3dabe4ab08a41e581b97b74b3abad352e3267c
workflow-type: tm+mt
source-wordcount: '680'
ht-degree: 2%

---

# 在UI中建立Google Ads來源連線

>[!WARNING]
>
>[!DNL Google Ads]來源暫時無法使用。 Adobe正在努力解決此來源的問題。

>[!NOTE]
>
>Google Ads來源為測試版。 如需使用Beta版標籤來源的相關資訊，請參閱[來源概觀](../../../../home.md#terms-and-conditions)。

本教學課程提供使用Google使用者介面建立Adobe Experience Platform Ads來源連線的步驟。

## 快速入門

本教學課程需要您實際瞭解下列Experience Platform元件：

* [[!DNL Experience Data Model (XDM)] 系統](../../../../../xdm/home.md)：Experience Platform用來組織客戶體驗資料的標準化架構。
   * [結構描述組合的基本概念](../../../../../xdm/schema/composition.md)：瞭解XDM結構描述的基本建置區塊，包括結構描述組合中的關鍵原則和最佳實務。
   * [結構描述編輯器教學課程](../../../../../xdm/tutorials/create-schema-ui.md)：瞭解如何使用結構描述編輯器使用者介面建立自訂結構描述。
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md)：根據來自多個來源的彙總資料，提供統一的即時消費者設定檔。

如果您已經有有效的Google Ads連線，可以略過本檔案的其餘部分，並繼續進行有關[設定資料流](../../dataflow/advertising.md)的教學課程

### 收集必要的認證

若要存取Google Ads帳戶平台，您必須提供下列值：

| 認證 | 說明 |
| ---------- | ----------- |
| 用戶端客戶 ID | 使用者端客戶ID為對應至您要使用Google Ads API管理的Google Ads使用者端帳戶的帳號。 此ID遵循`123-456-7890`的範本。 |
| 登入客戶ID | 登入客戶ID是與您的Google Ads管理員帳戶對應的帳號，用於擷取特定營運客戶的報表資料。 如需登入客戶ID的詳細資訊，請參閱[Google Ads API檔案](https://developers.google.com/search-ads/reporting/concepts/login-customer-id)。 |
| 開發人員權杖 | 開發人員Token可讓您存取Google Ads API。 您可以使用相同的開發人員Token，對所有Google Ads帳戶提出要求。 [登入您的管理員帳戶](https://ads.google.com/home/tools/manager-accounts/)，然後導覽至API中心頁面，以擷取您的開發人員權杖。 |
| 重新整理權杖 | 重新整理權杖是[!DNL OAuth2]驗證的一部分。 此權杖可讓您在存取權杖過期後重新產生存取權杖。 |
| 用戶端 ID | 使用者端ID與使用者端密碼搭配使用，是[!DNL OAuth2]驗證的一部分。 使用者端ID和使用者端密碼可讓您的應用程式藉由在Google中識別您的應用程式，以代表您的帳戶運作。 |
| 用戶端密碼 | 使用者端密碼會與使用者端ID搭配使用，作為[!DNL OAuth2]驗證的一部分。 使用者端ID和使用者端密碼可讓您的應用程式藉由在Google中識別您的應用程式，以代表您的帳戶運作。 |

閱讀API概觀檔案，以瞭解[開始使用Google Ads的詳細資訊](https://developers.google.com/google-ads/api/docs/first-call/overview)。

## 連線您的Google Ads帳戶

在Platform UI中，從左側導覽列選取&#x200B;**[!UICONTROL 來源]**&#x200B;以存取[!UICONTROL 來源]工作區。 [!UICONTROL 目錄]畫面會顯示您可以建立帳戶的各種來源。

您可以從熒幕左側的目錄中選取適當的類別。 或者，您可以使用搜尋選項來尋找您要使用的特定來源。

在&#x200B;**[!UICONTROL Advertising]**&#x200B;類別下，選取&#x200B;**[!UICONTROL Google Ads]**，然後選取&#x200B;**[!UICONTROL 新增資料]**。

![Experience PlatformUI中的來源目錄。](../../../../images/tutorials/create/ads/catalog.png)。

**[!UICONTROL 連線至Google Ads]**&#x200B;頁面隨即顯示。 您可以在此頁面使用新的證明資料或現有的證明資料。

### 現有帳戶

若要連線現有帳戶，請選取您要連線的Google Ads帳戶，然後選取[下一步] **[!UICONTROL 以繼續。]**

![來源工作流程中現有帳戶的選擇頁面。](../../../../images/tutorials/create/ads/existing.png)。

### 新帳戶

如果您正在使用新認證，請選取&#x200B;**[!UICONTROL 新帳戶]**。 在出現的輸入表單中，提供名稱、選擇性說明，以及您的Google Ads認證。 完成時，請選取&#x200B;**[!UICONTROL 連線到來源]**，然後等待一段時間以建立新連線。

![來源工作流程中的新帳戶介面。](../../../../images/tutorials/create/ads/new.png)。

## 後續步驟

依照本教學課程中的指示，您已建立與Google Ads帳戶的連線。 您現在可以繼續進行下一個教學課程，並[設定資料流以將廣告資料帶入Platform](../../dataflow/advertising.md)。
