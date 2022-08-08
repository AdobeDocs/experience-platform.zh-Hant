---
description: 此配置允許您指明基本資訊，如目標名稱、類別、說明、徽標等。 此配置中的設定還確定Experience Platform用戶如何驗證到目標、Experience Platform用戶介面中的顯示方式以及可以導出到目標的身份。
title: 流式傳輸目標配置選項，用於Destination SDK
exl-id: b7e4db67-2981-4f18-b202-3facda5c8f0b
source-git-commit: 75399d2fbe111a296479f8d3404d43c6ba0d50b5
workflow-type: tm+mt
source-wordcount: '1888'
ht-degree: 4%

---

# 流目標配置 {#destination-configuration}

## 總覽 {#overview}

此配置允許您指示流式傳輸目標的基本資訊，如目標名稱、類別、說明等。 此配置中的設定還確定Experience Platform用戶如何驗證到目標、Experience Platform用戶介面中的顯示方式以及可以導出到目標的身份。

此配置還將目標工作所需的其他配置（目標伺服器和受眾元資料）連接到此配置。 閱讀如何在 [下](./destination-configuration.md#connecting-all-configurations)。

您可以使用 `/authoring/destinations` API終結點。 閱讀 [目標API終結點操作](./destination-configuration-api.md) 可在端點上執行的操作的完整清單。

## 流配置示例 {#example-configuration}

這是虛構流目的地Moviestar的一個示例配置，該目的地在全球四個位置具有端點。 目標屬於移動目標類別。

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
| `name` | 字串 | 指示Experience Platform目錄中目標的標題。 |
| `description` | 字串 | 在Experience Platform目標目錄中提供目標卡的說明。 目標不超過4-5句。 |
| `status` | 字串 | 指示目標卡的生命週期狀態。 接受的值為 `TEST`、`PUBLISHED` 和 `DELETED`。使用 `TEST` 在首次配置目標時。 |

{style=&quot;table-layout:auto&quot;}

## 客戶驗證配置 {#customer-authentication-configurations}

目標配置中的此部分將生成 [配置新目標](/help/destinations/ui/connect-destination.md) Experience Platform用戶介面中的「Experience Platform」頁，其中用戶將連接到他們與目標的帳戶。 取決於您在中指示的驗證選項 `authType` 欄位中，將為用戶生成Experience Platform頁，如下所示：

### 承載驗證

配置承載驗證類型時，用戶需要輸入從目標獲取的承載令牌。

![具有承載驗證的UI呈現](assets/bearer-authentication-ui.png)

### OAuth 2身份驗證

用戶選擇 **[!UICONTROL 連接到目標]** 觸發到目標的OAuth 2身份驗證流，如下面的Twitter自定義訪問群體目標示例所示。 有關將OAuth 2身份驗證配置到目標終結點的詳細資訊，請閱讀專用 [Destination SDKOAuth 2身份驗證頁](./oauth2-authentication.md)。

![UI呈現與OAuth 2身份驗證](assets/oauth2-authentication-ui.png)

| 參數 | 類型 | 說明 |
|---------|----------|------|
| `customerAuthenticationConfigurations` | 字串 | 指示用於將Experience Platform客戶驗證到伺服器的配置。 請參閱 `authType` 下面是接受的值。 |
| `authType` | 字串 | 流目標的接受值為：<ul><li>`BEARER`。如果目標支援承載身份驗證，請設定 `"authType":"Bearer"` 和  `"authenticationRule":"CUSTOMER_AUTHENTICATION"` 的 [目標傳遞部分](./destination-configuration.md)。</li><li>`OAUTH2`。如果目標支援OAuth 2身份驗證，請設定 `"authType":"OAUTH2"` 並添加OAuth 2的必填欄位，如 [Destination SDKOAuth 2身份驗證頁](./oauth2-authentication.md)。 此外， `"authenticationRule":"CUSTOMER_AUTHENTICATION"` 的 [目標傳遞部分](./destination-configuration.md)。</li> |

{style=&quot;table-layout:auto&quot;&quot;

## 客戶資料欄位 {#customer-data-fields}

使用此部分可在連接到Experience PlatformUI中的目標時要求用戶填寫特定於目標的自定義欄位。 配置將反映在驗證流中，如下所示。

![自定義欄位驗證流](./assets/custom-field-authentication-flow.png)

>[!TIP]
>
>您可以訪問和使用模板中客戶資料欄位中的客戶輸入。 使用宏 `{{customerData.name}}`。 例如，如果要求用戶輸入「客戶ID」欄位，並且該欄位的名稱 `userId`，可使用宏在模板中訪問 `{{customerData.userId}}`。 查看API終結點的URL中如何使用客戶資料欄位的示例，位於 [目標伺服器配置](/help/destinations/destination-sdk/server-and-template-configuration.md#server-specs)。

| 參數 | 類型 | 說明 |
|---------|----------|------|
| `name` | 字串 | 提供要引入的自定義欄位的名稱。 |
| `type` | 字串 | 指示您要引入的自定義欄位類型。 接受的值為 `string`。 `object`。 `integer`。 |
| `title` | 字串 | 指示欄位的名稱，如客戶在Experience Platform用戶介面中看到的。 |
| `description` | 字串 | 提供自定義欄位的說明。 |
| `isRequired` | 布林值 | 指示目標設定工作流中是否需要此欄位。 |
| `enum` | 字串 | 將自定義欄位呈現為下拉菜單並列出用戶可用的選項。 |
| `pattern` | 字串 | 如果需要，為自定義欄位強制實施模式。 使用規則運算式來強制模式。 例如，如果客戶ID不包括數字或下划線，請輸入 `^[A-Za-z]+$` 的子菜單。 |

{style=&quot;table-layout:auto&quot;&quot;

## UI屬性 {#ui-attributes}

本節指上述配置中的UI元素，該Adobe應用於Adobe Experience Platform用戶介面中的目標。 請參見以下內容：

![UI屬性配置的映像。](/help/destinations/destination-sdk/assets/ui-attributes-configuration.png)

| 參數 | 類型 | 說明 |
|---------|----------|------|
| `documentationLink` | 字串 | 引用中的文檔頁面 [目標目錄](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/overview.html?lang=en#catalog) 你的目的地。 使用 `http://www.adobe.com/go/destinations-YOURDESTINATION-en`，也請參見Wiki頁。 `YOURDESTINATION` 是目標的名稱。 對於名為Moviestar的目標，您將使用 `http://www.adobe.com/go/destinations-moviestar-en`。 請注意，此連結僅在Adobe設定目標即時並發佈文檔後才起作用。 |
| `category` | 字串 | 指分配給您在Adobe Experience Platform的目標的類別。 有關詳細資訊，請閱讀 [目標類別](https://experienceleague.adobe.com/docs/experience-platform/destinations/destination-types.html)。 使用以下值之一： `adobeSolutions, advertising, analytics, cdp, cloudStorage, crm, customerSuccess, database, dmp, ecommerce, email, emailMarketing, enrichment, livechat, marketingAutomation, mobile, personalization, protocols, social, streaming, subscriptions, surveys, tagManagers, voc, warehouses, payments`。 <br> 請注意，當前每個目標只能選擇一個類別。 |
| `connectionType` | 字串 | `Server-to-server` 是當前唯一可用的選項。 |
| `frequency` | 字串 | 引用目標支援的資料導出類型。 支援的值： <ul><li>`Streaming`</li><li>`Batch`</li></ul> |

{style=&quot;table-layout:auto&quot;&quot;

## 映射步驟中的架構配置 {#schema-configuration}

![啟用映射步驟](./assets/enable-mapping-step.png)

使用中的參數 `schemaConfig` 啟用目標激活工作流的映射步驟。 通過使用下面描述的參數，您可以確定Experience Platform用戶是否可以將配置檔案屬性和/或標識映射到目標端的所需架構。

| 參數 | 類型 | 說明 |
|---------|----------|------|
| `profileFields` | 陣列 | *上面的示例配置中未顯示。* 添加預定義項時 `profileFields`,Experience Platform用戶可以選擇將平台屬性映射到目標側的預定義屬性。 |
| `profileRequired` | 布林值 | 使用 `true` 如果用戶應能將配置檔案屬性從Experience Platform映射到目標側的自定義屬性，如上面的示例配置所示。 |
| `segmentRequired` | 布林值 | 始終使用 `segmentRequired:true`。 |
| `identityRequired` | 布林值 | 使用 `true` 如果用戶應能將標識命名空間從Experience Platform映射到所需的架構。 |

{style=&quot;table-layout:auto&quot;&quot;

## 標識和屬性 {#identities-and-attributes}

本節中的參數確定目標接受的標識。 此配置還填充中的目標標識和屬性 [映射步驟](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping) Experience Platform用戶介面中，用戶將標識和屬性從其XDM架構映射到目標中的架構。

必須指明 [!DNL Platform] 標識客戶能夠導出到您的目標。 一些示例 [!DNL Experience Cloud ID]，散列電子郵件，設備ID([!DNL IDFA]。 [!DNL GAID])。 這些值 [!DNL Platform] 客戶可以從目標映射到標識命名空間的標識命名空間。 您還可以指示客戶是否可以將自定義命名空間映射到目標支援的標識。

標識命名空間不需要在 [!DNL Platform] 和你的目的地。
例如，客戶可以 [!DNL Platform] [!DNL IDFA] 命名空間到 [!DNL IDFA] 命名空間，或者它們可以映射 [!DNL Platform] [!DNL IDFA] 命名空間到 [!DNL Customer ID] 目標中的命名空間。

閱讀 [Identity Namespace概述](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=en)。

![在UI中呈現目標標識](./assets/target-identities-ui.png)

| 參數 | 類型 | 說明 |
|---------|----------|------|
| `acceptsAttributes` | 布林值 | 指示目標是否接受標準配置檔案屬性。 通常，這些屬性會在合作夥伴的文檔中突出顯示。 |
| `acceptsCustomNamespaces` | 布林值 | 指示客戶是否可以在目標中設定自定義命名空間。 |
| `transformation` | 字串 | *未在示例配置中顯示*。 例如，在 [!DNL Platform] 客戶將純電子郵件地址作為屬性，而您的平台只接受經過散列的電子郵件。 在此對象中，可以應用需要的轉換（例如，將電子郵件轉換為小寫，然後是哈希）。 有關示例，請參見 `requiredTransformation` 的 [目標配置API參考](./destination-configuration-api.md#update)。 |
| `acceptedGlobalNamespaces` | - | 用於平台接受 [標準標識命名空間](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=en#standard-namespaces) （例如，IDFA），因此您可以限制平台用戶只選擇這些標識命名空間。 |

{style=&quot;table-layout:auto&quot;&quot;

## 目標傳遞 {#destination-delivery}

| 參數 | 類型 | 說明 |
|---------|----------|------|
| `authenticationRule` | 字串 | 指示如何 [!DNL Platform] 客戶連接到您的目標。 接受的值為 `CUSTOMER_AUTHENTICATION`。 `PLATFORM_AUTHENTICATION`。 `NONE`。 <br> <ul><li>使用 `CUSTOMER_AUTHENTICATION` 如果平台客戶通過用戶名和密碼、持有者令牌或其他身份驗證方法登錄到您的系統。 例如，如果同時選擇了 `authType: OAUTH2` 或 `authType:BEARER` 在 `customerAuthenticationConfigurations`。 </li><li> 使用 `PLATFORM_AUTHENTICATION` 如果Adobe與目標之間有全局身份驗證系統， [!DNL Platform] 客戶不需要提供任何身份驗證憑據來連接到目標。 在這種情況下，必須使用 [憑據](./credentials-configuration-api.md) 配置。 </li><li>使用 `NONE` 如果向目標平台發送資料不需要身份驗證。 </li></ul> |
| `destinationServerId` | 字串 | 的 `instanceId` 的 [目標伺服器配置](./destination-server-api.md) 用於此目標。 |

{style=&quot;table-layout:auto&quot;&quot;

## 段映射配置 {#segment-mapping}

![段映射配置部分](./assets/segment-mapping-configuration.png)

目標配置的這一部分涉及段元資料（如段名稱或ID）在Experience Platform與目標之間應如何共用。

通過 `audienceTemplateId`，本節還將此配置與 [觀眾元資料配置](./audience-metadata-management.md)。

上述配置中顯示的參數在 [目標終結點API引用](./destination-configuration-api.md)。

## 聚合策略 {#aggregation}

![配置模板中的聚合策略](./assets/aggregation-configuration.png)

此部分允許您設定將資料導出到目標時Experience Platform應使用的聚合策略。

聚合策略確定導出的配置檔案如何在資料導出中組合。 可選擇下列選項：
* 盡力聚合
* 可配置聚合（如上配置所示）

閱讀上的部分 [使用模板](./message-format.md#using-templating) 和 [聚合鍵示例](./message-format.md#template-aggregation-key) 瞭解如何根據所選聚合策略將聚合策略包含在消息轉換模板中。

### 盡力聚合 {#best-effort-aggregation}

>[!TIP]
>
>如果API終結點每個API調用接受的配置檔案少於100個，則使用此選項。

此選項最適合於每個請求選擇較少的配置檔案的目標，並且寧可使用較少的資料接收更多的請求，也不願使用較少的資料請求。

使用 `maxUsersPerRequest` 參數，以指定目標在請求中可接收的最大配置檔案數。

### 可配置聚合 {#configurable-aggregation}

如果您希望批量較大，並且同一呼叫上有數千個配置檔案，則此選項最有效。 此選項還允許您基於複雜的聚合規則聚合導出的配置檔案。

此選項允許您：

* 在對目標進行API調用之前，設定要聚合的配置檔案的最大時間和最大數量。
* 根據以下資訊聚合映射到目標的導出配置檔案：
   * 段ID;
   * 段狀態；
   * 身份或身份組。

>[!NOTE]
>
>在為目標使用可配置的聚合選項時，請注意可用於這兩個參數的最小值和最大值 `maxBatchAgeInSecs` （最少1,800和最多3,600） `maxNumEventsInBatch` （最少1000，最多1000）。

有關聚合參數的詳細說明，請參閱 [目標API終結點操作](./destination-configuration-api.md) 參考頁，其中描述了每個參數。

## 歷史配置檔案資格 {#profile-backfill}

您可以使用 `backfillHistoricalProfileData` 目標配置中的參數，以確定是否應將歷史配置檔案資格導出到目標。

| 參數 | 類型 | 說明 |
|---------|----------|------|
| `backfillHistoricalProfileData` | 布林值 | 控制在將段激活到目標時是否導出歷史配置檔案資料。 <br> <ul><li> `true`: [!DNL Platform] 發送在激活段之前符合段的歷史用戶配置檔案。 </li><li> `false`: [!DNL Platform] 僅包括激活段後符合段條件的用戶配置檔案。 </li></ul> |

{style=&quot;table-layout:auto&quot;&quot;

## 此配置如何連接目標的所有必要資訊 {#connecting-all-configurations}

您的某些目標設定必須通過 [目標伺服器](./server-and-template-configuration.md) 或 [觀眾元資料配置](./audience-metadata-management.md)。 此處描述的目標配置通過引用以下兩個其他配置來連接所有這些設定：

* 使用 `destinationServerId` 引用為目標設定的目標伺服器和模板配置。
* 使用 `audienceMetadataId` 引用為目標設定的受眾元資料配置。