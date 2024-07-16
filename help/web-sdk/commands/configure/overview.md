---
title: 設定Adobe Experience Platform Web SDK
description: 使用Web SDK時，請使用configure命令來設定必要的設定。
exl-id: 05ba98ae-c004-4b7b-b55b-38290ca62cfa
source-git-commit: 1c614ef525d55d7476d037c6838b35c3471e4501
workflow-type: tm+mt
source-wordcount: '205'
ht-degree: 0%

---

# 設定Adobe Experience Platform Web SDK

使用`configure`命令完成Web SDK的設定。 設定Web SDK是重要且必要的步驟，必須在使用程式庫或標籤擴充功能時進行。

## 使用標籤擴充功能設定Web SDK {#configure-tag-extension}

請依照下列步驟，透過標籤擴充功能設定Web SDK。

1. 使用您的Adobe ID憑證登入[experience.adobe.com](https://experience.adobe.com)。
1. 導覽至&#x200B;**[!UICONTROL 資料彙集]** > **[!UICONTROL 標籤]**。
1. 選取所需的標籤屬性。
1. 導覽至&#x200B;**[!UICONTROL 擴充功能]**，然後按一下[!UICONTROL Adobe Experience Platform Web SDK]卡片上的&#x200B;**[!UICONTROL 設定]**。
1. 請前往[Web SDK標籤延伸設定頁面](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md)，取得所有設定選項的詳細資訊。

當您使用擴充功能傳送資料給Adobe時，就會設定這些組態設定。

## 使用JavaScript資料庫設定Web SDK {#configure-js}

執行`configure`命令。 您必須先執行此命令，才能呼叫任何其他Web SDK命令，例如[`sendEvent`](../sendevent/overview.md)。

需要[`edgeConfigId`](edgeconfigid.md)和[`orgId`](orgid.md)屬性。 所有其他屬性皆為選用，視您組織的實作需求而定。

請參閱本使用手冊的目錄，瞭解每個支援命令的詳細資訊。

```js
alloy("configure", {
  edgeConfigId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  clickCollectionEnabled: true,
  clickCollection: {
    internalLinkEnabled: true,
    downloadLinkEnabled: true,
    externalLinkEnabled: true,
    eventGroupingEnabled: true,
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
  onBeforeLinkClickSend: function(content) {
    content.xdm.web.webPageDetails.URL = "https://example.com/current.html";
  },
  prehidingStyle: "#container { opacity: 0 !important }",
  targetMigrationEnabled: true,
  thirdPartyCookiesEnabled: false
});
```
