---
keywords: Experience Platform；首頁；熱門主題
solution: Experience Platform
title: 訂閱Privacy Service事件
description: 了解如何使用預先設定的網頁連結來訂閱Privacy Service事件。
exl-id: 9bd34313-3042-46e7-b670-7a330654b178
source-git-commit: 0f7ef438db5e7141197fb860a5814883d31ca545
workflow-type: tm+mt
source-wordcount: '440'
ht-degree: 2%

---

# 訂閱 [!DNL Privacy Service Events]

[!DNL Privacy Service Events] 由Adobe Experience Platform提供 [!DNL Privacy Service]，此功能會利用傳送至已設定之webhook的Adobe I/O事件來促進有效的工作請求自動化。 它們減少或消除輪詢 [!DNL Privacy Service] API，以檢查工作是否完成，或工作流程中是否已達到特定里程碑。

目前有四種與隱私權工作請求生命週期相關的通知類型：

| 類型 | 說明 |
| --- | --- |
| 作業完成 | 全部 [!DNL Experience Cloud] 應用程式已返回報告，作業的整體或全局狀態已標籤為已完成。 |
| 作業錯誤 | 一個或多個應用程式在處理請求時報告了錯誤。 |
| 產品完成 | 與此作業關聯的一個應用程式已完成其工作。 |
| 產品錯誤 | 其中一個應用程式在處理請求時報告了錯誤。 |

本檔案提供設定 [!DNL Privacy Service] 通知，以及如何解譯通知裝載。

## 快速入門

開始本教學課程之前，請先檢閱下列Privacy Service檔案：

* [Privacy Service 概觀](./home.md)
* [Privacy ServiceAPI指南](./api/overview.md)

## 將網頁鈎註冊到 [!DNL Privacy Service Events]

為了接收 [!DNL Privacy Service Events]，您必須使用Adobe Developer Console將網頁連結註冊至您的 [!DNL Privacy Service] 整合。

請依照 [訂閱[!DNL I/O Event]通知](../observability/alerts/subscribe.md) 以取得完成此作業的詳細步驟。 確保您選擇 **[!UICONTROL Privacy Service事件]** 作為事件提供者，以存取上述事件。

## 接收 [!DNL Privacy Service Event] 通知

成功註冊網頁連結和隱私權工作後，您就可以開始接收事件通知。 這些事件可使用網頁連結本身，或選取 **[!UICONTROL 調試跟蹤]** 頁簽(在Adobe Developer Console中)。

![](images/privacy-events/debug-tracing.png)

下列JSON是 [!DNL Privacy Service Event] 當與隱私權工作相關聯的應用程式完成其工作時，會傳送至您的webhook的通知裝載：

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
| `id` | 通知的唯一、系統產生的ID。 |
| `type` | 要傳送的通知類型，提供下列項目所提供資訊的內容 `data`. 潛在值包括： <ul><li>`com.adobe.platform.gdpr.jobcomplete`</li><li>`com.adobe.platform.gdpr.joberror`</li><li>`com.adobe.platform.gdpr.productcomplete`</li><li>`com.adobe.platform.gdpr.producterror`</li></ul> |
| `time` | 事件發生時的時間戳記。 |
| `data.value` | 包含有關觸發通知的其他資訊： <ul><li>`jobId`:觸發通知的隱私權工作ID。</li><li>`message`:有關作業的特定狀態的訊息。 針對 `productcomplete` 或 `producterror` 通知，此欄位指示有關的Experience Cloud應用程式。</li></ul> |

## 後續步驟

本檔案說明如何將Privacy Service事件註冊至已設定的WebHook，以及如何解譯通知裝載。 若要了解如何使用使用者介面追蹤隱私權工作，請參閱 [Privacy Service使用手冊](./ui/user-guide.md).
