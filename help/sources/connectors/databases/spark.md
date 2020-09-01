---
keywords: Experience Platform;home;popular topics;Apache Spark;apache spark;Azure HDInsights;azure hdinsights
solution: Experience Platform
title: Apache Spark on Azure HDInsights連接器
topic: overview
description: 以下說明檔案提供如何使用API或使用者介面，將Azure HDInsights上的Apache Spark連接至平台的資訊。
translation-type: tm+mt
source-git-commit: d3ece56d10b1940a5992906a65a50ffe2f7e4346
workflow-type: tm+mt
source-wordcount: '253'
ht-degree: 0%

---


# （測試版） [!DNL Apache Spark] ，連接 [!DNL Azure HDInsights] 器

>[!NOTE]
>
>開 [!DNL Apache Spark] 機接 [!DNL Azure HDInsights] 頭為測試版。 如需使用 [測試版標籤連接器的詳細資訊](../../home.md#terms-and-conditions) ，請參閱來源概觀。

Adobe Experience Platform可讓您從外部來源擷取資料，同時提供您使用服務建構、標示及增強傳入資料的 [!DNL Platform] 能力。 您可以從多種來源（例如Adobe應用程式、雲端儲存空間、資料庫等）擷取資料。

[!DNL Experience Platform] 提供從第三方資料庫擷取資料的支援。 [!DNL Platform] 可以連接到不同類型的資料庫，如關係型、 NoSQL或資料倉庫。 對資料庫提供者的支援包括 [!DNL Apache Spark] 在 [!DNL Azure HDInsights]。

## IP位址允許清單

在使用源連接器之前，必須將下列IP位址新增至允許清單。 若未將您地區專屬的IP位址新增至您的允許清單，在使用來源時可能會導致錯誤或效能不佳。

### 美國東部地區

- `20.41.2.0/23`
- `20.41.4.0/26`
- `20.44.17.80/28`
- `20.49.102.16/29`
- `40.70.148.160/28`
- `52.167.107.224/28`

### 西歐地區

- `13.69.67.192/28`
- `13.69.107.112/28`
- `13.69.112.128/28`
- `40.74.24.192/26`
- `40.74.26.0/23`
- `40.113.176.232/29`
- `52.236.187.112/28`

### 澳洲東部

- `13.70.74.144/28`
- `20.37.193.0/25`
- `20.37.193.128/26`
- `20.37.198.224/29`
- `40.79.163.80/28`
- `40.79.171.160/28`

以下檔案提供如何使用API [!DNL Apache Spark] 或使 [!DNL Azure HDInsights] 用者 [!DNL Platform] 介面連線的資訊：

## 使用 [!DNL Apache Spark] API連 [!DNL Azure HDInsights] 接 [!DNL Platform] 至

- [在Azure HDInsights上使用Flow Service API建立Apache Spark連接器](../../tutorials/api/create/databases/spark.md)
- [使用Flow Service API探索資料庫系統](../../tutorials/api/explore/database-nosql.md)
- [使用Flow Service API從資料庫收集資料](../../tutorials/api/collect/database-nosql.md)

## 使 [!DNL Apache Spark] 用 [!DNL Azure HDInsights] UI連 [!DNL Platform] 接至

- [在Azure HDInsights的UI中建立Apache Spark來源連接器](../../tutorials/ui/create/databases/spark.md)
- [在UI中為資料庫連接器配置資料流](../../tutorials/ui/dataflow/databases.md)