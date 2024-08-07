---
title: Acxiom 潛在客戶禁止
description: 將您的第一方對象匯出至Acxiom目的地，以允許Acxiom抑制已知或轉換的客戶。 然後使用Acxiom來源聯結器從Acxiom擷取並啟用潛在客戶清單，將您的已知或轉換的客戶移除。
last-substantial-update: 2024-03-14T00:00:00Z
badge: Beta
exl-id: d82e8cd3-970c-44af-99b0-ea154eb3655e
source-git-commit: c35b43654d31f0f112258e577a1bb95e72f0a971
workflow-type: tm+mt
source-wordcount: '1466'
ht-degree: 2%

---

# [!DNL Acxiom Prospect-Suppression]目的地連線

>[!NOTE]
>
>[!DNL Acxiom Prospect-Suppression]目的地是測試版。 此目的地聯結器和檔案頁面是由Acxiom團隊建立和維護的。 如有任何查詢或更新要求，請直接透過acxiom-adobe-help@acxiom.com聯絡。

## 概觀 {#overview}

使用[!DNL Acxiom Prospect-Suppression]儘可能提供生產力最高的潛在客戶對象。 此聯結器會從Real-time Customer Data Platform安全地匯出第一方資料，並透過獲獎的衛生和身分解析來執行它，這會產生要用作隱藏清單的資料檔案。 這將與[!DNL Acxiom Global]資料庫進行比對，讓潛在客戶清單可以針對匯入量身打造。 然後，使用[[!DNL Acxiom Prospecting Data Import]](/help/sources/connectors/data-partners/acxiom-prospecting-data-import.md)來源聯結器將潛在客戶清單從Acxiom傳回Real-Time CDP，並移除您的已知或轉換的客戶。

![行銷圖表將第一方資料匯出至Acxiom，然後將潛在客戶資料匯回Real-Time CDP](/help/destinations/assets/catalog/data-partner/acxiom/marketing-workflow.png)

Acxiom擁有超過12,000個全球資料屬性的最大目錄，專門用於提供個人化體驗，提供業界表現最佳的對象。 運用高品質資料的無限組合，建立和發佈對象以滿足特定的行銷活動需求。

本教學課程提供使用Adobe Experience Platform使用者介面建立[!DNL Acxiom Prospect-Suppression]目的地連線和資料流的步驟。 此聯結器是用來將資料傳遞至Acxiom潛在客戶服務，使用Amazon S3作為放置點。 開始將檔案匯出至Amazon S3放置點後，請聯絡您的Acxiom客戶代表。

![已選取Acxiom目的地的目的地目錄。](../../assets/catalog/data-partner/acxiom/image-destination-catalog.png)

## 使用案例 {#use-cases}

為協助您更清楚瞭解您應如何及何時使用[!DNL Acxiom Prospect-Suppression]目的地，以下是Adobe Experience Platform客戶可藉由使用此目的地解決的範例使用案例。

### 為潛在客戶資料集建立隱藏清單 {#create-suppression-list}

行銷專業人員為了提高其外展策略的有效性，通常會建立隱藏清單。 此清單包括現有客戶和特定區段，以確保在鎖定目標的行銷活動中，將其排除在潛在客戶活動之外。 此策略方法有助於調整受眾、避免多餘的溝通，以及促成更聚焦且有效率的行銷工作。

例如，身為行銷人員，您可能想要根據您提供的細分和隱藏條件，將目標潛在客戶設定檔新增至行銷活動，以擴大行銷活動觸及範圍。

使用案例是透過結合目的地和來源聯結器來執行。

您一開始會使用此目的地聯結器匯出現有的客戶設定檔，以用作隱藏檔案。 這可確保不包含現有的客戶記錄。

Acxiom的服務會搜尋檔案、擷取檔案，並搭配其他選取條件使用，以及產生潛在客戶檔案。 您之後會使用對應的[[!DNL Acxiom Prospecting Data Import]](/help/sources/connectors/data-partners/acxiom-prospecting-data-import.md)來源聯結器將潛在客戶設定檔擷取到Adobe Real-Time CDP。

## 先決條件 {#prerequisites}

