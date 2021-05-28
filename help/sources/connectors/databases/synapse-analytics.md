---
keywords: Experience Platform；首頁；熱門主題；Azure synapse分析；azure synapse分析；Synapse;Synapse
solution: Experience Platform
title: azure synapseAnalytics來源連接器概觀
topic-legacy: overview
description: 了解如何使用API或使用者介面將Azure synapseAnalytics連線至Adobe Experience Platform。
exl-id: 5b94ae74-e5a7-40e9-a952-41eddf06dcde
source-git-commit: e150f05df2107d7b3a2e95a55dc4ad072294279e
workflow-type: tm+mt
source-wordcount: '288'
ht-degree: 0%

---

# [!DNL Azure Synapse Analytics] 連接器

Adobe Experience Platform可讓您從外部來源擷取資料，同時使用[!DNL Platform]服務來建構、加標籤及增強傳入資料。 您可以從多種來源(如Adobe應用程式、雲儲存、資料庫等)內嵌資料。

[!DNL Experience Platform] 支援從協力廠商資料庫擷取資料。[!DNL Platform] 可以連接到不同類型的資料庫，如關係、 NoSQL或資料倉庫。對資料庫提供程式的支援包括[!DNL Azure Synapse Analytics]。

## IP位址允許清單

使用來源連接器前，必須將IP位址清單新增至允許清單。 若未將您地區專屬的IP位址新增至允許清單，在使用來源時可能會導致錯誤或效能不佳。 如需詳細資訊，請參閱[IP位址允許清單](../../ip-address-allow-list.md)頁面。

>[!IMPORTANT]
>
>[!DNL Azure Synapse Analytics]源連接器當前不支援與Platform的相同區域連接。 這表示，如果您的Azure執行個體使用與Platform相同的網路區域，則無法建立與Platform來源的連線。 目前僅支援跨地區連線。 如需詳細資訊，請連絡您的Adobe客戶經理。

以下檔案提供如何使用API或使用者介面將[!DNL Azure Synapse Analytics]連線至[!DNL Platform]的資訊：

## 使用API將[!DNL Azure Synapse Analytics]連線至[!DNL Platform]

- [使用流量服務API建立Azure synapseAnalytics來源連線](../../tutorials/api/create/databases/synapse-analytics.md)
- [使用流服務API探索資料庫系統](../../tutorials/api/explore/database-nosql.md)
- [使用流服務API從資料庫收集資料](../../tutorials/api/collect/database-nosql.md)

## 使用UI將[!DNL Azure Synapse Analytics]連線至[!DNL Platform]

- [在UI中建立Azure synapseAnalytics來源連線](../../tutorials/ui/create/databases/synapse-analytics.md)
- [在UI中為資料庫連接配置資料流](../../tutorials/ui/dataflow/databases.md)
