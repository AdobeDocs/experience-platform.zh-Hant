---
title: Acxiom前景抑制
description: 將您的第一方對象匯出至Acxiom目的地，以允許Acxiom抑制已知或轉換的客戶。 然後使用Acxiom來源聯結器從Acxiom擷取並啟用潛在客戶清單，將您的已知或轉換的客戶移除。
last-substantial-update: 2024-03-14T00:00:00Z
badge: Beta
source-git-commit: c881f8375bc0eccb8e64666a888735c03018421c
workflow-type: tm+mt
source-wordcount: '1476'
ht-degree: 2%

---

# [!DNL Acxiom Prospect-Suppression] 目的地連線

>[!NOTE]
>
>此 [!DNL Acxiom Prospect-Suppression] 目的地是測試版。 此目的地聯結器和檔案頁面是由Acxiom團隊建立和維護的。 如有任何查詢或更新要求，請直接透過acxiom-adobe-help@acxiom.com聯絡。

## 概觀 {#overview}

使用 [!DNL Acxiom Prospect-Suppression] 儘可能提供生產力最高的潛在客戶對象。 此聯結器會從Real-time Customer Data Platform安全地匯出第一方資料，並透過獲獎的衛生和身分解析來執行它，這會產生要用作隱藏清單的資料檔案。 此專案將與 [!DNL Acxiom Global] 資料庫，可針對匯入量身打造潛在客戶清單。 然後，使用 [[!DNL Acxiom Prospecting Data Import]](/help/sources/connectors/data-partners/acxiom-prospecting-data-import.md) 從Acxiom將潛在客戶清單的來源聯結器傳回Real-Time CDP，並移除已知或轉換的客戶。

![行銷圖表可將第一方資料匯出至Acxiom，然後將潛在客戶資料匯回Real-Time CDP](/help/destinations/assets/catalog/data-partner/acxiom/marketing-workflow.png)

Acxiom擁有超過12,000個全球資料屬性的最大目錄，專門用於提供個人化體驗，提供業界表現最佳的對象。 運用高品質資料的無限組合，建立和發佈對象以滿足特定的行銷活動需求。

本教學課程提供建立 [!DNL Acxiom Prospect-Suppression] 使用Adobe Experience Platform使用者介面的目的地連線和資料流。 此聯結器是用來將資料傳遞至Acxiom潛在客戶服務，使用Amazon S3作為放置點。 開始將檔案匯出至Amazon S3放置點後，請聯絡您的Acxiom客戶代表。

![已選取Acxiom目的地的目的地目錄。](../../assets/catalog/data-partner/acxiom/image-destination-catalog.png)

## 使用案例 {#use-cases}

為了協助您更清楚瞭解您應如何及何時使用 [!DNL Acxiom Prospect-Suppression] 目的地，以下是Adobe Experience Platform客戶可以使用此目的地解決的範例使用案例。

### 為潛在客戶資料集建立隱藏清單 {#create-suppression-list}

行銷專業人員為了提高其外展策略的有效性，通常會建立隱藏清單。 此清單包括現有客戶和特定區段，以確保在鎖定目標的行銷活動中，將其排除在潛在客戶活動之外。 此策略方法有助於調整受眾、避免多餘的溝通，以及促成更聚焦且有效率的行銷工作。

例如，身為行銷人員，您可能想要根據您提供的細分和隱藏條件，將目標潛在客戶設定檔新增至行銷活動，以擴大行銷活動觸及範圍。

使用案例是透過結合目的地和來源聯結器來執行。

您一開始會使用此目的地聯結器匯出現有的客戶設定檔，以用作隱藏檔案。 這可確保不包含現有的客戶記錄。

Acxiom的服務會搜尋檔案、擷取檔案，並搭配其他選取條件使用，以及產生潛在客戶檔案。 然後您會使用相對應的 [[!DNL Acxiom Prospecting Data Import]](/help/sources/connectors/data-partners/acxiom-prospecting-data-import.md) 來源聯結器以將潛在客戶設定檔擷取到Adobe Real-Time CDP。

## 先決條件 {#prerequisites}

