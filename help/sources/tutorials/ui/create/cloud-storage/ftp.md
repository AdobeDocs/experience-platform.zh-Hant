---
keywords: Experience Platform；首頁；熱門主題；FTP；ftp
solution: Experience Platform
title: 在使用者介面中建立FTP Source連線
type: Tutorial
description: 瞭解如何使用Adobe Experience Platform UI建立FTP來源連線。
exl-id: 8e505ead-4bae-43fe-830b-75620e8fba28
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '464'
ht-degree: 2%

---

# 在使用者介面中建立FTP來源連線

>[!NOTE]
>
>FTP聯結器為Beta版。 如需使用Beta標籤聯結器的詳細資訊，請參閱[來源概觀](../../../../home.md#terms-and-conditions)。

本教學課程提供使用Adobe Experience Platform UI建立FTP來源連線的步驟。

## 快速入門

本教學課程需要您實際瞭解下列Adobe Experience Platform元件：

* [[!DNL Experience Data Model (XDM)] 系統](../../../../../xdm/home.md)： Experience Platform用來組織客戶體驗資料的標準化架構。
   * [結構描述組合的基本概念](../../../../../xdm/schema/composition.md)：瞭解XDM結構描述的基本建置區塊，包括結構描述組合中的關鍵原則和最佳實務。
   * [結構描述編輯器教學課程](../../../../../xdm/tutorials/create-schema-ui.md)：瞭解如何使用結構描述編輯器使用者介面建立自訂結構描述。
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md)：根據來自多個來源的彙總資料，提供統一的即時消費者設定檔。

如果您已經有有效的FTP連線，可以略過本檔案的其餘部分，並繼續進行有關[設定資料流](../../dataflow/batch/cloud-storage.md)的教學課程。

### 收集必要的認證

若要連線至FTP，您必須提供下列連線屬性的值：

| 認證 | 說明 |
| ---------- | ----------- |
| `host` | 與您的FTP伺服器關聯的名稱或IP位址。 |
| `username` | 可存取您FTP伺服器的使用者名稱。 |
| `password` | FTP伺服器的密碼。 |

## 連線至您的FTP伺服器

收集完所需的認證後，您可以依照下列步驟建立新的FTP帳戶以連線至Experience Platform。

登入[Adobe Experience Platform](https://platform.adobe.com)，然後從左側導覽列中選取&#x200B;**[!UICONTROL 來源]**&#x200B;以存取[!UICONTROL 來源]工作區。 [!UICONTROL 目錄]畫面會顯示各種來源，您可為這些來源建立傳入帳戶。

您可以從熒幕左側的目錄中選取適當的類別。 或者，您可以使用搜尋選項來尋找您要使用的特定來源。

在[!UICONTROL 雲端儲存空間]類別下，選取&#x200B;**[!UICONTROL FTP]**。 如果這是您第一次使用此聯結器，請選取&#x200B;**[!UICONTROL 設定]**。 否則，請選取&#x200B;**[!UICONTROL 新增資料]**&#x200B;以建立新的FTP連線。

![目錄](../../../../images/tutorials/create/ftp/catalog.png)

**[!UICONTROL 連線至FTP]**&#x200B;頁面隨即顯示。 您可以在此頁面使用新的證明資料或現有的證明資料。

### 新帳戶

如果您正在使用新認證，請選取&#x200B;**[!UICONTROL 新帳戶]**。 在出現的輸入表單上，提供名稱、選擇性說明和您的認證。 完成時，請選取&#x200B;**[!UICONTROL 連線]**，然後等待一段時間以建立新連線。

![新](../../../../images/tutorials/create/ftp/new.png)

### 現有帳戶

若要連線現有帳戶，請選取您要連線的FTP帳戶，然後選取[下一步] **[!UICONTROL 以繼續。]**

![現有](../../../../images/tutorials/create/ftp/existing.png)

## 後續步驟

依照本教學課程中的指示，您已建立與FTP帳戶的連線。 您現在可以繼續進行下一個教學課程，並[設定資料流，將您的雲端儲存空間中的資料匯入Experience Platform](../../dataflow/batch/cloud-storage.md)。
