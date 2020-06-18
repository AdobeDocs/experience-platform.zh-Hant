---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 在UI中建立HP Vertica來源連接器
topic: overview
translation-type: tm+mt
source-git-commit: 5ad763d2167c68f3293a2813248efaee22230a52
workflow-type: tm+mt
source-wordcount: '512'
ht-degree: 0%

---


# 在UI中建立HP Vertica來源連接器

> [!NOTE]
> HP Vertica連接器正在測試中。 如需使用 [測試版標籤連接器的詳細資訊](../../../../home.md#terms-and-conditions) ，請參閱來源概觀。

Adobe Experience Platform中的來源連接器可讓您依計畫吸收外部來源的資料。 本教學課程提供使用Platform使用者介面建立HP Vertica來源連接器的步驟。

## 快速入門

本教學課程需要對Adobe Experience Platform的下列元件有正確的認識：

* [體驗資料模型(XDM)系統](../../../../../xdm/home.md): Experience Platform組織客戶體驗資料的標準化架構。
   * [架構構成基礎](../../../../../xdm/schema/composition.md): 瞭解XDM架構的基本建置區塊，包括架構組合的主要原則和最佳實務。
   * [架構編輯器教程](../../../../../xdm/tutorials/create-schema-ui.md): 瞭解如何使用架構編輯器UI建立自訂架構。
* [即時客戶個人檔案](../../../../../profile/home.md): 根據來自多個來源的匯整資料，提供統一、即時的消費者個人檔案。

如果您已經有有效的HP Vertica連接，則可以跳過本文檔的其餘部分，並繼續有關配置資料流 [的教程](../../dataflow/databases.md)。

### 收集必要的認證

以下各節提供您需要瞭解的其他資訊，以便使用Flow Service API成功連線至HP Vertica。

| 憑證 | 說明 |
| ---------- | ----------- |
| `connectionString` | 用於連接到HP Vertica實例的連接字串。 HP Vertica的連接字串模式是 `Server={SERVER};Port={PORT};Database={DATABASE};UID={USERNAME};PWD={PASSWORD}` |

有關快速入門的詳細資訊，請參 [閱此HP Vertica檔案](https://www.vertica.com/docs/9.2.x/HTML/Content/Authoring/ConnectingToVertica/ClientJDBC/CreatingAndConfiguringAConnection.htm)。

## 連接您的HP Vertica帳戶

收集完所需憑證後，您可依照下列步驟建立新的HP Vertica帳戶以連線至平台。

登入 [Adobe Experience Platform](https://platform.adobe.com) ，然後從左側導覽列選取 **[!UICONTROL Sources]** ，以存取 ** Sources工作區。 「目 *[!UICONTROL 錄]* 」畫面會顯示多種來源，您可以為其建立傳入帳戶，而每個來源會顯示與其關聯的現有帳戶和資料集流量。

您可以從畫面左側的目錄中選取適當的類別。 或者，您也可以使用搜尋選項找到您要使用的特定來源。

在「資 *[!UICONTROL 料庫]* 」類別下，選取 **[!UICONTROL HP Vertica]** ，按一 **下+圖示(+)** ，以建立新的HP Vertica連接器。

![目錄](../../../../images/tutorials/create/hp-vertica/catalog.png)

此時 *[!UICONTROL 將顯示「連接到HP Vertica]* 」頁。 在此頁上，您可以使用新認證或現有認證。

### 新帳戶

如果您使用新認證，請選擇「新 **[!UICONTROL 帳戶」]**。 在顯示的輸入表單上，提供連線名稱、選用說明和您的HP Vertica認證。 完成後，選擇 **[!UICONTROL Connect]** ，然後為新帳戶建立留出一些時間。

![連接](../../../../images/tutorials/create/hp-vertica/new.png)

### 現有帳戶

若要連線現有帳戶，請選取您要連線的HP Vertica帳戶，然後在右上角選取 **[!UICONTROL Next]** （下一步）以繼續。

![現有](../../../../images/tutorials/create/hp-vertica/existing.png)

## 後續步驟

在本教學課程中，您已建立與HP Vertica帳戶的連線。 您現在可以繼續下一個教程，並 [配置資料流以將資料導入平台](../../dataflow/databases.md)。