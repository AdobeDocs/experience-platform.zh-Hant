---
description: 瞭解如何為支援的標識和屬性映射配置配置目標。
title: 支援的映射配置
source-git-commit: 118ff85a9fceb8ee81dbafe2c381d365b813da29
workflow-type: tm+mt
source-wordcount: '659'
ht-degree: 0%

---


# 支援的映射配置

使用Destination SDK構建的目標支援基於目標類型的特定標識命名空間和屬性映射配置。

本文介紹配置目標時可以使用的所有受支援的映射配置。

>[!WARNING]
>
>Destination SDK不支援本文中未描述的任何映射配置。

在構建目標時，請根據本頁中描述的映射配置之一配置架構和標識命名空間。

>[!IMPORTANT]
>
>Destination SDK支援的所有參數名和值均 **區分大小寫**。 為避免區分大小寫錯誤，請完全按文檔所示使用參數名稱和值。

## 流目標支援的映射 {#streaming-mappings}

通過Destination SDK構建的即時（流）目標支援下表中所述的映射配置。

| 來源欄位 | 目標欄位 |
| --- | --- |
| XDM屬性 | 自定義屬性 |
| 標識命名空間 | 標識命名空間 |

下面的配置示例允許客戶在上表中使用這兩個映射。

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

### 將XDM屬性映射到自定義屬性 {#streaming-xdm-to-custom}

用戶可以將其源XDM配置檔案的屬性映射到目標端的自定義屬性。

用戶在選擇目標欄位映射時必須手動輸入目標自定義屬性的名稱。

![顯示自定義屬性選擇的平台UI螢幕快照。](../../assets/functionality/destination-configuration/mapping-streaming-select-custom-attribute.png)

生成的UI體驗顯示在下圖中。

![平台UI螢幕快照，顯示XDM屬性映射到流目標的自定義屬性。](../../assets/functionality/destination-configuration/mapping-streaming-xdm-custom.png)

### 將標識命名空間映射到夥伴標識命名空間 {#streaming-identity-to-identity}

用戶可以將自定義或全局標識命名空間從平台映射到您定義的標識命名空間。

生成的UI體驗顯示在下圖中。

![平台UI螢幕快照，顯示流目標的標識映射到標識。](../../assets/functionality/destination-configuration/mapping-streaming-identity-identity.png)

## 基於檔案的目標支援的映射 {#batch-mappings}

使用Destination SDK構建的基於檔案的目標支援下表中所述的映射配置。 有關詳細的映射示例，請參見下一節。

| 來源欄位 | 目標欄位 |
| --- | --- |
| XDM屬性 | 屬性/自定義屬性 |
| 標識命名空間 | 屬性/自定義屬性 |
| 標識命名空間 | 標識命名空間 |

下面的配置示例允許客戶使用上表中的所有映射。

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

### 將XDM屬性映射到自定義屬性 {#batch-xdm-to-custom}

用戶可以將其源XDM配置檔案的屬性映射到目標端的自定義屬性。

對於基於檔案的目標，目標欄位將自動填充與源欄位同名的預設屬性。

生成的UI體驗顯示在下圖中。

![平台UI螢幕快照，顯示XDM映射到基於檔案的目標的自定義屬性。](../../assets/functionality/destination-configuration/mapping-batch-xdm-custom.png)

用戶可以保留預設名稱，或在目標欄位選擇螢幕中輸入自定義屬性名稱。

![平台UI螢幕快照，顯示基於檔案的目標的自定義目標屬性選擇。](../../assets/functionality/destination-configuration/mapping-batch-custom-attribute.png)

### 將標識命名空間映射到自定義屬性 {#batch-identity-to-custom}

用戶可以將自定義或全局標識命名空間從平台映射到目標端的自定義屬性。

當選擇標識命名空間作為源欄位時，目標欄位將自動填充等效的標識命名空間。 要將目標欄位替換為自定義屬性，用戶必須在目標欄位選擇螢幕中輸入自定義屬性名稱。

![平台UI螢幕快照，顯示基於檔案的目標的自定義目標屬性選擇。](../../assets/functionality/destination-configuration/mapping-batch-custom-attribute.png)

生成的UI體驗顯示在下圖中。

![平台UI螢幕快照，顯示基於檔案的目標的自定義屬性的標識映射。](../../assets/functionality/destination-configuration/mapping-batch-identity-custom.png)

### 將標識命名空間映射到夥伴標識命名空間 {#batch-identity-to-identity}

用戶可以將自定義或全局標識命名空間從平台映射到等效的標識命名空間。

當選擇標識命名空間作為源欄位時，目標欄位將自動填充等效的標識命名空間。

生成的UI體驗顯示在下圖中。

![平台UI螢幕快照，顯示基於檔案的目標的標識到標識的映射。](../../assets/functionality/destination-configuration/mapping-batch-identity-identity.png)


## 後續步驟 {#next-steps}

閱讀本文後，您應該更好地瞭解使用Destination SDK構建的目標支援哪些映射。

要瞭解有關其他目標元件的詳細資訊，請參閱以下文章：

* [客戶驗證](customer-authentication.md)
* [OAuth2身份驗證](oauth2-authentication.md)
* [客戶資料欄位](customer-data-fields.md)
* [UI屬性](ui-attributes.md)
* [架構配置](schema-configuration.md)
* [標識命名空間配置](identity-namespace-configuration.md)
* [目標傳遞](destination-delivery.md)
* [受眾元資料配置](audience-metadata-configuration.md)
* [聚合策略](aggregation-policy.md)
* [批配置](batch-configuration.md)
* [歷史配置檔案資格](historical-profile-qualifications.md)