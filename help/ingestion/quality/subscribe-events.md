---
keywords: Experience Platform；首頁；熱門主題；資料接收通知；通知；訂閱事件；資料接收狀態事件；狀態事件；訂閱；狀態通知；
solution: Experience Platform
title: 資料接收通知
description: 為了幫助監控攝取過程，Adobe Experience Platform允許訂閱一組事件，這些事件由該過程的每個步驟發佈，並通知您所攝取資料的狀態和任何可能的故障。
exl-id: fd34e1ab-f6f6-44f0-88ee-7020e9322c39
source-git-commit: 76ef5638316a89aee1c6fb33370af943228b75e1
workflow-type: tm+mt
source-wordcount: '677'
ht-degree: 1%

---

# 資料接收通知

將資料輸入到Adobe Experience Platform的過程由多個步驟組成。 一旦確定需要接收到的資料檔案 [!DNL Platform]，攝取過程開始，每個步驟都連續進行，直到資料成功攝取或失敗。 可使用 [Adobe Experience Platform批量攝取API](https://developer.adobe.com/experience-platform-apis/references/batch-ingestion/) 或使用 [!DNL Experience Platform] 用戶介面。

資料載入到 [!DNL Platform] 必須經過多個步驟才能到達目的地， [!DNL Data Lake] 或 [!DNL Real-Time Customer Profile] 資料儲存。 每個步驟都包括處理資料、驗證資料，然後在將資料傳遞到下一步之前儲存資料。 根據所攝取的資料量，這可能會成為一個耗時的過程，並且始終存在由於驗證、語義或處理錯誤而導致該過程失敗的可能性。 在發生故障時，需要修復資料問題，然後必須使用更正的資料檔案重新啟動整個接收過程。

為了協助監測攝入過程， [!DNL Experience Platform] 使您能夠訂閱由流程的每個步驟發佈的一組事件，並通知您所接收資料的狀態和任何可能的故障。

## 註冊網路掛接以接收資料通知

要接收資料接收通知，您必須使用 [Adobe Developer控制台](https://www.adobe.com/go/devs_console_ui) 將webhook註冊到Experience Platform整合。

按照本教程 [訂閱 [!DNL Adobe I/O Event] 通知](../../observability/alerts/subscribe.md) 詳細的步驟。

>[!IMPORTANT]
>
>在訂閱過程中，確保選擇 **[!UICONTROL 平台通知]** 作為事件提供程式，並選擇 **[!UICONTROL 資料接收通知]** 事件訂閱（出現提示時）。

## 接收資料接收通知

成功註冊網路掛接並接收新資料後，您就可以開始接收事件通知。 可以使用webhook本身或通過選擇 **[!UICONTROL 調試跟蹤]** 頁籤。

以下JSON是通知負載的示例，在發生失敗的批接收事件時，將發送到Webhook:

```json
{
  "event_id": "93a5b11a-b0e6-4b29-ad82-81b1499cb4f2",
  "event": {
    "xdm:ingestionId": "01EGK8H8HF9JGFKNDCABHGA24G",
    "xdm:customerIngestionId": "01EGK8H8HF9JGFKNDCABHGA24G",
    "xdm:imsOrg": "{ORG_ID}",
    "xdm:completed": 1598374341560,
    "xdm:datasetId": "5e55b556c2ae4418a8446037",
    "xdm:eventCode": "ing_load_failure",
    "xdm:sandboxName": "prod",
    "sentTime": "1598374341595",
    "processStartTime": 1598374342614,
    "transformedTime": 1598374342621,
    "header": {
      "_adobeio": {
        "imsOrgId": "{ORG_ID}",
        "providerMetadata": "aep_observability_catalog_events",
        "eventCode": "platform_event"
      }
    }
  }
}
```

| 屬性 | 說明 |
| --- | --- |
| `event_id` | 通知的唯一系統生成ID。 |
| `event` | 包含觸發通知的事件詳細資訊的對象。 |
| `event.xdm:datasetId` | 接收事件應用到的資料集的ID。 |
| `event.xdm:eventCode` | 一個狀態代碼，用於指示為資料集觸發的事件的類型。 查看 [附錄](#event-codes) 定義。 |

要查看事件通知的完整架構，請參閱 [公共GitHub儲存庫](https://github.com/adobe/xdm/blob/master/schemas/notifications/ingestion.schema.json)。

## 後續步驟

註冊後 [!DNL Platform] 通知項目，您可以從 [!UICONTROL 項目概述]。 請參閱上的指南 [跟蹤Adobe I/O事件](https://www.adobe.io/apis/experienceplatform/events/docs.html#!adobedocs/adobeio-events/master/support/tracing.md) 有關如何跟蹤事件的詳細說明。

## 附錄

以下部分包含有關解釋資料接收通知負載的其他資訊。

### 可用狀態通知事件 {#event-codes}

下表列出了可預訂的可用資料接收狀態通知。

| 事件代碼 | 平台服務 | 狀態 | 事件說明 |
| --- | ---------------- | ------ | ----------------- |
| `ing_load_success` | [!DNL Data Ingestion] | success | 已成功將批處理導入資料集中 [!DNL Data Lake]。 |
| `ing_load_failure` | [!DNL Data Ingestion] | 失敗 | 未能將批攝取到 [!DNL Data Lake]。 |
| `ps_load_success` | [!DNL Real-Time Customer Profile] | success | 已成功將批攝取到 [!DNL Profile] 資料儲存。 |
| `ps_load_failure` | [!DNL Real-Time Customer Profile] | 失敗 | 未能將批攝取到 [!DNL Profile] 資料儲存。 |
| `ig_load_success` | [!DNL Identity Service] | success | 已成功將資料載入到標識圖中。 |
| `ig_load_failure` | [!DNL Identity Service] | 失敗 | 資料無法載入到標識圖中。 |

>[!NOTE]
>
>只為所有資料接收通知提供了一個事件主題。 為了區分不同的狀態，可以使用事件代碼。
