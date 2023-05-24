---
description: 瞭解如何為使用Destination SDK構建的目標配置支援的目標標識。
title: 標識命名空間配置
source-git-commit: 118ff85a9fceb8ee81dbafe2c381d365b813da29
workflow-type: tm+mt
source-wordcount: '842'
ht-degree: 4%

---


# 標識命名空間配置

Experience Platform使用標識命名空間來描述特定標識的類型。 例如，名為 `Email` 標識值類似 `name@email.com` 地址。

通過Destination SDK建立目標時，除 [配置夥伴架構](schema-configuration.md) 用戶可以將配置檔案屬性和標識映射到目標平台，您還可以定義目標平台支援的標識命名空間。

執行此操作時，除了目標配置檔案屬性外，用戶還有選擇目標身份的附加選擇。

要瞭解有關Experience Platform中標識命名空間的詳細資訊，請參見 [標識命名空間文檔](../../../../identity-service/namespaces.md)。

在為目標配置標識命名空間時，您可以微調目標支援的目標標識映射，例如：

* 允許用戶將XDM屬性映射到標識命名空間。
* 允許用戶映射 [標準標識命名空間](../../../../identity-service/namespaces.md#standard) 到您自己的標識命名空間。
* 允許用戶映射 [自定義標識命名空間](../../../../identity-service/namespaces.md#manage-namespaces) 到您自己的標識命名空間。

要瞭解此元件在與Destination SDK建立的整合中的位置，請參閱 [配置選項](../configuration-options.md) 文檔，或參閱有關如何 [使用Destination SDK配置基於檔案的目標](../../guides/configure-file-based-destination-instructions.md#create-server-file-configuration)。

您可以通過 `/authoring/destinations` 端點。 有關詳細的API調用示例，請參閱以下API參考頁，在這些示例中可以配置此頁中顯示的元件。

* [建立目標配置](../../authoring-api/destination-configuration/create-destination-configuration.md)
* [更新目標配置](../../authoring-api/destination-configuration/update-destination-configuration.md)

本文介紹可用於目標的所有受支援的標識命名空間配置選項，並顯示客戶將在平台UI中看到的內容。

>[!IMPORTANT]
>
>Destination SDK支援的所有參數名和值均 **區分大小寫**。 為避免區分大小寫錯誤，請完全按文檔所示使用參數名稱和值。

## 支援的整合類型 {#supported-integration-types}

有關哪些類型的整合支援本頁所述功能的詳細資訊，請參閱下表。

| 整合類型 | 支援功能 |
|---|---|
| 即時（流）整合 | 是 |
| 基於檔案（批處理）的整合 | 是 |

## 支援的參數 {#supported-parameters}

定義目標支援的目標標識時，可以使用下表中描述的參數來配置其行為。

| 參數 | 類型 | 必填/選填 | 說明 |
|---------|----------|---|------|
| `acceptsAttributes` | 布林值 | 選填 | 指示客戶是否可以將標準配置檔案屬性映射到您正在配置的標識。 |
| `acceptsCustomNamespaces` | 布林值 | 選填 | 指示客戶是否可以將自定義標識命名空間映射到您正在配置的標識命名空間。 |
| `acceptedGlobalNamespaces` | - | 選填 | 指示 [標準標識命名空間](../../../../identity-service/namespaces.md#standard) (例如， [!UICONTROL IDFA])客戶可以映射到您正在配置的標識。 |
| `transformation` | 字串 | 選填 | 顯示 [[!UICONTROL 應用轉換]](../../../ui/activate-segment-streaming-destinations.md#apply-transformation) 當源欄位是XDM屬性或自定義標識命名空間時，選中該對話框。 使用此選項可讓用戶在導出時能夠散列源屬性。 要啟用此選項，請將值設定為 `sha256(lower($))`。 |
| `requiredTransformation` | 字串 | 選填 | 當客戶選擇此源標識命名空間時， [[!UICONTROL 應用轉換]](../../../ui/activate-segment-streaming-destinations.md#apply-transformation) 複選框將自動應用於映射，客戶無法禁用它。 要啟用此選項，請將值設定為 `sha256(lower($))`。 |

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

必須指明 [!DNL Platform] 標識客戶能夠導出到您的目標。 一些示例 [!DNL Experience Cloud ID]，散列電子郵件，設備ID([!DNL IDFA]。 [!DNL GAID])。 這些值 [!DNL Platform] 客戶可以從目標映射到標識命名空間的標識命名空間。

標識命名空間不需要在 [!DNL Platform] 和你的目的地。
例如，客戶可以 [!DNL Platform] [!DNL IDFA] 命名空間到 [!DNL IDFA] 命名空間，或者它們可以映射 [!DNL Platform] [!DNL IDFA] 命名空間到 [!DNL Customer ID] 目標中的命名空間。

閱讀有關 [標識命名空間概述](../../../../identity-service/namespaces.md)。

## 映射注意事項

如果客戶選擇了源標識命名空間，而未選擇目標映射，平台將自動使用同名的屬性填充目標映射。

## 配置可選源欄位散列

Experience Platform客戶可以選擇以散列格式或純文字檔案格式將資料輸入平台。 如果目標平台同時接受散列資料和未散列資料，則您可以為客戶提供選擇在將源欄位值導出到目標時平台是否應散列源欄位值。

以下配置可選 [應用轉換](../../../ui/activate-segment-streaming-destinations.md#apply-transformation) 選項。

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

將未散列的源屬性映射到目標預期散列的目標屬性時(例如： `email_lc_sha256` 或 `phone_sha256`)，檢查 **應用轉換** 選項，使Adobe Experience Platform在激活時自動散列源屬性。

## 配置強制源欄位散列

如果目標僅接受散列資料，則可以將導出的屬性配置為由平台自動散列。 以下配置將自動檢查 **應用轉換** 選項 `Email` 和 `Phone` 標識被映射。

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

閱讀本文後，您應更瞭解如何為使用Destination SDK構建的目標配置標識命名空間。

要瞭解有關其他目標元件的詳細資訊，請參閱以下文章：

* [客戶驗證](customer-authentication.md)
* [OAuth2身份驗證](oauth2-authentication.md)
* [客戶資料欄位](customer-data-fields.md)
* [UI屬性](ui-attributes.md)
* [架構配置](schema-configuration.md)
* [標識命名空間配置](identity-namespace-configuration.md)
* [支援的映射配置](supported-mapping-configurations.md)
* [目標傳遞](destination-delivery.md)
* [受眾元資料配置](audience-metadata-configuration.md)
* [聚合策略](aggregation-policy.md)
* [批配置](batch-configuration.md)
* [歷史配置檔案資格](historical-profile-qualifications.md)
