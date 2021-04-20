---
keywords: Experience Platform；首頁；熱門主題；AzureData Explorer;azure資料瀏覽器
solution: Experience Platform
title: AzureData Explorer源連接器概述
topic: overview
description: 瞭解如何使用API或使用者介面將AzureData Explorer連接至Adobe Experience Platform。
translation-type: tm+mt
source-git-commit: 0fb97fcf5d3f8230ff86906aeef245e4a7f44f30
workflow-type: tm+mt
source-wordcount: '270'
ht-degree: 0%

---


# （測試版）[!DNL Azure Data Explorer]連接器

>[!NOTE]
>
>[!DNL Azure Data Explorer]介面處於測試狀態。 有關使用beta標籤連接器的詳細資訊，請參閱[ Sources綜覽](../../home.md#terms-and-conditions)。

Adobe Experience Platform為[!DNL Microsoft]、MySQL和[!DNL Azure]等資料庫提供程式提供本機連接。 您可以將這些系統中的資料導入[!DNL Platform]。

支援不同類型的第三方資料庫，包括關聯式、NoSQL或資料倉庫。 支援資料庫提供者，包括[!DNL Azure Data Explorer]。

## IP位址允許清單

在使用來源連接器之前，必須將IP位址清單新增至允許清單。 若未將您地區專屬的IP位址新增至您的允許清單，在使用來源時可能會導致錯誤或效能不佳。 如需詳細資訊，請參閱[IP位址允許清單](../../ip-address-allow-list.md)頁面。

>[!IMPORTANT]
>
>[!DNL Azure Data Explorer]源連接器當前不支援與平台的相同區域連接。 這表示如果您的Azure例項使用與平台相同的網路區域，則無法建立與平台來源的連線。 目前僅支援跨地區連線。 如需詳細資訊，請洽詢您的Adobe客戶經理。

下面的文檔提供了如何使用API或用戶介面將[!DNL Azure Data Explorer]連接到[!DNL Platform]的資訊：

## 使用API將[!DNL Azure Data Explorer]連接至[!DNL Platform]

- [使用Flow Service API建立AzureData Explorer來源連線](../../tutorials/api/create/databases/data-explorer.md)
- [使用Flow Service API探索資料庫系統](../../tutorials/api/explore/database-nosql.md)
- [使用Flow Service API從資料庫收集資料](../../tutorials/api/collect/database-nosql.md)

## 使用UI將[!DNL Azure Data Explorer]連接至[!DNL Platform]

- [在UI中建立AzureData Explorer來源連線](../../tutorials/ui/create/databases/data-explorer.md)
- [在UI中為資料庫連接配置資料流](../../tutorials/ui/dataflow/databases.md)