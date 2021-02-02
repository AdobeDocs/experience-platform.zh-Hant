---
keywords: Experience Platform;home；熱門主題
solution: Experience Platform
title: 訂閱隱私權服務事件
topic: privacy events
description: 瞭解如何使用預先設定的網頁掛接訂閱隱私權服務事件。
translation-type: tm+mt
source-git-commit: 2b919a3b6cbbd59521874cfd2d11e20de3077740
workflow-type: tm+mt
source-wordcount: '437'
ht-degree: 1%

---


# 訂閱[!DNL Privacy Service Events]

[!DNL Privacy Service Events] 是Adobe Experience Platform提供的訊息，它運 [!DNL Privacy Service]用傳送至已設定網頁掛接的Adobe I/O事件，以協助有效率的工作要求自動化。它們可降低或免除輪詢[!DNL Privacy Service] API的需求，以檢查工作是否完成或工作流程中是否達到特定里程碑。

目前有四種與隱私作業請求生命週期相關的通知類型：

| 類型 | 說明 |
| --- | --- |
| 工作完成 | 所有[!DNL Experience Cloud]應用程式都已回報，作業的整體或全域狀態已標示為完成。 |
| 作業錯誤 | 一或多個應用程式在處理請求時報告錯誤。 |
| 產品完整 | 與此作業關聯的其中一個應用程式已完成其工作。 |
| 產品錯誤 | 其中一個應用程式在處理請求時報告錯誤。 |

本檔案提供設定[!DNL Privacy Service]通知事件註冊的步驟，以及如何解譯通知負載。

## 快速入門

開始本教學課程之前，請先閱讀下列隱私權服務檔案：

* [隱私權服務概觀](./home.md)
* [隱私權服務API開發人員指南](./api/getting-started.md)

## 向[!DNL Privacy Service Events]註冊Webhook

若要接收[!DNL Privacy Service Events]，您必須使用Adobe Developer Console註冊網頁掛接至您的[!DNL Privacy Service]整合。

請依照[訂閱 [!DNL I/O Event] 通知](../observability/notifications/subscribe.md)的教學課程，瞭解如何完成此作業的詳細步驟。 請確定您選擇&#x200B;**[!UICONTROL 隱私服務事件]**&#x200B;作為事件提供者，以存取上述事件。

## 接收[!DNL Privacy Service Event]通知

在您成功註冊網頁掛接和隱私權工作後，您就可以開始接收事件通知。 這些事件可使用網頁掛接本身來檢視，或在Adobe Developer Console中，選取專案事件註冊概觀中的&#x200B;**[!UICONTROL 除錯追蹤]**&#x200B;標籤來檢視。

![](images/privacy-events/debug-tracing.png)

以下JSON是[!DNL Privacy Service Event]通知裝載的範例，當其中一個與隱私權工作相關的應用程式完成其工作時，會傳送至您的網頁掛接：

```json
{
  "id":"b472e249-368b-4706-90f3-1d774713f827",
  "event_id":"b116f797-e50b-432e-9c65-189106a34820",
  "specversion":"0.2",
  "type":"com.adobe.platform.gdpr.productcomplete",
  "source":"https://ns.adobe.com/platform/gdpr",
  "time":"Wed Oct 23 18:52:32 GMT 2019",
  "data":{
    "imsOrg":"{IMS_ORG}",
    "value":{
      "jobId":"6f0f2b62-88a7-4515-ba05-432d9a7021c5",
      "message":"analytics.access.complete"
    }
  }
}
```

| 屬性 | 說明 |
| --- | --- |
| `id` | 通知的唯一系統產生ID。 |
| `type` | 所發送的通知類型，提供`data`下提供的資訊的上下文。 潛在值包括： <ul><li>`com.adobe.platform.gdpr.jobcomplete`</li><li>`com.adobe.platform.gdpr.joberror`</li><li>`com.adobe.platform.gdpr.productcomplete`</li><li>`com.adobe.platform.gdpr.producterror`</li></ul> |
| `time` | 事件發生的時間戳記。 |
| `data.value` | 包含觸發通知的其他資訊： <ul><li>`jobId`:觸發通知的隱私權工作ID。</li><li>`message`:有關作業特定狀態的消息。對於`productcomplete`或`producterror`通知，此欄位會指出相關的Experience Cloud應用程式。</li></ul> |

## 後續步驟

本檔案涵蓋如何將隱私權服務事件註冊至已設定的網頁掛接，以及如何解譯通知負載。 要瞭解如何使用用戶介面跟蹤隱私作業，請參閱[隱私服務使用手冊](./ui/user-guide.md)。