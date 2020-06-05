---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 在UI中建立Google Cloud儲存空間來源連接器
topic: overview
translation-type: tm+mt
source-git-commit: 75ba0bce7ce070af851bbf7e220dbf08febc4c20
workflow-type: tm+mt
source-wordcount: '553'
ht-degree: 1%

---


# 在UI中建立Google Cloud儲存空間來源連接器

Adobe Experience Platform中的來源連接器可讓您依計畫吸收外部來源的資料。 本教學課程提供使用平台使用者介面建立Google雲端儲存空間（以下稱為「GCS」）來源連接器的步驟。

## 快速入門

本教學課程需要對Adobe Experience Platform的下列元件有正確的認識：

* [體驗資料模型(XDM)系統](../../../../../xdm/home.md): Experience Platform組織客戶體驗資料的標準化架構。
   * [架構構成基礎](../../../../../xdm/schema/composition.md): 瞭解XDM架構的基本建置區塊，包括架構組合的主要原則和最佳實務。
   * [架構編輯器教程](../../../../../xdm/tutorials/create-schema-ui.md): 瞭解如何使用架構編輯器UI建立自訂架構。
* [即時客戶個人檔案](../../../../../profile/home.md): 根據來自多個來源的匯整資料，提供統一、即時的消費者個人檔案。

如果您已有GCS基本連接，則可以跳過本文檔的其餘部分，並繼續有關配置資料流 [的教程](../../dataflow/batch/cloud-storage.md)。

### 支援的檔案格式

Experience Platform支援下列從外部儲存擷取的檔案格式：

* 分隔字元分隔值(DSV): 目前，對DSV格式化資料檔案的支援僅限於逗號分隔值。 DSV格式檔案中欄位標題的值只能由字母數字字元和下划線組成。 將來將提供對一般DSV檔案的支援。
* JavaScript物件符號(JSON): JSON格式的資料檔案必須符合XDM規範。
* Apache Parce: 拼花格式化的資料檔案必須與XDM相容。

### 收集必要的認證

若要在平台上存取您的GCS資料，您必須提供有效的GCS **存取金鑰ID** 和 **密碼**。 您可以閱讀Google Cloud的伺服器對伺服器驗證指南，進 <a href="https://cloud.google.com/docs/authentication/production" target="_blank">一步瞭解如何取得這些值</a> 。

## 連接您的GCS帳戶

收集完所需的認證後，您可依照下列步驟建立新的GCS帳戶以連線至平台。

登入 [Adobe Experience Platform](https://platform.adobe.com) ，然後從左側導覽列選取 **[!UICONTROL Sources]** ，以存取 ** Sources工作區。 「目 *[!UICONTROL 錄]* 」螢幕顯示各種源，您可以為其建立入站帳戶，每個源顯示與其關聯的現有帳戶和資料流的數量。

您可以從畫面左側的目錄中選取適當的類別。 或者，您也可以使用搜尋選項找到您要使用的特定來源。

在「資 *[!UICONTROL 料庫]* 」類別下，選取「 **[!UICONTROL Google Cloud Storage]** 」(Google Cloud **儲存)，按一下+圖示(+)** ，以建立新的GCS連接器。

![目錄](../../../../images/tutorials/create/google-cloud-storage/catalog.png)

此時 *[!UICONTROL 會顯示「連線至Google雲端儲存空間]* 」頁面。 在此頁上，您可以使用新認證或現有認證。

### 新帳戶

如果您使用新認證，請選擇「新 **[!UICONTROL 帳戶」]**。 在出現的輸入表單上，提供名稱、選用說明和您的GCS認證連線。 完成後，選擇 **[!UICONTROL Connect]** ，然後為新帳戶建立留出一些時間。

![連接](../../../../images/tutorials/create/google-cloud-storage/connect.png)

### 現有帳戶

若要連線現有帳戶，請選取您要連線的GCS帳戶，然後選取「下 **[!UICONTROL 一步]** 」繼續。

![現有](../../../../images/tutorials/create/google-cloud-storage/existing.png)

## 後續步驟

在本教學課程中，您已建立與GCS帳戶的連線。 您現在可以繼續下一個教學課程，並 [設定資料流，將雲端儲存空間的資料匯入平台](../../dataflow/batch/cloud-storage.md)。