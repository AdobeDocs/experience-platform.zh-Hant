---
description: 本頁面列出並說明使用Destination SDK設定串流目的地的步驟。
title: 使用Destination SDK來設定串流目的地
exl-id: d8aa7353-ba55-4a0d-81c4-ea2762387638
source-git-commit: 0d58d949ff24b9059d6afe81de354da0783ec8a4
workflow-type: tm+mt
source-wordcount: '825'
ht-degree: 0%

---

# 使用Destination SDK來設定串流目的地

## 總覽 {#overview}

本頁面說明如何使用 [目的地SDK中的設定選項](./configuration-options.md) 和其他Destination SDK功能及API參考檔案中，以設定 [串流目的地](/help/destinations/destination-types.md#streaming-destinations). 步驟依序排列如下。

## 先決條件 {#prerequisites}

在前進到下面所示的步驟之前，請閱讀 [Destination SDK快速入門](./getting-started.md) 頁面，以取得使用Adobe I/OAPI所需的Destination SDK驗證憑證和其他必要條件的相關資訊。

## 使用Destination SDK中設定選項來設定目的地的步驟 {#steps}

![使用Destination SDK端點的說明步驟](./assets/destination-sdk-steps.png)

## 步驟1:建立伺服器和範本配置 {#create-server-template-configuration}

首先，使用 `/destinations-server` 端點（讀取） [API參考](destination-server-api.md))。 有關伺服器和模板配置的詳細資訊，請參閱 [伺服器和模板規格](server-and-template-configuration.md) 在參考區段中。

以下是設定範例。 請注意， `requestBody.value` 參數在步驟3中處理， [建立轉換範本](./configure-destination-instructions.md#create-transformation-template).

```json
POST platform.adobe.io/data/core/activation/authoring/destination-servers

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

以下是目標範本的設定範例，建立方法為使用 `/destinations` API端點。 有關此配置的詳細資訊，請參閱 [目標配置](./destination-configuration.md).

要將步驟1中的伺服器和模板配置連接到此目標配置，請將伺服器和模板配置的實例ID添加為 `destinationServerId` 這裡。

>[!IMPORTANT]
>
>若要建立正確設定的目的地，請 *必須* 在 `identityNamespaces`，如下所示。 如果未設定目標身分，則使用者將無法通過 [對應步驟](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping) 啟動工作流程。

```json
POST platform.adobe.io/data/core/activation/authoring/destinations
 
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
   "segmentMappingConfig":{
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

## 步驟3:建立消息轉換模板 — 使用模板語言指定消息輸出格式 {#create-transformation-template}

您必鬚根據目的地支援的裝載，建立範本，將匯出資料的格式從AdobeXDM格式轉換為目的地支援的格式。 請參閱區段中的範本範例 [使用範本語言進行身分、屬性和區段成員資格轉換](./message-format.md#using-templating) 並使用 [範本製作工具](./create-template.md) 由Adobe提供。

在您精心編製了適用於您的消息轉換模板後，將其添加到您在步驟1中建立的伺服器和模板配置中。

## 步驟4:建立對象中繼資料設定 {#create-audience-metadata-configuration}

對於某些目的地，Destination SDK需要您設定對象中繼資料設定，以程式設計方式建立、更新或刪除目標中的對象。 請參閱 [對象中繼資料管理](./audience-metadata-management.md) 以了解您何時需要設定此設定及如何設定。

如果您使用對象中繼資料設定，則必須將其連線至您在步驟2建立的目的地設定。 將對象中繼資料設定的例項ID新增至目的地設定，作為 `audienceTemplateId`.

## 步驟5:設定驗證 {#set-up-authentication}

視您是否指定 `"authenticationRule": "CUSTOMER_AUTHENTICATION"` 或 `"authenticationRule": "PLATFORM_AUTHENTICATION"` 在上述的目的地設定中，您可以使用 `/destination` 或 `/credentials` 端點。

* **最常見的案例**:如果您選取 `"authenticationRule": "CUSTOMER_AUTHENTICATION"` 在目的地設定中，且您的目的地支援OAuth 2驗證方法，請參閱 [OAuth 2驗證](./oauth2-authentication.md).
* 如果您選取 `"authenticationRule": "PLATFORM_AUTHENTICATION"`，請參閱 [驗證配置](./authentication-configuration.md#when-to-use).

## 步驟6:測試您的目的地 {#test-destination}

使用前述步驟中的設定端點設定目的地後，您可以使用 [目的地測試工具](./test-destination.md) 來測試Adobe Experience Platform與目的地之間的整合。

在測試目的地的程式中，您必須使用Experience PlatformUI來建立區段，以便您對目的地啟用。 如需如何在Experience Platform中建立區段的指示，請參閱以下兩個資源：

* [建立區段檔案頁面](/help/segmentation/ui/overview.md#create-segment)
* [建立區段視訊逐步說明](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html?lang=en)

## 步驟7:發佈您的目的地 {#publish-destination}

>[!NOTE]
>
>如果您要建立私人目的地以供自己使用，且不想將其發佈至目的地目錄以供其他客戶使用，則不需要執行此步驟。

設定並測試您的目的地後，請使用 [目的地發佈API](./destination-publish-api.md) 將配置提交到Adobe以供審核。

## 步驟8:記錄您的目的地 {#document-destination}

>[!NOTE]
>
>如果您要建立私人目的地以供自己使用，且不想將其發佈至目的地目錄以供其他客戶使用，則不需要執行此步驟。

如果您是獨立軟體供應商(ISV)或系統整合商(SI)，則建立 [產品化整合](./overview.md#productized-custom-integrations)，請使用 [自助服務檔案程式](./docs-framework/documentation-instructions.md) 若要為您的目的地建立產品檔案頁面，請在 [Experience Platform目的地目錄](/help/destinations/catalog/overview.md).

## 步驟9:提交目標供Adobe審核 {#submit-for-review}

>[!NOTE]
>
>如果您要建立私人目的地以供自己使用，且不想將其發佈至目的地目錄以供其他客戶使用，則不需要執行此步驟。

最後，在目標可以發佈到Experience Platform目錄且所有Experience Platform客戶都看得到之前，您需要正式提交目標以供Adobe審核。 尋找有關如何 [提交以審核在Destination SDK中創作的已產品化目標](/help/destinations/destination-sdk/submit-destination.md).
