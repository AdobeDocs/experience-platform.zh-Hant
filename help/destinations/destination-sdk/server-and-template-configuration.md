---
description: 伺服器和範本規格可透過通用端點「/authoring/destination-servers」，在Adobe Experience Platform Destination SDK中設定。
title: 目的地SDK中伺服器和範本規格的設定選項
exl-id: cf493ed5-0bdb-4b90-b84d-73926a566a2a
source-git-commit: bd65cfa557fb42d23022578b98bc5482e8bd50b1
workflow-type: tm+mt
source-wordcount: '411'
ht-degree: 7%

---

# 伺服器和模板規格的配置選項

## 概覽 {#overview}

伺服器和範本規格可透過通用端點`/authoring/destination-servers`在Adobe Experience Platform Destination SDK中設定。 如需可在端點上執行的完整操作清單，請參閱[目標API端點操作](./destination-server-api.md) 。

## 組態範例 {#example-configuration}

```json
{
   "name":"Moviestar destination server",
   "destinationServerType":"URL_BASED",
   "urlBasedDestination":{
      "url":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"https://api.moviestar.com/data/{{customerData.region}}/items"
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

## 伺服器規格 {#server-specs}

![突出顯示伺服器配置](./assets/server-configuration.png)

客戶將能透過HTTP匯出功能，將資料從Adobe Experience Platform啟動至您的目的地。 伺服器配置包含接收消息的伺服器（您這邊的伺服器）的相關資訊。

此程式會以一系列HTTP訊息的形式將使用者資料傳送至您的目的地平台。 以下參數構成HTTP伺服器規格模板。

| 參數 | 類型 | 說明 |
|---|---|---|
| `name` | 字串 | 代表您伺服器的好記名稱，只顯示給Adobe。 合作夥伴或客戶看不到此名稱。 範例 `Moviestar destination server`. |
| `destinationServerType` | 字串 | `URL_BASED` 是目前唯一可用的選項。 |
| `templatingStrategy` | 字串 | <ul><li>如果Adobe需要轉換下方`value`欄位中的URL，請使用`PEBBLE_V1`。 如果您的端點如下所示，請使用此選項：`https://api.moviestar.com/data/{{customerData.region}}/items` </li><li> 如果Adobe端不需要轉換，例如，如果您有如下的端點，請使用`NONE`:`https://api.moviestar.com/data/items` </li></ul> |
| `value` | 字串 | 填入Experience Platform應連線之API端點的位址。 |

{style=&quot;table-layout:auto&quot;}

<!--

|Parameter | Type | Description|
|---------|----------|------|
|`hostname` | String | This is the hostname of your server. Example `https://data-in.acmecompany.net`.  |
|`port` | integer | The server port of your destination, for example `443`, `80`. |
|`maxUsersPerRequest` | integer | Specifies the maximum number of users per request allowed for your server. |
|`path` | String | This represents the url path and parameters of your server. Example:  `/path/to/import` |
|`httpMethod` | String | The method that Adobe will use in calls to your server. Options are `GET`, `PUT`, `POST`, `DELETE`, `PATCH`, `OPTIONS`, `HEAD`. |
|`contentType` | String | Defines how to structure the content sent to your servers. Supported options are JSON and XML. |

-->

## 模板規格 {#template-specs}

![醒目提示範本設定](./assets/template-configuration.png)

