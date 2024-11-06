---
title: Phoenix Source概觀
description: 瞭解如何使用API或使用者介面將您的Phoenix帳戶連結至Adobe Experience Platform。
last-substantial-update: 2023-07-26T00:00:00Z
exl-id: 45e6ef18-a0b7-4bb2-b099-b2a878e96637
source-git-commit: 0781d04af12c4c11dfc917adfdec8673cf3be8de
workflow-type: tm+mt
source-wordcount: '204'
ht-degree: 0%

---

# [!DNL Phoenix]

>[!IMPORTANT]
>
>[!DNL Phoenix]來源將於2025年5月底淘汰。 您可以使用[[!DNL Data Landing Zone]](../cloud-storage/data-landing-zone.md)取代[!DNL Phoenix]來源。

Adobe Experience Platform來源支援從協力廠商資料庫（例如[[!DNL Phoenix]](https://phoenix.apache.org/index.html)）擷取資料。 在透過[!DNL Flow Service] API或Experience Platform使用者介面連線您的[!DNL Phoenix]帳戶之前，本檔案會提供先決條件資訊。

## IP位址允許清單

使用來源聯結器之前，必須將IP位址清單新增至允許清單。 未能將您區域特定的IP位址新增到允許清單可能會導致使用來源時的錯誤或效能不佳。 如需詳細資訊，請參閱[IP位址允許清單](../../ip-address-allow-list.md)頁面。

以下檔案提供有關如何使用API或使用者介面連線[!DNL Phoenix]以Experience Platform的資訊：

## 連線[!DNL Phoenix]以使用APIExperience Platform

* [使用Flow Service API建立Phoenix基本連線](../../tutorials/api/create/databases/phoenix.md)
* [使用流量服務API探索資料表](../../tutorials/api/explore/tabular.md)
* [使用流程服務API為資料庫來源建立資料流](../../tutorials/api/collect/database-nosql.md)

## 使用UI連線[!DNL Phoenix]以Experience Platform

* [使用Experience Platform使用者介面連線您的 [!DNL Phoenix] 帳戶](../../tutorials/ui/create/databases/phoenix.md)
* [在UI中建立資料庫來源連線的資料流](../../tutorials/ui/dataflow/databases.md)
