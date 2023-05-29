---
keywords: Experience Platform；首頁；熱門主題；Apache Spark；Apache Spark；Azure HDInsights；Azure hdinsights
solution: Experience Platform
title: Azure HDInsights來源聯結器上的Apache Spark概述
description: 瞭解如何使用API或使用者介面將Azure HDInsights上的Apache Spark連線到Adobe Experience Platform。
exl-id: c4a2a14e-5e16-44b7-b3f1-a98b7229f69e
source-git-commit: e37c00863249e677f1645266859bf40fe6451827
workflow-type: tm+mt
source-wordcount: '271'
ht-degree: 0%

---

# (Beta) [!DNL Apache Spark] 於 [!DNL Azure HDInsights] 聯結器

>[!NOTE]
>
>此 [!DNL Apache Spark] 於 [!DNL Azure HDInsights] 聯結器為測試版。 請參閱 [來源概觀](../../home.md#terms-and-conditions) 以取得使用Beta標籤聯結器的詳細資訊。

Adobe Experience Platform可從外部來源擷取資料，同時讓您能夠使用來建構、加標籤及增強傳入資料 [!DNL Platform] 服務。 您可以從多種來源(例如Adobe應用程式、雲端儲存、資料庫和許多其他來源)內嵌資料。

[!DNL Experience Platform] 支援從第三方資料庫擷取資料。 [!DNL Platform] 可以連線到不同型別的資料庫，例如關聯式、NoSQL或資料倉儲。 對資料庫提供者的支援包括 [!DNL Apache Spark] 於 [!DNL Azure HDInsights].

## IP位址允許清單

在使用來源聯結器之前，必須將IP位址清單新增至允許清單。 使用來源時，若未將您地區專屬的IP位址新增至允許清單，可能會導致錯誤或效能不佳。 請參閱 [IP位址允許清單](../../ip-address-allow-list.md) 頁面以取得詳細資訊。

以下檔案提供有關如何連線的資訊 [!DNL Apache Spark] 於 [!DNL Azure HDInsights] 至 [!DNL Platform] 使用API或使用者介面：

## Connect [!DNL Apache Spark] 於 [!DNL Azure HDInsights] 至 [!DNL Platform] 使用API

- [使用Flow Service API在Azure HDInsights基本連線上建立Apache Spark](../../tutorials/api/create/databases/spark.md)
- [使用Flow Service API探索資料表](../../tutorials/api/explore/tabular.md)
- [使用流程服務API為資料庫來源建立資料流](../../tutorials/api/collect/database-nosql.md)

## Connect [!DNL Apache Spark] 於 [!DNL Azure HDInsights] 至 [!DNL Platform] 使用UI

- [在UI中的Azure HDInsights來源連線上建立Apache Spark](../../tutorials/ui/create/databases/spark.md)
- [在UI中建立資料庫來源連線的資料流](../../tutorials/ui/dataflow/databases.md)