範本規格可讓您設定如何將匯出的訊息格式化至目的地。 Adobe使用類似[Jinja](https://jinja.palletsprojects.com/en/2.11.x/)的範本語言，將XDM結構的欄位轉換為目的地支援的格式。 如需轉換的詳細資訊，請造訪下列連結：

* [訊息格式](./message-format.md)
* [使用範本語言進行身分、屬性和區段成員資格轉換 ](./message-format.md#using-templating)

>[!TIP]
>
>Adobe提供[開發人員工具](./create-template.md)，可協助您建立和測試訊息轉換範本。

| 參數 | 類型 | 說明 |
|---|---|---|
| `httpMethod` | 字串 | Adobe將用於呼叫伺服器的方法。 選項包括`GET`、`PUT`、`POST`、`DELETE`、`PATCH`。 |
| `templatingStrategy` | 字串 | 使用 `PEBBLE_V1`。 |
| `value` | 字串 | 此字串是字元逸出版本，可將Platform客戶的資料轉換為服務預期的格式。 <br> 如需如何編寫範本的資訊，請閱讀使用 [範本區段](./message-format.md#using-templating)。<br> 如需字元逸出的詳細資訊，請參 [閱RFC JSON標準，第七節](https://tools.ietf.org/html/rfc8259#section-7)。<br> 如需簡單轉換的範例，請參閱設定檔屬 [性](./message-format.md#attributes) 結構。 |
| `contentType` | 字串 | 伺服器接受的內容類型。 此值很可能是`application/json`。 |

{style=&quot;table-layout:auto&quot;}

<!--

|`requestBody` | String | The request body contains the data exported from Real-time CDP, activated to your destination. <br> We need to know which data format macros your destination should support. See [Outbound Template Macros](https://docs.adobe.com/content./en/audience-manager/user-guide/implementation-integration-guides/receiving-audience-data/batch-outbound-data-transfers/outbound-template-macros.html) and [Outbound Macro Examples](https://docs.adobe.com/content./en/audience-manager/user-guide/implementation-integration-guides/receiving-audience-data/batch-outbound-data-transfers/outbound-macro-examples.html) for examples from Adobe's DMP, Audience Manager. <br> See also, [Message format](#message-format) for further information.  |
|`queryParameters` | String | Request parameters defined as macros. See above.|



<br>&nbsp;

#### Example

A valid HTTP specs template could look like below:

```

{
  "name": "ACME company HTTP template",
  "type": "HTTP", 
  "httpTemplate": {
    "httpMethod": "POST",
    "requestBody": "{"AdvertiserId":"12345", "DataCenterId": 2, "SegmentID":"dfd215e4-8d6b-4fdb-90b9-fab4456f2c9d","Data":[{"Name":"4321"}]}",
    "queryParameters": "{"AdvertiserId":"12345", "DataCenterId": 2, "SegmentID":"dfd215e4-8d6b-4fdb-90b9-fab4456f2c9d","Data":[{"Name":"4321"}]}",
    "contentType": "JSON"
  }
}

```

// commenting out this part as these types of destination specs are not supported in phase one

### File specifications

File-based destinations deliver file exports containing segment qualifications and profile attributes to your preferred storage location. If you want to set up a batch file-based destination, the template we'll use will be as below:

## Server specs

The server configuration contains information about the server receiving the messages (the server on your side). 
Adobe Real-time CDP currently supports three types of server configurations:
* URL
* File-based SFTP
* File-based S3

For URL destinations, you would provide us your server's information, for File-based SFTP and File-based S3 you would provide information as to the storage locations where files should be delivered.
Provide us the necessary information about your server or storage locations, as shown in the sections below.


**urlBasedDestination**

|Parameter | Type | Description|
|---------|----------|------|
|`hostname` | String | This is the hostname of your server. Example `https://data-in.acmecompany.net`.  |
|`port` | integer | The server port of your destination, for example `443`, `80`. |
|`maxUsersPerRequest` | integer | Specifies the maximum number of users per request allowed for your server. |
|`path` | String | This represents the url path and parameters of your server. Example:  `/path/to/import` |


// commenting out this part as these types of destination specs are not supported in phase one

**SFTP Destinations**

For FTP destinations, we need the protocol details below:

Parameter | Type | 
---------|----------|
 hostname | String | 
 port | integer | 
 rootDirectory | String | 
 moveToWhenCompleted | integer | 
 tmpFileRename | integer | 
 encryptionMode | String |
 filenameSuffix | String | 

**Amazon S3 Destinations**

For Amazon S3 destinations, we need the protocol details below:

Parameter | Description | 
---------|----------|
 bucket | Your Amazon S3 bucket name | 
 path | Your Amazon S3 bucket path | 

-->