>[!IMPORTANT]
>
>* 若要連線到目的地，您需要 **[!UICONTROL 檢視目的地]** 和 **[!UICONTROL 管理目的地]**， **[!UICONTROL 啟用目的地]**， **[!UICONTROL 檢視設定檔]**、和 **[!UICONTROL 檢視區段]** [存取控制許可權](/help/access-control/home.md#permissions). 閱讀 [存取控制總覽](/help/access-control/ui/overview.md) 或聯絡您的產品管理員以取得必要許可權。
>* 要匯出 *身分*，您需要 **[!UICONTROL 檢視身分圖表]** [存取控制許可權](/help/access-control/home.md#permissions). <br> ![選取工作流程中反白顯示的身分名稱空間，以將對象啟用至目的地。](/help/destinations/assets/overview/export-identities-to-destination.png "選取工作流程中反白顯示的身分名稱空間，以將對象啟用至目的地。"){width="100" zoomable="yes"}

## 支援的對象 {#supported-audiences}

本節說明您可以將哪些型別的對象匯出至此目的地。

| 對象來源 | 支援 | 說明 |
|-----------------------------|-----------|---------------------------------------------------------------------------------------------------------------------|
| [!DNL Segmentation Service] | ✓ (A) | 透過Experience Platform產生的對象 [分段服務](../../../segmentation/home.md). |
| 自訂上傳 | x | 受眾 [已匯入](../../../segmentation/ui/overview.md#import-audience) 從CSV檔案Experience Platform為。 |

{style="table-layout:auto"}


## 匯出型別和頻率 {#export-type-frequency}

請參閱下表以取得目的地匯出型別和頻率的資訊。

| 項目 | 類型 | 附註 |
|------------------|--------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 匯出型別 | **[!UICONTROL 以設定檔為基礎]** | 您正在匯出區段的所有成員，以及所需的結構描述欄位（例如：電子郵件地址、電話號碼、姓氏），如 [目的地啟用工作流程](/help/destinations/ui/activate-batch-profile-destinations.md#select-attributes). |
| 匯出頻率 | **[!UICONTROL 批次]** | 批次目的地會以三、六、八、十二或二十四小時的增量將檔案匯出至下游平台。 深入瞭解 [批次檔案型目的地](/help/destinations/destination-types.md#file-based). |

{style="table-layout:auto"}

## 連線到目標 {#connect}

>[!IMPORTANT]
> 
>若要連線到目的地，您需要 **[!UICONTROL 檢視目的地]** 和 **[!UICONTROL 管理目的地]** [存取控制許可權](/help/access-control/home.md#permissions). 閱讀 [存取控制總覽](/help/access-control/ui/overview.md) 或聯絡您的產品管理員以取得必要許可權。

若要連線至此目的地，請遵循以下說明的步驟： [目的地設定教學課程](../../ui/connect-destination.md). 在目標設定工作流程中，填寫以下兩個區段中列出的欄位。

### 驗證目標 {#authenticate}

若要向目的地進行驗證，請填寫必填欄位並選取 **[!UICONTROL 連線到目的地]**.

若要在Experience Platform上存取貯體，您必須提供下列憑證的有效值：

| 認證 | 說明 |
|---------------|----------------------------------------------------------------------------------------------------------|
| S3存取金鑰 | 貯體的存取金鑰ID。 此值可取自 [!DNL Acxiom] 團隊。 |
| S3秘密金鑰 | 貯體的秘密金鑰ID。 此值可取自 [!DNL Acxiom] 團隊。 |
| 貯體名稱 | 這是您的貯體，檔案將在此共用。 此值可取自 [!DNL Acxiom] 團隊。 |

### 新帳戶

若要定義新的Acxiom Managed S3位置：

![新帳戶](../../assets/catalog/data-partner/acxiom/image-destination-new-account.png)

### 現有帳戶

已使用Acxiom Prospect-Suppression卡定義的帳戶將會出現在清單快顯視窗中，並且在選取時會提供帳戶的詳細資訊。  當您導覽至「 」，以下是UI的範例 **目的地** > **帳戶**；

![現有帳戶](../../assets/catalog/data-partner/acxiom/image-destination-account.png)

### 填寫目標詳細資訊 {#destination-details}

若要設定目的地的詳細資訊，請填寫下方的必填和選用欄位。 UI中欄位旁的星號表示該欄位為必填欄位。

![目的地詳細資料](../../assets/catalog/data-partner/acxiom/image-destination-details.png)

* **名稱（必要）**  — 要儲存目的地的名稱
* **說明**  — 目的地用途的簡短說明
* **貯體名稱（必要）** - S3上設定的Amazon S3貯體名稱
* **資料夾路徑（必要）**  — 如果使用儲存貯體中的子目錄，則必須定義路徑，或使用&#39;/&#39;來參照根路徑。
* **檔案型別**  — 選取匯出檔案應使用的格式Experience Platform。 目前，Acxiom處理所需的唯一檔案型別是CSV

>[!IMPORTANT]
>
>選取CSV選項時， *分隔符號*， *引號字元*， *逸出字元*， *空值*， *Null值*， *壓縮格式*、和 *包含資訊清單檔案* 將會顯示選項，以下檔案將更詳細地說明這些設定 [設定格式選項](../../ui/batch-destinations-file-formatting-options.md).

![CSV選項](../../assets/catalog/data-partner/acxiom/image-destination-csv-options.png)

### 啟用警示 {#enable-alerts}

您可以啟用警報以接收有關傳送到您目的地的資料流狀態的通知。 從清單中選取警報以訂閱接收有關資料流狀態的通知。 如需警示的詳細資訊，請參閱以下指南： [使用UI訂閱目的地警報](../../ui/alerts.md).

當您完成提供目的地連線的詳細資訊時，請選取「 」 **[!UICONTROL 下一個]**.

## 啟動此目標的對象 {#activate}

>[!IMPORTANT]
>
>* 若要啟用資料，您需要 **[!UICONTROL 檢視目的地]**， **[!UICONTROL 啟用目的地]**， **[!UICONTROL 檢視設定檔]**、和 **[!UICONTROL 檢視區段]** [存取控制許可權](/help/access-control/home.md#permissions). 閱讀 [存取控制總覽](/help/access-control/ui/overview.md) 或聯絡您的產品管理員以取得必要許可權。
>* 要匯出 *身分*，您需要 **[!UICONTROL 檢視身分圖表]** [存取控制許可權](/help/access-control/home.md#permissions). <br> ![選取工作流程中反白顯示的身分名稱空間，以將對象啟用至目的地。](/help/destinations/assets/overview/export-identities-to-destination.png "選取工作流程中反白顯示的身分名稱空間，以將對象啟用至目的地。"){width="100" zoomable="yes"}

讀取 [啟用對象資料至批次設定檔匯出目的地](/help/destinations/ui/activate-batch-profile-destinations.md) 以取得啟用此目的地對象的指示。

### 對應建議

處理需要名稱和位址元素，但並非所有元素都需要，提供儘可能多的內容以協助成功比對。  下表列出目標端的屬性，這些屬性用於Acxiom處理，可供客戶將設定檔屬性對應至。  這應視為建議，因為並非所有元素都是必要的，且來源值將取決於帳戶的需求。

| 目標欄位 | 來源說明 |
|--------------|-------------------------------------------------------------|
| 名稱 | Experience Platform中的person.name.fullName值。 |
| 名字 | Experience Platform中的person.name.firstName值。 |
| 姓氏 | Experience Platform中的person.name.lastName值。 |
| address1 | Experience Platform中的mailingAddress.street1值。 |
| address2 | Experience Platform中的mailingAddress.street2值。 |
| city | Experience Platform中的mailingAddress.city值。 |
| state | Experience Platform中的mailingAddress.state值。 |
| zip | Experience Platform的mailingAddress.postalCode值。 |

{style="table-layout:auto"}

>[!NOTE]
>
>以上未列出的其他欄位將會包含在匯出中，但會被Acxiom處理忽略。

## 檢閱您的資料流

在提交之前，請使用複查頁面來取得資料流的摘要

![請檢閱](../../assets/catalog/data-partner/acxiom/image-destination-review.png)

## 驗證資料匯出 {#exported-data}

若要確認資料是否已成功匯出，請檢查 [!DNL Amazon S3 Storage] 貯體，並確保匯出的檔案包含預期的設定檔母體。

## 後續步驟

依照本教學課程所述，您已成功建立資料流，以將批次資料從Experience Platform匯出至 [!DNL Acxiom] 受管理的S3位置。 您需要連絡您的Acxiom代表，提供帳戶名稱、檔案名稱和貯體路徑，以便設定處理。

## 資料使用與控管 {#data-usage-governance}

全部 [!DNL Adobe Experience Platform] 處理您的資料時，目的地符合資料使用原則。 如需如何操作的詳細資訊 [!DNL Adobe Experience Platform] 強制執行資料控管，讀取 [資料控管概觀](/help/data-governance/home.md).

## 其他資源 {#additional-resources}

*Acxiom對象資料與分發：* https://www.acxiom.com/customer-data/audience-data-distribution/
