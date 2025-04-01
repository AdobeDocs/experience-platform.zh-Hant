---
keywords: Experience Platform；目的地api；臨機啟動；臨機啟動對象
solution: Experience Platform
title: 透過臨機啟動API將對象啟動至批次目的地
description: 本文說明透過臨機啟動API啟動對象的端對端工作流程，包括在啟動前進行的細分工作。
type: Tutorial
exl-id: 1a09f5ff-0b04-413d-a9f6-57911a92b4e4
source-git-commit: f01a044d3d12ef457c6242a0b93acbfeeaf48588
workflow-type: tm+mt
source-wordcount: '1612'
ht-degree: 0%

---

# 透過臨機啟動API依需求啟用批次目的地的對象

>[!IMPORTANT]
>
>完成Beta階段後，[!DNL ad-hoc activation API]現在可供所有Experience Platform客戶普遍使用(GA)。 在GA版本中，API已升級至版本2。 步驟4 （[取得最新的對象匯出工作ID](#segment-export-id)）不再是必要步驟，因為API不再需要匯出工作ID。
>
>如需詳細資訊，請參閱本教學課程下方[執行臨機操作啟動工作](#activation-job)。

## 概觀 {#overview}

臨機啟動API可讓行銷人員針對需要立即啟動的情況，以快速且有效率的方式以程式設計方式將對象啟動至目的地。

使用臨機啟動API將完整檔案匯出至您想要的檔案接收系統。 僅[批次檔案型目的地](../destination-types.md#file-based)支援隨選對象啟用。

下圖說明透過臨機啟動API啟動對象的端對端工作流程，包括每24小時在Platform中發生的細分工作。

![臨機啟動](../assets/api/ad-hoc-activation/ad-hoc-activation-overview.png)

## 使用案例 {#use-cases}

### Flash銷售或促銷活動

線上retailer正在準備進行限量搶購，並希望在短時間內通知客戶。 透過Experience Platform隨選啟用API，行銷團隊可以依需求匯出對象，並快速傳送促銷電子郵件給客戶群。

### 最新事件或突發新聞

飯店期望在接下來的幾天內遇到惡劣天氣，而團隊想要快速通知到來的客人，以便他們做出相應的計畫。 行銷團隊可以使用Experience Platform隨選啟動API來隨選匯出受眾，並通知來賓。

### 整合測試

IT管理員可使用Experience Platform隨選啟用API來隨選匯出對象，以便測試其與Adobe Experience Platform的自訂整合，並確保一切都正常運作。

## 護欄 {#guardrails}

使用臨機啟動API時，請牢記以下護欄。

* 目前，每個隨選啟動工作最多可啟動80個對象。 嘗試為每個工作啟用超過80個對象會導致工作失敗。 未來版本可能會對此行為有所變更。
* 臨機啟動工作無法與排程的[對象匯出工作](../../segmentation/api/export-jobs.md)並行執行。 在執行臨機啟動工作之前，請確定已排程的對象匯出工作已完成。 如需如何監視啟用流程狀態的資訊，請參閱[目的地資料流程監視](../../dataflows/ui/monitor-destinations.md)。 例如，如果您的啟動資料流顯示&#x200B;**[!UICONTROL 正在處理]**&#x200B;狀態，請等待它完成後再執行臨機操作啟動工作。
* 請勿對每個對象執行多個同時的臨機啟動工作。

## 分段考量事項 {#segmentation-considerations}

Adobe Experience Platform每24小時執行一次排程的區段工作。 臨機啟動API會根據最新的分段結果執行。

## 步驟1：必要條件 {#prerequisites}

呼叫Adobe Experience Platform API之前，請確定您符合下列必要條件：

* 您擁有可存取Adobe Experience Platform的組織帳戶。
* 您的Experience Platform帳戶已針對Adobe Experience Platform API產品設定檔啟用`developer`和`user`角色。 請連絡您的[Admin Console](../../access-control/home.md)管理員，為您的帳戶啟用這些角色。
* 您有Adobe ID。 如果您沒有Adobe ID，請前往[Adobe Developer Console](https://developer.adobe.com/console)並建立新帳戶。

## 步驟2：收集認證 {#credentials}

若要呼叫Platform API，您必須先完成[驗證教學課程](https://www.adobe.com/go/platform-api-authentication-en)。 完成驗證教學課程，在所有Experience Platform API呼叫中提供每個必要標題的值，如下所示：

* 授權：持有人`{ACCESS_TOKEN}`
* x-api-key： `{API_KEY}`
* x-gw-ims-org-id： `{ORG_ID}`

Experience Platform中的資源可以隔離到特定的虛擬沙箱。 在對Platform API的請求中，您可以指定將執行作業的沙箱名稱和ID。 這些是選用引數。

* x-sandbox-name： `{SANDBOX_NAME}`

>[!NOTE]
>
>如需Experience Platform中沙箱的詳細資訊，請參閱[沙箱概觀檔案](../../sandboxes/home.md)。

包含裝載(POST、PUT、PATCH)的所有請求都需要額外的媒體型別標頭：

* Content-Type： `application/json`

## 步驟3：在Platform UI中建立啟動流程 {#activation-flow}

您必須先在平台UI中針對所選目的地設定啟用流程，才能透過臨機啟動API啟用對象。

這包括進入啟用工作流程、選取您的對象、設定排程並啟用它們。 您可以使用UI或API來建立啟用流程：

* [使用Platform UI建立批次設定檔匯出目的地的啟用流程](../ui/activate-batch-profile-destinations.md)
* [使用流程服務API來連線至批次設定檔匯出目的地並啟用資料](../api/connect-activate-batch-destinations.md)

## 步驟4：取得最新的對象匯出作業ID （v2中不需要） {#segment-export-id}

>[!IMPORTANT]
>
>在臨機啟動API v2中，您不需要取得最新的對象匯出工作ID。 您可以略過此步驟，繼續下一個步驟。

當您為批次目的地設定啟動流程後，排程的分段工作會每24小時自動執行一次。

您必須先取得最新對象匯出工作的ID，才能執行隨選啟動工作。 您必須在臨機啟動工作請求中傳遞此ID。

依照[這裡](../../segmentation/api/export-jobs.md#retrieve-list)說明的指示，擷取所有對象匯出工作的清單。

在回應中，尋找包含下列結構描述屬性的第一個記錄。

```
"schema":{
   "name":"_xdm.context.profile"
}
```

對象匯出工作ID位於`id`屬性中，如下所示。

![對象匯出工作ID](../assets/api/ad-hoc-activation/segment-export-job-id.png)


## 步驟5：執行臨機操作啟動工作 {#activation-job}

Adobe Experience Platform每24小時執行一次排程的區段工作。 臨機啟動API會根據最新的分段結果執行。

>[!IMPORTANT]
>
>請注意下列一次性限制：在執行臨機操作啟用工作之前，請確定根據您在[步驟3 — 在Platform UI](#activation-flow)中建立啟用流程中所設定的排程，從第一次啟用對象的那一刻起已過去至少一個小時。

在執行臨機啟動工作之前，請確定您對象的排程對象匯出工作已完成。 如需如何監視啟用流程狀態的資訊，請參閱[目的地資料流程監視](../../dataflows/ui/monitor-destinations.md)。 例如，如果您的啟動資料流顯示&#x200B;**[!UICONTROL 正在處理]**&#x200B;狀態，請等待它完成後再執行臨機操作啟動工作以匯出完整檔案。

對象匯出工作完成後，您可以觸發啟動。

>[!NOTE]
>
>目前，每個隨選啟動工作最多可啟動80個對象。 嘗試為每個工作啟用超過80個對象會導致工作失敗。 未來版本可能會對此行為有所變更。

### 請求 {#request}

>[!IMPORTANT]
>
>您必須在要求中加入`Accept: application/vnd.adobe.adhoc.activation+json; version=2`標頭，才能使用臨機啟動API v2。

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
| <ul><li>`destinationId1`</li><li>`destinationId2`</li></ul> | 您想要啟用對象之目的地執行個體的ID。 您可以導覽至&#x200B;**[!UICONTROL 目的地]** > **[!UICONTROL 瀏覽]**&#x200B;標籤，然後按一下所需的目的地列，在右側邊欄中叫出目的地ID，從Platform UI取得這些ID。 如需詳細資訊，請閱讀[目的地工作區檔案](/help/destinations/ui/destinations-workspace.md#browse)。 |
| <ul><li>`segmentId1`</li><li>`segmentId2`</li><li>`segmentId3`</li></ul> | 您要啟用至所選目的地的對象ID。 您可以使用臨機API匯出平台產生的對象以及外部（自訂上傳）對象。 啟用外部對象時，請使用系統產生的ID，而非對象ID。 您可以在對象UI的對象摘要檢視中找到系統產生的ID。<br> ![檢視不應選取的對象ID。](/help/destinations/assets/api/ad-hoc-activation/audience-id-do-not-use.png "檢視不應選取的對象ID。"){width="100" zoomable="yes"} <br> ![應該使用的系統產生對象ID的檢視。](/help/destinations/assets/api/ad-hoc-activation/system-generated-id-to-use.png "應該使用的系統產生對象ID的檢視。"){width="100" zoomable="yes"} |

{style="table-layout:auto"}

### 使用匯出ID的請求 {#request-export-ids}

<!--

>[!IMPORTANT]
>
>**Deprecated request type**. This example type describes the request type for the API version 1. In the v2 of the ad-hoc activation API, you do not need to include the latest audience export job ID.

-->

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
| <ul><li>`destinationId1`</li><li>`destinationId2`</li></ul> | 您想要啟用對象之目的地執行個體的ID。 您可以導覽至&#x200B;**[!UICONTROL 目的地]** > **[!UICONTROL 瀏覽]**&#x200B;標籤，然後按一下所需的目的地列，在右側邊欄中叫出目的地ID，從Platform UI取得這些ID。 如需詳細資訊，請閱讀[目的地工作區檔案](/help/destinations/ui/destinations-workspace.md#browse)。 |
| <ul><li>`segmentId1`</li><li>`segmentId2`</li><li>`segmentId3`</li></ul> | 您要啟用至所選目的地的對象ID。 |
| <ul><li>`exportId1`</li></ul> | [對象匯出](../../segmentation/api/export-jobs.md#retrieve-list)作業的回應中傳回的ID。 請參閱[步驟4：取得最新的對象匯出工作ID](#segment-export-id)，瞭解如何尋找此ID的說明。 |

{style="table-layout:auto"}

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
| `segment` | 已啟動受眾的ID。 |
| `order` | 對象啟用的目的地識別碼。 |
| `statusURL` | 啟動流程的狀態URL。 您可以使用[流量服務API](../../sources/tutorials/api/monitor.md)來追蹤流量進度。 |

{style="table-layout:auto"}

## API錯誤處理 {#api-error-handling}

Destination SDK API端點遵循一般Experience Platform API錯誤訊息原則。 請參閱Platform疑難排解指南中的[API狀態碼](../../landing/troubleshooting.md#api-status-codes)和[請求標頭錯誤](../../landing/troubleshooting.md#request-header-errors)。

### Ad Hoc Activation API專屬的API錯誤代碼和訊息 {#specific-error-messages}

使用臨機啟動API時，您可能會遇到特定於此API端點的錯誤訊息。 請檢閱表格以瞭解如何在它們出現時解決它們。

| 錯誤訊息 | 解決方法 |
|---------|----------|
| 已對執行識別碼為`flow run ID`的訂單`dataflow ID`的對象`segment ID`執行中 | 此錯誤訊息表示對象目前正在進行臨機啟動流程。 再次觸發啟動工作前，請等候工作完成。 |
| 區段`<segment name>`不是此資料流的一部分或超出排程範圍！ | 此錯誤訊息指出您選取要啟用的對象未對應至資料流，或是為對象設定的啟用排程已過期或尚未開始。 檢查對象是否確實對應至資料流，並確認對象啟用排程與目前日期重疊。 |

## 相關資訊 {#related-information}

* [使用流程服務API連線到批次目的地並啟用資料](/help/destinations/api/connect-activate-batch-destinations.md)
* [(Beta)使用Experience Platform UI隨選將檔案匯出至批次目的地](/help/destinations/ui/export-file-now.md)