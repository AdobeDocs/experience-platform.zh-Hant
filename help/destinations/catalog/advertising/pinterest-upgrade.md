---
title: pinterest目的地移轉至新API。 需要客戶動作。
description: pinterest即將淘汰Real-Time CDP中Pinterest目的地目前使用的v4廣告商API。 瞭解您的行動專案，以便順暢地轉換至新的API，而不會中斷您的Pinterest行銷活動。
hide: true
hidefromtoc: true
exl-id: c965235c-4208-4c28-9ac5-eb4c0061515d
source-git-commit: e3341ec6f62844858ecda7dd4db70d085f0bf217
workflow-type: tm+mt
source-wordcount: '531'
ht-degree: 0%

---

# pinterest目的地升級至新API。 2024年1月18日前需要客戶動作。

>[!IMPORTANT]
>
>如果您的組織已設定資料流，讓資料在2023年11月16日（新日期之前）匯出至Pinterest，則您會套用此頁面上的客戶動作專案 **[!UICONTROL pinterest]** 使用最新Pinterest API的目的地已新增至目的地目錄。

## 發生什麼事？

pinterest已將 [pinterest目的地](/help/destinations/catalog/advertising/pinterest.md) 在Real-Time CDP中。 Adobe已更新目標以使用 [v5廣告商API](https://developers.pinterest.com/docs/getting-started/migration/). 請閱讀本頁面以瞭解您的行動專案，以便順暢地轉換至新的API，而不會中斷您的Pinterest行銷活動。

## 為什麼會收到通知？

我們已識別您的組織具有使用中的資料流，可在Pinterest中啟用對象。

## 有什麼計畫？

Adobe已發行新的Pinterest目的地卡，此卡會利用Pinterest API v5，並將您現有的資料流保留在新連線中。

## 我是否需要做任何事來維持我啟用的對象正常運作？

是，在2024年1月18日之前，您需要使用Real-Time CDP中的Pinterest廣告商帳戶來驗證至新的Pinterest目的地。 請參閱以下的詳細說明。

### 向Pinterest重新驗證 {#reauthenticate}

1. 前往 **[!UICONTROL 目的地>帳戶]** 並在熒幕上使用篩選器以僅篩選Pinterest目的地。
   ![僅篩選Pinterest帳戶](/help/destinations/assets/catalog/advertising/pinterest-migration/filter-pinterest-acconts-only.png)
2. 在 **pinterest** 目的地，選取三點符號……並選取 **[!UICONTROL 編輯詳細資料]**.
   ![選取編輯詳細資訊](/help/destinations/assets/catalog/advertising/pinterest-migration/edit-details-pinterest.png)
3. 選取 **[!UICONTROL 重新連線OAuth]** 並登入您的Pinterest帳戶。
   ![選取重新連線OAuth](/help/destinations/assets/catalog/advertising/pinterest-migration/reconnect-oauth-pinterest.png)
4. 移至下節中的行動專案

### 啟用流向新目的地 {#disable-old-enable-new-flows}

然後，您需要啟用新的資料流  **[!UICONTROL pinterest]** 卡片。

1. 前往 **[!UICONTROL 目的地>瀏覽]** 並使用熒幕上的篩選器來篩選 **[!UICONTROL pinterest]** 僅限目的地。
   ![僅在「瀏覽」索引標籤中篩選Pinterest資料流程](/help/destinations/assets/catalog/advertising/pinterest-migration/filter-pinterest-browse.png)
2. 選取超連結的連線名稱（以上熒幕擷圖範例中的忠誠度行銷活動）至 **[!UICONTROL pinterest]** 目的地並切換 **[!UICONTROL 啟用]** 切換至 **於**.
   ![針對新連線切換開啟，針對舊連線切換關閉](/help/destinations/assets/catalog/advertising/pinterest-migration/enable-disable-toggle-new-destination.png)

<!--

While no disruption to your campaigns is expected, remember to check in the Pinterest UI that everything works as expected.

-->

## 您可以分享一些高階時間表嗎？

是，請參閱下文：

**2023年11月16日前**：新目的地已準備就緒，您應該會在目錄中看到兩張Pinterest卡片並排，直到Pinterest停止支援舊的v4 API為止。 您目前Pinterest卡片的所有現有資料流都會複製到新目的地。

![新舊的Pinterest目的地並排](/help/destinations/assets/catalog/advertising/pinterest-migration/pinterest-two-cards-side-by-side.png)

<!--

>[!IMPORTANT]
>
>After November 16th, 2023 the legacy Pinterest destination is marked **[!UICONTROL Deprecating]**. <span class="preview">Any changes that you make to dataflows to the (Deprecating) Pinterest destination after November 16th will *not* be automatically carried over to the new Pinterest destination. </span>
>For example, we *do not recommend* that you activate new audiences to the old destination after November 16th. If you do that, you will then have to follow the [regular activation steps](/help/destinations/ui/activate-segment-streaming-destinations.md) to add the audience to the new destination once the customer actions are taken.

-->

**最遲於2023年12月15日**： <span class="preview">客戶動作1</span>. 您需要重新向Pinterest進行驗證，以便新卡片連線到Pinterest。 在中檢視完整指示 [本節](#reauthenticate).

<span class="preview">客戶動作2</span>然後，您必須啟用新卡片中的資料流。 在中檢視完整指示 [本節](#disable-old-enable-new-flows).

<!--

>[!IMPORTANT]
>
>After December 15th, 2023, Adobe does not guarantee the integrity of dataflows to the old **[!UICONTROL (Deprecating) Pinterest]** destination.

-->

**2024年1月18日之後**： <span class="preview">pinterest已關閉V4廣告商API的存取權。 任何尚未升級至新目的地的Real-Time CDP客戶現在都會發現他們的資料流無法升級至Pinterest目的地。 [向Pinterest重新驗證](#reauthenticate) 和 [啟用資料流](#disable-old-enable-new-flows) 升級至目的地，繼續將行銷活動至Pinterest。</span>

<!--

## Other items to note

After you enable the dataflows on the new destination card and disable the dataflows on the old destination cards, you should see no disruption in your campaigns or in the numbers of qualified profiles in the audiences coming in from Adobe Real-Time CDP.

-->
