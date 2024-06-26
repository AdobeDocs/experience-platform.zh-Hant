---
title: Snowflake來源聯結器概述
description: 瞭解如何使用API或使用者介面將Snowflake連結至Adobe Experience Platform。
badgeUltimate: label="Ultimate" type="Positive"
exl-id: df066463-1ae6-4ecd-ae0e-fb291cec4bd5
source-git-commit: 8b0f6eca87deedd8090830e3375d5099bfb0dfc0
workflow-type: tm+mt
source-wordcount: '303'
ht-degree: 0%

---

# [!DNL Snowflake] 來源

>[!IMPORTANT]
>
>* 此 [!DNL Snowflake] 已購買Real-time Customer Data Platform Ultimate的使用者可在來源目錄中取得來源。
>* 根據預設， [!DNL Snowflake] 來源解譯 `null` 作為空字串。 請聯絡您的Adobe代表，確保 `null` 值會正確寫入為 `null` 在Adobe Experience Platform中。
>* 為了讓Experience Platform擷取資料，所有以表格為基礎的批次來源的時區都必須設定為UTC。 唯一支援的時間戳記 [!DNL Snowflake] 來源是TIMESTAMP_NTZ搭配UTC時間。

Adobe Experience Platform可讓您從外部來源擷取資料，同時使用Platform服務來建構、加標籤及增強傳入資料。 您可以從多種來源(例如Adobe應用程式、雲端儲存、資料庫和許多其他來源)內嵌資料。

Experience Platform支援從協力廠商資料庫擷取資料。 Platform可以連線到不同型別的資料庫，例如關聯式、NoSQL或資料倉儲。 對資料庫提供者的支援包括 [!DNL Snowflake].

## IP位址允許清單

使用來源聯結器之前，必須將IP位址清單新增至允許清單。 未能將您區域特定的IP位址新增到允許清單可能會導致使用來源時的錯誤或效能不佳。 請參閱 [IP位址允許清單](../../ip-address-allow-list.md) 頁面以取得詳細資訊。

以下檔案提供有關如何連線的資訊 [!DNL Snowflake] 使用API或使用者介面至Platform：

## 連線 [!DNL Snowflake] 使用API移至Platform

* [使用Flow Service API建立Snowflake基本連線](../../tutorials/api/create/databases/snowflake.md)
* [使用流量服務API探索資料表](../../tutorials/api/explore/tabular.md)
* [使用流程服務API為資料庫來源建立資料流](../../tutorials/api/collect/database-nosql.md)

## 連線 [!DNL Snowflake] 使用UI移至Platform

* [在使用者介面中建立Snowflake來源連線](../../tutorials/ui/create/databases/snowflake.md)
* [在UI中建立資料庫來源連線的資料流](../../tutorials/ui/dataflow/databases.md)
