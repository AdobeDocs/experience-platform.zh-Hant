---
title: 設定Adobe Experience Platform Web SDK
description: 使用Web SDK時，請使用configure命令來設定必要的設定。
exl-id: 05ba98ae-c004-4b7b-b55b-38290ca62cfa
source-git-commit: 58cd6300307881c3de7c52e07c401bf2ed908517
workflow-type: tm+mt
source-wordcount: '205'
ht-degree: 0%

---

# 設定Adobe Experience Platform Web SDK

Web SDK的設定可使用 `configure` 命令。 設定Web SDK是重要且必要的步驟，必須在使用程式庫或標籤擴充功能時進行。

## 使用標籤擴充功能設定Web SDK {#configure-tag-extension}

請依照下列步驟，透過標籤擴充功能設定Web SDK。

1. 登入 [experience.adobe.com](https://experience.adobe.com) 使用您的Adobe ID憑證。
1. 瀏覽至 **[!UICONTROL 資料彙集]** > **[!UICONTROL 標籤]**.
1. 選取所需的標籤屬性。
1. 瀏覽至 **[!UICONTROL 擴充功能]**，然後按一下 **[!UICONTROL 設定]** 於 [!UICONTROL Adobe Experience Platform Web SDK] 卡片。
1. 前往 [Web SDK標籤擴充功能設定頁面](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md) 以取得所有組態選項的詳細資訊。

當您使用擴充功能傳送資料給Adobe時，就會設定這些組態設定。

## 使用JavaScript程式庫設定Web SDK {#configure-js}

執行 `configure` 命令。 此指令是呼叫任何其他Web SDK指令(例如 [`sendEvent`](../sendevent/overview.md).

此 [`edgeConfigId`](edgeconfigid.md) 和 [`orgId`](orgid.md) 屬性為必要項。 所有其他屬性皆為選用，視您組織的實作需求而定。

請參閱本使用手冊的目錄，瞭解每個支援命令的詳細資訊。

```js
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "clickCollectionEnabled": false,
  "context": ["web", "device", "environment", "placeContext", "highEntropyUserAgentHints"],
  "debugEnabled": true,
  "defaultConsent": "pending",
  "downloadLinkQualifier": "\.(exe|zip|wav|mp3|mov|mpg|avi|wmv|pdf|doc|docx|xls|xlsx|ppt|pptx)$",
  "edgeBasePath": "ee",
  "edgeConfigOverrides": { "datastreamId": "0dada9f4-fa94-4c9c-8aaf-fdbac6c56287" },
  "edgeDomain": "data.example.com",
  "idMigrationEnabled": false,
  "onBeforeEventSend": function(content) {
    if(content.xdm.web?.webReferrer) delete content.xdm.web.webReferrer.URL;
  },
  "onBeforeLinkClickSend": function(content) {
    content.xdm.web.webPageDetails.URL = "https://example.com/current.html";
  },
  "prehidingStyle": "#container { opacity: 0 !important }",
  "targetMigrationEnabled": true,
  "thirdPartyCookiesEnabled": false
});
```
