---
description: 瞭解如何為使用Destination SDK建立的目的地設定支援的目標身分。
title: 身分名稱空間設定
exl-id: 30c0939f-b968-43db-b09b-ce5b34349c6e
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '925'
ht-degree: 3%

---

# 身分名稱空間設定

Experience Platform使用身分名稱空間來說明特定身分的型別。 例如，名為`Email`的身分名稱空間會將`name@email.com`之類的值識別為電子郵件地址。

根據您建立的目的地型別（串流或檔案型），請記住以下身分名稱空間要求：

* 透過Destination SDK建立即時（串流）目的地時，除了[設定使用者可將設定檔屬性和身分對應至的合作夥伴結構描述](schema-configuration.md)之外，您還必須定義目的地平台支援的&#x200B;*至少一個*&#x200B;身分名稱空間。 例如，如果您的目的地平台接受雜湊電子郵件和[!DNL IDFA]，您必須將這兩個身分定義為[，並在此檔案](#supported-parameters)中進一步說明。

  >[!IMPORTANT]
  >
  >將對象啟用至串流目的地時，除了目標設定檔屬性外，使用者還必須對應&#x200B;_至少一個目標身分_。 否則，不會將對象啟動至目的地平台。

* 透過Destination SDK建立以檔案為基礎的目的地時，身分識別名稱空間的設定是&#x200B;_選擇性_。

若要進一步瞭解Experience Platform中的身分識別名稱空間，請參閱[身分識別名稱空間檔案](../../../../identity-service/features/namespaces.md)。

設定目的地的身分識別名稱空間時，您可以微調目的地支援的目標身分對應，例如：

