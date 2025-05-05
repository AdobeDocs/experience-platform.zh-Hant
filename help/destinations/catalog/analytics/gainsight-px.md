---
title: Gainsight PX連線
description: 使用Gainsight PX目的地將分段資訊傳送到Gainsight PX平台。
last-substantial-update: 2024-02-20T00:00:00Z
exl-id: 0ca0d34f-f866-4f59-80f8-60198fbb86be
source-git-commit: c35b43654d31f0f112258e577a1bb95e72f0a971
workflow-type: tm+mt
source-wordcount: '890'
ht-degree: 2%

---

# Gainsight PX連線 {#gainsight-px}

## 概觀 {#overview}

[[!DNL Gainsight PX]](https://www.gainsight.com/product-experience/)是產品體驗平台，可讓產品團隊瞭解使用者如何使用其產品、收集意見回饋，以及建立應用程式內參與，例如產品逐步說明，以推動使用者上線和產品採用。

>[!IMPORTANT]
>
>目的地聯結器和檔案頁面是由&#x200B;*Gainsight PX*&#x200B;團隊建立和維護的。 若有任何查詢或更新要求，請直接透過&#x200B;*`pxsupport@gainsight.com`*&#x200B;連絡他們。

## 使用案例 {#use-cases}

為協助您更清楚瞭解您應如何及何時使用&#x200B;*Gainsight PX*&#x200B;目的地，以下是Adobe Experience Platform客戶可藉由使用此目的地解決的範例使用案例。

### 鎖定應用程式內參與目標 {#targeting-in-app-engagements}

SaaS公司想要透過在Gainsight PX上建構的應用程式內指南與其客戶互動。 已在Adobe Experience Platform上建立接收此參與的受眾。 Gainsight PX目的地會接收受眾，並可在Gainsight PX環境中使用。

## 先決條件 {#prerequisites}

* 請連絡[!DNL Gainsight]支援團隊，要求啟用您訂閱的外部區段功能。
* 使用位於[公司詳細資料頁面](https://app.aptrinsic.com/settings/subscription)底部的&#x200B;**[!UICONTROL 產生新密碼]**&#x200B;按鈕，為您的PX訂閱產生OAuth密碼值
  Gainsight PX中的![公司詳細資訊畫面顯示[產生新密碼]按鈕](../../assets/catalog/analytics/gainsight-px/generate_oauth_secret.png)

## 支援的身分 {#supported-identities}

Gainsight PX支援下表所述的身分啟用。 深入瞭解[身分](../../../identity-service/features/namespaces.md)。

| 目標身分 | 說明 |
|---|----|
| 識別ID | 可在Gainsight PX和Adobe Experience Platform中唯一識別使用者的常見使用者識別碼 |

{style="table-layout:auto"}

## 支援的對象 {#supported-audiences}

本節說明您可以將哪種型別的對象匯出至此目的地。

| 對象來源 | 支援 | 說明 |
|---|---|---|
| [!DNL Segmentation Service] | ✓ (A) | 透過Experience Platform[細分服務](../../../segmentation/home.md)產生的對象。 |
| 自訂上傳 | X | 對象[從CSV檔案匯入](../../../segmentation/ui/audience-portal.md#import-audience)至Experience Platform。 |

{style="table-layout:auto"}

## 匯出型別和頻率 {#export-type-frequency}

請參閱下表以取得目的地匯出型別和頻率的資訊。

| 項目 | 類型 | 附註 |
|---|---|---|
| 匯出類型 | **[!UICONTROL 區段匯出]** | 您正在匯出具有[!DNL Gainsight PX]目的地中所使用識別碼（名稱、電話號碼或其他）的對象的所有成員。 |
| 匯出頻率 | **[!UICONTROL 串流]** | 串流目的地是「一律開啟」的API型連線。 當根據對象評估在Experience Platform中更新設定檔時，聯結器會將更新傳送至下游的目標平台。 深入瞭解[串流目的地](/help/destinations/destination-types.md#streaming-destinations)。 |

{style="table-layout:auto"}

## 連線到目標 {#connect}

>[!IMPORTANT]
>
>若要連線到目的地，您需要&#x200B;**[!UICONTROL 管理目的地]** [存取控制許可權](/help/access-control/home.md#permissions)。 閱讀[存取控制總覽](/help/access-control/ui/overview.md)或連絡您的產品管理員以取得必要的許可權。

若要連線到此目的地，請依照[目的地組態教學課程](../../ui/connect-destination.md)中所述的步驟進行。 在目標設定工作流程中，填寫以下兩個區段中列出的欄位。

### 驗證目標 {#authenticate}

若要驗證到目的地，請填入必填欄位，然後選取&#x200B;**[!UICONTROL 連線到目的地]**。

![驗證熒幕擷圖](../../assets/catalog/analytics/gainsight-px/auth-screen.png)

* **[!UICONTROL 密碼]**：用來登入[[!DNL Gainsight PX]](https://app.aptrinsic.com)的密碼
* **[!UICONTROL 使用者端識別碼]**： [公司詳細資料頁面](https://app.aptrinsic.com/settings/subscription)上的Gainsight PX訂閱識別碼
* **[!UICONTROL 使用者端密碼]**： OAuth密碼產生於[!DNL Gainsight PX] UI中[公司詳細資料頁面](https://app.aptrinsic.com/settings/subscription)的底部。
* **[!UICONTROL 使用者名稱]**：用來登入[[!DNL Gainsight PX]](https://app.aptrinsic.com) UI的電子郵件

### 填寫目標詳細資訊 {#destination-details}

若要設定目的地的詳細資訊，請填寫下方的必填和選用欄位。 UI中欄位旁的星號表示該欄位為必填欄位。

![Experience Platform使用者介面中的目的地詳細資訊畫面，顯示如何填寫「名稱」和「說明」欄位](../../assets/catalog/analytics/gainsight-px/destination_details.png)

* **[!UICONTROL 名稱]**：您日後可辨識此目的地的名稱。
* **[!UICONTROL 描述]**：可協助您日後識別此目的地的描述。

當您完成提供目的地連線的詳細資訊後，請選取&#x200B;**[!UICONTROL 下一步]**。

## 啟用此目的地的區段 {#activate}

>[!IMPORTANT]
>
>* 若要啟用資料，您需要&#x200B;**[!UICONTROL 管理目的地]**、**[!UICONTROL 啟用目的地]**、**[!UICONTROL 檢視設定檔]**&#x200B;和&#x200B;**[!UICONTROL 檢視區段]** [存取控制許可權](/help/access-control/home.md#permissions)。 閱讀[存取控制總覽](/help/access-control/ui/overview.md)或連絡您的產品管理員以取得必要的許可權。
>* 若要匯出&#x200B;*身分*，您需要&#x200B;**[!UICONTROL 檢視身分圖表]** [存取控制許可權](/help/access-control/home.md#permissions)。<br> ![選取工作流程中反白的身分名稱空間，以啟用目的地的對象。](/help/destinations/assets/overview/export-identities-to-destination.png "選取工作流程中反白顯示的身分名稱空間，以啟用目的地的對象。"){width="100" zoomable="yes"}

閱讀[啟用串流區段匯出目的地的設定檔和區段](/help/destinations/ui/activate-segment-streaming-destinations.md)，以取得啟用此目的地的對象區段的指示。

### 對應身分 {#map}

此目的地支援設定檔屬性和身分名稱空間的對應。 目標對應必須一律為&#x200B;**[!UICONTROL IDENTIFY_ID]**&#x200B;身分名稱空間。

請參閱下列範例，深入瞭解如何設定對應。

#### 對應設定檔屬性 {#map-profile-attribute}

在以下範例中，來源欄位是XDM設定檔屬性，會對應至IDENTIFY_ID目標名稱空間。

![身分名稱空間範例對應畫面顯示如何選取來源和目標值](../../assets/catalog/analytics/gainsight-px/mapping_attribute.png)

#### 對應身分名稱空間 {#map-identity-namespace}

在下列範例中，來源欄位是對應至&#x200B;**[!UICONTROL IDENTIFY_ID]**&#x200B;目標名稱空間的身分名稱空間(**[!UICONTROL ECID]**)。

![屬性範例對應畫面顯示如何選取來源和目標值](../../assets/catalog/analytics/gainsight-px/mapping_identities.png)

## 匯出的資料/驗證資料匯出 {#exported-data}

分段資料會從Experience Platform串流至Gainsight PX。

區段中繼資料會顯示在[!DNL Gainsight PX] UI內的「區段」畫面中。

![Gainsight PX中的區段清單畫面顯示外部區段。](../../assets/catalog/analytics/gainsight-px/segment_metadata.png)

在[!DNL Gainsight PX] UI的Audience Explorer畫面的「區段」標籤上可看見區段會籍資訊。

Gainsight PX中的![Audience Explorer畫面會顯示使用者的相關區段。](../../assets/catalog/analytics/gainsight-px/PX_Segments.png)

## 資料使用與控管 {#data-usage-governance}

處理您的資料時，所有[!DNL Adobe Experience Platform]目的地都符合資料使用原則。 如需[!DNL Adobe Experience Platform]如何強制資料控管的詳細資訊，請閱讀[資料控管概觀](/help/data-governance/home.md)。
