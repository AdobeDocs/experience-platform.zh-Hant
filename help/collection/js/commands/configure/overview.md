---
title: 設定Adobe Experience Platform Web SDK
description: 使用Web SDK時，請使用configure命令來設定必要的設定。
exl-id: 05ba98ae-c004-4b7b-b55b-38290ca62cfa
source-git-commit: db7e6df1b1a0eb19518d9c6ccd6e6bb9131d5a3e
workflow-type: tm+mt
source-wordcount: '82'
ht-degree: 0%

---

# 設定Adobe Experience Platform Web SDK

使用&#x200B;**`configure`**&#x200B;命令完成Web SDK的設定。 在您呼叫任何其他Web SDK命令（例如[`sendEvent`](../sendevent/overview.md)）之前，每個頁面載入都需要此命令。

**需要[`datastreamId`](datastreamid.md)和[`orgId`](orgid.md)屬性。**&#x200B;所有其他屬性皆為選用屬性，視您組織的實作需求而定。 下列範例顯示使用大部分可用屬性的組態物件：

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  clickCollectionEnabled: true,
  clickCollection: {
    internalLinkEnabled: true,
    downloadLinkEnabled: true,
    externalLinkEnabled: true,
    eventGroupingEnabled: true,
    filterClickDetails: function(content) {
      content.linkUrl = "https://example.com/current.html";
    },
    sessionStorageEnabled: true
  },
  context: ["web", "device", "environment", "placeContext", "highEntropyUserAgentHints"],
  debugEnabled: true,
  defaultConsent: "pending",
  downloadLinkQualifier: "\.(exe|zip|wav|mp3|mov|mpg|avi|wmv|pdf|doc|docx|xls|xlsx|ppt|pptx)$",
  edgeBasePath: "ee",
  edgeConfigOverrides: { "datastreamId": "0dada9f4-fa94-4c9c-8aaf-fdbac6c56287" },
  edgeDomain: "data.example.com",
  idMigrationEnabled: false,
  onBeforeEventSend: function(content) {
    if(content.xdm.web?.webReferrer) delete content.xdm.web.webReferrer.URL;
  },
  prehidingStyle: "#container { opacity: 0 !important }",
  targetMigrationEnabled: true,
  thirdPartyCookiesEnabled: false
});
```
