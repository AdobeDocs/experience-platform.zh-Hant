---
title: Google Ads Source概觀
description: 瞭解如何使用API或使用者介面將Google Ads連結至Adobe Experience Platform。
exl-id: 1f6257e0-213c-4723-a240-511c11c5833c
source-git-commit: ac90eea69f493bf944a8f9920426a48d62faaa6c
workflow-type: tm+mt
source-wordcount: '562'
ht-degree: 0%

---

# [!DNL Google Ads]來源

>[!NOTE]
>
>[!DNL Google Ads]來源是測試版。 如需使用Beta標籤聯結器的詳細資訊，請參閱[來源概觀](../../home.md#terms-and-conditions)。

Adobe Experience Platform可讓您從外部來源擷取資料，同時使用Experience Platform服務來建構、加標籤及增強傳入資料。 您可以從多種來源(例如Adobe應用程式、雲端儲存、資料庫和許多其他來源)內嵌資料。

Experience Platform支援從協力廠商廣告系統擷取資料。 對廣告提供者的支援包括[!DNL Google Ads]。

## 先決條件 {#prerequisites}

### IP位址允許清單

使用來源聯結器之前，必須將IP位址清單新增至允許清單。 未能將您區域特定的IP位址新增到允許清單可能會導致使用來源時的錯誤或效能不佳。 如需詳細資訊，請參閱[IP位址允許清單](../../ip-address-allow-list.md)頁面。

### 在Experience Platform上設定許可權

您必須同時為您的帳戶啟用&#x200B;**[!UICONTROL 檢視來源]**&#x200B;和&#x200B;**[!UICONTROL 管理來源]**&#x200B;許可權，才能將您的[!DNL Google Ads]帳戶連線至Experience Platform。 請聯絡您的產品管理員以取得必要許可權。 如需詳細資訊，請閱讀[存取控制UI指南](../../../access-control/ui/overview.md)。

### 收集必要的認證

您必須提供適當的值給下列認證，才能成功地將您的[!DNL Google Ads]帳戶連線到Experience Platform。

| 認證 | 說明 |
| --- | --- |
| `clientCustomerId` | 使用者端客戶ID是與您要使用[!DNL Google Ads] API管理的[!DNL Google Ads]使用者端帳戶對應的帳號。 此ID遵循`123-456-7890`的範本。 |
| `loginCustomerId` | 登入客戶ID是與您的[!DNL Google Ads]管理員帳戶對應的帳號，用於從特定的作業客戶擷取報表資料。 如需登入客戶ID的詳細資訊，請閱讀[[!DNL Google Ads] API檔案](https://developers.google.com/search-ads/reporting/concepts/login-customer-id)。 |
| `developerToken` | 開發人員權杖可讓您存取[!DNL Google Ads] API。 您可以使用相同的開發人員Token來針對所有[!DNL Google Ads]帳戶提出要求。 透過[登入您的管理員帳戶](https://ads.google.com/home/tools/manager-accounts/)，然後導覽至[!DNL API Center]頁面來擷取您的開發人員權杖。 |
| `refreshToken` | 重新整理權杖是[!DNL OAuth2]驗證的一部分。 此權杖可讓您在存取權杖過期後重新產生存取權杖。 |
| `clientId` | 使用者端ID與使用者端密碼搭配使用，是[!DNL OAuth2]驗證的一部分。 使用者端ID和使用者端密碼可讓您的應用程式透過向[!DNL Google]識別您的應用程式來代表您的帳戶運作。 |
| `clientSecret` | 使用者端密碼會與使用者端ID搭配使用，作為[!DNL OAuth2]驗證的一部分。 使用者端ID和使用者端密碼可讓您的應用程式透過向[!DNL Google]識別您的應用程式來代表您的帳戶運作。 |
| `googleAdsApiVersion` | [!DNL Google Ads]目前支援的API版本。 雖然最新版本為`v18`，但Experience Platform上支援的最新版本為`v17`。 |
| `connectionSpec.id` | 連線規格會傳回來源的聯結器屬性，包括與建立基礎連線和來源連線相關的驗證規格。 [!DNL Google Ads]的連線規格識別碼為： `d771e9c1-4f26-40dc-8617-ce58c4b53702`。 如果您使用[!DNL Flow Service] API連線您的[!DNL Google Ads]帳戶，則需要此值。 |

## 將[!DNL Google Ads]連線至Experience Platform

以下檔案提供如何使用API或使用者介面將[!DNL Google Ads]連線至Experience Platform的資訊：

### 使用API

* [使用流量服務API建立Google Ads基本連線](../../tutorials/api/create/advertising/ads.md)
* [使用流量服務API探索資料表](../../tutorials/api/explore/tabular.md)
* [使用流量服務API為廣告來源建立資料流](../../tutorials/api/collect/advertising.md)

### 使用UI

* [在UI中建立Google Ads來源連線](../../tutorials/ui/create/advertising/ads.md)
* [在UI中為Advertising來源連線建立資料流](../../tutorials/ui/dataflow/advertising.md)
