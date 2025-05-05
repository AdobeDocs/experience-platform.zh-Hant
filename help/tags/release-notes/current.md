---
title: 標記和事件轉送的發行說明
description: Adobe Experience Platform 中標記和事件轉送的最新發行說明。
exl-id: 2ebeaa1e-64b8-48fd-b4e8-419663271a87
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '773'
ht-degree: 93%

---

# 標記和事件轉送的發行說明

>[!IMPORTANT]
>
>今後，此頁面將不再提供標記和事件轉送發行說明。請參閱最新的 [Adobe Experience Platform 發行說明](https://experienceleague.adobe.com/docs/experience-platform/release-notes/latest.html?lang=zh-Hant#data-collection)，了解標記和事件轉送的更新詳情。

## 2023 年 4 月 26 日

* **OAuth JWT Secret**：[OAuth JWT Secret](https://experienceleague.adobe.com/docs/experience-platform/tags/event-forwarding/secrets.html?lang=zh-Hant) 可讓客戶使用 Adob&#x200B;&#x200B;e 和 Google 服務權杖支援「事件轉送」中伺服器和伺服器的互動。

以下新擴充功能已發佈：

* **[!DNL Pinterest Conversions API]擴充功能**：[[!DNL Pinterest Conversions API]](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/pinterest/overview.html?lang=zh-Hant) 事件轉送擴充功能可讓您利用在 Adob&#x200B;&#x200B;e Experience Platform Edge Network 中擷取的資料並將其傳送到 [!DNL Pinterest] (使用 [!DNL Pinterest Conversions API] 並以伺服器端事件的形式)。

## 2023 年 3 月 29 日

**Quick Stark 工作流程 (Beta 版)**

從「資料集合」首頁畫面存取「快速入門」下全新的快速入門工作流程！以下工作流程現已作為公共 Beta 版提供給客戶。
* **[Meta Conversions API](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/meta/overview.html?lang=zh-Hant#quick-start)**：事件轉送客戶可快速收集並轉送事件資料，並將其從伺服器端轉送到 Meta，僅需幾個簡單步驟即可實現廣告轉換。
* **[行動 SDK](https://developer.adobe.com/client-sdks/documentation/)**：客戶只需幾個簡單的步驟即可快速實施行動 SDK 並驗證基本行動事件。

新擴充功能已發佈：

* **[!DNL Braze]事件轉送擴充功能**：[[!DNL Braze Track Events API]](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/braze/overview.html?lang=zh-Hant)事件轉送擴充功能可讓您利用在 Adob&#x200B;&#x200B;e Experience Platform Edge Network 中擷取的資料並將其傳送到 [!DNL Braze] (使用 [!DNL Braze] User Track API 並以伺服器端事件的形式)。
* **[Epsilon 事件 API] 事件轉送擴充功能**：[[!DNL Epsilon Events API]](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/braze/overview.html?lang=zh-Hant) 擴充功能可讓您利用事件轉送在 Adob&#x200B;&#x200B;e Experience Platform Edge Network 中擷取事件資訊並將其傳送到 [!DNL Epsilon] (使用 [!DNL Epsilon] Event API)。
* **[!DNL Mixpanel]事件擴充功能**：[[!DNL Mixpanel Track Events API]](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/braze/overview.html?lang=zh-Hant) 擴充功能可讓客戶利用事件轉送在 Adob&#x200B;&#x200B;e Experience Platform Edge Network 中擷取事件資訊並使用 Track Events API 將其傳送到 [!DNL Mixpanel]。

## 2023 年 1 月 25 日

* **新的主畫面**：資料集合 UI 的首頁已更新，包含實用的入門資訊和連結以提高工作效率。其中包括：
   1. 入門的文件和推薦的工作流程
   1. 最近的屬性、規則和資料元素
   1. 熱門的擴充功能
   1. 附帶快速安裝功能的新擴充功能更新
* **使用事件轉送將資料發送至 [!DNL Google Ads]**：您現在可以使用適用於事件轉送的 [[!DNL Google Ads Enhanced Conversions] API 擴充功能](../extensions/server/google-ads-enhanced-conversions/overview.md)，和 [Google Oauth 2 密碼](../ui/event-forwarding/secrets.md#google-oauth2)結合，即時將伺服器端資料安全地傳送到 [!DNL Google Ads]。

## 2022 年 11 月 23 日

* 事件轉送的 **[!DNL AWS]擴充功能**：您現在可以使用[事件轉送](../../tags/ui/event-forwarding/overview.md)擴充功能將資料傳送至 [!DNL Amazon Web Services] ([!DNL AWS])。如需詳細資訊，請參閱[[!DNL AWS] 擴充功能概觀](../../tags/extensions/server/aws/overview.md)。
* 事件轉送的 **[!DNL Google Ads Enhanced Conversions]擴充功能**：您現在可以使用[事件轉送](../../tags/ui/event-forwarding/overview.md)擴充功能將轉換資料傳送至 [!DNL Google Ads]。如需詳細資訊，請參閱[[!DNL Google Ads Enhanced Conversions] 擴充功能概觀](../../tags/extensions/server/google-ads-enhanced-conversions/overview.md)。
* 事件轉送的 **[!DNL Microsoft Azure]擴充功能**：您現在可以使用[事件轉送](../../tags/ui/event-forwarding/overview.md)擴充功能將資料傳送至 [!DNL Microsoft Azure]。如需詳細資訊，請參閱[[!DNL Microsoft Azure] 擴充功能概觀](../../tags/extensions/server/azure/overview.md)。

## 2022 年 10 月 26 日

* **資料串流的敏感資料處理**：資料串流現在會運用數種Experience Platform技術，依照健康保險可攜性及責任法案(HIPAA)等法規的強制執行，適當地處理敏感資料。 請參閱有關[處理資料流中的敏感資料](../../datastreams/overview.md#sensitive)部份，了解更多資訊。
* 事件轉送的 **[!DNL Splunk]擴充功能**：您現在可以使用[事件轉送](../ui/event-forwarding/overview.md)擴充功能將資料傳送至 [!DNL Splunk]。如需詳細資訊，請參閱[[!DNL Splunk] 擴充功能概觀](../extensions/server/splunk/overview.md)。
* 事件轉送的 **[!DNL Zendesk]擴充功能**：您現在可以使用[事件轉送](../ui/event-forwarding/overview.md)擴充功能將資料傳送至 [!DNL Zendesk]。如需詳細資訊，請參閱[[!DNL Zendesk] 擴充功能概觀](../extensions/server/zendesk/overview.md)。

## 2022 年 9 月 28 日

* **Adobe Experience Platform 左側導覽列整合**：以前資料彙集 UI 專有的所有功能 (包括標記和事件轉送) 現在也可以透過 Experience Platform UI 中的左側導覽列 (在&#x200B;**[!UICONTROL 數據彙集]**&#x200B;類別下) 使用。如此一來，在Experience Platform中使用資料收集功能時，便不需要在UI之間切換。
* **標記和事件轉送中的使用者屬性**：在標記和事件轉送中列出可用屬性時，每個列出的屬性現在都會顯示上次更新的時間和更新者。
* 事件轉送的 **[[!DNL Snap Conversions API] 擴充功能](https://exchange.adobe.com/apps/ec/108550)**：您現在可以使用[事件轉送](../../tags/ui/event-forwarding/overview.md)擴充功能將資料傳送至 [!DNL Snapchat Conversions API]。若要了解更多如何驗證和使用此 API，請參閱[[!DNL Snapchat Marketing API] 文件](https://marketingapi.snapchat.com/docs/conversion.html)。

## 2022 年 7 月 27 日

* 存取標記和事件轉送功能現在可透過 Adob&#x200B;&#x200B;e Admin Console (在 Adob&#x200B;&#x200B;e Experience Platform 資料彙集卡下) 進行管理。請參閱關於[資料彙集權限](../../collection/permissions.md)的指南，了解更多。
* 關於 Internet Explorer 10 和 11 的支援已[不再使用](../ie-deprecation.md)。

## 2022 年 6 月 22 日

新擴充功能已發佈：

* [Google 資料層標記擴充功能](../extensions/client/google-data-layer/overview.md)：允許您在標記實施中使用 Google 資料層。
* [Google Ads 增強的轉換相關事件轉送擴充功能](https://partners.adobe.com/exchangeprogram/experiencecloud/exchange.details.108630.html)：允許您即時增強 Google Ads 轉換。
* [Mailchimp 事件轉送擴充功能](../extensions/server/mailchimp/overview.md)：將事件傳送到 Mailchimp Marketing API，這可以觸發 Mailchimp 行銷活動、歷程或交易的電子郵件。