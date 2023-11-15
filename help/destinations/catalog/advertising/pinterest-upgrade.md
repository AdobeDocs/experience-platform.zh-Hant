---
title: pinterest目的地移轉至新API。 需要客戶動作。
description: pinterest即將淘汰Real-Time CDP中Pinterest目的地目前使用的v4廣告商API。 瞭解您的行動專案，以便順暢地轉換至新的API，而不會中斷您的Pinterest行銷活動。
hide: true
hidefromtoc: true
source-git-commit: 10bf63677c66366c226d647b1174093c1704a8b9
workflow-type: tm+mt
source-wordcount: '713'
ht-degree: 0%

---

# pinterest目的地升級至新API。 2023年12月15日前需要客戶動作

## 發生什麼事？

pinterest即將淘汰目前由使用的v4廣告商API。 [pinterest目的地](/help/destinations/catalog/advertising/pinterest.md) 在Real-Time CDP中。 Adobe正在與Pinterest搭配使用，且正在更新目的地以使用 [v5廣告商API](https://developers.pinterest.com/docs/getting-started/migration/). 請閱讀本頁面以瞭解您的行動專案，以便順暢地轉換至新的API，而不會中斷您的Pinterest行銷活動。

## 為什麼會收到通知？

我們已識別您的組織具有使用中的資料流，可在Pinterest中啟用對象。

## 有什麼計畫？

Adobe即將發行新的Pinterest目的地卡，此卡會利用Pinterest API v5，並將您現有的資料流保留在新連線中。

## 我是否需要做任何事來維持我啟用的對象正常運作？

是，一旦Adobe完成升級（目標為11月16日），您需要使用Adobe Experience Platform中的Pinterest廣告商帳戶重新驗證Pinterest。 請參閱以下的詳細說明。

### 向Pinterest重新驗證 {#reauthenticate}

1. 前往 **[!UICONTROL 目的地>帳戶]** 並在熒幕上使用篩選器以僅篩選Pinterest目的地。
   ![僅篩選Pinterest帳戶](/help/destinations/assets/catalog/advertising/pinterest-migration/filter-pinterest-acconts-only.png)
2. 在 **（新） Pinterest** 目的地，選取三點符號……並選取 **[!UICONTROL 編輯詳細資料]**.
   ![選取編輯詳細資訊](/help/destinations/assets/catalog/advertising/pinterest-migration/edit-details-pinterest.png)
3. 選取 **[!UICONTROL 重新連線OAuth]** 並登入您的Pinterest帳戶。
   ![選取重新連線OAuth](/help/destinations/assets/catalog/advertising/pinterest-migration/reconnect-oauth-pinterest.png)
4. 告知Adobe您已重新驗證 **[!UICONTROL （新） Pinterest]** 目的地。

### 停用現有流向舊目的地並啟用流向新目的地的流量 {#disable-old-enable-new-flows}

然後，您需要手動停用舊卡片的現有資料流，並啟用新卡片的資料流。

>[!IMPORTANT]
>
>重新驗證之後，您可以聯絡Adobe，我們將會為您執行這第二個步驟。 如果您偏好手動執行此步驟，請遵循下列步驟：

1. 前往 **[!UICONTROL 目的地>瀏覽]** 並使用熒幕上的篩選器來篩選 **[!UICONTROL （新） Pinterest]** 和 **[!UICONTROL （淘汰） Pinterest]** 僅限目的地。
   ![僅在「瀏覽」索引標籤中篩選Pinterest資料流程](/help/destinations/assets/catalog/advertising/pinterest-migration/filter-pinterest-browse.png)
2. 選取超連結的連線名稱（以上熒幕擷圖範例中的忠誠度促銷活動），然後切換 **[!UICONTROL 啟用]** 切換至 **關閉** 用於舊連線和 **於** 用於新連線。
   ![針對新連線切換開啟，針對舊連線切換關閉](/help/destinations/assets/catalog/advertising/pinterest-migration/enable-disable-toggle.png)
3. 比較舊資料流和新資料流中已啟用的對象清單，並確保舊流程中沒有新流程中缺少的任何新對象。

雖然行銷活動不會如預期般中斷，但請記得存取Pinterest UI，確認一切都如預期般運作。

## 您可以分享一些高階時間表嗎？

是，請參閱下文：

**最遲於11月16日**：新目的地已準備就緒，您應該會在目錄中看到兩張Pinterest卡片並排，而且流向目前Pinterest卡片的所有現有資料流都會複製到新目的地。

![新舊的Pinterest目的地並排](/help/destinations/assets/catalog/advertising/pinterest-migration/pinterest-two-cards-side-by-side.png)

>[!IMPORTANT]
>
>11月16日之後，系統會標籤舊版Pinterest目的地 **[!UICONTROL 棄用]**. <span class="preview">您在11月16日之後對（淘汰） Pinterest目的地的資料流所做的任何變更都將 *非* 會自動轉至新的Pinterest目的地。 </span>
>例如，我們 *不推薦* 您在11月16日之後對舊目的地啟用新對象。 若您這麼做，您將必須遵循 [一般啟動步驟](/help/destinations/ui/activate-segment-streaming-destinations.md) 在採取客戶動作後，將對象新增至新目的地。

**最遲於12月15日**： <span class="preview">客戶動作</span>. 您需要重新向Pinterest進行驗證，以便新卡片連線到Pinterest （如上進一步的說明）。 完成此操作後，請聯絡我們。

需要停用舊卡片中Pinterest的資料流，並且需要啟用新卡片中的資料流。 您可以在UI中手動執行此操作，或聯絡Adobe，我們將會為您執行此操作。

## 其他要注意的專案

在新目的地卡片上啟用資料流並停用舊目的地卡片上的資料流後，您應該不會看到行銷活動或來自Adobe Real-Time CDP的受眾中合格設定檔數的中斷。