* 允許使用者將XDM屬性對應至身分識別名稱空間。
* 允許使用者將[標準身分名稱空間](../../../../identity-service/features/namespaces.md#standard)對應到您自己的身分名稱空間。
* 允許使用者將[自訂識別名稱空間](../../../../identity-service/features/namespaces.md#manage-namespaces)對應到您自己的識別名稱空間。

若要瞭解此元件在何處適合使用Destination SDK建立的整合，請參閱[設定選項](../configuration-options.md)檔案中的圖表，或參閱如何[使用Destination SDK設定檔案型目的地](../../guides/configure-file-based-destination-instructions.md#create-server-file-configuration)的指南。

您可以透過`/authoring/destinations`端點設定支援的身分識別名稱空間。 請參閱下列API參考頁面，以取得詳細的API呼叫範例，您可在此範例設定本頁面中顯示的元件。

* [建立目的地設定](../../authoring-api/destination-configuration/create-destination-configuration.md)
* [更新目的地設定](../../authoring-api/destination-configuration/update-destination-configuration.md)

本文會說明您可用於目的地的所有支援身分識別名稱空間設定選項，並顯示客戶在Experience Platform UI中會看到的內容。

>[!IMPORTANT]
>
>Destination SDK支援的所有引數名稱和值都會區分大小寫&#x200B;**&#x200B;**。 為避免區分大小寫錯誤，請完全依照檔案中所示使用引數名稱和值。

## 支援的整合型別 {#supported-integration-types}

如需瞭解哪些型別的整合支援本頁面所述功能的詳細資訊，請參閱下表。

| 整合型別 | 支援功能 |
|---|---|
| 即時（串流）整合 | 是（必要） |
| 檔案式（批次）整合 | 是（選擇性） |

## 支援的引數 {#supported-parameters}

定義目的地支援的目標身分時，您可以使用下表所述的引數來設定其行為。

| 參數 | 類型 | 必填/選填 | 說明 |
|---------|----------|---|------|
| `acceptsAttributes` | 布林值 | 選填 | 指出客戶是否可將標準設定檔屬性對應至您正在設定的身分。 |
| `acceptsCustomNamespaces` | 布林值 | 選填 | 指出客戶是否可將自訂身分名稱空間對應至您正在設定的身分名稱空間。 |
| `acceptedGlobalNamespaces` | - | 選填 | 指出客戶可以將哪些[標準身分名稱空間](../../../../identity-service/features/namespaces.md#standard) （例如[!UICONTROL IDFA]）對應到您正在設定的身分。 |
| `transformation` | 字串 | 選填 | 當來源欄位是XDM屬性或自訂身分名稱空間時，顯示Experience Platform UI中的[[!UICONTROL 套用轉換]](../../../ui/activate-segment-streaming-destinations.md#apply-transformation)核取方塊。 使用此選項可讓使用者在匯出時雜湊來源屬性。 若要啟用此選項，請將值設為`sha256(lower($))`。 |
| `requiredTransformation` | 字串 | 選填 | 當客戶選取此來源身分名稱空間時，[[!UICONTROL 套用轉換]](../../../ui/activate-segment-streaming-destinations.md#apply-transformation)核取方塊會自動套用至對應，且客戶無法停用它。 若要啟用此選項，請將值設為`sha256(lower($))`。 |

{style="table-layout:auto"}


```json
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
   }
```

您必須指出客戶可以將哪些[!DNL Experience Platform]身分匯出至您的目的地。 例如： [!DNL Experience Cloud ID]、雜湊電子郵件、裝置識別碼([!DNL IDFA]、[!DNL GAID])。 這些值是[!DNL Experience Platform]個身分識別名稱空間，客戶可以從您的目的地對應至身分識別名稱空間。

身分名稱空間不需要[!DNL Experience Platform]與您的目的地之間有一對一的對應關係。
例如，客戶可以從您的目的地將[!DNL Experience Platform] [!DNL IDFA]名稱空間對應至[!DNL IDFA]名稱空間，也可以將相同的[!DNL Experience Platform] [!DNL IDFA]名稱空間對應至您目的地的[!DNL Customer ID]名稱空間。

深入瞭解[身分名稱空間概觀](../../../../identity-service/features/namespaces.md)中的身分。

## 對應考量事項

如果客戶選取來源身分名稱空間但未選取目標對應，Experience Platform會自動以相同名稱的屬性填入目標對應。

## 設定選擇性來源欄位雜湊

Experience Platform客戶可選擇以雜湊格式或純文字將資料擷取至Experience Platform。 如果您的目的地平台接受雜湊和未雜湊的資料，您可以讓客戶自行選擇是否要讓Experience Platform在來源欄位值匯出至您的目的地時，將來源欄位值雜湊。

下列組態會在對應步驟中，啟用Experience Platform UI中的選用[套用轉換](../../../ui/activate-segment-streaming-destinations.md#apply-transformation)選項。

```json {line-numbers="true" highlight="5"}
"identityNamespaces":{
      "Customer_contact":{
         "acceptsAttributes":true,
         "acceptsCustomNamespaces":true,
         "transformation": "sha256(lower($))",
         "acceptedGlobalNamespaces":{
            "Email":{
            },
            "Phone":{
            }
         }
      }
   }
```

使用未雜湊的來源欄位時勾選此選項，讓 Adobe Experience Platform 在啟動時自動將它們雜湊。

將未雜湊的來源屬性對應到目的地預期雜湊的目標屬性時（例如： `email_lc_sha256`或`phone_sha256`），請核取&#x200B;**套用轉換**&#x200B;選項，讓Adobe Experience Platform在啟用時自動雜湊來源屬性。

## 設定強制來源欄位雜湊

如果您的目的地僅接受雜湊資料，您可以設定匯出的屬性，讓Experience Platform自動對其進行雜湊。 當對應`Email`和`Phone`身分時，下列組態會自動檢查&#x200B;**套用轉換**&#x200B;選項。

```json {line-numbers="true" highlight="8,11"}
"identityNamespaces":{
      "Customer_contact":{
         "acceptsAttributes":true,
         "acceptsCustomNamespaces":true,
         "transformation": "sha256(lower($))",
         "acceptedGlobalNamespaces":{
            "Email":{
               "requiredTransformation": "sha256(lower($))"
            },
            "Phone":{
               "requiredTransformation": "sha256(lower($))"
            }
         }
      }
   }
```

## 後續步驟 {#next-steps}

閱讀本文後，您應該更瞭解如何為使用Destination SDK建置的目的地設定您的身分識別名稱空間。

若要深入瞭解其他目的地元件，請參閱下列文章：

* [客戶驗證](customer-authentication.md)
* [OAuth2授權](oauth2-authorization.md)
* [客戶資料欄位](customer-data-fields.md)
* [UI屬性](ui-attributes.md)
* [結構描述設定](schema-configuration.md)
* [身分名稱空間設定](identity-namespace-configuration.md)
* [支援的對應設定](supported-mapping-configurations.md)
* [目的地傳遞](destination-delivery.md)
* [對象中繼資料設定](audience-metadata-configuration.md)
* [彙總原則](aggregation-policy.md)
* [批次設定](batch-configuration.md)
* [歷史設定檔資格](historical-profile-qualifications.md)
