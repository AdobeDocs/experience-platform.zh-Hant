---
title: Experience Platform中的事件重複處理
description: 瞭解Adobe Experience Platform如何處理事件重複
exl-id: ac8c3ee8-52cf-459c-b283-16ed32d2976d
source-git-commit: bb90bbddf33bc4b0557026a0f34965ac37475c65
workflow-type: tm+mt
source-wordcount: '443'
ht-degree: 0%

---

# Adobe Experience Platform中的事件重複處理

Adobe Experience Platform是高度分散的系統，專為最大化可靠性而設計，同時可擴充至不斷增加的資料量。

針對即時資料收集，會透過Edge Network從使用者端來源(例如Web SDK或[Mobile SDK](/help/xdm/classes/experienceevent.md))收集[體驗事件](https://developer.adobe.com/client-sdks/home/)，並傳送至Experience Platform處理和儲存層。 這些圖層會組成解決方案，例如Experience Platform、[Real-Time CDP](/help/rtcdp/home.md)、[Customer Journey Analytics](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-overview/cja-overview.html?lang=zh-Hant)和[Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/ajo-home.html?lang=zh-Hant)。

為了將體驗事件遺失減至最少，使用者端SDK和內部Experience Platform傳送服務會要求您確認已成功收集事件。

如果未收到該確認，使用者端SDK或內部Experience Platform傳送服務會觸發重試，然後再次傳送體驗事件。

這是處理暫時性失敗的最佳作法。 副作用是可能會引入重複事件。

若要深入瞭解處理暫時性失敗的最佳實務，請參閱這篇有關[暫時性錯誤處理](https://learn.microsoft.com/en-us/azure/architecture/best-practices/transient-faults)的文章。

## 事件重複情況 {#scenarios}

事件重複可能會發生在各種案例中，例如但不限於：

* 使用者端SDK與[!DNL Edge Network]之間的網路相關問題。 這些問題可能源自網際網路服務提供者故障、行動訊號遺失或其他網路故障，因為客戶與Edge Network之間的連線是透過公用網際網路完成的。
* 內部Experience Platform自動縮放事件。 有時候，由於雲端基礎結構不穩定，資料可以重新平衡。

Adobe Experience Platform資料收集層可支援「至少一次」處理作業。 因此，在有限且極少數的情況下，可能會發生事件重複。

若要瞭解有關「至少一次」處理的詳細資訊，請參閱[訊息傳遞保證](https://docs.confluent.io/kafka/design/delivery-semantics.html)上的文章。

## 事件重複資料刪除選項 {#deduplication}

針對對重複事件敏感的業務案例，Experience Platform在其下游儲存系統中使用多種事件重複資料刪除方法，如下所述。

* 如果`_id`中已存在具有相同[!DNL Profile store]的事件，Real-Time CDP設定檔存放區會捨棄事件。 如需詳細資訊，請參閱[XDM ExperienceEvent類別](/help/xdm/classes/experienceevent.md)的相關檔案。
* Customer Journey Analytics可讓使用者設定量度，以非重複的方式僅計算值。 若要瞭解如何執行此動作，請參閱有關[量度重複資料刪除元件設定](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-dataviews/component-settings/metric-deduplication.html?lang=zh-Hant)的檔案。
* 當需要從計算中移除整個列或忽略特定欄位集（因為列中只有部分資料是重複資訊）時，Experience Platform查詢服務支援重複資料刪除。 如需詳細資訊，請參閱查詢服務[中有關](/help/query-service/key-concepts/deduplication.md)重複資料刪除的檔案。

>[!NOTE]
>
>如果您在上述使用案例之外遇到事件重複問題，請聯絡您的Adobe代表，並提供您使用案例的詳細資訊。
