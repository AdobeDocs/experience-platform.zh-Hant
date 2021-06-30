---
keywords: Experience Platform；首頁；熱門主題；Azure表儲存；Azure表儲存；ATS;ATS
solution: Experience Platform
title: Azure表儲存源連接器概述
topic-legacy: overview
description: 了解如何使用API或使用者介面將Azure表格儲存連接至Adobe Experience Platform。
exl-id: 096e01b1-7e95-4e30-87de-d0976f8b438a
source-git-commit: 5821f9304a37c1a03d17f0113d09548799662a2e
workflow-type: tm+mt
source-wordcount: '314'
ht-degree: 0%

---

# (Beta)[!DNL Azure Table Storage]連接器

>[!NOTE]
>
>[!DNL Azure Table Storage]連接器為測試版。 有關使用測試版標籤連接器的詳細資訊，請參閱[來源概述](../../home.md#terms-and-conditions)。

Adobe Experience Platform可讓您從外部來源擷取資料，同時使用[!DNL Platform]服務來建構、加標籤及增強傳入資料。 您可以從多種來源(如Adobe應用程式、雲儲存、資料庫等)內嵌資料。

[!DNL Experience Platform] 支援從協力廠商資料庫擷取資料。[!DNL Platform] 可以連接到不同類型的資料庫，如關係、 NoSQL或資料倉庫。對資料庫提供程式的支援包括[!DNL Azure Table Storage]。

## IP位址允許清單

使用來源連接器前，必須將IP位址清單新增至允許清單。 若未將您地區專屬的IP位址新增至允許清單，在使用來源時可能會導致錯誤或效能不佳。 如需詳細資訊，請參閱[IP位址允許清單](../../ip-address-allow-list.md)頁面。

>[!IMPORTANT]
>
>[!DNL Azure Table Storage]源連接器當前不支援與Platform的相同區域連接。 這表示，如果您的Azure執行個體使用與Platform相同的網路區域，則無法建立與Platform來源的連線。 目前僅支援跨地區連線。 如需詳細資訊，請連絡您的Adobe客戶經理。

以下檔案提供如何使用API或使用者介面將[!DNL Azure Table Storage]連線至[!DNL Platform]的資訊：

## 使用API將[!DNL Azure Table Storage]連線至[!DNL Platform]

- [使用流服務API建立Azure表儲存基連接](../../tutorials/api/create/databases/ats.md)
- [使用流服務API探索資料庫源的資料結構和內容](../../tutorials/api/explore/database-nosql.md)
- [使用流服務API為資料庫源建立資料流](../../tutorials/api/collect/database-nosql.md)

## 使用UI將[!DNL Azure Table Storage]連線至[!DNL Platform]

- [在UI中建立Azure表儲存源連接](../../tutorials/ui/create/databases/ats.md)
- [在UI中為資料庫源連接建立資料流](../../tutorials/ui/dataflow/databases.md)
