---
keywords: Experience Platform；首頁；熱門主題；Apache HDFS; HDFS; HDFS
solution: Experience Platform
title: 在UI中建立Apache HDFS源連接
type: Tutorial
description: 了解如何使用Adobe Experience Platform UI建立ApacheHadoop分佈式檔案系統源連接。
exl-id: 3b8bf210-13b6-44e6-9090-152998f67452
source-git-commit: ed92bdcd965dc13ab83649aad87eddf53f7afd60
workflow-type: tm+mt
source-wordcount: '492'
ht-degree: 1%

---

# 建立 [!DNL Apache] UI中的HDFS源連接

>[!NOTE]
>
>此 [!DNL Apache] HDFS連接器為測試版。 請參閱 [來源概觀](../../../../home.md#terms-and-conditions) 有關使用測試版標籤連接器的詳細資訊。

中的源連接器 [!DNL Adobe Experience Platform] 提供依排程擷取外部來源資料的功能。 本教學課程提供驗證 [!DNL Apache Hadoop Distributed File System] （以下簡稱HDFS）源連接器，使用 [!DNL Platform] 使用者介面。

## 快速入門

本教學課程需要妥善了解以下元件： [!DNL Platform]:

- [[!DNL Experience Data Model (XDM)] 系統](../../../../../xdm/home.md):標準化框架 [!DNL Experience Platform] 組織客戶體驗資料。
   - [結構構成基本概念](../../../../../xdm/schema/composition.md):了解XDM結構描述的基本建置組塊，包括結構描述的主要原則和最佳實務。
   - [結構編輯器教學課程](../../../../../xdm/tutorials/create-schema-ui.md):了解如何使用結構編輯器UI建立自訂結構。
- [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md):根據來自多個來源的匯總資料，提供統一的即時消費者設定檔。

如果您已經擁有有效的HDFS連接，則可以跳過本文檔的其餘部分，並繼續進行有關 [配置資料流](../../dataflow/batch/cloud-storage.md).

### 收集所需憑據

要驗證您的HDFS源連接器，必須為以下連接屬性提供值：

| 憑據 | 說明 |
| ---------- | ----------- |
| `url` | URL定義匿名連接到HDFS所需的身份驗證參數。 有關如何獲取此值的詳細資訊，請參閱以下文檔： [HDFS的HTTPS驗證](https://hadoop.apache.org/docs/r1.2.1/HttpAuthentication.html). |

## 連接您的HDFS帳戶

收集到所需的憑據後，您可以按照以下步驟將HDFS帳戶連結到 [!DNL Platform].

登入 [Adobe Experience Platform](https://platform.adobe.com) 然後選取 **[!UICONTROL 來源]** 從左側導覽列存取 **[!UICONTROL 來源]** 工作區。 此 **[!UICONTROL 目錄]** 畫面會顯示您可以為其建立帳戶的各種來源。

您可以從畫面左側的目錄中選取適當的類別。 或者，您也可以使用搜尋選項找到您要使用的特定來源。

在 **[!UICONTROL 雲端儲存空間]** 類別，選擇 **[!UICONTROL Apache HDFS]**. 如果這是您第一次使用此連接器，請選取 **[!UICONTROL 設定]**. 否則，請選取 **[!UICONTROL 新增資料]** 建立新的HDFS連接器。

![目錄](../../../../images/tutorials/create/hdfs/catalog.png)

此 **[!UICONTROL 連接到HDFS]** 頁。 在此頁面上，您可以使用新憑證或現有憑證。

### 新帳戶

如果使用新憑據，請選擇 **[!UICONTROL 新帳戶]**. 在顯示的輸入表單中，提供名稱、可選說明和您的HDFS憑據。 完成後，請選取 **[!UICONTROL 連接到源]** 然後讓新連接建立一段時間。

![connect](../../../../images/tutorials/create/hdfs/new.png)

### 現有帳戶

要連接現有帳戶，請選擇要連接的HDFS帳戶，然後選擇 **[!UICONTROL 下一個]** 繼續。

![現有](../../../../images/tutorials/create/hdfs/existing.png)

## 後續步驟

按照本教程，您已建立了與HDFS帳戶的連接。 您現在可以繼續下一個教學課程，以及 [配置資料流，將雲儲存中的資料帶入 [!DNL Platform]](../../dataflow/batch/cloud-storage.md).
