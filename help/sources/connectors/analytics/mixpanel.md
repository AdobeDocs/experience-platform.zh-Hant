---
keywords: Experience Platform；首頁；熱門主題；
title: （測試版）Mixpanel源連接器概述
description: 了解如何使用API或使用者介面將Mixpanel連線至Adobe Experience Platform。
exl-id: 7eb605f6-8580-40b7-a9b3-96b9c3444f5d
source-git-commit: e44f6d5bb2fd891a3e3b3c5e4aed68e8d4687b53
workflow-type: tm+mt
source-wordcount: '472'
ht-degree: 0%

---

# （測試版） [!DNL Mixpanel]

>[!NOTE]
>
>此 [!DNL Mixpanel] 來源為測試版。 請參閱 [來源概觀](../../home.md#terms-and-conditions) 以取得使用測試版標籤來源的詳細資訊。

Adobe Experience Platform可讓您從外部來源擷取資料，同時使用Platform服務來建構、加標籤及增強傳入資料。 您可以從多種來源(如Adobe應用程式、雲儲存、資料庫等)內嵌資料。

Experience Platform支援從協力廠商分析應用程式擷取資料。 支援分析提供者包括 [!DNL Mixpanel].

[[!DNL Mixpanel]](https://www.mixpanel.com) 是產品分析工具，可讓您擷取使用者與數位產品互動的相關資料。 Mixpanel可讓您透過簡單的互動式報表來分析此產品資料，只需按幾下即可查詢及視覺化資料。

來源利用 [Mixpanel事件匯出API >下載](https://developer.mixpanel.com/reference/raw-event-export) 在收到事件資料時下載該資料並儲存在 [!DNL Mixpanel]，以及所有事件屬性(包括 `distinct_id`)和事件傳送至Experience Platform的確切時間戳記。 Mixpanel使用承載權杖作為驗證機制，以與Mixpanel事件匯出API通訊。

## IP位址允許清單

使用來源連接器前，必須將IP位址清單新增至允許清單。 若未將您地區專屬的IP位址新增至允許清單，在使用來源時可能會導致錯誤或效能不佳。 請參閱 [IP位址允許清單](../../ip-address-allow-list.md) 頁面以取得詳細資訊。

## 驗證您的 [!DNL Mixpanel] 帳戶

本節概述要完成的先決條件步驟，以便驗證您的帳戶並帶入您的 [!DNL Mixpanel] 資料至Platform。

若要建立 [!DNL Mixpanel] 源連接和資料流，必須先具有有效 [!DNL Mixpanel] 帳戶。 如果您沒有有效 [!DNL Mixpanel] 帳戶，請參閱 [混合面板寄存器](https://mixpanel.com/register/) 頁面來建立您的帳戶。

成功建立 [!DNL Mixpanel] 帳戶，導覽至 [!DNL Project Details] 標籤 [!DNL Project Seettings] 頁面 [!DNL Mixpanel] UI來擷取您的專案ID和設定時區。

![mixpanel-project-settings](../../images/tutorials/create/mixpanel-export-events/mixpanel-project-settings.png)

接下來，導覽至 [!DNL Service Accounts] 標籤 [!DNL Project Settings] 頁面 [!DNL Mixpanel] UI以擷取您的服務帳戶憑證。

>[!TIP]
>
>為獲得最佳實務，請選擇一個服務帳戶 [不會過期](https://developer.mixpanel.com/reference/service-accounts#service-account-expiration).

![Mixpanel服務帳戶](../../images/tutorials/create/mixpanel-export-events/mixpanel-service-account.png)

最後，建立平台 [綱要](../../../xdm/schema/composition.md) 必填 [!DNL Mixpanel Event Export API]. 如需架構所需對應的詳細資訊，請參閱 [建立 [!DNL Mixpanel] UI中的源連接](../../tutorials/ui/create/analytics/mixpanel.md#additional-resources).

![建立結構](../../images/tutorials/create/mixpanel-export-events/schema.png)

## Connect [!DNL Mixpanel] 使用API到平台

以下檔案提供如何連線的資訊 [!DNL Mixpanel] 若要使用API或使用者介面來建立平台：

* [為建立源連接和資料流 [!DNL Mixpanel] 使用流量服務API](../../tutorials/api/create/analytics/mixpanel.md)

## Connect [!DNL Mixpanel] 使用UI設為Platform

* [建立 [!DNL Mixpanel] UI中的源連接](../../tutorials/ui/create/analytics/mixpanel.md)
* [在UI中為客戶成功源連接建立資料流](../../tutorials/ui/dataflow/analytics.md)
