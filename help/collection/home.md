---
keywords: Experience Platform；首頁；熱門主題；資料收集；啟動；Web sdk
solution: Experience Platform
title: 資料彙集概觀
topic-legacy: overview
description: 了解在Adobe Experience Platform中收集客戶體驗資料所涉及的各種技術。
exl-id: 03ce5339-e68d-4adf-8c3c-82846a626dad
source-git-commit: 0926f0a6dc005b1bf278e7a0fa0afe4296d8ad80
workflow-type: tm+mt
source-wordcount: '458'
ht-degree: 4%

---

# 資料收集概觀

Adobe Experience Platform提供一套技術，可讓您從用戶端來源收集客戶體驗資料，並傳送至Adobe Experience Platform Edge Network，以便在數秒內擴充、轉換及分送至Adobe或非Adobe目的地。

下列用戶端來源支援資料收集：

* 基於Web的應用程式
* 原生行動應用程式
* 網路串流(OTT)應用程式

Experience Platform提供的資料收集技術著重於所擷取資料集的可探索性和協助功能。 這些技術包括下列內容：

* [Adobe Experience Platform Edge Network](https://experienceleague.adobe.com/docs/web-sdk-learn/tutorials/introduction-to-web-sdk-and-edge-network.html)
* [標籤](../tags/home.md)
* [資料流](../edge/fundamentals/datastreams.md)
* [事件轉送](../tags/ui/event-forwarding/overview.md)
* [Adobe Experience Platform Web SDK](../edge/home.md)
* [Adobe Experience Platform Mobile SDK](https://aep-sdks.gitbook.io/docs/)
* [Adobe Experience Platform Debugger](https://chrome.google.com/webstore/detail/adobe-experience-platform/bfnnokhpnncpkdmbokanobigaccjkpob?hl=en)
* [Experience Data Model(XDM)](../xdm/home.md)
* [Adobe Experience Platform Identity Service](../identity-service/home.md)

本指南提供資料收集架構的高階簡介，以及如何透過Platform Edge Network將資料傳送至Adobe Experience Cloud產品和非Adobe應用程式。

## 標籤、Web SDK和行動SDK

Platform Web SDK和Platform Mobile SDK會分別將所有Adobe產品程式庫折疊並壓縮為適用於Web和行動平台的單一開發套件。 這些可使用原始程式碼來實作，或使用 [標籤](../tags/home.md) 透過資料收集UI。

壓縮這些庫可加快資料收集速度，並將操作整合到從客戶端設備到Platform Edge Network的單個流中。

![標籤， Web SDK，行動SDK](./images/home/tags-sdks.png)

## 平台邊緣網路和資料流 {#edge}

Platform Edge Network是一個全球分佈、快速、可靠的伺服器網路，能夠以大規模接收和處理資料。 使用標籤時，您可以設定 [資料流](../edge/fundamentals/datastreams.md) 針對Adobe Target、Adobe Audience Manager和Adobe Analytics等產品，這可讓您在伺服器端啟用這些產品，而不需變更用戶端代碼。

![資料流和Adobe解決方案](./images/home/adobe-solutions.png)

>[!NOTE]
>
>如需Platform Edge Network的概要介紹，請參閱以下內容 [互動產品導覽](https://adobe-ideacloud.forgedx.com/adobe-adobe-edge-collection/adobe-experience-edge/public/mx?SUID=hgb1a48ICSCpbM6MzBYHbxnsh9DgjUy1).

## 事件轉送

[事件轉送](../tags/ui/event-forwarding/overview.md) 可點選任何Experience Platform資料流，讓您以極低的延遲轉換、擴充及傳送資料至任何非Adobe目的地，而無須將任何協力廠商程式碼新增至用戶端裝置。

![事件轉送](./images/home/event-forwarding.png)

## 後續步驟

本檔案概略介紹Platform的資料收集技術如何運作，以自動化將您收集的客戶體驗資料傳送至Adobe產品和協力廠商目的地的程式。

![資料收集框架](./images/home/collection.png)

如需透過邊緣網路傳送事件資料所涉及之一般工作流程的詳細資訊，請參閱 [資料收集的端對端概觀](./e2e.md).
