---
keywords: google客戶比對；Google客戶比對；Google客戶比對
title: Google Customer Match連線
description: Google Customer Match可讓您使用線上和離線資料，透過Google所擁有和營運的屬性（例如搜尋、購物和Gmail）聯絡客戶，並與客戶重新互動。
exl-id: 8209b5eb-b05c-4ef7-9fdc-22a528d5f020
source-git-commit: ce205622260f4252d1a7db7c5011366fb2ed4d3c
workflow-type: tm+mt
source-wordcount: '2410'
ht-degree: 2%

---

# [!DNL Google Customer Match]個連線

>[!IMPORTANT]
>
> Google正在發佈[Google Ads API](https://developers.google.com/google-ads/api/docs/start)、[Customer Match](https://ads-developers.googleblog.com/2023/10/updates-to-customer-match-conversion.html)和[Display &amp; Video 360 API](https://developers.google.com/display-video/api/guides/getting-started/overview)的變更，以支援歐盟（[歐盟使用者同意政策](https://www.google.com/about/company/user-consent-policy/)）中[數位市場法](https://digital-markets-act.ec.europa.eu/index_en) (DMA)所定義的法規遵循與同意相關需求。 自2024年3月6日起，將開始強制執行同意要求的這些變更。
><br/>
>為了遵循歐盟使用者同意政策並繼續為歐洲經濟區(EEA)的使用者建立對象清單，廣告商和合作夥伴必須確保在上傳對象資料時傳遞一般使用者同意。 作為 Google 合作夥伴，Adobe 會為您提供必要的工具，以遵守歐盟之 DMA 規定的這些同意要求。
><br/>
>已購買Adobe Privacy &amp; Security Shield且已設定[同意原則](../../../data-governance/enforcement/auto-enforcement.md#consent-policy-evaluation)以篩選掉非同意的設定檔的客戶，不必採取任何動作。
><br/>
>未購買Adobe Privacy &amp; Security Shield的客戶必須使用[區段產生器](../../../segmentation/ui/segment-builder.md)中的[區段定義](../../../segmentation/home.md#segment-definitions)功能，篩選出未同意的設定檔，才能繼續使用現有的Real-Time CDP Google目的地而不中斷。

[[!DNL Google Customer Match]](https://support.google.com/google-ads/answer/6379332?hl=en)可讓您使用線上和離線資料，透過Google所擁有和運作的屬性（例如： [!DNL Search]、[!DNL Shopping]和[!DNL Gmail]），聯絡及重新與您的客戶互動。

>[!TIP]
>
>若要透過[!DNL YouTube]詳細目錄聯絡客戶，請使用[Google Customer Match + DV360](/help/destinations/catalog/advertising/google-customer-match-dv360.md)目的地，此目的地使用Google對象合作夥伴API。

![Adobe Experience Platform UI中的Google Customer Match目的地。](../../assets/catalog/advertising/google-customer-match/catalog.png)

## 使用案例 {#use-cases}

為協助您更清楚瞭解如何使用[!DNL Google Customer Match]目的地，以下是Adobe Experience Platform客戶可以使用此功能解決的範例使用案例。

### 使用案例#1

運動服裝品牌想要透過[!DNL Google Search]和[!DNL Google Shopping]觸及現有客戶，以根據他們過去的購買和瀏覽記錄來個人化優惠和專案。 服飾品牌可以從他們自己的CRM擷取電子郵件地址到Experience Platform，並從他們自己的離線資料建立受眾。 接著，他們可以將這些對象傳送至[!DNL Google Customer Match]，以便在[!DNL Search]和[!DNL Shopping]中使用，最佳化其廣告支出。

### 使用案例#2

>[!TIP]
>
>若要在[!DNL YouTube]詳細目錄上執行此使用案例，請使用新的[Google Customer Match + DV360](/help/destinations/catalog/advertising/google-customer-match-dv360.md)目的地，此目的地使用Google對象合作夥伴API。

一家知名科技公司推出新手機。 為了推廣此新款手機，他們想要讓擁有舊款手機的客戶進一步瞭解手機的新功能和特性。

為了提升此版本，他們會使用電子郵件地址作為識別碼，從CRM資料庫將電子郵件地址上傳到Experience Platform。 建立受眾的基礎是擁有舊款手機型號的客戶。 然後會將對象傳送到[!DNL Google Customer Match]，以便公司可以在[!DNL YouTube]上鎖定目前的客戶、擁有舊版手機型號的客戶以及類似的客戶。

## [!DNL Google Customer Match]個目的地的資料控管 {#data-governance}

Experience Platform中的某些目的地對於傳送到目的地平台或從目的地平台接收的資料具有某些規則和義務。 您有責任瞭解您資料的限制與義務，以及如何在Adobe Experience Platform和目的地平台中使用該資料。 Adobe Experience Platform提供資料治理工具，協助您管理其中一些資料使用義務。 [進一步瞭解](../../../data-governance/labels/overview.md)資料治理工具和原則。

## 支援的身分 {#supported-identities}

[!DNL Google Customer Match]支援下表所述的身分啟用。 深入瞭解[身分](/help/identity-service/features/namespaces.md)。

| 目標身分 | 說明 | 考量事項 |
|---|---|---|
| `GAID` | GOOGLE ADVERTISING ID | 當您的來源身分是GAID名稱空間時，請選取此目標身分。 |
| `IDFA` | 廣告商適用的Apple ID | 當您的來源身分是IDFA名稱空間時，請選取此目標身分。 |
| `phone_sha256_e.164` | E164格式的電話號碼，使用SHA256演演算法雜湊 | Adobe Experience Platform同時支援純文字和SHA256雜湊電話號碼。 請依照[識別碼符合需求](#id-matching-requirements-id-matching-requirements)區段中的指示操作，分別使用適當的名稱空間來使用純文字和雜湊電話號碼。 當您的來源欄位包含未雜湊的屬性時，請核取&#x200B;**[!UICONTROL 套用轉換]**&#x200B;選項，讓[!DNL Experience Platform]在啟用時自動雜湊資料。 |
| `email_lc_sha256` | 使用SHA256演演算法雜湊的電子郵件地址 | Adobe Experience Platform同時支援純文字和SHA256雜湊電子郵件地址。 請依照[識別碼符合需求](#id-matching-requirements-id-matching-requirements)區段中的指示操作，針對純文字和雜湊電子郵件地址分別使用適當的名稱空間。 當您的來源欄位包含未雜湊的屬性時，請核取&#x200B;**[!UICONTROL 套用轉換]**&#x200B;選項，讓[!DNL Experience Platform]在啟用時自動雜湊資料。 |
| `user_id` | 自訂使用者ID | 當您的來源身分是自訂名稱空間時，請選取此目標身分。 |
| `address_info_first_name` | 使用者的名字 | 當您想要將郵寄地址資料傳送到目的地時，此目標身分應該與`address_info_last_name`、`address_info_country_code`和`address_info_postal_code`搭配使用。 <br><br>為確保Google符合位址，您必須對應全部四個位址欄位（`address_info_first_name`、`address_info_last_name`、`address_info_country_code`和`address_info_postal_code`），並確定這些欄位在匯出的設定檔中都沒有遺漏資料。 <br>如果有任何欄位未對應或包含遺漏的資料，Google將不會符合位址。 |
| `address_info_last_name` | 使用者的姓氏 | 當您想要將郵寄地址資料傳送到目的地時，此目標身分應該與`address_info_first_name`、`address_info_country_code`和`address_info_postal_code`搭配使用。 <br><br>為確保Google符合位址，您必須對應全部四個位址欄位（`address_info_first_name`、`address_info_last_name`、`address_info_country_code`和`address_info_postal_code`），並確定這些欄位在匯出的設定檔中都沒有遺漏資料。 <br>如果有任何欄位未對應或包含遺漏的資料，Google將不會符合位址。 |
| `address_info_country_code` | 使用者地址國家/地區代碼 | 當您想要將郵寄地址資料傳送到目的地時，此目標身分應該與`address_info_first_name`、`address_info_last_name`和`address_info_postal_code`搭配使用。 <br><br>為確保Google符合位址，您必須對應全部四個位址欄位（`address_info_first_name`、`address_info_last_name`、`address_info_country_code`和`address_info_postal_code`），並確定這些欄位在匯出的設定檔中都沒有遺漏資料。 <br>如果有任何欄位未對應或包含遺漏的資料，Google將不會符合位址。 <br><br>接受的格式：小寫、雙字母國碼，格式為[ISO 3166-1 alpha-2](https://en.wikipedia.org/wiki/ISO_3166-1_alpha-2)。 |
| `address_info_postal_code` | 使用者地址郵遞區號 | 當您想要將郵寄地址資料傳送到目的地時，此目標身分應該與`address_info_first_name`、`address_info_last_name`和`address_info_country_code`搭配使用。 <br><br>為確保Google符合位址，您必須對應全部四個位址欄位（`address_info_first_name`、`address_info_last_name`、`address_info_country_code`和`address_info_postal_code`），並確定這些欄位在匯出的設定檔中都沒有遺漏資料。 <br>如果有任何欄位未對應或包含遺漏的資料，Google將不會符合位址。 |

{style="table-layout:auto"}

## 支援的對象 {#supported-audiences}

本節說明您可以將哪些型別的對象匯出至此目的地。

| 對象來源 | 支援 | 說明 |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | 透過Experience Platform [細分服務](../../../segmentation/home.md)產生的對象。 |
| 自訂上傳 | ✓ | 對象[從CSV檔案匯入](../../../segmentation/ui/audience-portal.md#import-audience)至Experience Platform。 |

{style="table-layout:auto"}

## 匯出型別和頻率 {#export-type-frequency}

請參閱下表以取得目的地匯出型別和頻率的資訊。

| 項目 | 類型 | 附註 |
---------|----------|---------|
| 匯出類型 | **[!UICONTROL 對象匯出]** | 您正在匯出具有[!DNL Google Customer Match]目的地中所使用識別碼（名稱、電話號碼及其他）之對象的所有成員。 |
| 匯出頻率 | **[!UICONTROL 串流]** | 串流目的地是「一律開啟」的API型連線。 根據對象評估在Experience Platform中更新設定檔後，聯結器會立即將更新傳送至下游的目標平台。 深入瞭解[串流目的地](/help/destinations/destination-types.md#streaming-destinations)。 |

{style="table-layout:auto"}

## [!DNL Google Customer Match]帳戶必要條件 {#google-account-prerequisites}

在Experience Platform中設定[!DNL Google Customer Match]目的地之前，請確定您已閱讀並遵守Google有關使用[!DNL Customer Match]的原則(如[Google支援檔案](https://support.google.com/google-ads/answer/6299717)中所述)。

接下來，確定您的[!DNL Google]帳戶已設定為[!DNL Standard]或更高的許可權等級。 如需詳細資訊，請參閱[Google Ads檔案](https://support.google.com/google-ads/answer/9978556?visit_id=637611563637058259-4176462731&amp;rd=1)。

### 允許清單 {#allowlist}

在Experience Platform中建立[!DNL Google Customer Match]目的地之前，請確定您的[!DNL Google Ads]帳戶符合[[!DNL Google Customer Match] 原則](https://support.google.com/google-ads/answer/6299717/customer-match-policy)。

Google會自動將擁有合規帳戶的客戶加入允許清單。

## ID比對要求 {#id-matching-requirements}

[!DNL Google]要求未明確傳送任何個人識別資訊(PII)。 因此，啟用至[!DNL Google Customer Match]的對象可以從&#x200B;*雜湊*&#x200B;識別碼中中斷連線，例如電子郵件地址或電話號碼。

根據您擷取至Adobe Experience Platform的ID型別，您必須遵守其對應的要求。

### 電話號碼雜湊需求 {#phone-number-hashing-requirements}

在[!DNL Google Customer Match]中啟用電話號碼的方法有兩種：

* **擷取原始電話號碼**：您可以將[!DNL E.164]格式的原始電話號碼擷取至[!DNL Experience Platform]，這些電話號碼在啟用時自動雜湊。 如果選擇此選項，請務必將原始電話號碼擷取到`Phone_E.164`名稱空間。
* **擷取雜湊電話號碼**：您可以在擷取至[!DNL Experience Platform]之前預先雜湊電話號碼。 如果選擇此選項，請務必將雜湊電話號碼擷取到`PHONE_SHA256_E.164`名稱空間。

>[!NOTE]
>
>無法在[!DNL Google Customer Match]中啟用擷取至`Phone`名稱空間的電話號碼。

### 電子郵件雜湊需求 {#hashing-requirements}

您可以將電子郵件地址雜湊後再擷取至Adobe Experience Platform，或在Experience Platform中清楚使用電子郵件地址，並在啟用時將[!DNL Experience Platform]個電子郵件地址雜湊。

如需Google雜湊需求和其他啟用限制的詳細資訊，請參閱Google檔案中的下列章節：

* [[!DNL Customer Match] 使用電子郵件地址、地址或使用者識別碼](https://developers.google.com/google-ads/api/docs/remarketing/audience-types/customer-match#customer_match_with_email_address_address_or_user_id)
* [[!DNL Customer Match] 考量事項](https://developers.google.com/google-ads/api/docs/remarketing/audience-types/customer-match#customer_match_considerations)
* [[!DNL Customer Match] 使用電話號碼](https://developers.google.com/google-ads/api/docs/remarketing/audience-types/customer-match#customer_match_with_phone_number)
* [[!DNL Customer Match] 使用行動裝置ID](https://developers.google.com/google-ads/api/docs/remarketing/audience-types/customer-match#customer_match_with_mobile_device_ids)


若要瞭解如何在Experience Platform中擷取電子郵件地址，請參閱[批次擷取總覽](../../../ingestion/batch-ingestion/overview.md)和[串流擷取總覽](../../../ingestion/streaming-ingestion/overview.md)。

如果您選擇自行雜湊電子郵件地址，請務必遵守Google的要求，如上述連結所述。

### 滿足欄位雜湊需求 {#address-field-hashing}

將位址相關欄位對應至[!DNL Google Customer Match]時，Experience Platform **會在傳送至Google之前，自動雜湊** `address_info_first_name`和`address_info_last_name`值。 此自動雜湊是遵守Google安全性和隱私權需求所需。

請&#x200B;**不要**&#x200B;提供`address_info_first_name`或`address_info_last_name`的預先雜湊值。 如果您提供已雜湊的值，比對程式將會失敗。

### 使用自訂名稱空間 {#custom-namespaces}

在使用`User_ID`名稱空間將資料傳送至Google之前，請確定您使用[!DNL gTag]同步處理自己的識別碼。 如需詳細資訊，請參閱[Google正式檔案](https://support.google.com/google-ads/answer/9199250)。

<!-- Data from unhashed namespaces is automatically hashed by [!DNL Experience Platform] upon activation.

Attribute source data is not automatically hashed. When your source field contains unhashed attributes, check the **[!UICONTROL Apply transformation]** option, to have [!DNL Experience Platform] automatically hash the data on activation.
![Identity mapping transformation](../../assets/ui/activate-destinations/identity-mapping-transformation.png) -->

<!-- ## Configure destination - video walkthrough {#video}

The video below demonstrates the steps to configure a [!DNL Google Customer Match] destination and activate audiences. The steps are also laid out sequentially in the next sections.

>[!VIDEO](https://video.tv.adobe.com/v/332599/?quality=12&learn=on&captions=eng) -->

## 影片概觀 {#video-overview}

觀看以下影片，瞭解優點以及如何對Google Customer Match啟用資料。

>[!VIDEO](https://video.tv.adobe.com/v/38180/)

## 連線到目標 {#connect}

>[!IMPORTANT]
> 
>若要連線到目的地，您需要&#x200B;**[!UICONTROL 檢視目的地]**&#x200B;和&#x200B;**[!UICONTROL 管理目的地]** [存取控制許可權](/help/access-control/home.md#permissions)。 閱讀[存取控制總覽](/help/access-control/ui/overview.md)或連絡您的產品管理員以取得必要的許可權。

若要連線到此目的地，請依照[目的地組態教學課程](../../ui/connect-destination.md)中所述的步驟進行。

### 連線參數 {#parameters}

在[設定](../../ui/connect-destination.md)此目的地時，您必須提供下列資訊：

* **[!UICONTROL 名稱]**：提供此目的地連線的名稱
* **[!UICONTROL 描述]**：提供此目的地連線的描述
* **[!UICONTROL 帳戶ID]**：您的[Google Ads客戶識別碼](https://support.google.com/google-ads/answer/1704344?hl=en)。 ID的格式為xxx-xxx-xxxx。 如果您使用[!DNL Google Ads Manager Account (My Client Center)]，請勿使用您的管理員帳戶ID。 請改用[Google Ads客戶ID](https://support.google.com/google-ads/answer/1704344?hl=en)。

>[!IMPORTANT]
>
> * 預設會為[!DNL Google Customer Match]目的地選取&#x200B;**[!UICONTROL 與PII]**&#x200B;結合行銷動作，且無法移除。

### 啟用警示 {#enable-alerts}

您可以啟用警報以接收有關傳送到您目的地的資料流狀態的通知。 從清單中選取警報以訂閱接收有關資料流狀態的通知。 如需警示的詳細資訊，請參閱[使用UI訂閱目的地警示](../../ui/alerts.md)的指南。

當您完成提供目的地連線的詳細資訊後，請選取&#x200B;**[!UICONTROL 下一步]**。

## 啟動此目標的對象 {#activate}

>[!IMPORTANT]
> 
>* 若要啟用資料，您需要&#x200B;**[!UICONTROL 檢視目的地]**、**[!UICONTROL 啟用目的地]**、**[!UICONTROL 檢視設定檔]**&#x200B;和&#x200B;**[!UICONTROL 檢視區段]** [存取控制許可權](/help/access-control/home.md#permissions)。 閱讀[存取控制總覽](/help/access-control/ui/overview.md)或連絡您的產品管理員以取得必要的許可權。
>* 若要將&#x200B;*身分*&#x200B;匯出至目的地，您需要&#x200B;**[!UICONTROL 檢視身分圖表]** [存取控制許可權](/help/access-control/home.md#permissions)。<br> ![選取工作流程中反白的身分名稱空間，以啟用目的地的對象。](/help/destinations/assets/overview/export-identities-to-destination.png "選取工作流程中反白顯示的身分名稱空間，以啟用目的地的對象。"){width="100" zoomable="yes"}

如需啟用此目的地的對象的指示，請參閱[啟用串流對象匯出目的地的對象資料](../../ui/activate-segment-streaming-destinations.md)。

在&#x200B;**[!UICONTROL 區段排程]**&#x200B;步驟中，傳送[!DNL IDFA]或[!DNL GAID]對象至[!DNL Google Customer Match]時，您必須提供[!UICONTROL 應用程式ID]。

![啟用工作流程區段排程步驟中反白顯示的Google客戶比對應用程式ID欄位。](../../assets/catalog/advertising/google-customer-match/gcm-destination-appid.png)

如需如何尋找[!DNL App ID]的詳細資訊，請參閱[Google官方檔案](https://developers.google.com/adwords/api/docs/reference/v201809/AdwordsUserListService.CrmBasedUserList#appid)，或詢問您的Google代表。

### 對應範例：在[!DNL Google Customer Match]中啟用對象資料 {#example-gcm}

這是在[!DNL Google Customer Match]中啟用對象資料時的正確身分對應範例。

選取來源欄位：

* 如果您使用的電子郵件地址未進行雜湊處理，請選取`Email`名稱空間作為來源身分。
* 如果您根據[!DNL Google Customer Match] [電子郵件雜湊需求](#hashing-requirements)將資料擷取的客戶電子郵件地址雜湊至[!DNL Experience Platform]，請選取`Email_LC_SHA256`名稱空間作為來源身分。
* 如果您的資料包含非雜湊電話號碼，請選取`PHONE_E.164`名稱空間作為來源身分。 [!DNL Experience Platform]將雜湊電話號碼以符合[!DNL Google Customer Match]要求。
* 如果您根據[!DNL Facebook] [電話號碼雜湊需求](#phone-number-hashing-requirements)，將資料擷取中的電話號碼雜湊至[!DNL Experience Platform]，請選取`Phone_SHA256_E.164`名稱空間作為來源身分。
* 如果您的資料包含[!DNL Apple]個裝置識別碼，請選取`IDFA`名稱空間作為來源識別碼。
* 如果您的資料包含[!DNL Android]個裝置識別碼，請選取`GAID`名稱空間作為來源識別碼。
* 如果您的資料包含其他型別的識別碼，請選取`Custom`名稱空間作為來源識別碼。

選取目標欄位：

* 當來源名稱空間為`Email`或`Email_LC_SHA256`時，請選取`Email_LC_SHA256`名稱空間作為目標身分。
* 當來源名稱空間為`PHONE_E.164`或`Phone_SHA256_E.164`時，請選取`Phone_SHA256_E.164`名稱空間作為目標身分。
* 當來源名稱空間為`IDFA`或`GAID`時，請選取`IDFA`或`GAID`名稱空間作為目標身分。
* 當您的來源名稱空間是自訂名稱空間時，請選取`User_ID`名稱空間作為目標身分。

![啟動工作流程對應步驟中顯示的來源與目標欄位之間的身分對應。](../../assets/ui/activate-segment-streaming-destinations/identity-mapping-gcm.png)

來自未雜湊名稱空間的資料在啟用時由[!DNL Experience Platform]自動雜湊。

屬性來源資料不會自動雜湊。 當您的來源欄位包含未雜湊的屬性時，請核取&#x200B;**[!UICONTROL 套用轉換]**&#x200B;選項，讓[!DNL Experience Platform]在啟用時自動雜湊資料。

![套用啟用工作流程對應步驟中反白顯示的轉換控制項。](../../assets/ui/activate-segment-streaming-destinations/identity-mapping-gcm-transformation.png)

## 監視目的地 {#monitor-destination}

連線到目的地並建立目的地資料流後，您可以使用Real-Time CDP中的[監視功能](/help/dataflows/ui/monitor-destinations.md)來取得每次資料流執行中在您的目的地啟用的設定檔記錄的廣泛資訊。

>[!IMPORTANT]
>
>當您對應四個與位址相關的目標身分（`address_info_first_name`、`address_info_last_name`、`address_info_country_code`及`address_info_postal_code`）時，它們會在資料流監視頁面中計為每個設定檔的個別身分。

## 驗證對象啟用是否成功 {#verify-activation}

完成啟用流程後，切換至您的&#x200B;**[!UICONTROL Google Ads]**&#x200B;帳戶。 啟用的對象會在您的Google帳戶中顯示為客戶清單。 根據您的對象規模，除非有100多位活躍使用者可服務，否則部分對象不會填入。

將對象對應至[!DNL IDFA]和[!DNL GAID]行動ID時，[!DNL Google Customer Match]會為每個ID對應建立個別的對象。 您的[!DNL Google Ads]帳戶顯示兩個不同的區段，一個用於[!DNL IDFA]，另一個用於[!DNL GAID]對應。

## 疑難排解 {#troubleshooting}

### 400錯誤請求錯誤訊息 {#bad-request}

設定此目的地時，您可能會收到下列錯誤：

`{"message":"Google Customer Match Error: OperationAccessDenied.ACTION_NOT_PERMITTED","code":"400 BAD_REQUEST"}`

當客戶帳戶不符合[必要條件](#google-account-prerequisites)時，就會發生此錯誤。 若要修正此問題，請連絡Google，並確認您的帳戶已加入允許清單，且已設定為[!DNL Standard]或更高的許可權等級。 如需詳細資訊，請參閱[Google Ads檔案](https://support.google.com/google-ads/answer/9978556?visit_id=637611563637058259-4176462731&amp;rd=1)。