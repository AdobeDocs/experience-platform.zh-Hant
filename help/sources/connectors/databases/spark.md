---
keywords: Experience Platform；首頁；熱門主題；Apache Spark;Apache spark;Azure HDInsights;Azure Hindsights
solution: Experience Platform
title: Azure HDInsights Source Connector概述
topic-legacy: overview
description: 了解如何使用API或使用者介面，將Azure HDInsights上的Apache Spark連線至Adobe Experience Platform。
exl-id: c4a2a14e-5e16-44b7-b3f1-a98b7229f69e
source-git-commit: 5821f9304a37c1a03d17f0113d09548799662a2e
workflow-type: tm+mt
source-wordcount: '278'
ht-degree: 0%

---

# (Beta)[!DNL Apache Spark]連接器上的[!DNL Azure HDInsights]

>[!NOTE]
>
>[!DNL Azure HDInsights]連接器上的[!DNL Apache Spark]為測試版。 有關使用測試版標籤連接器的詳細資訊，請參閱[來源概述](../../home.md#terms-and-conditions)。

Adobe Experience Platform可讓您從外部來源擷取資料，同時使用[!DNL Platform]服務來建構、加標籤及增強傳入資料。 您可以從多種來源(如Adobe應用程式、雲儲存、資料庫等)內嵌資料。

[!DNL Experience Platform] 支援從協力廠商資料庫擷取資料。[!DNL Platform] 可以連接到不同類型的資料庫，如關係、 NoSQL或資料倉庫。對資料庫提供程式的支援包括[!DNL Azure HDInsights]上的[!DNL Apache Spark]。

## IP位址允許清單

使用來源連接器前，必須將IP位址清單新增至允許清單。 若未將您地區專屬的IP位址新增至允許清單，在使用來源時可能會導致錯誤或效能不佳。 如需詳細資訊，請參閱[IP位址允許清單](../../ip-address-allow-list.md)頁面。

以下檔案提供如何使用API或使用者介面將[!DNL Azure HDInsights]上的[!DNL Apache Spark]連線至[!DNL Platform]的資訊：

## 使用API將[!DNL Azure HDInsights]上的[!DNL Apache Spark]連線至[!DNL Platform]

- [使用流量服務API在Azure HDInsights基礎連線上建立Apache Spark](../../tutorials/api/create/databases/spark.md)
- [使用流服務API探索資料庫源的資料結構和內容](../../tutorials/api/explore/database-nosql.md)
- [使用流服務API為資料庫源建立資料流](../../tutorials/api/collect/database-nosql.md)

## 使用UI將[!DNL Azure HDInsights]上的[!DNL Apache Spark]連接到[!DNL Platform]

- [在UI中在Azure HDInsights來源連線上建立Apache Spark](../../tutorials/ui/create/databases/spark.md)
- [在UI中為資料庫源連接建立資料流](../../tutorials/ui/dataflow/databases.md)
