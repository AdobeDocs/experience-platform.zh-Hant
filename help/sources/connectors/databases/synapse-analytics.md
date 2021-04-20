---
keywords: Experience Platform;home；熱門主題；Azure synapse分析；azure synapse分析；Synapse;synapse
solution: Experience Platform
title: azure synapse分析來源連接器概觀
topic: overview
description: 瞭解如何使用API或使用者介面將Azure synapse分析連接至Adobe Experience Platform。
translation-type: tm+mt
source-git-commit: 0fb97fcf5d3f8230ff86906aeef245e4a7f44f30
workflow-type: tm+mt
source-wordcount: '290'
ht-degree: 0%

---


# （測試版）[!DNL Azure Synapse Analytics]連接器

Adobe Experience Platform允許從外部來源接收資料，同時提供使用[!DNL Platform]服務構建、標籤和增強傳入資料的能力。 您可以從多種來源收錄資料，例如Adobe應用程式、雲端儲存空間、資料庫等。

[!DNL Experience Platform] 提供從第三方資料庫擷取資料的支援。[!DNL Platform] 可以連接到不同類型的資料庫，如關係型、 NoSQL或資料倉庫。支援資料庫提供者包括[!DNL Azure Synapse Analytics]。

## IP位址允許清單

在使用來源連接器之前，必須將IP位址清單新增至允許清單。 若未將您地區專屬的IP位址新增至您的允許清單，在使用來源時可能會導致錯誤或效能不佳。 如需詳細資訊，請參閱[IP位址允許清單](../../ip-address-allow-list.md)頁面。

>[!IMPORTANT]
>
>[!DNL Azure Synapse Analytics]源連接器當前不支援與平台的相同區域連接。 這表示如果您的Azure例項使用與平台相同的網路區域，則無法建立與平台來源的連線。 目前僅支援跨地區連線。 如需詳細資訊，請洽詢您的Adobe客戶經理。

下面的文檔提供了如何使用API或用戶介面將[!DNL Azure Synapse Analytics]連接到[!DNL Platform]的資訊：

## 使用API將[!DNL Azure Synapse Analytics]連接至[!DNL Platform]

- [使用Flow Service API建立Azure synapseAnalytics來源連線](../../tutorials/api/create/databases/synapse-analytics.md)
- [使用Flow Service API探索資料庫系統](../../tutorials/api/explore/database-nosql.md)
- [使用Flow Service API從資料庫收集資料](../../tutorials/api/collect/database-nosql.md)

## 使用UI將[!DNL Azure Synapse Analytics]連接至[!DNL Platform]

- [在UI中建立Azure synapse分析來源連線](../../tutorials/ui/create/databases/synapse-analytics.md)
- [在UI中為資料庫連接配置資料流](../../tutorials/ui/dataflow/databases.md)