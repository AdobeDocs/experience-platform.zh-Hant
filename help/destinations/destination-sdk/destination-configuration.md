---
description: 此設定可讓您指出基本資訊，例如目的地名稱、類別、說明、標誌等。 此設定中的設定也會決定Experience Platform使用者如何驗證您的目的地、Experience Platform使用者介面中的顯示方式，以及可匯出至您目的地的身分識別。
title: 串流目的地組態選項，適用於Destination SDK
exl-id: b7e4db67-2981-4f18-b202-3facda5c8f0b
source-git-commit: 21278b39a2dc12771449b9a471ea4182c6b999a3
workflow-type: tm+mt
source-wordcount: '1894'
ht-degree: 4%

---

# 串流目的地設定 {#destination-configuration}

## 總覽 {#overview}

此設定可讓您指出串流目的地的基本資訊，例如目的地名稱、類別、說明等。 此設定中的設定也會決定Experience Platform使用者如何驗證您的目的地、Experience Platform使用者介面中的顯示方式，以及可匯出至您目的地的身分識別。

此設定也會將目的地運作所需的其他設定（目的地伺服器和對象中繼資料）連線至此設定。 請參閱 [下文](./destination-configuration.md#connecting-all-configurations).

您可以使用 `/authoring/destinations` API端點。 閱讀 [目的地API端點作業](./destination-configuration-api.md) 可在端點上執行的操作的完整清單。

## 串流組態範例 {#example-configuration}

這是虛構的串流目的地Moviestar的一個配置示例，它在全球的四個位置有端點。 目的地屬於行動目的地類別。

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
         "name":"endpointRegion",
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
   "aggregation":{
      "aggregationType":"CONFIGURABLE_AGGREGATION",
      "configurableAggregation":{
         "splitUserById":true,
         "maxBatchAgeInSecs":2400,
         "maxNumEventsInBatch":5000,
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
   },
   "backfillHistoricalProfileData":true
}
```

| 參數 | 類型 | 說明 |
|---------|----------|------|
| `name` | 字串 | 指出Experience Platform目錄中的目的地標題。 |
| `description` | 字串 | 在Experience Platform目的地目錄中提供目的地卡片的說明。 目標不超過4-5句。 |
| `status` | 字串 | 指示目標卡的生命週期狀態。 接受的值為 `TEST`、`PUBLISHED` 和 `DELETED`。使用 `TEST` 設定目的地時。 |

{style=&quot;table-layout:auto&quot;}

## 客戶驗證設定 {#customer-authentication-configurations}

目的地設定中的此區段會產生 [配置新目標](/help/destinations/ui/connect-destination.md) 頁面，使用者可在此將Experience Platform連線至其與您目的地的帳戶。 視您在 `authType` 欄位中，系統會為使用者產生「Experience Platform」頁面，如下所示：

### 承載驗證

當您配置承載身份驗證類型時，用戶需要輸入從您的目標獲取的承載令牌。

![使用承載驗證呈現UI](assets/bearer-authentication-ui.png)

### OAuth 2驗證

用戶選擇 **[!UICONTROL 連接到目標]** 觸發OAuth 2驗證流程至您的目的地，如下列Twitter自訂對象目的地範例所示。 如需設定OAuth 2驗證至目的地端點的詳細資訊，請參閱專用 [Destination SDKOAuth 2驗證頁面](./oauth2-authentication.md).

![UI以OAuth 2驗證呈現](assets/oauth2-authentication-ui.png)

| 參數 | 類型 | 說明 |
|---------|----------|------|
| `customerAuthenticationConfigurations` | 字串 | 指示用於驗證Experience Platform客戶到伺服器的配置。 請參閱 `authType` 以取得接受的值。 |
| `authType` | 字串 | 串流目的地的接受值為：<ul><li>`BEARER`。如果您的目的地支援承載驗證，請設定 `"authType":"Bearer"` 和  `"authenticationRule":"CUSTOMER_AUTHENTICATION"` 在 [目的地傳送區段](./destination-configuration.md).</li><li>`OAUTH2`。如果您的目的地支援OAuth 2驗證，請設定 `"authType":"OAUTH2"` 和新增OAuth 2的必要欄位，如 [Destination SDKOAuth 2驗證頁面](./oauth2-authentication.md). 此外，請設定 `"authenticationRule":"CUSTOMER_AUTHENTICATION"` 在 [目的地傳送區段](./destination-configuration.md).</li> |

{style=&quot;table-layout:auto&quot;}

## 客戶資料欄位 {#customer-data-fields}

使用本區段，可在連線至Experience PlatformUI中的目的地時，要求使用者填寫您目的地專屬的自訂欄位。 設定會反映在驗證流程中，如下所示。

![自訂欄位驗證流程](./assets/custom-field-authentication-flow.png)

>[!TIP]
>
>您可以存取並使用範本中客戶資料欄位的客戶輸入。 使用巨集 `{{customerData.name}}`. 例如，如果您要求使用者輸入「客戶ID」欄位，並加上名稱 `userId`，則可使用巨集在範本中存取 `{{customerData.userId}}`. 檢視如何在API端點的URL中使用客戶資料欄位的範例，位於 [目標伺服器配置](/help/destinations/destination-sdk/server-and-template-configuration.md#server-specs).

| 參數 | 類型 | 說明 |
|---------|----------|------|
| `name` | 字串 | 提供您要引入的自訂欄位名稱。 |
| `type` | 字串 | 指出您要引入的自訂欄位類型。 接受的值為 `string`, `object`, `integer`. |
| `title` | 字串 | 指出欄位的名稱，如Experience Platform使用者介面中的客戶所見。 |
| `description` | 字串 | 提供自訂欄位的說明。 |
| `isRequired` | 布林值 | 指示目標設定工作流中是否需要此欄位。 |
| `enum` | 字串 | 將自訂欄位轉譯為下拉式功能表，並列出使用者可用的選項。 |
| `pattern` | 字串 | 視需要為自訂欄位強制使用模式。 使用規則運算式來強制模式。 例如，若您的客戶ID未包含數字或底線，請輸入 `^[A-Za-z]+$` 在此欄位中。 |

{style=&quot;table-layout:auto&quot;}

## UI屬性 {#ui-attributes}

本節說明上述設定中，Adobe應用於Adobe Experience Platform使用者介面中目的地的UI元素。 請參閱下列內容：

![UI屬性設定的影像。](/help/destinations/destination-sdk/assets/ui-attributes-configuration.png)

| 參數 | 類型 | 說明 |
|---------|----------|------|
| `documentationLink` | 字串 | 指 [目的地目錄](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/overview.html?lang=en#catalog) 你的目的地。 使用 `http://www.adobe.com/go/destinations-YOURDESTINATION-en`，其中 `YOURDESTINATION` 是您目的地的名稱。 對於名為Moviestar的目的地，您將使用 `http://www.adobe.com/go/destinations-moviestar-en`. 請注意，此連結只有在Adobe將您的目的地設為現時且檔案已發佈後才有效。 |
| `category` | 字串 | 是指指派給Adobe Experience Platform中目的地的類別。 如需詳細資訊，請閱讀 [目標類別](https://experienceleague.adobe.com/docs/experience-platform/destinations/destination-types.html). 使用下列其中一個值： `adobeSolutions, advertising, analytics, cdp, cloudStorage, crm, customerSuccess, database, dmp, ecommerce, email, emailMarketing, enrichment, livechat, marketingAutomation, mobile, personalization, protocols, social, streaming, subscriptions, surveys, tagManagers, voc, warehouses, payments`. <br> 請注意，您目前只能為每個目的地選取一個類別。 |
| `connectionType` | 字串 | `Server-to-server` 是目前唯一可用的選項。 |
| `frequency` | 字串 | 是指目的地支援的資料匯出類型。 支援的值： <ul><li>`Streaming`</li><li>`Batch`</li></ul> |

{style=&quot;table-layout:auto&quot;}

## 對應步驟中的架構配置 {#schema-configuration}

![啟用映射步驟](./assets/enable-mapping-step.png)

在中使用參數 `schemaConfig` 啟用目標啟動工作流程的對應步驟。 使用下列所述的參數，您可以判斷Experience Platform使用者是否可將設定檔屬性和/或身分對應至您目的地端的所需結構。

| 參數 | 類型 | 說明 |
|---------|----------|------|
| `profileFields` | 陣列 | *上述範例設定中未顯示。* 新增預先定義的 `profileFields`,Experience Platform使用者可以選擇將Platform屬性對應至目的地端的預先定義屬性。 |
| `profileRequired` | 布林值 | 使用 `true` 如果使用者應能將設定檔屬性從Experience Platform對應至目的地端的自訂屬性，如上方的範例設定所示。 |
| `segmentRequired` | 布林值 | 一律使用 `segmentRequired:true`. |
| `identityRequired` | 布林值 | 使用 `true` 如果使用者應能將身分識別命名空間從Experience Platform對應至您所需的架構。 |

{style=&quot;table-layout:auto&quot;}

## 身分和屬性 {#identities-and-attributes}

本節中的參數決定您的目的地接受的身分。 此設定也會填入 [對應步驟](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping) Experience Platform使用者介面的，使用者可將身分和屬性從其XDM結構對應至目的地的結構。

您必須指出 [!DNL Platform] 身分識別客戶可匯出至您的目的地。 例如 [!DNL Experience Cloud ID]，雜湊電子郵件，裝置ID([!DNL IDFA], [!DNL GAID])。 這些值包括 [!DNL Platform] 客戶可從您的目的地對應至身分識別命名空間的身分識別命名空間。 您也可以指出客戶是否可將自訂命名空間對應至您目的地支援的身分識別(`acceptsCustomNamespaces: true`)，以及如果客戶可以將標準XDM屬性對應至您目的地支援的身分識別(`acceptsAttributes: true`)。

身分識別命名空間不需要 [!DNL Platform] 和你的目的地。
例如，客戶可以對應 [!DNL Platform] [!DNL IDFA] 命名空間 [!DNL IDFA] 來自您目的地的命名空間，或者可以對應相同的 [!DNL Platform] [!DNL IDFA] 命名空間 [!DNL Customer ID] 命名空間。

請前往 [身分命名空間概觀](/help/identity-service/namespaces.md).

![在UI中呈現目標身分](./assets/target-identities-ui.png)

| 參數 | 類型 | 說明 |
|---------|----------|------|
| `acceptsAttributes` | 布林值 | 指出客戶是否可將標準設定檔屬性對應至您正在設定的身分。 |
| `acceptsCustomNamespaces` | 布林值 | 指出客戶是否可在您的目的地中設定自訂命名空間。 |
| `transformation` | 字串 | *範例設定中未顯示*. 例如，當 [!DNL Platform] 客戶有純電子郵件地址作為屬性，而您的平台僅接受雜湊電子郵件。 在此物件中，您可以套用需要的轉換（例如，將電子郵件轉換為小寫，然後雜湊）。 如需範例，請參閱 `requiredTransformation` 在 [目的地設定API參考](./destination-configuration-api.md#update). |
| `acceptedGlobalNamespaces` | - | 指出 [標準身分命名空間](/help/identity-service/namespaces.md#standard) （例如IDFA）客戶可對應至您所設定的身分。 <br> 使用 `acceptedGlobalNamespaces`，您可以使用 `"requiredTransformation":"sha256(lower($))"` 小寫和雜湊電子郵件地址或電話號碼。 |

{style=&quot;table-layout:auto&quot;}

## 目的地傳送 {#destination-delivery}

| 參數 | 類型 | 說明 |
|---------|----------|------|
| `authenticationRule` | 字串 | 指示方式 [!DNL Platform] 客戶可連線至您的目的地。 接受的值為 `CUSTOMER_AUTHENTICATION`, `PLATFORM_AUTHENTICATION`, `NONE`. <br> <ul><li>使用 `CUSTOMER_AUTHENTICATION` 如果Platform客戶透過使用者名稱和密碼、承載權杖或其他驗證方法登入您的系統。 例如，如果您也選取了 `authType: OAUTH2` 或 `authType:BEARER` in `customerAuthenticationConfigurations`. </li><li> 使用 `PLATFORM_AUTHENTICATION` 如果Adobe與目的地之間有全域驗證系統，則 [!DNL Platform] 客戶不需要提供任何驗證憑證來連線至您的目的地。 在此情況下，您必須使用 [憑證](./credentials-configuration-api.md) 設定。 </li><li>使用 `NONE` 若無需驗證即可將資料傳送至目的地平台。 </li></ul> |
| `destinationServerId` | 字串 | 此 `instanceId` 的 [目標伺服器配置](./destination-server-api.md) 用於此目的地。 |

{style=&quot;table-layout:auto&quot;}

## 區段對應設定 {#segment-mapping}

![區段對應設定區段](./assets/segment-mapping-configuration.png)

目的地設定的此區段與區段中繼資料（例如區段名稱或ID）在Experience Platform與目的地之間共用的方式相關。

透過 `audienceTemplateId`，本節也會將此設定與 [對象中繼資料設定](./audience-metadata-management.md).

上述設定中所示的參數如 [目的地端點API參考](./destination-configuration-api.md).

## 聚合策略 {#aggregation}

![配置模板中的聚合策略](./assets/aggregation-configuration.png)

此部分允許您設定將資料導出到目標時Experience Platform應使用的聚合策略。

匯總策略確定導出的配置檔案在資料導出中的組合方式。 可選擇下列選項：
* 最佳成果匯總
* 可配置聚合（如上面的配置所示）

閱讀 [使用模板](./message-format.md#using-templating) 和 [聚合鍵示例](./message-format.md#template-aggregation-key) 了解如何根據所選聚合策略將聚合策略包含在消息轉換模板中。

### 最佳成果匯總 {#best-effort-aggregation}

>[!TIP]
>
>如果您的API端點接受每個API呼叫少於100個設定檔，請使用此選項。

此選項最適合每個請求偏好較少設定檔的目的地，而且偏好以較少資料接收較多請求，而非以較少資料接收較少請求。

使用 `maxUsersPerRequest` 參數，指定目的地在請求中可以取用的設定檔數目上限。

### 可配置聚合 {#configurable-aggregation}

如果您想要大批次執行，同一呼叫上有數千個設定檔，此選項最適合使用。 此選項也可讓您根據複雜的匯總規則匯總匯出的設定檔。

此選項可讓您：

* 在對您的目的地發出API呼叫之前，設定要匯總的設定檔最大時間和最大數量。
* 根據以下項目匯總對應至目的地的匯出設定檔：
   * 區段ID;
   * 區段狀態；
   * 身分或身分群組。

>[!NOTE]
>
>為目標使用可配置的聚合選項時，請注意可以用於兩個參數的最小值和最大值 `maxBatchAgeInSecs` （最少1,800和最多3,600）和 `maxNumEventsInBatch` （最少1,000，最多10,000）。

有關聚合參數的詳細說明，請參閱 [目的地API端點作業](./destination-configuration-api.md) 參考頁面，其中會說明每個參數。

## 歷史設定檔資格 {#profile-backfill}

您可以使用 `backfillHistoricalProfileData` 設定中的參數，以判斷是否應將歷史設定檔資格匯出至您的目的地。

| 參數 | 類型 | 說明 |
|---------|----------|------|
| `backfillHistoricalProfileData` | 布林值 | 控制在將區段啟動至目的地時，是否匯出歷史設定檔資料。 <br> <ul><li> `true`: [!DNL Platform] 傳送在啟用區段之前符合區段資格的歷史使用者設定檔。 </li><li> `false`: [!DNL Platform] 僅包含區段啟動後符合區段資格的使用者設定檔。 </li></ul> |

{style=&quot;table-layout:auto&quot;}

## 此設定如何連接目的地的所有必要資訊 {#connecting-all-configurations}

您的部分目的地設定必須透過 [目的地伺服器](./server-and-template-configuration.md) 或 [對象中繼資料設定](./audience-metadata-management.md). 此處描述的目的地設定會參照下列其他兩種設定，以連接所有這些設定：

* 使用 `destinationServerId` 以參考為目的地設定的目的地伺服器和範本設定。
* 使用 `audienceMetadataId` 以參考為目的地設定的對象中繼資料設定。