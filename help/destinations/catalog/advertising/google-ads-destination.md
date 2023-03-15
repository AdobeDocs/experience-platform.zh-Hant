---
keywords: Google廣告；Google廣告；Google Adwords;Google AdWords;Google Adwords
title: Google Ads連線
description: Google Ads(舊稱Google AdWords)是線上廣告服務，可讓企業在文字搜尋、圖形顯示、YouTube視訊和應用程式內行動顯示器間，按點付費廣告。
exl-id: 7143f476-49a8-42aa-bfb4-b11fc2b8f5c3
source-git-commit: 7d32499bec8d7248472ae60b07893dbb5496d984
workflow-type: tm+mt
source-wordcount: '939'
ht-degree: 2%

---

# [!DNL Google Ads] 連接

## 總覽 {#overview}

[!DNL Google Ads]，先前稱為 [!DNL Google AdWords]，是線上廣告服務，可讓企業透過文字型搜尋、圖形顯示、 [!DNL YouTube] 影片和應用程式內行動裝置顯示。

## 目的地細節 {#specifics}

請注意下列 [!DNL Google Ads] 目的地：

* 以程式設計方式在 [!DNL Google] 平台。
* [!DNL Platform] 目前不包含驗證是否成功啟用的測量量度。 請參考Google中的對象計數，以驗證整合併了解對象鎖定目標大小。

>[!IMPORTANT]
>
>如果您想要使用 [!DNL Google Ads] 並未啟用 [ID同步功能](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/idsync.html) 過去的Experience CloudID服務(含Audience Manager或其他應用程式)，請聯絡Adobe諮詢或客戶服務以啟用ID同步。 如果您先前已在Audience Manager中設定Google整合，則您設定的ID同步會持續到Platform。

## 支援的身分 {#supported-identities}

[!DNL Google Ad Manager] 支援啟用下表所述的身分。

| Target身分 | 說明 | 考量事項 |
|---|---|---|
| GAID | [!DNL Google Advertising ID] | 當源標識為GAID命名空間時，選擇此目標標識。 |
| IDFA | [!DNL Apple ID for Advertisers] | 當您的來源識別為IDFA命名空間時，請選取此目標識別。 |
| AAM UUID | [Adobe Audience Manager [!DNL Unique User ID]](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/ids-in-aam.html)，又稱為 [!DNL Device ID]. 38位數的裝置ID,Audience Manager會與其互動的每個裝置建立關聯。 | Google使用 [AAM UUID](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/ids-in-aam.html?lang=zh-Hant) 來鎖定加州的使用者，以及所有其他使用者的Google Cookie ID。 |
| [!DNL Google] cookie ID | [!DNL Google] cookie ID | [!DNL Google] 使用此ID來鎖定加州以外的使用者。 |
| RIDA | 廣告專用的Roku ID。 此ID可唯一識別Roku裝置。 |  |
| 女傭 | Microsoft Advertising ID。 此ID可唯一識別執行Windows 10的裝置。 |  |
| Amazon Fire TV ID | 此ID可唯一識別Amazon Fire TV。 |  |

{style="table-layout:auto"}

## 匯出類型和頻率 {#export-type-frequency}

有關目標導出類型和頻率的資訊，請參閱下表。

