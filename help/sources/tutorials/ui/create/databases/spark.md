---
keywords: Experience Platform；首頁；熱門主題；Azure HDInsights；Apache Spark
solution: Experience Platform
title: 在UI中的Azure HDInsights Source連線上建立Apache Spark
type: Tutorial
description: 瞭解如何使用Adobe Experience Platform UI在Azure HDInsights來源連線上建立Apache Spark。
exl-id: 30d0b740-cec4-486f-9c9b-1579fd04f28b
source-git-commit: e37c00863249e677f1645266859bf40fe6451827
workflow-type: tm+mt
source-wordcount: '489'
ht-degree: 1%

---

# 在UI中的[!DNL Azure HDInsights]來源連線上建立[!DNL Apache Spark]

>[!NOTE]
>
> [!DNL Azure HDInsights]聯結器上的[!DNL Apache Spark]為Beta版。 如需使用Beta標籤聯結器的詳細資訊，請參閱[來源概觀](../../../../home.md#terms-and-conditions)。

Adobe Experience Platform中的Source聯結器可讓您依排程擷取外部來源資料。 本教學課程提供使用[!DNL Platform]使用者介面在[!DNL Azure HDInsights]來源聯結器上建立[!DNL Apache Spark]的步驟。

## 快速入門

本教學課程需要您實際瞭解下列Adobe Experience Platform元件：

* [體驗資料模型(XDM)系統](../../../../../xdm/home.md)：Experience Platform用來組織客戶體驗資料的標準化架構。
   * [結構描述組合的基本概念](../../../../../xdm/schema/composition.md)：瞭解XDM結構描述的基本建置區塊，包括結構描述組合中的關鍵原則和最佳實務。
   * [結構描述編輯器教學課程](../../../../../xdm/tutorials/create-schema-ui.md)：瞭解如何使用結構描述編輯器使用者介面建立自訂結構描述。
* [即時客戶個人檔案](../../../../../profile/home.md)：根據來自多個來源的彙總資料，提供統一的即時客戶個人檔案。

如果您已經有有效的[!DNL Spark]連線，您可以略過本檔案的其餘部分，並繼續進行有關[設定資料流](../../dataflow/databases.md)的教學課程

### 收集必要的認證

若要在[!DNL Platform]上存取您的[!DNL Spark]帳戶，您必須提供下列值：

| 認證 | 說明 |
| ---------- | ----------- |
| `host` | [!DNL Spark]伺服器的IP位址或主機名稱。 |
| `username` | 您用來存取[!DNL Spark]伺服器的使用者名稱。 |
| `password` | 與使用者對應的密碼。 |

如需開始使用的詳細資訊，請參閱[此Spark檔案](https://docs.microsoft.com/en-us/azure/hdinsight/spark/apache-spark-overview)。

## 連線您的[!DNL Spark]帳戶

收集必要的認證後，您可以依照下列步驟連結[!DNL Spark]帳戶以連線至[!DNL Platform]。

登入[Adobe Experience Platform](https://platform.adobe.com)，然後從左側導覽列中選取&#x200B;**[!UICONTROL 來源]**&#x200B;以存取&#x200B;**[!UICONTROL 來源]**&#x200B;工作區。 **[!UICONTROL 目錄]**&#x200B;畫面會顯示您可以建立帳戶的各種來源。

您可以從熒幕左側的目錄中選取適當的類別。 或者，您可以使用搜尋選項來尋找您要使用的特定來源。

在&#x200B;**[!UICONTROL 資料庫]**&#x200B;類別下，選取&#x200B;**[!UICONTROL Spark]**。 如果這是您第一次使用此聯結器，請選取&#x200B;**[!UICONTROL 設定]**。 否則，請選取&#x200B;**[!UICONTROL 新增資料]**&#x200B;以建立新的[!DNL Spark]聯結器。

![目錄](../../../../images/tutorials/create/spark/catalog.png)

**[!UICONTROL 連線至Spark]**&#x200B;頁面隨即顯示。 您可以在此頁面使用新的證明資料或現有的證明資料。

### 新帳戶

如果您正在使用新認證，請選取&#x200B;**[!UICONTROL 新帳戶]**。 在出現的輸入表單上，提供名稱、選擇性說明和您的[!DNL Spark]認證。 完成時，請選取&#x200B;**[!UICONTROL 連線]**，然後等待一段時間以建立新連線。

![新](../../../../images/tutorials/create/spark/new.png)

### 現有帳戶

若要連線現有帳戶，請選取您要連線的[!DNL Spark]帳戶，然後選取[下一步]**[!UICONTROL 以繼續。]**

![現有](../../../../images/tutorials/create/spark/existing.png)

## 後續步驟

依照本教學課程中的指示，您已建立與[!DNL Spark]帳戶的連線。 您現在可以繼續進行下一個教學課程，並[設定資料流以將資料帶入 [!DNL Platform]](../../dataflow/databases.md)。
