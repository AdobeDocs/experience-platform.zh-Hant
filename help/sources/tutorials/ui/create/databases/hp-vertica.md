---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 在UI中建立HP Vertica來源連接器
topic: overview
translation-type: tm+mt
source-git-commit: ec2d0a33e0ae92a3153b7bdcad29734e487a0439
workflow-type: tm+mt
source-wordcount: '478'
ht-degree: 1%

---


# 在UI中建 [!DNL Vertica] 立HP來源連接器

>[!NOTE]
> HP接 [!DNL Vertica] 口處於測試階段。 如需使用 [測試版標籤連接器的詳細資訊](../../../../home.md#terms-and-conditions) ，請參閱來源概觀。

Adobe Experience Platform中的來源連接器可讓您依計畫吸收外部來源的資料。 本教學課程提供使用使用者介 [!DNL Vertica] 面建立HP來源連 [!DNL Platform] 接器的步驟。

## 快速入門

本教學課程需要對Adobe Experience Platform的下列元件有正確的認識：

* [[!DNL Experience Data Model] (XDM)系統](../../../../../xdm/home.md):組織客戶體驗資料 [!DNL Experience Platform] 的標準化架構。
   * [架構構成基礎](../../../../../xdm/schema/composition.md):瞭解XDM架構的基本建置區塊，包括架構組合的主要原則和最佳實務。
   * [架構編輯器教程](../../../../../xdm/tutorials/create-schema-ui.md):瞭解如何使用架構編輯器UI建立自訂架構。
* [[!DNL 即時客戶基本資料]](../../../../../profile/home.md):根據來自多個來源的匯整資料，提供統一、即時的消費者個人檔案。

如果您已經有有效的HP連 [!DNL Vertica] 接，則可以跳過本文檔的其餘部分，並繼續有關配置資料 [流的教程](../../dataflow/databases.md)。

### 收集必要的認證

以下各節提供您必須知道的其他資訊，以便使用API成功連 [!DNL Vertica] 接至 [!DNL Flow Service] HP。

| 憑證 | 說明 |
| ---------- | ----------- |
| `connectionString` | 用於連接到HP實例的連接字串 [!DNL Vertica] 。 HP的連接字串模式 [!DNL Vertica] 是 `Server={SERVER};Port={PORT};Database={DATABASE};UID={USERNAME};PWD={PASSWORD}` |

有關快速入門的詳細資訊，請參 [閱 [!DNL Vertica] 此HP文檔](https://www.vertica.com/docs/9.2.x/HTML/Content/Authoring/ConnectingToVertica/ClientJDBC/CreatingAndConfiguringAConnection.htm)。

## 連接您的HP帳 [!DNL Vertica] 戶

收集完所需的憑證後，您可以依照下列步驟將HP帳戶連 [!DNL Vertica] 結至 [!DNL Platform]。

登入 [Adobe Experience Platform](https://platform.adobe.com) ，然後從左側導覽列選取 **[!UICONTROL Sources]** ，以存取 **** Sources工作區。 「目 **[!UICONTROL 錄]** 」畫面會顯示多種來源，您可以用來建立帳戶。

您可以從畫面左側的目錄中選取適當的類別。 或者，您也可以使用搜尋選項找到您要使用的特定來源。

在「數 **[!UICONTROL 據庫]** 」類別下，選 **[!UICONTROL 擇HP Vertica]**。 如果這是您第一次使用此連接器，請選擇「配 **[!UICONTROL 置」]**。 否則，請選 **[!UICONTROL 擇「添加資料]** 」以建立新的HP [!DNL Vertica] 連接器。

![目錄](../../../../images/tutorials/create/hp-vertica/catalog.png)

此時 **[!UICONTROL 將顯示「連接到HP Vertica]** 」頁。 在此頁上，您可以使用新認證或現有認證。

### 新帳戶

如果您使用新認證，請選擇「新 **[!UICONTROL 帳戶」]**。 在顯示的輸入表單上，提供名稱、可選說明和您的HP憑 [!DNL Vertica] 證。 完成後，選擇 **[!UICONTROL Connect]** ，然後為建立新連接留出一些時間。

![連接](../../../../images/tutorials/create/hp-vertica/new.png)

### 現有帳戶

若要連線現有帳戶，請選 [!DNL Vertica] 取您要連線的HP帳戶，然後選取右上角的 **[!UICONTROL Next]** （下一步）以繼續。

![現有](../../../../images/tutorials/create/hp-vertica/existing.png)

## 後續步驟

按照本教程，您已建立與HP帳戶的連 [!DNL Vertica] 接。 您現在可以繼續下一個教程，並 [配置資料流以將資料導入 [!DNL Platform]](../../dataflow/databases.md)。