| 項目 | 類型 | 附註 |
---------|----------|---------|
| 匯出類型 | **[!UICONTROL 區段匯出]** | 您正在將區段（對象）的所有成員匯出至Google目的地。 |
| 匯出頻率 | **[!UICONTROL 串流]** | 串流目的地是「一律開啟」API型連線。 一旦根據區段評估在Experience Platform中更新設定檔，連接器就會將更新傳送至下游的目的地平台。 深入了解 [串流目的地](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## 先決條件 {#prerequisites}

### 現有 [!DNL Google Ads] 帳戶

>[!IMPORTANT]
>
> [!DNL Google] 已過時新 [!DNL Google Ads] cookie與協力廠商的整合。 若要在下一節中執行允許清單步驟，您必須與 [!DNL Google Ads]. 因此，建議使用 [!DNL Google Ads] 正在設定 [!DNL Google Customer Match] 整合。 如需建立 [!DNL Google Customer Match] 整合，請閱讀有關建立 [[!DNL Google Customer Match]](./google-customer-match.md) 連線。

### 允許清單 {#allow-listing}

>[!NOTE]
>
>在設定第一個 [!DNL Google Ads] 目標。 請確保以下所述的允許清單過程已由 [!DNL Google] 建立目的地之前。
>此規則的例外為 [Audience Manager](https://experienceleague.adobe.com/docs/audience-manager/user-guide/aam-home.html) 客戶。 如果您已Audience Manager建立連線至此Google目的地，則不需要再次執行允許清單程式，您可以繼續執行後續步驟。

建立之前 [!DNL Google Ads] 目的地，您必須聯絡 [!DNL Google] 讓Adobe列入允許的資料提供者清單，並讓您的帳戶新增至允許清單。 連絡人 [!DNL Google] 並提供下列資訊：

* **帳戶ID**:Adobe的帳戶ID與Google。 帳戶ID:87933855。
* **客戶ID**:Adobe的客戶帳戶ID與Google。 客戶ID:89690775。
* 您的帳戶類型： **AdWords**
* **Google AdWords ID**:這是您的ID，包含 [!DNL Google]. ID格式通常為123-456-7890。

## 連接到目標 {#connect}

>[!IMPORTANT]
> 
>若要連線至目的地，您需要 **[!UICONTROL 管理目的地]** [存取控制權限](/help/access-control/home.md#permissions). 閱讀 [存取控制概觀](/help/access-control/ui/overview.md) 或聯絡您的產品管理員以取得所需的權限。

若要連線至此目的地，請依照 [目的地設定教學課程](../../ui/connect-destination.md).

### 連線參數 {#parameters}

同時 [設定](../../ui/connect-destination.md) 此目的地時，您必須提供下列資訊：

* **[!UICONTROL 名稱]**:填寫此目的地的首選名稱。
* **[!UICONTROL 說明]**:選填。 例如，您可以提及您使用此目的地的促銷活動。
* **[!UICONTROL 帳戶類型]**:AdWords是唯一可用的選項。
* **[!UICONTROL 帳戶ID]**:以填入您的帳戶ID [!DNL Google Ads]. ID格式通常為123-456-7890。

### 啟用警報 {#enable-alerts}

您可以啟用警報，接收有關資料流到目標狀態的通知。 從清單中選擇要訂閱的警報，以接收有關資料流狀態的通知。 如需警報的詳細資訊，請參閱 [使用UI訂閱目的地警報](../../ui/alerts.md).

完成提供目標連接的詳細資訊後，請選擇 **[!UICONTROL 下一個]**.

## 啟用此目的地的區段 {#activate}

>[!IMPORTANT]
> 
>若要啟用資料，您需要 **[!UICONTROL 管理目的地]**, **[!UICONTROL 啟動目的地]**, **[!UICONTROL 檢視設定檔]**，和 **[!UICONTROL 檢視區段]** [存取控制權限](/help/access-control/home.md#permissions). 閱讀 [存取控制概觀](/help/access-control/ui/overview.md) 或聯絡您的產品管理員以取得所需的權限。

請參閱 [對串流區段匯出目的地啟用受眾資料](../../ui/activate-segment-streaming-destinations.md) 以取得啟用受眾區段至此目的地的指示。

## 匯出的資料

驗證資料是否已成功導出到 [!DNL Google Ads] 目的地，檢查 [!DNL Google Ads] 帳戶。 如果啟動成功，則會在您的帳戶中填入對象。

## 疑難排解 {#troubleshooting}

### 400錯誤請求錯誤消息 {#bad-request}

設定此目的地時，您可能會收到下列錯誤：

`{"message":"Google Error: AuthorizationError.USER_PERMISSION_DENIED","code":"400 BAD_REQUEST"}`

當客戶帳戶不符合 [必要條件](#prerequisites) 或當客戶嘗試設定目的地時，沒有現有 [!DNL Google Ads] 帳戶。

[!DNL Google] 已過時新 [!DNL Google Ads] cookie與協力廠商的整合。 若要執行 [allow-list](#allow-listing) 步驟中，您必須與 [!DNL Google Ads].

建議的使用方法 [!DNL Google Ads] 正在設定 [[!DNL Google Customer Match]](google-customer-match.md) 整合。
