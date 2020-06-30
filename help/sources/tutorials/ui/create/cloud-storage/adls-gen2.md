---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 在UI中建立Azure資料湖儲存Gen2來源連接器
topic: overview
translation-type: tm+mt
source-git-commit: d3c725c4760acb3857a67d0d30b24732c963a030
workflow-type: tm+mt
source-wordcount: '491'
ht-degree: 1%

---


# 在UI中 [!DNL Azure Data Lake Storage Gen2] 建立來源連接器

Adobe Experience Platform中的來源連接器可讓您依計畫吸收外部來源的資料。 本教學課程提供使用使 [!DNL Azure Data Lake Storage Gen2] 用者介面驗證（以下稱為「ADLS Gen2」）來源連接器的 [!DNL Platform] 步驟。

## 快速入門

本教學課程需要對Adobe Experience Platform的下列元件有正確的認識：

- [體驗資料模型(XDM)系統](../../../../../xdm/home.md): 組織客戶體驗資料 [!DNL Experience Platform] 的標準化架構。
   - [架構構成基礎](../../../../../xdm/schema/composition.md): 瞭解XDM架構的基本建置區塊，包括架構組合的主要原則和最佳實務。
   - [架構編輯器教程](../../../../../xdm/tutorials/create-schema-ui.md): 瞭解如何使用架構編輯器UI建立自訂架構。
- [即時客戶個人檔案](../../../../../profile/home.md): 根據來自多個來源的匯整資料，提供統一、即時的消費者個人檔案。

如果您已有ADLS Gen2基本連接，則可以跳過本文檔的其餘部分，並繼續有關配置資料流 [的教程](../../dataflow/batch/cloud-storage.md)。

### 收集必要的認證

為驗證您的ADLS Gen2來源連接器，您必須提供下列連線屬性的值：

| 憑證 | 說明 |
| ---------- | ----------- |
| `url` | ADLS Gen2的端點。 |
| `servicePrincipalId` | 應用程式的用戶端ID。 |
| `servicePrincipalKey` | 應用程式的金鑰。 |
| `tenant` | 包含您應用程式的租用戶資訊。 |

如需這些值的詳細資訊，請參 [閱本ADLS Gen2檔案](https://docs.microsoft.com/en-us/azure/data-factory/connector-azure-data-lake-storage)。

## 連接您的ADLS Gen2帳戶

收集完所需憑證後，您可以遵循下列步驟建立新的傳入基本連線，將ADLS Gen2帳戶連結至 [!DNL Platform]。

登入 <a href="https://platform.adobe.com" target="_blank">Adobe [!DNL Experience Platform]</a> ，然後從左側導覽列選取 **[!UICONTROL Sources]** ，以存取 *[!UICONTROL Sources]* 工作區。 「目 *[!UICONTROL 錄]* 」頁籤顯示了用於建立入站基本連接的各種源。 每個源顯示與其關聯的現有基本連接數。

在「 *[!UICONTROL 雲端儲存]* 」類別下，選取 **[!UICONTROL Azure Data Lake Gen2]** ，在螢幕右側顯示資訊列。 資訊列提供所選來源的簡短說明，以及與來源檢視其說明檔案連線的選項。 要建立新的入站基本連接，請按一下「連 **[!UICONTROL 接源」]**。

![](../../../../images/tutorials/create/adls-gen2/catalog.png)

此時 *[!UICONTROL 將顯示「連接到Azure資料湖Gen2]* 」對話框。 在此頁上，您可以使用新認證或現有認證。

### 新帳戶

如果您使用新認證，請選擇「新 **[!UICONTROL 帳戶」]**。 在顯示的輸入表單上，提供基本連線名稱、可選說明和您的ADLS Gen2憑證。 完成後，選擇 **[!UICONTROL Connect]** ，然後為建立新的基本連接留出一些時間。

![](../../../../images/tutorials/create/adls-gen2/connect.png)

### 現有帳戶

若要連線現有帳戶，請選取您要連線的ADLS Gen2帳戶，然後選取「下 **[!UICONTROL 一]** 步」繼續。

![](../../../../images/tutorials/create/adls-gen2/existing.png)

## 後續步驟

在本教學課程中，您已建立與ADLS Gen2帳戶的基本連線。 您現在可以繼續下一個教學課程，並 [設定資料流，將雲端儲存空間的資料匯入平台](../../dataflow/batch/cloud-storage.md)。