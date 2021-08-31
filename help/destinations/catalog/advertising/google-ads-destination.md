---
keywords: Google廣告；Google廣告；Google廣告；Google AdWords;Google AdWords
title: Google Ads連線
description: Google Ads（舊稱Google AdWords）是線上廣告服務，可讓企業在文字搜尋、圖形顯示、YouTube視訊和應用程式內行動顯示器間，按點付費廣告。
exl-id: 7143f476-49a8-42aa-bfb4-b11fc2b8f5c3
source-git-commit: f04ea9aed586c8582286de82bfeee3f6f04cc360
workflow-type: tm+mt
source-wordcount: '708'
ht-degree: 2%

---

# [!DNL Google Ads] 連接

## 概覽 {#overview}

[!DNL Google Ads](舊稱為 [!DNL Google AdWords])線上廣告服務，可讓企業在文字型搜尋、圖形顯示、視訊和應用程式內行動顯示器間， [!DNL YouTube] 依點按付費廣告。

## 目的地細節 {#specifics}

請注意下列特定於[!DNL Google Ads]目的地的詳細資訊：

* 在[!DNL Google]平台中以程式設計方式建立已啟用的對象。
* [!DNL Platform] 目前不包含驗證是否成功啟用的測量量度。請參考Google中的對象計數，以驗證整合併了解對象鎖定目標大小。

>[!IMPORTANT]
>
>如果您想使用[!DNL Google Ads]建立第一個目的地，而過去(透過Audience Manager或其他應用程式)未在Experience CloudID服務中啟用[ID同步功能](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/idsync.html)，請洽詢Adobe諮詢或客戶服務以啟用ID同步。 如果您先前已在Audience Manager中設定Google整合，則您設定的ID同步會持續到Platform。

## 支援的身分 {#supported-identities}

[!DNL Google Ad Manager] 支援啟用下表所述的身分。

| Target身分 | 說明 | 考量事項 |
|---|---|---|
| GAID | [!DNL Google Advertising ID] | 當源標識為GAID命名空間時，選擇此目標標識。 |
| IDFA | [!DNL Apple ID for Advertisers] | 當您的來源識別為IDFA命名空間時，請選取此目標識別。 |
| AAM UUID | [Adobe Audience Manager [!DNL Unique User ID]](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/ids-in-aam.html)，也稱為 [!DNL Device ID]。38位數的裝置ID,Audience Manager會與其互動的每個裝置建立關聯。 | Google使用[AAM UUID](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/ids-in-aam.html?lang=en)來鎖定加州的使用者，並將Google Cookie ID設為所有其他使用者。 |
| [!DNL Google] cookie ID | [!DNL Google] cookie ID | [!DNL Google] 使用此ID來鎖定加州以外的使用者。 |
| RIDA | 廣告專用的Roku ID。 此ID可唯一識別Roku裝置。 |  |
| 女傭 | Microsoft Advertising ID。 此ID可唯一識別執行Windows 10的裝置。 |  |
| Amazon Fire TV ID | 此ID可唯一識別Amazon Fire TV。 |  |

## 匯出類型 {#export-type}

**區段匯出**  — 您正在將區段（對象）的所有成員匯出至Google目的地。

## 先決條件 {#prerequisites}

### 現有[!DNL Google Ads]帳戶

>[!IMPORTANT]
>
> [!DNL Google] 已棄用與協 [!DNL Google Ads] 力廠商的新cookie整合。若要在下一節中執行允許清單步驟，您必須具備與[!DNL Google Ads]的現有整合。 因此，使用[!DNL Google Ads]的建議方法是設定[!DNL Google Customer Match]整合。 有關建立[!DNL Google Customer Match]整合的詳細資訊，請閱讀有關建立[[!DNL Google Customer Match]](./google-customer-match.md)連接的教程。

### 允許清單 {#allow-listing}

>[!NOTE]
>
>在Platform中設定您的第一個[!DNL Google Ads]目的地前，允許清單是必填的。 建立目標之前，請確保[!DNL Google]已完成下面所述的允許清單進程。

在Platform中建立[!DNL Google Ads]目的地之前，您必須聯絡[!DNL Google]，才能將Adobe加入允許的資料提供者清單中，並將您的帳戶新增至允許清單中。 聯繫[!DNL Google]並提供以下資訊：

* **帳戶ID**:Adobe的帳戶ID與Google。帳戶ID:87933855。
* **客戶ID**:Adobe的客戶帳戶ID與Google。客戶ID:89690775。
* 您的帳戶類型：**AdWords**
* **Google AdWords ID**:這是您的ID  [!DNL Google]。ID格式通常為123-456-7890。

## 連接到目標 {#connect}

要連接到此目標，請按照[目標配置教程](../../ui/connect-destination.md)中所述的步驟操作。

### 連線參數 {#parameters}

在[設定](../../ui/connect-destination.md)此目標時，您必須提供下列資訊：

* **[!UICONTROL 名稱]**:填寫此目的地的首選名稱。
* **[!UICONTROL 說明]**:選填。例如，您可以提及您使用此目的地的促銷活動。
* **[!UICONTROL 帳戶類型]**:AdWords是唯一可用的選項。
* **[!UICONTROL 帳戶ID]**:用填入您的帳戶ID  [!DNL Google Ads]。ID格式通常為123-456-7890。

## 啟用此目的地的區段 {#activate}

請參閱[對串流區段匯出目的地啟用受眾資料](../../ui/activate-segment-streaming-destinations.md) ，以取得對此目的地啟用受眾區段的指示。

## 匯出的資料

要驗證資料是否已成功導出到[!DNL Google Ads]目標，請檢查[!DNL Google Ads]帳戶。 如果啟動成功，則會在您的帳戶中填入對象。

## 疑難排解 {#troubleshooting}

### 400錯誤請求錯誤消息 {#bad-request}

設定此目的地時，您可能會收到下列錯誤：

`{"message":"Google Error: AuthorizationError.USER_PERMISSION_DENIED","code":"400 BAD_REQUEST"}`

當客戶帳戶不符合[必要條件](#prerequisites)時，或當客戶嘗試在沒有現有[!DNL Google Ads]帳戶的情況下配置目標時，即會發生此錯誤。

[!DNL Google] 已棄用與協 [!DNL Google Ads] 力廠商的新cookie整合。若要執行[allow-list](#allow-listing)步驟，您必須有與[!DNL Google Ads]的現有整合。

使用[!DNL Google Ads]的建議方法是設定[[!DNL Google Customer Match]](google-customer-match.md)整合。
