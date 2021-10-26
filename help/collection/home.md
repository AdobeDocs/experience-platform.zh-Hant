---
keywords: Experience Platform；首頁；熱門主題；資料收集；啟動；Web sdk
solution: Experience Platform
title: 資料彙集概觀
topic-legacy: overview
description: 了解在Adobe Experience Platform中收集客戶體驗資料所涉及的各種技術。
exl-id: 03ce5339-e68d-4adf-8c3c-82846a626dad
source-git-commit: bbaf272313d5a8afe33178598063164792f4d8c0
workflow-type: tm+mt
source-wordcount: '357'
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
* [事件轉送](../tags/ui/event-forwarding/overview.md)
* [Adobe Experience Platform Web SDK](../edge/home.md)
* [Adobe Experience Platform Mobile SDK](https://aep-sdks.gitbook.io/docs/)
* [Adobe Experience Platform Debugger](https://chrome.google.com/webstore/detail/adobe-experience-platform/bfnnokhpnncpkdmbokanobigaccjkpob?hl=en)
* [Experience Data Model(XDM)](../xdm/home.md)
* [Adobe Experience Platform Identity Service](../identity-service/home.md)

<!-- (Outdated terminology)
![](./images/Collection.png)
-->

## 更簡單的實施，更快的用戶端效能

Adobe Experience Platform Web和Mobile SDK會折疊所有Adobe產品程式庫，並壓縮為適用於網頁或行動平台的單一開發套件。 壓縮這些程式庫可加快資料收集速度，並將操作整合為從用戶端裝置到Adobe Experience Platform邊緣網路的單一資料流。

## 切換過程以部署Adobe技術 {#edge}

Platform Edge Network是一個全球分佈、快速、可靠的伺服器網路，能夠以大規模接收和處理資料。 使用標籤時，您可以設定 [資料流](../edge/fundamentals/datastreams.md) 針對Adobe Target、Adobe Audience Manager和Adobe Analytics等產品，這可讓您在伺服器端啟用這些產品，而不需變更用戶端代碼。

<!-- (Outdated terminology)
![](./images/deploy.png)
-->

>[!NOTE]
>
>如需Platform Edge Network的概要介紹，請參閱以下內容 [互動產品導覽](https://adobe-ideacloud.forgedx.com/adobe-adobe-edge-collection/adobe-experience-edge/public/mx?SUID=hgb1a48ICSCpbM6MzBYHbxnsh9DgjUy1).

## 快速、安全地轉換、豐富和發送資料

[Adobe Experience Platform中的事件轉送](../tags/ui/event-forwarding/overview.md) 可點選任何Platform資料流。 您可以以極低的延遲轉換、擴充及傳送資料至任何非Adobe目的地，而無須將任何協力廠商代碼新增至用戶端裝置，提供更快速且安全的資料收集與發佈。

<!-- (Outdated terminology)
![](./images/launch.png)
-->