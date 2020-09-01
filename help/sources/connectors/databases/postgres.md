---
keywords: Experience Platform;home;popular topics;PostgreSQL;postgresql
solution: Experience Platform
title: PostgreSQL連接器
topic: overview
description: 以下文檔提供了有關如何使用API或用戶介面將PostgreSQL連接到平台的資訊。
translation-type: tm+mt
source-git-commit: d3ece56d10b1940a5992906a65a50ffe2f7e4346
workflow-type: tm+mt
source-wordcount: '232'
ht-degree: 0%

---


# （測試版）連 [!DNL PostgreSQL] 接器

>[!NOTE]
>
>連接 [!DNL PostgreSQL] 器為測試版。 如需使用 [測試版標籤連接器的詳細資訊](../../home.md#terms-and-conditions) ，請參閱來源概觀。

Adobe Experience Platform可讓您從外部來源擷取資料，同時提供您使用平台服務來建構、標示及增強傳入資料的能力。 您可以從多種來源（例如Adobe應用程式、雲端儲存空間、資料庫等）擷取資料。

[!DNL Experience Platform] 提供從第三方資料庫擷取資料的支援。 [!DNL Platform] 可以連接到不同類型的資料庫，如關係型、 NoSQL或資料倉庫。 支援資料庫提供者包括 [!DNL PostgreSQL]。

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

以下檔案提供如何連線至使用API [!DNL PostgreSQL] 或使 [!DNL Platform] 用者介面的資訊：

## 連線 [!DNL PostgreSQL] 至使 [!DNL Platform] 用API

- [使用流服務API建立PostgreSQL連接器](../../tutorials/api/create/databases/postgres.md)
- [使用Flow Service API探索資料庫系統](../../tutorials/api/explore/database-nosql.md)
- [使用Flow Service API從資料庫收集資料](../../tutorials/api/collect/database-nosql.md)

## 使用 [!DNL PostgreSQL] UI [!DNL Platform] 連線至

- [在UI中建立PostgreSQL源連接器](../../tutorials/ui/create/databases/postgres.md)
- [在UI中為資料庫連接器配置資料流](../../tutorials/ui/dataflow/databases.md)