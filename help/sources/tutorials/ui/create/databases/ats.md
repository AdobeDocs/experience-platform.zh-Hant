---
keywords: Experience Platform；首頁；熱門主題；Azure表儲存；Azure表儲存；ATS;ATS
solution: Experience Platform
title: 在UI中建立Azure表儲存源連接
topic-legacy: overview
type: Tutorial
description: 了解如何使用Adobe Experience Platform UI建立Azure表儲存源連接。
exl-id: 045cb954-e3e1-439d-a3cd-170d688dfbc8
source-git-commit: 7af79b9e0d6ed29b796ac7c98b4df1dda09f3513
workflow-type: tm+mt
source-wordcount: '480'
ht-degree: 1%

---

# 在UI中建立[!DNL Azure Table Storage]源連接

Adobe Experience Platform中的來源連接器可讓您依排程內嵌外部來源資料。 本教學課程提供使用[!DNL Platform]使用者介面建立[!DNL Azure Table Storage]（以下稱為「ATS」）來源連接器的步驟。

## 快速入門

本教學課程需要妥善了解下列Adobe Experience Platform元件：

* [[!DNL Experience Data Model (XDM)] 系統](../../../../../xdm/home.md):組織客戶體驗資 [!DNL Experience Platform] 料的標準化架構。
   * [結構構成基本概念](../../../../../xdm/schema/composition.md):了解XDM結構描述的基本建置組塊，包括結構描述的主要原則和最佳實務。
   * [結構編輯器教學課程](../../../../../xdm/tutorials/create-schema-ui.md):了解如何使用結構編輯器UI建立自訂結構。
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md):根據來自多個來源的匯總資料，提供統一的即時消費者設定檔。

如果您已有有效的ATS連接，則可以跳過本文檔的其餘部分，並繼續參閱有關[配置資料流](../../dataflow/databases.md)的教程。

### 收集所需憑據

若要在[!DNL Platform]上存取您的ATS帳戶，您必須提供下列值：

| 憑據 | 說明 |
| ---------- | ----------- |
| `connectionString` | 連接到[!DNL Azure Table Storage]實例的連接字串。 連線至ATS例項的連線字串。 ATS的連接字串模式為`DefaultEndpointsProtocol=https;AccountName={ACCOUNT_NAME};AccountKey={ACCOUNT_KEY}`。 |

有關入門的詳細資訊，請參閱[this [!DNL Azure Table Storage] document](https://docs.microsoft.com/en-us/azure/storage/common/storage-introduction)。

## 連接您的[!DNL Azure Table Storage]帳戶

收集完所需憑證後，您可以依照下列步驟，將ATS帳戶連結至[!DNL Platform]。

登入[Adobe Experience Platform](https://platform.adobe.com)，然後從左側導覽列選取&#x200B;**[!UICONTROL 來源]**&#x200B;以存取&#x200B;**[!UICONTROL 來源]**&#x200B;工作區。 **[!UICONTROL 目錄]**&#x200B;螢幕顯示了各種源，您可以用這些源建立帳戶。

您可以從畫面左側的目錄中選取適當的類別。 或者，您也可以使用搜尋選項找到您要使用的特定來源。

在&#x200B;**[!UICONTROL 資料庫]**&#x200B;類別下，選擇&#x200B;**[!UICONTROL Azure表儲存]**。 如果這是您第一次使用此連接器，請選擇&#x200B;**[!UICONTROL 配置]**。 否則，選擇&#x200B;**[!UICONTROL 添加資料]**&#x200B;以建立新的ATS連接器。

![目錄](../../../../images/tutorials/create/ats/catalog.png)

此時將顯示&#x200B;**[!UICONTROL 連接到Azure表儲存]**&#x200B;頁。 在此頁面上，您可以使用新憑證或現有憑證。

### 新帳戶

如果您正在使用新憑據，請選擇&#x200B;**[!UICONTROL 新帳戶]**。 在顯示的輸入表單中，提供名稱、選用說明和您的ATS憑證。 完成後，選擇&#x200B;**[!UICONTROL Connect]**，然後允許一些時間建立新連接。

![connect](../../../../images/tutorials/create/ats/new.png)

### 現有帳戶

若要連線現有帳戶，請選取您要連線的ATS帳戶，然後選取&#x200B;**[!UICONTROL Next]**&#x200B;以繼續。

![現有](../../../../images/tutorials/create/ats/existing.png)

## 後續步驟

依照本教學課程，您已建立與ATS帳戶的連線。 您現在可以繼續下一個教程，並[配置資料流以將資料帶入 [!DNL Platform]](../../dataflow/databases.md)。
