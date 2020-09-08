---
keywords: Experience Platform;home;popular topics;data ingestion notifications;notifications;subscribe events;data ingestion status events;status events;subscribe;status notifications;
solution: Experience Platform
title: 訂閱資料擷取事件
topic: overview
translation-type: tm+mt
source-git-commit: 80a1694f11cd2f38347989731ab7c56c2c198090
workflow-type: tm+mt
source-wordcount: '621'
ht-degree: 1%

---


# 資料擷取通知

將資料擷取至Adobe Experience Platform的程式由多個步驟組成。 一旦您識別需要擷取的資料檔案後，擷取程 [!DNL Platform]序就會開始，每個步驟都會連續進行，直到資料被成功擷取或失敗為止。 您可以使用 [Adobe Experience Platform Data Ingestion API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/ingest-api.yaml) ，或使用使用者介面來啟 [!DNL Experience Platform] 動擷取程式。

載入的資 [!DNL Platform] 料必須經過多個步驟，才能到達其目的地、 [!DNL Data Lake] 或資 [!DNL Real-time Customer Profile] 料儲存。 每個步驟都包括處理資料、驗證資料，然後儲存資料，再傳遞至下一步驟。 視所擷取的資料量而定，這可能會變成耗時的程式，而且程式總會因為驗證、語義或處理錯誤而失敗。 發生故障時，需要修正資料問題，然後必須使用修正的資料檔案重新啟動整個擷取程式。

為協助監控擷取程式， [!DNL Experience Platform] 可訂閱由程式每個步驟所發佈的一組事件，並通知您所擷取資料的狀態和任何可能的失敗。

## 註冊網頁掛接以取得資料擷取通知

若要接收資料擷取通知，您必須使用 [Adobe Developer Console](https://www.adobe.com/go/devs_console_ui) ，註冊Experience Platform整合的網頁掛接。

請依照訂閱通知 [的教 [!DNL Adobe I/O Event] 學課程](../../observability/notifications/subscribe.md) ，取得如何完成此作業的詳細步驟。

>[!IMPORTANT]
>
>在訂閱程式中，請確定您選擇 **[!UICONTROL Platform notifications]** 作為事件提供者，並在出現提示時選 **[!UICONTROL 擇Data ingestion notification]** event subscription。

## 接收資料擷取通知

在您成功註冊網頁掛接且已收錄新資料後，您就可以開始接收事件通知。 這些事件可使用網頁掛接本身來檢視，或在Adobe Developer Console中選取專案的事件註冊概觀中的 **[!UICONTROL Debug Tracing]** 標籤來檢視。

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
| `event.xdm:eventCode` | 狀態代碼，指出為資料集觸發的事件類型。 請參閱 [附錄](#event-codes) ，瞭解特定值及其定義。 |

要查看事件通知的完整模式，請參閱公 [用GitHub儲存庫](https://github.com/adobe/xdm/blob/master/schemas/notifications/ingestion.schema.json)。

## 後續步驟

在您將通知注 [!DNL Platform] 冊到專案後，您就可以從「專案」概觀中檢視收到 [!UICONTROL 的事件]。 如需如何追蹤 [事件的詳細指示](https://www.adobe.io/apis/experienceplatform/events/docs.html#!adobedocs/adobeio-events/master/support/tracing.md) ，請參閱追蹤Adobe I/O事件指南。

## 附錄

下節包含解釋資料擷取通知負載的其他資訊。

### 可用狀態通知事件 {#event-codes}

下表列出您可訂閱的可用資料擷取狀態通知。

| 事件代碼 | 平台服務 | 狀態 | 事件說明 |
| --- | ---------------- | ------ | ----------------- |
| `ing_load_success` | [!DNL Data Ingestion] | success | 批次已成功吸收至中的資料集 [!DNL Data Lake]。 |
| `ing_load_failure` | [!DNL Data Ingestion] | 失敗 | 無法將批次吸收到中的資料集中 [!DNL Data Lake]。 |
| `ps_load_success` | [!DNL Real-time Customer Profile] | success | 已成功將批次吸收至資料 [!DNL Profile] 儲存區。 |
| `ps_load_failure` | [!DNL Real-time Customer Profile] | 失敗 | 無法將批次吸收到資料 [!DNL Profile] 儲存中。 |
| `ig_load_success` | [!DNL Identity Service] | success | 資料已成功載入識別圖。 |
| `ig_load_failure` | [!DNL Identity Service] | 失敗 | 無法將資料載入識別圖。 |

>[!NOTE]
>
>所有資料擷取通知只提供一個事件主題。 為了區分不同的狀態，可以使用事件代碼。