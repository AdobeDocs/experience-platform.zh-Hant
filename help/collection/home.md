---
keywords: Experience Platform；首頁；熱門主題；資料收集；啟動；Web sdk
solution: Experience Platform
title: 資料彙集概觀
topic-legacy: overview
description: 了解在Adobe Experience Platform中收集客戶體驗資料所涉及的各種技術。
exl-id: 03ce5339-e68d-4adf-8c3c-82846a626dad
source-git-commit: 14e3eff3ea2469023823a35ee1112568f5b5f4f7
workflow-type: tm+mt
source-wordcount: '514'
ht-degree: 6%

---

# 資料彙集概觀

Adobe Experience Platform提供一套技術，可讓您從用戶端來源收集客戶體驗資料，並傳送至Adobe Experience Platform Edge Network，以便在數秒內擴充、轉換及分送至Adobe或非Adobe目的地。

下列用戶端來源支援資料收集：

* 基於Web的應用程式
* 原生行動應用程式
* 網路串流(OTT)應用程式

資料收集著重於所擷取資料集的可探索性和可存取性，其中包括：

* [Adobe Experience Platform Edge Network](https://experienceleague.adobe.com/docs/web-sdk-learn/tutorials/introduction-to-web-sdk-and-edge-network.html)
* [標記](../tags/home.md)
* [資料串流](../edge/datastreams/overview.md)
* [事件轉送](../tags/ui/event-forwarding/overview.md)
* [Adobe Experience Platform Web SDK](../edge/home.md)
* [Adobe Experience Platform Mobile SDK](https://aep-sdks.gitbook.io/docs/)
* [Adobe Experience Platform Debugger](https://chrome.google.com/webstore/detail/adobe-experience-platform/bfnnokhpnncpkdmbokanobigaccjkpob?hl=en)
* [Experience Data Model(XDM)](../xdm/home.md)
* [Adobe Experience Platform Identity Service](../identity-service/home.md)

本指南提供資料收集的高階簡介，以及如何透過Platform Edge Network將資料傳送至Adobe Experience Cloud產品和非Adobe應用程式。

## 標籤、Web SDK和行動SDK

Platform Web SDK和Platform Mobile SDK會分別將所有Adobe產品程式庫折疊並壓縮為適用於Web和行動平台的單一開發套件。 這些可使用原始程式碼來實作，或使用 [標籤](../tags/home.md) 透過資料收集UI或Adobe Experience Platform UI。

壓縮這些庫可加快資料收集速度，並將操作整合到從客戶端設備到Platform Edge Network的單個流中。

![標籤， Web SDK，行動SDK](./images/home/tags-sdks.png)

## 平台邊緣網路和資料流 {#edge}

Platform Edge Network是一個全球分佈、快速、可靠的伺服器網路，能夠以大規模接收和處理資料。 使用標籤時，您可以設定 [資料流](../edge/datastreams/overview.md) 針對Adobe Target、Adobe Audience Manager和Adobe Analytics等產品，這可讓您在伺服器端啟用這些產品，而不需變更用戶端代碼。

此外，資料流與多個平台功能整合，這些功能有助於確保您傳送的任何敏感資料在組織政策和法律法規方面得到適當處理。 請參閱 [處理敏感資料](../edge/datastreams/overview.md#sensitive) 如需詳細資訊，請參閱datastreams檔案。

![資料流和Adobe解決方案](./images/home/adobe-solutions.png)

>[!NOTE]
>
>有關Platform Edge Network的高級介紹，請參閱以下內容 [互動產品導覽](https://adobe-ideacloud.forgedx.com/adobe-adobe-edge-collection/adobe-experience-edge/public/mx?SUID=hgb1a48ICSCpbM6MzBYHbxnsh9DgjUy1).

## 事件轉送

[事件轉送](../tags/ui/event-forwarding/overview.md) 可點選任何Experience Platform資料流，讓您以極低的延遲轉換、擴充及傳送資料至任何非Adobe目的地，而無須將任何協力廠商程式碼新增至用戶端裝置。

![事件轉送](./images/home/event-forwarding.png)

>[!NOTE]
>
>事件轉送是付費功能，僅包含在Adobe Real-time Customer Data Platform連線產品中。

## 後續步驟

本檔案概略介紹資料收集如何運作，以自動將收集到的客戶體驗資料傳送至Adobe產品和協力廠商目的地的程式。

![資料收集框架](./images/home/collection.png)

如需透過邊緣網路傳送事件資料所涉及之一般工作流程的詳細資訊，請參閱 [端對端概述](./e2e.md).
