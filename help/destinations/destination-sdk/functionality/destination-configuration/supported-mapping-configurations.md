---
description: 了解如何針對支援的身分和屬性對應設定來設定您的目的地。
title: 支援的對應配置
source-git-commit: 118ff85a9fceb8ee81dbafe2c381d365b813da29
workflow-type: tm+mt
source-wordcount: '659'
ht-degree: 0%

---


# 支援的對應配置

以Destination SDK建置的目的地可支援根據目的地類型的特定身分命名空間和屬性對應設定。

本文說明在設定目的地時，可使用的所有支援對應設定。

>[!WARNING]
>
>Destination SDK不支援本文未說明的任何對應設定。

建置目的地時，請根據本頁面所述的其中一個對應設定，設定您的架構和身分識別命名空間。

>[!IMPORTANT]
>
>Destination SDK支援的所有參數名稱和值均為 **區分大小寫**. 為避免區分大小寫錯誤，請使用參數名稱和值，如說明檔案所示。

## 串流目的地的支援對應 {#streaming-mappings}

以Destination SDK建置的即時（串流）目的地支援下表所述的對應設定。

| 來源欄位 | 目標欄位 |
| --- | --- |
| XDM屬性 | 自訂屬性 |
| 身分命名空間 | 身分命名空間 |

下列設定範例可讓客戶使用上表中的兩個對應。

```json
"schemaConfig":{
   "profileRequired":true,
   "segmentRequired":true,
   "identityRequired":true
},
"identityNamespaces":{
   "Customer_contact":{
      "acceptsAttributes":false,
      "acceptsCustomNamespaces":true,
      "acceptedGlobalNamespaces":{
         "Email":{
            
         },
         "Phone":{
            
         }
      }
   }
},
```

### 將XDM屬性對應至自訂屬性 {#streaming-xdm-to-custom}

使用者可將來源XDM設定檔的屬性對應至目的地端的自訂屬性。

選取目標欄位對應時，使用者必須手動輸入目標自訂屬性的名稱。

![Platform UI螢幕擷取畫面，顯示自訂屬性選取項目。](../../assets/functionality/destination-configuration/mapping-streaming-select-custom-attribute.png)

產生的UI體驗會顯示在下圖中。

![Platform UI螢幕擷取畫面，顯示串流目的地的XDM屬性對應至自訂屬性。](../../assets/functionality/destination-configuration/mapping-streaming-xdm-custom.png)

### 將身分識別命名空間對應至合作夥伴身分識別命名空間 {#streaming-identity-to-identity}

使用者可將自訂或全域身分識別命名空間從Platform對應至您定義的身分識別命名空間。

產生的UI體驗會顯示在下圖中。

![Platform UI螢幕擷圖，顯示串流目的地的身分對應至身分識別。](../../assets/functionality/destination-configuration/mapping-streaming-identity-identity.png)

## 檔案型目的地的支援對應 {#batch-mappings}

以Destination SDK建置的檔案式目的地支援下表所述的對應設定。 如需詳細的對應範例，請參閱下一節。

| 來源欄位 | 目標欄位 |
| --- | --- |
| XDM屬性 | 屬性/自訂屬性 |
| 身分命名空間 | 屬性/自訂屬性 |
| 身分命名空間 | 身分命名空間 |

以下的設定範例可讓客戶使用上表中的所有對應。

```json
"schemaConfig":{
   "profileRequired":true,
   "segmentRequired":true,
   "identityRequired":true
},
"identityNamespaces":{
   "Customer_contact":{
      "acceptsAttributes":false,
      "acceptsCustomNamespaces":true,
      "acceptedGlobalNamespaces":{
         "Email":{
         },
         "Phone":{
         }
      }
   }
},
```

### 將XDM屬性對應至自訂屬性 {#batch-xdm-to-custom}

使用者可將來源XDM設定檔的屬性對應至目的地端的自訂屬性。

針對檔案型目的地，目標欄位會自動填入與來源欄位同名的預設屬性。

產生的UI體驗會顯示在下圖中。

![Platform UI的螢幕擷圖，顯示檔案式目的地的XDM對應至自訂屬性。](../../assets/functionality/destination-configuration/mapping-batch-xdm-custom.png)

使用者可保留預設名稱，或在目標欄位選取畫面中輸入自訂屬性名稱。

![Platform UI螢幕擷取畫面，顯示以檔案為基礎的目的地的自訂目標屬性選取項目。](../../assets/functionality/destination-configuration/mapping-batch-custom-attribute.png)

### 將身分識別命名空間對應至自訂屬性 {#batch-identity-to-custom}

使用者可將自訂或全域身分識別命名空間從Platform對應至您目的地端的自訂屬性。

選取身分命名空間作為來源欄位時，目標欄位會自動填入相等的身分命名空間。 若要以自訂屬性取代目標欄位，使用者必須在目標欄位選取畫面中輸入自訂屬性名稱。

![Platform UI螢幕擷取畫面，顯示以檔案為基礎的目的地的自訂目標屬性選取項目。](../../assets/functionality/destination-configuration/mapping-batch-custom-attribute.png)

產生的UI體驗會顯示在下圖中。

![Platform UI螢幕擷取畫面，顯示檔案式目的地的身分對應至自訂屬性。](../../assets/functionality/destination-configuration/mapping-batch-identity-custom.png)

### 將身分識別命名空間對應至合作夥伴身分識別命名空間 {#batch-identity-to-identity}

使用者可將自訂或全域身分識別命名空間從Platform對應至等效身分識別命名空間。

選取身分命名空間作為來源欄位時，目標欄位會自動填入相等的身分命名空間。

產生的UI體驗會顯示在下圖中。

![Platform UI螢幕擷取畫面，顯示以檔案為基礎之目的地的身分對應至身分識別。](../../assets/functionality/destination-configuration/mapping-batch-identity-identity.png)


## 後續步驟 {#next-steps}

閱讀本文後，您應該更清楚了解使用Destination SDK建置的目的地支援哪些對應。

若要進一步了解其他目的地元件，請參閱下列文章：

* [客戶驗證](customer-authentication.md)
* [OAuth2驗證](oauth2-authentication.md)
* [客戶資料欄位](customer-data-fields.md)
* [UI屬性](ui-attributes.md)
* [結構配置](schema-configuration.md)
* [身分命名空間設定](identity-namespace-configuration.md)
* [目的地傳送](destination-delivery.md)
* [對象中繼資料設定](audience-metadata-configuration.md)
* [聚合策略](aggregation-policy.md)
* [批次設定](batch-configuration.md)
* [歷史設定檔資格](historical-profile-qualifications.md)