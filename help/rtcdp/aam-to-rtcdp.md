---
title: 從Audience Manager演變至Real-Time CDP
description: 瞭解規劃從Audience Manager移轉至Real-Time CDP之前的考量事項。
source-git-commit: 147e95cce203933d591fc807d9d20bcbc06e68e3
workflow-type: tm+mt
source-wordcount: '538'
ht-degree: 0%

---


# 從Audience Manager演變至Real-Time CDP

隨著您的組織發展為使用Adobe Real-Time CDP，請探索這些考量事項以準備您的資料，並瞭解這兩種技術之間的關鍵差異。 本文內容主要針對從業者對象。

![Real-Time CDP演化圖Audience Manager](/help/rtcdp/assets/aam-to-rtcdp-evolution.png)

## 1.考慮Audience Manager中的資料架構

思考從Audience Manager到Real-Time CDP的演變，現在是分析您的產品的重要時刻。 [Audience Manager區段](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/segments/segments-purpose.html?lang=en) 並決定 [訊號](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/data-explorer/data-explorer-understanding-signals.html?lang=en)， [特徵](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/traits/trait-details-page.html?lang=en)、和 [規則](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/segments/segment-builder.html?lang=en#segment-builder-section) 這些區段是由哪些URL組成。

此外，請思考您目前在Audience Manager中使用的資料來源。

Adobe建議您依照下列方式將區段分類：

* 可透過傳送至Experience Platform的區段 [[!UICONTROL Audience Manager來源聯結器]](/help/sources/connectors/adobe-applications/audience-manager.md)，因為它們沒有資料相依性、沒有目的地或啟動挑戰，而且其細分規則可透過Real-time CDP建立 [區段產生器](/help/segmentation/ui/segment-builder.md) 稍後。
* 區段內有可支援的規則，但可能包含Real-Time CDP中無法提供的資料。
* 無法在Real-time CDP中建立且缺少功能的區段。

>[!TIP]
>
>Adobe Real-Time CDP優惠方案 [三種型別的區段評估](/help/segmentation/home.md#evaluate-segments)： [!UICONTROL 批次]， [!UICONTROL 串流]、和 [!UICONTROL Edge]. 在Audience Manager中使用即時區段的客戶，可能會受到Real-Time CDP中500個串流區段的目前限制所限制。 深入瞭解 [分段護欄](/help/profile/guardrails.md).

## 2.要透過傳送哪些區段至關重要 [!UICONTROL Audience Manager來源聯結器]？

根據評估標準，沒有資料相依性、沒有目的地或啟動挑戰的區段，以及區段規則，可透過Real-Time CDP資料收集建立，例如 [Adobe Experience Platform Web SDK](/help/edge/web-sdk-faq.md) 之後應透過Audience Manager來源聯結器傳送。

## 3.您是否會使用 [!UICONTROL Experience Cloud對象] 要將資料帶回Audience Manager的目的地？

區段如果具有Real-Time CDP可支援的規則，但具有Audience ManagerAudience Manager的啟動相依性，則可透過 [Experience Cloud對象](/help/destinations/catalog/adobe/experience-cloud-audiences.md) 目的地卡片。

## 4.您目前已有哪些目的地的Audience Manager可以開始移至Real-Time CDP？

Adobe強烈建議在Audience Manager中啟用的區段 [以人物為基礎的目的地](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/destinations/people-based/people-based-destinations-overview.html?lang=en) 透過「 」推送至Real-Time CDP [!UICONTROL Audience Manager來源聯結器]，然後透過Real-Time CDP啟用。

Audience Manager中提供的所有以人物為基礎的目的地 —  [facebook](/help/destinations/catalog/social/facebook.md)， [[!UICONTROL Google Customer Match]](/help/destinations/catalog/advertising/google-customer-match.md)， [linkedIn](/help/destinations/catalog/social/linkedin.md)  — 也可在Real-Time CDP中使用。

其他第一方資料和媒體策略合作夥伴，例如 [pinterest](/help/destinations/catalog/advertising/pinterest.md)， [Snapchat](/help/destinations/catalog/advertising/snap-inc.md)， [TikTok](/help/destinations/catalog/social/tiktok.md)， [Amazon Ads](/help/destinations/catalog/advertising/amazon-ads.md)、和 [[!UICONTROL 交易台]](/help/destinations/catalog/advertising/tradedesk.md) 可用。

Real-Time CDP目前原生支援中超過60個目的地 [目錄](/help/destinations/catalog/overview.md)，其中超過20個為支援第一方對象比對的廣告或社交目的地。

## 後續步驟

閱讀本頁後，當您開始從Audience Manager演變到Real-Time CDP時，首先要考慮的事項。
