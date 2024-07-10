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

[[!DNL Gainsight PX]](https://www.gainsight.com/product-experience/) 是一個產品體驗平台，可讓產品團隊瞭解使用者如何使用其產品、收集意見並建立應用程式內參與，例如產品逐步解說，以推動使用者上線和產品採用。

>[!IMPORTANT]
>
>目的地聯結器和檔案頁面是由 *Gainsight PX* 團隊。 如有任何查詢或更新要求，請直接聯絡他們： *`pxsupport@gainsight.com`*.

## 使用案例 {#use-cases}

為了協助您更清楚瞭解您應如何及何時使用 *Gainsight PX* 目的地，以下是Adobe Experience Platform客戶可以使用此目的地解決的範例使用案例。

### 鎖定應用程式內參與目標 {#targeting-in-app-engagements}

SaaS公司想要透過在Gainsight PX上建構的應用程式內指南與其客戶互動。 已在Adobe Experience Platform上建立接收此參與的受眾。 Gainsight PX目的地會接收受眾，並可在Gainsight PX環境中使用。

## 先決條件 {#prerequisites}

* 聯絡 [!DNL Gainsight] 支援團隊並要求為您的訂閱啟用外部區段功能。
* 使用，為您的PX訂閱產生OAuth密碼值。 **[!UICONTROL 產生新密碼]** 底部按鈕 [公司詳細資訊頁面](https://app.aptrinsic.com/settings/subscription)
  ![Gainsight PX中的「公司詳細資料」畫面會顯示「產生新密碼」按鈕](../../assets/catalog/analytics/gainsight-px/generate_oauth_secret.png)

## 支援的身分 {#supported-identities}

Gainsight PX支援下表所述的身分啟用。 進一步瞭解 [身分](../../../identity-service/features/namespaces.md).

| 目標身分 | 說明 |
|---|----|
| 識別ID | 可在Gainsight PX和Adobe Experience Platform中唯一識別使用者的常見使用者識別碼 |

{style="table-layout:auto"}

## 支援的對象 {#supported-audiences}

本節說明您可以將哪種型別的對象匯出至此目的地。

| 對象來源 | 支援 | 說明 |
|---|---|---|
| [!DNL Segmentation Service] | ✓ (A) | 透過Experience Platform產生的對象 [分段服務](../../../segmentation/home.md). |
| 自訂上傳 | X | 受眾 [已匯入](../../../segmentation/ui/audience-portal.md#import-audience) 從CSV檔案Experience Platform為。 |

{style="table-layout:auto"}

## 匯出型別和頻率 {#export-type-frequency}

請參閱下表以取得目的地匯出型別和頻率的資訊。

| 項目 | 類型 | 附註 |
|---|---|---|
| 匯出類型 | **[!UICONTROL 區段匯出]** | 您正在匯出某個對象的所有成員，而這些成員中都有用於的識別碼（名稱、電話號碼或其他）。 [!DNL Gainsight PX] 目的地。 |
| 匯出頻率 | **[!UICONTROL 串流]** | 串流目的地是「一律開啟」的API型連線。 當根據對象評估在Experience Platform中更新設定檔時，聯結器會將更新傳送至下游的目標平台。 深入瞭解 [串流目的地](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## 連線到目標 {#connect}

>[!IMPORTANT]
>
>若要連線到目的地，您需要 **[!UICONTROL 管理目的地]** [存取控制許可權](/help/access-control/home.md#permissions). 閱讀 [存取控制總覽](/help/access-control/ui/overview.md) 或聯絡您的產品管理員以取得必要許可權。

若要連線至此目的地，請遵循以下說明的步驟： [目的地設定教學課程](../../ui/connect-destination.md). 在目標設定工作流程中，填寫以下兩個區段中列出的欄位。

### 驗證目標 {#authenticate}

若要向目的地進行驗證，請填寫必填欄位並選取 **[!UICONTROL 連線到目的地]**.

![驗證熒幕擷圖](../../assets/catalog/analytics/gainsight-px/auth-screen.png)

* **[!UICONTROL 密碼]**：用來登入的密碼 [[!DNL Gainsight PX]](https://app.aptrinsic.com)
* **[!UICONTROL 使用者端ID]**：上的Gainsight PX訂閱ID [公司詳細資訊頁面](https://app.aptrinsic.com/settings/subscription)
* **[!UICONTROL 使用者端密碼]**：在「 」下方產生的OAuth機密 [公司詳細資訊頁面](https://app.aptrinsic.com/settings/subscription) 在 [!DNL Gainsight PX] UI。
* **[!UICONTROL 使用者名稱]**：用來登入的電子郵件 [[!DNL Gainsight PX]](https://app.aptrinsic.com) UI

### 填寫目標詳細資訊 {#destination-details}

若要設定目的地的詳細資訊，請填寫下方的必填和選用欄位。 UI中欄位旁的星號表示該欄位為必填欄位。

![Experience Platform使用者介面中的目的地詳細資訊畫面，顯示如何填寫名稱和說明欄位](../../assets/catalog/analytics/gainsight-px/destination_details.png)

* **[!UICONTROL 名稱]**：您日後可辨識此目的地的名稱。
* **[!UICONTROL 說明]**：可協助您日後識別此目的地的說明。

當您完成提供目的地連線的詳細資訊時，請選取「 」 **[!UICONTROL 下一個]**.

## 啟用此目的地的區段 {#activate}

>[!IMPORTANT]
>
>* 若要啟用資料，您需要 **[!UICONTROL 管理目的地]**， **[!UICONTROL 啟用目的地]**， **[!UICONTROL 檢視設定檔]**、和 **[!UICONTROL 檢視區段]** [存取控制許可權](/help/access-control/home.md#permissions). 閱讀 [存取控制總覽](/help/access-control/ui/overview.md) 或聯絡您的產品管理員以取得必要許可權。
>* 要匯出 *身分*，您需要 **[!UICONTROL 檢視身分圖表]** [存取控制許可權](/help/access-control/home.md#permissions). <br> ![選取工作流程中反白顯示的身分名稱空間，以將對象啟用至目的地。](/help/destinations/assets/overview/export-identities-to-destination.png "選取工作流程中反白顯示的身分名稱空間，以將對象啟用至目的地。"){width="100" zoomable="yes"}

讀取 [對串流區段匯出目的地啟用設定檔和區段](/help/destinations/ui/activate-segment-streaming-destinations.md) 以取得啟用此目的地的受眾區段的指示。

### 對應身分 {#map}

此目的地支援設定檔屬性和身分名稱空間的對應。 目標對應必須一律為 **[!UICONTROL 識別ID]** 身分名稱空間。

請參閱下列範例，深入瞭解如何設定對應。

#### 對應設定檔屬性 {#map-profile-attribute}

在以下範例中，來源欄位是XDM設定檔屬性，會對應至IDENTIFY_ID目標名稱空間。

![身分名稱空間範例對應畫面會顯示如何選取來源和目標值](../../assets/catalog/analytics/gainsight-px/mapping_attribute.png)

#### 對應身分名稱空間 {#map-identity-namespace}

在以下範例中，來源欄位是身分名稱空間(**[!UICONTROL ECID]**)對應至 **[!UICONTROL 識別ID]** 目標名稱空間。

![屬性範例對應畫面，顯示如何選取來源和目標值](../../assets/catalog/analytics/gainsight-px/mapping_identities.png)

## 匯出的資料/驗證資料匯出 {#exported-data}

分段資料會從Experience Platform串流至Gainsight PX。

區段中繼資料會顯示在 [!DNL Gainsight PX] UI。

![Gainsight PX中的區段清單畫面會顯示外部區段。](../../assets/catalog/analytics/gainsight-px/segment_metadata.png)

區段會籍資訊顯示在Audience Explorer畫面的「區段」標籤上。 [!DNL Gainsight PX] UI。

![Gainsight PX中的Audience Explorer畫面會顯示使用者的關聯區段。](../../assets/catalog/analytics/gainsight-px/PX_Segments.png)

## 資料使用與控管 {#data-usage-governance}

全部 [!DNL Adobe Experience Platform] 處理您的資料時，目的地符合資料使用原則。 如需如何操作的詳細資訊 [!DNL Adobe Experience Platform] 強制執行資料控管，讀取 [資料控管概觀](/help/data-governance/home.md).
