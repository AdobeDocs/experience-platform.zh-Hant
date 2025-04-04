---
description: 瞭解如何為使用Destination SDK建立的目的地設定合作夥伴結構。
title: 合作夥伴結構描述設定
exl-id: 0548e486-206b-45c5-8d18-0d6427c177c5
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1949'
ht-degree: 3%

---

# 合作夥伴結構描述設定

Experience Platform使用結構描述，以一致且可重複使用的方式說明資料結構。 將資料擷取至Experience Platform時，會根據XDM結構描述進行架構。 如需結構描述組合模型的詳細資訊，包括設計原則和最佳實務，請參閱結構描述組合的[基本概念](../../../../xdm/schema/composition.md)。

使用Destination SDK建立目的地時，您可以定義自己的合作夥伴結構描述，以由目的地平台使用。 這可讓使用者將設定檔屬性從Experience Platform對應至目的地平台可辨識的特定欄位，而且全都在Experience Platform UI中。

為您的目的地設定合作夥伴結構描述時，您可以微調目的地平台支援的欄位對應，例如：

* 允許使用者將`phoneNumber` XDM屬性對應到目的地平台支援的`phone`屬性。
* 建立Experience Platform可動態呼叫的動態合作夥伴結構描述，以擷取目的地內所有支援屬性的清單。
* 定義目的地平台所需的必要欄位對應。

