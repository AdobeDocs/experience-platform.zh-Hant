---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 在UI中建立IBM DB2源連接器
topic: overview
translation-type: tm+mt
source-git-commit: 5ad763d2167c68f3293a2813248efaee22230a52
workflow-type: tm+mt
source-wordcount: '535'
ht-degree: 0%

---



# 在UI中建立IBM DB2源連接器

> [!NOTE]
> IBM DB2連接器處於測試階段。 如需使用 [測試版標籤連接器的詳細資訊](../../../../home.md#terms-and-conditions) ，請參閱來源概觀。

Adobe Experience Platform中的來源連接器可讓您依計畫吸收外部來源的資料。 本教程提供使用平台用戶介面建立IBM DB2（以下稱為「DB2」）源連接器的步驟。

## 快速入門

本教學課程需要對Adobe Experience Platform的下列元件有正確的認識：

* [體驗資料模型(XDM)系統](../../../../../xdm/home.md): Experience Platform組織客戶體驗資料的標準化架構。
   * [架構構成基礎](../../../../../xdm/schema/composition.md): 瞭解XDM架構的基本建置區塊，包括架構組合的主要原則和最佳實務。
   * [架構編輯器教程](../../../../../xdm/tutorials/create-schema-ui.md): 瞭解如何使用架構編輯器UI建立自訂架構。
* [即時客戶個人檔案](../../../../../profile/home.md): 根據來自多個來源的匯整資料，提供統一、即時的消費者個人檔案。

如果您已經有有效的DB2連接，則可以跳過本文檔的其餘部分，並繼續有關配置資料 [流的教程](../../dataflow/databases.md)。

### 收集必要的認證

以下各節提供您需要知道的其他資訊，以便使用流服務API成功連接到DB2。

| 憑證 | 說明 |
| ---------- | ----------- |
| `server` | DB2伺服器的名稱。 您可以在伺服器名稱后面指定以冒號分隔的埠號。 例如： server:port. |
| `database` | DB2資料庫的名稱。 |
| `username` | 用於連接到DB2資料庫的用戶名。 |
| `password` | 您為使用者名稱指定之使用者帳戶的密碼。 |

有關入門的詳細資訊，請參 [閱此DB2文檔](https://www.ibm.com/support/knowledgecenter/SSFMBX/com.ibm.swg.im.dashdb.doc/connecting/connect_credentials.html)。

## 連接您的IBM DB2帳戶

收集到所需憑據後，您可以按照以下步驟建立新的DB2帳戶以連接到平台。

登入 [Adobe Experience Platform](https://platform.adobe.com) ，然後從左側導覽列選取 **[!UICONTROL Sources]** ，以存取 ** Sources工作區。 「目 *[!UICONTROL 錄]* 」畫面會顯示多種來源，您可以為其建立傳入帳戶，而每個來源會顯示與其關聯的現有帳戶和資料集流量。

您可以從畫面左側的目錄中選取適當的類別。 或者，您也可以使用搜尋選項找到您要使用的特定來源。

在「數 *[!UICONTROL 據庫]* 」類別下，選擇 **[!UICONTROL IBM DB2]** **，按一下+表徵圖(+)** ，以建立新的DB2連接器。

![目錄](../../../../images/tutorials/create/ibm-db2/catalog.png)

此時 *[!UICONTROL 將顯示「連接到IBM DB2]* 」頁。 在此頁上，您可以使用新認證或現有認證。

### 新帳戶

如果您使用新認證，請選擇「新 **[!UICONTROL 帳戶」]**。 在顯示的輸入表單上，提供連接名稱、可選說明和DB2憑據。 完成後，選擇 **[!UICONTROL Connect]** ，然後為新帳戶建立留出一些時間。

![連接](../../../../images/tutorials/create/ibm-db2/new.png)

### 現有帳戶

要連接現有帳戶，請選擇要連接的DB2帳戶，然後選擇「下 **[!UICONTROL 一步]** 」繼續。

![現有](../../../../images/tutorials/create/ibm-db2/existing.png)

## 後續步驟

通過本教程，您已建立了與DB2帳戶的連接。 您現在可以繼續下一個教程，並 [配置資料流以將資料導入平台](../../dataflow/databases.md)。