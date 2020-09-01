---
keywords: Experience Platform;home;popular topics;greenplum;GreenPlum
solution: Experience Platform
title: GreenPlum連接器
topic: overview
description: 以下檔案提供如何使用API或使用者介面將GreenPlum連接至平台的資訊。
translation-type: tm+mt
source-git-commit: d3ece56d10b1940a5992906a65a50ffe2f7e4346
workflow-type: tm+mt
source-wordcount: '197'
ht-degree: 0%

---


# （測試版）連 [!DNL GreenPlum] 接器

>[!NOTE]
>
>連接 [!DNL GreenPlum] 器為測試版。 如需使用 [測試版標籤連接器的詳細資訊](../../home.md#terms-and-conditions) ，請參閱來源概觀。

Adobe Experience Platform為資料庫提供者(例如MySQL [!DNL Microsoft]和)提供原生連接 [!DNL Azure]。 您可以將這些系統的資料匯入其中 [!DNL Platform]。

支援不同類型的第三方資料庫，包括關聯式、NoSQL或資料倉庫。 支援資料庫提供者包括 [!DNL GreenPlum]。

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

以下檔案提供如何連線至使用API [!DNL GreenPlum] 或使 [!DNL Platform] 用者介面的資訊：

## 連線 [!DNL GreenPlum] 至使 [!DNL Platform] 用API

- [使用Flow Service API建立GreenPlum連接器](../../tutorials/api/create/databases/greenplum.md)
- [使用Flow Service API探索資料庫系統](../../tutorials/api/explore/database-nosql.md)
- [使用Flow Service API從資料庫收集資料](../../tutorials/api/collect/database-nosql.md)

## 使用 [!DNL GreenPlum] UI [!DNL Platform] 連線至

- [在UI中建立GreenPlum來源連接器](../../tutorials/ui/create/databases/greenplum.md)
- [在UI中為資料庫連接器配置資料流](../../tutorials/ui/dataflow/databases.md)