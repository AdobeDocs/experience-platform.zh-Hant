---
keywords: Experience Platform；首頁；熱門主題；
title: (Beta)Mixpanel源連接器概述
description: 瞭解如何使用API或用戶介面將Mixpanel連接到Adobe Experience Platform。
exl-id: 7eb605f6-8580-40b7-a9b3-96b9c3444f5d
source-git-commit: e44f6d5bb2fd891a3e3b3c5e4aed68e8d4687b53
workflow-type: tm+mt
source-wordcount: '472'
ht-degree: 0%

---

# (Beta) [!DNL Mixpanel]

>[!NOTE]
>
>的 [!DNL Mixpanel] 源為beta。 查看 [源概述](../../home.md#terms-and-conditions) 的子菜單。

Adobe Experience Platform允許從外部源接收資料，同時讓您能夠使用平台服務構建、標籤和增強傳入資料。 您可以從多種源(如Adobe應用程式、基於雲的儲存、資料庫和許多其他源)接收資料。

Experience Platform支援從第三方分析應用程式接收資料。 對分析提供方的支援包括 [!DNL Mixpanel]。

[[!DNL Mixpanel]](https://www.mixpanel.com) 是一種產品分析工具，使您能夠捕獲有關用戶如何與數字產品交互的資料。 Mixpanel允許您使用簡單的互動式報告來分析此產品資料，這樣您只需按一下幾下即可查詢和可視化資料。

源利用 [Mixpanel事件導出API >下載](https://developer.mixpanel.com/reference/raw-event-export) 下載接收並儲存在中的事件資料 [!DNL Mixpanel]，以及所有事件屬性(包括 `distinct_id`)和事件發送到Experience Platform的確切時間戳。 Mixpanel使用承載令牌作為驗證機制與Mixpanel事件導出API通信。

## IP地址允許清單

在使用源連接器之前，必須將IP地址清單添加到允許清單。 如果無法將特定於區域的IP地址添加到允許清單，則在使用源時可能會導致錯誤或效能不佳。 查看 [IP地址允許清單](../../ip-address-allow-list.md) 的子菜單。

## 驗證您的 [!DNL Mixpanel] 帳戶

本節概述了為驗證帳戶和將您的 [!DNL Mixpanel] 資料到平台。

為了建立 [!DNL Mixpanel] 源連接和資料流，必須先具有有效 [!DNL Mixpanel] 帳戶。 如果您沒有有效 [!DNL Mixpanel] 帳戶，請參閱 [混合面板寄存器](https://mixpanel.com/register/) 的子菜單。

成功建立 [!DNL Mixpanel] 帳戶，導航到 [!DNL Project Details] 的 [!DNL Project Seettings] 的 [!DNL Mixpanel] UI以檢索項目ID並配置時區。

![混合面板 — 項目設定](../../images/tutorials/create/mixpanel-export-events/mixpanel-project-settings.png)

接下來，導航到 [!DNL Service Accounts] 的 [!DNL Project Settings] 的 [!DNL Mixpanel] 用於檢索服務帳戶憑據的UI。

>[!TIP]
>
>為獲得最佳實踐，請選擇一個 [未過期](https://developer.mixpanel.com/reference/service-accounts#service-account-expiration)。

![混合面板服務帳戶](../../images/tutorials/create/mixpanel-export-events/mixpanel-service-account.png)

最後，建立平台 [架構](../../../xdm/schema/composition.md) 為 [!DNL Mixpanel Event Export API]。 有關架構所需映射的詳細資訊，請參見上的指南 [建立 [!DNL Mixpanel] UI中的源連接](../../tutorials/ui/create/analytics/mixpanel.md#additional-resources)。

![建立架構](../../images/tutorials/create/mixpanel-export-events/schema.png)

## 連接 [!DNL Mixpanel] 到使用API的平台

以下文檔提供了有關如何連接的資訊 [!DNL Mixpanel] 到使用API或用戶介面的平台：

* [建立源連接和資料流 [!DNL Mixpanel] 使用流服務API](../../tutorials/api/create/analytics/mixpanel.md)

## 連接 [!DNL Mixpanel] 到使用UI的平台

* [建立 [!DNL Mixpanel] UI中的源連接](../../tutorials/ui/create/analytics/mixpanel.md)
* [在UI中為客戶成功源連接建立資料流](../../tutorials/ui/dataflow/analytics.md)
