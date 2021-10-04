---
description: 此設定可讓您指出基本資訊，例如目的地名稱、類別、說明、標誌等。 此設定中的設定也會決定Experience Platform使用者如何驗證您的目的地、Experience Platform使用者介面中的顯示方式，以及可匯出至您目的地的身分識別。
title: 目標SDK的目標配置選項
exl-id: b7e4db67-2981-4f18-b202-3facda5c8f0b
source-git-commit: 0d5cb5e47b3507cbbd5c34d1ae1fe99d81c67ffc
workflow-type: tm+mt
source-wordcount: '1552'
ht-degree: 4%

---

# 目標配置 {#destination-configuration}

## 總覽 {#overview}

此設定可讓您指出基本資訊，例如目的地名稱、類別、說明、標誌等。 此設定中的設定也會決定Experience Platform使用者如何驗證您的目的地、Experience Platform使用者介面中的顯示方式，以及可匯出至您目的地的身分識別。

您可以使用`/authoring/destinations` API端點來設定本檔案所述的功能。 如需可在端點上執行的完整操作清單，請參閱[目標API端點操作](./destination-configuration-api.md) 。

## 組態範例 {#example-configuration}

以下是虛構目的地Moviestar的設定範例，該目的地在全球的四個位置有端點。 目的地屬於行動目的地類別。 以下各節將劃分此設定的建構方式。

```json
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
      "documentationLink":"http://www.adobe.com/go/destinations-moviestar-en",
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
   "schemaConfig":{
      "profileRequired":false,
      "segmentRequired":true,
      "identityRequired":true
   },
   "destinationDelivery":[
      {
         "authenticationRule":"CUSTOMER_AUTHENTICATION",
         "destinationServerId":"9c77000a-4559-40ae-9119-a04324a3ecd4"
      }
   ],
   "segmentMappingConfig":{
      "mapExperiencePlatformSegmentName":false,
      "mapExperiencePlatformSegmentId":false,
      "mapUserInput":false,
      "audienceTemplateId":"cbf90a70-96b4-437b-86be-522fbdaabe9c"
   },
   "inputSchemaId":"cc8621770a9243b98aba4df79898b1ed",
   "aggregation":{
      "aggregationType":"CONFIGURABLE_AGGREGATION",
      "configurableAggregation":{
         "splitUserById":true,
         "maxBatchAgeInSecs":0,
         "maxNumEventsInBatch":0,
         "aggregationKey":{
            "includeSegmentId":true,
            "includeSegmentStatus":true,
            "includeIdentity":true,
            "oneIdentityPerGroup":false,
            "groups":[
               {
                  "namespaces":[
                     "IDFA",
                     "GAID"
                  ]
               },
               {
                  "namespaces":[
                     "EMAIL"
                  ]
               }
            ]
         }
      }
   }
}
```

| 參數 | 類型 | 說明 |
|---------|----------|------|
| `name` | 字串 | 指出Experience Platform目錄中的目的地標題。 |
| `description` | 字串 | 提供說明，供Adobe用於目的地卡的Experience Platform目的地目錄。 目標不超過4-5句。 |
| `status` | 字串 | 指示目標卡的生命週期狀態。 接受的值為 `TEST`、`PUBLISHED` 和 `DELETED`。首次配置目標時，請使用`TEST`。 |

{style=&quot;table-layout:auto&quot;}

## 客戶驗證設定 {#customer-authentication-configurations}

此區段會在Experience Platform使用者介面中產生帳戶頁面，使用者可在此將Experience Platform連線至其與您目的地的帳戶。 根據您在`authType`欄位中指出的驗證選項，系統會為使用者產生Experience Platform頁面，如下所示：

**承載驗證**

使用者必須輸入從您的目的地取得的不記名Token。

![使用承載驗證呈現UI](./assets/bearer-authentication-ui.png)

**OAuth 2驗證**

使用者選取&#x200B;**[!UICONTROL 連線至目的地]**&#x200B;以觸發OAuth 2驗證流程至您的目的地。

![UI以OAuth 2驗證呈現](./assets/oauth2-authentication-ui.png)


| 參數 | 類型 | 說明 |
|---------|----------|------|
| `customerAuthenticationConfigurations` | 字串 | 指示用於驗證Experience Platform客戶到伺服器的配置。 如需接受的值，請參閱下方的`authType`。 |
| `authType` | 字串 | 接受的值為`OAUTH2, BEARER`。 <br><ul><li> 如果您的目的地支援OAuth 2驗證，請選取`OAUTH2`值並新增OAuth 2的必要欄位，如「目的地SDK OAuth 2驗證」頁面所示。 此外，您應在[目標傳送區段](./destination-configuration.md)中選取`authenticationRule=CUSTOMER_AUTHENTICATION`。 </li><li>對於承載身份驗證，請選擇`BEARER`並在[目標傳送部分](./destination-configuration.md)中選擇`authenticationRule=CUSTOMER_AUTHENTICATION`。</li></ul> |

{style=&quot;table-layout:auto&quot;}

## 客戶資料欄位 {#customer-data-fields}

