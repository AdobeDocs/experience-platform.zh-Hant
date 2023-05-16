---
description: 了解如何針對以Destination SDK建置的目的地，設定支援的目標身分識別。
title: 身分命名空間設定
source-git-commit: 118ff85a9fceb8ee81dbafe2c381d365b813da29
workflow-type: tm+mt
source-wordcount: '842'
ht-degree: 4%

---


# 身分命名空間設定

Experience Platform使用身分識別命名空間來說明特定身分類型。 例如，身分命名空間稱為 `Email` 識別值類似 `name@email.com` 作為電子郵件地址。

透過Destination SDK建立目的地時，除 [配置合作夥伴架構](schema-configuration.md) 使用者可將設定檔屬性和身分對應至，您也可以定義目的地平台支援的身分識別命名空間。

執行此操作時，除了目標設定檔屬性外，使用者還可以選擇選取目標身分。

若要進一步了解Experience Platform中的身分識別命名空間，請參閱 [身分命名空間檔案](../../../../identity-service/namespaces.md).

為目的地設定身分識別命名空間時，您可以微調目的地支援的目標身分對應，例如：

* 可讓使用者將XDM屬性對應至身分識別命名空間。
* 允許用戶映射 [標準身分命名空間](../../../../identity-service/namespaces.md#standard) 至您自己的身分識別命名空間。
* 允許用戶映射 [自訂身分命名空間](../../../../identity-service/namespaces.md#manage-namespaces) 至您自己的身分識別命名空間。

若要了解此元件在透過Destination SDK建立的整合中的插入位置，請參閱 [配置選項](../configuration-options.md) 檔案，或參閱如何 [使用Destination SDK配置基於檔案的目標](../../guides/configure-file-based-destination-instructions.md#create-server-file-configuration).

您可以透過 `/authoring/destinations` 端點。 如需詳細API呼叫範例，請參閱下列API參考頁面，您可在其中設定本頁面所示的元件。

* [建立目標配置](../../authoring-api/destination-configuration/create-destination-configuration.md)
* [更新目標配置](../../authoring-api/destination-configuration/update-destination-configuration.md)

本文說明您可用於目的地的所有支援身分識別命名空間設定選項，並說明客戶在Platform UI中會看到什麼內容。

>[!IMPORTANT]
>
>Destination SDK支援的所有參數名稱和值均為 **區分大小寫**. 為避免區分大小寫錯誤，請使用參數名稱和值，如說明檔案所示。

## 支援的整合類型 {#supported-integration-types}

如需詳細資訊，請參閱下表以了解哪些類型的整合支援本頁面所述的功能。

| 整合類型 | 支援功能 |
|---|---|
| 即時（串流）整合 | 是 |
| 檔案式（批次）整合 | 是 |

## 支援的參數 {#supported-parameters}

定義目的地支援的目標身分識別時，您可以使用下表中所述的參數來設定其行為。

| 參數 | 類型 | 必填/選填 | 說明 |
|---------|----------|---|------|
| `acceptsAttributes` | 布林值 | 選填 | 指出客戶是否可將標準設定檔屬性對應至您正在設定的身分。 |
| `acceptsCustomNamespaces` | 布林值 | 選填 | 指出客戶是否可將自訂身分識別命名空間對應至您所設定的身分識別命名空間。 |
| `acceptedGlobalNamespaces` | - | 選填 | 指出 [標準身分命名空間](../../../../identity-service/namespaces.md#standard) (例如， [!UICONTROL IDFA])客戶可對應至您正在設定的身分。 |
| `transformation` | 字串 | 選填 | 顯示 [[!UICONTROL 套用轉換]](../../../ui/activate-segment-streaming-destinations.md#apply-transformation) 當來源欄位為XDM屬性或自訂身分命名空間時，請在Platform UI中核取方塊。 使用此選項可讓使用者在匯出時雜湊來源屬性。 若要啟用此選項，請將值設為 `sha256(lower($))`. |
| `requiredTransformation` | 字串 | 選填 | 當客戶選取此來源身分命名空間時， [[!UICONTROL 套用轉換]](../../../ui/activate-segment-streaming-destinations.md#apply-transformation) 核取方塊會自動套用至對應，而客戶無法加以停用。 若要啟用此選項，請將值設為 `sha256(lower($))`. |

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

您必須指出 [!DNL Platform] 身分識別客戶可匯出至您的目的地。 例如 [!DNL Experience Cloud ID]，雜湊電子郵件，裝置ID([!DNL IDFA], [!DNL GAID])。 這些值包括 [!DNL Platform] 客戶可從您的目的地對應至身分識別命名空間的身分識別命名空間。

身分識別命名空間不需要 [!DNL Platform] 和你的目的地。
例如，客戶可以對應 [!DNL Platform] [!DNL IDFA] 命名空間 [!DNL IDFA] 來自您目的地的命名空間，或者可以對應相同的 [!DNL Platform] [!DNL IDFA] 命名空間 [!DNL Customer ID] 命名空間。

請前往 [身分命名空間概述](../../../../identity-service/namespaces.md).

## 對應考量事項

如果客戶選取來源身分命名空間而未選取目標對應，Platform會自動以相同名稱的屬性填入目標對應。

## 配置可選源欄位哈希

Experience Platform客戶可選擇以雜湊格式或純文字格式將資料內嵌至Platform。 如果您的目的地平台同時接受雜湊和未雜湊資料，您可讓客戶選擇在將來源欄位值匯出至您的目的地時，Platform是否應該雜湊來源欄位值。

以下設定會啟用選用 [套用轉換](../../../ui/activate-segment-streaming-destinations.md#apply-transformation) 選項（在「對應」步驟中）。

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

將非雜湊來源屬性對應至目標預期雜湊的目標屬性時(例如： `email_lc_sha256` 或 `phone_sha256`)，檢查 **套用轉換** 選項，讓Adobe Experience Platform在啟動時自動雜湊來源屬性。

## 配置強制源欄位哈希

如果您的目的地只接受雜湊資料，您可以將匯出的屬性設定為由Platform自動雜湊。 以下設定會自動檢查 **套用轉換** 選項 `Email` 和 `Phone` 身分會對應。

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

閱讀本文後，您應該更清楚了解如何針對使用Destination SDK建置的目的地設定身分識別命名空間。

若要進一步了解其他目的地元件，請參閱下列文章：

* [客戶驗證](customer-authentication.md)
* [OAuth2驗證](oauth2-authentication.md)
* [客戶資料欄位](customer-data-fields.md)
* [UI屬性](ui-attributes.md)
* [結構配置](schema-configuration.md)
* [身分命名空間設定](identity-namespace-configuration.md)
* [支援的對應配置](supported-mapping-configurations.md)
* [目的地傳送](destination-delivery.md)
* [對象中繼資料設定](audience-metadata-configuration.md)
* [聚合策略](aggregation-policy.md)
* [批次設定](batch-configuration.md)
* [歷史設定檔資格](historical-profile-qualifications.md)
