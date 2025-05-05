---
title: 從 Audience Manager 到 Real-Time CDP 的進化
description: 瞭解規劃從Audience Manager移轉至Adobe Real-Time CDP之前的考量事項。
exl-id: 83ab9a5d-9abc-4072-b449-e2a9ecd48639
source-git-commit: 2704184446f7945c744e7e2d2a8c3cda3fc12527
workflow-type: tm+mt
source-wordcount: '499'
ht-degree: 86%

---

# 從 Audience Manager 到 Real-Time CDP 的進化

由於您的組織進化為使用 Adobe Real-Time CDP，需探索這些考量事項以準備您的資料，並了解這兩種技術之間關鍵性的差異。本文內容主要以從業人員為客群。

![Audience Manager 到 Real-Time CDP 的進化圖表](/help/rtcdp/assets/aam-to-rtcdp-evolution.png)

## 1. 考慮 Audience Manager 中的資料架構

由於您考慮從 Audience Manager 進化到 Real-Time CDP，現在是分析您的 [Audience Manager 區段](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/segments/segments-purpose.html?lang=zh-Hant)並確定構成這些區段的是哪些[訊號](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/data-explorer/data-explorer-understanding-signals.html?lang=zh-Hant)、[特徵](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/traits/trait-details-page.html?lang=zh-Hant)和[規則](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/segments/segment-builder.html?lang=zh-Hant#segment-builder-section)的關鍵性時刻。

此外，需考慮您目前在 Audience Manager 中使用的資料來源。

Adobe 建議您依照下列方式將區段分類：

* 可透過[[!UICONTROL Audience ManagerSource Connector]](/help/sources/connectors/adobe-applications/audience-manager.md)傳送至Experience Platform的區段，因為它們沒有資料相依性、沒有目的地或啟用挑戰，而且其區段規則稍後可透過Real-Time CDP [區段產生器](/help/segmentation/ui/segment-builder.md)建立。
* 區段具有可受支援的規則但可能包含無法在 Real-Time CDP 中取得的資料。
* 無法在Real-Time CDP中建立且缺少功能的區段。

>[!TIP]
>
>Adobe Real-Time CDP 可提供[三種類型的區段評估](/help/segmentation/home.md#evaluate-segments)：[!UICONTROL 批次]、[!UICONTROL 串流]和[!UICONTROL 邊緣]。在 Audience Manager 中使用即時區段的客戶可能會受到 Real-Time CDP 中目前 500 個串流區段的限制。若要了解詳細資訊，請閱讀[分段護欄](/help/profile/guardrails.md)。

## 2. 哪些區段對於透過 [!UICONTROL Audience Manager 來源連接器]傳送至關重要？

根據其評估標準，沒有資料相依性、沒有目的地或啟動挑戰，且其分段規則可在之後的日期透過 [Adobe Experience Platform Web SDK](/help/web-sdk/faq.md) 之類的 Real-Time CDP 資料集合建立的區段應透過 Audience Manager 來源連接器傳送。

## 3. 您會使用 [!UICONTROL Experience Cloud 對象]目的地將資料帶回 Audience Manager 嗎？

具有在 Real-Time CDP 中可受支援的規則但對 Audience Manager 具有啟動相依性的區段可以透過 [Experience Cloud 對象](/help/destinations/catalog/adobe/experience-cloud-audiences.md)目的地卡傳送至 Audience Manager。

## 4. 現在您在 Audience Manager 中已有哪些目的地可以開始移動到 Real-Time CDP？

Adobe 強烈建議應將在 Audience Manager 中啟動至[以人物為基礎的目標](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/destinations/people-based/people-based-destinations-overview.html?lang=zh-Hant)的區段透過 [!UICONTROL &#x200B; Audience Manager 來源連接器]推送至 Real-Time CDP，然後再透過 Real-Time CDP 啟動。

Audience Manager 中提供的所有以人物為基礎的目標 - [Facebook](/help/destinations/catalog/social/facebook.md)、[[!UICONTROL Google 目標客戶比對]](/help/destinations/catalog/advertising/google-customer-match.md)、[LinkedIn](/help/destinations/catalog/social/linkedin.md) - 也可在 Real-Time CDP 中使用。

還可使用其他第一方資料和媒體策略合作夥伴，例如，[Pinterest](/help/destinations/catalog/advertising/pinterest.md)、[Snapchat](/help/destinations/catalog/advertising/snap-inc.md)、[TikTok](/help/destinations/catalog/social/tiktok.md)、[Amazon Ads](/help/destinations/catalog/advertising/amazon-ads.md) 和 [[!UICONTROL The Trade Desk]](/help/destinations/catalog/advertising/tradedesk.md)。

Real-Time CDP 目前支援[目錄](/help/destinations/catalog/overview.md)中超過 60 個原生目的地，其中有 20 個以上屬於支援第一方客群媒合的廣告或社群目的地。

## 後續步驟

詳閱本頁面後，當您要開始從 Audience Manager 進化至 Real-Time CDP 時，立刻就有第一組需解決的注意事項。
