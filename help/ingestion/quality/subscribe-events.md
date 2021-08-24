---
keywords: Experience Platform；首頁；熱門主題；資料擷取通知；通知；訂閱事件；資料擷取狀態事件；狀態事件；訂閱；狀態通知；
solution: Experience Platform
title: 資料擷取通知
topic-legacy: overview
description: 為協助監控擷取程式，Adobe Experience Platform可訂閱程式每個步驟所發佈的一組事件，並通知您所擷取資料的狀態以及任何可能的失敗情況。
exl-id: fd34e1ab-f6f6-44f0-88ee-7020e9322c39
source-git-commit: a455134a45137b171636d6525ce9124bc95f4335
workflow-type: tm+mt
source-wordcount: '681'
ht-degree: 1%

---

# 資料擷取通知

將資料擷取至Adobe Experience Platform的程式由多個步驟組成。 一旦您識別需要內嵌至[!DNL Platform]的資料檔案，內嵌程式就會開始，且每個步驟會連續進行，直到資料成功內嵌或失敗為止。 擷取程式可使用[Adobe Experience Platform資料擷取API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/ingest-api.yaml)或使用[!DNL Experience Platform]使用者介面來起始。

載入到[!DNL Platform]的資料必須執行多個步驟才能到達其目的地，即[!DNL Data Lake]或[!DNL Real-time Customer Profile]資料儲存區。 每個步驟都包括處理資料、驗證資料，然後儲存資料再傳遞至下一個步驟。 視擷取的資料量而定，這可能會成為耗時的程式，且程式總有可能因驗證、語意或處理錯誤而失敗。 發生失敗時，需要修正資料問題，然後必須使用修正的資料檔案重新啟動整個擷取程式。

為協助監控擷取程式，[!DNL Experience Platform]可訂閱程式每個步驟所發佈的一組事件，並通知您所擷取資料的狀態以及任何可能的失敗。

## 註冊網頁連結以接收資料擷取通知

若要接收資料擷取通知，您必須使用[Adobe開發人員控制台](https://www.adobe.com/go/devs_console_ui)來註冊網頁連結至您的Experience Platform整合。

請依照[訂閱 [!DNL Adobe I/O Event] notifications](../../observability/alerts/subscribe.md)的教學課程，了解如何完成此作業的詳細步驟。

>[!IMPORTANT]
>
>在訂閱過程中，請確保選擇&#x200B;**[!UICONTROL 平台通知]**&#x200B;作為事件提供程式，並在出現提示時選擇&#x200B;**[!UICONTROL 資料獲取通知]**&#x200B;事件訂閱。

## 接收資料擷取通知

一旦您成功註冊網頁連結且已內嵌新資料後，即可開始接收事件通知。 這些事件可以使用Webhook本身來檢視，或在「Adobe開發人員控制台」中選取專案事件註冊概覽中的&#x200B;**[!UICONTROL Debug Tracing]**&#x200B;標籤來檢視。

下列JSON是通知裝載的範例，若批次擷取事件失敗，會將其傳送至您的網頁掛接：

```json
{
  "event_id": "93a5b11a-b0e6-4b29-ad82-81b1499cb4f2",
  "event": {
    "xdm:ingestionId": "01EGK8H8HF9JGFKNDCABHGA24G",
    "xdm:customerIngestionId": "01EGK8H8HF9JGFKNDCABHGA24G",
    "xdm:imsOrg": "{IMS_ORG}",
    "xdm:completed": 1598374341560,
    "xdm:datasetId": "5e55b556c2ae4418a8446037",
    "xdm:eventCode": "ing_load_failure",
    "xdm:sandboxName": "prod",
    "sentTime": "1598374341595",
    "processStartTime": 1598374342614,
    "transformedTime": 1598374342621,
    "header": {
      "_adobeio": {
        "imsOrgId": "{IMS_ORG}",
        "providerMetadata": "aep_observability_catalog_events",
        "eventCode": "platform_event"
      }
    }
  }
}
```

| 屬性 | 說明 |
| --- | --- |
| `event_id` | 通知的唯一、系統產生的ID。 |
| `event` | 一個物件，包含觸發通知之事件的詳細資料。 |
| `event.xdm:datasetId` | 擷取事件套用至的資料集ID。 |
| `event.xdm:eventCode` | 狀態代碼，指出為資料集觸發的事件類型。 請參閱[附錄](#event-codes)以了解特定值及其定義。 |

若要檢視事件通知的完整結構，請參閱[公用GitHub存放庫](https://github.com/adobe/xdm/blob/master/schemas/notifications/ingestion.schema.json)。

## 後續步驟

在您將[!DNL Platform]通知註冊到項目後，您就可以查看從[!UICONTROL 項目概述]接收的事件。 有關如何跟蹤事件的詳細說明，請參閱[跟蹤Adobe I/O事件](https://www.adobe.io/apis/experienceplatform/events/docs.html#!adobedocs/adobeio-events/master/support/tracing.md)上的指南。

## 附錄

以下章節包含解譯資料擷取通知裝載的其他資訊。

### 可用狀態通知事件 {#event-codes}

下表列出您可訂閱的可用資料擷取狀態通知。

| 事件代碼 | 平台服務 | 狀態 | 事件說明 |
| --- | ---------------- | ------ | ----------------- |
| `ing_load_success` | [!DNL Data Ingestion] | success | 批次匯入[!DNL Data Lake]內的資料整合功。 |
| `ing_load_failure` | [!DNL Data Ingestion] | 失敗 | 無法將批次內嵌至[!DNL Data Lake]內的資料集。 |
| `ps_load_success` | [!DNL Real-time Customer Profile] | 成功 | 已成功將批次擷取至[!DNL Profile]資料存放區。 |
| `ps_load_failure` | [!DNL Real-time Customer Profile] | 失敗 | 無法將批次內嵌到[!DNL Profile]資料儲存中。 |
| `ig_load_success` | [!DNL Identity Service] | 成功 | 資料已成功載入到標識圖中。 |
| `ig_load_failure` | [!DNL Identity Service] | 失敗 | 無法將資料載入到標識圖中。 |

>[!NOTE]
>
>只為所有資料擷取通知提供一個事件主題。 為了區分不同的狀態，可使用事件代碼。