若要瞭解此元件在何處適合使用Destination SDK建立的整合，請參閱[設定選項](../configuration-options.md)檔案中的圖表，或參閱如何[使用Destination SDK設定檔案型目的地](../../guides/configure-file-based-destination-instructions.md#create-server-file-configuration)的指南。

您可以透過`/authoring/destinations`端點設定您的結構描述設定。 請參閱下列API參考頁面，以取得詳細的API呼叫範例，您可在此範例設定本頁面中顯示的元件。

* [建立目的地設定](../../authoring-api/destination-configuration/create-destination-configuration.md)
* [更新目的地設定](../../authoring-api/destination-configuration/update-destination-configuration.md)

本文說明可用於目的地的所有支援結構描述設定選項，並顯示客戶在Experience Platform UI中會看到的內容。

>[!IMPORTANT]
>
>Destination SDK支援的所有引數名稱和值都會區分大小寫&#x200B;****。 為避免區分大小寫錯誤，請完全依照檔案中所示使用引數名稱和值。

## 支援的整合型別 {#supported-integration-types}

如需瞭解哪些型別的整合支援本頁面所述功能的詳細資訊，請參閱下表。

| 整合型別 | 支援功能 |
|---|---|
| 即時（串流）整合 | 是 |
| 檔案式（批次）整合 | 是 |

## 支援的結構描述設定 {#supported-schema-types}

Destination SDK支援多個結構描述設定：

* 靜態結構描述是透過`schemaConfig`區段中的`profileFields`陣列來定義。 在靜態結構描述中，您定義應顯示在`profileFields`陣列中Experience Platform UI的每個目標屬性。 如果您需要更新結構描述，您必須[更新目的地組態](../../authoring-api/destination-configuration/update-destination-configuration.md)。
* 動態結構描述會使用稱為[動態結構描述伺服器](../../authoring-api/destination-server/create-destination-server.md#dynamic-schema-servers)的其他目的地伺服器型別，以動態擷取支援的目標屬性，並根據您自己的API產生結構描述。 動態結構描述不使用`profileFields`陣列。 如果您需要更新結構描述，則無需[更新目的地組態](../../authoring-api/destination-configuration/update-destination-configuration.md)。 而是由動態結構描述伺服器從您的API擷取更新的結構描述。
* 在架構設定中，您可以選擇新增必要（或預先定義）的對應。 使用者可以在Experience Platform UI中檢視這些對應，但在設定與目的地的連線時無法修改這些對應。 例如，您可以強制電子郵件位址列位一律傳送到目的地。

`schemaConfig`區段會根據您所需的結構描述型別，使用多個設定引數，如下節所示。

## 建立靜態結構描述 {#attributes-schema}

若要使用設定檔屬性建立靜態結構描述，請在`profileFields`陣列中定義目標屬性，如下所示。

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
      "identityRequired":true,
      "segmentNamespaceAllowList": ["someNamespace"],
      "segmentNamespaceDenyList": ["someOtherNamespace"]

}
```

| 參數 | 類型 | 必要/選用 | 說明 |
|---------|----------|------|---|
| `profileFields` | 陣列 | 選填 | 定義目的地平台接受的目標屬性陣列，客戶可將其設定檔屬性對應至該陣列。 使用`profileFields`陣列時，您可以完全省略`useCustomerSchemaForAttributeMapping`引數。 |
| `useCustomerSchemaForAttributeMapping` | 布林值 | 選填 | 啟用或停用客戶結構描述中的屬性對應到您在`profileFields`陣列中定義的屬性。 <ul><li>如果設為`true`，使用者只會在對應欄位中看到來源欄。 `profileFields`不適用於此情況。</li><li>如果設為`false`，使用者可以從其結構描述將來源屬性對應到您在`profileFields`陣列中定義的屬性。</li></ul> 預設值為 `false`。 |
| `profileRequired` | 布林值 | 選填 | 如果使用者應該能夠從Experience Platform將設定檔屬性對應到您目的地平台上的自訂屬性，請使用`true`。 |
| `segmentRequired` | 布林值 | 必要 | Destination SDK需要此引數，且應一律設為`true`。 |
| `identityRequired` | 布林值 | 必要 | 若使用者應能將Experience Platform中的[身分型別](identity-namespace-configuration.md)對應到您在`profileFields`陣列中定義的屬性，則設為`true`。 |
| `segmentNamespaceAllowList` | 陣列 | 選填 | 定義使用者可將受眾對應至目的地的特定受眾名稱空間。 使用此引數可限制Experience Platform使用者僅從您在陣列中定義的對象名稱空間匯出對象。 此引數不能與`segmentNamespaceDenyList`.<br>一起使用 <br>範例： `"segmentNamespaceAllowList": ["AudienceManager"]`將允許使用者僅將對象從`AudienceManager`名稱空間對應至此目的地。<br> <br>若要允許使用者將任何對象匯出至您的目的地，您可以忽略此引數。<br> <br>如果您的設定中同時缺少`segmentNamespaceAllowList`和`segmentNamespaceDenyList`，使用者將只能匯出源自[分段服務](../../../../segmentation/home.md)的對象。 |
| `segmentNamespaceDenyList` | 陣列 | 選填 | 從陣列中定義的對象名稱空間，限制將對象對應到目的地的使用者。 無法與`segmentNamespaceAllowed`一起使用。<br> <br>範例： `"segmentNamespaceDenyList": ["AudienceManager"]`將封鎖使用者從`AudienceManager`名稱空間對應對象到此目的地。<br> <br>若要允許使用者將任何對象匯出至您的目的地，您可以忽略此引數。<br> <br>如果您的設定中同時缺少`segmentNamespaceAllowed`和`segmentNamespaceDenyList`，使用者將只能匯出源自[分段服務](../../../../segmentation/home.md)的對象。<br> <br>若要允許匯出所有對象，無論來源為何，請設定`"segmentNamespaceDenyList":[]`。 |

{style="table-layout:auto"}

產生的UI體驗會顯示在下圖中。

當使用者選取目標對應時，他們可以看到`profileFields`陣列中定義的欄位。

![顯示目標屬性畫面的UI影像。](../../assets/functionality/destination-configuration/select-attributes.png)

選取屬性後，他們便可在目標欄位欄中看到這些屬性。

![UI影像顯示具有屬性的靜態目標結構描述](../../assets/functionality/destination-configuration/static-schema-attributes.png)

## 建立動態結構描述 {#dynamic-schema-configuration}

Destination SDK支援建立動態合作夥伴方案。 相對於靜態結構描述，動態結構描述不會使用`profileFields`陣列。 動態方案會改用動態方案伺服器，此伺服器會連線至您自己的API，從其中擷取方案設定。

>[!IMPORTANT]
>
>建立動態結構描述之前，您必須[建立動態結構描述伺服器](../../authoring-api/destination-server/create-destination-server.md#dynamic-schema-servers)。

在動態結構描述設定中，`profileFields`陣列會由`dynamicSchemaConfig`區段取代，如下所示。

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

| 參數 | 類型 | 必要/選用 | 說明 |
|---------|----------|------|---|
| `dynamicEnum.authenticationRule` | 字串 | 必要 | 指示[!DNL Experience Platform]客戶如何連線至您的目的地。 接受的值為`CUSTOMER_AUTHENTICATION`、`PLATFORM_AUTHENTICATION`、`NONE`。<br> <ul><li>如果Experience Platform客戶透過[此處](customer-authentication.md)說明的任何驗證方法登入您的系統，請使用`CUSTOMER_AUTHENTICATION`。 </li><li> 如果Adobe與您的目的地之間有全域驗證系統，且[!DNL Experience Platform]客戶不需要提供任何驗證認證即可連線至您的目的地，請使用`PLATFORM_AUTHENTICATION`。 在此情況下，您必須使用認證API [建立認證物件](../../credentials-api/create-credential-configuration.md)。 </li><li>如果不需要驗證即可將資料傳送至您的目的地平台，請使用`NONE`。 </li></ul> |
| `dynamicEnum.destinationServerId` | 字串 | 必要 | 動態結構描述伺服器的`instanceId`。 此目的地伺服器包含Experience Platform將呼叫以擷取動態結構描述的API端點。 |
| `dynamicEnum.value` | 字串 | 必要 | 動態架構的名稱，如動態架構伺服器設定中所定義。 |
| `dynamicEnum.responseFormat` | 字串 | 必要 | 定義動態結構描述時一律設為`SCHEMA`。 |
| `profileRequired` | 布林值 | 選填 | 如果使用者應該能夠從Experience Platform將設定檔屬性對應到您目的地平台上的自訂屬性，請使用`true`。 |
| `segmentRequired` | 布林值 | 必要 | Destination SDK需要此引數，且應一律設為`true`。 |
| `identityRequired` | 布林值 | 必要 | 若使用者應能將Experience Platform中的[身分型別](identity-namespace-configuration.md)對應到您在`profileFields`陣列中定義的屬性，則設為`true`。 |

{style="table-layout:auto"}

## 必要的對應 {#required-mappings}

在結構描述設定中，除了您的靜態或動態結構描述外，您還可以選擇新增必要（或預先定義）的對應。 使用者可以在Experience Platform UI中檢視這些對應，但在設定與目的地的連線時無法修改這些對應。

例如，您可以強制電子郵件位址列位一律傳送到目的地。

>[!NOTE]
>
>目前支援下列必要對應的組合：
>* 您可以設定必要來源欄位和必要目的地欄位。 在此情況下，使用者無法編輯或選取兩個欄位中的任何一個，並且只能檢視選取專案。
>* 您只能設定必要的目的地欄位。 在此情況下，使用者可選取來源欄位，以對應至目的地。
>
> 僅設定必要的來源欄位目前是&#x200B;*不支援*。

請參閱以下兩個結構描述設定範例，其中包含必要的對應，以及[啟動資料至批次目的地工作流程](../../../ui/activate-batch-profile-destinations.md)的對應步驟中這些設定的外觀。


>[!BEGINTABS]

>[!TAB 必要的來源和目的地對應]

以下範例顯示必要的來源和目的地對應。 當來源欄位和目的地欄位都指定為必要對應時，使用者無法選取或編輯這兩個欄位中的任何一個，且只能檢視預先定義的選取專案。

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

| 參數 | 類型 | 必要/選用 | 說明 |
|---|---|---|---|
| `requiredMappingsOnly` | 布林值 | 選填 | 當此設定為true時，除了您在`requiredMappings`陣列中定義的必要對應之外，使用者無法對應啟動流程中的其他屬性和身分。 |
| `requiredMappings.sourceType` | 字串 | 必要 | 指示`source`欄位的型別。 支援的值： <ul><li>`text/x.schema-path`：當`source`欄位是XDM結構描述的設定檔屬性時，請使用此值。</li><li>`text/x.aep-xl`：當您的`source`欄位是由規則運算式定義時，請使用此值。 範例：`iif(segmentMembership.ups.aep_seg_id.status==\"exited\", \"1\", \"0\")`</li><li>`text/plain`：當您的`source`欄位是由巨集範本定義時，請使用此值。 目前唯一支援的巨集範本是`metadata.segment.alias`。</li></ul> |
| `requiredMappings.source` | 字串 | 必要 | 表示來源欄位的值。 支援的值型別： <ul><li>xdm設定檔屬性。 範例： `personalEmail.address`。 當您的來源屬性是XDM設定檔屬性時，請將`sourceType`引數設定為`text/x.schema-path`。</li><li>規則運算式。 範例： `iif(segmentMembership.ups.aep_seg_id.status==\"exited\", \"1\", \"0\")`。 當您的來源屬性是規則運算式時，請將`sourceType`引數設定為`text/x.aep-xl`。</li><li>巨集範本。 範例： `metadata.segment.alias`。 當您的來源屬性是巨集範本時，請將`sourceType`引數設定為`text/plain`。 目前唯一支援的巨集範本是`metadata.segment.alias`。</li></ul> |
| `requiredMappings.destination` | 字串 | 必要 | 表示目標欄位的值。 當來源欄位和目的地欄位都指定為必要對應時，使用者無法選取或編輯這兩個欄位中的任何一個，且只能檢視選取專案。 |

{style="table-layout:auto"}

因此，Experience Platform UI中的&#x200B;**[!UICONTROL Source欄位]**&#x200B;和&#x200B;**[!UICONTROL 目標欄位]**&#x200B;區段都會呈現灰色。

![ UI啟用流程中所需對應的影像。](../../assets/functionality/destination-configuration/required-mappings-2.png)

>[!TAB 必要的目的地對應]

以下範例顯示必要的目的地對應。 如果僅將目的地欄位指定為必要欄位，則使用者可以選擇要與其對應的來源欄位。

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

| 參數 | 類型 | 必要/選用 | 說明 |
|---|---|---|---|
| `requiredMappingsOnly` | 布林值 | 選填 | 當此設定為true時，除了您在`requiredMappings`陣列中定義的必要對應之外，使用者無法對應啟動流程中的其他屬性和身分。 |
| `requiredMappings.destination` | 字串 | 必要 | 表示目標欄位的值。 當僅指定目的地欄位時，使用者可以選取來源欄位以對應至目的地。 |
| `mandatoryRequired` | 布林值 | 選填 | 指示對應是否應標示為[必要屬性](../../../ui/activate-batch-profile-destinations.md#mandatory-attributes)。 |
| `primaryKeyRequired` | 布林值 | 選填 | 指示對應是否應標示為[重複資料刪除索引鍵](../../../ui/activate-batch-profile-destinations.md#deduplication-keys)。 |

{style="table-layout:auto"}

因此，Experience Platform UI中的&#x200B;**[!UICONTROL Target欄位]**&#x200B;區段會呈現灰色，而&#x200B;**[!UICONTROL Source欄位]**&#x200B;區段則會作用中，使用者可以與其互動。 **[!UICONTROL 必要索引鍵]**&#x200B;和&#x200B;**[!UICONTROL 重複資料刪除索引鍵]**&#x200B;選項作用中，使用者無法變更它們。

![ UI啟用流程中所需對應的影像。](../../assets/functionality/destination-configuration/required-mappings-1.png)

>[!ENDTABS]

## 設定對外部對象的支援 {#external-audiences}

若要設定您的目的地以支援[外部產生的對象](../../../../segmentation/ui/audience-portal.md#import-audience)的啟用，請在`schemaConfig`區段中加入以下程式碼片段。

```json
"schemaConfig": {
  "segmentNamespaceDenyList": [],
  ...
}
```

請參閱本頁上方的[表格](#attributes-schema)中的屬性說明，以進一步瞭解`segmentNamespaceDenyList`功能。

## 後續步驟 {#next-steps}

閱讀本文後，您應該更加瞭解Destination SDK支援的結構型別，以及如何設定您的結構描述。

若要深入瞭解其他目的地元件，請參閱下列文章：

* [客戶驗證](customer-authentication.md)
* [OAuth2授權](oauth2-authorization.md)
* [UI屬性](ui-attributes.md)
* [客戶資料欄位](customer-data-fields.md)
* [身分名稱空間設定](identity-namespace-configuration.md)
* [支援的對應設定](supported-mapping-configurations.md)
* [目的地傳遞](destination-delivery.md)
* [對象中繼資料設定](audience-metadata-configuration.md)
* [彙總原則](aggregation-policy.md)
* [批次設定](batch-configuration.md)
* [歷史設定檔資格](historical-profile-qualifications.md)
