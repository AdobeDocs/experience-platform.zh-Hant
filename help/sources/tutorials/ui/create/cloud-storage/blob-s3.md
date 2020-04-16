---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 在UI中建立Azure Blob或Amazon S3來源連接器
topic: overview
translation-type: tm+mt
source-git-commit: f09ff4d1b159a6989868c5cfc35b361cfb640a99

---


# 在UI中建立Azure Blob或Amazon S3來源連接器

Adobe Experience Platform中的來源連接器可讓您依計畫吸收外部來源的資料。 本教學課程提供使用平台使用者介面建立Azure Blob（以下稱為「Blob」）或Amazon S3（以下稱為「S3」）來源連接器的步驟。

## 快速入門

本教學課程需要對Adobe Experience Platform的下列元件有正確的認識：

* [體驗資料模型(XDM)系統](../../../../../xdm/home.md):Experience Platform組織客戶體驗資料的標準化架構。
   * [架構構成基礎](../../../../../xdm/schema/composition.md):瞭解XDM架構的基本建置區塊，包括架構組合的主要原則和最佳實務。
   * [架構編輯器教程](../../../../../xdm/tutorials/create-schema-ui.md):瞭解如何使用架構編輯器UI建立自訂架構。
* [即時客戶個人檔案](../../../../../profile/home.md):根據來自多個來源的匯整資料，提供統一、即時的消費者個人檔案。

如果您已經有Blob或S3基本連接，則可以跳過本文檔的其餘部分，並繼續有關配置資料流 [的教程](../../dataflow/cloud-storage.md)。

### 支援的檔案格式

Experience Platform支援下列從外部儲存擷取的檔案格式：

* 分隔字元分隔值(DSV):目前，對DSV格式化資料檔案的支援僅限於逗號分隔值。 DSV格式檔案中欄位標題的值只能由字母數字字元和下划線組成。 將來將提供對一般DSV檔案的支援。
* JavaScript物件符號(JSON):JSON格式的資料檔案必須符合XDM規範。
* Apache Parce:拼花格式化的資料檔案必須與XDM相容。

### 收集必要的認證

要訪問平台上的Blob儲存，必須提供有效的 **Azure儲存連接字串**。 您可以進一步瞭解連線字串，包括透過此Microsoft Azure檔案取得 <a href="https://docs.microsoft.com/en-us/azure/storage/common/storage-configure-connection-string" target="_blank">連線字串的方式</a>。

同樣地，在Platform上存取您的S3儲存貯體也需要您提供 **S3存取金鑰****和S3密鑰**。 有關詳細資訊，請參 <a href="https://aws.amazon.com/blogs/security/wheres-my-secret-access-key/" target="_blank">閱本AWS文檔</a>。

## 連接您的Blob或S3帳戶

在雲端儲存空間的認證就緒後，您可以依照下列步驟建立新的傳入基本連線，將您的Blob或S3帳戶連結至平台。

登入 <a href="https://platform.adobe.com" target="_blank">Adobe Experience Platform</a> ，然後從左側導覽列選 **取Sources** ，以存取來源工作區。 「目 *錄* 」螢幕顯示各種源，您可以為其建立入站基本連接，而每個源顯示與其關聯的現有基本連接數。

在「 *雲端儲存* 」類別下，選取「 **Azure Blob Storage** 」或「 **Amazon S3** 」，以在畫面右側顯示資訊列。 資訊列提供所選來源的簡短說明，以及檢視其檔案或連線來源的選項。 要建立新的入站基本連接，請按一下「連 **接源」**。

![](../../../../images/tutorials/create/s3/s3_sources_catalog.png)

在輸入表單中，為基本連接提供名稱、可選說明和Blob或S3憑據。 最後，按一下 **Connect** ，然後允許一些時間建立新的基本連接。

![](../../../../images/tutorials/create/s3/s3_credentials.png)

## 後續步驟

通過本教程，您已建立了與Azure Blob或Amazon S3帳戶的基本連接。 您現在可以繼續下一個教程，並 [配置資料流以將資料導入平台](../../dataflow/cloud-storage.md)。