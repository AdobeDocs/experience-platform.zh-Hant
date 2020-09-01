---
keywords: Experience Platform;home;popular topics;MySQL;mysql;My sql;My SQL
solution: Experience Platform
title: MySQL連接器
topic: overview
description: 以下文檔提供了有關如何使用API或用戶介面將MySQL連接到平台的資訊。
translation-type: tm+mt
source-git-commit: d3ece56d10b1940a5992906a65a50ffe2f7e4346
workflow-type: tm+mt
source-wordcount: '237'
ht-degree: 0%

---


# （測試版）MySQL連接器

>[!NOTE]
>
>MySQL連接器處於測試階段。 如需使用 [測試版標籤連接器的詳細資訊](../../home.md#terms-and-conditions) ，請參閱來源概觀。

Adobe Experience Platform可讓您從外部來源擷取資料，同時提供您使用服務建構、標示及增強傳入資料的 [!DNL Platform] 能力。 您可以從多種來源（例如Adobe應用程式、雲端儲存空間、資料庫等）擷取資料。

[!DNL Experience Platform] 提供從第三方資料庫擷取資料的支援。 [!DNL Platform] 可以連接到不同類型的資料庫，如關係型、 NoSQL或資料倉庫。 支援資料庫提供者包括MySQL。

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

以下文檔提供了如何將MySQL連接到使用API [!DNL Platform] 或用戶介面的資訊：

## 將MySQL連接 [!DNL Platform] 到使用API

- [使用流服務API建立MySQL連接器](../../tutorials/api/create/databases/mysql.md)
- [使用Flow Service API探索資料庫系統](../../tutorials/api/explore/database-nosql.md)
- [使用Flow Service API從資料庫收集資料](../../tutorials/api/collect/database-nosql.md)

## 將MySQL連 [!DNL Platform] 接到UI

- [在UI中建立MySQL源連接器](../../tutorials/ui/create/databases/mysql.md)
- [在UI中為資料庫連接器配置資料流](../../tutorials/ui/dataflow/databases.md)