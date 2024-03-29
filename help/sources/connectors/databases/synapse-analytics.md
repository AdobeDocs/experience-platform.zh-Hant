---
title: azure synapse Analytics來源聯結器總覽
description: 瞭解如何使用API或使用者介面將Azure synapse Analytics連結至Adobe Experience Platform。
badgeUltimate: label="Ultimate" type="Positive"
exl-id: 5b94ae74-e5a7-40e9-a952-41eddf06dcde
source-git-commit: 9a8139c26b5bb5ff937a51986967b57db58aab6c
workflow-type: tm+mt
source-wordcount: '246'
ht-degree: 0%

---

# [!DNL Azure Synapse Analytics] 來源

>[!IMPORTANT]
>
>此 [!DNL Azure Synapse Analytics] 已購買Real-time Customer Data Platform Ultimate的使用者可在來源目錄中取得來源。

Adobe Experience Platform可讓您從外部來源擷取資料，同時能夠使用來建構、加標籤及增強傳入資料 [!DNL Platform] 服務。 您可以從多種來源(例如Adobe應用程式、雲端儲存、資料庫和許多其他來源)內嵌資料。

[!DNL Experience Platform] 支援從第三方資料庫擷取資料。 [!DNL Platform] 可以連線到不同型別的資料庫，例如關聯式、NoSQL或資料倉儲。 對資料庫提供者的支援包括 [!DNL Azure Synapse Analytics].

## IP位址允許清單

使用來源聯結器之前，必須將IP位址清單新增至允許清單。 未能將您區域特定的IP位址新增到允許清單可能會導致使用來源時的錯誤或效能不佳。 請參閱 [IP位址允許清單](../../ip-address-allow-list.md) 頁面以取得詳細資訊。

以下檔案提供有關如何連線的資訊 [!DNL Azure Synapse Analytics] 至 [!DNL Platform] 使用API或使用者介面：

## 連線 [!DNL Azure Synapse Analytics] 至 [!DNL Platform] 使用API

- [使用流量服務API建立Azure synapse Analytics基本連線](../../tutorials/api/create/databases/synapse-analytics.md)
- [使用流量服務API探索資料表](../../tutorials/api/explore/tabular.md)
- [使用流程服務API為資料庫來源建立資料流](../../tutorials/api/collect/database-nosql.md)

## 連線 [!DNL Azure Synapse Analytics] 至 [!DNL Platform] 使用UI

- [在UI中建立Azure synapse Analytics來源連線](../../tutorials/ui/create/databases/synapse-analytics.md)
- [在UI中建立資料庫來源連線的資料流](../../tutorials/ui/dataflow/databases.md)
