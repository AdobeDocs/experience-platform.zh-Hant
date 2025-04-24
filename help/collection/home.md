---
keywords: Experience Platform；首頁；熱門主題；資料收集；launch；web sdk
solution: Experience Platform
title: 資料彙集概觀
description: 瞭解在Adobe Experience Platform中收集客戶體驗資料相關的各種技術。
exl-id: 03ce5339-e68d-4adf-8c3c-82846a626dad
source-git-commit: 7f3459f678c74ead1d733304702309522dd0018b
workflow-type: tm+mt
source-wordcount: '479'
ht-degree: 3%

---

# 資料彙集概觀

Adobe Experience Platform提供了一套技術，可讓您從使用者端來源收集客戶體驗資料，並將資料傳送到Adobe Experience Platform Edge Network，在那裡可以快速擴充和轉換資料，並將其分發到Adobe或非Adobe目的地。

下列使用者端來源支援資料收集：

* 網頁式應用程式
* 原生行動應用程式
* 過頂式(OTT)應用程式

資料收集著重於所擷取資料集的可發現性和可存取性，包含下列專案：

* [Adobe Experience Platform Edge Network](https://experienceleague.adobe.com/docs/web-sdk-learn/tutorials/introduction-to-web-sdk-and-edge-network.html)
* [標記](../tags/home.md)
* [資料流](../datastreams/overview.md)
* [事件轉送](../tags/ui/event-forwarding/overview.md)
* [Adobe Experience Platform Web SDK](../web-sdk/home.md)
* [Adobe Experience Platform Mobile SDK](https://developer.adobe.com/client-sdks/documentation/)
* [Edge Network API](https://developer.adobe.com/data-collection-apis/docs/api/)
* [Adobe Experience Platform Debugger](https://chrome.google.com/webstore/detail/adobe-experience-platform/bfnnokhpnncpkdmbokanobigaccjkpob?hl=en)
* [Experience Platform Assurance](../assurance/home.md)


本指南提供資料收集的高層級簡介，並說明如何透過Experience Platform Edge Network將資料傳送至Adobe Experience Cloud產品和非Adobe應用程式。

## 標籤、Web SDK和Mobile SDK

Experience Platform Web SDK和Experience Platform Mobile SDK可摺疊所有Adobe產品程式庫，並將其壓縮為分別適用於Web和行動平台的單一開發套件。 您可以使用原始程式碼或透過資料收集UI或Adobe Experience Platform UI使用[標籤](../tags/home.md)來實作這些專案。

壓縮這些程式庫可加快資料收集速度，並將從使用者端裝置到Experience Platform Edge Network的作業整合為單一資料流。

![標籤，網頁SDK，行動SDK](./images/home/tags-sdks.png)

## Experience Platform Edge Network和資料串流 {#edge}

Experience Platform Edge Network是一套遍佈全球、快速且可靠的伺服器網路，能夠接收和處理規模龐大的資料。 使用標籤，您可以為Adobe Target、Adobe Audience Manager和Adobe Analytics等產品設定[資料串流](../datastreams/overview.md)，讓您無需變更使用者端程式碼即可在伺服器端啟動這些產品。

此外，資料串流可與數項Experience Platform功能整合，有助於確保您傳送的任何敏感資料都會受到組織政策和法規的適當處理。 如需詳細資訊，請參閱資料串流檔案中有關[處理敏感資料](../datastreams/overview.md#sensitive)的部分。

![資料串流和Adobe解決方案](./images/home/adobe-solutions.png)

## 事件轉送

[事件轉送](../tags/ui/event-forwarding/overview.md)可以利用任何Experience Platform資料串流，讓您以極低的延遲轉換及擴充資料，並將資料傳送到任何非Adobe目的地，而且不需要將任何協力廠商程式碼新增到使用者端裝置。

![事件轉送](./images/home/event-forwarding.png)

>[!NOTE]
>
>事件轉送是一項付費功能，包含在Adobe Real-Time Customer Data Platform連線、Prime或Ultimate供應專案中。

## 後續步驟

本檔案以高階方式概述資料收集如何運作，以自動化將收集的客戶體驗資料傳送至Adobe產品和第三方目的地的程式。

![資料收集架構](./images/home/collection.png)

如需有關透過Edge Network傳送事件資料所需的一般工作流程的詳細資訊，請參閱[端對端總覽](./e2e.md)。
