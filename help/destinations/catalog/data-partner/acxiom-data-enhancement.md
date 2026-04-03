---
title: Acxiom資料增強功能
description: 使用此聯結器在Real-Time CDP中啟動第一方Adobe設定檔至Acxiom，以擴充資料並跨行銷管道使用。 然後，您可以使用 Acxiom 來源匯入含有增強資料的設定檔，並在 Real-Time CDP 中使用它們。
last-substantial-update: 2024-03-14T00:00:00Z
badge: label="Beta" type="Informative"
exl-id: 59edc43d-ae8e-4c3d-820c-b5be1c4483f9
source-git-commit: 58f69a78fb3c622c8741d7a1618f15509c160a5b
workflow-type: tm+mt
source-wordcount: '1413'
ht-degree: 5%

---

# [!DNL Acxiom Data Enhancement]目的地連線

>[!NOTE]
>
>[!DNL Acxiom Data Enhancement]目的地是測試版。  此目的地聯結器和檔案頁面是由Acxiom團隊建立和維護的。 如有任何查詢或更新要求，請直接透過acxiom-adobe-help@acxiom.com聯絡。

## 概觀 {#overview}

使用[!DNL Acxiom Data Enhancement]聯結器為您的客戶設定檔提供額外的描述性資料，以用於分析、細分和目標定位應用程式。 由於有數百個可用元素，因此可啟用更好的細分和資料模型，進而實現更精確的目標定位和預測性模型。

![行銷圖表可將第一方資料匯出至Acxiom，然後將擴充的資料匯回Real-Time CDP](/help/destinations/assets/catalog/data-partner/acxiom/marketing-workflow-data-enhancement.png)

本教學課程提供使用[!DNL Acxiom Data Enhancement]使用者介面建立[!DNL Adobe Experience Platform]目的地連線和資料流的步驟。 此聯結器會使用Amazon S3作為放置點，將資料傳送至Acxiom增強服務。

![已選取Acxiom目的地的目的地目錄。](../../assets/catalog/data-partner/acxiom/image-destination-enhancement-catalog.png)

## 使用案例 {#use-cases}

為協助您更清楚瞭解您應如何及何時使用[!DNL Acxiom Data Enhancement]目的地，以下是[!DNL Adobe Experience Platform]客戶可以使用此目的地解決的範例使用案例。

### 增強客戶資料 {#enhance-customer-data}

行銷專業人員應使用此聯結器，藉由將選取的描述性元素附加至其客戶設定檔中，並運用這些元素更好地鎖定行銷活動，以提高其外展策略的成效。

例如，身為行銷人員，您可能想要透過使用其他資料豐富現有對象的設定檔，以加深對現有對象的瞭解。 這麼做將改善您的細分和目標定位策略，進而促進行銷活動個人化和轉換。

使用案例是透過結合目的地和來源聯結器來執行。

一開始您可以使用此目的地聯結器匯出現有客戶記錄以進行擴充。 Acxiom的服務會搜尋檔案、擷取檔案、使用Acxiom的資料擴充檔案並產生檔案。

然後，客戶將使用對應的[Acxiom資料擷取](/help/sources/connectors/data-partners/acxiom-data-ingestion.md)來源卡片，將水合的客戶設定檔擷取回Adobe [!DNL Real-Time CDP]。

## 先決條件 {#prerequisites}

>[!IMPORTANT]
>
>* 若要連線到目的地，您需要&#x200B;**[!UICONTROL View Destinations]**&#x200B;和&#x200B;**[!UICONTROL Manage Destinations]**、**[!UICONTROL Activate Destinations]**、**[!UICONTROL View Profiles]**&#x200B;和&#x200B;**[!UICONTROL View Segments]** [存取控制許可權](/help/access-control/home.md#permissions)。 閱讀[存取控制總覽](/help/access-control/ui/overview.md)或連絡您的產品管理員以取得必要的許可權。
>* 若要匯出&#x200B;*身分*，您需要&#x200B;**[!UICONTROL View Identity Graph]** [存取控制許可權](/help/access-control/home.md#permissions)。<br> ![選取工作流程中反白的身分名稱空間，以啟用目的地的對象。](/help/destinations/assets/overview/export-identities-to-destination.png "選取工作流程中反白顯示的身分名稱空間，以啟用目的地的對象。"){width="100" zoomable="yes"}

## 支援的對象 {#supported-audiences}

本節說明您可以將哪些型別的對象匯出至此目的地。

