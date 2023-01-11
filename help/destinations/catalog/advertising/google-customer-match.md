---
keywords: google客戶比對；Google客戶比對；Google客戶比對
title: Google Customer Match連線
description: Google Customer Match可讓您使用您的線上和離線資料，在Google擁有且運作的屬性(例如Search、Shopping、Gmail和YouTube)中觸及客戶並與其重新互動。
exl-id: 8209b5eb-b05c-4ef7-9fdc-22a528d5f020
source-git-commit: d6b34f3bd3a432e1cf7d3dcce242934391b65d78
workflow-type: tm+mt
source-wordcount: '1769'
ht-degree: 1%

---

# [!DNL Google Customer Match] 連接

## 總覽 {#overview}

[[!DNL Google Customer Match]](https://support.google.com/google-ads/answer/6379332?hl=en) 可讓您使用線上和離線資料，觸及Google擁有且運作的屬性中的客戶，並與其重新互動，例如： [!DNL Search], [!DNL Shopping], [!DNL Gmail]，和 [!DNL YouTube].

![GoogleAdobe Experience Platform UI中的客戶比對目的地。](../../assets/catalog/advertising/google-customer-match/catalog.png)

## 使用案例 {#use-cases}

協助您更清楚了解如何及何時使用 [!DNL Google Customer Match] 目的地，以下是Adobe Experience Platform客戶可透過此功能解決的範例使用案例。

### 使用案例#1

運動服裝品牌希望通過 [!DNL Google Search] 和 [!DNL Google Shopping] 以根據其過去的購買和瀏覽記錄來個人化選件和項目。 服飾品牌可從自己的CRM擷取電子郵件地址至Experience Platform，並從自己的離線資料建立區段。 接著，他們可將這些區段傳送至 [!DNL Google Customer Match] 用於 [!DNL Search] 和 [!DNL Shopping]，最佳化其廣告支出。

### 使用案例#2

一家知名科技公司推出了一款新手機。 為了推廣這種新手機型號，他們希望讓擁有舊款手機的客戶了解這款手機的新功能。

為了促銷此版本，他們使用電子郵件地址做為識別碼，從其CRM資料庫上傳電子郵件地址至Experience Platform。 會根據擁有舊款手機型號的客戶來建立區段。 然後區段會傳送至 [!DNL Google Customer Match]，因此公司可以鎖定目前的客戶、擁有舊款手機型號的客戶，以及 [!DNL YouTube].

## 適用於 [!DNL Google Customer Match] 目的地 {#data-governance}

Experience Platform中的某些目的地對於傳送至目的地平台或從目的地平台接收的資料，有特定的規則和義務。 您有責任了解資料的限制和義務，以及如何在Adobe Experience Platform和目的地平台中使用該資料。 Adobe Experience Platform提供資料控管工具，可協助您管理其中部分資料使用義務。 [深入了解](../../../data-governance/labels/overview.md) 關於資料控管工具和原則。

## 支援的身分 {#supported-identities}

[!DNL Google Customer Match] 支援啟用下表所述的身分。 深入了解 [身分](/help/identity-service/namespaces.md).

| Target身分 | 說明 | 考量事項 |
|---|---|---|
| GAID | Google Advertising ID | 當源標識為GAID命名空間時，選擇此目標標識。 |
| IDFA | Apple ID for Advertisers | 當您的來源識別為IDFA命名空間時，請選取此目標識別。 |
| phone_sha256_e.164 | E164格式的電話號碼，使用SHA256演算法雜湊 | Adobe Experience Platform支援純文字和SHA256雜湊電話號碼。 遵循 [ID比對需求](#id-matching-requirements-id-matching-requirements) 區段，並分別使用純文字和雜湊電話號碼的適當命名空間。 當來源欄位包含未雜湊屬性時，請檢查 **[!UICONTROL 套用轉換]** 選項，必須 [!DNL Platform] 啟動時自動雜湊資料。 |
| email_lc_sha256 | 使用SHA256演算法雜湊的電子郵件地址 | Adobe Experience Platform支援純文字和SHA256雜湊電子郵件地址。 遵循 [ID比對需求](#id-matching-requirements-id-matching-requirements) 區段，並分別使用純文字和雜湊電子郵件地址的適當命名空間。 當來源欄位包含未雜湊屬性時，請檢查 **[!UICONTROL 套用轉換]** 選項，必須 [!DNL Platform] 啟動時自動雜湊資料。 |
| user_id | 自訂使用者ID | 當源標識為自定義命名空間時，選擇此目標標識。 |

{style=&quot;table-layout:auto&quot;}

## 匯出類型和頻率 {#export-type-frequency}

有關目標導出類型和頻率的資訊，請參閱下表。

| 項目 | 類型 | 附註 |
---------|----------|---------|
| 匯出類型 | **[!UICONTROL 區段匯出]** | 您正在匯出區段（對象）的所有成員，其中包含 [!DNL Google Customer Match] 目的地。 |
| 匯出頻率 | **[!UICONTROL 串流]** | 串流目的地是「一律開啟」API型連線。 一旦根據區段評估在Experience Platform中更新設定檔，連接器就會將更新傳送至下游的目的地平台。 深入了解 [串流目的地](/help/destinations/destination-types.md#streaming-destinations). |

{style=&quot;table-layout:auto&quot;}

## [!DNL Google Customer Match] 帳戶必要條件 {#google-account-prerequisites}

設定之前 [!DNL Google Customer Match] Experience Platform中的目的地，請務必閱讀並遵循Google的使用政策 [!DNL Customer Match]，於 [Google支援檔案](https://support.google.com/google-ads/answer/6299717).

接下來，請確定 [!DNL Google] 帳戶已設定為 [!DNL Standard] 或更高的權限級別。 請參閱 [Google Ads檔案](https://support.google.com/google-ads/answer/9978556?visit_id=637611563637058259-4176462731&amp;rd=1) 以取得詳細資訊。

### 允許清單 {#allowlist}

建立之前 [!DNL Google Customer Match] 目的地Experience Platform中，請確定您的 [!DNL Google Ads] 帳戶符合 [[!DNL Google Customer Match] 原則](https://support.google.com/google-ads/answer/6299717/customer-match-policy).

符合帳戶的客戶會自動獲得Google的允許。

## ID比對需求 {#id-matching-requirements}

[!DNL Google] 需要清楚傳送任何個人識別資訊(PII)。 因此，對象已啟動至 [!DNL Google Customer Match] 可以砍掉 *雜湊* 識別碼，例如電子郵件地址或電話號碼。

視您擷取至Adobe Experience Platform的ID類型而定，您必須遵守其對應要求。

### 電話號碼雜湊要求 {#phone-number-hashing-requirements}

在中啟用電話號碼的方法有兩種 [!DNL Google Customer Match]:

* **擷取原始電話號碼**:您可以在 [!DNL E.164] 格式 [!DNL Platform]，而且在啟動時會自動雜湊。 如果您選擇此選項，請務必一律將原始電話號碼內嵌至 `Phone_E.164` 命名空間。
* **擷取雜湊電話號碼**:您可以先預先雜湊電話號碼，再擷取至 [!DNL Platform]. 如果您選擇此選項，請務必一律將雜湊電話號碼內嵌至 `PHONE_SHA256_E.164` 命名空間。

>[!NOTE]
>
>擷取到 `Phone` 命名空間無法在中啟用 [!DNL Google Customer Match].

### 電子郵件雜湊要求 {#hashing-requirements}

您可以先雜湊電子郵件地址再將其擷取至Adobe Experience Platform，或在Experience Platform中清除使用電子郵件地址，並 [!DNL Platform] 激活時將其哈希。

如需Google雜湊要求和其他啟用限制的詳細資訊，請參閱Google檔案中的下列章節：

* [[!DNL Customer Match] 包含電子郵件地址、地址或使用者ID](https://developers.google.com/google-ads/api/docs/remarketing/audience-types/customer-match#customer_match_with_email_address_address_or_user_id)
* [[!DNL Customer Match] 考量事項](https://developers.google.com/google-ads/api/docs/remarketing/audience-types/customer-match#customer_match_considerations)
* [[!DNL Customer Match] 使用電話號碼](https://developers.google.com/google-ads/api/docs/remarketing/audience-types/customer-match#customer_match_with_phone_number)
* [[!DNL Customer Match] 使用行動裝置ID](https://developers.google.com/google-ads/api/docs/remarketing/audience-types/customer-match#customer_match_with_mobile_device_ids)


若要了解如何在Experience Platform中擷取電子郵件地址，請參閱 [批次匯入概觀](../../../ingestion/batch-ingestion/overview.md) 和 [串流獲取概觀](../../../ingestion/streaming-ingestion/overview.md).

如果您選取自行雜湊電子郵件地址，請務必遵守上述連結中概述的Google要求。

### 使用自訂命名空間 {#custom-namespaces}

您可以使用 `User_ID` 將資料傳送至Google的命名空間，請務必使用 [!DNL gTag]. 請參閱 [Google官方檔案](https://support.google.com/google-ads/answer/9199250) 以取得詳細資訊。

<!-- Data from unhashed namespaces is automatically hashed by [!DNL Platform] upon activation.

Attribute source data is not automatically hashed. When your source field contains unhashed attributes, check the **[!UICONTROL Apply transformation]** option, to have [!DNL Platform] automatically hash the data on activation.
![Identity mapping transformation](../../assets/ui/activate-destinations/identity-mapping-transformation.png) -->

<!-- ## Configure destination - video walkthrough {#video}

The video below demonstrates the steps to configure a [!DNL Google Customer Match] destination and activate segments. The steps are also laid out sequentially in the next sections.

>[!VIDEO](https://video.tv.adobe.com/v/332599/?quality=12&learn=on&captions=eng) -->

## 連接到目標 {#connect}

>[!IMPORTANT]
> 
>若要連線至目的地，您需要 **[!UICONTROL 管理目的地]** [存取控制權限](/help/access-control/home.md#permissions). 閱讀 [存取控制概觀](/help/access-control/ui/overview.md) 或聯絡您的產品管理員以取得所需的權限。

若要連線至此目的地，請依照 [目的地設定教學課程](../../ui/connect-destination.md).

### 連線參數 {#parameters}

同時 [設定](../../ui/connect-destination.md) 此目的地時，您必須提供下列資訊：

* **[!UICONTROL 名稱]**:提供此目標連接的名稱
* **[!UICONTROL 說明]**:提供此目標連接的說明
* **[!UICONTROL 帳戶ID]**:您的 [Google Ads客戶ID](https://support.google.com/google-ads/answer/1704344?hl=en). ID的格式為xxx-xxx-xxxx。 如果您使用 [!DNL Google Ads Manager Account (My Client Center)]，請勿使用您的Manager帳戶ID。 使用 [Google Ads客戶ID](https://support.google.com/google-ads/answer/1704344?hl=en) 。

>[!IMPORTANT]
>
> * 此 **[!UICONTROL 與PII結合]** 預設會選取 [!DNL Google Customer Match] 目標和無法移除。


### 啟用警報 {#enable-alerts}

您可以啟用警報，接收有關資料流到目標狀態的通知。 從清單中選擇要訂閱的警報，以接收有關資料流狀態的通知。 如需警報的詳細資訊，請參閱 [使用UI訂閱目的地警報](../../ui/alerts.md).

完成提供目標連接的詳細資訊後，請選擇 **[!UICONTROL 下一個]**.

## 啟用此目的地的區段 {#activate}

>[!IMPORTANT]
> 
>若要啟用資料，您需要 **[!UICONTROL 管理目的地]**, **[!UICONTROL 啟動目的地]**, **[!UICONTROL 檢視設定檔]**，和 **[!UICONTROL 檢視區段]** [存取控制權限](/help/access-control/home.md#permissions). 閱讀 [存取控制概觀](/help/access-control/ui/overview.md) 或聯絡您的產品管理員以取得所需的權限。

請參閱 [對串流區段匯出目的地啟用受眾資料](../../ui/activate-segment-streaming-destinations.md) 以取得啟用受眾區段至此目的地的指示。

在 **[!UICONTROL 區段排程]** 步驟，您必須提供 [!UICONTROL 應用程式ID] 傳送 [!DNL IDFA] 或 [!DNL GAID] 區段至 [!DNL Google Customer Match].

![Google Customer Match應用程式ID](../../assets/catalog/advertising/google-customer-match/gcm-destination-appid.png)

如需如何尋找 [!DNL App ID]，請參閱 [Google官方檔案](https://developers.google.com/adwords/api/docs/reference/v201809/AdwordsUserListService.CrmBasedUserList#appid).

### 對應範例：在 [!DNL Google Customer Match] {#example-gcm}

以下是在中啟用受眾資料時，正確身分對應的範例 [!DNL Google Customer Match].

選擇源欄位：

* 選取 `Email` 如果您使用的電子郵件地址未雜湊，則命名空間作為來源身分。
* 選取 `Email_LC_SHA256` 如果您在將資料匯入至時雜湊客戶電子郵件地址，則命名空間設為來源身分 [!DNL Platform]，根據 [!DNL Google Customer Match] [電子郵件雜湊要求](#hashing-requirements).
* 選取 `PHONE_E.164` 命名空間作為來源識別（如果您的資料包含非雜湊電話號碼）。 [!DNL Platform] 會雜湊電話號碼以符合 [!DNL Google Customer Match] 需求。
* 選取 `Phone_SHA256_E.164` 將命名空間作為來源識別(如果您在資料擷取時將電話號碼雜湊至 [!DNL Platform]，根據 [!DNL Facebook] [電話號碼雜湊要求](#phone-number-hashing-requirements).
* 選取 `IDFA` 命名空間作為來源識別（如果您的資料包含） [!DNL Apple] 裝置ID。
* 選取 `GAID` 命名空間作為來源識別（如果您的資料包含） [!DNL Android] 裝置ID。
* 選取 `Custom` 命名空間作為來源識別（如果您的資料包含其他類型的識別碼）。

選擇目標欄位：

* 選取 `Email_LC_SHA256` 命名空間作為目標識別(當您的來源命名空間為 `Email` 或 `Email_LC_SHA256`.
* 選取 `Phone_SHA256_E.164` 命名空間作為目標識別(當您的來源命名空間為 `PHONE_E.164` 或 `Phone_SHA256_E.164`.
* 選取 `IDFA` 或 `GAID` 來源命名空間時，命名空間會設為目標身分識別 `IDFA` 或 `GAID`.
* 選取 `User_ID` 當您的來源命名空間為自訂命名空間時，命名空間做為目標身分。

![身分對應](../../assets/ui/activate-segment-streaming-destinations/identity-mapping-gcm.png)

來自未雜湊命名空間的資料會由 [!DNL Platform] 啟動後。

屬性來源資料不會自動雜湊。 當來源欄位包含未雜湊屬性時，請檢查 **[!UICONTROL 套用轉換]** 選項，必須 [!DNL Platform] 啟動時自動雜湊資料。

![身分對應轉換](../../assets/ui/activate-segment-streaming-destinations/identity-mapping-gcm-transformation.png)

## 確認區段啟動成功 {#verify-activation}

完成啟動流程後，切換至 **[!UICONTROL Google Ads]** 帳戶。 已啟動的區段會在您的Google帳戶中顯示為客戶清單。 請注意，除非有超過100個使用中使用者提供服務，否則不會填入部分對象（視您的區段大小而定）。

將區段對應至兩者時 [!DNL IDFA] 和 [!DNL GAID] 行動ID、 [!DNL Google Customer Match] 會為每個ID對應建立個別的區段。 您的 [!DNL Google Ads] 帳戶會顯示兩個不同的區段，其中一個 [!DNL IDFA]，和一個 [!DNL GAID] 對應。

## 疑難排解 {#troubleshooting}

### 400錯誤請求錯誤消息 {#bad-request}

設定此目的地時，您可能會收到下列錯誤：

`{"message":"Google Customer Match Error: OperationAccessDenied.ACTION_NOT_PERMITTED","code":"400 BAD_REQUEST"}`

當客戶帳戶不符合 [必要條件](#google-account-prerequisites). 若要修正此問題，請連絡Google，並確認您的帳戶已列入允許清單，且已設定 [!DNL Standard] 或更高的權限級別。 請參閱 [Google Ads檔案](https://support.google.com/google-ads/answer/9978556?visit_id=637611563637058259-4176462731&amp;rd=1) 以取得詳細資訊。

## 其他資源 {#additional-resources}

* [整合 [!DNL Google Customer Match]  — 教學課程影片](https://experienceleague.adobe.com/docs/platform-learn/tutorials/rtcdp/integrate-with-google-customer-match.html)

