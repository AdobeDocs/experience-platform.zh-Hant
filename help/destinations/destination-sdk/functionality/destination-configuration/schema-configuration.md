---
description: 了解如何為使用Destination SDK建置的目的地設定合作夥伴結構。
title: 合作夥伴架構配置
source-git-commit: acb7075f49b4194c31371d2de63709eea7821329
workflow-type: tm+mt
source-wordcount: '1715'
ht-degree: 5%

---


# 合作夥伴架構配置

Experience Platform 會使用結構，以一致且可重複使用的方式說明資料結構。將資料內嵌至Platform時，會根據XDM架構進行結構化。 如需結構構成模型的詳細資訊，包括設計原則和最佳實務，請參閱 [綱要構成基本知識](../../../../xdm/schema/composition.md).

使用Destination SDK建立目的地時，您可以定義要由目的地平台使用的專屬合作夥伴結構。 這可讓使用者將設定檔屬性從Platform對應至目的地平台所辨識的特定欄位，全部在Platform UI中。

為目的地設定合作夥伴架構時，您可以微調目的地平台支援的欄位對應，例如：

* 允許使用者對應 `phoneNumber` XDM屬性至 `phone` 目的地平台支援的屬性。
* 建立動態合作夥伴結構，Experience Platform可以動態呼叫，以擷取目的地內所有支援屬性的清單。
* 定義目標平台需要的必填欄位對應。

