---
description: 了解如何格式化傳送至端點的HTTP要求。 使用/authoring/destination-servers端點來配置Adobe Experience Platform Destination SDK中的目標伺服器模板規範。
title: 使用Destination SDK建立的目的地的範本規格
source-git-commit: 118ff85a9fceb8ee81dbafe2c381d365b813da29
workflow-type: tm+mt
source-wordcount: '524'
ht-degree: 4%

---


# 使用Destination SDK建立的目的地的範本規格

使用目標伺服器配置的模板規範部分配置如何格式化發送到目標的HTTP請求。

在範本規格中，您可以定義如何在XDM架構與您的平台支援的格式之間轉換設定檔屬性欄位。

範本規格是即時（串流）目的地的目的地伺服器設定的一部分。

若要了解此元件在透過Destination SDK建立的整合中的插入位置，請參閱 [配置選項](../configuration-options.md) 檔案，或參閱如何 [使用Destination SDK來設定串流目的地](../../guides/configure-destination-instructions.md#create-server-template-configuration).

您可以透過 `/authoring/destination-servers` 端點。 如需詳細API呼叫範例，請參閱下列API參考頁面，您可在其中設定本頁面所示的元件。

* [建立目標伺服器配置](../../authoring-api/destination-server/create-destination-server.md)
* [更新目標伺服器配置](../../authoring-api/destination-server/update-destination-server.md)

>[!IMPORTANT]
>
>Destination SDK支援的所有參數名稱和值均為 **區分大小寫**. 為避免區分大小寫錯誤，請使用參數名稱和值，如說明檔案所示。

## 支援的整合類型 {#supported-integration-types}

如需詳細資訊，請參閱下表以了解哪些類型的整合支援本頁面所述的功能。

| 整合類型 | 支援功能 |
|---|---|
| 即時（串流）整合 | 是 |
| 檔案式（批次）整合 | 無 |

## 配置模板規格 {#configure-template-spec}

Adobe使用類似以下的範本語言： [金子](https://jinja.palletsprojects.com/en/2.11.x/) 將XDM架構的欄位轉換為目的地支援的格式。

![醒目提示範本設定](../../assets/functionality/destination-server/template-configuration.png)

如需轉換的詳細資訊，請造訪下列連結：

* [訊息格式](message-format.md)
* [使用範本語言進行身分、屬性和區段成員資格轉換 ](message-format.md#using-templating)

>[!TIP]
>
>Adobe提供 [開發人員工具](../../testing-api/streaming-destinations/create-template.md) 可協助您建立和測試訊息轉換範本。

請參閱以下的HTTP要求範本範例，以及每個個別參數的說明。

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
| `httpMethod` | 字串 | *必填。* Adobe將用於呼叫伺服器的方法。 支援的方法： `GET`, `PUT`, `POST`, `DELETE`, `PATCH`. |
| `templatingStrategy` | 字串 | *必填。* 使用 `PEBBLE_V1`. |
| `value` | 字串 | *必填。* 此字串是範本的字元逸出版本，可將Platform傳送的HTTP要求格式化為目的地預期的格式。 <br> 如需如何撰寫範本的資訊，請閱讀 [使用模板](message-format.md#using-templating). <br> 如需字元逸出的詳細資訊，請參閱 [RFC JSON標準，第七節](https://tools.ietf.org/html/rfc8259#section-7). <br> 如需簡單轉換的範例，請參閱 [設定檔屬性](message-format.md#attributes) 轉換。 |
| `contentType` | 字串 | *必填。* 伺服器接受的內容類型。 根據轉換模板生成的輸出類型，這可以是任何受支援的輸出 [HTTP應用程式內容類型](https://www.iana.org/assignments/media-types/media-types.xhtml#application). 在大多數情況下，此值應設為 `application/json`. |

{style="table-layout:auto"}

## 後續步驟 {#next-steps}

閱讀本文後，您應該更清楚了解範本規格是什麼，以及如何設定範本規格。

若要進一步了解其他目標伺服器元件，請參閱下列文章：

* [使用Destination SDK建立的目的地的伺服器規格](server-specs.md)
* [訊息格式](message-format.md)
* [檔案格式設定](file-formatting.md)