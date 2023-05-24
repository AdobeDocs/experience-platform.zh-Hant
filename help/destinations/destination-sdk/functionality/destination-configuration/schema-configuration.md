---
description: 瞭解如何為使用Destination SDK構建的目標配置合作夥伴架構。
title: 合作夥伴架構配置
source-git-commit: acb7075f49b4194c31371d2de63709eea7821329
workflow-type: tm+mt
source-wordcount: '1715'
ht-degree: 5%

---


# 合作夥伴架構配置

Experience Platform 會使用結構，以一致且可重複使用的方式說明資料結構。當資料被引入平台時，它是根據XDM架構進行結構化的。 有關架構組成模型（包括設計原則和最佳做法）的詳細資訊，請參見 [架構組合基礎](../../../../xdm/schema/composition.md)。

在構建具有Destination SDK的目標時，您可以定義目標平台要使用的自己的合作夥伴架構。 這使用戶能夠將配置檔案屬性從平台映射到目標平台識別的特定欄位，所有欄位都在平台UI中。

在為目標配置合作夥伴架構時，您可以微調目標平台支援的欄位映射，例如：

* 允許用戶映射 `phoneNumber` XDM屬性 `phone` 目標平台支援的屬性。
* 建立動態夥伴架構，Experience Platform可動態調用該架構以檢索目標中所有支援的屬性的清單。
* 定義目標平台需要的必需欄位映射。

