---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 在UI中建立MariaDB來源連接器
topic: overview
translation-type: tm+mt
source-git-commit: d3c725c4760acb3857a67d0d30b24732c963a030
workflow-type: tm+mt
source-wordcount: '473'
ht-degree: 1%

---


# 在UI中 [!DNL MariaDB] 建立來源連接器

> [!NOTE]
> 連接 [!DNL MariaDB] 器為測試版。 如需使用 [測試版標籤連接器的詳細資訊](../../../../home.md#terms-and-conditions) ，請參閱來源概觀。

Adobe Experience Platform中的來源連接器可讓您依計畫吸收外部來源的資料。 本教程提供使用用戶介面建立Maria DB源連接器 [!DNL Platform] 的步驟。

## 快速入門

本教學課程需要對Adobe Experience Platform的下列元件有正確的認識：

* [體驗資料模型(XDM)系統](../../../../../xdm/home.md): 組織客戶體驗資料 [!DNL Experience Platform] 的標準化架構。
   * [架構構成基礎](../../../../../xdm/schema/composition.md): 瞭解XDM架構的基本建置區塊，包括架構組合的主要原則和最佳實務。
   * [架構編輯器教程](../../../../../xdm/tutorials/create-schema-ui.md): 瞭解如何使用架構編輯器UI建立自訂架構。
* [即時客戶個人檔案](../../../../../profile/home.md): 根據來自多個來源的匯整資料，提供統一、即時的消費者個人檔案。

如果您已有Maria DB基本連接，則可以跳過本文檔的其餘部分，並繼續有關配置資料流 [的教程](../../dataflow/databases.md)。

### 收集必要的認證

若要存取您的帳 [!DNL Maria DB] 戶， [!DNL Platform]您必須提供下列值：

| 憑證 | 說明 |
| ---------- | ----------- |
| `connectionString` | 與您的MariaDB驗證相關聯的連接字串。 MariaDB連接字串模式是： `Server={HOST};Port={PORT};Database={DATABASE};UID={USERNAME};PWD={PASSWORD}`. |

有關開始使 [用MariaDB的詳細資訊](https://mariadb.com/kb/en/about-mariadb-connector-odbc/) ，請參閱本檔案。

## 連線您的帳 [!DNL Maria DB] 戶

收集完所需憑證後，您可依照下列步驟建立新的入站基本連線，將帳戶連結 [!DNL Maria DB] 至 [!DNL Platform]。

登入 <a href="https://platform.adobe.com" target="_blank">Adobe Experience Platform</a> ，然後從左側導覽列選取 **[!UICONTROL Sources]** ，以存取 ** Sources工作區。 「目 *[!UICONTROL 錄]* 」螢幕顯示各種源，您可以為其建立入站基本連接，而每個源顯示與其關聯的現有基本連接數。

在「數 *[!UICONTROL 據庫]* 」類別下，選擇 **[!UICONTROL Maria DB]** ，以在螢幕右側顯示資訊欄。 資訊列提供所選來源的簡短說明，以及與來源連線或檢視其檔案的選項。 要建立新的入站基本連接，請選擇「 **[!UICONTROL 連接源」]**。

![](../../../../images/tutorials/create/maria-db/catalog.png)

此時 *[!UICONTROL 將顯示「連接到Maria DB]* 」頁。 在此頁上，您可以使用新認證或現有認證。

### 新帳戶

如果您使用新認證，請選擇「新 **[!UICONTROL 帳戶」]**。 在出現的輸入表單上，提供基本連線名稱、選用說明和您的認 [!DNL Maria DB] 證。 完成後，選擇 **[!UICONTROL Connect]** ，然後為建立新的基本連接留出一些時間。

![](../../../../images/tutorials/create/maria-db/new.png)

### 現有帳戶

若要連線現有帳戶，請選 [!DNL Maria DB] 取您要連線的帳戶，然後選取「下 **[!UICONTROL 一]** 步」繼續。

![](../../../../images/tutorials/create/maria-db/existing.png)

## 後續步驟

在本教學課程中，您已建立了與帳戶的基本連 [!DNL Maria DB] 接。 您現在可以繼續下一個教程，並 [配置資料流以將資料導入平台](../../dataflow/databases.md)。