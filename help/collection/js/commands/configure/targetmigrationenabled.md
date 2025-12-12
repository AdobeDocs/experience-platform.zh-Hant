---
title: targetMigrationEnabled
description: 允許網頁SDK讀取和寫入Adobe Target Cookie。
exl-id: 4b9203c6-31b7-45af-a6a6-a206d7edac3f
source-git-commit: 051374def898d3797711525c5343e0a8454970a2
workflow-type: tm+mt
source-wordcount: '141'
ht-degree: 0%

---

# `targetMigrationEnabled`

`targetMigrationEnabled`屬性是布林值，可讓Web SDK讀取和寫入Adobe Target 1.x和2.x程式庫使用的[`mbox`和`mboxEdgeCluster` Cookie](https://experienceleague.adobe.com/zh-hant/docs/core-services/interface/data-collection/cookies/web-sdk)。 此選項可讓您保留使用先前Adobe Target實作的頁面與使用Web SDK的頁面之間的訪客設定檔。

執行`targetMigrationEnabled`命令時設定`configure`布林值。 如果您在設定Web SDK時省略此屬性，其預設值為`false`。 如果您有部分頁面仍使用Adobe Target 1.x或2.x資料庫，請將此值設為`true`。

使用此屬性時，請確定您也在Adobe Target實作的[`overrideMboxEdgeServer`中啟用](https://experienceleague.adobe.com/zh-hant/docs/target-dev/developer/client-side/at-js-implementation/functions-overview/targetglobalsettings#overridemboxedgeserver)`targetGlobalSettings()`。

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  targetMigrationEnabled: true
});
```

## 使用網頁SDK標籤擴充功能啟用Target移轉

您可以使用[Personalization組態設定](/help/tags/extensions/client/web-sdk/configure/personalization.md#migrate-target-from-atjs-to-the-web-sdk)，在網頁SDK標籤擴充功能中設定此設定。