要瞭解此元件在與Destination SDK建立的整合中的位置，請參閱 [配置選項](../configuration-options.md) 文檔，或參閱有關如何 [使用Destination SDK配置基於檔案的目標](../../guides/configure-file-based-destination-instructions.md#create-server-file-configuration)。

您可以通過 `/authoring/destinations` 端點。 有關詳細的API調用示例，請參閱以下API參考頁，在這些示例中可以配置此頁中顯示的元件。

* [建立目標配置](../../authoring-api/destination-configuration/create-destination-configuration.md)
* [更新目標配置](../../authoring-api/destination-configuration/update-destination-configuration.md)

本文介紹可用於目標的所有支援的架構配置選項，並顯示客戶將在平台UI中看到的內容。

>[!IMPORTANT]
>
>Destination SDK支援的所有參數名和值均 **區分大小寫**。 為避免區分大小寫錯誤，請完全按文檔所示使用參數名稱和值。

## 支援的整合類型 {#supported-integration-types}

有關哪些類型的整合支援本頁所述功能的詳細資訊，請參閱下表。

| 整合類型 | 支援功能 |
|---|---|
| 即時（流）整合 | 是 |
| 基於檔案（批處理）的整合 | 是 |

## 支援的架構配置 {#supported-schema-types}

Destination SDK支援多個架構配置：

* 通過 `profileFields` 陣列 `schemaConfig` 的子菜單。 在靜態架構中，定義應顯示在Experience PlatformUI中的每個目標屬性 `profileFields` 陣列。 如果需要更新架構，則必須 [更新目標配置](../../authoring-api/destination-configuration/update-destination-configuration.md)。
* 動態架構使用稱為 [動態架構伺服器](../../authoring-api/destination-server/create-destination-server.md)，以根據您自己的API動態生成架構。 動態架構不使用 `profileFields` 陣列。 如果需要更新架構，則無需 [更新目標配置](../../authoring-api/destination-configuration/update-destination-configuration.md)。 相反，動態架構伺服器會從API中檢索更新的架構。
* 在架構配置中，您可以選擇添加所需（或預定義）映射。 這些映射是用戶可以在平台UI中查看的，但在設定到目標的連接時，它們無法修改這些映射。 例如，您可以強制電子郵件地址欄位始終發送到目標。

的 `schemaConfig` section使用多個配置參數，具體取決於所需的架構類型，如下面各節所示。

## 建立靜態架構 {#attributes-schema}

要使用配置檔案屬性建立靜態架構，請在 `profileFields` 如下所示。

```json
"schemaConfig":{
      "profileFields":[
           {
              "name":"phoneNo",
              "title":"phoneNo",
              "description":"This is a fixed attribute on your destination side that customers can map profile attributes to. For example, the mobilePhone.number value in Experience Platform could be phoneNo on your side.",
              "type":"string",
              "isRequired":false,
              "readOnly":false,
              "hidden":false
           },
                      {
              "name":"firstName",
              "title":"firstName",
              "description":"This is a fixed attribute on your destination side that customers can map profile attributes to. For example, the person.name.firstName value in Experience Platform could be firstName on your side.",
              "type":"string",
              "isRequired":false,
              "readOnly":false,
              "hidden":false
           },
                      {
              "name":"lastName",
              "title":"lastName",
              "description":"This is a fixed attribute on your destination side that customers can map profile attributes to. For example, the person.name.lastName value in Experience Platform could be phoneNo on your side.",
              "type":"string",
              "isRequired":false,
              "readOnly":false,
              "hidden":false
           }
        ],
      "useCustomerSchemaForAttributeMapping":false,
      "profileRequired":true,
      "segmentRequired":true,
      "identityRequired":true
}
```

| 參數 | 類型 | 必填/選填 | 說明 |
|---------|----------|------|---|
| `profileFields` | 陣列 | 選填 | 定義目標平台接受的目標屬性陣列，客戶可以將其配置檔案屬性映射到該陣列。 使用 `profileFields` 陣列，可以忽略 `useCustomerSchemaForAttributeMapping` 參數。 |
| `useCustomerSchemaForAttributeMapping` | 布林值 | 選填 | 啟用或禁用屬性從客戶方案到您在中定義的屬性的映射 `profileFields` 陣列。 <ul><li>如果設定為 `true`，用戶只能在映射欄位中查看源列。 `profileFields` 在此情況下不適用。</li><li>如果設定為 `false`，用戶可以將源屬性從其架構映射到您在 `profileFields` 陣列。</li></ul> 預設值為 `false`。 |
| `profileRequired` | 布林值 | 選填 | 使用 `true` 如果用戶應能夠將配置檔案屬性從Experience Platform映射到目標平台上的自定義屬性。 |
| `segmentRequired` | 布林值 | 必填 | 此參數是Destination SDK所必需的，應始終設定為 `true`。 |
| `identityRequired` | 布林值 | 必填 | 設定為 `true` 如果用戶能夠映射 [標識類型](identity-namespace-configuration.md) 從Experience Platform到在 `profileFields` 陣列。 |

{style="table-layout:auto"}

生成的UI體驗顯示在下面的影像中。

當用戶選擇目標映射時，他們可以查看在 `profileFields` 陣列。

![顯示目標屬性螢幕的UI影像。](../../assets/functionality/destination-configuration/select-attributes.png)

選擇屬性後，它們可以在目標欄位列中看到這些屬性。

![顯示具有屬性的靜態目標架構的UI影像](../../assets/functionality/destination-configuration/static-schema-attributes.png)

## 建立動態架構 {#dynamic-schema-configuration}

Destination SDK支援建立動態夥伴架構。 與靜態模式不同，動態模式不使用 `profileFields` 陣列。 相反，動態架構使用動態架構伺服器，該伺服器連接到您自己的API，從中檢索架構配置。

>[!IMPORTANT]
>
>建立動態架構之前，必須 [建立動態模式伺服器](../../authoring-api/destination-server/create-destination-server.md)。

在動態架構配置中， `profileFields` 陣列被替換為 `dynamicSchemaConfig` ，如下所示。

```json
"schemaConfig":{
   "dynamicSchemaConfig":{
      "dynamicEnum": {
         "authenticationRule":"CUSTOMER_AUTHENTICATION",
         "destinationServerId":"DYNAMIC_SCHEMA_SERVER_ID",
         "value": "Schema Name",
         "responseFormat": "SCHEMA"
      }
   },
   "profileRequired":true,
   "segmentRequired":true,
   "identityRequired":true
}
```

| 參數 | 類型 | 必填/選填 | 說明 |
|---------|----------|------|---|
| `dynamicEnum.authenticationRule` | 字串 | 必填 | 指示如何 [!DNL Platform] 客戶連接到您的目標。 接受的值為 `CUSTOMER_AUTHENTICATION`。 `PLATFORM_AUTHENTICATION`。 `NONE`。 <br> <ul><li>使用 `CUSTOMER_AUTHENTICATION` 如果平台客戶通過所述的任何身份驗證方法登錄到您的系統 [這裡](customer-authentication.md)。 </li><li> 使用 `PLATFORM_AUTHENTICATION` 如果Adobe與目標之間有全局身份驗證系統， [!DNL Platform] 客戶不需要提供任何身份驗證憑據來連接到目標。 在這種情況下，你必須 [建立憑據對象](../../credentials-api/create-credential-configuration.md) 使用憑據API。 </li><li>使用 `NONE` 如果向目標平台發送資料不需要身份驗證。 </li></ul> |
| `dynamicEnum.destinationServerId` | 字串 | 必填 | 的 `instanceId` 動態架構伺服器。 此目標伺服器包括將調用以檢索動態架構的API終結點。 |
| `dynamicEnum.value` | 字串 | 必填 | 動態架構的名稱，如動態架構伺服器配置中所定義。 |
| `dynamicEnum.responseFormat` | 字串 | 必填 | 始終設定為 `SCHEMA` 定義動態架構時。 |
| `profileRequired` | 布林值 | 選填 | 使用 `true` 如果用戶應能夠將配置檔案屬性從Experience Platform映射到目標平台上的自定義屬性。 |
| `segmentRequired` | 布林值 | 必填 | 此參數是Destination SDK所必需的，應始終設定為 `true`。 |
| `identityRequired` | 布林值 | 必填 | 設定為 `true` 如果用戶能夠映射 [標識類型](identity-namespace-configuration.md) 從Experience Platform到在 `profileFields` 陣列。 |

{style="table-layout:auto"}

## 必需的映射 {#required-mappings}

在架構配置中，除靜態或動態架構外，您還可以選擇添加所需（或預定義）映射。 這些映射是用戶可以在平台UI中查看的，但在設定到目標的連接時，它們無法修改這些映射。

例如，您可以強制電子郵件地址欄位始終發送到目標。

>[!NOTE]
>
>當前支援以下所需映射的組合：
>* 您可以配置必需的源欄位和必需的目標欄位。 在這種情況下，用戶不能編輯或選擇這兩個欄位中的任何一個，只能查看選擇。
>* 您只能配置所需的目標欄位。 在這種情況下，將允許用戶選擇要映射到目標的源欄位。
>
> 當前僅配置必需的源欄位 *不* 支援。

請參見下面兩個具有所需映射的架構配置示例以及這些示例在的映射步驟中 [將資料激活至批處理目標工作流](../../../ui/activate-batch-profile-destinations.md)。


>[!BEGINTABS]

>[!TAB 所需的源和目標映射]

以下示例顯示了所需的源映射和目標映射。 如果源欄位和目標欄位都指定為必需的映射，則用戶不能選擇或編輯這兩個欄位中的任何一個，並且只能查看預定義的選擇。

```json
"schemaConfig": {
    "requiredMappingsOnly": true,
    "requiredMappings": [
      {
        "sourceType": "text/x.schema-path",
        "source": "personalEmail.address",
        "destination": "personalEmail.address"
      }
    ] 
}
```

| 參數 | 類型 | 必填/選填 | 說明 |
|---|---|---|---|
| `requiredMappingsOnly` | 布林值 | 選填 | 如果此值設定為true，則除了在中定義的必需映射之外，用戶無法映射激活流中的其他屬性和標識 `requiredMappings` 陣列。 |
| `requiredMappings.sourceType` | 字串 | 必填 | 指示 `source` 的子菜單。 支援的值： <ul><li>`text/x.schema-path`:在 `source` 欄位是XDM架構中的配置檔案屬性。</li><li>`text/x.aep-xl`:在 `source` 欄位由規則運算式定義。 範例：`iif(segmentMembership.ups.aep_seg_id.status==\"exited\", \"1\", \"0\")`</li><li>`text/plain`:在 `source` 欄位由宏模板定義。 當前，唯一支援的宏模板是 `metadata.segment.alias`。</li></ul> |
| `requiredMappings.source` | 字串 | 必填 | 指示源欄位的值。 支援的值類型： <ul><li>XDM配置檔案屬性。 範例: `personalEmail.address`. 如果源屬性是XDM配置檔案屬性，請設定 `sourceType` 參數 `text/x.schema-path`。</li><li>規則運算式. 範例: `iif(segmentMembership.ups.aep_seg_id.status==\"exited\", \"1\", \"0\")`. 如果源屬性是規則運算式，請設定 `sourceType` 參數 `text/x.aep-xl`。</li><li>宏模板。 範例:`metadata.segment.alias`. 如果源屬性是宏模板，請設定 `sourceType` 參數 `text/plain`。 當前，唯一支援的宏模板是 `metadata.segment.alias`。</li></ul> |
| `requiredMappings.destination` | 字串 | 必填 | 指示目標欄位的值。 如果源欄位和目標欄位都指定為必需的映射，則用戶不能選擇或編輯這兩個欄位中的任何一個，並且只能查看選擇。 |

{style="table-layout:auto"}

因此， **[!UICONTROL 源欄位]** 和 **[!UICONTROL 目標欄位]** 平台UI中的部分將呈灰色顯示。

![UI激活流中所需映射的影像。](../../assets/functionality/destination-configuration/required-mappings-2.png)

>[!TAB 所需的目標映射]

以下示例顯示了所需的目標映射。 如果只根據需要指定目標欄位，則用戶可以選擇要映射到該目標欄位的源欄位。

```json
"schemaConfig": {
    "requiredMappingsOnly": true,
    "requiredMappings": [
      {
        "destination": "identityMap.ExamplePartner_ID",
        "mandatoryRequired": true,
        "primaryKeyRequired": true
      }
    ] 
}
```

| 參數 | 類型 | 必填/選填 | 說明 |
|---|---|---|---|
| `requiredMappingsOnly` | 布林值 | 選填 | 如果此值設定為true，則除了在中定義的必需映射之外，用戶無法映射激活流中的其他屬性和標識 `requiredMappings` 陣列。 |
| `requiredMappings.destination` | 字串 | 必填 | 指示目標欄位的值。 當僅指定目標欄位時，用戶可以選擇要映射到目標的源欄位。 |
| `mandatoryRequired` | 布林值 | 選填 | 指示是否應將映射標籤為 [必備屬性](../../../ui/activate-batch-profile-destinations.md#mandatory-attributes)。 |
| `primaryKeyRequired` | 布林值 | 選填 | 指示是否應將映射標籤為 [重複資料消除密鑰](../../../ui/activate-batch-profile-destinations.md#deduplication-keys)。 |

{style="table-layout:auto"}

因此， **[!UICONTROL 目標欄位]** 「Platform UI（平台UI）」中的「Paltom UI（平台UI）」部分顯示為灰色， **[!UICONTROL 源欄位]** 部分處於活動狀態，用戶可與其進行交互。 的 **[!UICONTROL 強制鍵]** 和 **[!UICONTROL 重複資料消除密鑰]** 選項處於活動狀態，用戶無法更改它們。

![UI激活流中所需映射的影像。](../../assets/functionality/destination-configuration/required-mappings-1.png)

>[!ENDTABS]

## 後續步驟 {#next-steps}

閱讀本文後，您應該更好地瞭解Destination SDK支援哪些架構類型以及如何配置您的架構。

要瞭解有關其他目標元件的詳細資訊，請參閱以下文章：

* [客戶驗證](customer-authentication.md)
* [OAuth2身份驗證](oauth2-authentication.md)
* [UI屬性](ui-attributes.md)
* [客戶資料欄位](customer-data-fields.md)
* [標識命名空間配置](identity-namespace-configuration.md)
* [支援的映射配置](supported-mapping-configurations.md)
* [目標傳遞](destination-delivery.md)
* [受眾元資料配置](audience-metadata-configuration.md)
* [聚合策略](aggregation-policy.md)
* [批配置](batch-configuration.md)
* [歷史配置檔案資格](historical-profile-qualifications.md)