本節可讓合作夥伴導入自訂欄位。 在上述範例設定中， `customerDataFields`要求使用者在驗證流程中選取端點，並使用目的地指出其客戶ID。 設定會反映在驗證流程中，如下所示：

![自訂欄位驗證流程](./assets/custom-field-authentication-flow.png)

| 參數 | 類型 | 說明 |
|---------|----------|------|
| `name` | 字串 | 提供您要引入的自訂欄位名稱。 |
| `type` | 字串 | 指出您要引入的自訂欄位類型。 接受的值為`string`、`object`、`integer`。 |
| `title` | 字串 | 指出欄位的名稱，如Experience Platform使用者介面中的客戶所見。 |
| `description` | 字串 | 提供自訂欄位的說明。 |
| `isRequired` | 布林值 | 指示目標設定工作流中是否需要此欄位。 |
| `enum` | 字串 | 將自訂欄位轉譯為下拉式功能表，並列出使用者可用的選項。 |
| `pattern` | 字串 | 視需要為自訂欄位強制使用模式。 使用規則運算式來強制模式。 例如，若您的客戶ID未包含數字或底線，請在此欄位中輸入`^[A-Za-z]+$`。 |

{style=&quot;table-layout:auto&quot;}

## UI屬性 {#ui-attributes}

本節說明上述設定中，Adobe應用於Adobe Experience Platform使用者介面中目的地的UI元素。 請參閱下列內容：

