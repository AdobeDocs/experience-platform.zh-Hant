---
title: 從 Audience Manager 到 Real-Time CDP 的進化
description: 瞭解規劃從Audience Manager移轉至Adobe Real-Time CDP之前的考量事項。
exl-id: 83ab9a5d-9abc-4072-b449-e2a9ecd48639
source-git-commit: bb90bbddf33bc4b0557026a0f34965ac37475c65
workflow-type: tm+mt
source-wordcount: '475'
ht-degree: 67%

---

# 從 Audience Manager 到 Real-Time CDP 的進化

由於您的組織進化為使用 Adobe Real-Time CDP，需探索這些考量事項以準備您的資料，並了解這兩種技術之間關鍵性的差異。本文內容主要以從業人員為客群。

![Audience Manager 到 Real-Time CDP 的進化圖表](/help/rtcdp/assets/aam-to-rtcdp-evolution.png)

## &#x200B;1. 考慮 Audience Manager 中的資料架構

由於您考慮從 Audience Manager 進化到 Real-Time CDP，現在是分析您的 [Audience Manager 區段](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/segments/segments-purpose.html)並確定構成這些區段的是哪些[訊號](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/data-explorer/data-explorer-understanding-signals.html)、[特徵](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/traits/trait-details-page.html)和[規則](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/segments/segment-builder.html#segment-builder-section)的關鍵性時刻。

此外，需考慮您目前在 Audience Manager 中使用的資料來源。

Adobe 建議您依照下列方式將區段分類：

* 可以透過[[!UICONTROL Audience Manager Source Connector]](/help/sources/connectors/adobe-applications/audience-manager.md)傳送至Experience Platform的區段，因為它們沒有資料相依性、沒有目的地或啟用挑戰，而且其區段規則稍後可以透過Real-Time CDP [區段產生器](/help/segmentation/ui/segment-builder.md)建立。
* 區段具有可受支援的規則但可能包含無法在 Real-Time CDP 中取得的資料。
* 無法在Real-Time CDP中建立且缺少功能的區段。

>[!TIP]
>
>Adobe Real-Time CDP提供[三種型別的區段評估](/help/segmentation/home.md#evaluate-segments)： [!UICONTROL Batch]、[!UICONTROL Streaming]和[!UICONTROL Edge]。 在 Audience Manager 中使用即時區段的客戶可能會受到 Real-Time CDP 中目前 500 個串流區段的限制。若要了解詳細資訊，請閱讀[分段護欄](/help/profile/guardrails.md)。

## 2.哪些區段是透過[!UICONTROL Audience Manager Source Connector]傳送的關鍵？

根據其評估標準，沒有資料相依性、沒有目的地或啟動挑戰，且其分段規則可在之後的日期透過 [Adobe Experience Platform Web SDK](/help/collection/js/faq.md) 之類的 Real-Time CDP 資料集合建立的區段應透過 Audience Manager 來源連接器傳送。

## 3.您是否會使用[!UICONTROL Experience Cloud Audiences]目的地將資料帶回Audience Manager？

具有在 Real-Time CDP 中可受支援的規則但對 Audience Manager 具有啟動相依性的區段可以透過 [Experience Cloud 對象](/help/destinations/catalog/adobe/experience-cloud-audiences.md)目的地卡傳送至 Audience Manager。

## &#x200B;4. 現在您在 Audience Manager 中已有哪些目的地可以開始移動到 Real-Time CDP？

Adobe強烈建議Audience Manager中啟用至[以人物為基礎的目的地](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/destinations/people-based/people-based-destinations-overview.html)的區段，要透過[!UICONTROL Audience Manager Source Connector]推送至Real-Time CDP，然後透過Real-Time CDP啟用。

Audience Manager中可用的所有以人物為基礎的目的地 — [Facebook](/help/destinations/catalog/social/facebook.md)、[[!UICONTROL Google Customer Match]](/help/destinations/catalog/advertising/google-customer-match.md)、[LinkedIn](/help/destinations/catalog/social/linkedin.md) — 也可在Real-Time CDP中取得。

提供其他第一方資料和媒體策略合作夥伴，例如[Pinterest](/help/destinations/catalog/advertising/pinterest.md)、[Snapchat](/help/destinations/catalog/advertising/snap-inc.md)、[TikTok](/help/destinations/catalog/social/tiktok.md)、[Amazon Ads](/help/destinations/catalog/advertising/amazon-ads.md)和[[!UICONTROL The Trade Desk]](/help/destinations/catalog/advertising/tradedesk.md)。

Real-Time CDP 目前支援[目錄](/help/destinations/catalog/overview.md)中超過 60 個原生目的地，其中有 20 個以上屬於支援第一方客群媒合的廣告或社群目的地。

## 後續步驟

詳閱本頁面後，當您要開始從 Audience Manager 進化至 Real-Time CDP 時，立刻就有第一組需解決的注意事項。
