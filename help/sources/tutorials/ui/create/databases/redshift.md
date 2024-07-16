---
title: 在UI中建立Amazon Redshift Source連線
description: 瞭解如何使用Adobe Experience Platform UI建立Amazon Redshift來源連線。
badgeUltimate: label="Ultimate" type="Positive"
exl-id: 4faf3200-673b-4a20-8f94-d049e800444b
source-git-commit: a7c2c5e4add5c80e0622d5aeb766cec950d79dbb
workflow-type: tm+mt
source-wordcount: '486'
ht-degree: 3%

---

# 使用來源工作區連線您的[!DNL Amazon Redshift]帳戶

>[!IMPORTANT]
>
>[!DNL Amazon Redshift]來源可在來源目錄中提供給已購買Real-time Customer Data Platform Ultimate的使用者。

本教學課程提供如何使用使用者介面將您的[!DNL Amazon Redshift] （以下稱為「[!DNL Redshift]」）帳戶連線至Adobe Experience Platform的步驟。

## 快速入門

本教學課程需要您實際瞭解下列Experience Platform元件：

- [[!DNL Experience Data Model (XDM)] 系統](../../../../../xdm/home.md)：Experience Platform用來組織客戶體驗資料的標準化架構。
   - [結構描述組合的基本概念](../../../../../xdm/schema/composition.md)：瞭解XDM結構描述的基本建置區塊，包括結構描述組合中的關鍵原則和最佳實務。
   - [結構描述編輯器教學課程](../../../../../xdm/tutorials/create-schema-ui.md)：瞭解如何使用結構描述編輯器使用者介面建立自訂結構描述。
- [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md)：根據來自多個來源的彙總資料，提供統一的即時消費者設定檔。

如果您已經有有效的[!DNL Redshift]連線，您可以略過本檔案的其餘部分，並繼續進行有關[設定資料流](../../dataflow/databases.md)的教學課程。

### 收集必要的認證

若要在Experience Platform上存取您的[!DNL Redshift]帳戶，您必須提供下列值：

| **認證** | **說明** |
| -------------- | --------------- |
| 伺服器 | 與您的[!DNL Redshift]帳戶關聯的伺服器。 |
| 連接埠 | [!DNL Redshift]伺服器用來監聽使用者端連線的TCP連線埠。 |
| 使用者名稱 | 與您的[!DNL Redshift]帳戶相關聯的使用者名稱。 |
| 密碼 | 與您的[!DNL Redshift]帳戶關聯的密碼。 |
| 資料庫 | 您正在存取的[!DNL Redshift]資料庫。 |

如需開始使用的詳細資訊，請參閱[此 [!DNL Redshift] 檔案](https://docs.aws.amazon.com/redshift/latest/gsg/getting-started.html)。

收集必要的認證後，您可以依照下列步驟連結您的[!DNL Redshift]帳戶以Experience Platform。

## 連線您的[!DNL Redshift]帳戶

>[!NOTE]
>
>[!DNL Redshift]的預設編碼標準為Unicode。 無法變更此設定。

登入[Adobe Experience Platform](https://platform.adobe.com)，然後從左側導覽列中選取&#x200B;**[!UICONTROL 來源]**&#x200B;以存取&#x200B;**[!UICONTROL 來源]**&#x200B;工作區。 **[!UICONTROL 目錄]**&#x200B;畫面會顯示您可以建立帳戶的各種來源。

您可以從熒幕左側的目錄中選取適當的類別。 或者，您可以使用搜尋選項來尋找您要使用的特定來源。

在&#x200B;**[!UICONTROL 資料庫]**&#x200B;類別下，選取&#x200B;**[!UICONTROL Amazon Redshift]**。 如果這是您第一次使用此聯結器，請選取&#x200B;**[!UICONTROL 設定]**。 否則，請選取&#x200B;**[!UICONTROL 新增資料]**&#x200B;以建立新的[!DNL Redshift]聯結器。

![](../../../../images/tutorials/create/redshift/catalog.png)

**[!UICONTROL 連線至Amazon Redshift]**&#x200B;頁面隨即顯示。 您可以在此頁面使用新的證明資料或現有的證明資料。

### 新帳戶

如果您正在使用新認證，請選取&#x200B;**[!UICONTROL 新帳戶]**。 在出現的輸入表單上，提供名稱、選擇性說明和您的[!DNL Redshift]認證。 完成時，請選取&#x200B;**[!UICONTROL 連線]**，然後等待一段時間以建立新連線。

![](../../../../images/tutorials/create/redshift/new.png)

### 現有帳戶

若要連線現有帳戶，請選取您要連線的[!DNL Redshift]帳戶，然後選取[下一步]**[!UICONTROL 以繼續。]**

![](../../../../images/tutorials/create/redshift/existing.png)

## 後續步驟

依照本教學課程中的指示，您已建立與[!DNL Redshift]帳戶的連線。 您現在可以繼續進行下一個教學課程，並[設定資料流以將資料帶入Experience Platform](../../dataflow/databases.md)。
