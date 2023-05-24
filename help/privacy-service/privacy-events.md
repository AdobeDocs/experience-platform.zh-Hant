---
keywords: Experience Platform；首頁；熱門主題
solution: Experience Platform
title: 訂閱Privacy Service事件
description: 瞭解如何使用預配置的webhook訂閱Privacy Service事件。
exl-id: 9bd34313-3042-46e7-b670-7a330654b178
source-git-commit: 0f7ef438db5e7141197fb860a5814883d31ca545
workflow-type: tm+mt
source-wordcount: '440'
ht-degree: 2%

---

# 訂閱 [!DNL Privacy Service Events]

[!DNL Privacy Service Events] 由Adobe Experience Platform提供 [!DNL Privacy Service]，它利用發送到已配置webhook的Adobe I/O事件來促進高效的作業請求自動化。 它們減少或消除了 [!DNL Privacy Service] API，以檢查作業是否完成或是否已達到工作流中的某個里程碑。

當前有四種類型的通知與隱私作業請求生命週期相關：

| 類型 | 說明 |
| --- | --- |
| 作業完成 | 全部 [!DNL Experience Cloud] 應用程式已返回，作業的總體或全局狀態已標籤為完成。 |
| 作業錯誤 | 一個或多個應用程式在處理請求時報告錯誤。 |
| 產品完成 | 與此作業關聯的其中一個應用程式已完成其工作。 |
| 產品錯誤 | 其中一個應用程式在處理請求時報告錯誤。 |

本文檔提供了設定事件註冊的步驟 [!DNL Privacy Service] 通知，以及如何解釋通知負載。

## 快速入門

在開始本教程之前，請查看以下Privacy Service文檔：

* [Privacy Service 概觀](./home.md)
* [Privacy ServiceAPI指南](./api/overview.md)

## 將網鈎註冊到 [!DNL Privacy Service Events]

為了接收 [!DNL Privacy Service Events]，必須使用Adobe Developer控制台將Webhook註冊到 [!DNL Privacy Service] 整合。

按照本教程 [訂閱[!DNL I/O事件]通知](../observability/alerts/subscribe.md) 詳細的步驟。 確保您選擇 **[!UICONTROL Privacy Service事件]** 作為事件提供程式以訪問上面列出的事件。

## 接收 [!DNL Privacy Service Event] 通知

成功註冊Webhook和隱私作業後，可以開始接收事件通知。 可以使用webhook本身或通過選擇 **[!UICONTROL 調試跟蹤]** 頁籤。

![](images/privacy-events/debug-tracing.png)

以下JSON是 [!DNL Privacy Service Event] 當與隱私作業關聯的應用程式之一完成其工作時，將發送到webhook的通知負載：

```json
{
  "id":"b472e249-368b-4706-90f3-1d774713f827",
  "event_id":"b116f797-e50b-432e-9c65-189106a34820",
  "specversion":"0.2",
  "type":"com.adobe.platform.gdpr.productcomplete",
  "source":"https://ns.adobe.com/platform/gdpr",
  "time":"Wed Oct 23 18:52:32 GMT 2019",
  "data":{
    "imsOrg":"{ORG_ID}",
    "value":{
      "jobId":"6f0f2b62-88a7-4515-ba05-432d9a7021c5",
      "message":"analytics.access.complete"
    }
  }
}
```

| 屬性 | 說明 |
| --- | --- |
| `id` | 通知的唯一系統生成ID。 |
| `type` | 正在發送的通知的類型，為下面提供的資訊提供上下文 `data`。 潛在值包括： <ul><li>`com.adobe.platform.gdpr.jobcomplete`</li><li>`com.adobe.platform.gdpr.joberror`</li><li>`com.adobe.platform.gdpr.productcomplete`</li><li>`com.adobe.platform.gdpr.producterror`</li></ul> |
| `time` | 事件發生時間的時間戳。 |
| `data.value` | 包含有關觸發通知的其他資訊： <ul><li>`jobId`:觸發通知的隱私作業的ID。</li><li>`message`:有關作業的特定狀態的消息。 對於 `productcomplete` 或 `producterror` 通知，此欄位表示有問題的Experience Cloud應用程式。</li></ul> |

## 後續步驟

本文檔介紹如何將Privacy Service事件註冊到已配置的Webhook，以及如何解釋通知負載。 要瞭解如何使用用戶介面跟蹤隱私作業，請參閱 [Privacy Service使用手冊](./ui/user-guide.md)。
