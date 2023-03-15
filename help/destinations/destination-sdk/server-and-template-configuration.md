---
description: 伺服器和模板規格可通過公共端點「/authoring/destination-servers」在Adobe Experience Platform Destination SDK中配置。
title: 伺服器和模板規格的配置選項，Destination SDK
exl-id: cf493ed5-0bdb-4b90-b84d-73926a566a2a
source-git-commit: a08201c4bc71b0e37202133836e9347ed4d3cd6b
workflow-type: tm+mt
source-wordcount: '419'
ht-degree: 7%

---

# 串流目的地伺服器和範本規格的設定選項

## 總覽 {#overview}

伺服器和模板規格可通過公共端點在Adobe Experience Platform Destination SDK中配置 `/authoring/destination-servers`. 閱讀 [目的地API端點作業](./destination-server-api.md) 可在端點上執行的操作的完整清單。

## 伺服器規格 {#server-specs}

![突出顯示伺服器配置](./assets/server-configuration.png)

客戶將能透過HTTP匯出功能，將資料從Adobe Experience Platform啟動至您的目的地。 伺服器配置包含接收消息的伺服器（您這邊的伺服器）的相關資訊。

此程式會以一系列HTTP訊息的形式將使用者資料傳送至您的目的地平台。 以下參數構成HTTP伺服器規格模板。

| 參數 | 類型 | 說明 |
|---|---|---|
| `name` | 字串 | *必填。* 代表您伺服器的好記名稱，只顯示給Adobe。 合作夥伴或客戶看不到此名稱。 範例 `Moviestar destination server`. |
| `destinationServerType` | 字串 | *必填。* 設為 `URL_BASED` 用於串流目的地。 |
| `templatingStrategy` | 字串 | *必填.* <ul><li>使用 `PEBBLE_V1` 如果您在 `value` 欄位。 如果您的端點如下所示，請使用此選項： `https://api.moviestar.com/data/{{customerData.region}}/items` </li><li> 使用 `NONE` 如果Adobe端不需要轉換，例如，如果您有如下的端點： `https://api.moviestar.com/data/items` </li></ul> |
| `value` | 字串 | *必填。* 填入Experience Platform應連線之API端點的位址。 |

{style="table-layout:auto"}

## 模板規格 {#template-specs}

![醒目提示範本設定](./assets/template-configuration.png)

範本規格可讓您設定如何將匯出的訊息格式化至目的地。 Adobe使用類似以下的範本語言： [金子](https://jinja.palletsprojects.com/en/2.11.x/) 將XDM架構的欄位轉換為目的地支援的格式。 如需轉換的詳細資訊，請造訪下列連結：

* [訊息格式](./message-format.md)
* [使用範本語言進行身分、屬性和區段成員資格轉換 ](./message-format.md#using-templating)

>[!TIP]
>
>Adobe提供 [開發人員工具](./create-template.md) 可協助您建立和測試訊息轉換範本。

## 串流目的地範例設定  {#example-configuration}

```json
{
   "name":"Moviestar destination server",
   "destinationServerType":"URL_BASED",
   "urlBasedDestination":{
      "url":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"https://api.moviestar.com/data/{{customerData.endpointRegion}}/items"
      }
   },
   "httpTemplate":{
      "httpMethod":"POST",
      "requestBody":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{ \"attributes\": [ {% for ns in [\"external_id\", \"yourdestination_id\"] %} {% if input.profile.identityMap[ns] is not empty and first_namespace_encountered %} , {% endif %} {% set first_namespace_encountered = true %} {% for identity in input.profile.identityMap[ns]%} { \"{{ ns }}\": \"{{ identity.id }}\" {% if input.profile.segmentMembership.ups is not empty %} , \"AEPSegments\": { \"add\": [ {% for segment in input.profile.segmentMembership.ups %} {% if segment.value.status == \"realized\" or segment.value.status == \"existing\" %} {% if added_segment_found %} , {% endif %} {% set added_segment_found = true %} \"{{ destination.segmentAliases[segment.key] }}\" {% endif %} {% endfor %} ], \"remove\": [ {% for segment in input.profile.segmentMembership.ups %} {% if segment.value.status == \"exited\" %} {% if removed_segment_found %} , {% endif %} {% set removed_segment_found = true %} \"{{ destination.segmentAliases[segment.key] }}\" {% endif %} {% endfor %} ] } {% set removed_segment_found = false %} {% set added_segment_found = false %} {% endif %} {% if input.profile.attributes is not empty %} , {% endif %} {% for attribute in input.profile.attributes %} \"{{ attribute.key }}\": {% if attribute.value is empty %} null {% else %} \"{{ attribute.value.value }}\" {% endif %} {% if not loop.last%} , {% endif %} {% endfor %} } {% if not loop.last %} , {% endif %} {% endfor %} {% endfor %} ] }"
      },
      "contentType":"application/json"
   }
}
```

| 參數 | 類型 | 說明 |
|---|---|---|
| `httpMethod` | 字串 | *必填。* Adobe將用於呼叫伺服器的方法。 選項包括 `GET`, `PUT`, `POST`, `DELETE`, `PATCH`. |
| `templatingStrategy` | 字串 | *必填。* 使用 `PEBBLE_V1`. |
| `value` | 字串 | *必填。* 此字串是字元逸出版本，可將Platform客戶的資料轉換為服務預期的格式。 <br> 如需如何編寫範本的資訊，請閱讀 [使用模板部分](./message-format.md#using-templating). <br> 如需字元逸出的詳細資訊，請參閱 [RFC JSON標準，第七節](https://tools.ietf.org/html/rfc8259#section-7). <br> 如需簡單轉換的範例，請參閱 [設定檔屬性](./message-format.md#attributes) 轉換。 |
| `contentType` | 字串 | *必填。* 伺服器接受的內容類型。 此值很可能 `application/json`. |

{style="table-layout:auto"}