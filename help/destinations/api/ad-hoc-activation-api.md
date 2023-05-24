---
keywords: Experience Platform；目標api;ad-hoc激活；激活段ad-hoc
solution: Experience Platform
title: 通過即席激活API激活受眾段以批處理目標
description: 本文闡述了通過即席激活API激活受眾段的端到端工作流，包括激活前發生的分段作業。
type: Tutorial
exl-id: 1a09f5ff-0b04-413d-a9f6-57911a92b4e4
source-git-commit: 81f48de908b274d836f551bec5693de13c5edaf1
workflow-type: tm+mt
source-wordcount: '1553'
ht-degree: 1%

---

# 通過即席激活API按需激活受眾段以批處理目標

>[!IMPORTANT]
>
>完成測試階段後， [!DNL ad-hoc activation API] 現已正式面向所有Experience Platform客戶。 在GA版本中，API已升級到版本2。 步驟4([獲取最新段導出作業ID](#segment-export-id))不再需要，因為API不再需要導出ID。
>
>請參閱 [運行即席激活作業](#activation-job) 詳細資訊，請參見本教程的下面。

## 總覽 {#overview}

該即席激活API允許營銷者以快速和有效的方式以寫程式方式將受眾段激活到目的地，以用於需要立即激活的情況。

使用即席激活API將完整檔案導出到所需的檔案接收系統。 僅支援即席受眾激活 [基於批檔案的目標](../destination-types.md#file-based)。

下圖說明了通過即席激活API激活段的端到端工作流，包括每24小時在平台中發生的分段作業。

![自組織激活](../assets/api/ad-hoc-activation/ad-hoc-activation-overview.png)



## 使用案例 {#use-cases}

### Flash銷售或促銷

一家線上零售商正準備進行有限的閃購，希望在短時間通知客戶。 通過Experience Platform即席激活API，營銷團隊可以按需導出細分市場，並快速向客戶群發送促銷電子郵件。

### 時事或突發新聞

酒店預計接下來幾天天氣會非常惡劣，團隊希望盡快通知到達的客人，以便他們能做出相應的規劃。 營銷團隊可以使用Experience Platform即席激活API按需導出段並通知來賓。

### 整合測試

IT經理可以使用Experience Platform即席激活API按需導出段，因此他們可以test與Adobe Experience Platform的自定義整合，並確保一切正常工作。

## 護欄 {#guardrails}

使用即席激活API時，請記住以下護欄。

* 目前，每個即席激活作業最多可激活80個段。 嘗試激活每個作業超過80個段將導致作業失敗。 此行為在未來版本中可能會發生更改。
* Ad-hoc激活作業無法與計畫的並行運行 [段導出作業](../../segmentation/api/export-jobs.md)。 在運行即席激活作業之前，請確保計畫的段導出作業已完成。 請參閱 [目標資料流監視](../../dataflows/ui/monitor-destinations.md) 有關如何監視激活流狀態的資訊。 例如，如果激活資料流顯示 **[!UICONTROL 處理]** 狀態，等待其完成，然後運行即席激活作業。
* 每個段不要運行多個併發即席激活作業。

## 分段注意事項 {#segmentation-considerations}

Adobe Experience Platform每24小時運行一次分段作業。 基於最新分段結果運行ad-hoc激活API。

## 步驟1:先決條件 {#prerequisites}

在調用Adobe Experience PlatformAPI之前，請確保滿足以下先決條件：

* 您有一個組織帳戶，可以訪問Adobe Experience Platform。
* 您的Experience Platform帳戶 `developer` 和 `user` 為Adobe Experience PlatformAPI產品配置檔案啟用的角色。 聯繫您 [Admin Console](../../access-control/home.md) 管理員，以為您的帳戶啟用這些角色。
* 你有個Adobe ID。 如果你沒有Adobe ID，去 [Adobe Developer控制台](https://developer.adobe.com/console) 並建立新帳戶。

## 步驟2:收集憑據 {#credentials}

要調用平台API，必須先完成 [驗證教程](https://www.adobe.com/go/platform-api-authentication-en)。 完成Experience Platform教程將提供所有驗證API調用中每個必需標頭的值，如下所示：

* 授權：持 `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{ORG_ID}`

Experience Platform中的資源可以隔離到特定的虛擬沙箱。 在對平台API的請求中，可以指定操作將在其中進行的沙盒的名稱和ID。 這些是可選參數。

* x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>有關Experience Platform中沙箱的詳細資訊，請參見 [沙盒概述文檔](../../sandboxes/home.md)。

所有包含負載(POST、PUT、PATCH)的請求都需要附加的媒體類型報頭：

* Content-Type: `application/json`

## 第3步：在平台UI中建立激活流 {#activation-flow}

必須先在平台UI中為所選目標配置激活流，然後才能通過點對點激活API激活段。

這包括進入激活工作流、選擇段、配置調度並激活它們。 可以使用UI或API建立激活流：

* [使用平台UI建立用於批配置檔案導出目標的激活流](../ui/activate-batch-profile-destinations.md)
* [使用流服務API連接到批配置檔案導出目標並激活資料](../api/connect-activate-batch-destinations.md)

## 第4步：獲取最新段導出作業ID（v2中不需要） {#segment-export-id}

>[!IMPORTANT]
>
>在即席激活API的v2中，您不需要獲得最新的段導出作業ID。 您可以跳過此步驟並繼續下一步。

為批處理目標配置激活流後，計畫的分段作業每24小時自動運行一次。

在運行即席激活作業之前，必須獲取最新段導出作業的ID。 必須在即席激活作業請求中傳遞此ID。

按照說明進行操作 [這裡](../../segmentation/api/export-jobs.md#retrieve-list) 以檢索所有段導出作業的清單。

在響應中，查找包含以下架構屬性的第一條記錄。

```
"schema":{
   "name":"_xdm.context.profile"
}
```

段導出作業ID位於 `id` 屬性，如下所示。

![段導出作業ID](../assets/api/ad-hoc-activation/segment-export-job-id.png)


## 第5步：運行即席激活作業 {#activation-job}

Adobe Experience Platform每24小時運行一次分段作業。 基於最新分段結果運行ad-hoc激活API。

>[!IMPORTANT]
>
>請注意以下一次性約束：在運行即席激活作業之前，請確保從根據您在中設定的時間表首次激活段的那一刻起至少已經過20分鐘 [步驟3 — 在平台UI中建立激活流](#activation-flow)。

在運行即席激活作業之前，請確保已完成段的計畫段導出作業。 請參閱 [目標資料流監視](../../dataflows/ui/monitor-destinations.md) 有關如何監視激活流狀態的資訊。 例如，如果激活資料流顯示 **[!UICONTROL 處理]** 狀態，等待其完成，然後運行ad-hoc激活作業以導出完整檔案。

段導出作業完成後，可以觸發激活。

>[!NOTE]
>
>目前，每個即席激活作業最多可激活80個段。 嘗試激活每個作業超過80個段將導致作業失敗。 此行為在未來版本中可能會發生更改。

### 請求 {#request}

>[!IMPORTANT]
>
>必須包括 `Accept: application/vnd.adobe.adhoc.activation+json; version=2` 請求中的標頭，以便使用ad-hoc激活API的v2。

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
| <ul><li>`destinationId1`</li><li>`destinationId2`</li></ul> | 要激活段的目標實例的ID。 通過導航到 **[!UICONTROL 目標]** > **[!UICONTROL 瀏覽]** 頁籤，然後按一下所需的目標行以在右欄中顯示目標ID。 有關詳細資訊，請閱讀 [目標工作區文檔](/help/destinations/ui/destinations-workspace.md#browse)。 |
| <ul><li>`segmentId1`</li><li>`segmentId2`</li><li>`segmentId3`</li></ul> | 要激活到選定目標的段的ID。 |

{style="table-layout:auto"}

### 具有導出ID的請求（不建議使用） {#request-deprecated}

>[!IMPORTANT]
>
>**不建議使用的請求類型**。 此示例類型描述API版本1的請求類型。 在即席激活API的v2中，您不需要包括最新的段導出作業ID。

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
| <ul><li>`destinationId1`</li><li>`destinationId2`</li></ul> | 要激活段的目標實例的ID。 通過導航到 **[!UICONTROL 目標]** > **[!UICONTROL 瀏覽]** 頁籤，然後按一下所需的目標行以在右欄中顯示目標ID。 有關詳細資訊，請閱讀 [目標工作區文檔](/help/destinations/ui/destinations-workspace.md#browse)。 |
| <ul><li>`segmentId1`</li><li>`segmentId2`</li><li>`segmentId3`</li></ul> | 要激活到選定目標的段的ID。 |
| <ul><li>`exportId1`</li></ul> | 在響應中返回的ID [段出口](../../segmentation/api/export-jobs.md#retrieve-list) 工作。 請參閱 [第4步：獲取最新段導出作業ID](#segment-export-id) 有關如何查找此ID的說明。 |

{style="table-layout:auto"}

### 回應 {#response}

成功響應返回HTTP狀態200。

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
| `segment` | 已激活段的ID。 |
| `order` | 段被激活到的目標的ID。 |
| `statusURL` | 激活流的狀態URL。 您可以使用 [流服務API](../../sources/tutorials/api/monitor.md)。 |

{style="table-layout:auto"}

## API錯誤處理 {#api-error-handling}

Destination SDKAPI端點遵循常規Experience PlatformAPI錯誤消息原則。 請參閱 [API狀態代碼](../../landing/troubleshooting.md#api-status-codes) 和 [請求標頭錯誤](../../landing/troubleshooting.md#request-header-errors) 中。

### 特定於ad-hoc激活API的API錯誤代碼和消息 {#specific-error-messages}

使用點對點激活API時，可能遇到特定於此API終結點的錯誤消息。 查看表，瞭解當它們確實出現時如何解決它們。

| 錯誤訊息 | 解決方法 |
|---------|----------|
| 已運行段 `segment ID` 訂單 `dataflow ID` 運行id `flow run ID` | 此錯誤消息表示當前正在為段執行點對點激活流。 等待作業完成，然後再次觸發激活作業。 |
| 段 `<segment name>` 不是此資料流的一部分或超出計畫範圍！ | 此錯誤消息表示選定要激活的段未映射到資料流，或者為段設定的激活計畫已過期或尚未啟動。 檢查段是否確實映射到資料流，並驗證段激活計畫是否與當前日期重疊。 |

## 相關資訊 {#related-information}

* [使用流服務API連接到批處理目標並激活資料](/help/destinations/api/connect-activate-batch-destinations.md)
* [(Beta)使用Experience PlatformUI按需導出檔案到批處理目標](/help/destinations/ui/export-file-now.md)