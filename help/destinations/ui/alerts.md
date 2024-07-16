---
keywords: Experience Platform；首頁；熱門主題；警報；目的地
description: 您可以在建立資料流時訂閱警報，以接收有關流程執行的狀態、成功或失敗的警報訊息。
title: 訂閱內容感知目的地警示
exl-id: 134144a0-cdfe-49a8-bd8b-e36a4f053de5
source-git-commit: 165793619437f403045b9301ca6fa5389d55db31
workflow-type: tm+mt
source-wordcount: '948'
ht-degree: 8%

---

# 訂閱內容感知目的地警示

Adobe Experience Platform可讓您訂閱有關Adobe Experience Platform活動的事件型警報。 警示可減少或消除輪詢[[!DNL Observability Insights] API](../../observability/api/overview.md)的需求，以檢查工作是否已完成、工作流程中是否已達到特定里程碑，或是否已發生任何錯誤。

建立資料流時，您可以訂閱警示以接收有關資料流執行狀態、成功或失敗的警示訊息。

本檔案提供如何訂閱目的地資料流接收警報訊息的步驟。

## 快速入門

參閱本檔案前，請先實際瞭解下列Adobe Experience Platform元件：

* [目的地](../home.md)：預先建立與目的地平台的整合，可順暢地從Adobe Experience Platform啟用資料。 您可使用目的地啟用已知和未知的資料，以進行跨通路行銷活動、電子郵件行銷活動、設定目標的廣告活動和其他諸多使用案例。
* [可觀察性](../../observability/home.md)： [!DNL Observability Insights]可讓您透過使用統計量度和事件通知來監視Platform活動。
   * [警示](../../observability/alerts/overview.md)：當您的Platform作業達到特定條件集時（例如系統違反臨界值時會發生潛在問題），Platform可以將警示訊息傳送給貴組織中訂閱這些訊息的任何使用者。

## 訂閱 UI 中的警示 {#subscribe-destination-alerts}

>[!CONTEXTUALHELP]
>id="platform_destination_alerts_subscribe"
>title="訂閱目的地警示"
>abstract="警示可讓您根據目的地資料流的狀態接收通知。如果資料流已啟動、成功、失敗或未向目的地傳送任何資料，您可以設定警示通知以獲取更新。"
>text="Learn more in documentation"

>[!IMPORTANT]
>
>您必須為您的Platform帳戶啟用即時電子郵件通知，才能接收資料流程的電子郵件式警報通知。

您可以在[目的地連線](connect-destination.md)工作流程的[!UICONTROL 設定新目的地]步驟期間，為資料流程啟用警示。

![顯示目的地警示區段的UI影像。](../assets/ui/alerts/destination-alerts.png)

選取您要訂閱的警示，然後選取&#x200B;**[!UICONTROL 下一步]**&#x200B;以檢視並完成您的資料流。

下表說明可用於目的地資料流程的警報。

* 對於串流目的地，只有[!DNL Activation Skipped Rate Exceeded]警報可用。
* 針對以檔案為基礎的目的地，所有警報皆可使用。

| 警報 | 說明 |
| --- | --- |
| 目的地資料流執行延遲 | 此警報會在目的地流程執行需要150分鐘以上的時間才會啟用對象時通知您。 |
| 目的地資料流執行失敗 | 將受眾啟用至目的地時發生錯誤，此警報會通知您。 |
| 目的地流程執行成功 | 此警報會在對象成功啟用至目的地時通知您。 |
| 目的地資料流執行開始 | 此警報會在目的地流程執行開始啟用對象時通知您。 |
| 超過啟用略過率 | 此警報會在啟用略過率超過啟用總數的1%時通知您。 當身分缺少屬性或違反同意時，會在啟用期間略過身分。 |

## 接收警示 {#receiving-alerts}

目的地資料流執行後，您可以透過UI或電子郵件接收警報。

### 在UI中接收警報 {#receiving-alerts-in-ui}

警報會在UI中以Platform UI頂端標題中的通知圖示表示。 選取通知圖示以檢視有關資料流的特定警報訊息。

顯示Experience Platform](../assets/ui/alerts/notification.png)中通知圖示的![UI影像

此時會顯示通知面板，其中顯示您所建立之資料流上的狀態更新清單。

![顯示通知面板的UI影像](../assets/ui/alerts/alert-window.png)

您可以將滑鼠指標暫留在警示訊息上，以將其標示為已讀取，也可以選取時鐘圖示來設定未來對資料流狀態的提醒。

![顯示通知提醒選項的UI影像](../assets/ui/alerts/remind-me.png)

選取警示訊息，以檢視資料流的特定資訊。

顯示如何選取通知的![使用者介面影像](../assets/ui/alerts/select-alert-message.png)

[!UICONTROL 資料流執行詳細資料]頁面就會顯示。 畫面的上半部會顯示資料流程的概觀，包括其屬性的相關資訊、對應的資料流程執行ID和高階錯誤摘要。

![顯示資料流執行詳細資訊頁面的UI影像。](../assets/ui/alerts/dataflow-overview.png)

頁面下半部顯示在資料流執行階段期間發生的任何[!UICONTROL 資料流執行錯誤]。 從這裡，您可以預覽錯誤診斷，或使用[[!DNL Data Access] API](https://www.adobe.io/experience-platform-apis/references/data-access/)下載與您的資料流對應的錯誤診斷或檔案資訊清單。

![顯示資料流執行詳細資訊頁面的UI影像，錯誤區段上有醒目提示。](../assets/ui/alerts/dataflow-run-error.png)

如需有關處理資料流錯誤的詳細資訊，請參閱UI](../../dataflows/ui/monitor-destinations.md)中[監視目的地資料流的指南。

### 透過電子郵件接收警示 {#receiving-alerts-by-email}

您的資料流警示也會透過電子郵件傳送給您。 選取電子郵件內文中的資料流名稱，以檢視資料流的詳細資訊。

![警示電子郵件的熒幕擷圖](../assets/ui/alerts/email.png)

類似於UI警示，[!UICONTROL 資料流執行總覽]頁面會出現，為您提供介面以調查與資料流關聯的任何錯誤。

![資料流總覽](../assets/ui/alerts/dataflow-overview.png)

## 訂閱和取消訂閱警示 {#subscribe-and-unsubscribe}

您可以針對目的地[!UICONTROL 瀏覽]頁面中的現有目的地資料流，訂閱更多警示或取消訂閱已建立的警示。

顯示[目的地瀏覽]頁面的![UI影像](../assets/ui/alerts/destination-list.png)

找到您要接收警示的目的地連線，並選取省略符號(`...`)以檢視選項的下拉式功能表。 接著，選取&#x200B;**[!UICONTROL 訂閱警示]**&#x200B;以修改目的地資料流程的警示設定。

![顯示目的地選項的UI影像](../assets/ui/alerts/destination-alerts-subscribe.png)

此時會出現快顯視窗，提供您目的地警示的清單。 選取您要訂閱的警示，或取消選取您要取消訂閱的警示。 完成後，選取&#x200B;**[!UICONTROL 儲存]**。

![顯示目的地警示訂閱頁面的UI影像](../assets/ui/alerts/destination-alerts-list.png)

## 後續步驟 {#next-steps}

本檔案逐步說明如何訂閱目的地資料流程的內容感知警報。 如需詳細資訊，請參閱[警示使用者介面指南](../../observability/alerts/ui.md)。
