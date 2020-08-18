---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 在UI中建立FTP或SFTP來源連接器
topic: overview
translation-type: tm+mt
source-git-commit: 9995a1d7daae3860783d2b4e4e0d2f1314eaa643
workflow-type: tm+mt
source-wordcount: '545'
ht-degree: 1%

---


# 在UI中建立FTP或SFTP來源連接器

>[!NOTE]
>FTP和SFTP連接器為測試版。 如需使用 [測試版標籤連接器的詳細資訊](../../../../home.md#terms-and-conditions) ，請參閱來源概觀。

Adobe Experience Platform中的來源連接器可讓您依計畫吸收外部來源的資料。 本教學課程提供使用使用者介面建立FTP或SFTP來源連接器 [!DNL Platform] 的步驟。

## 快速入門

本教學課程需要對Adobe Experience Platform的下列元件有正確的認識：

* [[!DNL Experience Data Model] (XDM)系統](../../../../../xdm/home.md):Experience Platform組織客戶體驗資料的標準化架構。
   * [架構構成基礎](../../../../../xdm/schema/composition.md):瞭解XDM架構的基本建置區塊，包括架構組合的主要原則和最佳實務。
   * [架構編輯器教程](../../../../../xdm/tutorials/create-schema-ui.md):瞭解如何使用架構編輯器UI建立自訂架構。
* [[!DNL即時客戶基本資料]](../../../../../profile/home.md):根據來自多個來源的匯整資料，提供統一、即時的消費者個人檔案。

如果您已經有有效的FTP或SFTP連線，則可略過本文檔的其餘部分，並繼續有關配置資料 [流的教程](../../dataflow/batch/cloud-storage.md)。

### 支援的檔案格式

[!DNL Experience Platform] 支援從外部來源擷取下列檔案格式：

* 分隔字元分隔值(DSV):目前，對DSV格式化資料檔案的支援僅限於逗號分隔值(CSV)。 DSV格式檔案中欄位標題的值只能由字母數字字元和下划線組成。 今後將提供對一般DSV的支援。
* JavaScript物件符號(JSON):JSON格式的資料檔案必須符合XDM規範。
* Apache Parce:拼花格式化的資料檔案必須與XDM相容。

### 收集必要的認證

若要在上存取您的FTP或SFTP伺服器 [!DNL Platform]，您必須提供伺服器的 **主機名**、使 **用者名**&#x200B;稱和密 **碼**。

## 連線至您的FTP或SFTP伺服器

收集完所需憑證後，您可依照下列步驟建立新的FTP或SFTP帳戶以連線至 [!DNL Platform]。

登入 [Adobe Experience Platform](https://platform.adobe.com) ，然後從左側導覽列選取 **[!UICONTROL Sources]** ，以存取 **** Sources工作區。 「目 **[!UICONTROL 錄]** 」畫面會顯示多種來源，您可為其建立傳入帳戶。

您可以從畫面左側的目錄中選取適當的類別。 或者，您也可以使用搜尋選項找到您要使用的特定來源。

在「數 **[!UICONTROL 據庫]** 」類別下，選 **[!UICONTROL 擇SFTP]**。 如果這是您第一次使用此連接器，請選擇「配 **[!UICONTROL 置」]**。 否則，請選 **[!UICONTROL 取「新增資料]** 」以建立新的FTP或SFTP連接器。

![目錄](../../../../images/tutorials/create/sftp/catalog.png)

此時 **[!UICONTROL 將顯示「連接到SFTP]** 」頁。 在此頁上，您可以使用新認證或現有認證。

### 新帳戶

如果您使用新認證，請選擇「新 **[!UICONTROL 帳戶」]**。 在出現的輸入表單上，提供名稱、選用說明以及您的FTP或SFTP憑證。 完成後，選擇 **[!UICONTROL Connect]** ，然後為建立新連接留出一些時間。

![連接](../../../../images/tutorials/create/sftp/new.png)

### 現有帳戶

若要連線現有帳戶，請選取您要連線的FTP或SFTP帳戶，然後選取「下 **[!UICONTROL 一]** 步」繼續。

![現有](../../../../images/tutorials/create/sftp/existing.png)

## 後續步驟

在本教學課程中，您已建立與FTP或SFTP帳戶的連線。 您現在可以繼續下一個教學課程，並 [設定資料流，將雲端儲存空間的資料匯入 [!DNL Platform]](../../dataflow/batch/cloud-storage.md)。