---
keywords: Experience Platform;home；熱門主題；PostgreSQL;postgresql
solution: Experience Platform
title: PostgreSQL源連接器概述
topic: overview
description: 瞭解如何使用API或使用者介面將PostgreSQL連線至Adobe Experience Platform。
translation-type: tm+mt
source-git-commit: c7fb0d50761fa53c1fdf4dd70a63c62f2dcf6c85
workflow-type: tm+mt
source-wordcount: '242'
ht-degree: 0%

---


# （測試版）[!DNL PostgreSQL]連接器

>[!NOTE]
>
>[!DNL PostgreSQL]介面處於測試狀態。 有關使用beta標籤連接器的詳細資訊，請參閱[來源概觀](../../home.md#terms-and-conditions)。

Adobe Experience Platform可讓您從外部來源擷取資料，同時提供您使用平台服務來建構、標示及增強傳入資料的能力。 您可以從多種來源（例如Adobe應用程式、雲端儲存空間、資料庫等）擷取資料。

[!DNL Experience Platform] 提供從第三方資料庫擷取資料的支援。[!DNL Platform] 可以連接到不同類型的資料庫，如關係型、 NoSQL或資料倉庫。支援資料庫提供者包括[!DNL PostgreSQL]。

## IP位址允許清單

在使用來源連接器之前，必須將IP位址清單新增至允許清單。 若未將您地區專屬的IP位址新增至您的允許清單，在使用來源時可能會導致錯誤或效能不佳。 如需詳細資訊，請參閱[IP位址允許清單](../../ip-address-allow-list.md)頁面。

下面的文檔提供了如何使用API或用戶介面將[!DNL PostgreSQL]連接到[!DNL Platform]的資訊：

## 使用API將[!DNL PostgreSQL]連接至[!DNL Platform]

- [使用流服務API建立PostgreSQL源連接](../../tutorials/api/create/databases/postgres.md)
- [使用Flow Service API探索資料庫系統](../../tutorials/api/explore/database-nosql.md)
- [使用Flow Service API從資料庫收集資料](../../tutorials/api/collect/database-nosql.md)

## 使用UI將[!DNL PostgreSQL]連接至[!DNL Platform]

- [在UI中建立PostgreSQL源連接](../../tutorials/ui/create/databases/postgres.md)
- [在UI中為資料庫連接配置資料流](../../tutorials/ui/dataflow/databases.md)