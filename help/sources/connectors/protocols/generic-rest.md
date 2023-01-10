---
keywords: Experience Platform；首頁；熱門主題；一般REST；一般REST
solution: Experience Platform
title: 一般REST API來源連接器概觀
description: 了解如何使用API或使用者介面將一般REST API連線至Adobe Experience Platform。
exl-id: e3449e33-7261-4aa2-bce9-5530eb4fcc68
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '228'
ht-degree: 0%

---

# （測試版） [!DNL Generic REST API]

>[!NOTE]
>
>此 [!DNL Generic REST API] 來源為測試版。 請參閱 [來源概觀](../../home.md#terms-and-conditions) 有關使用測試版標籤連接器的詳細資訊。

Adobe Experience Platform可讓您從外部來源擷取資料，同時使用來建構、加標籤及增強傳入資料 [!DNL Platform] 服務。 您可以從多種來源(如Adobe應用程式、雲儲存、資料庫等)內嵌資料。

Platform支援從通訊協定應用程式擷取資料，包括 [!DNL Generic REST API].

此 [!DNL Generic REST API] 源允許將基於REST的應用程式中的資料導入Platform。 [!DNL Generic REST API] 支援基本驗證和OAuth 2重新整理程式碼式驗證。

## IP位址允許清單

使用來源連接器前，必須將IP位址清單新增至允許清單。 若未將您地區專屬的IP位址新增至允許清單，在使用來源時可能會導致錯誤或效能不佳。 請參閱 [IP位址允許清單](../../ip-address-allow-list.md) 頁面以取得詳細資訊。

以下檔案提供如何連線 [!DNL Generic REST API] 來源至平台（使用API）。

## Connect [!DNL Generic REST API] to [!DNL Platform] 使用API

- [使用流量服務API建立一般REST API基本連線](../../tutorials/api/create/protocols/generic-rest.md)
- [使用流量服務API探索資料表](../../tutorials/api/explore/tabular.md)
- [使用流服務API為協定源建立資料流](../../tutorials/api/collect/protocols.md)
