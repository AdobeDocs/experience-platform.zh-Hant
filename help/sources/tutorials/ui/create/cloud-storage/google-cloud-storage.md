---
keywords: Experience Platform；首頁；熱門主題；Google雲端儲存空間；google雲端儲存空間；GCS;gcs
solution: Experience Platform
title: 在UI中建立Google雲端儲存來源連線
topic: 概述
type: 教學課程
description: 瞭解如何使用Adobe Experience PlatformUI建立Google雲端儲存空間來源連線。
translation-type: tm+mt
source-git-commit: f6a63ca1e21b3c3f6a55574f31fdf04038b7e5c4
workflow-type: tm+mt
source-wordcount: '577'
ht-degree: 1%

---


# 在UI中建立[!DNL Google Cloud Storage]源連接

Adobe Experience Platform的來源連接器提供按計畫接收外部來源資料的能力。 本教學課程提供使用[!DNL Platform]使用者介面建立[!DNL Google Cloud Storage]（以下稱為「GCS」）來源連接器的步驟。

## 快速入門

本教學課程需要對Adobe Experience Platform的下列部分有正確的理解：

* [[!DNL Experience Data Model (XDM)] 系統](../../../../../xdm/home.md):Experience Platform組織客戶體驗資料的標準化架構。
   * [架構構成基礎](../../../../../xdm/schema/composition.md):瞭解XDM架構的基本建置區塊，包括架構組合的主要原則和最佳實務。
   * [架構編輯器教程](../../../../../xdm/tutorials/create-schema-ui.md):瞭解如何使用架構編輯器UI建立自訂架構。
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md):根據來自多個來源的匯整資料，提供統一、即時的消費者個人檔案。

如果您已經有有效的GCS連接，則可以跳過本文檔的其餘部分，繼續[配置資料流](../../dataflow/batch/cloud-storage.md)的教程。

### 支援的檔案格式

[!DNL Experience Platform] 支援從外部儲存中提取的以下檔案格式：

* 分隔字元分隔值(DSV):目前，對DSV格式化資料檔案的支援僅限於逗號分隔值。 DSV格式檔案中欄位標題的值只能由字母數字字元和下划線組成。 將來將提供對一般DSV檔案的支援。
* JavaScript物件符號(JSON):JSON格式的資料檔案必須符合XDM規範。
* Apache Parce:拼花格式化的資料檔案必須與XDM相容。

### 收集必要的認證

若要存取[!DNL Platform]上的GCS資料，您必須提供下列值：

| 憑證 | 說明 |
| ---------- | ----------- |
| 存取金鑰ID | 用於向平台驗證[!DNL Google Cloud Storage]帳戶的61個字元英數字串。 |
| 機密存取金鑰 | 40個字元、基本64編碼的字串，用於向平台驗證您的[!DNL Google Cloud Storage]帳戶。 |

如需這些值的詳細資訊，請參閱[ Google Cloud Storage HMAC金鑰指南。 ](https://cloud.google.com/storage/docs/authentication/hmackeys#overview)有關如何生成自己的訪問密鑰ID和秘密訪問密鑰的步驟，請參閱[[!DNL Google Cloud Storage] overview](../../../../connectors/cloud-storage/google-cloud-storage.md)。

## 連接您的[!DNL Google Cloud Storage]帳戶

收集完所需憑證後，您可依照下列步驟將GCS帳戶連結至[!DNL Platform]。

登入[Adobe Experience Platform](https://platform.adobe.com)，然後從左側導覽列選擇&#x200B;**[!UICONTROL Sources]**&#x200B;以存取&#x200B;**[!UICONTROL Sources]**&#x200B;工作區。 **[!UICONTROL Catalog]**&#x200B;畫面會顯示各種來源，您可以用來建立帳戶。

您可以從畫面左側的目錄中選取適當的類別。 或者，您也可以使用搜尋選項找到您要使用的特定來源。

在&#x200B;**[!UICONTROL Databases]**&#x200B;類別下，選擇&#x200B;**[!UICONTROL Google Cloud Storage]**。 如果這是您第一次使用此連接器，請選擇&#x200B;**[!UICONTROL Configure]**。 否則，請選擇&#x200B;**[!UICONTROL Add data]**&#x200B;以建立新的GCS連接器。

![目錄](../../../../images/tutorials/create/google-cloud-storage/catalog.png)

此時將顯示&#x200B;**[!UICONTROL Connect to Google Cloud Storage]**&#x200B;頁。 在此頁上，您可以使用新認證或現有認證。

### 新帳戶

如果使用新憑據，請選擇&#x200B;**[!UICONTROL New account]**。 在出現的輸入表單上，提供名稱、選用說明和您的GCS認證。 完成後，選擇&#x200B;**[!UICONTROL Connect]** ，然後允許一些時間建立新連接。

![連接](../../../../images/tutorials/create/google-cloud-storage/connect.png)

### 現有帳戶

若要連線現有帳戶，請選取您要連線的GCS帳戶，然後選取&#x200B;**[!UICONTROL Next]**&#x200B;以繼續。

![現有](../../../../images/tutorials/create/google-cloud-storage/existing.png)

## 後續步驟

在本教學課程中，您已建立與GCS帳戶的連線。 您現在可以繼續下一個教學課程，並[設定資料流，將雲端儲存空間的資料匯入 [!DNL Platform]](../../dataflow/batch/cloud-storage.md)。