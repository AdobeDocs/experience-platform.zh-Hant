---
description: 瞭解如何格式化傳送至您端點的HTTP請求。 使用/authoring/destination-servers端點在Adobe Experience Platform Destination SDK中設定目的地伺服器範本規格。
title: 使用Destination SDK建立之目的地的範本規格
exl-id: 066781c8-0af0-4958-b62f-194c6ba13f3a
source-git-commit: b4334b4f73428f94f5a7e5088f98e2459afcaf3c
workflow-type: tm+mt
source-wordcount: '523'
ht-degree: 4%

---

# 以Destination SDK建立之目的地的範本規格

使用目的地伺服器設定的範本規格部分來設定如何格式化傳送到目的地的HTTP要求。

在範本規格中，您可以定義如何在XDM結構描述和平台支援的格式之間轉換設定檔屬性欄位。

範本規格是即時（串流）目的地的目的地伺服器設定的一部分。

若要瞭解此元件在何處適合使用Destination SDK建立的整合，請參閱 [設定選項](../configuration-options.md) 檔案或請參閱操作說明指南 [使用Destination SDK設定串流目的地](../../guides/configure-destination-instructions.md#create-server-template-configuration).

您可以透過 `/authoring/destination-servers` 端點。 請參閱下列API參考頁面，以取得詳細的API呼叫範例，您可在此範例設定本頁面中顯示的元件。

* [建立目的地伺服器組態](../../authoring-api/destination-server/create-destination-server.md)
* [更新目的地伺服器設定](../../authoring-api/destination-server/update-destination-server.md)

>[!IMPORTANT]
>
>Destination SDK支援的所有引數名稱和值如下 **區分大小寫**. 為避免區分大小寫錯誤，請完全依照檔案中所示使用引數名稱和值。

## 支援的整合型別 {#supported-integration-types}

如需瞭解哪些型別的整合支援本頁面所述功能的詳細資訊，請參閱下表。

| 整合型別 | 支援功能 |
|---|---|
| 即時（串流）整合 | 是 |
| 檔案式（批次）整合 | 無 |

## 設定範本規格 {#configure-template-spec}

Adobe使用類似以下的範本化語言 [金家](https://jinja.palletsprojects.com/en/2.11.x/) 將欄位從XDM結構描述轉換為目的地支援的格式。

![醒目提示的範本設定](../../assets/functionality/destination-server/template-configuration.png)

如需轉換的詳細資訊，請造訪下列連結：

* [訊息格式](message-format.md)
* [使用範本語言進行身分、屬性和對象成員資格轉換](message-format.md#using-templating)

>[!TIP]
>
>Adobe選件 [開發人員工具](../../testing-api/streaming-destinations/create-template.md) 可協助您建立和測試訊息轉換範本。

請參閱以下的HTTP要求範本範例，以及各個引數的說明。

```json
{
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
| `httpMethod` | 字串 | *必要.* Adobe將在對伺服器呼叫中使用的方法。 支援的方法： `GET`， `PUT`， `POST`， `DELETE`， `PATCH`. |
| `templatingStrategy` | 字串 | *必要.* 使用 `PEBBLE_V1`. |
| `value` | 字串 | *必要.* 此字串是範本的字元逸出版本，可將Platform傳送的HTTP要求格式化為目的地預期的格式。 <br> 如需如何撰寫範本的詳細資訊，請閱讀以下章節： [使用範本](message-format.md#using-templating). <br> 如需字元逸出的詳細資訊，請參閱 [RFC JSON標準，第七節](https://tools.ietf.org/html/rfc8259#section-7). <br> 如需簡單轉換的範例，請參閱 [設定檔屬性](message-format.md#attributes) 轉換。 |
| `contentType` | 字串 | *必要.* 您的伺服器接受的內容型別。 根據轉換範本產生的輸出型別，這可以是任何支援的 [HTTP應用程式內容型別](https://www.iana.org/assignments/media-types/media-types.xhtml#application). 在大多數情況下，此值應設為 `application/json`. |

{style="table-layout:auto"}

## 後續步驟 {#next-steps}

閱讀本文後，您應該更瞭解什麼是範本規格，以及如何進行設定。

若要深入瞭解其他目的地伺服器元件，請參閱下列文章：

* [以Destination SDK建立的目的地的伺服器規格](server-specs.md)
* [訊息格式](message-format.md)
* [檔案格式設定](file-formatting.md)
