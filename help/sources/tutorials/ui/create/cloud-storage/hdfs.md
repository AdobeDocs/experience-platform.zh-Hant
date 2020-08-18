---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 在UI中建立Apache HDFS來源連接器
topic: overview
translation-type: tm+mt
source-git-commit: dd036cf4df5d772206d2b73292c60f2d866ba0de
workflow-type: tm+mt
source-wordcount: '470'
ht-degree: 1%

---


# 在UI中 [!DNL Apache] 建立HDFS來源連接器

>[!NOTE]
>HDFS [!DNL Apache] 介面處於測試階段。 如需使用 [測試版標籤連接器的詳細資訊](../../../../home.md#terms-and-conditions) ，請參閱來源概觀。

中的來源連 [!DNL Adobe Experience Platform] 接器可讓您依計畫接收外部來源的資料。 本教學課程提供使用使 [!DNL Apache Hadoop Distributed File System] 用者介面驗證（下稱「HDFS」）來源連接器的 [!DNL Platform] 步驟。

## 快速入門

本教學課程需要有效瞭解下列元件 [!DNL Platform]:

- [[!DNL Experience Data Model] (XDM)系統](../../../../../xdm/home.md):組織客戶體驗資料 [!DNL Experience Platform] 的標準化架構。
   - [架構構成基礎](../../../../../xdm/schema/composition.md):瞭解XDM架構的基本建置區塊，包括架構組合的主要原則和最佳實務。
   - [架構編輯器教程](../../../../../xdm/tutorials/create-schema-ui.md):瞭解如何使用架構編輯器UI建立自訂架構。
- [[!DNL即時客戶基本資料]](../../../../../profile/home.md):根據來自多個來源的匯整資料，提供統一、即時的消費者個人檔案。

如果您已經有有效的HDFS連接，則可以跳過本文檔的其餘部分，並繼續有關配置資料 [流的教程](../../dataflow/batch/cloud-storage.md)。

### 收集必要的認證

為了驗證您的HDFS源連接器，您必須為以下連接屬性提供值：

| 憑證 | 說明 |
| ---------- | ----------- |
| `url` | URL會以匿名方式定義連線至HDFS所需的驗證參數。 有關如何獲取此值的詳細資訊，請參閱以下有關HDFS的 [HTTPS驗證的文檔](https://hadoop.apache.org/docs/r1.2.1/HttpAuthentication.html)。 |

## 連接您的HDFS帳戶

收集完所需憑證後，您可依照下列步驟將HDFS帳戶連結至 [!DNL Platform]。

登入 [Adobe Experience Platform](https://platform.adobe.com) ，然後從左側導覽列選取 **[!UICONTROL Sources]** ，以存取 **** Sources工作區。 「目 **[!UICONTROL 錄]** 」畫面會顯示多種來源，您可以用來建立帳戶。

您可以從畫面左側的目錄中選取適當的類別。 或者，您也可以使用搜尋選項找到您要使用的特定來源。

在「雲端 **[!UICONTROL 儲存空間]** 」類別下，選 **[!UICONTROL 取「Apache HDFS」]**。 如果這是您第一次使用此連接器，請選擇「配 **[!UICONTROL 置」]**。 否則，請選 **[!UICONTROL 擇「添加資料]** 」以建立新的HDFS連接器。

![目錄](../../../../images/tutorials/create/hdfs/catalog.png)

出現 **[!UICONTROL 「Connect to HDFS]** （連接到HDFS）」頁。 在此頁上，您可以使用新認證或現有認證。

### 新帳戶

如果您使用新認證，請選擇「新 **[!UICONTROL 帳戶」]**。 在顯示的輸入表單上，提供名稱、可選說明和您的HDFS認證。 完成後，選擇「 **[!UICONTROL 連接到源」]** ，然後為建立新連接留出一些時間。

![連接](../../../../images/tutorials/create/hdfs/new.png)

### 現有帳戶

要連接現有帳戶，請選擇要連接的HDFS帳戶，然後選擇「下 **[!UICONTROL 一步]** 」繼續。

![現有](../../../../images/tutorials/create/hdfs/existing.png)

## 後續步驟

按照本教程，您已建立與HDFS帳戶的連線。 您現在可以繼續下一個教學課程，並 [設定資料流，將雲端儲存空間的資料匯入 [!DNL Platform]](../../dataflow/batch/cloud-storage.md)。