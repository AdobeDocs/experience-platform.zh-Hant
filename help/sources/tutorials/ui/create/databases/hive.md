---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 在Azure HDInsights的UI中建立Apache Hive來源連接器
topic: overview
translation-type: tm+mt
source-git-commit: 2162c66b1664ecaaf0b609fe3f7ccf58c4a5d31d
workflow-type: tm+mt
source-wordcount: '534'
ht-degree: 0%

---


# 在Azure HDInsights的UI中建立Apache Hive來源連接器

> [!NOTE]
> Apache Hive on Azure HDInsights連接器為beta版。 功能和檔案可能會有所變更。

Adobe Experience Platform中的來源連接器可讓您依計畫吸收外部來源的資料。 本教學課程提供在Azure HDInsights來源連接器上使用平台使用者介面建立Apache Hive的步驟。

## 快速入門

本教學課程需要對Adobe Experience Platform的下列元件有正確的認識：

* [體驗資料模型(XDM)系統](../../../../../xdm/home.md): Experience Platform組織客戶體驗資料的標準化架構。
   * [架構構成基礎](../../../../../xdm/schema/composition.md): 瞭解XDM架構的基本建置區塊，包括架構組合的主要原則和最佳實務。
   * [架構編輯器教程](../../../../../xdm/tutorials/create-schema-ui.md): 瞭解如何使用架構編輯器UI建立自訂架構。
* [即時客戶個人檔案](../../../../../profile/home.md): 根據來自多個來源的匯整資料，提供統一、即時的消費者個人檔案。

如果您已經有有效的Hive連接，則可以跳過本文檔的其餘部分，並繼續有關配置資料 [流的教程](../../dataflow/databases.md)

### 收集必要的認證

要訪問平台上的Hive帳戶，必須提供以下值：

| 憑證 | 說明 |
| ---------- | ----------- |
| `host` | Hive伺服器的IP地址或主機名。 |
| `username` | 用於訪問Hive伺服器的用戶名。 |
| `password` | 與用戶對應的口令。 |

有關快速入門的詳細資訊，請參 [閱此Hive文檔](https://cwiki.apache.org/confluence/display/Hive/Tutorial#Tutorial-GettingStarted)。

## 連接您的Hive帳戶

收集完所需的憑證後，您可依照下列步驟建立新的Hive帳戶以連線至平台。

登入 <a href="https://platform.adobe.com" target="_blank">Adobe Experience Platform</a> ，然後從左側導覽列選取 **Sources** ，以存取 ** Sources工作區。 「目 *錄* 」畫面會顯示多種來源，您可以為這些來源建立傳入帳戶，而每個來源會顯示與這些來源相關聯的現有帳戶和資料集流數。

您可以從畫面左側的目錄中選取適當的類別。 或者，您也可以使用搜尋選項找到您要使用的特定來源。

在「數 *據庫* 」類別下，選擇 **Hive** ，以在螢幕右側顯示資訊欄。 資訊列提供所選來源的簡短說明，以及與來源連線或檢視其檔案的選項。 要建立新入站連接，請選擇「連 **接源」**。

![目錄](../../../../images/tutorials/create/hive/catalog.png)

此時 *將顯示「連接到蜂巢* 」頁。 在此頁上，您可以使用新認證或現有認證。

### 新帳戶

如果您使用新認證，請選擇「新 **帳戶」**。 在顯示的輸入表單上，提供名稱、可選說明和Hive認證的連線。 完成後，選擇 **Connect** ，然後為新帳戶建立留出一些時間。

![連接](../../../../images/tutorials/create/hive/new.png)

### 現有帳戶

要連接現有帳戶，請選擇要連接的Hive帳戶，然後選擇「下 **一步** 」繼續。

![現有](../../../../images/tutorials/create/hive/existing.png)

## 後續步驟

通過本教程，您已建立了與Hive帳戶的連接。 您現在可以繼續下一個教程，並 [配置資料流以將資料導入平台](../../dataflow/databases.md)。