>[!IMPORTANT]
>
>* 若要連線到目的地，您需要&#x200B;**[!UICONTROL 檢視目的地]**&#x200B;和&#x200B;**[!UICONTROL 管理目的地]**、**[!UICONTROL 啟用目的地]**、**[!UICONTROL 檢視設定檔]**&#x200B;和&#x200B;**[!UICONTROL 檢視區段]** [存取控制許可權](/help/access-control/home.md#permissions)。 閱讀[存取控制總覽](/help/access-control/ui/overview.md)或連絡您的產品管理員以取得必要的許可權。
>* 若要匯出&#x200B;*身分*，您需要&#x200B;**[!UICONTROL 檢視身分圖表]** [存取控制許可權](/help/access-control/home.md#permissions)。<br> ![選取工作流程中反白的身分名稱空間，以啟用目的地的對象。](/help/destinations/assets/overview/export-identities-to-destination.png "選取工作流程中反白顯示的身分名稱空間，以啟用目的地的對象。"){width="100" zoomable="yes"}

## 支援的對象 {#supported-audiences}

本節說明您可以將哪些型別的對象匯出至此目的地。

| 對象來源 | 支援 | 說明 |
|-----------------------------|-----------|---------------------------------------------------------------------------------------------------------------------|
| [!DNL Segmentation Service] | ✓ (A) | 透過Experience Platform[細分服務](../../../segmentation/home.md)產生的對象。 |
| 自訂上傳 | x | 對象[從CSV檔案匯入](../../../segmentation/ui/audience-portal.md#import-audience)至Experience Platform。 |

{style="table-layout:auto"}


## 匯出型別和頻率 {#export-type-frequency}

請參閱下表以取得目的地匯出型別和頻率的資訊。

| 項目 | 類型 | 附註 |
|------------------|--------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 匯出類型 | **[!UICONTROL 以設定檔為基礎]** | 您正在匯出區段的所有成員，以及所需的結構描述欄位（例如：電子郵件地址、電話號碼、姓氏），如[目的地啟用工作流程](/help/destinations/ui/activate-batch-profile-destinations.md#select-attributes)的選取設定檔屬性畫面中所選。 |
| 匯出頻率 | **[!UICONTROL 批次]** | 批次目的地會以三、六、八、十二或二十四小時的增量將檔案匯出至下游平台。 深入瞭解[批次檔案型目的地](/help/destinations/destination-types.md#file-based)。 |

{style="table-layout:auto"}

## 連線到目標 {#connect}

>[!IMPORTANT]
> 
>若要連線到目的地，您需要&#x200B;**[!UICONTROL 檢視目的地]**&#x200B;和&#x200B;**[!UICONTROL 管理目的地]** [存取控制許可權](/help/access-control/home.md#permissions)。 閱讀[存取控制總覽](/help/access-control/ui/overview.md)或連絡您的產品管理員以取得必要的許可權。

若要連線到此目的地，請依照[目的地組態教學課程](../../ui/connect-destination.md)中所述的步驟進行。 在目標設定工作流程中，填寫以下兩個區段中列出的欄位。

### 驗證目標 {#authenticate}

若要驗證到目的地，請填入必填欄位，然後選取&#x200B;**[!UICONTROL 連線到目的地]**。

若要在Experience Platform上存取貯體，您必須提供下列憑證的有效值：

| 認證 | 說明 |
|---------------|----------------------------------------------------------------------------------------------------------|
| S3存取金鑰 | 貯體的存取金鑰ID。 您可以從[!DNL Acxiom]團隊擷取此值。 |
| S3秘密金鑰 | 貯體的秘密金鑰ID。 您可以從[!DNL Acxiom]團隊擷取此值。 |
| 貯體名稱 | 這是您的貯體，檔案將在此共用。 您可以從[!DNL Acxiom]團隊擷取此值。 |

### 新帳戶

若要定義新的Acxiom Managed S3位置：

![新帳戶](../../assets/catalog/data-partner/acxiom/image-destination-new-account.png)

### 現有帳戶

已使用[!DNL Acxiom Prospect Suppression]目的地定義的帳戶會出現在清單快顯視窗中。 選取後，您可以在右側邊欄中檢視帳戶的詳細資料。 當您導覽至&#x200B;**[!UICONTROL 目的地]** > **[!UICONTROL 帳戶]**&#x200B;時，從UI檢視範例：

![現有帳戶](../../assets/catalog/data-partner/acxiom/image-destination-account.png)

### 填寫目標詳細資訊 {#destination-details}

若要設定目的地的詳細資訊，請填寫下方的必填和選用欄位。 UI中欄位旁的星號表示該欄位為必填欄位。

![目的地詳細資料](../../assets/catalog/data-partner/acxiom/image-destination-details.png)

* **名稱（必要）** — 將目的地儲存於其下的名稱
* **描述** — 目的地的簡短說明
* **貯體名稱（必要）** — 在S3上設定的Amazon S3貯體的名稱
* **資料夾路徑（必要）** — 如果使用儲存貯體中的子目錄，則必須定義路徑，或使用&#39;/&#39;來參考根路徑。
* **檔案型別** — 選取匯出檔案應使用的格式Experience Platform。 目前，Acxiom處理所需的唯一檔案型別是CSV

>[!IMPORTANT]
>
>選取CSV選項&#x200B;*分隔符號*、*引號字元*、*逸出字元*、*空值*、*空值*、*壓縮格式*&#x200B;以及&#x200B;*包含資訊清單檔案*&#x200B;選項時，下列檔案將詳細說明這些設定[設定格式選項](../../ui/batch-destinations-file-formatting-options.md)。

![CSV選項](../../assets/catalog/data-partner/acxiom/image-destination-csv-options.png)

### 啟用警示 {#enable-alerts}

您可以啟用警報以接收有關傳送到您目的地的資料流狀態的通知。 從清單中選取警報以訂閱接收有關資料流狀態的通知。 如需警示的詳細資訊，請參閱[使用UI訂閱目的地警示](../../ui/alerts.md)的指南。

當您完成提供目的地連線的詳細資訊後，請選取&#x200B;**[!UICONTROL 下一步]**。

## 啟動此目標的對象 {#activate}

>[!IMPORTANT]
>
>* 若要啟用資料，您需要&#x200B;**[!UICONTROL 檢視目的地]**、**[!UICONTROL 啟用目的地]**、**[!UICONTROL 檢視設定檔]**&#x200B;和&#x200B;**[!UICONTROL 檢視區段]** [存取控制許可權](/help/access-control/home.md#permissions)。 閱讀[存取控制總覽](/help/access-control/ui/overview.md)或連絡您的產品管理員以取得必要的許可權。
>* 若要匯出&#x200B;*身分*，您需要&#x200B;**[!UICONTROL 檢視身分圖表]** [存取控制許可權](/help/access-control/home.md#permissions)。<br> ![選取工作流程中反白的身分名稱空間，以啟用目的地的對象。](/help/destinations/assets/overview/export-identities-to-destination.png "選取工作流程中反白顯示的身分名稱空間，以啟用目的地的對象。"){width="100" zoomable="yes"}

讀取[啟用批次設定檔匯出目的地的對象資料](/help/destinations/ui/activate-batch-profile-destinations.md)，以取得啟用此目的地對象的指示。

### 對應建議

處理需要名稱和位址元素，但並非所有元素都需要，提供儘可能多的內容以協助成功比對。  下表列出目標端的屬性，這些屬性用於Acxiom處理，可供客戶將設定檔屬性對應至。  這應視為建議，因為並非所有元素都是必要的，且來源值將取決於帳戶的需求。

| 目標欄位 | Source說明 |
|--------------|-------------------------------------------------------------|
| 名稱 | Experience Platform中的`person.name.fullName`值。 |
| 名字 | Experience Platform中的`person.name.firstName`值。 |
| 姓氏 | Experience Platform中的`person.name.lastName`值。 |
| address1 | Experience Platform中的`mailingAddress.street1`值。 |
| address2 | Experience Platform中的`mailingAddress.street2`值。 |
| 城市 | Experience Platform中的`mailingAddress.city`值。 |
| state | Experience Platform中的`mailingAddress.state`值。 |
| zip | Experience Platform中的`mailingAddress.postalCode`值。 |

{style="table-layout:auto"}

>[!NOTE]
>
>以上未列出的其他欄位將會包含在匯出中，但會被Acxiom處理忽略。

## 檢閱您的資料流

在提交之前，請使用複查頁面來取得資料流的摘要

![檢閱](../../assets/catalog/data-partner/acxiom/image-destination-review.png)

## 驗證資料匯出 {#exported-data}

若要驗證是否已成功匯出資料，請檢查您的[!DNL Amazon S3 Storage]貯體，並確定匯出的檔案包含預期的設定檔母體。

## 後續步驟

依照此教學課程中的指示，您已成功建立資料流，以將批次資料從Experience Platform匯出至[!DNL Acxiom]受管理的S3位置。 您需要連絡您的Acxiom代表，提供帳戶名稱、檔案名稱和貯體路徑，以便設定處理。

## 資料使用與控管 {#data-usage-governance}

處理您的資料時，所有[!DNL Adobe Experience Platform]目的地都符合資料使用原則。 如需[!DNL Adobe Experience Platform]如何強制資料控管的詳細資訊，請閱讀[資料控管概觀](/help/data-governance/home.md)。

## 其他資源 {#additional-resources}

*Acxiom對象資料與分佈：* https://www.acxiom.com/customer-data/audience-data-distribution/
