---
description: 此頁列出並說明使用Destination SDK配置流目標的步驟。
title: 使用Destination SDK配置流目標
exl-id: d8aa7353-ba55-4a0d-81c4-ea2762387638
source-git-commit: 0befd65b91e49cacab67c76fd9ed5d77bf790b9d
workflow-type: tm+mt
source-wordcount: '820'
ht-degree: 0%

---

# 使用Destination SDK配置流目標

## 總覽 {#overview}

本頁介紹如何使用中的資訊 [目標SDK中的配置選項](../functionality/configuration-options.md) 和其他Destination SDK功能和API參考文檔中 [流目標](../../destination-types.md#streaming-destinations)。 這些步驟按如下順序排列。

## 先決條件 {#prerequisites}

在前進到下面所示的步驟之前，請閱讀 [Destination SDK入門](../getting-started.md) 頁，以獲取使用Adobe I/OAPI的必要Destination SDK身份驗證憑據和其他先決條件。 這假定您已完成合作關係和權限先決條件，並準備開始開發目標。

## 使用Destination SDK中的配置選項設定目標的步驟 {#steps}

![使用Destination SDK端點的說明步驟](../assets/guides/destination-sdk-steps.png)

## 步驟1:建立伺服器和模板配置 {#create-server-template-configuration}

開始於 [建立伺服器和模板配置](../authoring-api/destination-server/create-destination-server.md) 使用 `/destinations-server` 端點。

下面是一個配置示例。 請注意， `requestBody.value` 參數在步驟3中定址， [建立轉換模板](#create-transformation-template)。

```shell
POST platform.adobe.io/data/core/activation/authoring/destination-servers
```

```json {line-numbers="true" highlight="14"}
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
         "value":"insert after you create a template in step 3"
      },
      "contentType":"application/json"
   }
}
```

## 步驟2:建立目標配置 {#create-destination-configuration}

下面是目標模板的配置示例，它使用 `/destinations` API終結點。 請參閱 [建立目標配置](../authoring-api/destination-configuration/create-destination-configuration.md) 的子菜單。

要將步驟1中的伺服器和模板配置連接到此目標配置，請將伺服器和模板配置的實例ID添加為 `destinationServerId` 給。

>[!IMPORTANT]
>
>要建立正確配置的即時（流）目標，請 *必須* 在中添加至少一個目標標識 `identityNamespaces`，如下所示。 如果未配置目標標識，則用戶將無法通過 [映射步驟](../../ui/activate-segment-streaming-destinations.md#mapping) 的子菜單。

```shell
POST platform.adobe.io/data/core/activation/authoring/destinations
```

```json {line-numbers="true" highlight="74"}
{
   "name":"Moviestar",
   "description":"Moviestar is a fictional destination, used for this example.",
   "status":"TEST",
   "customerAuthenticationConfigurations":[
      {
         "authType":"BEARER"
      }
   ],
   "customerDataFields":[
      {
         "name":"endpointsInstance",
         "type":"string",
         "title":"Select Endpoint",
         "description":"Moviestar manages several instances across the globe for REST endpoints that our customers are provisioned for. Select your endpoint in the dropdown list.",
         "isRequired":true,
         "enum":[
            "US",
            "EU",
            "APAC",
            "NZ"
         ]
      },
      {
         "name":"customerID",
         "type":"string",
         "title":"Moviestar Customer ID",
         "description":"Your customer ID in the Moviestar destination (e.g. abcdef).",
         "isRequired":true,
         "pattern":""
      }
   ],
   "uiAttributes":{
      "documentationLink":"http://www.adobe.com/go/destinations-moviestar-en",
      "category":"mobile",
      "connectionType":"Server-to-server",
      "frequency":"Streaming"
   },
   "identityNamespaces":{
      "external_id":{
         "acceptsAttributes":true,
         "acceptsCustomNamespaces":true
      },
      "another_id":{
         "acceptsAttributes":true,
         "acceptsCustomNamespaces":true
      }
   },
   "audienceMetadataConfig":{
      "mapExperiencePlatformSegmentName":false,
      "mapExperiencePlatformSegmentId":false,
      "mapUserInput":false,
      "audienceTemplateId":"cbf90a70-96b4-437b-86be-522fbdaabe9c"
   },   
   "aggregation":{
      "aggregationType":"CONFIGURABLE_AGGREGATION",
      "configurableAggregation":{
         "aggregationPolicyId":null,
         "aggregationKey":{
            "includeSegmentId":true,
            "includeSegmentStatus":true,
            "includeIdentity":true,
            "oneIdentityPerGroup":true,
            "groups":null
         },
         "splitUserById":true,
         "maxBatchAgeInSecs":2400,
         "maxNumEventsInBatch":5000
      }
   },
   "destinationDelivery":[
      {
         "authenticationRule":"CUSTOMER_AUTHENTICATION",
         "destinationServerId":"9c77000a-4559-40ae-9119-a04324a3ecd4"
      }
   ]
}
```

## 第3步：建立消息轉換模板 — 使用模板語言指定消息輸出格式 {#create-transformation-template}

您必鬚根據目標支援的負載建立模板，將導出資料的格式從AdobeXDM格式轉換為目標支援的格式。 請參閱一節中的模板示例 [使用模板語言進行身份、屬性和段成員身份轉換](../functionality/destination-server/message-format.md#using-templating) 並使用 [模板創作工具](../testing-api/streaming-destinations/create-template.md) 由Adobe提供。

編製適合您的消息轉換模板後，將其添加到您在步驟1中建立的伺服器和模板配置中。

```json {line-numbers="true" highlight="13-14"}
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
      "requestBody":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{\n    \"users\": [\n        {% for profile in input.profiles %}\n            {{profile|raw}}{% if not loop.last %},{% endif %}\n        {% endfor %}\n    ]\n}"
      },
      "contentType":"application/json"
   }
}
```

## 第4步：建立受眾元資料配置 {#create-audience-metadata-configuration}

對於某些目標，Destination SDK要求您配置訪問群體元資料配置，以寫程式方式在目標中建立、更新或刪除訪問群體。 請參閱 [受眾元資料管理](../functionality/audience-metadata-management.md) 有關您何時需要設定此配置以及如何進行配置的資訊。

如果使用訪問群體元資料配置，則必須將其連接到您在步驟2中建立的目標配置。 將受眾元資料配置的實例ID添加到目標配置中，作為 `audienceTemplateId`。

```json {line-numbers="true" highlight="53"}
{
   "name":"Moviestar",
   "description":"Moviestar is a fictional destination, used for this example.",
   "status":"TEST",
   "customerAuthenticationConfigurations":[
      {
         "authType":"BEARER"
      }
   ],
   "customerDataFields":[
      {
         "name":"endpointsInstance",
         "type":"string",
         "title":"Select Endpoint",
         "description":"Moviestar manages several instances across the globe for REST endpoints that our customers are provisioned for. Select your endpoint in the dropdown list.",
         "isRequired":true,
         "enum":[
            "US",
            "EU",
            "APAC",
            "NZ"
         ]
      },
      {
         "name":"customerID",
         "type":"string",
         "title":"Moviestar Customer ID",
         "description":"Your customer ID in the Moviestar destination (e.g. abcdef).",
         "isRequired":true,
         "pattern":""
      }
   ],
   "uiAttributes":{
      "documentationLink":"http://www.adobe.com/go/destinations-moviestar-en",
      "category":"mobile",
      "connectionType":"Server-to-server",
      "frequency":"Streaming"
   },
   "identityNamespaces":{
      "external_id":{
         "acceptsAttributes":true,
         "acceptsCustomNamespaces":true
      },
      "another_id":{
         "acceptsAttributes":true,
         "acceptsCustomNamespaces":true
      }
   },
   "audienceMetadataConfig":{
      "mapExperiencePlatformSegmentName":false,
      "mapExperiencePlatformSegmentId":false,
      "mapUserInput":false,
      "audienceTemplateId":"cbf90a70-96b4-437b-86be-522fbdaabe9c"
   },   
   "aggregation":{
      "aggregationType":"CONFIGURABLE_AGGREGATION",
      "configurableAggregation":{
         "aggregationPolicyId":null,
         "aggregationKey":{
            "includeSegmentId":true,
            "includeSegmentStatus":true,
            "includeIdentity":true,
            "oneIdentityPerGroup":true,
            "groups":null
         },
         "splitUserById":true,
         "maxBatchAgeInSecs":2400,
         "maxNumEventsInBatch":5000
      }
   },
   "destinationDelivery":[
      {
         "authenticationRule":"CUSTOMER_AUTHENTICATION",
         "destinationServerId":"9c77000a-4559-40ae-9119-a04324a3ecd4"
      }
   ]
}
```


## 第5步：設定身份驗證 {#set-up-authentication}

取決於是否指定 `"authenticationRule": "CUSTOMER_AUTHENTICATION"` 或 `"authenticationRule": "PLATFORM_AUTHENTICATION"` 在上面的目標配置中，您可以使用 `/destination` 或 `/credentials` 端點。

如果已選擇 `"authenticationRule": "CUSTOMER_AUTHENTICATION"` 在目標配置中，並且目標支援OAuth 2身份驗證方法，請閱讀 [OAuth 2身份驗證](../functionality/destination-configuration/oauth2-authentication.md)。

如果已選擇 `"authenticationRule": "PLATFORM_AUTHENTICATION"`，必須建立 [憑據配置](../credentials-api/create-credential-configuration.md)。

## 步驟6:Test目標 {#test-destination}

使用前面步驟中的配置端點設定目標後，可以使用 [目標測試工具](../testing-api/streaming-destinations/streaming-destination-testing-overview.md) testAdobe Experience Platform和你目的地的融合。

在test目標的過程中，必須使用Experience PlatformUI建立段，您將激活這些段到目標。 有關如何在Experience Platform中建立段的說明，請參閱以下兩種資源：

* [建立段文檔頁面](/help/segmentation/ui/overview.md#create-segment)
* [建立段視頻穿透](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html?lang=en)

## 第7步：發佈目標 {#publish-destination}

>[!NOTE]
>
>如果您要建立專用目標供自己使用，並且不想將其發佈到目標目錄中以供其他客戶使用，則無需執行此步驟。

配置和測試目標後，使用 [目標發佈API](../publishing-api/create-publishing-request.md) 將您的配置提交給Adobe以供審閱。

## 第8步：記錄目標 {#document-destination}

>[!NOTE]
>
>如果您要建立專用目標供自己使用，並且不想將其發佈到目標目錄中以供其他客戶使用，則無需執行此步驟。

如果您是獨立軟體供應商(ISV)或系統整合商(SI)，則 [產品化整合](../overview.md#productized-custom-integrations)，使用 [自助文檔處理](../docs-framework/documentation-instructions.md) 為目標建立產品文檔頁面 [Experience Platform目標目錄](/help/destinations/catalog/overview.md)。

## 第9步：提交目標供Adobe審閱 {#submit-for-review}

>[!NOTE]
>
>如果您要建立專用目標供自己使用，並且不想將其發佈到目標目錄中以供其他客戶使用，則無需執行此步驟。

最後，在目標可以發佈到Experience Platform目錄中並且所有Experience Platform客戶都能看到之前，您需要正式提交目標供Adobe審查。 查找有關如何 [提交以審閱在Destination SDK中創作的已生產化目標](../guides/submit-destination.md)。
