---
keywords: Experience Platform;home;popular topics;Azure Table Storage;azure table storage;ats;ATS
solution: Experience Platform
title: 在UI中建立Azure表格儲存來源連接器
topic: overview
type: Tutorial
description: 本教學課程提供使用平台使用者介面建立Azure表格儲存（以下稱為「ATS」）來源連接器的步驟。
translation-type: tm+mt
source-git-commit: 97dfd3a9a66fe2ae82cec8954066bdf3b6346830
workflow-type: tm+mt
source-wordcount: '494'
ht-degree: 1%

---


# 在UI中 [!DNL Azure Table Storage] 建立來源連接器

>[!NOTE]
>
>連接 [!DNL Azure Table Storage] 器為測試版。 如需使用 [測試版標籤連接器的詳細資訊](../../../../home.md#terms-and-conditions) ，請參閱來源概觀。

Adobe Experience Platform中的來源連接器可讓您依計畫吸收外部來源的資料。 本教學課程提供使用使 [!DNL Azure Table Storage] 用者介面建立（以下稱為「ATS」）來源連接器 [!DNL Platform] 的步驟。

## 快速入門

本教學課程需要對Adobe Experience Platform的下列元件有正確的認識：

* [[!DNL Experience Data Model] (XDM)系統](../../../../../xdm/home.md):組織客戶體驗資料 [!DNL Experience Platform] 的標準化架構。
   * [架構構成基礎](../../../../../xdm/schema/composition.md):瞭解XDM架構的基本建置區塊，包括架構組合的主要原則和最佳實務。
   * [架構編輯器教程](../../../../../xdm/tutorials/create-schema-ui.md):瞭解如何使用架構編輯器UI建立自訂架構。
* [[!DNL即時客戶基本資料]](../../../../../profile/home.md):根據來自多個來源的匯整資料，提供統一、即時的消費者個人檔案。

如果您已有有效的ATS連線，則可略過本檔案的其餘部分，並繼續有關設定資料 [流的教學課程](../../dataflow/databases.md)。

### 收集必要的認證

若要存取您的ATS帳戶 [!DNL Platform]，您必須提供下列值：

| 憑證 | 說明 |
| ---------- | ----------- |
| `connectionString` | 連接到實例的連接字串 [!DNL Azure Table Storage] 。 連線至ATS例項的連線字串。 ATS的連接字串模式是 `DefaultEndpointsProtocol=https;AccountName={ACCOUNT_NAME};AccountKey={ACCOUNT_KEY}`。 |

如需快速入門的詳細資訊，請參閱本 [ [!DNL Azure Table Storage] 檔案](https://docs.microsoft.com/en-us/azure/storage/common/storage-introduction)。

## 連線您的帳 [!DNL Azure Table Storage] 戶

收集完所需的認證後，您可依照下列步驟將ATS帳戶連結至 [!DNL Platform]。

登入 [Adobe Experience Platform](https://platform.adobe.com) ，然後從左側導覽列選取 **[!UICONTROL Sources]** ，以存取 **** Sources工作區。 「目 **[!UICONTROL 錄]** 」畫面會顯示多種來源，您可以用來建立帳戶。

您可以從畫面左側的目錄中選取適當的類別。 或者，您也可以使用搜尋選項找到您要使用的特定來源。

在「數 **[!UICONTROL 據庫]** 」類別下，選 **[!UICONTROL 擇Azure表儲存]**。 如果這是您第一次使用此連接器，請選擇「配 **[!UICONTROL 置」]**。 否則，請選 **[!UICONTROL 擇「新增資料]** 」以建立新的ATS連接器。

![目錄](../../../../images/tutorials/create/ats/catalog.png)

此時 **[!UICONTROL 將顯示「連接到Azure表儲存]** 」頁。 在此頁上，您可以使用新認證或現有認證。

### 新帳戶

如果您使用新認證，請選擇「新 **[!UICONTROL 帳戶」]**。 在出現的輸入表單上，提供名稱、選用說明和您的ATS認證。 完成後，選擇 **[!UICONTROL Connect]** ，然後為建立新連接留出一些時間。

![連接](../../../../images/tutorials/create/ats/new.png)

### 現有帳戶

若要連線現有帳戶，請選取您要連線的ATS帳戶，然後選取「下 **[!UICONTROL 一]** 步」繼續。

![現有](../../../../images/tutorials/create/ats/existing.png)

## 後續步驟

在本教學課程中，您已建立與ATS帳戶的連線。 您現在可以繼續下一個教程，並 [配置資料流以將資料導入 [!DNL Platform]](../../dataflow/databases.md)。