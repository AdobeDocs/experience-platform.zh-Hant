---
keywords: Experience Platform;home；熱門主題；Apache HDFS;HDFS;hdfs
solution: Experience Platform
title: 在UI中建立Apache HDFS來源連線
topic-legacy: overview
type: Tutorial
description: 瞭解如何使用Adobe Experience PlatformUI建立ApacheHadoop分佈式檔案系統源連接。
exl-id: 3b8bf210-13b6-44e6-9090-152998f67452
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '473'
ht-degree: 1%

---

# 在UI中建立[!DNL Apache] HDFS來源連線

>[!NOTE]
>
>[!DNL Apache] HDFS介面處於測試狀態。 有關使用beta標籤連接器的詳細資訊，請參閱[ Sources綜覽](../../../../home.md#terms-and-conditions)。

[!DNL Adobe Experience Platform]中的源連接器提供按計畫接收外部源資料的能力。 本教學課程提供使用[!DNL Platform]使用者介面驗證[!DNL Apache Hadoop Distributed File System]（以下稱為「HDFS」）來源連接器的步驟。

## 快速入門

本教學課程需要對[!DNL Platform]的下列元件有正確的理解：

- [[!DNL Experience Data Model (XDM)] 系統](../../../../../xdm/home.md):組織客戶體驗資 [!DNL Experience Platform] 料的標準化架構。
   - [架構構成基礎](../../../../../xdm/schema/composition.md):瞭解XDM架構的基本建置區塊，包括架構組合的主要原則和最佳實務。
   - [架構編輯器教程](../../../../../xdm/tutorials/create-schema-ui.md):瞭解如何使用架構編輯器UI建立自訂架構。
- [[!DNL Real-time Customer Profile]](../../../../../profile/home.md):根據來自多個來源的匯整資料，提供統一、即時的消費者個人檔案。

如果您已經有有效的HDFS連接，則可以跳過本文檔的其餘部分，繼續[配置資料流](../../dataflow/batch/cloud-storage.md)的教程。

### 收集必要的認證

為了驗證您的HDFS源連接器，您必須為以下連接屬性提供值：

| 憑證 | 說明 |
| ---------- | ----------- |
| `url` | URL會以匿名方式定義連線至HDFS所需的驗證參數。 有關如何獲取此值的詳細資訊，請參閱以下有關HDFS](https://hadoop.apache.org/docs/r1.2.1/HttpAuthentication.html)的[HTTPS驗證的文檔。 |

## 連接您的HDFS帳戶

收集完所需憑證後，您可依照下列步驟將HDFS帳戶連結至[!DNL Platform]。

登入[Adobe Experience Platform](https://platform.adobe.com)，然後從左側導覽列選擇&#x200B;**[!UICONTROL Sources]**&#x200B;以存取&#x200B;**[!UICONTROL Sources]**&#x200B;工作區。 **[!UICONTROL Catalog]**&#x200B;畫面會顯示各種來源，您可以用來建立帳戶。

您可以從畫面左側的目錄中選取適當的類別。 或者，您也可以使用搜尋選項找到您要使用的特定來源。

在&#x200B;**[!UICONTROL Cloud storage]**&#x200B;類別下，選擇&#x200B;**[!UICONTROL Apache HDFS]**。 如果這是您第一次使用此連接器，請選擇&#x200B;**[!UICONTROL Configure]**。 否則，請選擇&#x200B;**[!UICONTROL Add data]**&#x200B;以建立新的HDFS連接器。

![目錄](../../../../images/tutorials/create/hdfs/catalog.png)

此時將顯示&#x200B;**[!UICONTROL Connect to HDFS]**&#x200B;頁。 在此頁上，您可以使用新認證或現有認證。

### 新帳戶

如果使用新憑據，請選擇&#x200B;**[!UICONTROL New account]**。 在顯示的輸入表單上，提供名稱、可選說明和您的HDFS認證。 完成後，選擇&#x200B;**[!UICONTROL Connect to source]** ，然後允許一些時間建立新連接。

![連接](../../../../images/tutorials/create/hdfs/new.png)

### 現有帳戶

要連接現有帳戶，請選擇要連接的HDFS帳戶，然後選擇&#x200B;**[!UICONTROL Next]**&#x200B;繼續。

![現有](../../../../images/tutorials/create/hdfs/existing.png)

## 後續步驟

按照本教程，您已建立與HDFS帳戶的連線。 您現在可以繼續下一個教學課程，並[設定資料流，將雲端儲存空間的資料匯入 [!DNL Platform]](../../dataflow/batch/cloud-storage.md)。
