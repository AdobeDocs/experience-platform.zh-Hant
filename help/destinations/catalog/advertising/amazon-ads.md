---
title: Amazon Ads
description: Amazon Ads提供一系列選項，協助您為註冊賣家、廠商、圖書供應商、Kindle Direct Publishing (KDP)作者、應用程式開發人員和/或代理商達成廣告目標。 Amazon Ads與Adobe Experience Platform的整合提供與Amazon Ads產品(包括Amazon DSP (ADSP))的鑰匙式整合。 使用Adobe Experience Platform中的Amazon Ads目的地，使用者能在Amazon DSP上定義用於鎖定和啟用的廣告商對象。
last-substantial-update: 2024-02-20T00:00:00Z
exl-id: 724f3d32-65e0-4612-a882-33333e07c5af
source-git-commit: 56971631eb7ab2ef3dd2dcf077ee3b52f131ffe7
workflow-type: tm+mt
source-wordcount: '1761'
ht-degree: 2%

---

# (Beta) Amazon Ads連線 {#amazon-ads}

## 概觀 {#overview}

[!DNL Amazon Ads]提供一系列選項，協助您為註冊賣家、廠商、圖書廠商、Kindle Direct Publishing (KDP)作者、應用程式開發人員和/或代理商達成廣告目標。

[!DNL Amazon Ads]與Adobe Experience Platform的整合提供與[!DNL Amazon Ads]產品的按鍵式整合，包括Amazon DSP (ADSP)和AmazonMarketing Cloud(AMC)。

使用Adobe Experience Platform中的[!DNL Amazon Ads]目的地，使用者能在Amazon DSP上定義目標定位和啟用的廣告商對象。  此外，使用者可將其資料上傳至[!DNL Amazon Marketing Cloud]，以瞭解對象、廣告商提供的維度、Amazon區段中的成員資格，或AMC中可用的其他訊號的效能。 將廣告商受眾上傳至AMC後，使用者可以使用[!DNL Amazon Marketing Cloud]來修改、增強或附加至使用[!DNL Amazon Marketing Cloud]內Amazon訊號的受眾成員。

AMC將Amazon擁有和運營的屬性所產生的獨特訊號整合在一起，橫跨多種媒體，包括顯示器、視訊、串流電視、音訊和贊助廣告。 使用者可以輕鬆地從Adobe Experience Platform將已組織的區段傳送至AMC，以增強學習，例如受眾的市場內群組、生活方式同類群組及品牌參與模式。 然後可以使用增強的區段來最佳化Amazon DSP中的媒體啟用。

>[!IMPORTANT]
>
>此目的地聯結器和檔案頁面是由&#x200B;*[!DNL Amazon Ads]*&#x200B;團隊建立和維護。 此產品目前為測試版，功能可能會有所變更。 若有任何查詢或更新要求，請直接在&#x200B;*`amc-support@amazon.com`.*&#x200B;聯絡他們

## 使用案例 {#use-cases}

為協助您更清楚瞭解您應如何及何時使用&#x200B;*[!DNL Amazon Ads]*&#x200B;目的地，以下是Adobe Experience Platform客戶可藉由使用此目的地解決的範例使用案例。

### 啟用與定位 {#activation-and-targeting}

此與Amazon DSP的整合可讓[!DNL Amazon Ads]個廣告商從Adobe Experience Platform將廣告商CDP受眾傳遞至Amazon的DSP，以建立廣告商受眾以用於廣告鎖定。 您可以在Amazon DSP中選取正面目標定位和負面目標定位（隱藏）的對象。

### Analytics與Measurement {#analytics-and-measurement}

此與[!DNL Amazon Marketing Cloud] (AMC)的整合可讓[!DNL Amazon Ads]個廣告商將CDP區段從Adobe Experience Platform表單傳遞至AMC。 廣告商可以使用[!DNL Amazon Ads]訊號加入CDP輸入，並以符合隱私權要求的格式對媒體影響、受眾區段和客戶歷程等主題進行自訂分析。 例如，廣告商可能會上傳其現有客戶的清單，以瞭解彙總的廣告促銷活動成效，或Amazon上轉換事件的彙總統計資料，例如檢視產品詳細資料頁面、將產品新增至購物車或購買產品。

