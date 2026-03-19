---
keywords: 廣告； microsoft ads；客戶符合；
title: Microsoft Ads Customer Match連線
description: 使用Microsoft Ads客戶比對目的地，依電子郵件地址比對客戶，並在Microsoft Advertising網路中與客戶重新互動，包括搜尋和受眾廣告。
badge: label="Beta" type="Informative"
hide: true
hidefromtoc: true
exl-id: 4d405ffb-f600-463b-a215-44e806b6d139
source-git-commit: 2dd4ae4146f7c1c5228e22d24ff2ba31010adedb
workflow-type: tm+mt
source-wordcount: '1347'
ht-degree: 16%

---

# [!DNL Microsoft Ads Customer Match] 連線 {#microsoft-ads-customer-match-destination}

>[!AVAILABILITY]
>
>此目的地聯結器目前可用性有限。 若想取得存取權，請聯絡您的 Adobe 代表。

## 概觀 {#overview}

使用[!DNL Microsoft Ads Customer Match]目的地，依電子郵件地址比對客戶，並在[!DNL Microsoft Advertising Network]中與客戶重新互動，包括搜尋和對象廣告。 將您的[!DNL Microsoft Advertising]帳戶連結至Real-Time CDP，以直接從Experience Platform自動建立和管理客戶比對清單。

## 使用案例 {#use-cases}

為協助您更清楚瞭解如何使用[!DNL Microsoft Ads Customer Match]目的地，以下是Adobe Experience Platform客戶可以使用此功能解決的範例使用案例。

### 使用案例#1 {#use-case-1}

電子商務品牌想要透過[!DNL Microsoft Search]和[!DNL Microsoft Audience Network]觸及現有客戶，以根據客戶過去的購買和瀏覽記錄來個人化優惠方案。 品牌可以從自己的CRM將電子郵件地址擷取到Experience Platform，從自己的離線資料建立對象，並將這些對象傳送到[!DNL Microsoft Ads Customer Match]以用於搜尋和對象廣告，最佳化其廣告支出。

### 使用案例#2 {#use-case-2}

一家技術公司推出了一項新產品。 為了推廣此新產品，他們想要提高先前購買過相關產品的客戶的認知度。 他們使用電子郵件地址作為識別碼，從CRM資料庫上傳電子郵件地址到Experience Platform。 建立受眾是根據擁有相關產品的客戶而定。 這些對象會傳送至[!DNL Microsoft Ads Customer Match]，這樣公司就能鎖定整個[!DNL Microsoft Advertising Network]中的目前客戶和類似客戶。

## 支援的身分 {#supported-identities}

[!DNL Microsoft Ads Customer Match]支援下表所述的身分啟用。 深入瞭解[身分](/help/identity-service/features/namespaces.md)。

| 目標身分 | 說明 | 考量事項 |
|---|---|---|
| `email` | 純文字電子郵件地址 | [!DNL Microsoft Ads Customer Match]連線只支援純文字電子郵件地址。 Experience Platform會在匯出時自動雜湊電子郵件地址，以符合Microsoft的需求。 |

{style="table-layout:auto"}

## 支援的對象 {#supported-audiences}

本節說明您可以將哪些型別的對象匯出至此目的地。

