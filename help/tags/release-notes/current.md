---
title: 標籤和事件轉送的發行說明
description: Adobe Experience Platform 中標記和事件轉送的最新發行說明。
exl-id: 2ebeaa1e-64b8-48fd-b4e8-419663271a87
source-git-commit: e300e57df998836a8c388511b446e90499185705
workflow-type: tm+mt
source-wordcount: '771'
ht-degree: 7%

---

# 標籤和事件轉送的發行說明

>[!IMPORTANT]
>
>往前看，本頁將不再提供標籤和事件轉送發行說明。 請參閱最新的[Adobe Experience Platform發行說明](https://experienceleague.adobe.com/docs/experience-platform/release-notes/latest.html#data-collection)，以取得詳細的標籤和事件轉送更新。

## 2023年4月26日

* **OAuth JWT密碼**： [OAuth JWT密碼](https://experienceleague.adobe.com/docs/experience-platform/tags/event-forwarding/secrets.html)可讓客戶使用Adobe和Google服務權杖，在事件轉送中支援伺服器對伺服器互動。

下列新擴充功能已發行：

* **[!DNL Pinterest Conversions API]擴充功能**： [[!DNL Pinterest Conversions API]](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/pinterest/overview.html)事件轉送擴充功能可讓您運用Adobe Experience PlatformEdge Network中擷取的資料，並使用[!DNL Pinterest Conversions API]以伺服器端事件的形式將其傳送至[!DNL Pinterest]。

## 2023年3月29日

**快速Stark工作流程(Beta)**

從「資料集合」首頁畫面存取「快速入門」下全新的快速入門工作流程！以下工作流程現在可作為公用Beta供客戶使用。
* **[Meta Conversions API](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/meta/overview.html#quick-start)**：事件轉送客戶只需幾個簡單的步驟，即可快速收集並轉送事件資料、伺服器端至中繼以進行廣告轉換。
* **[行動SDK](https://developer.adobe.com/client-sdks/documentation/)**：客戶只需幾個簡單的步驟，即可快速實作Mobile SDK及驗證基本行動事件。

已發行新的擴充功能：

* **[!DNL Braze]事件轉送擴充功能**： [[!DNL Braze Track Events API]](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/braze/overview.html)事件轉送擴充功能可讓您運用Adobe Experience PlatformEdge Network中擷取的資料，並使用[!DNL Braze]使用者追蹤API，以伺服器端事件的形式將其傳送至[!DNL Braze]。
* **[Epsilon Events API]事件轉送擴充功能**： [[!DNL Epsilon Events API]](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/braze/overview.html)擴充功能可讓您運用事件轉送，擷取Adobe Experience PlatformEdge Network中的事件資訊，並使用[!DNL Epsilon]事件API傳送給[!DNL Epsilon]。
* **[!DNL Mixpanel]事件轉送擴充功能**： [[!DNL Mixpanel Track Events API]](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/braze/overview.html)擴充功能可讓您運用事件轉送，擷取Adobe Experience PlatformEdge Network中的事件資訊，並使用追蹤事件API傳送給[!DNL Mixpanel]。

## 2023年1月25日

* **新首頁**：資料收集UI的首頁已更新，包含實用的入門資訊和簡化生產力的連結。 其中包括：
   1. 入門的文件和推薦的工作流程
   1. 最近的屬性、規則和資料元素
   1. 熱門的擴充功能
   1. 附帶快速安裝功能的新擴充功能更新
* **使用事件轉送將資料傳送至[!DNL Google Ads]**：您現在可以使用[[!DNL Google Ads Enhanced Conversions] API擴充功能](../extensions/server/google-ads-enhanced-conversions/overview.md)進行事件轉送，結合[Google Oauth 2機密](../ui/event-forwarding/secrets.md#google-oauth2)，將伺服器端資料安全地即時傳送至[!DNL Google Ads]。

## 2022年11月23日

* 用於事件轉送的&#x200B;**[!DNL AWS]延伸模組**：您現在可以使用[事件轉送](../../tags/ui/event-forwarding/overview.md)延伸模組，將資料傳送至[!DNL Amazon Web Services] ([!DNL AWS])。 如需詳細資訊，請參閱[[!DNL AWS] 擴充功能概觀](../../tags/extensions/server/aws/overview.md)。
* 用於事件轉送的&#x200B;**[!DNL Google Ads Enhanced Conversions]擴充功能**：您現在可以使用[事件轉送](../../tags/ui/event-forwarding/overview.md)擴充功能，將轉換資料傳送至[!DNL Google Ads]。 如需詳細資訊，請參閱[[!DNL Google Ads Enhanced Conversions] 擴充功能概觀](../../tags/extensions/server/google-ads-enhanced-conversions/overview.md)。
* 用於事件轉送的&#x200B;**[!DNL Microsoft Azure]延伸模組**：您現在可以使用[事件轉送](../../tags/ui/event-forwarding/overview.md)延伸模組將資料傳送至[!DNL Microsoft Azure]。 如需詳細資訊，請參閱[[!DNL Microsoft Azure] 擴充功能概觀](../../tags/extensions/server/azure/overview.md)。

## 2022年10月26日

* **資料串流的敏感資料處理**：資料串流現在會運用數種平台技術，依照健康保險可攜性及責任法案(HIPAA)等法規，適當地處理敏感資料。 如需詳細資訊，請參閱[處理資料串流](../../datastreams/overview.md#sensitive)中的敏感資料一節。
* 用於事件轉送的&#x200B;**[!DNL Splunk]延伸模組**：您現在可以使用[事件轉送](../ui/event-forwarding/overview.md)延伸模組將資料傳送至[!DNL Splunk]。 如需詳細資訊，請參閱[[!DNL Splunk] 擴充功能概觀](../extensions/server/splunk/overview.md)。
* 用於事件轉送的&#x200B;**[!DNL Zendesk]延伸模組**：您現在可以使用[事件轉送](../ui/event-forwarding/overview.md)延伸模組將資料傳送至[!DNL Zendesk]。 如需詳細資訊，請參閱[[!DNL Zendesk] 擴充功能概觀](../extensions/server/zendesk/overview.md)。

## 2022年9月28日

* **Adobe Experience Platform左側導覽整合**：先前專屬至資料收集UI的所有功能（包括標籤和事件轉送）現在也可透過Experience PlatformUI中類別&#x200B;**[!UICONTROL 資料收集]**&#x200B;下的左側導覽取得。 如此一來，在Platform中使用資料收集功能時，就不需要在UI之間切換。
* **標籤和事件轉送中的使用者歸因**：在標籤和事件轉送中列出可用屬性時，每個列出的屬性現在會顯示其上次更新時間以及由誰更新。
* **[[!DNL Snap Conversions API] 擴充功能](https://exchange.adobe.com/apps/ec/108550)用於事件轉送**：您現在可以使用[事件轉送](../../tags/ui/event-forwarding/overview.md)擴充功能，將資料傳送至[!DNL Snapchat Conversions API]。 如需如何驗證及使用API的詳細資訊，請參閱[[!DNL Snapchat Marketing API] 檔案](https://marketingapi.snapchat.com/docs/conversion.html)。

## 2022 年 7 月 27 日

* 現在，您可以在Adobe Experience Platform資料收集的卡片底下，透過Adobe Admin Console管理標籤和事件轉送功能的存取權。 如需詳細資訊，請參閱[資料彙集許可權](../../collection/permissions.md)的指南。
* [已停止支援Internet Explorer 10和11](../ie-deprecation.md)。

## 2022年6月22日

已發行新的擴充功能：

* [Google資料層標籤延伸模組](../extensions/client/google-data-layer/overview.md)：可讓您在標籤實作中使用Google資料層。
* [Google Ads Enhanced Conversions事件轉送擴充功能](https://partners.adobe.com/exchangeprogram/experiencecloud/exchange.details.108630.html)：可讓您即時增強Google Ads轉換。
* [Mailchimp事件轉送擴充功能](../extensions/server/mailchimp/overview.md)：傳送事件至Mailchimp行銷API，可觸發Mailchimp行銷活動、歷程或交易的電子郵件。