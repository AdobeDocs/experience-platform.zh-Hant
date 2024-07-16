---
keywords: Experience Platform；首頁；熱門主題；Azure Data Lake Storage Gen2；ADLS Gen2；adls gen2；adls聯結器
solution: Experience Platform
title: 在UI中建立Azure Data Lake Storage Gen2 Source連線
type: Tutorial
description: 瞭解如何使用Adobe Experience Platform UI建立Azure Data Lake Storage Gen2來源連線。
exl-id: d81b7593-08a3-43f8-a8bc-f5547a6cd55a
source-git-commit: ed92bdcd965dc13ab83649aad87eddf53f7afd60
workflow-type: tm+mt
source-wordcount: '478'
ht-degree: 1%

---

# 在使用者介面中建立[!DNL Azure Data Lake Storage Gen2]來源連線

Adobe Experience Platform中的Source聯結器可讓您依排程擷取外部來源資料。 本教學課程提供使用[!DNL Platform]使用者介面驗證[!DNL Azure Data Lake Storage Gen2] （以下稱為「[!DNL ADLS Gen2]」）來源聯結器的步驟。

## 快速入門

本教學課程需要您實際瞭解下列Adobe Experience Platform元件：

- [[!DNL Experience Data Model (XDM)] 系統](../../../../../xdm/home.md)： [!DNL Experience Platform]用來組織客戶體驗資料的標準化架構。
   - [結構描述組合的基本概念](../../../../../xdm/schema/composition.md)：瞭解XDM結構描述的基本建置區塊，包括結構描述組合中的關鍵原則和最佳實務。
   - [結構描述編輯器教學課程](../../../../../xdm/tutorials/create-schema-ui.md)：瞭解如何使用結構描述編輯器使用者介面建立自訂結構描述。
- [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md)：根據來自多個來源的彙總資料，提供統一的即時消費者設定檔。

如果您已經有有效的ADLS Gen2連線，您可以略過本檔案的其餘部分，並繼續進行有關[設定資料流](../../dataflow/batch/cloud-storage.md)的教學課程。

### 收集必要的認證

為了驗證您的[!DNL ADLS Gen2]來源聯結器，您必須提供下列連線屬性的值：

| 認證 | 說明 |
| ---------- | ----------- |
| `url` | [!DNL ADLS Gen2]的端點。 |
| `servicePrincipalId` | 應用程式的使用者端ID。 |
| `servicePrincipalKey` | 應用程式的索引鍵。 |
| `tenant` | 包含您應用程式的租使用者資訊。 |

如需這些值的詳細資訊，請參閱[此 [!DNL ADLS Gen2] 檔案](https://docs.microsoft.com/en-us/azure/data-factory/connector-azure-data-lake-storage)。

## 連線您的[!DNL ADLS Gen2]帳戶

收集必要的認證後，您可以依照下列步驟連結[!DNL ADLS Gen2]帳戶以連線至[!DNL Platform]。

登入[Adobe Experience Platform](https://platform.adobe.com)，然後從左側導覽列中選取&#x200B;**[!UICONTROL 來源]**&#x200B;以存取&#x200B;**[!UICONTROL 來源]**&#x200B;工作區。 **[!UICONTROL 目錄]**&#x200B;畫面會顯示您可以建立帳戶的各種來源。

您可以從熒幕左側的目錄中選取適當的類別。 或者，您可以使用搜尋選項來尋找您要使用的特定來源。

在&#x200B;**[!UICONTROL 資料庫]**&#x200B;類別下，選取&#x200B;**[!UICONTROL Azure Data Lake Gen2]**。 如果這是您第一次使用此聯結器，請選取&#x200B;**[!UICONTROL 設定]**。 否則，請選取&#x200B;**[!UICONTROL 新增資料]**&#x200B;以建立新的ADLS Gen2聯結器。

![](../../../../images/tutorials/create/adls-gen2/catalog.png)

**[!UICONTROL 連線至Azure Data Lake Gen2]**&#x200B;對話方塊就會顯示。 您可以在此頁面使用新的證明資料或現有的證明資料。

### 新帳戶

如果您正在使用新認證，請選取&#x200B;**[!UICONTROL 新帳戶]**。 在出現的輸入表單上，提供名稱、選擇性說明和您的[!DNL ADLS Gen2]認證。 完成時，請選取&#x200B;**[!UICONTROL 連線]**，然後等待一段時間以建立新連線。

![](../../../../images/tutorials/create/adls-gen2/connect.png)

### 現有帳戶

若要連線現有帳戶，請選取您要連線的[!DNL ADLS Gen2]帳戶，然後選取[下一步]**[!UICONTROL 以繼續。]**

![](../../../../images/tutorials/create/adls-gen2/existing.png)

## 後續步驟

依照本教學課程中的指示，您已建立與[!DNL ADLS Gen2]帳戶的連線。 您現在可以繼續進行下一個教學課程，並[設定資料流，將雲端儲存空間中的資料匯入 [!DNL Platform]](../../dataflow/batch/cloud-storage.md)。
