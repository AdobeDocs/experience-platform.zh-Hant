---
keywords: Experience Platform;home；熱門主題；資料提取通知；通知；訂閱事件；資料提取狀態事件；狀態事件；subscribe；狀態通知；
solution: Experience Platform
title: 資料擷取通知
topic-legacy: overview
description: 為協助監控擷取程式，Adobe Experience Platform可訂閱在程式每個步驟發佈的一組事件，並通知您所擷取資料的狀態和任何可能的失敗。
exl-id: fd34e1ab-f6f6-44f0-88ee-7020e9322c39
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '672'
ht-degree: 1%

---

# 資料擷取通知

將資料收錄到Adobe Experience Platform的過程由多個步驟組成。 在您識別需要收錄至[!DNL Platform]的資料檔案後，擷取程式就會開始，每個步驟都會連續進行，直到資料成功收錄或失敗為止。 可以使用[Adobe Experience Platform資料攝取API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/ingest-api.yaml)或使用[!DNL Experience Platform]用戶介面來啟動攝取過程。

載入到[!DNL Platform]中的資料必須經過多個步驟才能到達其目標、[!DNL Data Lake]或[!DNL Real-time Customer Profile]資料儲存。 每個步驟都包括處理資料、驗證資料，然後儲存資料，再傳遞至下一步驟。 視所擷取的資料量而定，這可能會變成耗時的程式，而且程式總會因為驗證、語義或處理錯誤而失敗。 發生故障時，需要修正資料問題，然後必須使用修正的資料檔案重新啟動整個擷取程式。

為協助監控擷取程式，[!DNL Experience Platform]可訂閱由程式每個步驟發佈的一組事件，並通知您所擷取資料的狀態和任何可能的失敗。

## 註冊網頁掛接以取得資料擷取通知

若要接收資料擷取通知，您必須使用[Adobe開發人員主控台](https://www.adobe.com/go/devs_console_ui)來註冊網頁掛接至您的Experience Platform整合。

請依照[訂閱 [!DNL Adobe I/O Event] 通知](../../observability/notifications/subscribe.md)的教學課程，瞭解如何完成此作業的詳細步驟。

>[!IMPORTANT]
>
>在訂閱程式中，請確定您選擇&#x200B;**[!UICONTROL Platform notifications]**&#x200B;做為事件提供者，並在出現提示時選擇&#x200B;**[!UICONTROL Data ingestion notification]**&#x200B;事件訂閱。

## 接收資料擷取通知

在您成功註冊網頁掛接且已收錄新資料後，您就可以開始接收事件通知。 這些事件可使用網頁掛接本身來檢視，或在「Adobe開發人員主控台」中選取專案事件註冊概述中的&#x200B;**[!UICONTROL Debug Tracing]**&#x200B;標籤。

下列JSON是通知裝載的範例，在批次擷取事件失敗時，會傳送至您的網頁掛接：

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
| `event_id` | 通知的唯一系統產生ID。 |
| `event` | 包含觸發通知之事件的詳細資料的物件。 |
| `event.xdm:datasetId` | 擷取事件套用至的資料集ID。 |
| `event.xdm:eventCode` | 狀態代碼，指出為資料集觸發的事件類型。 有關特定值及其定義，請參見[附錄](#event-codes)。 |

要查看事件通知的完整模式，請參閱[public GitHub儲存庫](https://github.com/adobe/xdm/blob/master/schemas/notifications/ingestion.schema.json)。

## 後續步驟

在您將[!DNL Platform]通知註冊到您的專案後，即可檢視從[!UICONTROL Project overview]收到的事件。 有關如何跟蹤事件的詳細說明，請參閱[跟蹤Adobe I/O事件](https://www.adobe.io/apis/experienceplatform/events/docs.html#!adobedocs/adobeio-events/master/support/tracing.md)上的指南。

## 附錄

下節包含解釋資料擷取通知負載的其他資訊。

### 可用狀態通知事件{#event-codes}

下表列出您可訂閱的可用資料擷取狀態通知。

| 事件代碼 | 平台服務 | 狀態 | 事件說明 |
| --- | ---------------- | ------ | ----------------- |
| `ing_load_success` | [!DNL Data Ingestion] | success | 已成功將批次吸收至[!DNL Data Lake]中的資料集。 |
| `ing_load_failure` | [!DNL Data Ingestion] | 失敗 | 無法將批次吸收到[!DNL Data Lake]中的資料集中。 |
| `ps_load_success` | [!DNL Real-time Customer Profile] | 成功 | 已成功將批裝入[!DNL Profile]資料儲存。 |
| `ps_load_failure` | [!DNL Real-time Customer Profile] | 失敗 | 未能將批次吸收到[!DNL Profile]資料儲存中。 |
| `ig_load_success` | [!DNL Identity Service] | 成功 | 資料已成功載入識別圖。 |
| `ig_load_failure` | [!DNL Identity Service] | 失敗 | 無法將資料載入識別圖。 |

>[!NOTE]
>
>所有資料擷取通知只提供一個事件主題。 為了區分不同的狀態，可以使用事件代碼。
