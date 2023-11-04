---
keywords: linkedin連線；linkedin連線；linkedin目的地；linkedin；
title: Linkedin相符受眾連線
description: 根據雜湊電子郵件，為您的LinkedIn行銷活動啟用設定檔，以用於對象目標定位、個人化和隱藏。
exl-id: 74c233e9-161a-4e4a-98ef-038a031feff0
source-git-commit: 05e996f9e33e0d8be3d15a9ab3baaaf6d8152b5a
workflow-type: tm+mt
source-wordcount: '1103'
ht-degree: 4%

---

# [!DNL LinkedIn Matched Audiences] 連線

## 概觀 {#overview}

為您的啟動設定檔 [!DNL LinkedIn] 根據雜湊電子郵件和行動ID，針對對象鎖定目標、個人化和抑制的促銷活動。

![Adobe Experience Platform UI中的LinkedIn目的地](../../assets/catalog/social/linkedin/catalog.png)

## 使用案例

協助您更清楚瞭解使用的方法和時機 [!DNL LinkedIn Matched Audiences] 目的地，以下是Adobe Experience Platform客戶可使用此功能解決的使用案例。

軟體公司會組織會議並想要與參與者保持聯絡，並根據其會議出席狀態向他們顯示個人化優惠。 公司可從自己的電子郵件地址或行動裝置ID擷取 [!DNL CRM] 移入Adobe Experience Platform。 接著，他們可以從本身的離線資料建立對象，並將這些對象傳送至 [!DNL LinkedIn] 社交平台，最佳化廣告支出。

## 支援的身分 {#supported-identities}

[!DNL LinkedIn Matched Audiences] 支援下表所述的身分啟用。 進一步瞭解 [身分](/help/identity-service/namespaces.md).

