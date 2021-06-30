---
keywords: Experience Platform；首頁；熱門主題；AzureData Explorer;azure資料瀏覽器
solution: Experience Platform
title: AzureData Explorer源連接器概述
topic-legacy: overview
description: 了解如何使用API或使用者介面將AzureData Explorer連線至Adobe Experience Platform。
exl-id: 869bd8bb-51e6-4e0c-a3ec-ff083dda5789
source-git-commit: 5821f9304a37c1a03d17f0113d09548799662a2e
workflow-type: tm+mt
source-wordcount: '278'
ht-degree: 0%

---

# (Beta)[!DNL Azure Data Explorer]連接器

>[!NOTE]
>
>[!DNL Azure Data Explorer]連接器為測試版。 有關使用測試版標籤連接器的詳細資訊，請參閱[來源概述](../../home.md#terms-and-conditions)。

Adobe Experience Platform為[!DNL Microsoft]、MySQL和[!DNL Azure]等資料庫提供程式提供本機連接。 您可以將資料從這些系統帶入[!DNL Platform]。

支援不同類型的第三方資料庫，包括關係、 NoSQL或資料倉庫。 對資料庫提供程式的支援包括[!DNL Azure Data Explorer]。

## IP位址允許清單

使用來源連接器前，必須將IP位址清單新增至允許清單。 若未將您地區專屬的IP位址新增至允許清單，在使用來源時可能會導致錯誤或效能不佳。 如需詳細資訊，請參閱[IP位址允許清單](../../ip-address-allow-list.md)頁面。

>[!IMPORTANT]
>
>[!DNL Azure Data Explorer]源連接器當前不支援與Platform的相同區域連接。 這表示，如果您的Azure執行個體使用與Platform相同的網路區域，則無法建立與Platform來源的連線。 目前僅支援跨地區連線。 如需詳細資訊，請連絡您的Adobe客戶經理。

以下檔案提供如何使用API或使用者介面將[!DNL Azure Data Explorer]連線至[!DNL Platform]的資訊：

## 使用API將[!DNL Azure Data Explorer]連線至[!DNL Platform]

- [使用流服務API建立AzureData Explorer基連接](../../tutorials/api/create/databases/data-explorer.md)
- [使用流服務API探索資料庫源的資料結構和內容](../../tutorials/api/explore/database-nosql.md)
- [使用流服務API為資料庫源建立資料流](../../tutorials/api/collect/database-nosql.md)

## 使用UI將[!DNL Azure Data Explorer]連線至[!DNL Platform]

- [在UI中建立AzureData Explorer來源連線](../../tutorials/ui/create/databases/data-explorer.md)
- [在UI中為資料庫源連接建立資料流](../../tutorials/ui/dataflow/databases.md)