| 參數 | 類型 | 說明 |
|---------|----------|------|
| `documentationLink` | 字串 | 指您目的地的[目的地目錄](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/overview.html?lang=en#catalog)中的檔案頁面。 使用`http://www.adobe.com/go/destinations-YOURDESTINATION-en`，其中`YOURDESTINATION`是目的地的名稱。 對於名為Moviestar的目標，您將使用`http://www.adobe.com/go/destinations-moviestar-en` |
| `category` | 字串 | 是指指派給Adobe Experience Platform中目的地的類別。 如需詳細資訊，請參閱[目標類別](https://experienceleague.adobe.com/docs/experience-platform/destinations/destination-types.html)。 使用下列其中一個值：`adobeSolutions, advertising, analytics, cdp, cloudStorage, crm, customerSuccess, database, dmp, ecommerce, email, emailMarketing, enrichment, livechat, marketingAutomation, mobile, personalization, protocols, social, streaming, subscriptions, surveys, tagManagers, voc, warehouses, payments`。 |
| `connectionType` | 字串 | `Server-to-server` 是目前唯一可用的選項。 |
| `frequency` | 字串 | `Streaming` 是目前唯一可用的選項。 |

{style=&quot;table-layout:auto&quot;}

## 對應步驟中的架構配置 {#schema-configuration}

![啟用映射步驟](./assets/enable-mapping-step.png)

使用`schemaConfig`中的參數啟用目標激活工作流的映射步驟。 使用下列所述的參數，您可以判斷Experience Platform使用者是否可將設定檔屬性和/或身分對應至您目的地端的所需結構。

| 參數 | 類型 | 說明 |
|---------|----------|------|
| `profileFields` | 陣列 | *上述範例設定中未顯示。* 新增預先定義 `profileFields`的Experience Platform時，使用者可以選擇將目標屬性對應至目的地端的預先定義屬性。 |
| `profileRequired` | 布林值 | 如果使用者應能將設定檔屬性從Experience Platform對應至目的地端的自訂屬性，請使用`true` ，如上方的範例設定所示。 |
| `segmentRequired` | 布林值 | 請一律使用`segmentRequired:true`。 |
| `identityRequired` | 布林值 | 如果使用者應能將身分識別命名空間從Experience Platform對應至您想要的架構，請使用`true`。 |

{style=&quot;table-layout:auto&quot;}

## 身分和屬性 {#identities-and-attributes}

本節中的參數決定在Experience Platform使用者介面的對應步驟中如何填入目標身分和屬性，使用者可在此將其XDM結構對應至目的地的結構。

Adobe需要知道哪些[!DNL Platform]身分識別客戶將能夠匯出至您的目的地。 有些範例包括[!DNL Experience Cloud ID]、雜湊電子郵件、裝置ID([!DNL IDFA]、[!DNL GAID])。 這些值是[!DNL Platform]身分識別命名空間，客戶可將其對應至您目的地的身分識別命名空間。

身分識別命名空間不需要[!DNL Platform]與目的地之間的1對1通信。
例如，客戶可以將[!DNL Platform] [!DNL IDFA]命名空間從您的目的地對應到[!DNL IDFA]命名空間，或將相同的[!DNL Platform] [!DNL IDFA]命名空間對應到您目的地的[!DNL Customer ID]命名空間。

如需詳細資訊，請參閱[身分命名空間概述](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=en)。

![在UI中呈現目標身分](./assets/target-identities-ui.png)

| 參數 | 類型 | 說明 |
|---------|----------|------|
| `acceptsAttributes` | 布林值 | 指出目的地是否接受標準設定檔屬性。 通常，合作夥伴的檔案會強調顯示這些屬性。 |
| `acceptsCustomNamespaces` | 布林值 | 指出客戶是否可在您的目的地中設定自訂命名空間。 |
| `allowedAttributesTransformation` | 字串 | *範例設定中未顯示*。例如，當[!DNL Platform]客戶有純電子郵件地址作為屬性，且您的平台僅接受雜湊電子郵件時，就會使用。 您可在此提供需要套用的轉換（例如，將電子郵件轉換為小寫，然後雜湊）。 |
| `acceptedGlobalNamespaces` | - | 用於您的平台接受[標準身分識別命名空間](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=en#standard-namespaces)（例如IDFA）時的情況，因此您可以限制Platform使用者僅選取這些身分識別命名空間。 |

{style=&quot;table-layout:auto&quot;}

## 目的地傳送 {#destination-delivery}

| 參數 | 類型 | 說明 |
|---------|----------|------|
| `authenticationRule` | 字串 | 指示[!DNL Platform]客戶如何連接到目標。 接受的值為`CUSTOMER_AUTHENTICATION`、`PLATFORM_AUTHENTICATION`、`NONE`。 <br> <ul><li>如果Platform客戶透過使用者名稱和密碼、承載權杖或其他驗證方法登入您的系統，請使用`CUSTOMER_AUTHENTICATION`。 例如，如果您也在`customerAuthenticationConfigurations`中選取了`authType: OAUTH2`或`authType:BEARER`，則可以選取此選項。 </li><li> 如果Adobe和目標之間存在全局身份驗證系統，並且[!DNL Platform]客戶不需要提供任何身份驗證憑據來連接到目標，請使用`PLATFORM_AUTHENTICATION`。 在這種情況下，必須使用[Credentials](./credentials-configuration.md)配置建立憑據對象。 </li><li>如果不需要任何身份驗證才能將資料發送到目標平台，請使用`NONE`。 </li></ul> |
| `destinationServerId` | 字串 | 用於此目標的[目標伺服器配置](./destination-server-api.md)的`instanceId`。 |
| `backfillHistoricalProfileData` | 布林值 | 控制在將區段啟動至目的地時，是否匯出歷史設定檔資料。<br> <ul><li> `true`: [!DNL Platform] 傳送在啟用區段之前符合區段資格的歷史使用者設定檔。 </li><li> `false`: [!DNL Platform] 僅包含區段啟動後符合區段資格的使用者設定檔。 </li></ul> |

{style=&quot;table-layout:auto&quot;}

## 區段對應設定 {#segment-mapping}

![區段對應設定區段](./assets/segment-mapping-configuration.png)

目的地設定的此區段與區段中繼資料（例如區段名稱或ID）在Experience Platform與目的地之間共用的方式相關。

透過`audienceTemplateId`，本區段也將此設定與[對象中繼資料設定](./audience-metadata-management.md)連結在一起。

上述設定中顯示的參數在[目的地端點API參考](./destination-configuration-api.md)中有說明。

## 聚合策略 {#aggregation}

![配置模板中的聚合策略](./assets/aggregation-configuration.png)

此部分允許您設定將資料導出到目標時Experience Platform將使用的聚合策略。

匯總原則可決定匯出的設定檔在資料匯出中如何結合。 可選擇下列選項：
* 最佳成果匯總
* 可配置聚合（如上面的配置所示）

閱讀有關[使用模板](./message-format.md#using-templating)和[聚合鍵示例](./message-format.md#template-aggregation-key)的部分，了解如何根據所選聚合策略將聚合策略包含在消息轉換模板中。

### 最佳成果匯總 {#best-effort-aggregation}

>[!TIP]
>
>如果您的API端點接受每個API呼叫少於100個設定檔，請使用此選項。

此選項最適合每個請求偏好較少設定檔的目的地，而且偏好以較少資料接收較多請求，而非以較少資料接收較少請求。

使用`maxUsersPerRequest`參數來指定目的地在請求中可採用的設定檔數上限。

### 可配置聚合 {#configurable-aggregation}

如果您想要大批次執行，同一呼叫上有數千個設定檔，此選項最適合使用。 此選項也可讓您根據複雜的匯總規則匯總匯出的設定檔。

此選項可讓您：
* 在對您的目的地發出API呼叫之前，設定要匯總的設定檔最大時間和數量。
* 根據以下項目匯總對應至目的地的匯出設定檔：
   * 區段ID
   * 區段狀態
   * 身分或身分群組

有關聚合參數的詳細解釋，請參閱[目標API端點操作](./destination-configuration-api.md)參考頁，其中描述了每個參數。

<!--

commenting out the `backfillHistoricalProfileData` parameter, which will only be used after an April release

|`backfillHistoricalProfileData` | Boolean | Controls whether historical profile data is exported when segments are activated to the destination. <br> <ul><li> `true`: [!DNL Platform] sends the historical user profiles that qualified for the segment before the segment is activated. </li><li> `false`: [!DNL Platform] only includes user profiles that qualify for the segment after the segment is activated. </li></ul> |

-->
