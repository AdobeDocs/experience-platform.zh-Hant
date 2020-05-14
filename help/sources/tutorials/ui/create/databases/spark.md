---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 在Azure HDInsights的UI中建立Apache Spark來源連接器
topic: overview
translation-type: tm+mt
source-git-commit: 2162c66b1664ecaaf0b609fe3f7ccf58c4a5d31d
workflow-type: tm+mt
source-wordcount: '534'
ht-degree: 0%

---


# 在Azure HDInsights的UI中建立Apache Spark來源連接器

> [!NOTE]
> Apache Spark on Azure HDInsights連接器為測試版。 功能和檔案可能會有所變更。

Adobe Experience Platform中的來源連接器可讓您依計畫吸收外部來源的資料。 本教學課程提供在Azure HDInsights來源連接器上使用平台使用者介面建立Apache Spark的步驟。

## 快速入門

本教學課程需要對Adobe Experience Platform的下列元件有正確的認識：

* [體驗資料模型(XDM)系統](../../../../../xdm/home.md): Experience Platform組織客戶體驗資料的標準化架構。
   * [架構構成基礎](../../../../../xdm/schema/composition.md): 瞭解XDM架構的基本建置區塊，包括架構組合的主要原則和最佳實務。
   * [架構編輯器教程](../../../../../xdm/tutorials/create-schema-ui.md): 瞭解如何使用架構編輯器UI建立自訂架構。
* [即時客戶個人檔案](../../../../../profile/home.md): 根據來自多個來源的匯整資料，提供統一、即時的消費者個人檔案。

如果您已有有效的Spark連線，則可略過本檔案的其餘部分，並繼續有關設定資料 [流的教學課程](../../dataflow/databases.md)

### 收集必要的認證

若要存取您的Spark帳戶，您必須提供下列值：

| 憑證 | 說明 |
| ---------- | ----------- |
| `host` | Spark伺服器的IP位址或主機名稱。 |
| `username` | 您用來存取Spark伺服器的使用者名稱。 |
| `password` | 與用戶對應的口令。 |

如需快速入門的詳細資訊，請參閱 [此Spark檔案](https://docs.microsoft.com/en-us/azure/hdinsight/spark/apache-spark-overview)。

## 連接您的Spark帳戶

收集完所需憑證後，您可依照下列步驟建立新的Spark帳戶以連線至平台。

登入 <a href="https://platform.adobe.com" target="_blank">Adobe Experience Platform</a> ，然後從左側導覽列選取 **Sources** ，以存取 ** Sources工作區。 「目 *錄* 」畫面會顯示多種來源，您可以為這些來源建立傳入帳戶，而每個來源會顯示與這些來源相關聯的現有帳戶和資料集流數。

您可以從畫面左側的目錄中選取適當的類別。 或者，您也可以使用搜尋選項找到您要使用的特定來源。

在「資 *料庫* 」類別下，選取 **Spark** ，以在螢幕右側顯示資訊列。 資訊列提供所選來源的簡短說明，以及與來源連線或檢視其檔案的選項。 要建立新入站連接，請選擇「連 **接源」**。

![目錄](../../../../images/tutorials/create/spark/catalog.png)

此時 *會顯示「連線至Spark* 」頁面。 在此頁上，您可以使用新認證或現有認證。

### 新帳戶

如果您使用新認證，請選擇「新 **帳戶」**。 在出現的輸入表單上，提供連線名稱、選用說明和您的Spark認證。 完成後，選擇 **Connect** ，然後為新帳戶建立留出一些時間。

![new](../../../../images/tutorials/create/spark/new.png)

### 現有帳戶

若要連線現有帳戶，請選取您要連線的Spark帳戶，然後選取「下 **一** 步」繼續。

![現有](../../../../images/tutorials/create/spark/existing.png)

## 後續步驟

在本教學課程中，您已建立與Spark帳戶的連線。 您現在可以繼續下一個教程，並 [配置資料流以將資料導入平台](../../dataflow/databases.md)。