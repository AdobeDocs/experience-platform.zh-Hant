---
title: 標籤和事件轉發的發行說明
description: Adobe Experience Platform 中標記和事件轉送的最新發行說明。
exl-id: 2ebeaa1e-64b8-48fd-b4e8-419663271a87
source-git-commit: c7f09da40d2ea84de6f21669bdda16c0175a63c1
workflow-type: tm+mt
source-wordcount: '798'
ht-degree: 3%

---

# 標籤和事件轉發的發行說明

## 2023 年 4 月 26 日

* **OAuth JWT密碼**:的 [OAuth JWT密碼](https://experienceleague.adobe.com/docs/experience-platform/tags/event-forwarding/secrets.html?lang=en) 允許客戶使用Adobe和Google服務令牌支援事件轉發中的伺服器到伺服器交互。

已發佈以下新擴展：

* **[!DNL Pinterest Conversions API]擴展**:的 [[!DNL Pinterest Conversions API]](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/pinterest/overview.html) 事件轉發擴展允許您利用在Adobe Experience Platform邊緣網路中捕獲的資料並將其發送到 [!DNL Pinterest] 以伺服器端事件的形式使用 [!DNL Pinterest Conversions API]。

## 2023 年 3 月 29 日

**快速Stark工作流(Beta)**

從「資料收集」主螢幕訪問「入門」下的新快速啟動工作流！ 以下工作流現在作為公共測試版提供給客戶。
* **[元轉換API](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/meta/overview.html?lang=en#quick-start)**:事件轉發客戶只需幾個簡單的步驟即可快速收集和轉發事件資料，從伺服器端到Meta進行廣告轉換。
* **[移動SDK](https://developer.adobe.com/client-sdks/documentation/)**:客戶只需幾個簡單的步驟即可快速實施移動軟體開發工具包並驗證基本移動事件。

已發佈新擴展：

* **[!DNL Braze]事件轉發擴展**:的 [[!DNL Braze Track Events API]](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/braze/overview.html) 事件轉發擴展允許您利用在Adobe Experience Platform邊緣網路中捕獲的資料並將其發送到 [!DNL Braze] 以伺服器端事件的形式使用 [!DNL Braze] 用戶跟蹤API。
* **[Epsilon事件API] 事件轉發擴展**:的 [[!DNL Epsilon Events API]](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/braze/overview.html) 擴展允許您利用事件轉發來捕獲Adobe Experience Platform邊緣網路中的事件資訊並將其發送到 [!DNL Epsilon] 使用 [!DNL Epsilon] 事件API。
* **[!DNL Mixpanel]事件轉發擴展**:的 [[!DNL Mixpanel Track Events API]](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/braze/overview.html) 擴展允許您利用事件轉發來捕獲Adobe Experience Platform邊緣網路中的事件資訊並將其發送到 [!DNL Mixpanel] 使用跟蹤事件API。

## 2023 年 1 月 25 日

* **新建主螢幕**:資料收集UI的首頁已更新，以包含有助於提高工作效率的入門資訊和連結。 其中包括:
   1. 要開始的文檔和建議的工作流
   1. 最近的屬性、規則和資料元素
   1. 常用擴展
   1. 具有快速安裝功能的新擴展更新
* **將資料發送到 [!DNL Google Ads] 使用事件轉發**:您現在可以使用 [[!DNL Google Ads Enhanced Conversions] API擴展](../extensions/server/google-ads-enhanced-conversions/overview.md) 用於事件轉發，與 [GoogleOauth 2機密](../ui/event-forwarding/secrets.md#google-oauth2)，將伺服器端資料安全地發送到 [!DNL Google Ads] 即時。

## 2022 年 11 月 23 日

* **[!DNL AWS]事件轉發擴展**:您現在可以將資料發送到 [!DNL Amazon Web Services] ([!DNL AWS])使用 [事件轉發](../../tags/ui/event-forwarding/overview.md) 擴展。 查看 [[!DNL AWS] 擴展概述](../../tags/extensions/server/aws/overview.md) 的子菜單。
* **[!DNL Google Ads Enhanced Conversions]事件轉發擴展**:您現在可以將轉換資料發送到 [!DNL Google Ads] 使用 [事件轉發](../../tags/ui/event-forwarding/overview.md) 擴展。 查看 [[!DNL Google Ads Enhanced Conversions] 擴展概述](../../tags/extensions/server/google-ads-enhanced-conversions/overview.md) 的子菜單。
* **[!DNL Microsoft Azure]事件轉發擴展**:您現在可以將資料發送到 [!DNL Microsoft Azure] 使用 [事件轉發](../../tags/ui/event-forwarding/overview.md) 擴展。 查看 [[!DNL Microsoft Azure] 擴展概述](../../tags/extensions/server/azure/overview.md) 的子菜單。

## 2022 年 10 月 26 日

* **資料流的敏感資料處理**:Datastreams現在利用多種平台技術來適當地處理由健康保險流通和責任法案(HIPAA)等法規強制實施的敏感資料。 請參閱 [處理資料流中的敏感資料](../../edge/datastreams/overview.md#sensitive) 的子菜單。
* **[!DNL Splunk]事件轉發擴展**:您現在可以將資料發送到 [!DNL Splunk] 使用 [事件轉發](../ui/event-forwarding/overview.md) 擴展。 查看 [[!DNL Splunk] 擴展概述](../extensions/server/splunk/overview.md) 的子菜單。
* **[!DNL Zendesk]事件轉發擴展**:您現在可以將資料發送到 [!DNL Zendesk] 使用 [事件轉發](../ui/event-forwarding/overview.md) 擴展。 查看 [[!DNL Zendesk] 擴展概述](../extensions/server/zendesk/overview.md) 的子菜單。

## 2022 年 9 月 28 日

* **Adobe Experience Platform左導航**:以前只有資料收集UI（包括標籤和事件轉發）的所有功能現在也可通過Experience PlatformUI的左導航（位於類別下）獲得 **[!UICONTROL 資料收集]**。 這樣，在平台中使用資料收集功能時，無需在UI之間切換。
* **標籤和事件轉發中的用戶屬性**:當在標籤和事件轉發中列出可用屬性時，每個列出的屬性現在都會顯示上次更新時間和更新者。
* **[[!DNL Snap Conversions API] 擴展](https://exchange.adobe.com/apps/ec/108550) 用於事件轉發**:您現在可以將資料發送到 [!DNL Snapchat Conversions API] 使用 [事件轉發](../../tags/ui/event-forwarding/overview.md) 擴展。 有關如何驗證和使用API的詳細資訊，請參閱 [[!DNL Snapchat Marketing API] 文檔](https://marketingapi.snapchat.com/docs/conversion.html)。

## 2022 年 7 月 27 日

* 現在，對標籤和事件轉發功能的訪問通過Adobe Admin Console管理，Adobe Experience Platform資料收集卡下。 請參閱上的指南 [資料收集權限](../../collection/permissions.md) 的子菜單。
* 已支援Internet Explorer 10和11 [棄用](../ie-deprecation.md)。

## 2022 年 6 月 22 日

已發佈新擴展：

* [Google資料層標籤擴展](../extensions/client/google-data-layer/overview.md):允許您在標籤實現中使用Google資料層。
* [Google廣告增強轉換事件轉發擴展](https://partners.adobe.com/exchangeprogram/experiencecloud/exchange.details.108630.html):允許您即時增強Google廣告的轉換。
* [Mailchimp事件轉發擴展](../extensions/server/mailchimp/overview.md):將事件發送到Mailchimp Marketing API，該API可觸發Mailchimp營銷活動、行程或交易的電子郵件。