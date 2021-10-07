---
description: 本頁列出並說明您可使用「/authoring/destinations」 API端點執行的所有API操作。
title: 目的地API端點作業
exl-id: 96755e9d-be62-432f-b985-91330575b395
source-git-commit: 76a596166edcdbf141b5ce5dc01557d2a0b4caf3
workflow-type: tm+mt
source-wordcount: '2405'
ht-degree: 3%

---

# 目的地端點API作業 {#destination-configuration}

>[!IMPORTANT]
>
>**API端點**:  `platform.adobe.io/data/core/activation/authoring/destinations`

本頁列出並說明了所有可使用`/authoring/destinations` API端點執行的API操作。 有關此終結點支援的功能的說明，請閱讀[目標配置](./destination-configuration.md)。

## 目的地API作業快速入門 {#get-started}

繼續之前，請檢閱[快速入門手冊](./getting-started.md)，以取得成功呼叫API所需的重要資訊，包括如何取得必要的目的地編寫權限和必要的標題。

## 建立目標的設定 {#create}

您可以向`/authoring/destinations`端點提出POST請求，以建立新的目標配置。

**API格式**


```http
POST /authoring/destinations
```

**要求**

下列要求會建立新的目的地設定，由裝載中提供的參數所設定。 以下裝載包含`/authoring/destinations`端點接受的所有參數。 請注意，您不必在呼叫上新增所有參數，且可根據您的API需求自訂範本。

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/destinations \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
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
         "pattern":"^[A-Za-z]+$"
      }
   ],
   "uiAttributes":{
      "documentationLink":"https://www.adobe.com/go/destinations-moviestar-en",
      "category":"mobile",
      "connectionType":"Server-to-server",
      "frequency":"Streaming"
   },
   "identityNamespaces":{
      "external_id":{
         "acceptsAttributes":true,
         "acceptsCustomNamespaces":true,
         "acceptedGlobalNamespaces":{
            "Email":{
            }
         }
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
   "schemaConfig":{
      "profileFields":[
         {
            "name":"a_custom_attribute",
            "title":"a_custom_attribute",
            "description":"This is a fixed attribute on your destination side that customers can map profile attributes to. For example, the phoneNumber value in Experience Platform could be phoneNo on your side.",
            "type":"string",
            "isRequired":false,
            "readOnly":false,
            "hidden":false
         }
      ],
      "profileRequired":true,
      "segmentRequired":true,
      "identityRequired":true
   },
   "aggregation":{
      "aggregationType":"BEST_EFFORT",
      "bestEffortAggregation":{
         "maxUsersPerRequest":10,
         "splitUserById":false
      }
   },
   "destinationDelivery":[
      {
         "authenticationRule":"CUSTOMER_AUTHENTICATION",
         "destinationServerId":"9c77000a-4559-40ae-9119-a04324a3ecd4"
      }
   ],
   "backfillHistoricalProfileData":true
}
```

| 參數 | 類型 | 說明 |
|---------|----------|------|
| `name` | 字串 | 指出Experience Platform目錄中的目的地標題 |
| `description` | 字串 | 提供說明，供Adobe用於目的地卡的Experience Platform目的地目錄。 目標不超過4-5句。 |
| `status` | 字串 | 指示目標卡的生命週期狀態。 接受的值為 `TEST`、`PUBLISHED` 和 `DELETED`。首次配置目標時，請使用`TEST`。 |
| `customerAuthenticationConfigurations` | 字串 | 指示用於驗證Experience Platform客戶到伺服器的配置。 如需接受的值，請參閱下方的`authType`。 |
| `customerAuthenticationConfigurations.authType` | 字串 | 接受的值為`OAUTH2, BEARER`。 |
| `customerDataFields.name` | 字串 | 提供您要引入的自訂欄位名稱。 |
| `customerDataFields.type` | 字串 | 指出您要引入的自訂欄位類型。 接受的值為`string`、`object`、`integer` |
| `customerDataFields.title` | 字串 | 指出欄位的名稱，如Experience Platform使用者介面中的客戶所見 |
| `customerDataFields.description` | 字串 | 提供自訂欄位的說明。 |
| `customerDataFields.isRequired` | 布林值 | 指示目標設定工作流中是否需要此欄位。 |
| `customerDataFields.enum` | 字串 | 將自訂欄位轉譯為下拉式功能表，並列出使用者可用的選項。 |
| `customerDataFields.pattern` | 字串 | 視需要為自訂欄位強制使用模式。 使用規則運算式來強制模式。 例如，若您的客戶ID未包含數字或底線，請在此欄位中輸入`^[A-Za-z]+$`。 |
| `uiAttributes.documentationLink` | 字串 | 指您目的地的[目的地目錄](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/overview.html?lang=en#catalog)中的檔案頁面。 使用`https://www.adobe.com/go/destinations-YOURDESTINATION-en`，其中`YOURDESTINATION`是目的地的名稱。 對於名為Moviestar的目標，請使用`https://www.adobe.com/go/destinations-moviestar-en`。 |
| `uiAttributes.category` | 字串 | 是指指派給Adobe Experience Platform中目的地的類別。 如需詳細資訊，請參閱[目標類別](https://experienceleague.adobe.com/docs/experience-platform/rtcdp/destinations/destination-types.html?lang=en#destination-categories)。 使用下列其中一個值：`adobeSolutions, advertising, analytics, cdp, cloudStorage, crm, customerSuccess, database, dmp, ecommerce, email, emailMarketing, enrichment, livechat, marketingAutomation, mobile, personalization, protocols, social, streaming, subscriptions, surveys, tagManagers, voc, warehouses, payments`。 |
| `uiAttributes.connectionType` | 字串 | `Server-to-server` 是目前唯一可用的選項。 |
| `uiAttributes.frequency` | 字串 | `Streaming` 是目前唯一可用的選項。 |
| `identityNamespaces.externalId.acceptsAttributes` | 布林值 | 指出目的地是否接受標準設定檔屬性。 通常，合作夥伴的檔案會強調顯示這些屬性。 |
| `identityNamespaces.externalId.acceptsCustomNamespaces` | 布林值 | 指出客戶是否可在您的目的地中設定自訂命名空間。 |
| `identityNamespaces.externalId.allowedAttributesTransformation` | 字串 | _範例設定中未顯示_。例如，當[!DNL Platform]客戶有純電子郵件地址作為屬性，且您的平台僅接受雜湊電子郵件時，就會使用。 您可在此提供需要套用的轉換（例如，將電子郵件轉換為小寫，然後雜湊）。 |
| `identityNamespaces.externalId.acceptedGlobalNamespaces` | - | 用於您的平台接受[標準身分識別命名空間](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=en#standard-namespaces)（例如IDFA）時的情況，因此您可以限制Platform使用者僅選取這些身分識別命名空間。 <br> 使用時， `acceptedGlobalNamespaces`您可以使用小寫 `"requiredTransformation":"sha256(lower($))"` 和雜湊電子郵件地址或電話號碼。 |
| `destinationDelivery.authenticationRule` | 字串 | 指示[!DNL Platform]客戶如何連接到目標。 接受的值為`CUSTOMER_AUTHENTICATION`、`PLATFORM_AUTHENTICATION`、`NONE`。 <br> <ul><li>如果Platform客戶透過使用者名稱和密碼、承載權杖或其他驗證方法登入您的系統，請使用`CUSTOMER_AUTHENTICATION`。 例如，如果您也在`customerAuthenticationConfigurations`中選取了`authType: OAUTH2`或`authType:BEARER`，則可以選取此選項。 </li><li> 如果Adobe和目標之間存在全局身份驗證系統，並且[!DNL Platform]客戶不需要提供任何身份驗證憑據來連接到目標，請使用`PLATFORM_AUTHENTICATION`。 在這種情況下，必須使用[Credentials](./credentials-configuration.md)配置建立憑據對象。 </li><li>如果不需要任何身份驗證才能將資料發送到目標平台，請使用`NONE`。 </li></ul> |
| `destinationDelivery.destinationServerId` | 字串 | 用於此目標的[目標伺服器模板](./destination-server-api.md)的`instanceId`。 |
| `backfillHistoricalProfileData` | 布林值 | 控制在將區段啟動至目的地時，是否匯出歷史設定檔資料。<br> <ul><li> `true`: [!DNL Platform] 傳送在啟用區段之前符合區段資格的歷史使用者設定檔。 </li><li> `false`: [!DNL Platform] 僅包含區段啟動後符合區段資格的使用者設定檔。 </li></ul> |
| `segmentMappingConfig.mapUserInput` | 布林值 | 控制使用者是否輸入目標啟動工作流程中的區段對應ID。 |
| `segmentMappingConfig.mapExperiencePlatformSegmentId` | 布林值 | 控制目標啟動工作流程中的區段對應ID是否為Experience Platform區段ID。 |
| `segmentMappingConfig.mapExperiencePlatformSegmentName` | 布林值 | 控制目標啟動工作流程中的區段對應ID是否為Experience Platform區段名稱。 |
| `segmentMappingConfig.audienceTemplateId` | 布林值 | 用於此目的地的[對象中繼資料範本](./audience-metadata-api.md)的`instanceId`。 |
| `schemaConfig.profileFields` | 陣列 | 如上述設定所示，當您新增預先定義的`profileFields`時，使用者將可以選擇將Experience Platform屬性對應至目的地端的預先定義屬性。 |
| `schemaConfig.profileRequired` | 布林值 | 如果使用者應能將設定檔屬性從Experience Platform對應至目的地端的自訂屬性，請使用`true` ，如上方的範例設定所示。 |
| `schemaConfig.segmentRequired` | 布林值 | 請一律使用`segmentRequired:true`。 |
| `schemaConfig.identityRequired` | 布林值 | 如果您的使用者應能將身分識別命名空間從Experience Platform對應至您想要的架構，請使用`true`。 |
| `aggregation.aggregationType` | - | 選取「`BEST_EFFORT`」或「`CONFIGURABLE_AGGREGATION`」。上述範例設定包含`BEST_EFFORT`匯總。 有關`CONFIGURABLE_AGGREGATION`的示例，請參閱[目標配置](./destination-configuration.md#example-configuration)文檔中的示例配置。 下表介紹了與可配置聚合相關的參數。 |
| `aggregation.bestEffortAggregation.maxUsersPerRequest` | 整數 | Experience Platform可以在單一HTTP呼叫中匯總多個匯出的設定檔。 指定端點在單一HTTP呼叫中應接收的設定檔數上限。 請注意，這是最佳的匯總方式。 例如，如果您指定值100,Platform可能會在呼叫中傳送小於100的任何設定檔數量。 <br> 如果您的伺服器不接受每個請求有多個使用者，請將此值設為1。 |
| `aggregation.bestEffortAggregation.splitUserById` | 布林值 | 如果目標的呼叫應依身分分割，請使用此標幟。 如果您的伺服器在指定的命名空間中每次呼叫僅接受一個身分識別，請將此標幟設為`true`。 |
| `aggregation.configurableAggregation.splitUserById` | 布林值 | 請參閱範例設定[此處](./destination-configuration.md#example-configuration)中的參數。 如果目標的呼叫應依身分分割，請使用此標幟。 如果您的伺服器在指定的命名空間中每次呼叫僅接受一個身分識別，請將此標幟設為`true`。 |
| `aggregation.configurableAggregation.maxBatchAgeInSecs` | 整數 | *最大值：3600*。請參閱範例設定[此處](./destination-configuration.md#example-configuration)中的參數。 這會與`maxNumEventsInBatch`一起決定Experience Platform應等待多久，直到傳送API呼叫至端點為止。 <br> 例如，如果您對這兩個參數使用最大值，Experience Platform會先等候3600秒或直到有10.000個合格設定檔才進行API呼叫（以先發生者為準）。 |
| `aggregation.configurableAggregation.maxNumEventsInBatch` | 整數 | *最大值：10000*。請參閱範例設定[此處](./destination-configuration.md#example-configuration)中的參數。 請參閱上方的`maxBatchAgeInSecs`。 |
| `aggregation.configurableAggregation.aggregationKey` | 布林值 | 請參閱範例設定[此處](./destination-configuration.md#example-configuration)中的參數。 可讓您根據下列參數，匯總對應至目的地的匯出設定檔：<br> <ul><li>區段ID</li><li> 區段狀態 </li><li> 身分命名空間 </li></ul> |
| `aggregation.configurableAggregation.aggregationKey.includeSegmentId` | 布林值 | 請參閱範例設定[此處](./destination-configuration.md#example-configuration)中的參數。 如果您想要依區段ID將匯出至目的地的設定檔分組，請將此項目設為`true`。 |
| `aggregation.configurableAggregation.aggregationKey.includeSegmentStatus` | 布林值 | 請參閱範例設定[此處](./destination-configuration.md#example-configuration)中的參數。 如果要依區段ID和區段狀態將匯出至目的地的設定檔分組，您必須同時設定`includeSegmentId:true`和`includeSegmentStatus:true`。 |
| `aggregation.configurableAggregation.aggregationKey.includeIdentity` | 布林值 | 請參閱範例設定[此處](./destination-configuration.md#example-configuration)中的參數。 如果您想要依身分命名空間將匯出至目的地的設定檔分組，請將此設為`true`。 |
| `aggregation.configurableAggregation.aggregationKey.oneIdentityPerGroup` | 布林值 | 請參閱範例設定[此處](./destination-configuration.md#example-configuration)中的參數。 使用此參數可指定是否要將匯出的設定檔匯總為單一身分的群組（GAID、IDFA、電話號碼、電子郵件等）。 |
| `aggregation.configurableAggregation.aggregationKey.groups` | 字串 | 請參閱範例設定[此處](./destination-configuration.md#example-configuration)中的參數。 如果您想要依身分命名空間的群組，將匯出至目的地的設定檔分組，請建立身分群組清單。 例如，您可以使用範例中的設定，將包含IDFA和GAID行動識別碼的設定檔，合併至對您目的地的呼叫和電子郵件中。 |

{style=&quot;table-layout:auto&quot;}

**回應**

成功的回應會傳回HTTP狀態200，並包含您新建立之目的地組態的詳細資訊。

## 列出目標配置 {#retrieve-list}

您可以向`/authoring/destinations`端點提出GET要求，以擷取IMS組織的所有目標設定清單。

**API格式**


```http
GET /authoring/destinations
```

**要求**

下列請求會根據IMS組織和沙箱設定，擷取您有權存取的目的地設定清單。

```shell
curl -X GET https://platform.adobe.io/data/core/activation/authoring/destinations \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

下列回應會根據您使用的IMS組織ID和沙箱名稱，傳回HTTP狀態200，並列出您可存取的目標設定。 一個`instanceId`對應於一個目標的模板。 回應會為簡潔而截斷。

```json
{
   "items":[
      {
         "instanceId":"b0780cb5-2bb7-4409-bf2c-c625ca818588",
         "createdDate":"2020-10-28T06:14:09.784471Z",
         "lastModifiedDate":"2021-06-28T06:14:09.784471Z",
         "imsOrg":"AC3428435BF324E90A49402A@AdobeOrg",
         "sandboxName":"prod",
         "sandboxId":"r5g6660-c5da-11e9-93d4-6d5fc3a66a8e",
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
               "pattern":"^[A-Za-z]+$"
            }
         ],
         "uiAttributes":{
            "documentationLink":"https://www.adobe.com/go/destinations-moviestar-en",
            "category":"mobile",
            "connectionType":"Server-to-server",
            "frequency":"Streaming"
         },
         "identityNamespaces":{
            "external_id":{
               "acceptsAttributes":true,
               "acceptsCustomNamespaces":true,
               "acceptedGlobalNamespaces":{
                  "Email":{
                     
                  }
               }
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
         "schemaConfig":{
            "profileFields":[
               {
                  "name":"a_custom_attribute",
                  "title":"a_custom_attribute",
                  "description":"This is a fixed attribute on your destination side that customers can map profile attributes to. For example, the phoneNumber value in Experience Platform could be phoneNo on your side.",
                  "type":"string",
                  "isRequired":false,
                  "readOnly":false,
                  "hidden":false
               }
            ],
            "profileRequired":true,
            "segmentRequired":true,
            "identityRequired":true
         },
         "aggregation":{
            "aggregationType":"BEST_EFFORT",
            "bestEffortAggregation":{
               "maxUsersPerRequest":10,
               "splitUserById":false
            }
         },
         "destinationDelivery":[
            {
               "authenticationRule":"CUSTOMER_AUTHENTICATION",
               "destinationServerId":"9c77000a-4559-40ae-9119-a04324a3ecd4"
            }
         ],
         "destConfigId":"410631b8-f6b3-4b7c-82da-7998aa3f327c",
         "backfillHistoricalProfileData":true
      }
   ]
}
    
```

| 參數 | 類型 | 說明 |
|---------|----------|------|
| `name` | 字串 | 指出Experience Platform目錄中的目的地標題。 |
| `description` | 字串 | 提供說明，供Adobe用於目的地卡的Experience Platform目的地目錄。 目標不超過4-5句。 |
| `status` | 字串 | 指示目標卡的生命週期狀態。 接受的值為 `TEST`、`PUBLISHED` 和 `DELETED`。首次配置目標時，請使用`TEST`。 |
| `customerAuthenticationConfigurations` | 字串 | 指示用於驗證Experience Platform客戶到伺服器的配置。 如需接受的值，請參閱下方的`authType`。 |
| `customerAuthenticationConfigurations.authType` | 字串 | 接受的值為`OAUTH2, BEARER`。 |
| `customerDataFields.name` | 字串 | 提供您要引入的自訂欄位名稱。 |
| `customerDataFields.type` | 字串 | 指出您要引入的自訂欄位類型。 接受的值為`string`、`object`、`integer` |
| `customerDataFields.title` | 字串 | 指出欄位的名稱，如Experience Platform使用者介面中的客戶所見 |
| `customerDataFields.description` | 字串 | 提供自訂欄位的說明。 |
| `customerDataFields.isRequired` | 布林值 | 指示目標設定工作流中是否需要此欄位。 |
| `customerDataFields.enum` | 字串 | 將自訂欄位轉譯為下拉式功能表，並列出使用者可用的選項。 |
| `customerDataFields.pattern` | 字串 | 視需要為自訂欄位強制使用模式。 使用規則運算式來強制模式。 例如，若您的客戶ID未包含數字或底線，請在此欄位中輸入`^[A-Za-z]+$`。 |
| `uiAttributes.documentationLink` | 字串 | 指您目的地的[目的地目錄](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/overview.html?lang=en#catalog)中的檔案頁面。 使用`https://www.adobe.com/go/destinations-YOURDESTINATION-en`，其中`YOURDESTINATION`是目的地的名稱。 對於名為Moviestar的目標，您將使用`https://www.adobe.com/go/destinations-moviestar-en` |
| `uiAttributes.category` | 字串 | 是指指派給Adobe Experience Platform中目的地的類別。 如需詳細資訊，請參閱[目標類別](https://experienceleague.adobe.com/docs/experience-platform/rtcdp/destinations/destination-types.html?lang=en#destination-categories)。 使用下列其中一個值：`adobeSolutions, advertising, analytics, cdp, cloudStorage, crm, customerSuccess, database, dmp, ecommerce, email, emailMarketing, enrichment, livechat, marketingAutomation, mobile, personalization, protocols, social, streaming, subscriptions, surveys, tagManagers, voc, warehouses, payments` |
| `uiAttributes.connectionType` | 字串 | `Server-to-server` 是目前唯一可用的選項。 |
| `uiAttributes.frequency` | 字串 | `Streaming` 是目前唯一可用的選項。 |
| `identityNamespaces.externalId.acceptsAttributes` | 布林值 | 指出目的地是否接受標準設定檔屬性。 通常，合作夥伴的檔案會強調顯示這些屬性。 |
| `identityNamespaces.externalId.acceptsCustomNamespaces` | 布林值 | 指出客戶是否可在您的目的地中設定自訂命名空間。 閱讀更多有關Adobe Experience Platform中[自訂命名空間](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=en#manage-namespaces)的資訊。 |
| `identityNamespaces.externalId.allowedAttributesTransformation` | 字串 | _範例設定中未顯示_。例如，當[!DNL Platform]客戶有純電子郵件地址作為屬性，且您的平台僅接受雜湊電子郵件時，就會使用。 您可在此提供需要套用的轉換（例如，將電子郵件轉換為小寫，然後雜湊）。 |
| `identityNamespaces.externalId.acceptedGlobalNamespaces` | - | 用於您的平台接受[標準身分識別命名空間](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=en#standard-namespaces)（例如IDFA）時的情況，因此您可以限制Platform使用者僅選取這些身分識別命名空間。 |
| `destinationDelivery.authenticationRule` | 字串 | 指示[!DNL Platform]客戶如何連接到目標。 接受的值為`CUSTOMER_AUTHENTICATION`、`PLATFORM_AUTHENTICATION`、`NONE`。 <br> <ul><li>如果Platform客戶透過使用者名稱和密碼、承載權杖或其他驗證方法登入您的系統，請使用`CUSTOMER_AUTHENTICATION`。 例如，如果您也在`customerAuthenticationConfigurations`中選取了`authType: OAUTH2`或`authType:BEARER`，則可以選取此選項。 </li><li> 如果Adobe和目標之間存在全局身份驗證系統，並且[!DNL Platform]客戶不需要提供任何身份驗證憑據來連接到目標，請使用`PLATFORM_AUTHENTICATION`。 在這種情況下，必須使用[Credentials](./credentials-configuration.md)配置建立憑據對象。 </li><li>如果不需要任何身份驗證才能將資料發送到目標平台，請使用`NONE`。 </li></ul> |
| `destinationDelivery.destinationServerId` | 字串 | 用於此目標的[目標伺服器模板](./destination-server-api.md)的`instanceId`。 |
| `destConfigId` | 字串 | 此欄位會自動產生，不需要您輸入。 |
| `backfillHistoricalProfileData` | 布林值 | 控制在將區段啟動至目的地時，是否匯出歷史設定檔資料。<br> <ul><li> `true`: [!DNL Platform] 傳送在啟用區段之前符合區段資格的歷史使用者設定檔。 </li><li> `false`: [!DNL Platform] 僅包含區段啟動後符合區段資格的使用者設定檔。 </li></ul> |
| `segmentMappingConfig.mapUserInput` | 布林值 | 控制使用者是否輸入目標啟動工作流程中的區段對應ID。 |
| `segmentMappingConfig.mapExperiencePlatformSegmentId` | 布林值 | 控制目標啟動工作流程中的區段對應ID是否為Experience Platform區段ID。 |
| `segmentMappingConfig.mapExperiencePlatformSegmentName` | 布林值 | 控制目標啟動工作流程中的區段對應ID是否為Experience Platform區段名稱。 |
| `segmentMappingConfig.audienceTemplateId` | 布林值 | 用於此目的地的[對象中繼資料範本](./audience-metadata-management.md)的`instanceId`。 若要設定對象中繼資料範本，請閱讀[對象中繼資料API參考](./audience-metadata-api.md)。 |

{style=&quot;table-layout:auto&quot;}

## 更新現有目標配置 {#update}

您可以向`/authoring/destinations`端點發出PUT請求並提供要更新的目標配置的實例ID，以更新現有目標配置。 在呼叫內文中，提供更新的目的地設定。

**API格式**


```http
PUT /authoring/destinations/{INSTANCE_ID}
```

| 參數 | 說明 |
| -------- | ----------- |
| `{INSTANCE_ID}` | 要更新的目標配置ID。 |

**要求**

下列要求會更新現有的目的地設定，由裝載中提供的參數所設定。 在以下範例呼叫中，我們正在更新先前](./destination-configuration-api.md#create)建立的設定[，現在接受GAID、IDFA和雜湊電子郵件識別碼做為身分識別命名空間。

```shell
curl -X PUT https://platform.adobe.io/data/core/activation/authoring/destinations/b0780cb5-2bb7-4409-bf2c-c625ca818588 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
   "instanceId":"b0780cb5-2bb7-4409-bf2c-c625ca818588",
   "createdDate":"2020-10-28T06:14:09.784471Z",
   "lastModifiedDate":"2021-04-28T06:14:09.784471Z",
   "imsOrg":"AC3428435BF324E90A49402A@AdobeOrg",
   "sandboxName":"prod",
   "sandboxId":"r5g6660-c5da-11e9-93d4-6d5fc3a66a8e",
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
         "pattern":"^[A-Za-z]+$"
      }
   ],
   "uiAttributes":{
      "documentationLink":"https://www.adobe.com/go/destinations-moviestar-en",
      "category":"mobile",
      "connectionType":"Server-to-server",
      "frequency":"Streaming"
   },
   "identityNamespaces":{
      "external_id":{
         "acceptsAttributes":true,
         "acceptsCustomNamespaces":true,
         "acceptedGlobalNamespaces":{
            "Email":{
            }
         }
      },
      "another_id":{
         "acceptsAttributes":true,
         "acceptsCustomNamespaces":true
      },
      "gaid":{
         "acceptsAttributes":true,
         "acceptsCustomNamespaces":true,
         "acceptedGlobalNamespaces":{
            "GAID":{
               
            }
         }
      },
      "idfa":{
         "acceptsAttributes":true,
         "acceptsCustomNamespaces":true,
         "acceptedGlobalNamespaces":{
            "IDFA":{
               
            }
         }
      },
      "email_lc_sha256":{
         "acceptsAttributes":true,
         "acceptsCustomNamespaces":true,
         "transformation":"sha256(lower($))",
         "acceptedGlobalNamespaces":{
            "Email":{
               "requiredTransformation":"sha256(lower($))"
            },
            "Email_LC_SHA256":{
               
            }
         }
      }
   },
   "segmentMappingConfig":{
      "mapExperiencePlatformSegmentName":false,
      "mapExperiencePlatformSegmentId":false,
      "mapUserInput":false,
      "audienceTemplateId":"cbf90a70-96b4-437b-86be-522fbdaabe9c"
   },
   "schemaConfig":{
      "profileFields":[
         {
            "name":"a_custom_attribute",
            "title":"a_custom_attribute",
            "description":"This is a fixed attribute on your destination side that customers can map profile attributes to. For example, the phoneNumber value in Experience Platform could be phoneNo on your side.",
            "type":"string",
            "isRequired":false,
            "readOnly":false,
            "hidden":false
         }
      ],
      "profileRequired":true,
      "segmentRequired":true,
      "identityRequired":true
   },
   "aggregation":{
      "aggregationType":"BEST_EFFORT",
      "bestEffortAggregation":{
         "maxUsersPerRequest":10,
         "splitUserById":false
      }
   },
   "destinationDelivery":[
      {
         "authenticationRule":"CUSTOMER_AUTHENTICATION",
         "destinationServerId":"9c77000a-4559-40ae-9119-a04324a3ecd4"
      }
   ],
   "backfillHistoricalProfileData":true
}
```

## 擷取特定目的地設定 {#get}

您可以向`/authoring/destinations`端點提出GET請求並提供要檢索的目標配置的實例ID，以檢索有關特定目標配置的詳細資訊。

**API格式**


```http
GET /authoring/destinations/{INSTANCE_ID}
```

| 參數 | 說明 |
| -------- | ----------- |
| `{INSTANCE_ID}` | 您要擷取的目的地設定ID。 |

**要求**

```shell
curl -X GET https://platform.adobe.io/data/core/activation/authoring/destinations/b0780cb5-2bb7-4409-bf2c-c625ca818588 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應會傳回HTTP狀態200，並包含指定目的地設定的詳細資訊。

```json
{
   "instanceId":"b0780cb5-2bb7-4409-bf2c-c625ca818588",
   "createdDate":"2020-10-28T06:14:09.784471Z",
   "lastModifiedDate":"2021-06-04T06:14:09.784471Z",
   "imsOrg":"AC3428435BF324E90A49402A@AdobeOrg",
   "sandboxName":"prod",
   "sandboxId":"r5g6660-c5da-11e9-93d4-6d5fc3a66a8e",
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
         "pattern":"^[A-Za-z]+$"
      }
   ],
   "uiAttributes":{
      "documentationLink":"https://www.adobe.com/go/destinations-moviestar-en",
      "category":"mobile",
      "connectionType":"Server-to-server",
      "frequency":"Streaming"
   },
   "identityNamespaces":{
      "external_id":{
         "acceptsAttributes":true,
         "acceptsCustomNamespaces":true,
         "acceptedGlobalNamespaces":{
            "Email":{
               
            }
         }
      },
      "another_id":{
         "acceptsAttributes":true,
         "acceptsCustomNamespaces":true
      },
      "gaid":{
         "acceptsAttributes":true,
         "acceptsCustomNamespaces":true,
         "acceptedGlobalNamespaces":{
            "GAID":{
               
            }
         }
      },
      "idfa":{
         "acceptsAttributes":true,
         "acceptsCustomNamespaces":true,
         "acceptedGlobalNamespaces":{
            "IDFA":{
               
            }
         }
      },
      "email_lc_sha256":{
         "acceptsAttributes":true,
         "acceptsCustomNamespaces":true,
         "transformation":"sha256(lower($))",
         "acceptedGlobalNamespaces":{
            "Email":{
               "requiredTransformation":"sha256(lower($))"
            },
            "Email_LC_SHA256":{
               
            }
         }
      }
   },
   "segmentMappingConfig":{
      "mapExperiencePlatformSegmentName":false,
      "mapExperiencePlatformSegmentId":false,
      "mapUserInput":false,
      "audienceTemplateId":"cbf90a70-96b4-437b-86be-522fbdaabe9c"
   },
   "schemaConfig":{
      "profileFields":[
         {
            "name":"a_custom_attribute",
            "title":"a_custom_attribute",
            "description":"This is a fixed attribute on your destination side that customers can map profile attributes to. For example, the phoneNumber value in Experience Platform could be phoneNo on your side.",
            "type":"string",
            "isRequired":false,
            "readOnly":false,
            "hidden":false
         }
      ],
      "profileRequired":true,
      "segmentRequired":true,
      "identityRequired":true
   },
   "aggregation":{
      "aggregationType":"BEST_EFFORT",
      "bestEffortAggregation":{
         "maxUsersPerRequest":10,
         "splitUserById":false
      }
   },
   "destinationDelivery":[
      {
         "authenticationRule":"CUSTOMER_AUTHENTICATION",
         "destinationServerId":"9c77000a-4559-40ae-9119-a04324a3ecd4"
      }
   ],
   "backfillHistoricalProfileData":true
}
```


## 刪除特定目標配置 {#delete}

您可以向`/authoring/destinations`端點提出DELETE請求，並在請求路徑中提供要刪除的目標配置的ID，以刪除指定的目標配置。

**API格式**

```http
DELETE /authoring/destinations/{INSTANCE_ID}
```

| 參數 | 說明 |
| --------- | ----------- |
| `{INSTANCE_ID}` | 要刪除的目標配置的`id`。 |

**要求**

```shell
curl -X DELETE https://platform.adobe.io/data/core/activation/authoring/destinations/b0780cb5-2bb7-4409-bf2c-c625ca818588 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**回應**

成功的回應會傳回HTTP狀態200，並傳回空的HTTP回應。

## API錯誤處理

目標SDK API端點會遵循一般Experience PlatformAPI錯誤訊息原則。 請參閱平台疑難排解指南中的[API狀態代碼](https://experienceleague.adobe.com/docs/experience-platform/landing/troubleshooting.html?lang=en#api-status-codes)和[要求標題錯誤](https://experienceleague.adobe.com/docs/experience-platform/landing/troubleshooting.html?lang=en#request-header-errors)。

## 後續步驟

閱讀本檔案後，您現在知道如何使用`/authoring/destinations` API端點來設定您的目的地。 請參閱[如何使用目標SDK來設定目標](./configure-destination-instructions.md) ，了解此步驟在設定目標程式中的適用位置。