### Advertising最佳化

此與[!DNL Amazon Marketing Cloud] (AMC)的整合可讓廣告商上傳自己的客戶清單，並使用[!DNL Amazon Marketing Cloud] SQL，在針對Amazon DSP中建立可啟動的受眾之前，定期對受眾執行重疊分析、隱藏、新增或最佳化。

## 先決條件 {#prerequisites}

若要使用[!DNL Amazon Ads]與Adobe Experience Platform的連線，使用者必須先存取Amazon DSP廣告商帳戶或[!DNL Amazon Marketing Cloud]執行個體。 若要布建這些執行個體，請造訪[!DNL Amazon Ads]網站上的下列頁面：

* [開始使用Amazon DSP](https://advertising.amazon.com/solutions/products/amazon-dsp)
* [開始使用AmazonMarketing Cloud](https://advertising.amazon.com/solutions/products/amazon-marketing-cloud)

## 支援的身分 {#supported-identities}

*[!DNL Amazon Ads]*&#x200B;連線支援啟用下表所述的身分。 深入瞭解[身分](/help/identity-service//features/namespaces.md)。 如需[!DNL Amazon Ads]支援的身分識別詳細資訊，請造訪[Amazon DSP支援中心](https://advertising.amazon.com/dsp/help/ss/en/audiences#GA6BC9BW52YFXBNE)。

| 目標身分 | 說明 | 考量事項 |
|---|---|---|
| phone_sha256 | 使用SHA256演演算法雜湊的電話號碼 | Adobe Experience Platform同時支援純文字和SHA256雜湊電話號碼。 當您的來源欄位包含未雜湊的屬性時，請核取&#x200B;**[!UICONTROL 套用轉換]**&#x200B;選項，讓[!DNL Platform]在啟用時自動雜湊資料。 |
| email_lc_sha256 | 使用SHA256演演算法雜湊的電子郵件地址 | Adobe Experience Platform同時支援純文字和SHA256雜湊電子郵件地址。 當您的來源欄位包含未雜湊的屬性時，請核取&#x200B;**[!UICONTROL 套用轉換]**&#x200B;選項，讓[!DNL Platform]在啟用時自動雜湊資料。 |

{style="table-layout:auto"}

## 匯出型別和頻率 {#export-type-frequency}

請參閱下表以取得目的地匯出型別和頻率的資訊。

| 項目 | 類型 | 附註 |
---------|----------|---------|
| 匯出類型 | **[!UICONTROL 對象匯出]** | 您正在匯出具有&#x200B;*[!DNL Amazon Ads]*&#x200B;目的地中所使用識別碼（名稱、電話號碼或其他）的對象的所有成員。 |
| 匯出頻率 | **[!UICONTROL 串流]** | 串流目的地是「一律開啟」的API型連線。 一旦根據對象評估在Experience Platform中更新了設定檔，聯結器就會將更新傳送至下游的目的地平台。 深入瞭解[串流目的地](/help/destinations/destination-types.md#streaming-destinations)。 |

{style="table-layout:auto"}

## 連線到目標 {#connect}

>[!IMPORTANT]
> 
>若要連線到目的地，您需要&#x200B;**[!UICONTROL 檢視目的地]**&#x200B;和&#x200B;**[!UICONTROL 管理目的地]** [存取控制許可權](/help/access-control/home.md#permissions)。 閱讀[存取控制總覽](/help/access-control/ui/overview.md)或連絡您的產品管理員以取得必要的許可權。

若要連線到此目的地，請依照[目的地組態教學課程](../../ui/connect-destination.md)中所述的步驟進行。 在設定目標工作流程中，填寫以下兩個區段中列出的欄位。

### 驗證目標 {#authenticate}

若要驗證到目的地，請填入必填欄位，然後選取&#x200B;**[!UICONTROL 連線到目的地]**。

系統會將您帶往[!DNL Amazon Ads]連線介面，讓您先選取要連線的廣告商帳戶。 連線後，系統會將您重新導向回Adobe Experience Platform，並顯示您選取的廣告商帳戶ID，其中包含新的連線。 在目的地設定畫面上選取適當的廣告商帳戶以繼續。

* **[!UICONTROL 持有人權杖]**：填入持有人權杖以驗證目的地。

### 填寫目標詳細資訊 {#destination-details}

若要設定目的地的詳細資訊，請填寫下方的必填和選用欄位。 UI中欄位旁的星號表示該欄位為必填欄位。

* **[!UICONTROL 名稱]**：您日後可辨識此目的地的名稱。
* **[!UICONTROL 描述]**：可協助您日後識別此目的地的描述。
* **[!UICONTROL Amazon Ads連線]**：選取用於目的地的目標[!DNL Amazon Ads]帳戶識別碼。

>[!NOTE]
>
>儲存目的地設定後，您將無法變更[!DNL Amazon Ads]廣告商ID，即使您透過Amazon帳戶重新驗證亦然。 若要使用其他[!DNL Amazon Ads]廣告商ID，您必須建立新的目的地連線。 已設定與ADSP整合的廣告商，如果他們想要將其對象傳送至AMC或其他ADSP帳戶，則必須建立新的目的地流程。

* **[!UICONTROL 廣告商地區]**：選取您的廣告商所在的適當地區。 如需各個區域支援之市場環境的詳細資訊，請瀏覽[Amazon Ads檔案](https://advertising.amazon.com/API/docs/en-us/info/api-overview#api-endpoints)。



![設定新的目的地](../../assets/catalog/advertising/amazon_ads_image_4.png)

### 啟用警示 {#enable-alerts}

您可以啟用警報以接收有關傳送到您目的地的資料流狀態的通知。 從清單中選取警報以訂閱接收有關資料流狀態的通知。 如需警示的詳細資訊，請參閱[使用UI訂閱目的地警示](../../ui/alerts.md)的指南。

當您完成提供目的地連線的詳細資訊後，請選取&#x200B;**[!UICONTROL 下一步]**。

## 啟動此目標的客群 {#activate}

>[!IMPORTANT]
> 
>* 若要啟用資料，您需要&#x200B;**[!UICONTROL 檢視目的地]**、**[!UICONTROL 啟用目的地]**、**[!UICONTROL 檢視設定檔]**&#x200B;和&#x200B;**[!UICONTROL 檢視區段]** [存取控制許可權](/help/access-control/home.md#permissions)。 閱讀[存取控制總覽](/help/access-control/ui/overview.md)或連絡您的產品管理員以取得必要的許可權。
>* 若要匯出&#x200B;*身分*，您需要&#x200B;**[!UICONTROL 檢視身分圖表]** [存取控制許可權](/help/access-control/home.md#permissions)。<br> ![選取工作流程中反白的身分名稱空間，以啟用目的地的對象。](/help/destinations/assets/overview/export-identities-to-destination.png "選取工作流程中反白顯示的身分名稱空間，以啟用目的地的對象。"){width="100" zoomable="yes"}

閱讀[將設定檔和對象啟用至串流對象匯出目的地](/help/destinations/ui/activate-segment-streaming-destinations.md)，以瞭解啟用此目的地對象的指示。

### 對應屬性和身分 {#map}

[!DNL Amazon Ads]連線支援雜湊電子郵件地址和雜湊電話號碼，以進行身分比對。 下面的熒幕擷圖提供與[!DNL Amazon Ads]連線相容的相符範例：

![Adobe至Amazon Ads對應](../../assets/catalog/advertising/amazon_ads_image_2.png)

* 若要對應雜湊電子郵件地址，請選取`Email_LC_SHA256`身分名稱空間作為來源欄位。
* 若要對應雜湊電話號碼，請選取`Phone_SHA256`身分名稱空間作為來源欄位。
* 若要對應未雜湊的電子郵件地址或電話號碼，請選取對應的身分識別名稱空間作為來源欄位，並核取`Apply Transformation`選項以讓Platform在啟用時雜湊身分。
* *自2024年9月發行版本開始新增*： Amazon Ads需要您對應包含2個字元ISO格式之`countryCode`值的欄位，以便加速身分解析程式（例如：US、GB、MX、CA等）。 沒有`countryCode`對應的連線將會對身分符合率產生負面影響。

您在[!DNL Amazon Ads]聯結器的目的地設定中只選取一次指定的目標欄位。  例如，如果您提交商務電子郵件，您就無法在同一目的地設定中對應個人電子郵件。

強烈建議您儘量對應可用欄位。 如果只有一個來源屬性可用，您可以對應單一欄位。 [!DNL Amazon Ads]目的地會使用所有對應的欄位來進行對應，如果提供更多欄位，則會產生較高的匹配率。 如需關於接受之識別碼的詳細資訊，請造訪[Amazon Ads雜湊對象說明頁面](https://advertising.amazon.com/dsp/help/ss/en/audiences#GA6BC9BW52YFXBNE)。

## 匯出的資料/驗證資料匯出 {#exported-data}

上傳對象後，您可使用以下步驟驗證對象是否已正確建立及上傳：

適用於Amazon DSP **的**

導覽至您的&#x200B;**[!UICONTROL 廣告商ID]** > **[!UICONTROL 對象]** > **[!UICONTROL 廣告商對象]**。 若您的對象已成功建立且符合對象成員的最小數量，您將會看到`Active`的狀態。 您可以在Amazon DSP使用者介面右側的預測觸及面板中，找到有關您對象人數和觸及率的其他詳細資訊。

![Amazon DSP對象建立驗證](../../assets/catalog/advertising/amazon_ads_image_3.png)

[!DNL Amazon Marketing Cloud]**的**

在左側結構描述瀏覽器中，在&#x200B;**[!UICONTROL 已上傳的廣告商]** > **[!UICONTROL aep_audiences]**&#x200B;下尋找您的對象。 然後，您可以在AMC SQL編輯器中使用下列子句查詢您的對象：

`select count(user_id) from adobeexperienceplatf_audience_view_000xyz where external_audience_segment_name = '1234567'`

![AmazonMarketing Cloud對象建立驗證](../../assets/catalog/advertising/amazon_ads_image_5.png)


## 資料使用與控管 {#data-usage-governance}

處理您的資料時，所有[!DNL Adobe Experience Platform]目的地都符合資料使用原則。 如需[!DNL Adobe Experience Platform]如何強制資料控管的詳細資訊，請閱讀[資料控管概觀](/help/data-governance/home.md)。

## 其他資源 {#additional-resources}

如需其他說明檔案，請瀏覽下列[!DNL Amazon Ads]說明資源：

* [Amazon DSP說明中心](https://www.amazon.com/ap/signin?openid.pape.max_auth_age=28800&amp;openid.return_to=https%3A%2F%2Fadvertising.amazon.com%2Fdsp%2Fhelp%2Fss%2Fen%2Faudiences&amp;openid.identity=http%3A%2F%2Fspecs.openid.net%2Fauth%2F2.0%2Fidentifier_select&amp;openid.assoc_handle=amzn_bt_desktop_us&amp;openid.mode=checkid_setup&amp;openid.claimed_id=http%3A%2F%2Fspecs.openid.net%2Fauth%2F2.0%2Fidentifier_select&amp;openid.ns=http%3A%2F%2Fspecs.openid.net%2Fauth%2F2.0)

## Changelog {#changelog}

本節擷取此目的地聯結器的功能和重要檔案更新。

+++ 檢視變更記錄檔

| 發行月份 | 更新型別 | 說明 |
|---|---|---|
| 2024 年 5 月 | 功能和檔案更新 | 已新增對應選項，以便將`countryCode`引數匯出至Amazon Ads。 在[對應步驟](#map)中使用`countryCode`來提高您與Amazon的身分符合率。 |
| 2024 年 3 月 | 功能和檔案更新 | 新增匯出對象以在[!DNL Amazon Marketing Cloud] (AMC)中使用的選項。 |
| 2023 年 5 月 | 功能和檔案更新 | <ul><li>已在[目的地連線工作流程](#destination-details)中新增對廣告商區域選取的支援。</li><li>更新說明檔案，反映新增廣告商地區選擇。 如需選取正確廣告商地區的詳細資訊，請參閱[Amazon檔案](https://advertising.amazon.com/API/docs/en-us/info/api-overview#api-endpoints)。</li></ul> |
| 2023 年 3 月 | 首次發行 | 已發佈初始目的地版本和檔案。 |

{style="table-layout:auto"}

+++