| 對象來源 | 支援 | 說明 |
|---------|----------|----------|
| [!DNL Segmentation Service] | 是 | 透過Experience Platform [細分服務](../../../segmentation/home.md)產生的對象。 |
| 所有其他受眾來源 | 無 | 此類別包含透過[!DNL Segmentation Service]產生的對象以外的所有對象來源。 閱讀[各種對象來源](/help/segmentation/ui/audience-portal.md#customize)。 部分範例包括： <ul><li> 自訂上傳對象[從CSV檔案匯入](../../../segmentation/ui/audience-portal.md#import-audience)至Experience Platform，</li><li> 相似受眾， </li><li> 同盟對象， </li><li> 其他Experience Platform應用程式中產生的對象，例如[!DNL Adobe Journey Optimizer]、 </li><li> 及更多內容。 </li></ul> |

{style="table-layout:auto"}




依受眾資料型別支援的受眾：

| 對象資料型別 | 支援 | 說明 | 使用案例 |
|--------------------|-----------|-------------|-----------|
| [人員對象](/help/segmentation/types/people-audiences.md) | 是 | 根據客戶設定檔，可讓您針對行銷活動的特定人群進行定位。 | 經常購買者、購物車放棄者 |
| [帳戶對象](/help/segmentation/types/account-audiences.md) | 無 | 針對帳戶型行銷策略，鎖定特定組織內的個人。 | B2B行銷 |
| [潛在客戶對象](/help/segmentation/types/prospect-audiences.md) | 無 | 將目標定位為尚未成為客戶但與目標受眾具有相同特性的個人。 | 使用第三方資料進行勘探 |
| [資料集匯出](/help/catalog/datasets/overview.md) | 無 | 儲存在[!DNL Adobe Experience Platform]資料湖中的結構化資料集合。 | 報告、資料科學工作流程 |

{style="table-layout:auto"}


## 匯出型別和頻率 {#export-type-frequency}

請參閱下表，以取得目的地匯出型別和頻率的資訊。

| 項目 | 類型 | 附註 |
|------------------|--------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 匯出類型 | **[!UICONTROL Profile-based]** | 您正在匯出區段的所有成員，以及所需的結構描述欄位（例如：電子郵件地址、電話號碼、姓氏），如[目的地啟用工作流程](/help/destinations/ui/activate-batch-profile-destinations.md#select-attributes)的選取設定檔屬性畫面中所選。 |
| 匯出頻率 | **[!UICONTROL Batch]** | 批次目的地會以三、六、八、十二或二十四小時的增量將檔案匯出至下游平台。 深入瞭解[批次檔案型目的地](/help/destinations/destination-types.md#file-based)。 |

{style="table-layout:auto"}

## 連線到目標 {#connect}

>[!IMPORTANT]
>
>若要連線到目的地，您需要&#x200B;**[!UICONTROL View Destinations]**&#x200B;和&#x200B;**[!UICONTROL Manage and Activate Dataset Destinations]** [存取控制許可權](/help/access-control/home.md#permissions)。 閱讀[存取控制總覽](/help/access-control/ui/overview.md)或連絡您的產品管理員以取得必要的許可權。

若要連線到此目的地，請依照[目的地組態教學課程](../../ui/connect-destination.md)中所述的步驟進行。 在目標設定工作流程中，填寫以下兩個區段中列出的欄位。

### 驗證目標 {#authenticate}

若要驗證到目的地，請填寫必填欄位並選取&#x200B;**[!UICONTROL Connect to destination]**。

若要在Experience Platform上存取貯體，您必須提供下列憑證的有效值：

| 認證 | 說明 |
|---------------|----------------------------------------------------------------------------------------------------------|
| S3存取金鑰 | 貯體的存取金鑰ID。 您可以從[!DNL Acxiom]團隊擷取此值。 |
| S3秘密金鑰 | 貯體的秘密金鑰ID。 您可以從[!DNL Acxiom]團隊擷取此值。 |
| 貯體名稱 | 這是您的貯體，檔案將在此共用。 您可以從[!DNL Acxiom]團隊擷取此值。 |

### 新帳戶 {#new-account}

若要定義新的Acxiom Managed S3位置：

![新帳戶](../../assets/catalog/data-partner/acxiom/image-destination-new-account.png)

### 現有帳戶 {#existing-account}

已使用[!DNL Acxiom Data Enhancement]目的地定義的帳戶會出現在清單快顯視窗中。 選取後，您可以在右側邊欄中檢視帳戶的詳細資料。 當您導覽至&#x200B;**[!UICONTROL Destinations]** > **[!UICONTROL Accounts]**&#x200B;時，從UI檢視範例；

![現有帳戶](../../assets/catalog/data-partner/acxiom/image-destination-enhancement-account.png)

### 填寫目標詳細資訊 {#destination-details}

若要設定目的地的詳細資訊，請填寫下方的必填和選用欄位。 UI中欄位旁的星號表示該欄位為必填欄位。

![目的地詳細資料](../../assets/catalog/data-partner/acxiom/image-destination-details.png)

* **名稱（必要）** — 將目的地儲存於其下的名稱
* **描述** — 目的地的簡短說明
* **貯體名稱（必要）** — 在S3上設定的Amazon S3貯體的名稱
* **資料夾路徑（必要）** — 如果使用儲存貯體中的子目錄，則必須定義路徑，或使用&#39;/&#39;來參考根路徑。
* **檔案型別** — 選取Experience Platform用於匯出檔案的格式。 目前，Acxiom處理所需的唯一檔案型別是CSV

>[!IMPORTANT]
>
>選取CSV選項&#x200B;*分隔符號*、*引號字元*、*逸出字元*、*空值*、*空值*、*壓縮格式*&#x200B;以及&#x200B;*包含資訊清單檔案*&#x200B;選項時，下列檔案將詳細說明這些設定[設定格式選項](../../ui/batch-destinations-file-formatting-options.md)。

![CSV選項](../../assets/catalog/data-partner/acxiom/image-destination-csv-options.png)

### 啟用警示 {#enable-alerts}

您可以啟用警報以接收有關傳送到您目的地的資料流狀態的通知。 從清單中選取警報以訂閱接收有關資料流狀態的通知。 如需警示的詳細資訊，請參閱[使用UI訂閱目的地警示](../../ui/alerts.md)的指南。

當您完成提供目的地連線的詳細資訊時，請選取&#x200B;**[!UICONTROL Next]**。

## 啟動此目標的對象 {#activate}

>[!IMPORTANT]
>
>* 若要啟用資料，您需要&#x200B;**[!UICONTROL View Destinations]**、**[!UICONTROL Activate Destinations]**、**[!UICONTROL View Profiles]**&#x200B;和&#x200B;**[!UICONTROL View Segments]** [存取控制許可權](/help/access-control/home.md#permissions)。 閱讀[存取控制總覽](/help/access-control/ui/overview.md)或連絡您的產品管理員以取得必要的許可權。
>* 若要匯出&#x200B;*身分*，您需要&#x200B;**[!UICONTROL View Identity Graph]** [存取控制許可權](/help/access-control/home.md#permissions)。<br> ![選取工作流程中反白的身分名稱空間，以啟用目的地的對象。](/help/destinations/assets/overview/export-identities-to-destination.png "選取工作流程中反白顯示的身分名稱空間，以啟用目的地的對象。"){width="100" zoomable="yes"}

讀取[啟用批次設定檔匯出目的地的對象資料](/help/destinations/ui/activate-batch-profile-destinations.md)，以取得啟用此目的地對象的指示。

### 對應建議 {#mapping-suggestions}

在Acxiom端正確處理檔案需要名稱和位址元素。 雖然並非所有元素都需要，但儘可能提供有助於成功比對。

下表列出目標端的屬性，這些屬性用於Acxiom處理，可供客戶將設定檔屬性對應至。 將這些元素視為建議，因為並非所有元素都是必要的，而來源值將視帳戶的需求而定。

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

>[!NOTE]
>
>如果您對映資料流中未列出的其他欄位，這些欄位將會包含在資料匯出中，但會被Acxiom處理忽略。

## 驗證資料匯出 {#exported-data}

若要驗證是否已成功匯出資料，請檢查您的[!DNL Amazon S3 Storage]貯體，並確定匯出的檔案包含預期的設定檔母體。

## 後續步驟 {#next-steps}

您已成功建立資料流，以將設定檔資料從Experience Platform匯出至[!DNL Acxiom]受管理的S3位置。 接下來，您需要連絡您的Acxiom代表，提供帳戶名稱、檔案名稱以及儲存貯體路徑，以便設定處理作業。

## 資料使用與控管 {#data-usage-governance}

處理您的資料時，所有[!DNL Adobe Experience Platform]目的地都符合資料使用原則。 如需[!DNL Adobe Experience Platform]如何強制資料控管的詳細資訊，請閱讀[資料控管概觀](/help/data-governance/home.md)。

## 其他資源 {#additional-resources}

*Acxiom Infobase：* https://www.acxiom.com/wp-content/uploads/2022/02/fs-acxiom-infobase_AC-0268-22.pdf
