---
title: Google Ads連線
description: Google Ads (先前稱為Google AdWords)是一項線上廣告服務，可讓企業在各種文字搜尋、圖形顯示、YouTube影片和應用程式內行動顯示中按一下付費廣告。
exl-id: 7143f476-49a8-42aa-bfb4-b11fc2b8f5c3
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '952'
ht-degree: 2%

---

# [!DNL Google Ads]個連線

## 概觀 {#overview}

[!DNL Google Ads] （先前稱為[!DNL Google AdWords]）是一項線上廣告服務，可讓企業透過文字搜尋、圖形顯示、[!DNL YouTube]視訊和應用程式內行動顯示，依每次點按付費進行廣告。

## 目的地詳情 {#specifics}

請注意下列專屬於[!DNL Google Ads]目的地的詳細資料：

* 啟用的對象是以程式設計方式在[!DNL Google]平台中建立。
* [!DNL Experience Platform]目前不包含驗證成功啟用的測量量度。 請參考Google中的對象計數，以驗證整合併瞭解對象目標定位大小。

>[!IMPORTANT]
>
>如果您想要使用[!DNL Google Ads]建立您的第一個目的地，而且過去尚未在Experience Cloud ID服務(使用Audience Manager或其他應用程式)中啟用[ID同步功能](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/idsync.html?lang=zh-Hant)，請聯絡Adobe Consulting或客戶服務以啟用ID同步。 如果您先前在Audience Manager中設定Google整合，您設定的ID同步會傳遞至Experience Platform。

## 支援的身分 {#supported-identities}

[!DNL Google Ads]支援下表所述的身分啟用。

| 目標身分 | 說明 | 考量事項 |
|---|---|---|
| GAID | [!DNL Google Advertising ID] | 當您的來源身分是GAID名稱空間時，請選取此目標身分。 |
| IDFA | [!DNL Apple ID for Advertisers] | 當您的來源身分是IDFA名稱空間時，請選取此目標身分。 |
| AAM UUID | [Adobe Audience Manager [!DNL Unique User ID]](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/ids-in-aam.html?lang=zh-Hant)，也稱為[!DNL Device ID]。 Audience Manager與其互動的每個裝置相關聯的數字38位數裝置ID。 | Google使用[AAM UUID](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/ids-in-aam.html?lang=zh-Hant)來鎖定加州的使用者，並使用所有其他使用者的Google Cookie ID。 |
| [!DNL Google] Cookie ID | [!DNL Google] Cookie ID | [!DNL Google]使用此ID來鎖定加州以外的使用者。 |
| RIDA | Advertising的Roku ID。 此ID可唯一識別Roku裝置。 |  |
| MAID | Microsoft Advertising ID。 此ID可唯一識別執行Windows 10的裝置。 |  |
| Amazon Fire TV ID | 此ID可唯一識別Amazon Fire電視。 |  |

{style="table-layout:auto"}

## 支援的對象 {#supported-audiences}

本節說明您可以將哪些型別的對象匯出至此目的地。

