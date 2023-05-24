---
description: 瞭解如何格式化發送到終結點的HTTP請求。 使用/authoring/destination-servers終結點在Adobe Experience Platform Destination SDK中配置目標伺服器模板規範。
title: 使用Destination SDK建立的目標的模板規格
source-git-commit: 118ff85a9fceb8ee81dbafe2c381d365b813da29
workflow-type: tm+mt
source-wordcount: '524'
ht-degree: 4%

---


# 使用Destination SDK建立的目標的模板規範

使用目標伺服器配置的模板規範部分配置如何格式化發送到目標的HTTP請求。

在模板規範中，可以定義如何在XDM架構和平台支援的格式之間轉換配置檔案屬性欄位。

模板規範是即時（流）目標的目標伺服器配置的一部分。

要瞭解此元件在與Destination SDK建立的整合中的位置，請參閱 [配置選項](../configuration-options.md) 文檔，或參閱有關如何 [使用Destination SDK配置流目標](../../guides/configure-destination-instructions.md#create-server-template-configuration)。

您可以通過 `/authoring/destination-servers` 端點。 有關詳細的API調用示例，請參閱以下API參考頁，在這些示例中可以配置此頁中顯示的元件。

* [建立目標伺服器配置](../../authoring-api/destination-server/create-destination-server.md)
* [更新目標伺服器配置](../../authoring-api/destination-server/update-destination-server.md)

>[!IMPORTANT]
>
>Destination SDK支援的所有參數名和值均 **區分大小寫**。 為避免區分大小寫錯誤，請完全按文檔所示使用參數名稱和值。

## 支援的整合類型 {#supported-integration-types}

有關哪些類型的整合支援本頁所述功能的詳細資訊，請參閱下表。

| 整合類型 | 支援功能 |
|---|---|
| 即時（流）整合 | 是 |
| 基於檔案（批處理）的整合 | 無 |

## 配置模板規範 {#configure-template-spec}

Adobe使用類似於 [金賈](https://jinja.palletsprojects.com/en/2.11.x/) 將XDM架構中的欄位轉換為目標支援的格式。

![已突出顯示模板配置](../../assets/functionality/destination-server/template-configuration.png)

有關轉換的詳細資訊，請訪問以下連結：

* [訊息格式](message-format.md)
* [使用模板語言進行身份、屬性和段成員身份轉換 ](message-format.md#using-templating)

>[!TIP]
>
>Adobe提供 [開發者工具](../../testing-api/streaming-destinations/create-template.md) 幫助您建立和test消息轉換模板。

請參見下面的HTTP請求模板示例以及每個單獨參數的說明。

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
| `httpMethod` | 字串 | *必填。* Adobe在對伺服器的調用中使用的方法。 支援的方法： `GET`。 `PUT`。 `POST`。 `DELETE`。 `PATCH`。 |
| `templatingStrategy` | 字串 | *必填。* 使用 `PEBBLE_V1`. |
| `value` | 字串 | *必填。* 此字串是模板的字元轉義版本，該模板將平台發送的HTTP請求格式化為目標所期望的格式。 <br> 有關如何編寫模板的資訊，請閱讀上 [使用模板](message-format.md#using-templating)。 <br> 有關字元轉義的詳細資訊，請參閱 [RFC JSON標準，第7節](https://tools.ietf.org/html/rfc8259#section-7)。 <br> 有關簡單轉換的示例，請參閱 [配置檔案屬性](message-format.md#attributes) 轉換。 |
| `contentType` | 字串 | *必填。* 伺服器接受的內容類型。 根據轉換模板生成的輸出類型，這可以是支援的 [HTTP應用程式內容類型](https://www.iana.org/assignments/media-types/media-types.xhtml#application)。 在大多數情況下，此值應設定為 `application/json`。 |

{style="table-layout:auto"}

## 後續步驟 {#next-steps}

閱讀本文後，您應更好地瞭解模板規範是什麼以及如何配置它。

要瞭解有關其他目標伺服器元件的詳細資訊，請參閱以下文章：

* [使用Destination SDK建立的目標的伺服器規格](server-specs.md)
* [訊息格式](message-format.md)
* [檔案格式配置](file-formatting.md)