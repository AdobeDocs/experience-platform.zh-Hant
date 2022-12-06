---
keywords: Experience Platform；目的地api；臨機啟動；啟動區段臨機
solution: Experience Platform
title: 透過臨機啟動API啟動對象區段以批次目的地
description: 本文說明透過臨機啟動API來啟動對象區段的端對端工作流程，包括啟動前發生的區段工作。
topic-legacy: tutorial
type: Tutorial
exl-id: 1a09f5ff-0b04-413d-a9f6-57911a92b4e4
source-git-commit: cdf96088be27cba1fb92f1348f002123614285fe
workflow-type: tm+mt
source-wordcount: '1563'
ht-degree: 1%

---

# 透過臨機啟動API隨選啟動受眾區段，以批次目的地

>[!IMPORTANT]
>
>完成測試階段後， [!DNL ad-hoc activation API] 現在已可供所有Experience Platform客戶使用(GA)。 在GA版本中，API已升級至版本2。 步驟4([取得最新的區段匯出工作ID](#segment-export-id))已不是必要項目，因為API不再需要匯出ID。
>
>請參閱 [執行臨機啟動工作](#activation-job) 如需詳細資訊，請參閱本教學課程的下文。

## 總覽 {#overview}

臨機啟動API可讓行銷人員針對需要立即啟動的情況，以快速且有效的方式，以程式設計方式將對象區段啟用至目的地。

使用Ad-Hoc Activation API將完整檔案匯出至您想要的檔案接收系統。 僅支援隨選對象啟動 [批次檔案型目的地](../destination-types.md#file-based).

下圖說明透過臨機啟動API來啟用區段的端對端工作流程，包括每24小時在Platform中發生的區段工作。

![臨機啟動](../assets/api/ad-hoc-activation/ad-hoc-activation-overview.png)



## 使用案例 {#use-cases}

### Flash銷售或促銷

一家線上零售商正在準備有限的快閃銷售，希望在短時間內通知客戶。 透過Experience Platform臨機啟動API，行銷團隊可以隨選匯出區段，並快速傳送促銷電子郵件給客戶群。

### 最新事件或突發新聞

酒店預計接下來幾天會有惡劣的天氣，團隊想要快速通知到達的客人，以便他們能據此進行規劃。 行銷團隊可使用Experience Platform臨機啟動API，依需求匯出區段，並通知客人。

### 整合測試

IT經理可以使用Experience Platform臨機啟動API，依需求匯出區段，以便測試其與Adobe Experience Platform的自訂整合，並確保一切正常運作。

## 護欄 {#guardrails}

使用臨機啟動API時，請記住下列護欄。

* 目前，每個臨機啟動工作最多可啟動80個區段。 嘗試啟動每個作業超過80個區段會導致作業失敗。 此行為在未來版本中可能會有所變更。
* 臨機啟動作業無法與已排程的同時執行 [區段匯出作業](../../segmentation/api/export-jobs.md). 在執行臨機啟動工作之前，請確定排程的區段匯出工作已完成。 請參閱 [目標資料流監視](../../dataflows/ui/monitor-destinations.md) 以了解如何監控啟動流程的狀態。 例如，如果激活資料流顯示 **[!UICONTROL 處理]** 狀態，請等待它完成，再執行臨機啟動工作。
* 每個區段請勿執行多個同時的臨機啟動工作。

## 區段考量事項 {#segmentation-considerations}

Adobe Experience Platform每24小時執行一次已排程的分段工作。 臨機啟動API會根據最新的細分結果執行。

## 步驟1:必要條件 {#prerequisites}

呼叫Adobe Experience Platform API之前，請務必符合下列必要條件：

* 您有可存取Adobe Experience Platform的IMS組織帳戶。
* 您的Experience Platform帳戶具有 `developer` 和 `user` 為Adobe Experience Platform API產品設定檔啟用的角色。 請連絡您的 [Admin Console](../../access-control/home.md) 管理員來為您的帳戶啟用這些角色。
* 你有Adobe ID。 如果您沒有Adobe ID，請前往 [Adobe Developer Console](https://developer.adobe.com/console) 並建立新帳戶。

## 步驟2:收集憑據 {#credentials}

若要呼叫Platform API，您必須先完成 [驗證教學課程](https://www.adobe.com/go/platform-api-authentication-en). 完成驗證教學課程後，所有Experience PlatformAPI呼叫中每個必要標題的值都會顯示，如下所示：

* 授權：承載 `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{ORG_ID}`

Experience Platform中的資源可以隔離至特定的虛擬沙箱。 在向Platform API提出的請求中，您可以指定要執行操作之沙箱的名稱和ID。 這些是選用參數。

* x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>如需Experience Platform中沙箱的詳細資訊，請參閱 [沙箱概述檔案](../../sandboxes/home.md).

所有包含裝載(POST、PUT、PATCH)的請求都需要其他媒體類型標題：

* Content-Type: `application/json`

## 步驟3:在Platform UI中建立啟動流程 {#activation-flow}

您必須先在平台UI中針對所選目的地設定啟動流程，才能透過臨機啟動API啟用區段。

這包括進入啟動工作流程、選取區段、設定排程和啟動這些區段。 您可以使用UI或API來建立啟動流程：

* [使用Platform UI建立啟動流程，以批次匯出設定檔目的地](../ui/activate-batch-profile-destinations.md)
* [使用流量服務API連線至批次設定檔匯出目的地並啟用資料](../api/connect-activate-batch-destinations.md)

## 步驟4:取得最新的區段匯出工作ID（v2中不需要） {#segment-export-id}

>[!IMPORTANT]
>
>在臨機啟動API的v2中，您不需要取得最新的區段匯出工作ID。 您可以略過此步驟，然後繼續進行下一個步驟。

為批次目的地設定啟動流程後，排程的分段工作會每24小時自動開始執行。

您必須先取得最新區段匯出工作的ID，才能執行臨機啟動工作。 您必須在臨機啟動工作請求中傳遞此ID。

請遵循說明 [此處](../../segmentation/api/export-jobs.md#retrieve-list) 以擷取所有區段匯出作業的清單。

在回應中，尋找第一個包含下方結構屬性的記錄。

```
"schema":{
   "name":"_xdm.context.profile"
}
```

區段匯出工作ID位於 `id` 屬性，如下所示。

![區段匯出作業ID](../assets/api/ad-hoc-activation/segment-export-job-id.png)


## 步驟5:執行臨機啟動工作 {#activation-job}

Adobe Experience Platform每24小時執行一次已排程的分段工作。 臨機啟動API會根據最新的細分結果執行。

>[!IMPORTANT]
>
>請注意下列一次性限制：在執行臨機啟動工作之前，請確定自根據您在 [步驟3 — 在Platform UI中建立啟動流程](#activation-flow).

在執行臨機啟動工作之前，請確定您區段的已排程區段匯出工作已完成。 請參閱 [目標資料流監視](../../dataflows/ui/monitor-destinations.md) 以了解如何監控啟動流程的狀態。 例如，如果激活資料流顯示 **[!UICONTROL 處理]** 狀態，請等待它完成，再執行臨機啟動工作以匯出完整檔案。

區段匯出工作完成後，您即可觸發啟動。

>[!NOTE]
>
>目前，每個臨機啟動工作最多可啟動80個區段。 嘗試啟動每個作業超過80個區段會導致作業失敗。 此行為在未來版本中可能會有所變更。

### 請求 {#request}

>[!IMPORTANT]
>
>必須包含 `Accept: application/vnd.adobe.adhoc.activation+json; version=2` 標題，以便使用ad-hoc啟動API的v2。

```shell
curl --location --request POST 'https://platform.adobe.io/data/core/activation/disflowprovider/adhocrun' \
--header 'x-gw-ims-org-id: 5555467B5D8013E50A494220@AdobeOrg' \
--header 'Authorization: Bearer {{token}}' \
--header 'x-sandbox-id: 6ef74723-3ee7-46a4-b747-233ee7a6a41a' \
--header 'x-sandbox-name: {sandbox-id}' \
--header 'Accept: application/vnd.adobe.adhoc.activation+json; version=2' \
--header 'Content-Type: application/json' \
--data-raw '{
   "activationInfo":{
      "destinationId1":[
         "segmentId1",
         "segmentId2"
      ],
      "destinationId2":[
         "segmentId2",
         "segmentId3"
      ]
   }
}'
```

| 屬性 | 說明 |
| -------- | ----------- |
| <ul><li>`destinationId1`</li><li>`destinationId2`</li></ul> | 您要啟用區段的目的地例項ID。 您可以導覽至 **[!UICONTROL 目的地]** > **[!UICONTROL 瀏覽]** ，然後按一下所需的目的地列，在右側邊欄中顯示目的地ID。 如需詳細資訊，請閱讀 [目的地工作區檔案](/help/destinations/ui/destinations-workspace.md#browse). |
| <ul><li>`segmentId1`</li><li>`segmentId2`</li><li>`segmentId3`</li></ul> | 您要啟用至所選目的地之區段的ID。 |

{style=&quot;table-layout:auto&quot;}

### 具有匯出ID的請求（即將廢止） {#request-deprecated}

>[!IMPORTANT]
>
>**已棄用的請求類型**. 此範例類型說明API第1版的請求類型。 在臨機啟動API的v2中，您不需要包含最新的區段匯出工作ID。

```shell
curl -X POST https://platform.adobe.io/data/core/activation/disflowprovider/adhocrun \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -d '
{
   "activationInfo":{
      "destinationId1":[
         "segmentId1",
         "segmentId2"
      ],
      "destinationId2":[
         "segmentId2",
         "segmentId3"
      ]
   },
   "exportIds":[
      "exportId1"
   ]
}
```

| 屬性 | 說明 |
| -------- | ----------- |
| <ul><li>`destinationId1`</li><li>`destinationId2`</li></ul> | 您要啟用區段的目的地例項ID。 您可以導覽至 **[!UICONTROL 目的地]** > **[!UICONTROL 瀏覽]** ，然後按一下所需的目的地列，在右側邊欄中顯示目的地ID。 如需詳細資訊，請閱讀 [目的地工作區檔案](/help/destinations/ui/destinations-workspace.md#browse). |
| <ul><li>`segmentId1`</li><li>`segmentId2`</li><li>`segmentId3`</li></ul> | 您要啟用至所選目的地之區段的ID。 |
| <ul><li>`exportId1`</li></ul> | 回應中傳回的ID為 [區段匯出](../../segmentation/api/export-jobs.md#retrieve-list) 工作。 請參閱 [步驟4:取得最新的區段匯出工作ID](#segment-export-id) 以取得如何找到此ID的指示。 |

{style=&quot;table-layout:auto&quot;}

### 回應 {#response}

成功的回應會傳回HTTP狀態200。

```shell
{
   "order":[
      {
         "segment":"db8961e9-d52f-45bc-b3fb-76d0382a6851",
         "order":"ef2dcbd6-36fc-49a3-afed-d7b8e8f724eb",
         "statusURL":"https://platform.adobe.io/data/foundation/flowservice/runs/88d6da63-dc97-460e-b781-fc795a7386d9"
      }
   ]
}
```

| 屬性 | 說明 |
| -------- | ----------- |
| `segment` | 已啟用區段的ID。 |
| `order` | 已啟動區段的目的地ID。 |
| `statusURL` | 啟動流程的狀態URL。 您可以使用 [流量服務API](../../sources/tutorials/api/monitor.md). |

{style=&quot;table-layout:auto&quot;}

## API錯誤處理 {#api-error-handling}

Destination SDKAPI端點遵循一般Experience PlatformAPI錯誤訊息原則。 請參閱 [API狀態代碼](../../landing/troubleshooting.md#api-status-codes) 和 [請求標題錯誤](../../landing/troubleshooting.md#request-header-errors) （位於平台疑難排解指南中）。

### Ad Hoc Activation API的API錯誤碼和訊息 {#specific-error-messages}

使用臨機啟動API時，您可能會遇到此API端點專屬的錯誤訊息。 請檢閱表格，了解在顯示時如何處理。

| 錯誤訊息 | 解析度 |
|---------|----------|
| 已針對區段執行 `segment ID` 訂購 `dataflow ID` 使用執行id `flow run ID` | 此錯誤訊息指出某個區段目前正在進行臨機啟動流程。 等待作業完成，然後再次觸發啟動作業。 |
| 區段 `<segment name>` 不屬於此資料流或超出計畫範圍！ | 此錯誤消息表示您選擇要激活的段未映射到資料流，或者為段設定的激活計畫已過期或尚未啟動。 檢查該段是否確實映射到資料流，並確認段激活時間表與當前日期重疊。 |

## 相關資訊 {#related-information}

* [使用流量服務API連線至批次目的地並啟動資料](/help/destinations/api/connect-activate-batch-destinations.md)
* [（測試版）使用Experience PlatformUI，隨選將檔案匯出至批次目的地](/help/destinations/ui/export-file-now.md)