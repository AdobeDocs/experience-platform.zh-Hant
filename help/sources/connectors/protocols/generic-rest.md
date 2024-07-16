---
keywords: Experience Platform；首頁；熱門主題；一般REST；一般Rest
solution: Experience Platform
title: 一般REST API Source聯結器概觀
description: 瞭解如何使用API或使用者介面將Generic REST API連線到Adobe Experience Platform。
exl-id: e3449e33-7261-4aa2-bce9-5530eb4fcc68
source-git-commit: e37c00863249e677f1645266859bf40fe6451827
workflow-type: tm+mt
source-wordcount: '229'
ht-degree: 0%

---

# (Beta) [!DNL Generic REST API]

>[!NOTE]
>
>[!DNL Generic REST API]來源是測試版。 如需使用Beta標籤聯結器的詳細資訊，請參閱[來源概觀](../../home.md#terms-and-conditions)。

Adobe Experience Platform允許從外部來源擷取資料，同時讓您能夠使用[!DNL Platform]服務來建構、加標籤及增強傳入資料。 您可以從多種來源(例如Adobe應用程式、雲端儲存、資料庫和許多其他來源)內嵌資料。

平台提供從通訊協定應用程式（包括[!DNL Generic REST API]）擷取資料的支援。

[!DNL Generic REST API]來源可讓您將資料從REST型應用程式帶入Platform。 [!DNL Generic REST API]支援基本驗證和OAuth 2重新整理程式碼型驗證。

## IP位址允許清單

使用來源聯結器之前，必須將IP位址清單新增至允許清單。 未能將您區域特定的IP位址新增到允許清單可能會導致使用來源時的錯誤或效能不佳。 如需詳細資訊，請參閱[IP位址允許清單](../../ip-address-allow-list.md)頁面。

以下檔案提供如何使用API將[!DNL Generic REST API]來源連線到Platform的資訊。

## 使用API連線[!DNL Generic REST API]至[!DNL Platform]

- [使用流程服務API建立一般REST API基本連線](../../tutorials/api/create/protocols/generic-rest.md)
- [使用流量服務API探索資料表](../../tutorials/api/explore/tabular.md)
- [使用流程服務API為通訊協定來源建立資料流](../../tutorials/api/collect/protocols.md)
