---
title: Launch快速入門
seo-title: Launch讓您快速入門Adobe Experience Platform Web SDK
description: 使用Experience Platform Web SDK擴充功能收集資料的快速入門手冊
seo-description: 使用Experience Platform Web SDK擴充功能收集資料的快速入門手冊
translation-type: tm+mt
source-git-commit: e23b0ce9c20d5d2d770d1c1261fe08de5743325a

---


# （測試版）必要條件

>[!IMPORTANT]
>
>Adobe Experience Platform Web SDK目前為測試版，並非所有使用者都能使用。 文件和功能可能會有所變更。

目前Adobe Experience Platform Web SDK僅支援使用XDM將資料傳送至Adobe Experience Platform。 您必須符合下列必要條件。

- 啟用 [第一方網域(CNAME)](https://docs.adobe.com/content/help/zh-Hant/core-services/interface/ec-cookies/cookies-first-party.html) 。 如果您已有Analytics的CNAME，則應使用該CNAME。
- 有權使用Adobe Experience Platform
- 正在使用最新版的訪客ID服務

## 準備平台

若要能夠傳送資料至Adobe Experience Platform，您必須建立XDM架構和使用該架構的資料集。

- [使用下列混音](../../xdm/tutorials/create-schema-ui.md) ，建立結構：
   - ExperienceEvent實作詳細資訊
   - ExperienceEvent環境詳細資訊
   - ExperienceEvent Web詳細資訊
- 將Adobe Experience Platform Web SDK mixin新增至您建立的架構
- [使用您的方案](https://platform.adobe.com/dataset/overview) ，建立資料集，讓資料著陸

## 建立設定ID

您可以在啟動時使用邊配置工 [具來建立配置](../fundamentals/edge-configuration.md) ID。

>注意： 您的組織必須列入功能白名單。 請連絡您的CSM以取得最終白名單。

## 在Launch中安裝SDK

登入啟動並安裝擴充 `AEP Web SDK` 功能。 在安裝SDK時，將會提示您設定擴充功能。 輸入上述請求的配置ID。 擴充功能會自動填入您的組織ID。

如需不同設定選項的詳細資訊，請參 [閱設定SDK](../fundamentals/configuring-the-sdk.md)。

## 傳送事件

安裝擴充功能後，從AEP Web SDK擴充功能新增「傳送信標」動作，開始傳送事件。 建議您在每次載入頁面時至少傳送一個事件，並勾選「在檢視開始時發生」選項。

如需追蹤事件的詳細資訊，請參閱追 [蹤事件](../fundamentals/tracking-events.md)。

## 傳送資料

您可以傳送符合您先前建立之結構的資料以及您的事件。 例如，如果您擁有商務網站並將商務混合新增至您的架構，當有人檢視產品時，您會傳送下列結構。

```javascript
{
  "commerce": {
    "productListAdds": {
        "value":1
    }
  },
  "productListItems":{
      "name":"Floppy Green Hat",
      "SKU":"HATFLP123",
      "product":"1234567",
      "quantity":2
  }
}
```
