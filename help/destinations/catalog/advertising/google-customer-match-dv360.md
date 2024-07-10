---
title: Google Customer Match +顯示器和視訊360連線
description: 透過Google Customer Match + Display & Video 360目的地聯結器，您可以使用Experience Platform的線上和離線資料，在Google擁有和營運的資產(例如搜尋、購物、Gmail和YouTube)觸及並重新與客戶互動。
badgeBeta: label="Beta" type="Informative"
exl-id: f6da3eae-bf3f-401a-99a1-2cca9a9058d2
source-git-commit: c35b43654d31f0f112258e577a1bb95e72f0a971
workflow-type: tm+mt
source-wordcount: '1935'
ht-degree: 1%

---

# [!DNL Google Customer Match + Display & Video 360] 連線

使用此目的地來啟用您的第一方PII型 [[!DNL Google Customer Match]](https://support.google.com/google-ads/answer/6379332?hl=en) 直接清單至 [!DNL Google Display & Video 360] 屬性，例如 [!DNL Search]， [!DNL YouTube]， [!DNL Gmail]，以及 [!DNL Google Display Network].

某些Google整合的第三方(例如Adobe Real-Time CDP)可使用 [!DNL Google Audience Partner API] 以建立 [!DNL Customer Match] 直接在客戶的 [!DNL Display & Video 360] 帳戶。

具備新推出的功能，能夠利用 [!DNL Customer Matched] 對象範圍 [!DNL Display & Video 360]，您現在可以在擴充的詳細目錄來源名冊中鎖定對象。

>[!IMPORTANT]
>
>此目的地聯結器為測試版，僅供特定客戶使用。 若要要求存取權，請聯絡您的Adobe代表。

![Adobe Experience Platform UI中的Google Customer Match + DV360目的地。](/help/destinations/assets/catalog/advertising/gcm-dv360/catalog.png)

## 與歐盟更新同意要求有關的Google目的地變更的重要通知

>[!IMPORTANT]
>
> Google即將發佈的變更專案 [Google Ads API](https://developers.google.com/google-ads/api/docs/start)， [Customer Match](https://ads-developers.googleblog.com/2023/10/updates-to-customer-match-conversion.html)，以及 [Display &amp; Video 360 API](https://developers.google.com/display-video/api/guides/getting-started/overview) 以支援「 」中定義的合規性和同意相關要求 [數位市場法案](https://digital-markets-act.ec.europa.eu/index_en) (DMA)在歐盟([歐盟使用者同意原則](https://www.google.com/about/company/user-consent-policy/))。 自2024年3月6日起，將開始強制執行同意要求的這些變更。
><br/>
>為了遵循歐盟使用者同意政策並繼續為歐洲經濟區(EEA)的使用者建立對象清單，廣告商和合作夥伴必須確保在上傳對象資料時傳遞一般使用者同意。 Adobe身為Google合作夥伴，為您提供在歐盟DMA下符合這些同意要求的必要工具。
><br/>
>已購買AdobePrivacy &amp; Security Shield且已設定 [同意原則](../../../data-governance/enforcement/auto-enforcement.md#consent-policy-evaluation) 不需要採取任何動作，即可篩選出未同意的設定檔。
><br/>
>尚未購買AdobePrivacy &amp; Security Shield的客戶必須使用 [區段定義](../../../segmentation/home.md#segment-definitions) 中的功能 [區段產生器](../../../segmentation/ui/segment-builder.md) 以篩選掉未同意的設定檔，以便持續使用現有的Real-Time CDP Google目標而不中斷。

## 使用此目的地的時間

目的地目錄中有數個與Google的整合，因此可能很難瞭解何時使用每個可用的Google目的地。 閱讀下表中的資訊，瞭解不同的使用案例：

| [Google 目標客戶比對](/help/destinations/catalog/advertising/google-customer-match.md) | [Google Display &amp; Video 360](/help/destinations/catalog/advertising/google-dv360.md) | [!DNL Google Customer Match] + [!DNL Display & Video 360] （此聯結器） |
|---------|----------|---------|
| 匯出以PII為基礎的對象，並透過中的可用詳細目錄聯絡他們。 [!DNL Google Customer Match]. | 透過以下方式觸及各種詳細目錄中的Cookie型對象： [!DNL Google Display & Video 360]，針對Google擁有及運營的資產，例如Youtube和 [!DNL Search]、及更多功能。 | 在中建立PII型對象 [!DNL Google Customer Match] 並透過中提供的詳細目錄聯絡他們 [!DNL Google Display & Video 360]，僅針對Google擁有及運作的屬性。 |

## 使用案例 {#use-cases}

為協助您更清楚瞭解如何及何時使用此目的地，以下是Adobe Experience Platform客戶可以使用此功能解決的範例使用案例。

### 使用案例#1

運動服裝品牌想要透過觸及現有客戶 [!DNL Google Search] 和 [!DNL Google Shopping] 根據優惠方案與專案的過去購買與瀏覽記錄，進行個人化。 服飾品牌可以從他們自己的CRM擷取電子郵件地址以進行Experience Platform，以及從他們自己的離線資料建立受眾。 接著，他們可以將這些對象傳送至 [!DNL Google Customer Match + Display & Video 360] 要跨以下專案使用的目的地： [!DNL Google Display & Video 360] 屬性，例如 [!DNL Search]， [!DNL YouTube]， [!DNL Gmail]，以及 [!DNL Google Display Network].

### 使用案例#2

一家知名科技公司已推出新手機。 為了推廣此新款手機，他們想要讓擁有舊款手機的客戶進一步瞭解手機的新功能和特性。

為了提升版本，他們會使用電子郵件地址作為識別碼，從CRM資料庫上傳電子郵件地址至Experience Platform。 建立受眾的基礎是擁有舊款手機型號的客戶。 然後會將對象傳送到 [!DNL Google Customer Match]，以便公司能鎖定目前的客戶、擁有舊款手機型號的客戶，以及在上的類似客戶 [!DNL Google Display & Video 360] 屬性，例如 [!DNL Search]， [!DNL YouTube]， [!DNL Gmail]，以及 [!DNL Google Display Network].

## 支援的身分 {#supported-identities}

[!DNL Google Customer Match] 支援下表所述的身分啟用。 進一步瞭解 [身分](/help/identity-service/features/namespaces.md).

| 目標身分 | 說明 | 考量事項 |
|---|---|---|
| phone_sha256_e.164 | E164格式的電話號碼，使用SHA256演演算法雜湊 | Adobe Experience Platform同時支援純文字和SHA256雜湊電話號碼。 請依照 [ID比對要求](#id-matching-requirements-id-matching-requirements) 區段，並針對純文字和雜湊電話號碼分別使用適當的名稱空間。 當來源欄位包含未雜湊屬性時，請核取 **[!UICONTROL 套用轉換]** 選項，擁有 [!DNL Platform] 啟動時自動雜湊資料。 |
| email_lc_sha256 | 使用SHA256演演算法雜湊的電子郵件地址 | Adobe Experience Platform同時支援純文字和SHA256雜湊電子郵件地址。 請依照 [ID比對要求](#id-matching-requirements-id-matching-requirements) 區段，並針對純文字和雜湊電子郵件地址分別使用適當的名稱空間。 當來源欄位包含未雜湊屬性時，請核取 **[!UICONTROL 套用轉換]** 選項，擁有 [!DNL Platform] 啟動時自動雜湊資料。 |

{style="table-layout:auto"}

<!-- not supported in beta

|GAID|Google Advertising ID|Select this target identity when your source identity is a GAID namespace.|
|IDFA|Apple ID for Advertisers|Select this target identity when your source identity is an IDFA namespace.|
|user_id|Custom user IDs|Select this target identity when your source identity is a custom namespace.| 

-->

## 支援的對象 {#supported-audiences}

本節說明您可以將哪些型別的對象匯出至此目的地。

| 對象來源 | 支援 | 說明 |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ (A) | 透過Experience Platform產生的對象 [分段服務](../../../segmentation/home.md). |
| 自訂上傳 | ✓ (A) | 受眾 [已匯入](../../../segmentation/ui/audience-portal.md#import-audience) 從CSV檔案Experience Platform為。 |

{style="table-layout:auto"}

## 匯出型別和頻率 {#export-type-frequency}

請參閱下表以取得目的地匯出型別和頻率的資訊。

| 項目 | 類型 | 附註 |
---------|----------|---------|
| 匯出類型 | **[!UICONTROL 對象匯出]** | 您正在匯出某個對象的所有成員，而這些成員中都有用於的識別碼（名稱、電話號碼及其他）。 [!DNL Google Customer Match] 目的地。 |
| 匯出頻率 | **[!UICONTROL 串流]** | 串流目的地是「一律開啟」的API型連線。 一旦根據對象評估在Experience Platform中更新了設定檔，聯結器就會將更新傳送至下游的目的地平台。 深入瞭解 [串流目的地](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## [!DNL Google Customer Match] 帳戶必要條件 {#google-account-prerequisites}

設定前 [!DNL Google Customer Match] 目的地為Experience Platform，請務必閱讀並遵守Google的使用原則 [!DNL Customer Match]，概述於 [Google支援檔案](https://support.google.com/google-ads/answer/6299717).

接下來，確定您的 [!DNL Google] 帳戶設定用於 [!DNL Standard] 或更高許可權層級。 請參閱 [Google Ads檔案](https://support.google.com/google-ads/answer/9978556?visit_id=637611563637058259-4176462731&amp;rd=1) 以取得詳細資訊。

### 允許清單 {#allowlist}

建立之前 [!DNL Google Customer Match] 目的地位於Experience Platform，請確定您的 [!DNL Google Ads] 帳戶符合 [[!DNL Google Customer Match] 原則](https://support.google.com/google-ads/answer/6299717/customer-match-policy).

Google會自動將擁有合規帳戶的客戶加入允許清單。

## ID比對要求 {#id-matching-requirements}

[!DNL Google] 需要未明確傳送任何個人識別資訊(PII)。 因此，啟用的對象 [!DNL Google Customer Match] 必須中斷連線 *雜湊* 識別碼，例如雜湊電子郵件地址或電話號碼。

根據您擷取至Adobe Experience Platform的ID型別，您必須遵守其對應的要求。

### 電話號碼雜湊需求 {#phone-number-hashing-requirements}

啟用電話號碼的方法有兩種 [!DNL Google Customer Match]：

* **擷取原始電話號碼**：您可以將原始電話號碼擷取至 [!DNL E.164] 格式至 [!DNL Platform]，而且會在啟動時自動執行雜湊處理。 如果選擇此選項，請務必將原始電話號碼擷取到 `Phone_E.164` 名稱空間。
* **擷取雜湊電話號碼**：您可以預先雜湊電話號碼，然後再擷取至 [!DNL Platform]. 如果您選取此選項，請務必將雜湊電話號碼擷取至 `PHONE_SHA256_E.164` 名稱空間。

>[!NOTE]
>
>擷取至「 」的電話號碼 `Phone` 名稱空間無法啟用至 [!DNL Google Customer Match + DV360] 目的地。

### 電子郵件雜湊需求 {#hashing-requirements}

您可以將電子郵件地址雜湊再擷取至Adobe Experience Platform，或使用Experience Platform中清楚的電子郵件地址，並擁有 [!DNL Platform] 啟用時雜湊這些專案。

如需Google雜湊需求和其他啟用限制的詳細資訊，請參閱Google檔案中的下列章節：

* [[!DNL Customer Match] 包含電子郵件地址、地址或使用者ID](https://developers.google.com/google-ads/api/docs/remarketing/audience-types/customer-match#customer_match_with_email_address_address_or_user_id)
* [[!DNL Customer Match] 考量事項](https://developers.google.com/google-ads/api/docs/remarketing/audience-types/customer-match#customer_match_considerations)
* [[!DNL Customer Match] 含電話號碼](https://developers.google.com/google-ads/api/docs/remarketing/audience-types/customer-match#customer_match_with_phone_number)
* [[!DNL Customer Match] 使用行動裝置ID](https://developers.google.com/google-ads/api/docs/remarketing/audience-types/customer-match#customer_match_with_mobile_device_ids)


若要瞭解如何在Experience Platform中擷取電子郵件地址，請參閱 [批次擷取概觀](../../../ingestion/batch-ingestion/overview.md) 和 [串流擷取概觀](../../../ingestion/streaming-ingestion/overview.md).

如果您選擇自行雜湊電子郵件地址，請務必遵守Google的要求，如上述連結所述。

<!-- ### Using custom namespaces {#custom-namespaces}

Before you can use the `User_ID` namespace to send data to Google, make sure you synchronize your own identifiers using [!DNL gTag]. Refer to the [Google official documentation](https://support.google.com/google-ads/answer/9199250) for detailed information. -->

<!-- Data from unhashed namespaces is automatically hashed by [!DNL Platform] upon activation.

Attribute source data is not automatically hashed. When your source field contains unhashed attributes, check the **[!UICONTROL Apply transformation]** option, to have [!DNL Platform] automatically hash the data on activation.
![Identity mapping transformation](../../assets/ui/activate-destinations/identity-mapping-transformation.png) -->

<!-- ## Configure destination - video walkthrough {#video}

The video below demonstrates the steps to configure a [!DNL Google Customer Match] destination and activate audiences. The steps are also laid out sequentially in the next sections.

>[!VIDEO](https://video.tv.adobe.com/v/332599/?quality=12&learn=on&captions=eng) -->

## 連線到目標 {#connect}

>[!IMPORTANT]
> 
>若要連線到目的地，您需要 **[!UICONTROL 檢視目的地]** 和 **[!UICONTROL 管理目的地]** [存取控制許可權](/help/access-control/home.md#permissions). 閱讀 [存取控制總覽](/help/access-control/ui/overview.md) 或聯絡您的產品管理員以取得必要許可權。

若要連線至此目的地，請遵循以下說明的步驟： [目的地設定教學課程](../../ui/connect-destination.md).

### 連線參數 {#parameters}

當 [設定](../../ui/connect-destination.md) 您必須提供下列資訊給此目的地：

* **[!UICONTROL 名稱]**：提供此目的地連線的名稱
* **[!UICONTROL 說明]**：提供此目的地連線的說明
* **[!UICONTROL 帳戶ID]**：您的 [Google Ads客戶ID](https://support.google.com/google-ads/answer/1704344?hl=en). ID的格式為xxx-xxx-xxxx。 如果您使用 [!DNL Google Ads Manager Account (My Client Center)]，請勿使用您的經理帳戶ID。 使用 [Google Ads客戶ID](https://support.google.com/google-ads/answer/1704344?hl=en) 而非。
* **[!UICONTROL 帳戶型別]**：您的Google帳戶型別。 根據您在Google中的廣告帳戶型別，選取選項：
   * **[!UICONTROL 顯示視訊合作夥伴]**
   * **[!UICONTROL 顯示視訊廣告商]**

### 啟用警示 {#enable-alerts}

您可以啟用警報以接收有關傳送到您目的地的資料流狀態的通知。 從清單中選取警報以訂閱接收有關資料流狀態的通知。 如需警示的詳細資訊，請參閱以下指南： [使用UI訂閱目的地警報](../../ui/alerts.md).

當您完成提供目的地連線的詳細資訊時，請選取「 」 **[!UICONTROL 下一個]**.

## 啟動此目標的對象 {#activate}

>[!IMPORTANT]
> 
>* 若要啟用資料，您需要 **[!UICONTROL 檢視目的地]**， **[!UICONTROL 啟用目的地]**， **[!UICONTROL 檢視設定檔]**、和 **[!UICONTROL 檢視區段]** [存取控制許可權](/help/access-control/home.md#permissions). 閱讀 [存取控制總覽](/help/access-control/ui/overview.md) 或聯絡您的產品管理員以取得必要許可權。
>* 要匯出 *身分* 若要前往目的地，您需要 **[!UICONTROL 檢視身分圖表]** [存取控制許可權](/help/access-control/home.md#permissions). <br> ![選取工作流程中反白顯示的身分名稱空間，以將對象啟用至目的地。](../../assets/overview/export-identities-to-destination.png "選取工作流程中反白顯示的身分名稱空間，以將對象啟用至目的地。"){width="100" zoomable="yes"}

另請參閱 [啟用受眾資料至串流受眾匯出目的地](../../ui/activate-segment-streaming-destinations.md) 以取得啟用此目的地對象的指示。

<!-- In the **[!UICONTROL Segment schedule]** step, you must provide the [!UICONTROL App ID] when sending [!DNL IDFA] or [!DNL GAID] audiences to [!DNL Google Customer Match].

![Google Customer Match App ID field highlighted in the Segment schedule step of the activation workflow.](../../assets/catalog/advertising/google-customer-match/gcm-destination-appid.png)

For details on how to find the [!DNL App ID], refer to the [Google official documentation](https://developers.google.com/adwords/api/docs/reference/v201809/AdwordsUserListService.CrmBasedUserList#appid) or ask your Google representative. -->

### 對應範例：啟用對象資料於 [!DNL Google Customer Match + Display & Video 360] {#example-gcm}

這是在中啟用對象資料時正確身分對應的範例 [!DNL Google Customer Match + Display & Video 360].

選取來源欄位：

* 選取 `Email` 如果您使用的電子郵件地址未進行雜湊處理，則名稱空間會作為來源身分。
* 選取 `Email_LC_SHA256` 如果您在資料擷取時已將客戶電子郵件地址雜湊至 [!DNL Platform]，根據 [!DNL Google Customer Match] [電子郵件雜湊需求](#hashing-requirements).
* 選取 `PHONE_E.164` 如果資料包含非雜湊電話號碼，則以名稱空間作為來源身分。 [!DNL Platform] 將雜湊電話號碼以符合 [!DNL Google Customer Match] 需求。
* 選取 `Phone_SHA256_E.164` 如果您在資料擷取時已將電話號碼雜湊到 [!DNL Platform]，根據 [!DNL Facebook] [電話號碼雜湊需求](#phone-number-hashing-requirements).

選取目標欄位：

* 選取 `Email_LC_SHA256` 當來源名稱空間為以下任一情況時，將名稱空間作為目標身分 `Email` 或 `Email_LC_SHA256`.
* 選取 `Phone_SHA256_E.164` 當來源名稱空間為以下任一情況時，將名稱空間作為目標身分 `PHONE_E.164` 或 `Phone_SHA256_E.164`.

![在啟動工作流程的「對應」步驟中顯示的來源和目標欄位之間的身分對應。](../../assets/catalog/advertising/google-customer-match-dv360/identity-mapping-gcm-dv360.png)

非雜湊名稱空間中的資料會自動透過雜湊處理 [!DNL Platform] 啟用時。

屬性來源資料不會自動雜湊。 當來源欄位包含未雜湊屬性時，請核取 **[!UICONTROL 套用轉換]** 選項，擁有 [!DNL Platform] 啟動時自動雜湊資料。

![套用啟動工作流程對應步驟中反白顯示的轉換控制項。](../../assets/catalog/advertising/google-customer-match-dv360/transformation.png)

## 驗證對象啟用是否成功 {#verify-activation}

完成啟動流程後，切換至您的 **[!UICONTROL Google Ads]** 帳戶。 啟用的對象會在您的Google帳戶中顯示為客戶清單。 根據您的對象規模，除非有1000多位活躍使用者可服務，否則部分對象不會填入。 欲知更多資訊，請參閱 [Google對象合作夥伴檔案](https://developers.google.com/audience-partner/api/docs/customer-match/get-started#verify-list). 請注意，您需要向Google詢問連結中檔案的存取權。

## 資料控管

Experience Platform中的某些目的地對於傳送到目的地平台或從目的地平台接收的資料具有某些規則和義務。 您有責任瞭解您資料的限制與義務，以及如何在Adobe Experience Platform和目的地平台中使用該資料。 Adobe Experience Platform提供資料治理工具，協助您管理其中一些資料使用義務。 [瞭解更多](../../../data-governance/labels/overview.md) 關於資料控管工具和原則。

## 疑難排解 {#troubleshooting}

### 400錯誤請求錯誤訊息 {#bad-request}

設定此目的地時，您可能會收到下列錯誤：

`{"message":"Google Customer Match Error: OperationAccessDenied.ACTION_NOT_PERMITTED","code":"400 BAD_REQUEST"}`

當客戶帳戶不符合 [必備條件](#google-account-prerequisites). 若要修正此問題，請聯絡Google，確認您的帳戶已加入允許清單並設定為 [!DNL Standard] 或更高許可權層級。 請參閱 [Google Ads檔案](https://support.google.com/google-ads/answer/9978556?visit_id=637611563637058259-4176462731&amp;rd=1) 以取得詳細資訊。
