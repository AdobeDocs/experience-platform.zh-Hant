---
keywords: Experience Platform；首頁；熱門主題
solution: Experience Platform
title: 訂閱Privacy Service事件
description: 瞭解如何使用預先設定的webhook訂閱Privacy Service事件。
exl-id: 9bd34313-3042-46e7-b670-7a330654b178
source-git-commit: 0f7ef438db5e7141197fb860a5814883d31ca545
workflow-type: tm+mt
source-wordcount: '440'
ht-degree: 2%

---

# 訂閱[!DNL Privacy Service Events]

[!DNL Privacy Service Events]是由Adobe Experience Platform [!DNL Privacy Service]提供的訊息，這些訊息會利用傳送至已設定的webhook的Adobe I/O事件來促進有效的工作請求自動化。 它們減少或消除了輪詢[!DNL Privacy Service] API以檢查工作是否完成或工作流程中是否已達到特定里程碑的需求。

目前與隱私權工作請求生命週期相關的通知有四種型別：

| 類型 | 說明 |
| --- | --- |
| 工作完成 | 所有[!DNL Experience Cloud]應用程式都已回報，且工作的整體或全域狀態已標示為完成。 |
| 工作錯誤 | 一或多個應用程式在處理請求時報告錯誤。 |
| 產品完成 | 與此工作關聯的其中一個應用程式已完成其工作。 |
| 產品錯誤 | 其中一個應用程式在處理請求時報告錯誤。 |

本檔案提供設定[!DNL Privacy Service]通知之事件註冊的步驟，以及如何解譯通知裝載。

## 快速入門

在開始本教學課程之前，請先檢閱下列Privacy Service檔案：

* [Privacy Service 概觀](./home.md)
* [Privacy Service API指南](./api/overview.md)

## 註冊webhook至[!DNL Privacy Service Events]

若要接收[!DNL Privacy Service Events]，您必須使用Adobe Developer Console註冊webhook以進行[!DNL Privacy Service]整合。

請依照有關[訂閱[！DNL I/O Event]通知](../observability/alerts/subscribe.md)的教學課程，取得如何完成此作業的詳細步驟。 請務必選擇&#x200B;**[!UICONTROL Privacy Service事件]**&#x200B;作為事件提供者，以存取上述事件。

## 接收[!DNL Privacy Service Event]個通知

成功註冊webhook並執行隱私權工作後，您就可以開始接收事件通知。 您可以使用webhook本身檢視這些事件，或是在Adobe Developer Console中選取專案事件註冊總覽中的&#x200B;**[!UICONTROL 偵錯追蹤]**&#x200B;索引標籤。

![](images/privacy-events/debug-tracing.png)

下列JSON為[!DNL Privacy Service Event]通知裝載的範例，當與隱私權工作相關聯的應用程式之一完成其工作時，會傳送至您的webhook：

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
| `id` | 系統產生的通知唯一ID。 |
| `type` | 正在傳送的通知型別，為`data`下提供的資訊提供內容。 可能的值包括： <ul><li>`com.adobe.platform.gdpr.jobcomplete`</li><li>`com.adobe.platform.gdpr.joberror`</li><li>`com.adobe.platform.gdpr.productcomplete`</li><li>`com.adobe.platform.gdpr.producterror`</li></ul> |
| `time` | 事件發生時間的時間戳記。 |
| `data.value` | 包含觸發通知之專案的其他資訊： <ul><li>`jobId`：觸發通知的隱私權工作識別碼。</li><li>`message`：關於工作特定狀態的訊息。 對於`productcomplete`或`producterror`通知，此欄位表示有問題的Experience Cloud應用程式。</li></ul> |

## 後續步驟

本檔案說明如何將Privacy Service事件註冊到已設定的webhook，以及如何解譯通知裝載。 若要瞭解如何使用使用者介面追蹤隱私權工作，請參閱[Privacy Service使用手冊](./ui/user-guide.md)。
