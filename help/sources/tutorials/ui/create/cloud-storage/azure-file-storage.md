---
keywords: Experience Platform；首頁；熱門主題；Azure檔案儲存；Azure檔案儲存連接器
solution: Experience Platform
title: 在UI中建立Azure檔案儲存源連接
topic-legacy: overview
type: Tutorial
description: 了解如何使用Adobe Experience Platform UI建立Azure檔案儲存來源連線。
exl-id: 25d483b6-3975-4e80-9dbe-28b7b91cb063
source-git-commit: e150f05df2107d7b3a2e95a55dc4ad072294279e
workflow-type: tm+mt
source-wordcount: '470'
ht-degree: 1%

---

# 在UI中建立[!DNL Azure File Storage]源連接

Adobe Experience Platform中的來源連接器可讓您依排程內嵌外部來源資料。 本教學課程提供使用[!DNL Platform]使用者介面驗證[!DNL Azure File Storage]來源連接器的步驟。

## 快速入門

本教學課程需要妥善了解下列Adobe Experience Platform元件：

- [[!DNL Experience Data Model (XDM)] 系統](../../../../../xdm/home.md):組織客戶體驗資 [!DNL Experience Platform] 料的標準化架構。
   - [結構構成基本概念](../../../../../xdm/schema/composition.md):了解XDM結構描述的基本建置組塊，包括結構描述的主要原則和最佳實務。
   - [結構編輯器教學課程](../../../../../xdm/tutorials/create-schema-ui.md):了解如何使用結構編輯器UI建立自訂結構。
- [[!DNL Real-time Customer Profile]](../../../../../profile/home.md):根據來自多個來源的匯總資料，提供統一的即時消費者設定檔。

如果已經有有效的[!DNL Azure File Storage]連接，則可以跳過本文檔的其餘部分，並繼續進行[配置資料流](../../dataflow/batch/cloud-storage.md)的教程。

### 收集所需憑據

要驗證[!DNL Azure File Storage]源連接器，必須為以下連接屬性提供值：

| 憑據 | 說明 |
| ---------- | ----------- |
| `host` | 您正在訪問的[!DNL Azure File Storage]實例的端點。 |
| `userId` | 對[!DNL Azure File Storage]端點具有足夠訪問權限的用戶。 |
| `password` | [!DNL Azure File Storage]訪問密鑰。 |

有關入門的詳細資訊，請參閱[this [!DNL Azure File Storage] document](https://docs.microsoft.com/en-us/azure/storage/files/storage-how-to-use-files-windows)。

## 連接您的[!DNL Azure File Storage]帳戶

收集到所需憑據後，可以按照以下步驟將[!DNL Azure File Storage]帳戶連結到[!DNL Platform]。

登入[Adobe Experience Platform](https://platform.adobe.com)，然後從左側導覽列選取&#x200B;**[!UICONTROL 來源]**&#x200B;以存取&#x200B;**[!UICONTROL 來源]**&#x200B;工作區。 **[!UICONTROL 目錄]**&#x200B;螢幕顯示了各種源，您可以用這些源建立帳戶。

您可以從畫面左側的目錄中選取適當的類別。 或者，您也可以使用搜尋選項找到您要使用的特定來源。

在&#x200B;**[!UICONTROL 資料庫]**&#x200B;類別下，選擇&#x200B;**[!UICONTROL Azure檔案儲存]**。 如果這是您第一次使用此連接器，請選擇&#x200B;**[!UICONTROL 配置]**。 否則，選擇&#x200B;**[!UICONTROL 添加資料]**&#x200B;以建立新的[!DNL Azure File Storage]連接器。

![目錄](../../../../images/tutorials/create/azure-file-storage/catalog.png)

此時將顯示&#x200B;**[!UICONTROL 連接到Azure檔案儲存]**&#x200B;頁。 在此頁面上，您可以使用新憑證或現有憑證。

### 新帳戶

如果您正在使用新憑據，請選擇&#x200B;**[!UICONTROL 新帳戶]**。 在顯示的輸入表單中，提供名稱、可選說明和您的[!DNL Azure File Storage]憑證。 完成後，選擇&#x200B;**[!UICONTROL Connect]**，然後允許一些時間建立新連接。

![connect](../../../../images/tutorials/create/azure-file-storage/new.png)

### 現有帳戶

要連接現有帳戶，請選擇要連接的[!DNL Azure File Storage]帳戶，然後選擇&#x200B;**[!UICONTROL Next]**&#x200B;以繼續。

![現有](../../../../images/tutorials/create/azure-file-storage/existing.png)

## 後續步驟

依照本教學課程，您已建立與[!DNL Azure File Storage]帳戶的連線。 您現在可以繼續下一個教程，並[配置資料流，以將雲儲存中的資料帶入 [!DNL Platform]](../../dataflow/batch/cloud-storage.md)。
