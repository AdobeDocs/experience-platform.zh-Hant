---
title: 使用純Javascript快速入門
seo-title: 'Adobe Experience Platform Web SDK快速入門 '
description: 使用Experience Platform Web SDK收集資料的快速入門手冊
seo-description: 使用Experience Platform Web SDK收集資料的快速入門手冊
keywords: 1st-party domain;CNAME;schema;create schema;configuration id;configuration tool;data element;create data element;XDM Object;sendEvent;send Event;install sdk;install web sdk;configure;configure web sdk;
translation-type: tm+mt
source-git-commit: 8c256b010d5540ea0872fa7e660f71f2903bfb04
workflow-type: tm+mt
source-wordcount: '517'
ht-degree: 5%

---


# 歡迎

本指南會引導您以不同的方式來設定Adobe Experience Platform Web SDK。 若要使用此功能，您必須加入白名單。 如果您想要加入等候清單，請聯絡您的CSM。

- 啟用 [第一方網域(CNAME)](https://docs.adobe.com/content/help/zh-Hant/core-services/interface/ec-cookies/cookies-first-party.html) 。 如果您已有Analytics的CNAME，則應使用該CNAME。 在開發中進行測試沒有CNAME，但您在開始生產之前需要CNAME。
- 取得Adobe Experience Platform的權益。  如果您尚未購買Platform,Adobe將提供您Experience Platform Data Services Foundation，讓您以有限方式與SDK搭配使用，不需額外付費。
- 使用最新版的訪客ID服務。

## 準備架構

將 [!DNL Experience Platform Edge Network] 資料視為XDM。 XDM是一種資料格式，可讓您定義結構描述。 架構定義資料 [!DNL Edge Network] 的格式化方式。 若要傳送資料，您必須定義您的架構。

- [建立架構](../../xdm/tutorials/create-schema-ui.md)
- 將Adobe Experience Platform混合新 [!DNL Web SDK] 增至您建立的架構

以下視訊旨在支援您建立資料的架構、資料集和串流來源連 [!DNL Web SDK] 接器。

>[!VIDEO](https://video.tv.adobe.com/v/35395?quality=12&learn=on)

## 建立設定ID

您可以使用Adobe Launch中的 [Edge設定工具](../fundamentals/edge-configuration.md) ，建立設定ID，即使您未使用標籤管理功能亦然。 這可讓您將資料 [!DNL Edge Network] 傳送至各種解決方案。 如需如何尋找每個選項的詳細資訊，請參閱「 [Edge Configuration Tool](../fundamentals/edge-configuration.md) 」（邊緣設定工具）頁面。

>[!NOTE]
>
>您的組織必須位於功能的允許清單中。 請連絡您的CSM以列入允許清單。

## 安裝SDK

若要安裝SDK，請盡可能將下列「基本程式碼」複製並貼在HTML `<head>` 的標籤中：

```markup
<script>
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n[o].q.push([i,l,u])})},n[o].q=[])})}
  (window,["alloy"]);
</script>
<script src="https://cdn1.adoberesources.net/alloy/1.0.0/alloy.min.js" async></script>
```

如需執行此動作之不同選項的詳細資訊，請參 [閱安裝SDK](../fundamentals/installing-the-sdk.md)。

## 設定SDK

接著，將您的設定提供至SDK。 這是使用命令完 `configure` 成的。 這應該是每個頁面上呼叫的第一個命令。

```javascript
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93:dev",
  "orgId":"ADB3LETTERSANDNUMBERS@AdobeOrg"
});
```

您可在此處提供您在上方建立的組態ID，以及您的組織ID。 這是唯二的必填欄位。 不過，還有許多其他 [配置選項](../fundamentals/configuring-the-sdk.md)。

## 傳送事件

呼叫configure命令後，您就可以開始追蹤事件。

```javascript
alloy("sendEvent", {});
```

通常，您會傳送包含某些資料的事件。 您可以像這樣傳送XDM資料。 您傳送的資料必須位於您在XDM中建立的架構中。

```javascript
alloy("sendEvent", {
  "xdm": {
    "web":{
      "webPageDetails":{
        "name":"Home Page"
      }
    }
  }
});
```

如需追蹤事件的詳細資訊，請參閱追 [蹤事件](../fundamentals/tracking-events.md)。

## 後續步驟

在資料流動後，您可以執行下列動作：

- [建立您的架構](https://docs.adobe.com/content/help/zh-Hant/experience-platform/xdm/schema/composition.html)
- [瞭解除錯](../fundamentals/debugging.md)
- 瞭解如何個 [人化體驗](../fundamentals/rendering-personalization-content.md)
- 瞭解如何將資料傳送至多個解決方案
   - [Adobe Analytics](../solution-specific/analytics/analytics-overview.md)
   - [Adobe Audience Manager](../solution-specific/audience-manager/audience-manager-overview.md)
   - [Adobe Target](../solution-specific/target/target-overview.md)
