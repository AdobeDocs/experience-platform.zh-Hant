---
keywords: Experience Platform；首頁；熱門主題；警報；目標
description: 在建立資料流時，您可以訂閱警報，以接收有關流運行狀態、成功或失敗的警報消息。
title: 訂閱上下文中的目標警報
exl-id: 134144a0-cdfe-49a8-bd8b-e36a4f053de5
source-git-commit: 3bb9858c236c91e1567fd8e78988f4049537ffe3
workflow-type: tm+mt
source-wordcount: '950'
ht-degree: 5%

---

# 訂閱上下文中的目標警報

Adobe Experience Platform允許您訂閱有關Adobe Experience Platform活動的基於事件的警報。 警報減少或消除輪詢 [[!DNL Observability Insights] API](../../observability/api/overview.md) 以檢查作業是否已完成、是否已達到工作流中的某個里程碑，或是否發生任何錯誤。

在建立資料流以接收有關流運行狀態、成功或失敗的警報消息時，可以訂閱警報。

本文檔提供了如何訂閱目標資料流的警報消息的步驟。

## 快速入門

本檔案要求對Adobe Experience Platform的下列構成部分有工作上的理解：

* [目標](../home.md):預構建的與目標平台的整合，允許無縫激活來自Adobe Experience Platform的資料。 您可以使用目標來激活跨渠道市場營銷活動、電子郵件活動、目標廣告和許多其他使用案例的已知和未知資料。
* [可觀測性](../../observability/home.md): [!DNL Observability Insights] 允許您通過使用統計度量和事件通知來監視平台活動。
   * [警報](../../observability/alerts/overview.md):當平台操作中達到某組條件時（例如當系統超過閾值時可能出現的問題），平台可以向組織中已訂閱這些條件的任何用戶發送警報消息。

## 訂閱UI中的警報 {#subscribe-destination-alerts}

>[!CONTEXTUALHELP]
>id="platform_destination_alerts_subscribe"
>title="訂閱目的地警示"
>abstract="警示可讓您根據目的地資料流的狀態接收通知。如果資料流已啟動、成功、失敗或未向目的地傳送任何資料，您可以設定警示通知以獲取更新。"
>text="Learn more in documentation"

>[!IMPORTANT]
>
>您必須為平台帳戶啟用電子郵件即時通知才能接收資料流基於電子郵件的警報通知。

您可以在 [!UICONTROL 配置新目標] 的 [目標連接](connect-destination.md) 工作流。

![顯示目標警報部分的UI影像。](../assets/ui/alerts/destination-alerts.png)

選擇要訂閱的警報，然後選擇 **[!UICONTROL 下一個]** 查看並完成資料流。

下表介紹了目標資料流可用的警報。

* 對於流目標，僅 [!DNL Activation Skipped Rate Exceeded] 警報可用。
* 對於基於檔案的目標，所有警報都可用。

| 警報 | 說明 |
| --- | --- |
| 目標流運行延遲 | 當目標流運行激活段所用時間超過150分鐘時，此警報會通知您。 |
| 目標流運行失敗 | 當激活到目標的段時出錯時，此警報會通知您。 |
| 目標流運行成功 | 當網段成功激活到目標時，此警報會通知您。 |
| 目標流運行開始 | 當目標流運行開始激活段時，此警報會通知您。 |
| 已跳過激活率 | 當激活跳過率超過總激活的1%時，此警報會通知您。 當標識缺少屬性或違反同意時，在激活過程中將跳過標識。 |

## 接收警報 {#receiving-alerts}

目標資料流一旦運行，您就可以通過UI或電子郵件接收警報。

### 在UI中接收警報 {#receiving-alerts-in-ui}

警報在UI中由平台UI頂部標題中的通知表徵圖表示。 選擇通知表徵圖以查看有關資料流的特定警報消息。

![顯示Experience Platform中通知表徵圖的UI影像](../assets/ui/alerts/notification.png)

此時將顯示通知面板，其中顯示您建立的資料流上的狀態更新清單。

![顯示通知面板的UI影像](../assets/ui/alerts/alert-window.png)

您可以懸停在警報消息上，將其標籤為已讀，也可以選擇時鐘錶徵圖以設定將來有關資料流狀態的提醒。

![顯示通知提醒選項的UI影像](../assets/ui/alerts/remind-me.png)

選擇警報消息以查看有關資料流的特定資訊。

![顯示如何選擇通知的UI影像](../assets/ui/alerts/select-alert-message.png)

的 [!UICONTROL 資料流運行詳細資訊] 的子菜單。 螢幕的上半部分顯示有關資料流的概述，包括有關其屬性、相應資料流運行ID和高級錯誤摘要的資訊。

![顯示「資料流運行詳細資料」頁的UI影像。](../assets/ui/alerts/dataflow-overview.png)

頁面的下半部分顯示任何 [!UICONTROL 資料流運行錯誤] 在資料流運行階段出現。 在此處，您可以預覽錯誤診斷或使用 [[!DNL Data Access] API](https://www.adobe.io/experience-platform-apis/references/data-access/) 下載錯誤診斷或與資料流對應的檔案清單。

![顯示「資料流運行詳細資訊」頁的UI影像，錯誤部分上有突出顯示部分。](../assets/ui/alerts/dataflow-run-error.png)

有關處理資料流錯誤的詳細資訊，請參見上的指南 [監視UI中的目標資料流](../../dataflows/ui/monitor-destinations.md)。

### 通過電子郵件接收警報 {#receiving-alerts-by-email}

您的資料流警報也通過電子郵件發送給您。 選擇電子郵件正文中的資料流名稱，以查看有關資料流的詳細資訊。

![警報電子郵件的螢幕快照](../assets/ui/alerts/email.png)

與UI警報類似， [!UICONTROL 資料流運行概述] 的子菜單。

![資料流概述](../assets/ui/alerts/dataflow-overview.png)

## 訂閱和取消訂閱警報 {#subscribe-and-unsubscribe}

您可以訂閱目標中現有目標資料流的更多警報或取消訂閱已建立的警報 [!UICONTROL 瀏覽] 的子菜單。

![顯示「目標瀏覽」頁的UI影像](../assets/ui/alerts/destination-list.png)

找到要接收警報的目標連接並選擇橢圓(`...`)以查看選項的下拉菜單。 下一步，選擇 **[!UICONTROL 訂閱警報]** 修改目標資料流的警報設定。

![顯示目標選項的UI影像](../assets/ui/alerts/destination-alerts-subscribe.png)

此時將出現一個彈出窗口，為您提供目標警報清單。 選擇要訂閱的警報或取消選擇要取消訂閱的警報。 完成後，選擇 **[!UICONTROL 保存]**。

![顯示目標警報訂閱頁的UI影像](../assets/ui/alerts/destination-alerts-list.png)

## 後續步驟 {#next-steps}

本文檔提供了有關如何訂閱目標資料流的上下文警報的逐步指南。 有關詳細資訊，請參見 [警報UI指南](../../observability/alerts/ui.md)。