若要了解此元件在透過Destination SDK建立的整合中的插入位置，請參閱 [配置選項](../configuration-options.md) 檔案，或參閱如何 [使用Destination SDK配置基於檔案的目標](../../guides/configure-file-based-destination-instructions.md#create-server-file-configuration).

您可以透過 `/authoring/destinations` 端點。 如需詳細API呼叫範例，請參閱下列API參考頁面，您可在其中設定本頁面所示的元件。

* [建立目標配置](../../authoring-api/destination-configuration/create-destination-configuration.md)
* [更新目標配置](../../authoring-api/destination-configuration/update-destination-configuration.md)

本文說明您可用於目的地的所有支援結構設定選項，並說明客戶在Platform UI中會看到什麼內容。

>[!IMPORTANT]
>
>Destination SDK支援的所有參數名稱和值均為 **區分大小寫**. 為避免區分大小寫錯誤，請使用參數名稱和值，如說明檔案所示。

## 支援的整合類型 {#supported-integration-types}

如需詳細資訊，請參閱下表以了解哪些類型的整合支援本頁面所述的功能。

| 整合類型 | 支援功能 |
|---|---|
| 即時（串流）整合 | 是 |
| 檔案式（批次）整合 | 是 |

## 支援的架構配置 {#supported-schema-types}

Destination SDK支援多種架構配置：

* 靜態結構可透過 `profileFields` 陣列 `schemaConfig` 區段。 在靜態結構中，您定義應顯示在Experience PlatformUI中的每個目標屬性，位於 `profileFields` 陣列。 如果您需要更新結構，則必須 [更新目標配置](../../authoring-api/destination-configuration/update-destination-configuration.md).
* 動態結構使用其他目的地伺服器類型，稱為 [動態綱要伺服器](../../authoring-api/destination-server/create-destination-server.md)，以根據您自己的API動態產生結構。 動態結構不使用 `profileFields` 陣列。 如果您需要更新結構，則不需要 [更新目標配置](../../authoring-api/destination-configuration/update-destination-configuration.md). 而動態結構伺服器會從您的API中擷取更新的結構。
* 在架構設定中，您可以選擇新增必要（或預先定義）對應。 這些是使用者可在Platform UI中檢視的對應，但當設定與您目的地的連線時，無法修改這些對應。 例如，您可以強制執行電子郵件地址欄位，以一律傳送至目的地。

此 `schemaConfig` section會根據所需的架構類型使用多個配置參數，如下節所示。

## 建立靜態結構 {#attributes-schema}

若要使用設定檔屬性建立靜態結構，請在 `profileFields` 陣列，如下所示。

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
| `profileFields` | 陣列 | 選填 | 定義目標平台接受的目標屬性陣列，客戶可將其設定檔屬性對應至該陣列。 使用 `profileFields` 陣列，您可以忽略 `useCustomerSchemaForAttributeMapping` 參數。 |
| `useCustomerSchemaForAttributeMapping` | 布林值 | 選填 | 啟用或停用從客戶結構到您在 `profileFields` 陣列。 <ul><li>若設為 `true`，則使用者只會在對應欄位中看見來源欄。 `profileFields` 不適用於此情況。</li><li>若設為 `false`，使用者可將來源屬性從其結構對應至您在 `profileFields` 陣列。</li></ul> 預設值為 `false`。 |
| `profileRequired` | 布林值 | 選填 | 使用 `true` 如果使用者應能將設定檔屬性從Experience Platform對應至目的地平台上的自訂屬性。 |
| `segmentRequired` | 布林值 | 必填 | 此參數是Destination SDK的必要參數，應一律設為 `true`. |
| `identityRequired` | 布林值 | 必填 | 設為 `true` 如果使用者應能對應 [身分類型](identity-namespace-configuration.md) 從Experience Platform到您在 `profileFields` 陣列。 |

{style="table-layout:auto"}

產生的UI體驗會顯示在下方的影像中。

當使用者選取目標對應時，可以看到 `profileFields` 陣列。

![顯示目標屬性畫面的UI影像。](../../assets/functionality/destination-configuration/select-attributes.png)

選取屬性後，他們可以在目標欄位欄中看到這些屬性。

![顯示具有屬性的靜態目標架構的UI影像](../../assets/functionality/destination-configuration/static-schema-attributes.png)

## 建立動態結構 {#dynamic-schema-configuration}

Destination SDK支援建立動態合作夥伴結構。 與靜態結構相反，動態結構不使用 `profileFields` 陣列。 動態結構會使用動態結構伺服器，從中連線至您自己的API，以擷取結構配置。

>[!IMPORTANT]
>
>建立動態結構之前，您必須 [建立動態架構伺服器](../../authoring-api/destination-server/create-destination-server.md).

在動態架構設定中， `profileFields` 陣列取代為 `dynamicSchemaConfig` 區段，如下所示。

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
| `dynamicEnum.authenticationRule` | 字串 | 必填 | 指示方式 [!DNL Platform] 客戶可連線至您的目的地。 接受的值為 `CUSTOMER_AUTHENTICATION`, `PLATFORM_AUTHENTICATION`, `NONE`. <br> <ul><li>使用 `CUSTOMER_AUTHENTICATION` 如果Platform客戶透過上述任何驗證方法登入您的系統 [此處](customer-authentication.md). </li><li> 使用 `PLATFORM_AUTHENTICATION` 如果Adobe與目的地之間有全域驗證系統，則 [!DNL Platform] 客戶不需要提供任何驗證憑證來連線至您的目的地。 在這種情況下，您必須 [建立憑據對象](../../credentials-api/create-credential-configuration.md) 使用憑證API。 </li><li>使用 `NONE` 若無需驗證即可將資料傳送至目的地平台。 </li></ul> |
| `dynamicEnum.destinationServerId` | 字串 | 必填 | 此 `instanceId` 動態綱要伺服器。 此目的地伺服器包含API端點，Experience Platform會呼叫該端點來擷取動態結構。 |
| `dynamicEnum.value` | 字串 | 必填 | 動態架構的名稱，如動態架構伺服器配置中所定義。 |
| `dynamicEnum.responseFormat` | 字串 | 必填 | 一律設為 `SCHEMA` 定義動態綱要時。 |
| `profileRequired` | 布林值 | 選填 | 使用 `true` 如果使用者應能將設定檔屬性從Experience Platform對應至目的地平台上的自訂屬性。 |
| `segmentRequired` | 布林值 | 必填 | 此參數是Destination SDK的必要參數，應一律設為 `true`. |
| `identityRequired` | 布林值 | 必填 | 設為 `true` 如果使用者應能對應 [身分類型](identity-namespace-configuration.md) 從Experience Platform到您在 `profileFields` 陣列。 |

{style="table-layout:auto"}

## 必要對應 {#required-mappings}

在架構配置中，除了靜態或動態架構外，您還可以選擇添加所需（或預定義）映射。 這些是使用者可在Platform UI中檢視的對應，但當設定與您目的地的連線時，無法修改這些對應。

例如，您可以強制執行電子郵件地址欄位，以一律傳送至目的地。

>[!NOTE]
>
>目前支援下列必要對應的組合：
>* 您可以設定必要的來源欄位和必要的目的地欄位。 在這種情況下，用戶無法編輯或選擇這兩個欄位中的任何一個，並且只能查看選擇。
>* 您只能設定必要的目的地欄位。 在這種情況下，將允許用戶選擇源欄位以映射到目標。
>
> 當前僅配置必需源欄位 *not* 支援。

請參閱以下兩個具有必要對應的架構設定範例，以及這些範例在的對應步驟中的外觀 [將資料啟用至批次目的地工作流程](../../../ui/activate-batch-profile-destinations.md).


>[!BEGINTABS]

>[!TAB 所需的源和目標映射]

下列範例顯示所需的來源和目的地對應。 將源欄位和目標欄位指定為必需映射時，用戶無法選擇或編輯這兩個欄位中的任何一個，並且只能查看預定義的選擇。

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
| `requiredMappingsOnly` | 布林值 | 選填 | 若此值設為true，除了您在 `requiredMappings` 陣列。 |
| `requiredMappings.sourceType` | 字串 | 必填 | 指出 `source` 欄位。 支援的值： <ul><li>`text/x.schema-path`:若 `source` 欄位是XDM結構的設定檔屬性。</li><li>`text/x.aep-xl`:若您的 `source` 欄位由規則運算式定義。 範例：`iif(segmentMembership.ups.aep_seg_id.status==\"exited\", \"1\", \"0\")`</li><li>`text/plain`:若您的 `source` 欄位由巨集範本定義。 目前，唯一支援的巨集範本是 `metadata.segment.alias`.</li></ul> |
| `requiredMappings.source` | 字串 | 必填 | 指示源欄位的值。 支援的值類型： <ul><li>XDM設定檔屬性。 範例: `personalEmail.address`. 如果來源屬性為XDM設定檔屬性，請設定 `sourceType` 參數 `text/x.schema-path`.</li><li>規則運算式. 範例: `iif(segmentMembership.ups.aep_seg_id.status==\"exited\", \"1\", \"0\")`. 如果來源屬性是規則運算式，請設定 `sourceType` 參數 `text/x.aep-xl`.</li><li>宏模板。 範例:`metadata.segment.alias`. 如果源屬性是宏模板，請設定 `sourceType` 參數 `text/plain`. 目前，唯一支援的巨集範本是 `metadata.segment.alias`.</li></ul> |
| `requiredMappings.destination` | 字串 | 必填 | 指示目標欄位的值。 將源欄位和目標欄位指定為必需映射時，用戶無法選擇或編輯這兩個欄位中的任何一個，並且只能查看選擇。 |

{style="table-layout:auto"}

因此， **[!UICONTROL 源欄位]** 和 **[!UICONTROL 目標欄位]** Platform UI中的區段會反灰。

![UI啟動流程中所需對應的影像。](../../assets/functionality/destination-configuration/required-mappings-2.png)

>[!TAB 必要的目標映射]

以下範例顯示所需的目的地對應。 如果僅將目標欄位指定為必要欄位，則用戶可以選擇要映射到哪個源欄位。

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
| `requiredMappingsOnly` | 布林值 | 選填 | 若此值設為true，除了您在 `requiredMappings` 陣列。 |
| `requiredMappings.destination` | 字串 | 必填 | 指示目標欄位的值。 僅指定目標欄位時，用戶可以選擇源欄位以映射到目標。 |
| `mandatoryRequired` | 布林值 | 選填 | 指出對應是否應標示為 [強制屬性](../../../ui/activate-batch-profile-destinations.md#mandatory-attributes). |
| `primaryKeyRequired` | 布林值 | 選填 | 指出對應是否應標示為 [去重複化金鑰](../../../ui/activate-batch-profile-destinations.md#deduplication-keys). |

{style="table-layout:auto"}

因此， **[!UICONTROL 目標欄位]** Platform UI中的區段會變灰，而 **[!UICONTROL 源欄位]** 區段處於作用中狀態，且使用者可與其互動。 此 **[!UICONTROL 必填金鑰]** 和 **[!UICONTROL 重複資料刪除密鑰]** 選項處於活動狀態，用戶無法更改它們。

![UI啟動流程中所需對應的影像。](../../assets/functionality/destination-configuration/required-mappings-1.png)

>[!ENDTABS]

## 後續步驟 {#next-steps}

閱讀本文後，您應該更清楚了解Destination SDK支援的架構類型，以及如何設定架構。

若要進一步了解其他目的地元件，請參閱下列文章：

* [客戶驗證](customer-authentication.md)
* [OAuth2驗證](oauth2-authentication.md)
* [UI屬性](ui-attributes.md)
* [客戶資料欄位](customer-data-fields.md)
* [身分命名空間設定](identity-namespace-configuration.md)
* [支援的對應配置](supported-mapping-configurations.md)
* [目的地傳送](destination-delivery.md)
* [對象中繼資料設定](audience-metadata-configuration.md)
* [聚合策略](aggregation-policy.md)
* [批次設定](batch-configuration.md)
* [歷史設定檔資格](historical-profile-qualifications.md)