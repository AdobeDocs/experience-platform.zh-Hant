---
keywords: Experience Platform；目的地api；臨機啟動；啟動區段臨機
solution: Experience Platform
title: （測試版）透過臨機啟動API啟動對象區段以批次目的地
description: 本文說明透過臨機啟動API來啟動對象區段的端對端工作流程，包括啟動前發生的區段工作。
topic-legacy: tutorial
type: Tutorial
source-git-commit: 749fa5dc1e8291382408d9b1a0391c4c7f2b2a46
workflow-type: tm+mt
source-wordcount: '1065'
ht-degree: 2%

---


# （測試版）透過臨機啟動API啟動對象區段以批次目的地

>[!IMPORTANT]
>
>此 [!DNL ad-hoc activation API] 中，目前為測試版。 文件和功能可能會有所變更。

## 總覽 {#overview}

臨機啟動API可讓行銷人員針對需要立即啟動的情況，以快速且有效的方式，以程式設計方式將對象區段啟用至目的地。

下圖說明透過臨機啟動API來啟用區段的端對端工作流程，包括每24小時在Platform中發生的區段工作。

![臨機啟動](../assets/api/ad-hoc-activation/ad-hoc-activation-overview.png)

>[!NOTE]
>
>僅支援隨選對象啟動 [批次檔案型目的地](../destination-types.md#file-based).

## 使用案例 {#use-cases}

### Flash銷售或促銷

一家線上零售商正在準備有限的快閃銷售，希望在短時間內通知客戶。 透過Experience Platform臨機啟動API，行銷團隊可以隨選匯出區段，並快速傳送促銷電子郵件給客戶群。


### 最新事件或突發新聞

酒店預計接下來幾天會有惡劣的天氣，團隊想要快速通知到達的客人，以便他們能據此進行規劃。 行銷團隊可使用Experience Platform臨機啟動API，依需求匯出區段，並通知客人。

### 整合測試

IT經理可以使用Experience Platform臨機啟動API，依需求匯出區段，以便測試其與Adobe Experience Platform的自訂整合，並確保一切正常運作。


## 護欄 {#guardrails}

使用臨機啟動API時，請記住下列護欄。

* 目前，每個臨機啟動工作最多可啟動20個區段。 嘗試啟動每個作業超過20個區段會導致作業失敗。 此行為在未來版本中可能會有所變更。
* 臨機啟動作業無法與已排程的同時執行 [區段匯出作業](../../segmentation/api/export-jobs.md). 在執行臨機啟動工作之前，請確定排程的區段匯出工作已完成。 請參閱 [目標資料流監視](../../dataflows/ui/monitor-destinations.md) 以了解如何監控啟動流程的狀態。 例如，如果激活資料流顯示 **[!UICONTROL 處理]** 狀態，請等待它完成，再執行臨機啟動工作。
* 每個區段請勿執行多個同時的臨機啟動工作。

## 區段考量事項 {#segmentation-considerations}

Adobe Experience Platform每24小時執行一次已排程的分段工作。 臨機啟動API會根據最新的細分結果執行。

## 步驟1:必要條件 {#prerequisites}

呼叫Adobe Experience Platform API之前，請務必符合下列必要條件：

* 您有可存取Adobe Experience Platform的IMS組織帳戶。
* 您的Experience Platform帳戶具有 `developer` 和 `user` 為Adobe Experience Platform API產品設定檔啟用的角色。 請連絡您的 [Admin Console](../../access-control/home.md) 管理員來為您的帳戶啟用這些角色。
* 你有Adobe ID。 如果您沒有Adobe ID，請前往 [Adobe開發人員控制台](https://developer.adobe.com/console) 並建立新帳戶。

## 步驟2:收集憑據 {#credentials}

若要呼叫Platform API，您必須先完成 [驗證教學課程](https://www.adobe.com/go/platform-api-authentication-en). 完成驗證教學課程後，所有Experience PlatformAPI呼叫中每個必要標題的值都會顯示，如下所示：

* 授權：承載 `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Experience Platform中的資源可以隔離至特定虛擬沙箱。 在向Platform API提出的請求中，您可以指定要執行操作之沙箱的名稱和ID。 這些是選用參數。

* x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>如需Experience Platform中沙箱的詳細資訊，請參閱 [沙箱概述檔案](../../sandboxes/home.md).

所有包含裝載(POST、PUT、PATCH)的請求都需要其他媒體類型標題：

* Content-Type: `application/json`

## 步驟3:在Platform UI中建立啟動流程 {#activation-flow}

您必須先在平台UI中針對所選目的地設定啟動流程，才能透過臨機啟動API啟用區段。

這包括進入啟動工作流程、選取區段、設定排程和啟動這些區段。

如需如何為批次目的地設定啟動流程的詳細指示，請參閱下列教學課程： [啟用受眾資料以批次設定檔匯出目的地](../ui/activate-batch-profile-destinations.md).

## 步驟4:取得最新的區段匯出工作ID {#segment-export-id}

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

在執行臨機啟動工作之前，請確定您區段的已排程區段匯出工作已完成。 請參閱 [目標資料流監視](../../dataflows/ui/monitor-destinations.md) 以了解如何監控啟動流程的狀態。 例如，如果激活資料流顯示 **[!UICONTROL 處理]** 狀態，請等待它完成，再執行臨機啟動工作。

區段匯出工作完成後，您即可觸發啟動。

>[!NOTE]
>
>目前，每個臨機啟動工作最多可啟動20個區段。 嘗試啟動每個作業超過20個區段會導致作業失敗。 此行為在未來版本中可能會有所變更。

### 請求

```shell
curl -X POST https://platform.adobe.io/data/core/activation/disflowprovider/adhocrun \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
| <ul><li>`destinationId1`</li><li>`destinationId2`</li></ul> | 您要啟用區段的目的地例項ID。 |
| <ul><li>`segmentId1`</li><li>`segmentId2`</li><li>`segmentId3`</li></ul> | 您要啟用至所選目的地之區段的ID。 |
| <ul><li>`exportId1`</li></ul> | 回應中傳回的ID為 [區段匯出](../../segmentation/api/export-jobs.md#retrieve-list) 工作。 請參閱 [步驟4:取得最新的區段匯出工作ID](#segment-export-id) 以取得如何找到此ID的指示。 |

### 回應

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


## API錯誤處理

目標SDK API端點會遵循一般Experience PlatformAPI錯誤訊息原則。 請參閱 [API狀態代碼](https://experienceleague.adobe.com/docs/experience-platform/landing/troubleshooting.html?lang=en#api-status-codes) 和 [請求標題錯誤](https://experienceleague.adobe.com/docs/experience-platform/landing/troubleshooting.html?lang=en#request-header-errors) （位於平台疑難排解指南中）。