| 對象來源 | 支援 | 說明 |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | 透過Experience Platform [細分服務](../../../segmentation/home.md)產生的對象。 |
| 自訂上傳 | ✓ | 對象[從CSV檔案匯入](../../../segmentation/ui/audience-portal.md#import-audience)至Experience Platform。 |

{style="table-layout:auto"}

## 匯出型別和頻率 {#export-type-frequency}

請參閱下表以取得目的地匯出型別和頻率的資訊。

| 項目 | 類型 | 附註 |
---------|----------|---------|
| 匯出類型 | **[!UICONTROL 對象匯出]** | 您正在將對象的所有成員匯出至Google目的地。 |
| 匯出頻率 | **[!UICONTROL 串流]** | 串流目的地是「一律開啟」的API型連線。 根據對象評估在Experience Platform中更新設定檔後，聯結器會立即將更新傳送至下游的目標平台。 深入瞭解[串流目的地](/help/destinations/destination-types.md#streaming-destinations)。 |

{style="table-layout:auto"}

## 先決條件 {#prerequisites}

### 現有[!DNL Google Ads]帳戶

>[!IMPORTANT]
>
> [!DNL Google]已棄用與協力廠商的新[!DNL Google Ads] Cookie整合。 若要執行下一節中的允許清單步驟，您必須與[!DNL Google Ads]現有整合。 因此，使用[!DNL Google Ads]的建議方法是設定[!DNL Google Customer Match]整合。 如需建立[!DNL Google Customer Match]整合的詳細資訊，請閱讀建立[[!DNL Google Customer Match]](./google-customer-match.md)連線的教學課程。

### 允許清單 {#allow-listing}

>[!NOTE]
>
>在Experience Platform中設定第一個[!DNL Google Ads]目的地前，必須先加入允許清單。 在建立目的地之前，請確定[!DNL Google]已完成下述允許清單程式。
>此規則的例外情況適用於[Audience Manager](https://experienceleague.adobe.com/docs/audience-manager/user-guide/aam-home.html?lang=zh-Hant)客戶。 如果您已經在Audience Manager中建立了與此Google目的地的連線，則不需要再次進行允許清單程式，您可以繼續後續步驟。

在Experience Platform中建立[!DNL Google Ads]目的地之前，您必須先聯絡[!DNL Google]，才能Adobe加入允許的資料提供者清單，並將您的帳戶新增至允許清單。 請連絡[!DNL Google]並提供下列資訊：

* **帳戶ID**： Adobe的帳戶ID與Google。 帳戶ID：87933855。
* **客戶ID**： Adobe的客戶帳戶ID與Google。 客戶ID：89690775。
* 您的帳戶型別： **AdWords**
* **Google AdWords ID**：這是您使用[!DNL Google]的ID。 ID格式通常為123-456-7890。

## 連線到目標 {#connect}

>[!IMPORTANT]
> 
>若要連線到目的地，您需要&#x200B;**[!UICONTROL 檢視目的地]**&#x200B;和&#x200B;**[!UICONTROL 管理目的地]** [存取控制許可權](/help/access-control/home.md#permissions)。 閱讀[存取控制總覽](/help/access-control/ui/overview.md)或連絡您的產品管理員以取得必要的許可權。

若要連線到此目的地，請依照[目的地組態教學課程](../../ui/connect-destination.md)中所述的步驟進行。

### 連線參數 {#parameters}

在[設定](../../ui/connect-destination.md)此目的地時，您必須提供下列資訊：

* **[!UICONTROL 名稱]**：填寫此目的地的偏好名稱。
* **[!UICONTROL 描述]**：選擇性。 例如，您可以提及要將此目的地用於哪個行銷活動。
* **[!UICONTROL 帳戶型別]**： AdWords是唯一可用的選項。
* **[!UICONTROL 帳戶ID]**：請使用[!DNL Google Ads]填入您的帳戶ID。 ID格式通常為123-456-7890。

### 啟用警示 {#enable-alerts}

您可以啟用警報以接收有關傳送到您目的地的資料流狀態的通知。 從清單中選取警報以訂閱接收有關資料流狀態的通知。 如需警示的詳細資訊，請參閱[使用UI訂閱目的地警示](../../ui/alerts.md)的指南。

當您完成提供目的地連線的詳細資訊後，請選取&#x200B;**[!UICONTROL 下一步]**。

## 啟動此目標的對象 {#activate}

>[!IMPORTANT]
> 
>若要啟用資料，您需要&#x200B;**[!UICONTROL 檢視目的地]**、**[!UICONTROL 啟用目的地]**、**[!UICONTROL 檢視設定檔]**&#x200B;和&#x200B;**[!UICONTROL 檢視區段]** [存取控制許可權](/help/access-control/home.md#permissions)。 閱讀[存取控制總覽](/help/access-control/ui/overview.md)或連絡您的產品管理員以取得必要的許可權。

如需啟用此目的地的對象的指示，請參閱[啟用串流對象匯出目的地的對象資料](../../ui/activate-segment-streaming-destinations.md)。

## 匯出的資料

若要確認資料是否已成功匯出至[!DNL Google Ads]目的地，請檢查您的[!DNL Google Ads]帳戶。 如果成功啟用，系統會將對象填入您的帳戶。

## 疑難排解 {#troubleshooting}

### 400錯誤請求錯誤訊息 {#bad-request}

設定此目的地時，您可能會收到下列錯誤：

`{"message":"Google Error: AuthorizationError.USER_PERMISSION_DENIED","code":"400 BAD_REQUEST"}`

當客戶帳戶不符合[必要條件](#prerequisites)或當客戶嘗試在沒有現有[!DNL Google Ads]帳戶的情況下設定目的地時，就會發生此錯誤。

[!DNL Google]已棄用與協力廠商的新[!DNL Google Ads] Cookie整合。 若要執行[允許清單](#allow-listing)步驟，您必須與[!DNL Google Ads]有現有的整合。

使用[!DNL Google Ads]的建議方法是設定[[!DNL Google Customer Match]](google-customer-match.md)整合。