| 對象來源 | 支援 | 說明 |
|---------|----------|----------|
| [!DNL Segmentation Service] | 是 | 透過Experience Platform [細分服務](../../../segmentation/home.md)產生的對象。 |
| 所有其他受眾來源 | 是 | 此類別包含透過[!DNL Segmentation Service]產生的對象以外的所有對象來源。 閱讀[各種對象來源](/help/segmentation/ui/audience-portal.md#customize)。 部分範例包括： <ul><li> 自訂上傳對象[從CSV檔案匯入](../../../segmentation/ui/audience-portal.md#import-audience)至Experience Platform，</li><li> 相似受眾， </li><li> 同盟對象， </li><li> 在其他Experience Platform應用程式（例如Adobe Journey Optimizer）中產生的對象， </li><li> 及更多內容。 </li></ul> |

{style="table-layout:auto"}

依受眾資料型別支援的受眾：

| 對象資料型別 | 支援 | 說明 | 使用案例 |
|--------------------|-----------|-------------|-----------|
| [人員對象](/help/segmentation/types/people-audiences.md) | 是 | 根據客戶設定檔，可讓您針對行銷活動的特定人群進行定位。 | 經常購買者、購物車放棄者 |
| [帳戶對象](/help/segmentation/types/account-audiences.md) | 無 | 針對帳戶型行銷策略，鎖定特定組織內的個人。 | B2B行銷 |
| [潛在客戶對象](/help/segmentation/types/prospect-audiences.md) | 無 | 將目標定位為尚未成為客戶但與目標受眾具有相同特性的個人。 | 使用第三方資料進行勘探 |
| [資料集匯出](/help/catalog/datasets/overview.md) | 無 | 儲存在Adobe Experience Platform Data Lake中的結構化資料集合。 | 報告、資料科學工作流程 |

{style="table-layout:auto"}

## 匯出型別和頻率 {#export-type-frequency}

請參閱下表以取得目的地匯出型別和頻率的資訊。

| 項目 | 類型 | 附註 |
|---------|----------|---------|
| 匯出類型 | **[!UICONTROL Audience export]** | 您正在匯出具有[!DNL Microsoft Ads Customer Match]目的地中所使用識別碼（電子郵件地址）之對象的所有成員。 |
| 匯出頻率 | **[!UICONTROL Streaming]** | 串流目的地是「一律開啟」的API型連線。 根據對象評估在Experience Platform中更新設定檔後，聯結器會立即將更新傳送至下游的目標平台。 深入瞭解[串流目的地](/help/destinations/destination-types.md#streaming-destinations)。 |

{style="table-layout:auto"}

## 先決條件 {#prerequisites}

若要將對象資料傳送至[!DNL Microsoft Ads]，您必須擁有作用中的[!DNL Microsoft Advertising]帳戶。 如需建立帳戶的詳細資訊，請瀏覽[Microsoft Advertising檔案](https://help.ads.microsoft.com/#apex/ads/en/53090/0)。

### 接受客戶比對條款與條件 {#accept-customer-match-terms}

您必須先在您的[!DNL Microsoft Advertising]帳戶中手動建立客戶比對清單，才能透過此目的地啟用對象。 接受客戶比對條款與條件時，需要這種初始手動建立，以便自動建立從Experience Platform傳送的對象。 若未完成此步驟，在啟用對象時可能會導致錯誤。

### 帳戶設定 {#account-configuration}

設定目的地時，您必須提供下列資訊：

* [!UICONTROL Customer ID]：您的[!DNL Microsoft Ads]客戶ID (CID)，使用整數格式。 如需如何尋找客戶ID的說明，請參閱[Microsoft Advertising檔案](https://learn.microsoft.com/zh-tw/advertising/guides/get-started?view=bingads-13#get-ids)。
* [!UICONTROL Customer Account ID]：您的[!DNL Microsoft Ads]客戶帳戶識別碼。 如需如何尋找客戶帳戶ID的說明，請參閱[Microsoft Advertising檔案](https://learn.microsoft.com/zh-tw/advertising/guides/get-started?view=bingads-13#get-ids)。

## 連線到目標 {#connect}

>[!IMPORTANT]
>
>若要連線到目的地，您需要&#x200B;**[!UICONTROL View Destinations]**&#x200B;和&#x200B;**[!UICONTROL Manage Destinations]** [存取控制許可權](/help/access-control/home.md#permissions)。 閱讀[存取控制總覽](/help/access-control/ui/overview.md)或連絡您的產品管理員以取得必要的許可權。

若要連線到此目的地，請依照[目的地組態教學課程](../../ui/connect-destination.md)中所述的步驟進行。

### 填寫目標詳細資訊 {#parameters}

>[!CONTEXTUALHELP]
>id="platform_destinations_microsoft_ads_cm_customer_id"
>title="Customer ID"
>abstract="您的 Microsoft Advertising 客戶 ID，也是管理員帳戶 ID。這是 Microsoft Advertising 中最上層的識別碼，其下可以有多個廣告商帳戶 (客戶帳戶 ID)。"
>additional-url="https://learn.microsoft.com/zh-tw/advertising/guides/get-started?view=bingads-13#get-ids" text="尋找您的客戶 ID"

>[!CONTEXTUALHELP]
>id="platform_destinations_microsoft_ads_cm_customer_account_id"
>title="客戶帳戶 ID"
>abstract="您的 Microsoft Advertising 客戶帳戶 ID，也是廣告商帳戶 ID。您的客戶 ID 下之特定廣告商帳戶以此作為識別。"
>additional-url="https://learn.microsoft.com/zh-tw/advertising/guides/get-started?view=bingads-13#get-ids" text="尋找您的客戶帳戶 ID"

>[!CONTEXTUALHELP]
>id="platform_destinations_microsoft_ads_cm_membership_duration"
>title="會籍有效期限"
>abstract="使用者留存在客戶比對清單中的天數。可接受的值介於 1 至 390 天之間。"

>[!CONTEXTUALHELP]
>id="platform_destinations_microsoft_ads_cm_list_availability"
>title="客戶比對清單可用性"
>abstract="選取客戶比對清單僅供單一廣告商帳戶使用，或是可供管理員帳戶下所有帳戶使用。選取客戶 ID，讓客戶 ID 下的所有廣告商帳戶皆可使用此清單。選取客戶帳戶 ID，僅限特定的客戶帳戶 ID 使用清單。"
>additional-url="https://help.ads.microsoft.com/apex/index/3/zh-tw/56727" text="了解更多關於 Microsoft Advertising 中客群清單共用的資訊"

在[設定](../../ui/connect-destination.md)此目的地時，您必須提供下列資訊：

* **[!UICONTROL Name]**：您日後可辨識此目的地的名稱。
* **[!UICONTROL Description]**：可協助您日後識別此目的地的說明。
* **[!UICONTROL Customer ID]**：您的[!DNL Microsoft Ads]客戶識別碼(CID)。 如需如何尋找客戶ID的說明，請參閱[Microsoft Advertising檔案](https://learn.microsoft.com/zh-tw/advertising/guides/get-started?view=bingads-13#get-ids)。
* **[!UICONTROL Customer Account ID]**：您的[!DNL Microsoft Ads]客戶帳戶識別碼。 如需如何尋找客戶帳戶ID的說明，請參閱[Microsoft Advertising檔案](https://learn.microsoft.com/zh-tw/advertising/guides/get-started?view=bingads-13#get-ids)。
* **[!UICONTROL Membership Duration]**：使用者保留在客戶比對清單中的天數。 可接受的值介於 1 至 390 天之間。
* **[!UICONTROL Customer Match List Availability]**：選取客戶比對清單的可用性。 在[!DNL Microsoft Advertising]中，客戶ID下可以有多個客戶帳戶ID （廣告商帳戶）。 選取&#x200B;**[!UICONTROL Customer ID (all advertising accounts)]**&#x200B;讓您的客戶ID下的所有廣告商帳戶都能使用清單，或選取&#x200B;**[!UICONTROL Customer Account ID (single advertising account)]**&#x200B;將清單限製為您在上方提供的特定客戶帳戶ID。 如需詳細資訊，請參閱[Microsoft Advertising檔案](https://help.ads.microsoft.com/apex/index/3/zh-tw/56727)。

![顯示Microsoft Ads客戶比對目的地之目的地詳細資訊欄位的Platform UI影像。](../../assets/catalog/advertising/microsoft-ads-customer-match/destination-details.png)

### 啟用警示 {#enable-alerts}

您可以啟用警報以接收有關傳送到您目的地的資料流狀態的通知。 從清單中選取警報以訂閱接收有關資料流狀態的通知。 如需警示的詳細資訊，請參閱[使用UI訂閱目的地警示](../../ui/alerts.md)的指南。

當您完成提供目的地連線的詳細資訊時，請選取&#x200B;**[!UICONTROL Next]**。

## 啟動此目標的對象 {#activate}

>[!IMPORTANT]
>
>* 若要啟用資料，您需要&#x200B;**[!UICONTROL View Destinations]**、**[!UICONTROL Activate Destinations]**、**[!UICONTROL View Profiles]**&#x200B;和&#x200B;**[!UICONTROL View Segments]** [存取控制許可權](/help/access-control/home.md#permissions)。 閱讀[存取控制總覽](/help/access-control/ui/overview.md)或連絡您的產品管理員以取得必要的許可權。
>* 若要將&#x200B;*身分*&#x200B;匯出至目的地，您需要&#x200B;**[!UICONTROL View Identity Graph]** [存取控制許可權](/help/access-control/home.md#permissions)。<br> ![選取工作流程中反白的身分名稱空間，以啟用目的地的對象。](/help/destinations/assets/overview/export-identities-to-destination.png "選取工作流程中反白顯示的身分名稱空間，以啟用目的地的對象。"){width="100" zoomable="yes"}

如需啟用此目的地的對象的指示，請參閱[啟用串流對象匯出目的地的對象資料](../../ui/activate-segment-streaming-destinations.md)。

### 對應 {#mapping}

在&#x200B;**[!UICONTROL Mapping]**&#x200B;步驟中，您必須將來源設定檔中的電子郵件識別對應到[!DNL Microsoft Ads Customer Match]中的目標識別。

* **Source欄位**：選取`IdentityMap: Email`作為來源欄位，以從您的設定檔對應電子郵件身分識別。 或者，您可以選取XDM屬性（例如`personalEmail.address`）作為來源欄位。
* **目標欄位**：選取`Identity: email`作為目標欄位。

>[!IMPORTANT]
>
>您必須使用非雜湊（純文字）來源欄位。 請勿使用預先雜湊的來源身分識別，例如`Emails (SHA256, lowercased)`。 Experience Platform會在匯出時自動雜湊電子郵件地址，以符合Microsoft的需求。

![顯示對應步驟的UI影像，其中IdentityMap電子郵件對應至身分識別電子郵件。](../../assets/catalog/advertising/microsoft-ads-customer-match/mapping.png)

## 匯出的資料 {#exported-data}

若要確認資料是否已成功匯出至[!DNL Microsoft Ads Customer Match]目的地，請檢查您的[!DNL Microsoft Advertising]帳戶。 如果成功啟用，系統會將對象填入您的帳戶作為客戶比對清單。

## 其他資源 {#additional-resources}

如需詳細資訊，請參閱[Microsoft Advertising說明中心](https://help.ads.microsoft.com/)。
