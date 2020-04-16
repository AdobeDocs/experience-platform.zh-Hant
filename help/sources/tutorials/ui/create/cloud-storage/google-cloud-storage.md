---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 在UI中建立Google Cloud儲存空間來源連接器
topic: overview
translation-type: tm+mt
source-git-commit: f09ff4d1b159a6989868c5cfc35b361cfb640a99

---


# 在UI中建立Google Cloud儲存空間來源連接器

Adobe Experience Platform中的來源連接器可讓您依計畫吸收外部來源的資料。 本教學課程提供使用平台使用者介面建立Google雲端儲存空間（以下稱為「GCS」）來源連接器的步驟。

## 快速入門

本教學課程需要對Adobe Experience Platform的下列元件有正確的認識：

* [體驗資料模型(XDM)系統](../../../../../xdm/home.md):Experience Platform組織客戶體驗資料的標準化架構。
   * [架構構成基礎](../../../../../xdm/schema/composition.md):瞭解XDM架構的基本建置區塊，包括架構組合的主要原則和最佳實務。
   * [架構編輯器教程](../../../../../xdm/tutorials/create-schema-ui.md):瞭解如何使用架構編輯器UI建立自訂架構。
* [即時客戶個人檔案](../../../../../profile/home.md):根據來自多個來源的匯整資料，提供統一、即時的消費者個人檔案。

如果您已有GCS基本連接，則可以跳過本文檔的其餘部分，並繼續有關配置資料流 [的教程](../../dataflow/cloud-storage.md)。

### 支援的檔案格式

Experience Platform支援下列從外部儲存擷取的檔案格式：

* 分隔字元分隔值(DSV):目前，對DSV格式化資料檔案的支援僅限於逗號分隔值。 DSV格式檔案中欄位標題的值只能由字母數字字元和下划線組成。 將來將提供對一般DSV檔案的支援。
* JavaScript物件符號(JSON):JSON格式的資料檔案必須符合XDM規範。
* Apache Parce:拼花格式化的資料檔案必須與XDM相容。

### 收集必要的認證

若要在平台上存取您的GCS資料，您必須提供有效的GCS **存取金鑰ID** 和 **密碼**。 您可以閱讀Google Cloud的伺服器對伺服器驗證指南，進 <a href="https://cloud.google.com/docs/authentication/production" target="_blank">一步瞭解如何取得這些值</a> 。

## 連接您的GCS帳戶

收集完所需憑證後，您可依照下列步驟建立新的入站基本連線，將GCS帳戶連結至平台。

登入 <a href="https://platform.adobe.com" target="_blank">Adobe Experience Platform</a> ，然後從左側導覽列選取 **Sources** ，以存取 ** Sources工作區。 「目 *錄* 」螢幕顯示各種源，您可以為其建立入站基本連接，而每個源顯示與其關聯的現有基本連接數。

在「 *雲端儲存* 」類別下，選取 **Google Cloud Storage** ，以在螢幕右側顯示資訊列。 資訊欄提供所選源的簡要說明，以及與源視圖連接或與源連接的選項。 要建立新的入站基本連接，請按一下「連 **接源」**。

![](../../../../images/tutorials/create/google-cloud-storage/sources-catalog.png)

此時 _會出現「連線至Google雲端儲存空間_ 」對話方塊。 在輸入表單中，提供基本連線名稱、選用說明和您的GCS認證。 完成後，按一下 **Connect** ，然後允許一段時間建立新的基本連接。

![](../../../../images/tutorials/create/google-cloud-storage/gcs-credentials.png)

建立基本連接後，您可以繼續下一節，並配置資料流以將資料導入平台。

## 後續步驟

在本教學課程中，您已建立GCS帳戶的基本連線。 您現在可以繼續下一個教程，並 [配置資料流以將資料導入平台](../../dataflow/cloud-storage.md)。