---
keywords: Experience Platform;home；熱門主題；Google Cloud Storage;google雲端儲存；GCS;gcs
solution: Experience Platform
title: 在UI中建立Google雲端儲存來源連線
topic: overview
type: Tutorial
description: 瞭解如何使用Adobe Experience Platform UI建立Google雲端儲存來源連線。
translation-type: tm+mt
source-git-commit: c7fb0d50761fa53c1fdf4dd70a63c62f2dcf6c85
workflow-type: tm+mt
source-wordcount: '561'
ht-degree: 1%

---


# 在UI中建立[!DNL Google Cloud Storage]源連接

Adobe Experience Platform中的來源連接器可讓您依計畫吸收外部來源的資料。 本教學課程提供使用[!DNL Platform]使用者介面建立[!DNL Google Cloud Storage]（以下稱為「GCS」）來源連接器的步驟。

## 快速入門

本教學課程需要對Adobe Experience Platform的下列元件有正確的認識：

* [[!DNL Experience Data Model (XDM)] 系統](../../../../../xdm/home.md):Experience Platform組織客戶體驗資料的標準化架構。
   * [架構構成基礎](../../../../../xdm/schema/composition.md):瞭解XDM架構的基本建置區塊，包括架構組合的主要原則和最佳實務。
   * [架構編輯器教程](../../../../../xdm/tutorials/create-schema-ui.md):瞭解如何使用架構編輯器UI建立自訂架構。
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md):根據來自多個來源的匯整資料，提供統一、即時的消費者個人檔案。

如果您已經有有效的GCS連接，則可跳過本文檔的其餘部分，繼續[配置資料流](../../dataflow/batch/cloud-storage.md)的教程。

### 支援的檔案格式

[!DNL Experience Platform] 支援從外部儲存中提取的以下檔案格式：

* 分隔字元分隔值(DSV):目前，對DSV格式化資料檔案的支援僅限於逗號分隔值。 DSV格式檔案中欄位標題的值只能由字母數字字元和下划線組成。 將來將提供對一般DSV檔案的支援。
* JavaScript物件符號(JSON):JSON格式的資料檔案必須符合XDM規範。
* Apache Parce:拼花格式化的資料檔案必須與XDM相容。

### 收集必要的認證

若要存取[!DNL Platform]上的GCS資料，您必須提供下列值：

| 憑證 | 說明 |
| ---------- | ----------- |
| 存取金鑰ID | [!DNL Google Cloud Storage]帳戶的存取金鑰ID。 |
| 機密存取金鑰 | [!DNL Google Cloud Storage]帳戶的客戶機密碼。 |

有關入門的詳細資訊，請參閱[!DNL Google Cloud Storage]的[伺服器到伺服器驗證指南](https://cloud.google.com/docs/authentication/production)。

## 連接您的[!DNL Google Cloud Storage]帳戶

收集完所需憑證後，您可依照下列步驟將GCS帳戶連結至[!DNL Platform]。

登入[Adobe Experience Platform](https://platform.adobe.com)，然後從左側導覽列選擇&#x200B;**[!UICONTROL Sources]**&#x200B;以存取&#x200B;**[!UICONTROL Sources]**&#x200B;工作區。 **[!UICONTROL Catalog]**&#x200B;畫面會顯示多種來源，您可以用來建立帳戶。

您可以從畫面左側的目錄中選取適當的類別。 或者，您也可以使用搜尋選項找到您要使用的特定來源。

在&#x200B;**[!UICONTROL Databases]**&#x200B;類別下，選擇&#x200B;**[!UICONTROL Google Cloud Storage]**。 如果這是您第一次使用此連接器，請選擇&#x200B;**[!UICONTROL Configure]**。 否則，請選擇&#x200B;**[!UICONTROL 添加資料]**&#x200B;以建立新的GCS連接器。

![目錄](../../../../images/tutorials/create/google-cloud-storage/catalog.png)

此時會顯示「連線至Google雲端儲存空間&#x200B;]**」頁面。**[!UICONTROL &#x200B;在此頁上，您可以使用新認證或現有認證。

### 新帳戶

如果您使用新憑據，請選擇&#x200B;**[!UICONTROL 新建帳戶]**。 在出現的輸入表單上，提供名稱、選用說明和您的GCS認證。 完成後，選擇&#x200B;**[!UICONTROL Connect]** ，然後為建立新連接留出一些時間。

![連接](../../../../images/tutorials/create/google-cloud-storage/connect.png)

### 現有帳戶

若要連接現有帳戶，請選擇您要連接的GCS帳戶，然後選擇&#x200B;**[!UICONTROL Next]**&#x200B;繼續。

![現有](../../../../images/tutorials/create/google-cloud-storage/existing.png)

## 後續步驟

在本教學課程中，您已建立與GCS帳戶的連線。 您現在可以繼續下一個教學課程，並[設定資料流，將雲端儲存空間的資料匯入 [!DNL Platform]](../../dataflow/batch/cloud-storage.md)。