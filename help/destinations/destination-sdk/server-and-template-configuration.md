---
description: 伺服器和模板規範可通過公共端點「/創作/目標伺服器」在Adobe Experience Platform Destination SDK中配置。
title: 伺服器和模板規範的配置選項Destination SDK
exl-id: cf493ed5-0bdb-4b90-b84d-73926a566a2a
source-git-commit: a08201c4bc71b0e37202133836e9347ed4d3cd6b
workflow-type: tm+mt
source-wordcount: '425'
ht-degree: 8%

---

# 流目標伺服器和模板規範的配置選項

## 總覽 {#overview}

伺服器和模板規範可通過公共端點在Adobe Experience Platform Destination SDK中配置 `/authoring/destination-servers`。 閱讀 [目標API終結點操作](./destination-server-api.md) 可在端點上執行的操作的完整清單。

## 伺服器規格 {#server-specs}

![已突出顯示伺服器配置](./assets/server-configuration.png)

客戶將能夠通過HTTP導出將資料從Adobe Experience Platform激活到您的目標。 伺服器配置包含有關伺服器接收消息的資訊（伺服器位於您的一側）。

此進程將用戶資料作為一系列HTTP消息傳送到目標平台。 下面的參數構成HTTP伺服器規範模板。

| 參數 | 類型 | 說明 |
|---|---|---|
| `name` | 字串 | *必填。* 表示伺服器的友好名稱，僅對Adobe可見。 合作夥伴或客戶看不到此名稱。 範例 `Moviestar destination server`. |
| `destinationServerType` | 字串 | *必填。* 設定為 `URL_BASED` 流目標。 |
| `templatingStrategy` | 字串 | *必填.* <ul><li>使用 `PEBBLE_V1` 在 `value` 的子菜單。 如果您具有端點，如： `https://api.moviestar.com/data/{{customerData.region}}/items` </li><li> 使用 `NONE` 如果Adobe端不需要轉換，例如，如果您有一個端點，如： `https://api.moviestar.com/data/items` </li></ul> |
| `value` | 字串 | *必填。* 填寫Experience Platform應連接到的API終結點的地址。 |

{style=&quot;table-layout:auto&quot;}

## 模板規格 {#template-specs}

![已突出顯示模板配置](./assets/template-configuration.png)

模板規範允許您配置如何將導出的消息格式化到目標。 Adobe使用類似於 [金賈](https://jinja.palletsprojects.com/en/2.11.x/) 將XDM架構中的欄位轉換為目標支援的格式。 有關轉換的詳細資訊，請訪問以下連結：

* [訊息格式](./message-format.md)
* [使用模板語言進行身份、屬性和段成員身份轉換 ](./message-format.md#using-templating)

>[!TIP]
>
>Adobe提供 [開發者工具](./create-template.md) 幫助您建立和test消息轉換模板。

## 流目標示例配置  {#example-configuration}

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
| `httpMethod` | 字串 | *必填。* Adobe在對伺服器的調用中使用的方法。 選項為 `GET`。 `PUT`。 `POST`。 `DELETE`。 `PATCH`。 |
| `templatingStrategy` | 字串 | *必填。* 使用 `PEBBLE_V1`. |
| `value` | 字串 | *必填。* 此字串是字元轉義版本，它將平台客戶的資料轉換為服務所需的格式。 <br> 有關如何編寫模板的資訊，請閱讀 [使用模板部](./message-format.md#using-templating)。 <br> 有關字元轉義的詳細資訊，請參閱 [RFC JSON標準，第7節](https://tools.ietf.org/html/rfc8259#section-7)。 <br> 有關簡單轉換的示例，請參閱 [配置檔案屬性](./message-format.md#attributes) 轉換。 |
| `contentType` | 字串 | *必填。* 伺服器接受的內容類型。 此值極有可能 `application/json`。 |

{style=&quot;table-layout:auto&quot;&quot;