| 目標身分 | 說明 | 考量事項 |
|---|---|---|
| GAID | Google廣告ID | 當您的來源身分是GAID名稱空間時，請選取此目標身分。 |
| IDFA | 廣告商適用的Apple ID | 當您的來源身分是IDFA名稱空間時，請選取此目標身分。 |
| email_lc_sha256 | 使用SHA256演演算法雜湊的電子郵件地址 | Adobe Experience Platform同時支援純文字和SHA256雜湊電子郵件地址。 請依照 [ID比對要求](#id-matching-requirements-id-matching-requirements) 區段，並針對純文字和雜湊電子郵件分別使用適當的名稱空間。 當來源欄位包含未雜湊屬性時，請核取 **[!UICONTROL 套用轉換]** 選項，擁有 [!DNL Platform] 啟動時自動雜湊資料。 |

{style="table-layout:auto"}

## 支援的對象 {#supported-audiences}

本節說明您可以將哪些型別的對象匯出至此目的地。

| 對象來源 | 支援 | 說明 |
---------|----------|----------|
| [!DNL Segmentation Service] | ✓ (A) | 透過Experience Platform產生的對象 [分段服務](../../../segmentation/home.md). |
| 自訂上傳 | ✓ | 受眾 [已匯入](../../../segmentation/ui/overview.md#import-audience) 從CSV檔案Experience Platform為。 |

{style="table-layout:auto"}

## 匯出型別和頻率 {#export-type-frequency}

請參閱下表以取得目的地匯出型別和頻率的資訊。

| 項目 | 類型 | 附註 |
---------|----------|---------|
| 匯出型別 | **[!UICONTROL 對象匯出]** | 您正在匯出某個對象的所有成員，而這些成員中都有用於的識別碼（名稱、電話號碼及其他）。 [!DNL LinkedIn Matched Audiences] 目的地。 |
| 匯出頻率 | **[!UICONTROL 串流]** | 串流目的地是「一律開啟」的API型連線。 一旦根據對象評估在Experience Platform中更新了設定檔，聯結器就會將更新傳送至下游的目的地平台。 深入瞭解 [串流目的地](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## linkedIn帳戶必要條件 {#LinkedIn-account-prerequisites}

開始使用 [!UICONTROL linkedIn相符的受眾] 目的地，確認您的 [!DNL LinkedIn Campaign Manager] 帳戶具有 [!DNL Creative Manager] 許可權層級或更高。

若要瞭解如何編輯您的 [!DNL LinkedIn Campaign Manager] 使用者許可權，請參閱 [新增、編輯和移除Advertising帳戶的使用者許可權](https://www.linkedin.com/help/lms/answer/5753) (位於LinkedIn檔案中)。

## ID比對要求 {#id-matching-requirements}

[!DNL LinkedIn Matched Audiences] 需要未明確傳送任何個人識別資訊(PII)。 因此，啟用的對象 [!DNL LinkedIn Matched Audiences] 鍵可關閉 *雜湊* 識別碼，例如電子郵件地址或行動裝置ID。

根據您擷取至Adobe Experience Platform的ID型別，您必須遵守其對應的要求。

## 電子郵件雜湊需求 {#email-hashing-requirements}

您可以將電子郵件地址雜湊再擷取至Adobe Experience Platform，或使用Experience Platform中清楚的電子郵件地址，並擁有 [!DNL Platform] 啟用時雜湊這些專案。

若要瞭解如何在Experience Platform中擷取電子郵件地址，請參閱 [批次擷取概觀](/help/ingestion/batch-ingestion/overview.md) 和 [串流擷取概觀](/help/ingestion/streaming-ingestion/overview.md).

如果您選擇自行雜湊電子郵件地址，請務必遵守下列要求：

* 修剪電子郵件字串中所有開頭和結尾的空格。 例如： `johndoe@example.com`，非 `<space>johndoe@example.com<space>`；
* 雜湊電子郵件字串時，請務必雜湊小寫字串；
   * 範例： `example@email.com`，非 `EXAMPLE@EMAIL.COM`；
* 確認雜湊字串全部為小寫
   * 範例： `55e79200c1635b37ad31a378c39feb12f120f116625093a19bc32fff15041149`，非 `55E79200C1635B37AD31A378C39FEB12F120F116625093A19bC32FFF15041149`；
* 請勿對字串執行Salt處理。

>[!NOTE]
>
>非雜湊名稱空間中的資料會自動透過雜湊處理 [!DNL Platform] 啟用時。
> 屬性來源資料不會自動雜湊。
> 
> 期間 [身分對應](../../ui/activate-segment-streaming-destinations.md#mapping) 步驟，當來源欄位包含未雜湊屬性時，請核取 **[!UICONTROL 套用轉換]** 選項，擁有 [!DNL Platform] 啟動時自動雜湊資料。
> 
> 此 **[!UICONTROL 套用轉換]** 選項只有在您選取屬性作為來源欄位時才會顯示。 選擇名稱空間時不會顯示。

![身分對應轉換](../../assets/ui/activate-destinations/identity-mapping-transformation.png)

## 連線到目標 {#connect}

>[!IMPORTANT]
> 
>若要連線到目的地，您需要 **[!UICONTROL 管理目的地]** [存取控制許可權](/help/access-control/home.md#permissions). 閱讀 [存取控制總覽](/help/access-control/ui/overview.md) 或聯絡您的產品管理員以取得必要許可權。

若要連線至此目的地，請遵循以下說明的步驟： [目的地設定教學課程](../../ui/connect-destination.md). 在設定目標工作流程中，填寫以下兩個區段中列出的欄位。

以下影片也會示範設定 [!DNL LinkedIn Matched Audiences] 目的地並啟用對象。

>[!VIDEO](https://video.tv.adobe.com/v/332599/?quality=12&learn=on&captions=eng)

>[!NOTE]
>
>Experience Platform使用者介面經常更新，自從錄製此影片後，該介面可能已經變更。 如需最新資訊，請參閱 [目的地設定教學課程](../../ui/connect-destination.md).

### 驗證目標 {#authenticate}

1. 尋找 [!DNL LinkedIn Matched Audiences] 目的地目錄中的目的地，然後選取 **[!UICONTROL 設定]**.
2. 選取 **[!UICONTROL 連線到目的地]**.
   ![向LinkedIn進行驗證](/help/destinations/assets/catalog/social/linkedin/authenticate-linkedin-destination.png)
3. 輸入您的LinkedIn認證，然後選取 **登入**.

### 填寫目標詳細資訊 {#destination-details}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_linkedin_accountid"
>title="帳戶 ID"
>abstract="您的 LinkedIn 行銷活動管理員帳戶 ID。您可以在您的 LinkedIn 行銷活動管理員帳戶中找到此 ID。"

若要設定目的地的詳細資訊，請填寫下方的必填和選用欄位。 UI中欄位旁的星號表示該欄位為必填欄位。

* **[!UICONTROL 名稱]**：您日後可辨識此目的地的名稱。
* **[!UICONTROL 說明]**：可協助您日後識別此目的地的說明。
* **[!UICONTROL 帳戶ID]**：您的 [!DNL LinkedIn Campaign Manager Account ID]. 此ID可在 [!DNL LinkedIn Campaign Manager] 帳戶。

### 啟用警示 {#enable-alerts}

您可以啟用警報以接收有關傳送到您目的地的資料流狀態的通知。 從清單中選取警報以訂閱接收有關資料流狀態的通知。 如需警示的詳細資訊，請參閱以下指南： [使用UI訂閱目的地警報](../../ui/alerts.md).

當您完成提供目的地連線的詳細資訊時，請選取「 」 **[!UICONTROL 下一個]**.

## 啟動此目標的對象 {#activate}

>[!IMPORTANT]
> 
>* 若要啟用資料，您需要 **[!UICONTROL 管理目的地]**， **[!UICONTROL 啟用目的地]**， **[!UICONTROL 檢視設定檔]**、和 **[!UICONTROL 檢視區段]** [存取控制許可權](/help/access-control/home.md#permissions). 閱讀 [存取控制總覽](/help/access-control/ui/overview.md) 或聯絡您的產品管理員以取得必要許可權。
>* 要匯出 *身分*，您需要 **[!UICONTROL 檢視身分圖表]** [存取控制許可權](/help/access-control/home.md#permissions). <br> ![選取工作流程中反白顯示的身分名稱空間，以將對象啟用至目的地。](/help/destinations/assets/overview/export-identities-to-destination.png "選取工作流程中反白顯示的身分名稱空間，以將對象啟用至目的地。"){width="100" zoomable="yes"}

另請參閱 [啟用受眾資料至串流受眾匯出目的地](../../ui/activate-segment-streaming-destinations.md) 以取得啟用此目的地對象的指示。

## 匯出的資料 {#exported-data}

成功啟用意味著 [!DNL LinkedIn] 自訂對象將以程式設計方式建立於 [[!DNL LinkedIn Campaign Manager]](https://www.linkedin.com/campaignmanager/login). 當使用者符合或不符合啟用的對象的資格時，將會新增及移除對象成員資格。

>[!TIP]
>
>Adobe Experience Platform與之間的整合 [!DNL LinkedIn Matched Audiences] 支援歷史對象回填。 所有歷史對象資格都會傳送至 [!DNL LinkedIn] 當您對目的地啟用對象時。
