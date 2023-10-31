---
description: 瞭解如何為使用Destination SDK建立的目的地設定支援的目標身分。
title: 身分名稱空間設定
exl-id: 30c0939f-b968-43db-b09b-ce5b34349c6e
source-git-commit: b4334b4f73428f94f5a7e5088f98e2459afcaf3c
workflow-type: tm+mt
source-wordcount: '841'
ht-degree: 4%

---

# 身分名稱空間設定

Experience Platform使用身分名稱空間來說明特定身分的型別。 例如，身分名稱空間稱為 `Email` 會識別類似這樣的值 `name@email.com` 作為電子郵件地址。

除了透過Destination SDK建立目的地之外， [設定合作夥伴結構描述](schema-configuration.md) 讓使用者可將設定檔屬性和身分對應至，您也可以定義目的地平台支援的身分名稱空間。

執行此操作時，除了目標設定檔屬性外，使用者還可以選擇目標身分。

若要進一步瞭解Experience Platform中的身分識別名稱空間，請參閱 [身分名稱空間檔案](../../../../identity-service/namespaces.md).

設定目的地的身分識別名稱空間時，您可以微調目的地支援的目標身分對應，例如：

* 允許使用者將XDM屬性對應至身分識別名稱空間。
* 允許使用者對應 [標準身分名稱空間](../../../../identity-service/namespaces.md#standard) 到您自己的身分識別名稱空間。
* 允許使用者對應 [自訂身分名稱空間](../../../../identity-service/namespaces.md#manage-namespaces) 到您自己的身分識別名稱空間。

若要瞭解此元件在何處適合使用Destination SDK建立的整合，請參閱 [設定選項](../configuration-options.md) 檔案或請參閱操作說明指南 [使用Destination SDK來設定以檔案為基礎的目的地](../../guides/configure-file-based-destination-instructions.md#create-server-file-configuration).

您可以透過以下方式設定支援的身分識別名稱空間： `/authoring/destinations` 端點。 請參閱下列API參考頁面，以取得詳細的API呼叫範例，您可在此範例設定本頁面中顯示的元件。

* [建立目的地設定](../../authoring-api/destination-configuration/create-destination-configuration.md)
* [更新目的地設定](../../authoring-api/destination-configuration/update-destination-configuration.md)

本文會說明您可用於目的地的所有支援身分識別名稱空間設定選項，並顯示客戶在Platform UI中會看到的內容。

>[!IMPORTANT]
>
>Destination SDK支援的所有引數名稱和值如下 **區分大小寫**. 為避免區分大小寫錯誤，請完全依照檔案中所示使用引數名稱和值。

## 支援的整合型別 {#supported-integration-types}

如需瞭解哪些型別的整合支援本頁面所述功能的詳細資訊，請參閱下表。

| 整合型別 | 支援功能 |
|---|---|
| 即時（串流）整合 | 是 |
| 檔案式（批次）整合 | 是 |

## 支援的引數 {#supported-parameters}

定義目的地支援的目標身分時，您可以使用下表所述的引數來設定其行為。

| 參數 | 類型 | 必填/選填 | 說明 |
|---------|----------|---|------|
| `acceptsAttributes` | 布林值 | 選填 | 指出客戶是否可將標準設定檔屬性對應至您正在設定的身分。 |
| `acceptsCustomNamespaces` | 布林值 | 選填 | 指出客戶是否可將自訂身分名稱空間對應至您正在設定的身分名稱空間。 |
| `acceptedGlobalNamespaces` | - | 選填 | 指示哪一個 [標準身分名稱空間](../../../../identity-service/namespaces.md#standard) (例如， [!UICONTROL IDFA])客戶可對應至您正在設定的身分。 |
| `transformation` | 字串 | 選填 | 顯示 [[!UICONTROL 套用轉換]](../../../ui/activate-segment-streaming-destinations.md#apply-transformation) 如果來源欄位是XDM屬性或自訂身分名稱空間，系統會勾選Platform UI中的核取方塊。 使用此選項可讓使用者在匯出時雜湊來源屬性。 若要啟用此選項，請將值設為 `sha256(lower($))`. |
| `requiredTransformation` | 字串 | 選填 | 當客戶選取此來源身分名稱空間時， [[!UICONTROL 套用轉換]](../../../ui/activate-segment-streaming-destinations.md#apply-transformation) 核取方塊會自動套用至對應，且客戶無法將其停用。 若要啟用此選項，請將值設為 `sha256(lower($))`. |

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

您必須指出哪個 [!DNL Platform] 身分客戶可以匯出至您的目的地。 部分範例為 [!DNL Experience Cloud ID]，雜湊電子郵件，裝置ID ([!DNL IDFA]， [!DNL GAID])。 這些值為 [!DNL Platform] 客戶可對應至目的地之身分識別名稱空間的身分識別名稱空間。

身分名稱空間不需要1對1的對應， [!DNL Platform] 以及您的目的地。
例如，客戶可將 [!DNL Platform] [!DNL IDFA] 名稱空間轉換為 [!DNL IDFA] 名稱空間，或可對應相同的名稱空間 [!DNL Platform] [!DNL IDFA] 名稱空間重新命名為 [!DNL Customer ID] 您目的地中的名稱空間。

深入瞭解中的身分 [身分名稱空間總覽](../../../../identity-service/namespaces.md).

## 對應考量事項

如果客戶選取來源身分名稱空間但未選取目標對應，Platform會自動以相同名稱的屬性填入目標對應。

## 設定選擇性來源欄位雜湊

Experience Platform客戶可以選擇以雜湊格式或純文字將資料擷取到Platform。 如果您的目的地平台接受雜湊和未雜湊資料，您可以讓客戶自行選擇是否要在來源欄位值匯出至目的地時，讓平台將來源欄位值雜湊。

下列設定可啟用選擇性 [套用轉換](../../../ui/activate-segment-streaming-destinations.md#apply-transformation) Platform UI中的選項，在對應步驟中。

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

將未雜湊的來源屬性對應到目的地預期會雜湊的目標屬性時(例如： `email_lc_sha256` 或 `phone_sha256`)，檢查 **套用轉換** 讓Adobe Experience Platform在啟動時自動雜湊來源屬性的選項。

## 設定強制來源欄位雜湊

如果您的目的地僅接受雜湊資料，您可以設定匯出的屬性由Platform自動雜湊。 以下設定會自動檢查 **套用轉換** 選項，當 `Email` 和 `Phone` 身分已對應。

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

閱讀本文後，您應該更瞭解如何為使用Destination SDK建立的目的地設定您的身分識別名稱空間。

若要深入瞭解其他目的地元件，請參閱下列文章：

* [客戶驗證](customer-authentication.md)
* [OAuth2驗證](oauth2-authentication.md)
* [客戶資料欄位](customer-data-fields.md)
* [UI屬性](ui-attributes.md)
* [綱要設定](schema-configuration.md)
* [身分名稱空間設定](identity-namespace-configuration.md)
* [支援的對應設定](supported-mapping-configurations.md)
* [目的地傳遞](destination-delivery.md)
* [對象中繼資料設定](audience-metadata-configuration.md)
* [彙總原則](aggregation-policy.md)
* [批次設定](batch-configuration.md)
* [歷史設定檔資格](historical-profile-qualifications.md)
