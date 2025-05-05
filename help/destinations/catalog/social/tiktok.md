---
title: TikTok連線
description: 使用您的資料在TikTok上建立自訂對象，以便透過廣告促銷活動進行目標定位。 這些對象可能是造訪過您的網站或與您的內容互動的人。 使用Adobe與TikTok Ads Manager的即時整合，快速安全地將所需的對象從Adobe Experience Platform推送到TikTok。
last-substantial-update: 2023-03-20T00:00:00Z
exl-id: 7b12d17f-7d9a-4615-9830-92bffe3f6927
source-git-commit: fded2f25f76e396cd49702431fa40e8e4521ebf8
workflow-type: tm+mt
source-wordcount: '1079'
ht-degree: 3%

---

# TikTok連線

## 概觀 {#overview}

使用您的資料在TikTok上建立自訂對象，以便透過廣告促銷活動進行目標定位。 這些對象可能是造訪過您的網站或與您的內容互動的人。 使用Adobe與TikTok Ads Manager的即時整合，快速安全地將所需的對象從Adobe Experience Platform推送到TikTok。 如需詳細資訊，請造訪[TikTok的商務說明中心](https://ads.tiktok.com/help/article/audiences)。

>[!IMPORTANT]
>
>此目的地聯結器和檔案頁面是由TikTok團隊建立和維護的。 若有任何查詢或更新要求，請直接透過[https://ads.tiktok.com/help/](https://ads.tiktok.com/help/)聯絡他們。

## 使用案例 {#use-cases}

為協助您更清楚瞭解如何使用TikTok目的地，以下是Adobe Experience Platform客戶的範例使用案例。

### 使用實例 {#use-case-1}

運動服裝品牌想要透過其社群媒體帳戶觸及現有客戶。 服飾品牌可以從他們自己的CRM擷取電子郵件地址到Adobe Experience Platform，從他們自己的離線資料建立對象，並將這些對象傳送到TikTok以在其客戶的社群媒體摘要中顯示廣告。

## 先決條件 {#prerequisites}

您必須擁有[!DNL Admin]或[!DNL Operator]許可權，才能存取您要傳送對象的TikTok Ads Manager帳戶。 如需更多說明，請參閱[TikTok說明中心](https://ads.tiktok.com/help/article/add-users-tiktok-business-center)。

在將資料傳送至您的TikTok Ads Manager帳戶之前，您需要授予Adobe Experience Platform許可權以存取`Audience Management`的廣告帳戶。 在Experience Platform使用者介面中輸入您的廣告管理員ID[&#128279;](#authenticate)，並在重新導向至您的TikTok廣告管理員帳戶後授與許可權，即可提供此許可權。

## 支援的身分 {#supported-identities}

TikTok支援下表所述的身分啟用。 深入瞭解[身分](/help/identity-service/features/namespaces.md)。

| 目標身分 | 說明 | 考量事項 |
|---|---|---|
| GAID | GOOGLE ADVERTISING ID | 當您的來源身分是GAID名稱空間時，請選取GAID目標身分。 |
| IDFA | 廣告商適用的Apple ID | 當您的來源身分是IDFA名稱空間時，請選取IDFA目標身分。 |
| 電話號碼 | 使用SHA256演演算法雜湊的電話號碼 | Adobe Experience Platform支援純文字和SHA256雜湊電話號碼，且必須採用E.164格式。 當您的來源欄位包含未雜湊的屬性時，請核取&#x200B;**[!UICONTROL 套用轉換]**&#x200B;選項，讓[!DNL Experience Platform]在啟用時自動雜湊資料。 |
| 電子郵件 | 使用SHA256演演算法雜湊的電子郵件地址 | Adobe Experience Platform同時支援純文字和SHA256雜湊電子郵件地址。 當您的來源欄位包含未雜湊的屬性時，請核取&#x200B;**[!UICONTROL 套用轉換]**&#x200B;選項，讓[!DNL Experience Platform]在啟用時自動雜湊資料。 |

{style="table-layout:auto"}

## 支援的對象 {#supported-audiences}

本節說明您可以將哪些型別的對象匯出至此目的地。

| 對象來源 | 支援 | 說明 |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | 透過Experience Platform [細分服務](../../../segmentation/home.md)產生的對象。 |
| 自訂上傳 | ✓ | 對象[從CSV檔案匯入](../../../segmentation/ui/audience-portal.md#import-audience)至Experience Platform。 |
| [!DNL Federated Audience Composition] | ✓ | 透過[同盟對象構成](https://experienceleague.adobe.com/zh-hant/docs/federated-audience-composition/using/start/audiences)匯入到Experience Platform中的對象。 |

{style="table-layout:auto"}

## 匯出型別和頻率 {#export-type-frequency}

請參閱下表以取得目的地匯出型別和頻率的資訊。

| 項目 | 類型 | 附註 |
---------|----------|---------|
| 匯出類型 | **[!UICONTROL 對象匯出]** | 您正在匯出具有TikTok目的地所使用識別碼（名稱、電話號碼或其他）的對象所有成員。 |
| 匯出頻率 | **[!UICONTROL 串流]** | 串流目的地是「一律開啟」的API型連線。 根據對象評估在Experience Platform中更新設定檔後，聯結器會立即將更新傳送至下游的目標平台。 深入瞭解[串流目的地](/help/destinations/destination-types.md#streaming-destinations)。 |

{style="table-layout:auto"}

## 連線到目標 {#connect}

>[!IMPORTANT]
> 
>若要連線到目的地，您需要&#x200B;**[!UICONTROL 檢視目的地]**&#x200B;和&#x200B;**[!UICONTROL 管理目的地]** [存取控制許可權](/help/access-control/home.md#permissions)。 閱讀[存取控制總覽](/help/access-control/ui/overview.md)或連絡您的產品管理員以取得必要的許可權。

若要連線到此目的地，請依照[目的地組態教學課程](../../ui/connect-destination.md)中所述的步驟進行。 在設定目標工作流程中，填寫以下兩個區段中列出的欄位。

### 驗證目標 {#authenticate}

若要驗證到目的地，系統會將您重新導向以登入您的[!DNL TikTok Ads Manager]帳戶，並授權Adobe代表您管理對象。

![TikTok許可權選取專案](/help/destinations/assets/catalog/social/tiktok/tiktok-authenticate-destination.png "用於選取許可權的TikTok UI影像")

### 填寫目標詳細資訊 {#destination-details}

若要設定目的地的詳細資訊，請填寫下方的必填和選用欄位。 UI中欄位旁的星號表示該欄位為必填欄位。

![目的地連線詳細資料](/help/destinations/assets/catalog/social/tiktok/tiktok-configure-destination-details.png "Experience Platform UI的影像，顯示要填寫的目的地連線詳細資料")

* **[!UICONTROL 名稱]**：您日後可辨識此目的地的名稱。
* **[!UICONTROL 描述]**：可協助您日後識別此目的地的描述。
* **[!UICONTROL TikTok廣告管理員ID]**：您的[!DNL TikTok Ads Manager ID]。 您可以在[!DNL TikTok Ads manager]帳戶中找到此專案。

![TikTok Ads Manager ID](/help/destinations/assets/catalog/social/tiktok/tiktok-ads-manager-ID.png "TikTok Ads Manager UI的影像，顯示如何取得TikTok Ads Manager ID")

### 啟用警示 {#enable-alerts}

您可以啟用警報以接收有關傳送到您目的地的資料流狀態的通知。 從清單中選取警報以訂閱接收有關資料流狀態的通知。 如需警示的詳細資訊，請參閱[使用UI訂閱目的地警示](../../ui/alerts.md)的指南。

當您完成提供目的地連線的詳細資訊後，請選取&#x200B;**[!UICONTROL 下一步]**。

## 啟動此目標的對象 {#activate}

>[!IMPORTANT]
> 
>* 若要啟用資料，您需要&#x200B;**[!UICONTROL 檢視目的地]**、**[!UICONTROL 啟用目的地]**、**[!UICONTROL 檢視設定檔]**&#x200B;和&#x200B;**[!UICONTROL 檢視區段]** [存取控制許可權](/help/access-control/home.md#permissions)。 閱讀[存取控制總覽](/help/access-control/ui/overview.md)或連絡您的產品管理員以取得必要的許可權。
>* 若要匯出&#x200B;*身分*，您需要&#x200B;**[!UICONTROL 檢視身分圖表]** [存取控制許可權](/help/access-control/home.md#permissions)。<br> ![選取工作流程中反白的身分名稱空間，以啟用目的地的對象。](/help/destinations/assets/overview/export-identities-to-destination.png "選取工作流程中反白顯示的身分名稱空間，以啟用目的地的對象。"){width="100" zoomable="yes"}

閱讀[將設定檔和對象啟用至串流對象匯出目的地](/help/destinations/ui/activate-segment-streaming-destinations.md)，以瞭解啟用此目的地對象的指示。

### 對應身分識別 {#map}

以下是將對象匯出至TikTok Ads Manager時的正確身分對應範例。

選取來源欄位：

* 選取識別碼（例如：` Email_LC_SHA256`）作為來源識別碼，以唯一識別Adobe Experience Platform和[!DNL TikTok Ads Manager]中的設定檔。

選取目標欄位：

* 選取電子郵件名稱空間作為目標身分。

![身分對應](/help/destinations/assets/catalog/social/tiktok/tiktok-map-identity.png "Experience Platform UI的影像，身分對應")

## 匯出的資料 {#exported-data}

檢查您的[!DNL TikTok Ads Manager]帳戶(位於「**Assets >對象**」下)，確認您的Experience Platform對象是否已成功匯出。 對象將會填入為對象型別： `Partner Audience`。

## 資料使用與控管 {#data-usage-governance}

處理您的資料時，所有[!DNL Adobe Experience Platform]目的地都符合資料使用原則。 如需[!DNL Adobe Experience Platform]如何強制資料控管的詳細資訊，請閱讀[資料控管概觀](/help/data-governance/home.md)。

## 其他資源 {#additional-resources}

如需詳細資訊，請參閱[TikTok說明中心頁面](https://ads.tiktok.com/help/article/audiences)。
