---
keywords: Experience Platform；首頁；熱門主題；Azure Data Lake Storage Gen2;ADLS Gen2;adls gen2;adls連接器
solution: Experience Platform
title: 在UI中建立Azure資料湖儲存Gen2來源連線
topic-legacy: overview
type: Tutorial
description: 瞭解如何使用Adobe Experience PlatformUI建立Azure資料湖儲存Gen2來源連線。
exl-id: d81b7593-08a3-43f8-a8bc-f5547a6cd55a
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '463'
ht-degree: 1%

---

# 在UI中建立[!DNL Azure Data Lake Storage Gen2]來源連線

Adobe Experience Platform的來源連接器提供按計畫接收外部來源資料的能力。 本教學課程提供使用[!DNL Platform]使用者介面驗證[!DNL Azure Data Lake Storage Gen2]（下稱「[!DNL ADLS Gen2]」）來源連接器的步驟。

## 快速入門

本教學課程需要對Adobe Experience Platform的下列部分有正確的理解：

- [[!DNL Experience Data Model (XDM)] 系統](../../../../../xdm/home.md):組織客戶體驗資 [!DNL Experience Platform] 料的標準化架構。
   - [架構構成基礎](../../../../../xdm/schema/composition.md):瞭解XDM架構的基本建置區塊，包括架構組合的主要原則和最佳實務。
   - [架構編輯器教程](../../../../../xdm/tutorials/create-schema-ui.md):瞭解如何使用架構編輯器UI建立自訂架構。
- [[!DNL Real-time Customer Profile]](../../../../../profile/home.md):根據來自多個來源的匯整資料，提供統一、即時的消費者個人檔案。

如果您已經有有效的ADLS Gen2連接，則可跳過本文檔的其餘部分，繼續[配置資料流](../../dataflow/batch/cloud-storage.md)的教程。

### 收集必要的認證

要驗證[!DNL ADLS Gen2]源連接器，必須為以下連接屬性提供值：

| 憑證 | 說明 |
| ---------- | ----------- |
| `url` | [!DNL ADLS Gen2]的端點。 |
| `servicePrincipalId` | 應用程式的用戶端ID。 |
| `servicePrincipalKey` | 應用程式的金鑰。 |
| `tenant` | 包含您應用程式的租用戶資訊。 |

有關這些值的詳細資訊，請參閱[this [!DNL ADLS Gen2] document](https://docs.microsoft.com/en-us/azure/data-factory/connector-azure-data-lake-storage)。

## 連接您的[!DNL ADLS Gen2]帳戶

收集完所需憑證後，您可以按照以下步驟將[!DNL ADLS Gen2]帳戶連結到[!DNL Platform]。

登入[Adobe Experience Platform](https://platform.adobe.com)，然後從左側導覽列選擇&#x200B;**[!UICONTROL Sources]**&#x200B;以存取&#x200B;**[!UICONTROL Sources]**&#x200B;工作區。 **[!UICONTROL Catalog]**&#x200B;畫面會顯示各種來源，您可以用來建立帳戶。

您可以從畫面左側的目錄中選取適當的類別。 或者，您也可以使用搜尋選項找到您要使用的特定來源。

在&#x200B;**[!UICONTROL Databases]**&#x200B;類別下，選擇&#x200B;**[!UICONTROL Azure Data Lake Gen2]**。 如果這是您第一次使用此連接器，請選擇&#x200B;**[!UICONTROL Configure]**。 否則，請選擇&#x200B;**[!UICONTROL Add data]**&#x200B;以建立新的ADLS Gen2連接器。

![](../../../../images/tutorials/create/adls-gen2/catalog.png)

出現&#x200B;**[!UICONTROL Connect to Azure Data Lake Gen2]**&#x200B;對話框。 在此頁上，您可以使用新認證或現有認證。

### 新帳戶

如果使用新憑據，請選擇&#x200B;**[!UICONTROL New Account]**。 在顯示的輸入表單上，提供名稱、可選說明和您的[!DNL ADLS Gen2]憑證。 完成後，選擇&#x200B;**[!UICONTROL Connect]** ，然後允許一些時間建立新連接。

![](../../../../images/tutorials/create/adls-gen2/connect.png)

### 現有帳戶

要連接現有帳戶，請選擇要連接的[!DNL ADLS Gen2]帳戶，然後選擇&#x200B;**[!UICONTROL Next]**&#x200B;繼續。

![](../../../../images/tutorials/create/adls-gen2/existing.png)

## 後續步驟

在本教學課程之後，您已建立與[!DNL ADLS Gen2]帳戶的連線。 您現在可以繼續下一個教學課程，並[設定資料流，將雲端儲存空間的資料匯入 [!DNL Platform]](../../dataflow/batch/cloud-storage.md)。
