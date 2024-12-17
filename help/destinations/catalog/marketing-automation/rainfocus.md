---
title: RainFocus與會者設定檔
description: 瞭解如何使用RainFocus與會者設定檔目的地聯結器，將受眾設定檔與RainFocus全域與會者設定檔同步。
last-substantial-update: 2024-12-17T00:00:00Z
source-git-commit: a3dcf49d3ed9afacd3ffef10d6f280c71ebdf584
workflow-type: tm+mt
source-wordcount: '1000'
ht-degree: 2%

---


# RainFocus與會者設定檔 {#rainfocus-destination}

## 概觀 {#overview}

使用[!DNL RainFocus Attendee Profiles]目的地將客戶設定檔從Adobe Experience Platform串流到[!DNL RainFocus]平台，以建立和更新出席者設定檔。

>[!IMPORTANT]
>
>目的地聯結器和檔案頁面是由[!DNL RainFocus]團隊建立和維護的。 若有任何查詢或更新要求，請直接透過`clientcare@rainfocus.com`聯絡或造訪RainFocus [說明中心](https://help.rainfocus.com/hc/en-us)。

## 使用案例 {#use-cases}

為協助您更清楚瞭解如何使用RainFocus目的地，以下是Adobe Experience Platform客戶可使用此目的地解決的範例使用案例。

### 使用案例#1 {#use-case-1}

一家大型企業技術公司即將開放註冊參加即將舉辦的全球博覽會，並且想要將客戶設定檔推送到[!DNL RainFocus]，以簡化註冊程式。

### 使用案例#2 {#use-case-2}

金融服務品牌即將舉辦一系列以新客戶和現有客戶為目標的路演。 他們與Adobe Experience Platform中的目標客戶有一系列受眾區段。 使用[!DNL RainFocus]目的地聯結器，他們就能輕鬆傳送這些設定檔至[!DNL RainFocus]以進行啟用。

## 先決條件 {#prerequisites}

使用[!DNL RainFocus]目的地之前，請務必符合下列必要條件：

* 使用OAuth （全域）建立[!DNL RainFocus] API設定檔。
   * 必須啟用&#x200B;**出席者存放區**&#x200B;端點。
   * 需要產生&#x200B;**使用者端識別碼**&#x200B;和&#x200B;**使用者端密碼**。

您也必須有RainFocus **事件代碼**&#x200B;識別碼，您想要將設定檔傳送至此識別碼。

## 支援的身分 {#supported-identities}

[!DNL RainFocus]支援下表所述的身分啟用。 深入瞭解[身分](/help/identity-service/features/namespaces.md)。

| 目標身分 | 說明 | 考量事項 |
|---|---|---|
| email_lc_sha256 | 使用SHA256演演算法雜湊的電子郵件地址 | Adobe Experience Platform同時支援純文字和SHA256雜湊電子郵件地址。 當您的來源欄位包含未雜湊的屬性時，請核取&#x200B;**[!UICONTROL 套用轉換]**&#x200B;選項，讓[!DNL Platform]在啟用時自動雜湊資料。 |

{style="table-layout:auto"}

## 支援的對象 {#supported-audiences}

本節說明您可以將哪些型別的對象匯出至此目的地。

| 對象來源 | 支援 | 說明 |
---------|----------|----------|
| [!DNL Segmentation Service] | ✓ (A) | 透過Experience Platform[細分服務](../../../segmentation/home.md)產生的對象。 |
| 自訂上傳 | ✓ (A) | 對象[從CSV檔案匯入](../../../segmentation/ui/overview.md#import-audience)至Experience Platform。 |

{style="table-layout:auto"}

## 匯出型別和頻率 {#export-type-frequency}

請參閱下表以取得目的地匯出型別和頻率的資訊。

| 項目 | 類型 | 附註 |
---------|----------|---------|
| 匯出類型 | **[!UICONTROL 以設定檔為基礎]** | 您正在匯出區段的所有成員，以及所需的結構描述欄位（例如：電子郵件地址、電話號碼、姓氏），如[目的地啟用工作流程](/help/destinations/ui/activate-batch-profile-destinations.md#select-attributes)的選取設定檔屬性畫面中所選。 |
| 匯出頻率 | **[!UICONTROL 串流]** | 串流目的地是「一律開啟」的API型連線。 一旦根據區段評估在Experience Platform中更新了設定檔，聯結器就會將更新傳送至下游的目標平台。 深入瞭解[串流目的地](/help/destinations/destination-types.md#streaming-destinations)。 |

{style="table-layout:auto"}

## 連線到目標 {#connect}

>[!IMPORTANT]
> 
>若要連線到目的地，您需要&#x200B;**[!UICONTROL 檢視目的地]**&#x200B;和&#x200B;**[!UICONTROL 管理目的地]** [存取控制許可權](/help/access-control/home.md#permissions)。 閱讀[存取控制總覽](/help/access-control/ui/overview.md)或連絡您的產品管理員以取得必要的許可權。

若要連線到此目的地，請依照[目的地組態教學課程](../../ui/connect-destination.md)中所述的步驟進行。 在設定目標工作流程中，填寫以下兩個區段中列出的欄位。

### 驗證目標 {#authenticate}

若要驗證到目的地，請填入必填欄位，然後選取&#x200B;**[!UICONTROL 連線到目的地]**。

![提供RainFocus目的地聯結器的驗證詳細資料](/help/destinations/assets/catalog/marketing-automation/rainfocus/rainfocus-destination-authentication.png)

* **[!UICONTROL 使用者端識別碼]**：填入RainFocus API設定檔提供的[!DNL Client ID]。
* **[!UICONTROL 使用者端密碼]**：填入RainFocus API設定檔提供的[!DNL Client Secret]。
* **[!UICONTROL 環境]**：指定您要連線至哪個RainFocus環境，例如`dev`、`prod`。
* **[!UICONTROL 組織ID]**：為您的RainFocus執行個體提供唯一的`orgid`。

### 填寫目標詳細資訊 {#destination-details}

若要設定目的地的詳細資訊，請填寫下方的必填和選用欄位。 UI中欄位旁的星號表示該欄位為必填欄位。

![提供RainFocus目的地聯結器的連線詳細資料](/help/destinations/assets/catalog/marketing-automation/rainfocus/rainfocus-configure-destination-details.png)

* **[!UICONTROL 名稱]**：您日後可辨識此目的地的名稱。
* **[!UICONTROL 描述]**：可協助您日後識別此目的地的描述。
* **[!UICONTROL 事件識別碼]**：您的[!DNL RainFocus]事件代碼識別碼，您想要將設定檔傳送至該識別碼。

### 啟用警示 {#enable-alerts}

您可以啟用警報以接收有關傳送到您目的地的資料流狀態的通知。 從清單中選取警報以訂閱接收有關資料流狀態的通知。 如需警示的詳細資訊，請參閱[使用UI訂閱目的地警示](../../ui/alerts.md)的指南。

當您完成提供目的地連線的詳細資訊後，請選取&#x200B;**[!UICONTROL 下一步]**。

## 啟用此目的地的區段 {#activate}

>[!IMPORTANT]
> 
>* 若要啟用資料，您需要&#x200B;**[!UICONTROL 檢視目的地]**、**[!UICONTROL 啟用目的地]**、**[!UICONTROL 檢視設定檔]**&#x200B;和&#x200B;**[!UICONTROL 檢視區段]** [存取控制許可權](/help/access-control/home.md#permissions)。 閱讀[存取控制總覽](/help/access-control/ui/overview.md)或連絡您的產品管理員以取得必要的許可權。

閱讀[啟用串流區段匯出目的地的設定檔和區段](/help/destinations/ui/activate-segment-streaming-destinations.md)，以取得啟用此目的地的對象區段的指示。

### 對應屬性和身分 {#map}

下列目標身分名稱空間必須根據使用案例進行對應：

* **電子郵件**&#x200B;必須使用&#x200B;**目標欄位>選取身分名稱空間>電子郵件**&#x200B;對應為目標欄位

![如何對應設定檔與身分欄位](/help/destinations/assets/catalog/marketing-automation/rainfocus/rainfocus-destination-mapping.png)

建議對應其他設定檔欄位，因為這將確保[!DNL RainFocus]中的出席者設定檔已完全填入。 下列目標欄位可從[!DNL RainFocus]取得：

| 目標欄位 | 說明 |
|------------|-------------|
| `address1` | 街道地址的第一行 |
| `address2` | 街道地址的第二行（如果適用） |
| `city` | 城市名稱 |
| `companyname` | 公司名稱 |
| `countryid` | 國家/地區的ISO 3166-1 alpha-2國家/地區代碼識別碼 |
| `email` | 電子郵件地址 |
| `firstname` | 人員的名字 |
| `lastname` | 人員的姓氏 |
| `jobtitle` | 個人的職稱 |
| `phone` | 電話號碼 |
| `state` | 該州或省的FIPS州字母代碼 |
| `zip` | 郵遞區號 |

{style="table-layout:auto"}

## 匯出的資料/驗證資料匯出 {#exported-data}

將一組設定檔傳送至[!DNL RainFocus]後，請使用[!DNL RainFocus]中的API設定檔記錄來驗證設定檔是否已成功擷取。

![在RainFocus中檢視API設定檔中的記錄檔](/help/destinations/assets/catalog/marketing-automation/rainfocus/rainfocus-destination-api-profile.png)

![驗證設定檔是否已成功擷取](/help/destinations/assets/catalog/marketing-automation/rainfocus/rainfocus-destination-api-logging.png)

## 資料使用與控管 {#data-usage-governance}

處理您的資料時，所有[!DNL Adobe Experience Platform]目的地都符合資料使用原則。 如需[!DNL Adobe Experience Platform]如何強制資料控管的詳細資訊，請閱讀[資料控管概觀](/help/data-governance/home.md)。

## 其他資源 {#additional-resources}

* [RainFocus串流Source聯結器](https://experienceleague.adobe.com/en/docs/experience-platform/sources/connectors/analytics/rainfocus)