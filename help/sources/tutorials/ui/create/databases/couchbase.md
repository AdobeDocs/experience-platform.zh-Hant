---
keywords: Experience Platform；首頁；熱門主題；Couchbase；Couchbase
solution: Experience Platform
title: 在使用者介面中建立Couchbase Source連線
type: Tutorial
description: 瞭解如何使用Adobe Experience Platform UI建立Couchbase來源連線。
exl-id: 4270a48a-843c-4f1e-b280-35b620581d68
source-git-commit: 474b81aa8caf58013f8ea7cff9ad59d92466aac8
workflow-type: tm+mt
source-wordcount: '457'
ht-degree: 2%

---

# 在使用者介面中建立[!DNL Couchbase]來源連線

>[!WARNING]
>
>[!DNL Couchbase]來源將於2025年5月底淘汰。

[!DNL Adobe Experience Platform]中的Source聯結器可讓您依排程擷取外部來源的資料。 本教學課程提供使用[!DNL Platform]使用者介面建立[!DNL Couchbase]來源聯結器的步驟。

## 快速入門

此教學課程需要您實際瞭解[!DNL Platform]的下列元件：

* [[!DNL Experience Data Model (XDM)] 系統](../../../../../xdm/home.md)： [!DNL Experience Platform]用來組織客戶體驗資料的標準化架構。
   * [結構描述組合的基本概念](../../../../../xdm/schema/composition.md)：瞭解XDM結構描述的基本建置區塊，包括結構描述組合中的關鍵原則和最佳實務。
   * [結構描述編輯器教學課程](../../../../../xdm/tutorials/create-schema-ui.md)：瞭解如何使用結構描述編輯器使用者介面建立自訂結構描述。
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md)：根據來自多個來源的彙總資料，提供統一的即時消費者設定檔。

如果您已經有有效的[!DNL Couchbase]連線，您可以略過本檔案的其餘部分，並繼續進行有關[設定資料流](../../dataflow/databases.md)的教學課程。

### 收集必要的認證

為了驗證您的[!DNL Couchbase]來源聯結器，您必須提供下列連線屬性的值：

| 認證 | 說明 |
| ---------- | ----------- |
| `connectionString` | 用來連線至您[!DNL Couchbase]執行個體的連線字串。 [!DNL Couchbase]的連線字串模式為`Server={SERVER}; Port={PORT};AuthMech=1;CredString=[{\"user\": \"{USER}\", \"pass\":\"{PASS}\"}];`。 如需取得連線字串的詳細資訊，請參閱[[!DNL Couchbase] 連線](https://docs.Couchbase.com/c-sdk/2.10/client-settings.html#configuring-overview)的檔案。 |

## 連線您的[!DNL Couchbase]帳戶

收集必要的認證後，您可以依照下列步驟將[!DNL Couchbase]帳戶連結至[!DNL Platform]。

登入[Adobe Experience Platform](https://platform.adobe.com)，然後從左側導覽列中選取&#x200B;**[!UICONTROL 來源]**&#x200B;以存取&#x200B;**[!UICONTROL 來源]**&#x200B;工作區。 **[!UICONTROL 目錄]**&#x200B;畫面會顯示您可以建立帳戶的各種來源。

您可以從熒幕左側的目錄中選取適當的類別。 或者，您可以使用搜尋選項來尋找您要使用的特定來源。

在&#x200B;**[!UICONTROL 資料庫]**&#x200B;類別下，選取&#x200B;**[!UICONTROL Couchbase]**。 如果這是您第一次使用此聯結器，請選取&#x200B;**[!UICONTROL 設定]**。 否則，請選取&#x200B;**[!UICONTROL 新增資料]**&#x200B;以建立新的[!DNL Couchbase]聯結器。

![目錄](../../../../images/tutorials/create/couchbase/catalog.png)

**[!UICONTROL 連線至Couchbase]**&#x200B;頁面就會顯示。 您可以在此頁面使用新的證明資料或現有的證明資料。

### 新帳戶

如果您正在使用新認證，請選取&#x200B;**[!UICONTROL 新帳戶]**。 在出現的輸入表單上，提供名稱、選擇性說明和您的[!DNL Couchbase]認證。 完成時，請選取&#x200B;**[!UICONTROL 連線到來源]**，然後等待一段時間以建立新連線。

![連線](../../../../images/tutorials/create/couchbase/new.png)

### 現有帳戶

若要連線現有帳戶，請選取您要連線的[!DNL Couchbase]帳戶，然後在右上角選取&#x200B;**[!UICONTROL 下一步]**&#x200B;以繼續。

![現有](../../../../images/tutorials/create/couchbase/existing.png)

## 後續步驟

依照本教學課程中的指示，您已建立與[!DNL Couchbase]帳戶的連線。 您現在可以繼續進行下一個教學課程，並[設定資料流以將資料帶入 [!DNL Platform]](../../dataflow/databases.md)。
